# Git Best Practices

## Commit-Hygiene

### 1. Oft und klein committen

**Gut** ✓:
```bash
git commit -m "Add login method to UserService"
git commit -m "Add unit tests for UserService"
git commit -m "Add validation in UserService"
```

**Schlecht** ✗:
```bash
git commit -m "Lots of stuff I did today"  # Was genau?
git commit -m "WIP"                        # Nicht aussagekräftig
```

**Vorteile von vielen kleinen Commits**:
- Einfacheres Debugging (bisect)
- Klare History
- Einfacher zu revertieren einzelner Änderungen

### 2. Aussagekräftige Commit-Messages

**Format**:
```
[Kurz] Eine Zeile, max 50 Zeichen, Imperativ

[Optional] Längere Beschreibung nach Leerzeile.
Erkläre WARUM, nicht WAS.
Mehrere Absätze sind ok.

[Optional] Issue-Referenz: Fixes #234
```

**Beispiele**:

Gut ✓:
```
Add email validation to registration form

Users were able to submit invalid email addresses.
Added regex validation on client and server side.

Fixes #156
```

Schlecht ✗:
```
fixed bugs         # Welche Bugs?
updated stuff      # Was? Warum?
asdf123            # Sinn?
```

### 3. Nur versionwürdiger Code committen

- Tests schreiben **bevor** du pushst
- `git diff` anschauen vor `git commit`
- Keine Debugging-Statements committen (`System.out.println()`)
- Keine temporären Dateien

```bash
# Vor Commit anschauen
git diff

# Staging überprüfen
git diff --cached

# Dann erst committen wenn alles ok ist
git commit
```

## Branch Management

### 1. Main Branch Schutz

Der `main` Branch sollte immer deploybar sein:

- Nur über Pull Requests ändern
- Code Review erforderlich
- Tests müssen grün sein
- Kein direktes Pushen zu main!

### 2. Feature Branches

Für jedes Feature einen neuen Branch:

```bash
git checkout -b feature/user-authentication
git checkout -b bugfix/login-crash
git checkout -b docs/api-documentation
```

**Naming Convention**:
```
feature/             # Neue Features
bugfix/              # Bug-Fixes
docs/                # Dokumentation
refactor/            # Code-Umstrukturierung
test/                # Tests hinzufügen
```

### 3. Branch Lebenszyklus

```
git checkout -b feature/new-feature
    ↓
    # Hier arbeiten, commiten
    # Mehrere Commits ok!
    ↓
git push -u origin feature/new-feature
    ↓
    # Pull Request erstellen (GitHub/GitLab)
    # Code Review
    ↓
    # Nach Merge
git checkout main
git pull
git branch -d feature/new-feature
```

## Zusammenarbeit

### 1. Vor dem Pushen

```bash
# Remote-Änderungen holen
git pull

# Deine lokalen Commits anschauen
git log origin/main..HEAD

# Dann pushen
git push
```

### 2. Merge Konflikte vermeiden

```bash
# Regel: Immer before push `git pull`
git add .
git commit -m "My changes"
git pull        # ← Vor Push!
git push
```

Falls Konflikt:
```bash
# 1. Konflikt-Marker anschauen (<<<<, ====, >>>>)
# 2. Lösen
git add gelöste-datei.java
git commit -m "Resolved merge conflict"
git push
```

### 3. Code Review

**Als Autor**:
- PR-Beschreibung schreiben (Was & Warum)
- Tests hinzufügen
- Auf Feedback reagieren

**Als Reviewer**:
- Code verstehen und überprüfen
- Sicherheit, Performance, Style beachten
- Konstruktiv kommentieren
- Approve nicht wenn Fragen offen sind

## Sicherheit

### 1. Secrets niemals committen!

```bash
# ❌ FALSCH
password = "super-secret"
api_key = "sk_live_..."

# ✓ RICHTIG
# Datei: .gitignore
.env
secrets.properties
.aws/credentials

# Und lokal verwenden:
# .env (nicht ins Repo)
DB_PASSWORD=lokal_passwort
```

Wenn Secrets schon gepusht wurden:
```bash
# Sofort secret rotieren!
# Branch history bereinigen mit:
git filter-branch --tree-filter 'rm -f secrets.txt' -- --all
```

### 2. Keine großen Binärdateien

```bash
# ❌ Nicht tun
git add movie.mp4          # Git wird langsam!

# ✓ Nutze
git lfs install            # Git Large File Storage
git lfs track '*.mp4'
git add movie.mp4
```

## Workflow Standard

Ein typischer Workday:

```bash
# 1. Morgens: Team-Änderungen holen
git pull

# 2. Feature-Branch erstellen
git checkout -b feature/my-feature

# 3. Tagsüber: Arbeiten und committen
git add .
git commit -m "Step 1"
git add .
git commit -m "Step 2"

# 4. Vor Feierabend: Pushen
git pull --rebase          # Local commits rebasieren
git push -u origin feature/my-feature

# 5. Pull Request erstellen (GitHub UI)
# 6. Code Review
# 7. Mergen (GitHub UI)

# 8. Cleanup
git checkout main
git pull
git branch -d feature/my-feature
```

## Häufige Fehler

| Fehler | Lösung |
|--------|--------|
| `git push` rejected (Remote ahead) | `git pull` vor push |
| Commit in falschen Branch | `git cherry-pick` zu richtigem Branch |
| Sensitiver Daten gepusht | Sofort rotieren, History bereinigen |
| Großes File committed | `git rm --cached`, `.gitignore` hinzufügen |
| Letzten Commit ändern | `git commit --amend` (nur lokal!) |

## Zusammenfassung

- ✓ Oft committen, aussagekräftige Messages
- ✓ Feature Branches für alles
- ✓ `git pull` vor `git push`
- ✓ Code Review vor Merge
- ✓ Keine Secrets, keine großen Binärdateien
- ✓ Main Branch immer deploybar

Siehe auch: [Git Grundlagen](Grundlagen.md), [Git Befehle](Befehle.md)
