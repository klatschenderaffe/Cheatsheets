# Cheatsheet Docker-Compose

## **Was ist Docker-Compose?**

Docker Compose ermöglicht es, mehrere Docker-Container mit einer einzigen Konfigurationsdatei (`docker-compose.yml`) zu definieren und zu orchestrieren. Mit einem einzigen Befehl lassen sich alle definierten Container starten, stoppen oder löschen. Dies erleichtert die Verwaltung komplexer Anwendungen, die aus mehreren Diensten bestehen.

---

## **Wie sieht eine Docker-Compose-Datei aus?**

```yaml
services:
  db:
    image: mongo
    container_name: db
    environment:
      - MONGO_INITDB_ROOT_USERNAME=admin
      - MONGO_INITDB_ROOT_PASSWORD=secret
    ports:
      - '27017:27017'
    networks:
      - todo

  backend:
    depends_on:
      - db
    container_name: backend
    build: ./todo-service
    image: backend
    environment:
      - DB_USER=admin
      - DB_PASSWORD=secret
      - DB_CONTAINER_NAME=db
      - DB_CONTAINER_PORT=27017
    ports:
      - '4000:4000'
    networks:
      - todo

  frontend:
    depends_on:
      - backend
      - db
    container_name: frontend
    build: ./todo-ui
    image: frontend
    ports:
      - '3000:3000'
    env_file:
      - ./todo-ui/.env.local
    networks:
      - todo

networks:
  todo:
    name: todo
    driver: bridge
```

Diese Konfiguration beschreibt eine Anwendung mit drei Diensten: einer Datenbank (`db`), einem Backend (`backend`) und einem Frontend (`frontend`). Alle Dienste sind über ein gemeinsames Netzwerk (`todo`) verbunden.

---

## **Abschnitte der Docker-Compose-Datei**

### **services**

Der Abschnitt `services` definiert die Container, die in der Anwendung gestartet werden sollen. In diesem Beispiel gibt es drei Dienste:

#### **1. db (Datenbank)**

- **image:** Verwendet das offizielle MongoDB-Image `mongo`.
- **container_name:** Der Container wird als `db` benannt.
- **environment:** Legt Umgebungsvariablen fest, um den MongoDB-Root-Benutzer und das Passwort zu konfigurieren.
  ```yaml
  MONGO_INITDB_ROOT_USERNAME=admin
  MONGO_INITDB_ROOT_PASSWORD=secret
  ```
- **ports:** Verbindet den Port `27017` des Containers mit dem gleichen Port auf dem Host.
- **networks:** Ordnet den Container dem Netzwerk `todo` zu.

#### **2. backend (Backend-Service)**

- **depends_on:** Gibt an, dass der Backend-Dienst erst startet, wenn der `db`-Dienst verfügbar ist.
- **container_name:** Der Container wird als `backend` benannt.
- **build:** Baut das Image aus dem Verzeichnis `./todo-service`.
- **image:** Der Name des erstellten Images ist `backend`.
- **environment:** Definiert Umgebungsvariablen für die Verbindung zur Datenbank.
  ```yaml
  DB_USER=admin
  DB_PASSWORD=secret
  DB_CONTAINER_NAME=db
  DB_CONTAINER_PORT=27017
  ```
- **ports:** Verbindet den Port `4000` des Containers mit dem gleichen Port auf dem Host.
- **networks:** Ordnet den Container dem Netzwerk `todo` zu.

#### **3. frontend (Frontend-Service)**

- **depends_on:** Gibt an, dass der Frontend-Dienst erst startet, wenn sowohl `backend` als auch `db` verfügbar sind.
- **container_name:** Der Container wird als `frontend` benannt.
- **build:** Baut das Image aus dem Verzeichnis `./todo-ui`.
- **image:** Der Name des erstellten Images ist `frontend`.
- **ports:** Verbindet den Port `3000` des Containers mit dem gleichen Port auf dem Host.
- **env_file:** Lädt Umgebungsvariablen aus einer Datei (`./todo-ui/.env.local`).
- **networks:** Ordnet den Container dem Netzwerk `todo` zu.

---

### **networks**

Der Abschnitt `networks` definiert Netzwerke, die von den Diensten verwendet werden können.

#### **todo**

- **name:** Das Netzwerk wird als `todo` benannt.
- **driver:** Verwendet den Standard-Netzwerktreiber `bridge`, der Container auf demselben Host miteinander verbindet.

---

## Zusammenfassung

Diese Docker-Compose-Datei beschreibt eine einfache Anwendung mit drei Diensten:

1. Eine MongoDB-Datenbank (`db`) für die Datenspeicherung.
2. Ein Backend-Service (`backend`), der mit der Datenbank kommuniziert.
3. Ein Frontend-Service (`frontend`), der Benutzern Zugriff auf die Anwendung bietet.

Alle Dienste sind über das gemeinsame Netzwerk `todo` verbunden und können so miteinander kommunizieren. Mit Docker Compose lässt sich diese gesamte Anwendung einfach starten, stoppen oder verwalten – alles basierend auf dieser einen Konfigurationsdatei!

## **Befehle**

Um die Docker-Compose-Datei auszuführen, navigiere im Terminal in das Verzeichnis, in dem sich die `docker-compose.yml`-Datei befindet. Verwende den folgenden Befehl, um die Container zu starten:

```bash
docker-compose up -d
```

- **`-d`**: Startet die Container im Hintergrund (detached mode), sodass das Terminal weiterhin für andere Aufgaben genutzt werden kann.
- **`--build`**: Nutze diesen Parameter, um vorhandene Images mit demselben Namen zu überschreiben und neu zu bauen. Dies ist nützlich, wenn Änderungen am Image vorgenommen wurden und diese aktualisiert werden müssen.

Um die Container zu stoppen und gleichzeitig zu entfernen, kannst du folgenden Befehl verwenden:

```bash
docker-compose down
```

Dieser Befehl beendet alle gestarteten Dienste und entfernt die zugehörigen Container sowie die Netzwerke, die von Docker Compose erstellt wurden.
