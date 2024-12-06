# Dockerfile Cheatsheet

## **Was ist eine Dockerfile?**

Eine _Dockerfile_ ist eine Art Bauanleitung für dein Docker-Image. Sie beschreibt Schritt für Schritt, welche Anweisungen der Befehl `docker buildx build` ausführen soll, um das gewünschte Image zu erstellen. Du kannst dir die Dockerfile wie eine Rezeptanleitung vorstellen, die alle notwendigen Schritte enthält, um deine Anwendung lauffähig zu machen.

## **Grundlegende Struktur**

Hier sind die wichtigsten Anweisungen einer Dockerfile und ihre Bedeutung:

- **`FROM <Basis-Image>`**  
  Gibt an, auf welcher Umgebung deine Anwendung basiert (z. B. `node:20-alpine` für Node.js). Dies ist die Grundlage deines Images.

- **`WORKDIR <Arbeitsverzeichnis>`**  
  Erstellt ein Arbeitsverzeichnis (Standard: `/app`) und wechselt in dieses Verzeichnis. Hier werden alle weiteren Befehle ausgeführt.

- **`COPY <Quelle> <Ziel>`**  
  Kopiert Dateien von deinem lokalen System in das Arbeitsverzeichnis im Container.  
  _Tipp:_ Kopiere zunächst nur die `package.json`, um unnötige Dateien zu vermeiden und den Build-Prozess zu beschleunigen. Verwende eine `.dockerignore`, um bestimmte Dateien auszuschließen.

- **`RUN <Befehl>`**  
  Führt einen Befehl während des Build-Prozesses aus. Zum Beispiel kannst du mit `RUN npm install` die Abhängigkeiten aus der `package.json` installieren.

- **`COPY . .`**  
  Kopiert den Rest deiner Dateien in das Arbeitsverzeichnis. Es werden nur Dateien kopiert, die noch nicht vorhanden sind. Solltest du eine `.dockerignore` File verwenden, könntest du die erste `COPY` Anweisung weglassen.

- **`EXPOSE <Port>`**  
  Gibt den Port an, den deine Anwendung verwendet (z. B. `3000`). Dies dient zur Dokumentation und als Hinweis für Tools wie Docker Compose.

- **`CMD ["<Befehl>", "<Argument>"]`**  
  Definiert den Startbefehl für den Container (z. B. `["node", "app.js"]`). Dieser wird erst beim Start des Containers ausgeführt, nicht während des Builds.

## **Beispiel einer vollständigen Dockerfile**

```dockerfile
FROM node:20-alpine

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 3000

CMD ["node", "app.js"]
```

Mit dieser Dockerfile erstellst du ein schlankes und effizientes Image für eine Node.js-Anwendung!
