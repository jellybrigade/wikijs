# Entwicklungsumgebung

## VSCode und WSL

VSCode verbindet sich unter Windows über WSL (Windows Subsystem for Linux) mit einem Linux-Subsystem. Die Benutzeroberfläche läuft auf Windows, der Source Code und alle Tools liegen jedoch im Linux-Subsystem. Das ermöglicht eine einheitliche Entwicklungsumgebung unabhängig vom Host-Betriebssystem.

## Extensions

VSCode installiert viele Extensions automatisch, sobald sie benötigt werden — zum Beispiel die WSL-Extension beim Verbinden mit einem WSL-System oder das Java-Pack beim Arbeiten mit Java-Projekten.

## Devcontainer

Ein Devcontainer ist eine von Microsoft definierte Konfiguration auf Basis von Docker, die allen Entwicklern dieselbe Umgebung bietet. Die Konfiguration liegt in `.devcontainer/devcontainer.json`.

```json
{
  "name": "Java 21 (Lehrgang 1)",
  "image": "mcr.microsoft.com/devcontainers/java:1-21-bookworm",

  "features": {
    "ghcr.io/devcontainers/features/git:1": {},
    "ghcr.io/devcontainers/features/java:1": {
      "installMaven": true,
      "version": "21"
    }
  },

  "customizations": {
    "vscode": {
      "extensions": ["vscjava.vscode-java-pack"],
      "settings": {
        "java.configuration.updateBuildConfiguration": "automatic"
      }
    }
  },

  "postCreateCommand": "mvn -q -DskipTests compile",

  "remoteUser": "vscode"
}
```

`postCreateCommand` wird nach dem Erstellen des Containers einmalig ausgeführt — hier kompiliert Maven das Projekt automatisch.
