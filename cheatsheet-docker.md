# Cheatsheet Docker Befehle

## Allgemeine Befehle

- `docker --help`: Zeigt eine Liste aller verfügbaren Docker-Befehle an.
- `docker version`: Zeigt die installierte Docker-Version an.
- `docker info`: Zeigt detaillierte Informationen über die Docker-Installation an.

## Image-Verwaltung

- `docker pull <image>`: Lädt ein Image aus einem Registry herunter.
- `docker buildx build -t <image_name> <path_to_dockerfile>` .: Erstellt ein neues Image aus einem Dockerfile.
- `docker images`: Listet alle lokal verfügbaren Images auf.
- `docker rmi <image>`: Entfernt ein Image.
- `docker image history <image_id>`: Die Geschichte des Images sehen.
- `docker image inspect <image_id>`: Informationen zu einem Image anzeigen.
- `docker image push <options> <NAME:TAG>`: Das Image auf Dockerhub publischen.

## Container-Verwaltung

- `docker run <image>`: Erstellt und startet einen neuen Container aus einem Image

  #### Optionen:

  - `-d`: Führt den Container im Hintergrund aus (detached mode).
  - `-p <host_port>:<container_port>`: Mappt Ports vom Host auf den Container.
  - `--name <container_name>`: Weist dem Container einen Namen zu.
  - `--rm`: Entfernt den Container nach Beendigung automatisch.
  - `-v <volumename>:<path>`: Volume an einen Container anhängen.
  - `--network`: Mit einem Netzwerk verbinden.
  - `sh -c "command"`: Öffne innerhalb des Containers eine Shell und führe folgenden Command aus. (-c = Command)
  - `-it`: Startet den Container im Interaktiven Modus.
  - `--restart <policy>`: Setzt eine Restart Policy.

- `docker ps`: Listet alle laufenden Container auf.
- `docker ps -a`: Listet alle Container auf, einschließlich gestoppter.
- `docker stop <container>`: Stoppt einen laufenden Container.
- `docker stop $(docker ps -q)`: Stoppt alle laufenden Container.
- `docker start <container>`: Startet einen gestoppten Container.
- `docker restart <container>`: Startet einen laufenden oder gestoppten Container neu.

## Erweiterte Container-Befehle

- `docker exec -it <container> <command>`: Führt einen Befehl in einem laufenden Container aus, z.B. eine Shell öffnen.
- `docker logs <container>`: Zeigt die Logs eines Containers an.
- `docker inspect <container>`: Zeigt detaillierte Informationen über einen Container an.
- `docker logs <container_id>`: Zeigt die Logs eines Containers.
- `docker rename <container_id> <new_container_name>`:Container umbenennen.
- `docker container port <container_id>`: Zeigt die gemappten Ports eines Containers an.

## Netzwerk

- `docker network ls`: Listet alle Docker-Netzwerke auf.
- `docker network create <network_name>`: Erstellt ein neues Netzwerk.

  ### Optionen:

  - `--gateway=<gateway>`: Fügt dem Netzwerk ein Gateway hinzu.
  - `--subnet=<subnet>`: Fügt dem Netzwerk ein Subnetz hinzu.
  - `--driver <driver>`: Fügt dem Netzwerk einen Treiber hinzu.

- `docker network inspect`: Details zu einem Netzwerk anzeigen.
- `docker network rm`: Netzwerk löschen.
- `docker network prune`: Löscht ungenutzte Netzwerke.
- `docker network connect <network> <container>`: Fügt dem Container ein Netzwerk hinzu.
- `docker network disconnect <network> <container>`: Entfernt einen Container einem Netzwerk.

## Volumes

- `docker volume ls`: Listet alle Docker-Volumes auf.
- `docker volume create <volumename>`: Neues Volume erstellen
- `docker volume rm <volume>`: Entfernt ein Volume.
- `docker volume inspect`: Details von den Volumes sehen.
-

## Bereinigung und Wartung

- `docker system prune`: Entfernt alle ungenutzten Daten wie gestoppte Container, ungenutzte Netzwerke und nicht referenzierte Images.
- `docker rm $(docker ps -a -q)`: Löscht alle gestoppten Container.
- `docker rm -f $(docker ps -a -q)`: Löscht alle Container.
- `docker rmi $(docker images -a -q)`: Löscht alle Images.

## Docker Hub

- `docker login -u <username>`: Login für Docker Hub.
- `docker push <username>/<image_name>`: Image publischen.
- `docker search <image_name>`: In Hub nach einem Image suchen.
