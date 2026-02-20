# Docker Grundlagen

## Was ist Docker?

Docker ist ein **Containerisierungs-Tool**. Ein Container ist wie eine leichte virtuelle Maschine, aber viel kleiner:

```
Tradition: VM
┌──────────────────────┐
│ Hypervisor           │
├──────────────────────┤
│ VM OS (Linux)        │  ← Ganzes Betriebssystem
│ ├─ Libraries         │
│ ├─ Runtime           │
│ └─ App               │
└──────────────────────┘
→ Groß, langsam, ressourcenhungrig

Docker: Container
┌──────────────────────┐
│ Docker Engine        │
├──────────────────────┤
│ Libraries + Runtime  │  ← Nur nötigste (kein OS)
│ ├─ App               │
│ └─ Config            │
└──────────────────────┘
→ Klein, schnell, ressourceneffizient
```

## Installation

### Windows

1. **Docker Desktop** herunterladen von [docker.com](https://www.docker.com/products/docker-desktop)
2. Installieren
3. WSL 2 Integration aktivieren:
   - Docker Desktop starten
   - Settings → Resources → WSL Integration
   - "Enable integration with my default WSL distro" aktivieren
   - Ubuntu-24.04 auswählen
4. `wsl --shutdown` (um WSL neu zu starten)

```powershell
# Testen
docker --version
docker run hello-world
```

### Linux

```bash
# Ubuntu/Debian
sudo apt install docker.io

# Service starten
sudo systemctl start docker
sudo systemctl enable docker

# User zur docker group hinzufügen (um sudo zu vermeiden)
sudo usermod -aG docker $USER
# Logout und login wieder!

# Testen
docker --version
docker run hello-world
```

### macOS

1. **Docker Desktop** von [docker.com](https://www.docker.com/products/docker-desktop) herunterladen
2. Installieren
3. Terminal: `docker --version`

## Zentrale Konzepte

### Image

Ein **Image** ist ein Blueprint für einen Container:

- Enthält Betriebssystem, Libraries, Runtime, Code
- Read-only (unveränderbar)
- Mehrere Container können vom selben Image stammen
- Von **Docker Hub** oder eigenen Repositories

```bash
# Image anschauen
docker images

# Image herunterladen
docker pull ubuntu:24.04

# Image löschen
docker rmi ubuntu:24.04
```

### Container

Ein **Container** ist eine laufende Instanz eines Image:

- Read-write (veränderbar)
- Isoliert vom Host-System
- Kann gestartet, gestoppt, gelöscht werden

```bash
# Container starten
docker run -it ubuntu:24.04

# Container Liste
docker ps          # Laufende
docker ps -a       # Alle

# Container stoppen / löschen
docker stop container_name
docker rm container_name
```

### Dockerfile

Ein **Dockerfile** ist das "Rezept" zum Erstellen eines Custom Image:

```dockerfile
FROM ubuntu:24.04

RUN apt-get update && apt-get install -y openjdk-21-jdk maven

WORKDIR /app

COPY . .

RUN mvn clean package

ENTRYPOINT ["java", "-jar", "target/app.jar"]
```

Dann:
```bash
docker build -t my-app:1.0 .
docker run my-app:1.0
```

### Docker Compose

**Docker Compose** startet mehrere Container zusammen:

```yaml
version: '3'
services:
  app:
    build: .
    ports:
      - "8080:8080"

  database:
    image: postgres:15
    environment:
      POSTGRES_PASSWORD: secret
    volumes:
      - db-data:/var/lib/postgresql/data

volumes:
  db-data:
```

Dann:
```bash
docker-compose up      # Start alle Services
docker-compose down    # Stop alle Services
```

## Devcontainer

Ein **Devcontainer** ist ein Container für Entwicklung mit VSCode Integration.

Config: `.devcontainer/devcontainer.json`

```json
{
  "name": "Java 21",
  "image": "mcr.microsoft.com/devcontainers/java:1-21-bookworm",

  "features": {
    "ghcr.io/devcontainers/features/git:1": {}
  },

  "customizations": {
    "vscode": {
      "extensions": ["vscjava.vscode-java-pack"]
    }
  },

  "postCreateCommand": "mvn -q -DskipTests compile"
}
```

Dann in VSCode: **Dev Containers: Open in Container**

Vorteil: Jeder Developer hat die GLEICHE Umgebung, keine "works on my machine" Probleme!

## Workflow

```
1. Dockerfile schreiben (oder vorhandenes Image nutzen)
         ↓
2. docker build -t app:1.0 .
         ↓
3. docker run app:1.0
         ↓
4. Tests, Debugging, etc.
         ↓
5. docker push app:1.0 (zu Registry wie Docker Hub)
         ↓
6. Production: docker run app:1.0
```

## Wichtige Befehle

```bash
# Images
docker images                # Alle Images
docker pull ubuntu:24.04    # Herunterladen
docker build -t app:1.0 .   # Erstellen
docker push app:1.0         # Zu Registry pushen

# Container
docker ps -a                # Alle Container Liste
docker run -it app:1.0      # Starten (interaktiv)
docker run -d app:1.0       # Starten (Hintergrund)
docker stop container_id    # Stoppen
docker rm container_id      # Löschen

# Inspect & Debug
docker logs container_id    # Logs anschauen
docker exec -it container_id bash   # Shell in Container
docker inspect container_id # Details

# Docker Compose
docker-compose up           # Start Services
docker-compose down         # Stop Services
docker-compose logs         # Logs
```

## Tipps

- **Alpine Images** nutzen für kleinere Container (`FROM alpine:3.19`)
- **Multi-stage Builds** für optimierte Images
- **Volumes** für Datenpersistenz zwischen Container-Instanzen
- **Networks** um Container miteinander zu verbinden

Siehe auch: [Devcontainer Setup](Devcontainer.md), [Docker-Befehle](Befehle.md)
