# Git Grundlagen

## Was ist Git?

Git ist ein **Versionskontrollsystem (VCS)**. Es speichert die komplette Geschichte deiner Dateien:

- Wer hat was geändert?
- Wann wurde es geändert?
- Warum wurde es geändert?

## Zentrale Konzepte

### Repository

Ein Repository ist ein Projekt mit vollständiger Git-Historie:

- **Remote Repository** — auf einem Server (z.B. GitHub, GitLab)
- **Local Repository** — auf deinem Computer (`.git` Ordner)

### Der Workflow (Lokal)

```
Working Directory  →  Staging Area  →  Local Repository  →  Remote Repository
   (deine Dateien)   (git add)        (git commit)         (git push)
```

**Umgekehrt:**
```
Remote Repository  →  Local Repository  →  Working Directory
   (github.com)          (git pull)         (du arbeitest hier)
```

### Commits

Ein **Commit** ist ein Snapshot deines Codes zu einem Zeitpunkt. Es speichert:

- Alle geänderten Dateien
- Eine Commit-Message ("Was habe ich geändert?")
- Autor und Timestamp
- Referenz zum vorherigen Commit (Geschichte)

## Die vier Bereiche

| Bereich | Bedeutung | Befehl |
|---------|-----------|--------|
| **Working Directory** | Deine lokalen Dateien | - |
| **Staging Area** | Markierte Änderungen | `git add` |
| **Local Repository** | Gespeicherte Commits (`.git`) | `git commit` |
| **Remote Repository** | Server (GitHub, etc.) | `git push` / `git pull` |

## Erste Schritte

### Repository klonen

```bash
git clone https://github.com/nutzer/projekt.git
```

Das macht automatisch:
1. `git init` (initialisiert `.git`)
2. Verbindung zur Remote URL
3. Herunterladung aller Dateien

### Neues Repository erstellen

```bash
# Im Projektordner
git init

# Remote hinzufügen
git remote add origin https://github.com/nutzer/projekt.git

# Erste Dateien hinzufügen
git add .
git commit -m "Initial commit"

# Zu Remote pushen
git push -u origin main
```

## Wichtige Befehle (Schnellreferenz)

```bash
# Status anschauen
git status

# Datei zum Staging hinzufügen
git add dateiname.java
# oder alle
git add .

# Commit erstellen
git commit -m "Beschreibung der Änderung"

# Zu Remote pushen
git push

# Vom Remote holen
git pull

# History anschauen
git log
git log --oneline   # Kompakt
```

Siehe [Befehle](Befehle.md) für ausführliche Dokumentation.

## Best Practices

- **Oft committen**: Viele kleine Commits > wenige große Commits
- **Aussagekräftige Messages**: "Fixed bug" ❌ vs "Fixed NPE in calculateTotal() #234" ✓
- **Nicht zu lange in einem Branch**: Mergen regelmäßig zum Main Branch
- **Vor Push immer git pull**: Konflikte vermeiden
- **Code Review**: Merges sollten reviewed werden

Siehe [Best-Practices](Best-Practices.md) für Details.

## Weitere Themen

- [Workflow Modell](Workflow.md)
- [Konfiguration: .gitignore & .gitattributes](Konfiguration.md)
- [Git Befehle](Befehle.md)
