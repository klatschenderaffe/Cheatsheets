# Cheatsheet: **Dockerfile.prod**

## **Was ist die Dockerfile.prod?**

Die _Dockerfile.prod_ dient zur Unterscheidung zwischen Entwicklungs- und Produktionsumgebungen. Sie stellt sicher, dass unser Code auch in einer Produktionsumgebung, beispielsweise mit einem Webserver wie **nginx**, reibungslos funktioniert.

## **Beispiel einer Dockerfile.prod**

```dockerfile
# Multi-Stage Build
# Stage 1: Build-Umgebung

FROM node:20-alpine AS build

WORKDIR /app

COPY . .

RUN npm ci

RUN npm run build

# Stage 2: Produktionsumgebung

FROM nginx:stable-alpine

COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

### **Erklärung der Schritte**

1. **Stage 1: Build-Umgebung**

   - Wir verwenden ein leichtgewichtiges Node.js-Image (`node:20-alpine`), um den Build-Prozess auszuführen.
   - Der Arbeitsordner wird auf `/app` gesetzt.
   - Der gesamte Quellcode wird in das Image kopiert.
   - Mit `npm ci` werden die Abhängigkeiten installiert, und mit `npm run build` wird ein optimierter _Build-Ordner_ erstellt, der die Anwendung kompakt zusammenfasst.

2. **Stage 2: Produktionsumgebung**
   - Hier nutzen wir ein schlankes nginx-Image (`nginx:stable-alpine`) als Webserver.
   - Der zuvor erstellte _Build-Ordner_ wird in das Verzeichnis `/usr/share/nginx/html` kopiert, wo nginx die Dateien hostet.
   - Der Port `80` wird geöffnet, damit die Anwendung erreichbar ist.
   - Mit dem Befehl `CMD ["nginx", "-g", "daemon off;"]` wird nginx im Vordergrund ausgeführt.
