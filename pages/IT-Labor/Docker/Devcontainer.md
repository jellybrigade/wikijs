# Devcontainer für VSCode

## Was ist ein Devcontainer?

Ein **Devcontainer** ist ein Docker Container speziell für die Entwicklung mit VSCode:

- Konsistente Entwicklungsumgebung für das ganze Team
- Keine "works on my machine" Probleme
- Alle Tools und Dependencies sind im Container
- VSCode lädt Extensions automatisch in den Container

## Vorteile

```
Ohne Devcontainer:
┌─────────────────────────────────────┐
│ Developer 1: Windows, Java 21, IDE  │
│ Developer 2: macOS, Java 20, IDE    │  ← Unterschiedlich!
│ Developer 3: Linux, Java 21, IDE    │
│ Result: Bugs auf anderen Systemen!  │
└─────────────────────────────────────┘

Mit Devcontainer:
┌─────────────────────────────────────┐
│ Alle:                               │
│ Debian 12, Java 21, Maven 3.9, ...  │  ← Gleich!
│ Result: Konsistenz, keine Überraschungen!
└─────────────────────────────────────┘
```

## Struktur

```
project/
├── .devcontainer/
│   ├── devcontainer.json         ← Hauptkonfiguration
│   ├── Dockerfile                ← Custom Image (optional)
│   └── docker-compose.yml        ← Mehrere Services (optional)
├── src/
├── pom.xml
└── README.md
```

## devcontainer.json

Basis-Beispiel:

```json
{
  "name": "Java 21 Entwicklung",
  "image": "mcr.microsoft.com/devcontainers/java:1-21-bookworm",

  "features": {
    "ghcr.io/devcontainers/features/git:1": {},
    "ghcr.io/devcontainers/features/github-cli:1": {}
  },

  "customizations": {
    "vscode": {
      "extensions": [
        "vscjava.vscode-java-pack",
        "GitLens.gitlens"
      ],
      "settings": {
        "java.configuration.updateBuildConfiguration": "automatic",
        "editor.defaultFormatter": "esbenp.prettier-vscode"
      }
    }
  },

  "postCreateCommand": "mvn -q -DskipTests compile",

  "remoteUser": "vscode",

  "forward": [
    8080,     // Ports freigeben für Localhost
    3000
  ]
}
```

### Felder erklären

| Feld | Bedeutung |
|------|-----------|
| `name` | Name des Containers (für Anzeige) |
| `image` | Docker Image, auf dem Container basiert |
| `features` | Zusätzliche Tools (Git, GitHub CLI, etc.) |
| `customizations` | IDE-spezifische Einstellungen |
| `extensions` | VSCode Extensions die automatisch installiert werden |
| `postCreateCommand` | Befehl der nach Container-Erstellung läuft |
| `remoteUser` | User im Container der VSCode nutzt |
| `forward` | Ports die zu Localhost gemappt werden |

## Mit Custom Dockerfile

Wenn du ein Custom Docker Image brauchst:

`.devcontainer/Dockerfile`:
```dockerfile
FROM mcr.microsoft.com/devcontainers/java:1-21-bookworm

# Zusätzliche Tools installieren
RUN apt-get update && apt-get install -y \
    curl \
    wget \
    git

# Custom Konfiguration
ENV MAVEN_VERSION=3.9.0
```

`.devcontainer/devcontainer.json`:
```json
{
  "name": "Java 21 Custom",
  "build": {
    "dockerfile": "Dockerfile",
    "context": "."
  }
  // rest wie zuvor
}
```

## Mit Docker Compose

Für mehrere Services (App + Database):

`.devcontainer/docker-compose.yml`:
```yaml
version: '3'

services:
  app:
    build: ..
    volumes:
      - ..:/workspace
    working_dir: /workspace
    command: sleep infinity   # Container läuft endlos

  postgres:
    image: postgres:15
    environment:
      POSTGRES_PASSWORD: devpass
    volumes:
      - postgres-data:/var/lib/postgresql/data

volumes:
  postgres-data:
```

`.devcontainer/devcontainer.json`:
```json
{
  "name": "Java + Postgres",
  "dockerComposeFile": "docker-compose.yml",
  "service": "app",
  "workspaceFolder": "/workspace",

  "customizations": {
    "vscode": {
      "extensions": ["vscjava.vscode-java-pack"]
    }
  }
}
```

## VSCode Integration

### Container öffnen

1. VSCode Command Palette (`Strg+Shift+P`)
2. Tippe: "Dev Containers: Open in Container"
3. Warte bis Container gebaut ist
4. VSCode lädt automatisch Extensions nach

### Arbeitsablauf

```
Projekt öffnen
    ↓
VSCode: "Dev Containers: Reopen in Container"
    ↓
Container wird gebaut (einmalig)
    ↓
VSCode verbindet sich zu Container
    ↓
Du schreibst Code wie normal, aber in Container
    ↓
Extensions sind im Container installiert
    ↓
Terminal commands laufen im Container
```

### Hinweise

- Erste Erstellung dauert länger (Image Download + Build)
- Danach ist es schnell (Cache)
- Container persistiert bis du ihn löschst
- Source Code ist im Container, nicht auf Windows!

## Best Practices

1. **Immer .devcontainer nutzen** für Team-Projekte
2. **In Git committen**: `.devcontainer/` sollte im Repo sein
3. **Dokumentieren**: Welche Ports? Welche Datenbanken?
4. **Ausreichend Ressourcen**: Docker Desktop RAM auf 4GB+ stellen
5. **Tests in Container laufen lassen**: `postCreateCommand`

## Troubleshooting

| Problem | Lösung |
|---------|--------|
| Container lädt Extensions nicht | `remoteUser` ist falsch gesetzt |
| Port-Mapping funktioniert nicht | `forward` in devcontainer.json prüfen |
| Zu langsam | Docker ressourcen erhöhen (Settings) |
| Container stuck | VSCode neustarten oder `docker-compose down` |
| Git funktioniert nicht | `features` Git einführen: `"ghcr.io/devcontainers/features/git:1"` |

## Beispiel Repository

```
.devcontainer/
  ├── devcontainer.json
  ├── Dockerfile (optional)
  └── docker-compose.yml (optional)
src/
  └── main/
      └── java/
          └── Main.java
pom.xml
README.md
.git/
.gitignore
.gitattributes
```

## Ressourcen

- [Microsoft Devcontainer Spec](https://containers.dev/)
- [Devcontainer Image Repository](https://github.com/devcontainers/images)
- [VSCode Remote Development](https://code.visualstudio.com/docs/remote/remote-overview)

Siehe auch: [Docker Grundlagen](Grundlagen.md)
