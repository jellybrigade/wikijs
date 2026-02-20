# Git Konfiguration: .gitignore & .gitattributes

## .gitignore

Die `.gitignore` Datei teilt Git mit, welche Dateien **nicht** versioniert werden sollen.

### Problem

Beim Arbeiten entstehen viele Dateien, die nicht ins Repository gehören:

- Kompilierte Dateien (`.class`, `.jar`)
- Build-Ordner (`target/`, `build/`)
- IDE-Konfiguration (`.idea/`, `.vscode/`)
- OS-Dateien (`.DS_Store`, `Thumbs.db`)
- Secrets (`api-key.txt`, Passwörter)

Ohne `.gitignore` würden diese in `git status` auftauchen.

### Syntax

```bash
# Kommentar
*.class           # Alle .class Dateien ignorieren
target/           # Ganzer Ordner ignorieren
.env              # Spezifische Datei
.DS_Store         # macOS Dateien
*.log             # Alle Log-Dateien
!important.log    # AUSNAHME: diese Log-Datei NICHT ignorieren
```

### Beispiel für Java + Maven Projekt

```bash
# Java
*.class
*.jar
*.war
*.ear
*.nar
hs_err_pid*
replay_pid*

# Maven
target/
pom.xml.tag
pom.xml.releaseBackup
pom.xml.bak
release.properties
dependency-reduced-pom.xml

# IDE
.idea/
.vscode/
*.iml
out/

# OS
.DS_Store
Thumbs.db

# Build
*.log
*.swp
*~
.gradle

# Secrets (niemals ins Repo!)
.env
api-key.txt
secrets.properties
```

### Tipps

- Erstelle `.gitignore` **bevor** du erste Commits machst
- `*.gitignore` globale Version: `git config --global core.excludesfile ~/.gitignore`
- Bereits getrackte Datei ignorieren: `git rm --cached datei.java`

## .gitattributes

Die `.gitattributes` Datei teilt Git mit, wie bestimmte Dateitypen behandelt werden. Besonders wichtig für **Zeilenumbrüche** bei Windows/Linux Unterschieden.

### Das Zeilenumbruch Problem

**Windows**: Zeilenende = `CRLF` (Carriage Return + Line Feed) = `\r\n`
**Linux/macOS**: Zeilenende = `LF` (Line Feed nur) = `\n`

**Problem**: Wenn Windows-User einen Code pushen, ändert sich die Zeilenumbruch-Art. Das sieht dann aus, als würde die ganze Datei geändert sein, obwohl nur die Zeilenumbrüche anders sind (sehr nervtig!).

**Lösung**: `.gitattributes` mit automatischer Normalisierung.

### Beispiel .gitattributes

```bash
# Automatische Normalisierung: Convert CRLF to LF
* text=auto

# Git-Konfiguration (immer LF)
.gitignore text eol=lf
.gitattributes text eol=lf
.devcontainer/devcontainer.json text eol=lf

# Java Sources
*.java          text diff=java
*.kt            text diff=kotlin
*.gradle        text diff=java
*.gradle.kts    text diff=kotlin

# Web-Dateien
*.css           text diff=css
*.html          text diff=html
*.js            text
*.json          text

# Diese Dateien sind BINÄR (nicht ändern!)
*.class         binary
*.jar           binary
*.war           binary
*.dll           binary
```

### Was bedeutet `text=auto`?

```
Git automatisch entscheiden lässt:
- Text-Datei → Zeilenumbrüche normalisieren
- Binär-Datei → Unverändert lassen
```

### `eol=lf` vs `eol=crlf`

```bash
text eol=lf     # Immer Linux Zeilenumbrüche (LF)
text eol=crlf   # Immer Windows Zeilenumbrüche (CRLF)
text=auto       # Auto-Erkennung
```

**Best Practice für Team-Projekte**: `* text=auto` + `text eol=lf` für kritische Dateien

### Diff für bestimmte Sprachen

```bash
*.java text diff=java
*.cpp text diff=cpp
```

Das sagt Git: "Verwende Java-aware Diffing für `.java` Dateien"

## Komplettes Beispiel Setup

```bash
# 1. Projekt initialisieren
git init

# 2. .gitattributes erstellen
cat > .gitattributes << 'EOF'
* text=auto
.gitignore text eol=lf
.gitattributes text eol=lf
*.java text diff=java
*.class binary
*.jar binary
EOF

# 3. .gitignore erstellen
cat > .gitignore << 'EOF'
# Java
*.class
target/
*.jar

# IDE
.idea/
.vscode/

# OS
.DS_Store
EOF

# 4. Beide hinzufügen und committen
git add .gitattributes .gitignore
git commit -m "Add git configuration"
```

## Troubleshooting

### "Alle Zeilen haben sich geändert!"

Wahrscheinlich ein Zeilenumbruch-Problem:

```bash
# Normalisierung erzwingen:
git add --renormalize .
git commit -m "Normalize line endings"
```

### Datei wird ignoriert, obwohl sie da ist

```bash
# Cached Eintrag löschen
git rm --cached dateiname
git add .gitignore
git commit -m "Remove cached file"
```

## Weitere Informationen

- [Git Grundlagen](Grundlagen.md)
- [Git Befehle](Befehle.md)
