# VSCode Remote Development & WSL

## Das Konzept

VSCode kann sich in verschiedene "Remote"-Umgebungen verbinden:

- **WSL (Windows Subsystem for Linux)**: Entwicklung im Linux-Subsystem von Windows
- **Docker Container**: Entwicklung in isolierten Containern
- **SSH**: Entwicklung auf entfernten Servern

Der große Vorteil: Die UI läuft auf deinem lokalen System, aber der Code und die Tools laufen im Remote-System.

## Windows + WSL

### Installation

1. **WSL 2 aktivieren**
   ```powershell
   wsl --install
   # oder manuell:
   # Systemsteuerung → Windows-Features → "Windows-Subsystem für Linux" aktivieren
   ```

2. **Ubuntu 24.04 LTS in WSL installieren**
   ```powershell
   wsl --install -d Ubuntu-24.04
   ```

3. **VSCode mit WSL Extension**
   - Remote - WSL Extension in VSCode installieren
   - `Strg+Shift+P` → "Remote-WSL: New Window" → öffnet VSCode in WSL

4. **Docker mit WSL Integration**
   - Docker Desktop installieren
   - Settings → Resources → WSL Integration
   - "Enable integration with my default WSL distro" aktivieren
   - Deine WSL Distro auswählen (Ubuntu-24.04)

### Workflow

```
┌─────────────────────────────────────────┐
│ Windows (UI, Explorer, Editor)          │
│ ┌─────────────────────────────────────┐ │
│ │ VSCode                              │ │
│ │ (Remote - WSL verbunden)            │ │
│ └─────────────────────────────────────┘ │
└────────────────┬────────────────────────┘
                 │ (WSL Remote Protocol)
                 │
┌────────────────▼────────────────────────┐
│ WSL (Linux Subsystem)                   │
│ ├─ Git                                  │
│ ├─ Java                                 │
│ ├─ Maven                                │
│ ├─ Docker                               │
│ └─ Source Code (lebt hier!)             │
└─────────────────────────────────────────┘
```

**Wichtig**: Dein Source Code lebt im WSL Linux System, nicht auf Windows!

### Befehle

```bash
# Shutdown WSL (Reset)
wsl --shutdown

# Schauen welche Distros existieren
wsl --list --verbose

# In WSL Ubuntu starten
wsl -d Ubuntu-24.04
```

## Linux / macOS

Auf nativen Linux oder macOS Systemen brauchst du WSL nicht.

1. **Remote - Containers Extension installieren**
2. **Docker starten**
3. [Devcontainer](../Docker/Devcontainer.md) nutzen

## Troubleshooting

| Problem | Lösung |
|---------|--------|
| VSCode kann sich nicht zu WSL verbinden | WSL 2 aktiviert? Remote - WSL Extension installiert? |
| Docker läuft nicht im WSL | Docker Desktop öffnen, WSL Integration aktivieren |
| Permission denied im WSL | `sudo` nutzen oder WSL User konfigurieren |
| Git Zeilenumbrüche falsch | Siehe [Git Konfiguration](../Git/Konfiguration.md) `.gitattributes` |

## Weitere Ressourcen

- [Microsoft WSL Docs](https://docs.microsoft.com/windows/wsl/)
- [VSCode Remote Development](https://code.visualstudio.com/docs/remote/remote-overview)
