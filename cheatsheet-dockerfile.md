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

## **Erweiterungsmöglichkeiten**

Es gibt verschiedene Möglichkeiten, die Arbeit mit einer Dockerfile zu vereinfachen und Fehler, wie beispielsweise Tippfehler, zu vermeiden.

- **`ENV <key=value>`**: Wenn du mit Umgebungsvariablen arbeitest, kannst du diese direkt in der Dockerfile definieren und abrufen. Das erleichtert die Konfiguration und macht deine Dockerfile flexibler. Ein Beispiel für die Verwendung von Umgebungsvariablen, etwa für die Festlegung eines Ports, sieht so aus:

  ```dockerfile
  ...
  ENV PORT=1234

  EXPOSE $PORT
  ...
  ```

  Wenn du jedoch beim Starten des Containers eine andere Portnummer übergibst, wird die in der Dockerfile definierte Variable überschrieben. Dies geschieht durch den Einsatz des `--env` Flags im `docker run` Befehl. Ein Beispiel:

  ```bash
  docker run -d --env PORT=4000 -p 3000:4000 <imagename>
  ```

  In diesem Fall wird der Port der Anwendung auf `4000` gesetzt, obwohl in der Dockerfile ursprünglich `1234` definiert war.

- **Code-Anpassung für Umgebungsvariablen**: Damit die Umgebungsvariable auch im Code verwendet werden kann, musst du sicherstellen, dass an der entsprechenden Stelle auf die Variable zugegriffen wird. In JavaScript oder Node.js kannst du beispielsweise den Port wie folgt abrufen:

  ```javascript
  const port = process.env.PORT || 3000;

  app.listen(port, () => {
    console.log(`Server läuft auf Port ${port}`);
  });
  ```

  Hier wird `process.env.PORT` genutzt, um den Wert der Umgebungsvariablen abzurufen. Falls keine Umgebungsvariable gesetzt ist, wird ein Standardwert (in diesem Fall `3000`) verwendet.
