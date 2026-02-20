# VSCode Extensions

## Automatische Installation

VSCode installiert viele Extensions automatisch, wenn du bestimmte Dateitypen oder Features nutzt:

- `.java` Dateien → Language Pack für Java wird automatisch installiert
- `.dockerfile` → Docker Extension
- `.git` → Git Integration

Viele davon werden auch automatisch im Remote-System installiert, wenn du über WSL oder einen Devcontainer arbeitest.

## Wichtige Extensions für diesen Kurs

### Git & Versionskontrolle

- **GitLens** — Erweiterte Git Integration
- **Git Graph** — Visualisierung des Commit-Graphen

### Java

- **Extension Pack for Java** (von Microsoft)
  - Language Support for Java (Red Hat)
  - Debugger for Java
  - Visual Studio IntelliCode

### Docker

- **Docker** (Microsoft) — Images, Container, Registry Management
- **Dev Containers** (Microsoft) — Devcontainer Support

### Produktivität

- **Prettier** — Code Formatter
- **ESLint** — Linting (auch für Java/Maven möglich)
- **Better Comments** — Highlighted Kommentare
- **TODO Highlight** — Hebt TODO/FIXME hervor

### Optional

- **Terminal** — Besseres Terminal Handling
- **Rainbow Brackets** — Farbliche Klammer-Highlights

## Extension im Devcontainer

Wenn du einen Devcontainer nutzt, wird die `.devcontainer.json` Datei bereits bestimmte Extensions definieren:

```json
"customizations": {
  "vscode": {
    "extensions": ["vscjava.vscode-java-pack"]
  }
}
```

Diese werden automatisch im Container installiert.

## Tipps

- Deaktiviere Extensions, die du nicht nutzt (Performance!)
- Im WSL können Extensions lokal (Windows) oder remote (WSL) laufen
- Schau in "Extensions" panel rechts oben → "Installed" um zu sehen was lädt
