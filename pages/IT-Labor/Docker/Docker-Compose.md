# Dockerfile & docker-compose.yml

## Dockerfile

Ein **Dockerfile** ist eine Textdatei mit Anweisungen zum Erstellen eines Docker Image.

### Struktur

```dockerfile
# 1. Base Image
FROM ubuntu:24.04

# 2. Metadaten
LABEL author="Dein Name" version="1.0"

# 3. Dependencies installieren
RUN apt-get update && apt-get install -y \
    openjdk-21-jdk \
    maven \
    git

# 4. Arbeitsordner setzen
WORKDIR /app

# 5. Dateien kopieren
COPY . .

# 6. Build-Befehle
RUN mvn clean package

# 7. Ports freigeben (Dokumentation)
EXPOSE 8080

# 8. Umgebungsvariablen
ENV JAVA_OPTS="-Xmx512m"

# 9. Startbefehl
ENTRYPOINT ["java", "-jar", "target/app.jar"]
```

### Befehle im Dockerfile

| Befehl | Bedeutung |
|--------|-----------|
| `FROM` | Base Image (muss zuerst) |
| `RUN` | Befehl im Container ausführen |
| `COPY` | Datei vom Host in Container |
| `ADD` | Wie COPY, aber mit Extras (tar-Entpackung) |
| `WORKDIR` | Arbeitsordner (wie `cd`) |
| `EXPOSE` | Port-Dokumentation (kein Mapping!) |
| `ENV` | Umgebungsvariable setzen |
| `ARG` | Build-Zeit Argument |
| `ENTRYPOINT` | Hauptbefehl beim Start |
| `CMD` | Default-Befehl (überschreibbar) |
| `VOLUME` | Persistenter Speicher |
| `USER` | User der Commands ausführt |

### Beispiel: Java App

```dockerfile
# Stage 1: Build
FROM maven:3.9-eclipse-temurin-21 as builder

WORKDIR /build
COPY . .
RUN mvn clean package -DskipTests

# Stage 2: Runtime (Multi-stage Build)
FROM eclipse-temurin:21-jre-alpine

WORKDIR /app
COPY --from=builder /build/target/app.jar .

EXPOSE 8080

ENTRYPOINT ["java", "-Xmx256m", "-jar", "app.jar"]
```

**Warum Multi-stage?**
- Builder Image groß (IDE, Maven, Compiler)
- Runtime Image klein (nur JRE, App)
- Finale Größe optimiert

### Building

```bash
# Image bauen
docker build -t myapp:1.0 .

# Mit Build-Argument
docker build -t myapp:1.0 --build-arg JAVA_VERSION=21 .

# Ohne Cache (fresh build)
docker build --no-cache -t myapp:1.0 .

# Mit Dockerfile an anderer Stelle
docker build -f path/to/Dockerfile -t myapp:1.0 .
```

## docker-compose.yml

**Docker Compose** orchestriert mehrere Container zusammen.

### Struktur

```yaml
version: '3.8'

services:
  # Service 1: Die Anwendung
  app:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: myapp
    ports:
      - "8080:8080"      # Host:Container
    environment:
      - DB_HOST=postgres
      - DB_USER=postgres
      - DB_PASSWORD=secret
    depends_on:
      - postgres
    volumes:
      - ./src:/app/src    # Host:Container (Live-Code)
      - ./target:/app/target
    networks:
      - app-network
    restart: unless-stopped

  # Service 2: Datenbank
  postgres:
    image: postgres:15-alpine
    container_name: myapp-db
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: secret
      POSTGRES_DB: myapp_db
    volumes:
      - postgres_data:/var/lib/postgresql/data
    ports:
      - "5432:5432"      # Für lokale Zugriffe optional
    networks:
      - app-network
    restart: unless-stopped

networks:
  app-network:
    driver: bridge

volumes:
  postgres_data:
    driver: local
```

### Felder erklären

| Feld | Bedeutung |
|------|-----------|
| `version` | Compose Format Version |
| `services` | Container die gestartet werden |
| `build` | Dockerfile zum Bauen |
| `image` | Fertig-Image von Docker Hub |
| `ports` | Port-Mapping |
| `environment` | Umgebungsvariablen |
| `depends_on` | Abhängigkeit zwischen Services |
| `volumes` | Daten-Persistenz oder Mounting |
| `networks` | Container-Networking |
| `restart` | Restart-Policy |

### Volumes

Volumes speichern Daten persistent:

```yaml
volumes:
  # Named Volume (Docker managed)
  postgres_data:
    driver: local

services:
  postgres:
    volumes:
      - postgres_data:/var/lib/postgresql/data   # Daten bleiben
```

```bash
# Volumes anschauen
docker volume ls
docker volume inspect postgres_data

# Volume löschen
docker volume rm postgres_data
```

### Networks

Containers können sich über ihren Namen erreichen:

```yaml
networks:
  app-network:
    driver: bridge

services:
  app:
    networks:
      - app-network
  postgres:
    networks:
      - app-network
```

```bash
# App kann Postgres so erreichen:
# jdbc:postgresql://postgres:5432/myapp_db
#                   ^^^^^^^^ = Service name
```

## Befehle

```bash
# Services starten
docker-compose up

# Hintergrund
docker-compose up -d

# Mit Rebuild
docker-compose up --build

# Logs anschauen
docker-compose logs
docker-compose logs -f app    # Folgen (tail -f)

# Services stoppen
docker-compose stop

# Komplett runter (Container weg, aber Volumes bleiben)
docker-compose down

# Mit Volumes löschen
docker-compose down -v

# Services Status
docker-compose ps

# Befehl in Service ausführen
docker-compose exec app bash
docker-compose exec postgres psql -U postgres

# Rebuild Image
docker-compose build
```

## Best Practices

### 1. Alpine Images für kleine Größe

```dockerfile
FROM alpine:3.19    # ~5MB statt 100+MB
```

### 2. Caching nutzen (spezifisch zu allgemein)

```dockerfile
COPY pom.xml .           # Separat
RUN mvn dependency:resolve
COPY . .                 # Erst dann
```

### 3. Multi-stage Builds für Größe

Reduziere finale Image-Größe durch Separation von Build und Runtime.

### 4. .dockerignore nutzen

```
.git
.idea
target/
.DS_Store
node_modules/
```

### 5. Environment Variablen für Config

```yaml
environment:
  - APP_ENV=production
  - LOG_LEVEL=info
```

## Beispiel: Java + PostgreSQL

**Dockerfile**:
```dockerfile
FROM maven:3.9-eclipse-temurin-21 as builder
WORKDIR /build
COPY . .
RUN mvn clean package -DskipTests

FROM eclipse-temurin:21-jre-alpine
WORKDIR /app
COPY --from=builder /build/target/*.jar app.jar
EXPOSE 8080
CMD ["java", "-jar", "app.jar"]
```

**docker-compose.yml**:
```yaml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "8080:8080"
    environment:
      - SPRING_DATASOURCE_URL=jdbc:postgresql://db:5432/mydb
      - SPRING_DATASOURCE_USERNAME=user
      - SPRING_DATASOURCE_PASSWORD=pass
    depends_on:
      - db

  db:
    image: postgres:15-alpine
    environment:
      POSTGRES_DB: mydb
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
    volumes:
      - db_data:/var/lib/postgresql/data

volumes:
  db_data:
```

Starten:
```bash
docker-compose up --build
```

Dann: http://localhost:8080

Siehe auch: [Docker Grundlagen](Grundlagen.md), [Devcontainer](Devcontainer.md)
