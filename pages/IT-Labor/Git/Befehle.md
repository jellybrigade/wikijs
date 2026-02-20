# Git Befehle - Referenz

## Setup & Konfiguration

```bash
# Globale Konfiguration
git config --global user.name "Dein Name"
git config --global user.email "dein@email.com"

# Für dieses Projekt nur
git config user.name "Dein Name"

# Anschauen
git config --global --list
git config --list
```

## Repository erstellen / klonen

```bash
# Neues Repository initialisieren
git init

# Existierendes Repository klonen
git clone https://github.com/nutzer/projekt.git
git clone git@github.com:nutzer/projekt.git   # SSH Variante

# Nach dem Klonen:
cd projekt
```

## Remote verwalten

```bash
# Remote hinzufügen
git remote add origin https://github.com/nutzer/projekt.git

# Remote anschauen
git remote -v

# Remote URL ändern
git remote set-url origin https://github.com/nutzer/neues-repo.git

# Remote löschen
git remote remove origin
```

## Änderungen tracken

```bash
# Status anschauen
git status
git status -s   # Kurz

# Diff anschauen (Working Dir vs Staging)
git diff

# Diff anschauen (Staging vs Last Commit)
git diff --cached

# Diff zwischen zwei Commits
git diff abc123 def456
```

## Änderungen in Staging

```bash
# Datei in Staging hinzufügen
git add datei.java

# Mehrere Dateien
git add src/main/*.java

# Alle Dateien
git add .

# Interaktiv (mit Auswahl)
git add -p

# Aus Staging entfernen
git reset datei.java
git reset   # Alle entfernen
```

## Commits erstellen

```bash
# Commit mit Nachricht
git commit -m "Kurze Nachricht"

# Mit länger Nachricht (öffnet Editor)
git commit

# Nur bestimmte Dateien committen
git commit datei.java -m "Nachricht"

# Letzten Commit ändern (nicht pushen!)
git commit --amend --no-edit   # Änderungen zu letztem Commit hinzufügen
git commit --amend -m "Neue Nachricht"

# Letzten Commit rückgängig machen
git reset --soft HEAD~1   # Commit weg, Dateien im Staging
git reset --hard HEAD~1   # Commit und Änderungen weg!
```

## Push & Pull

```bash
# Zu Remote pushen
git push

# Mit Upstream setzen (erste Mal)
git push -u origin main

# Zu Remote holen
git pull

# Nur Commits holen (kein Merge)
git fetch
git fetch origin

# Rebase statt Merge
git pull --rebase
```

## History anschauen

```bash
# Commits anschauen
git log

# Kompakte Anzeige
git log --oneline

# Mit Graph (für Branches)
git log --graph --oneline --all

# Bestimmter Author
git log --author="Name"

# Seit einer bestimmten Zeit
git log --since="2 weeks ago"
git log --since="2026-02-01"

# Nur bestimmte Datei
git log datei.java

# Änderungen mit anzeigen
git log -p
git log -p datei.java

# Einen bestimmten Commit anschauen
git show abc123def
git show HEAD~1   # Vorheriger Commit
```

## Branches

```bash
# Branches auflisten
git branch
git branch -a   # Mit Remote Branches

# Neuen Branch erstellen
git branch feature/neue-funktion

# Zu Branch wechseln
git checkout feature/neue-funktion

# Beides zusammen (modern)
git switch -c feature/neue-funktion

# Branch löschen
git branch -d feature/neue-funktion   # Sicher (nur wenn gemerged)
git branch -D feature/neue-funktion   # Erzwungen

# Aktuellen Branch anschauen
git branch --show-current
```

## Mergen

```bash
# Anderen Branch in aktuellen mergen
git checkout main
git pull
git merge feature/neue-funktion

# Merge committen oder abbrechen
git commit -m "Merged feature/neue-funktion"   # Nach Konflikt-Lösung
git merge --abort   # Merge abbrechen

# Rebase statt Merge (linearer History)
git rebase main
```

## Stashing (Änderungen speichern)

```bash
# Änderungen speichern (aus Working Dir)
git stash

# Mit Nachricht
git stash save "Mein WIP"

# Stash anschauen
git stash list

# Stash wieder anwenden
git stash pop
git stash apply   # Ohne zu löschen

# Stash löschen
git stash drop
```

## Undo & Cleanup

```bash
# Datei auf letzten Commit zurücksetzen
git checkout HEAD -- datei.java
git restore datei.java   # Modern

# Alle Änderungen rückgängig machen
git checkout -- .
git restore .

# Untracked Dateien löschen
git clean -f
git clean -fd   # Mit Ordnern

# Dangling Commits aufräumen
git reflog
git gc
```

## Tags (Release-Markierungen)

```bash
# Tag erstellen
git tag v1.0.0

# Tag mit Nachricht
git tag -a v1.0.0 -m "Version 1.0.0"

# Tag anschauen
git tag -l
git show v1.0.0

# Tag pushen
git push origin v1.0.0
git push origin --tags   # Alle

# Tag löschen
git tag -d v1.0.0
git push origin --delete v1.0.0
```

## Tipps & Tricks

```bash
# Git alias setzen
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.br branch

# Dann nutzen:
git st    # = git status

# Last commit anschauen
git log -1 --stat

# Schöne grafische Ausgabe
git log --graph --oneline --all --decorate
```

## Troubleshooting

```bash
# Reflog (wenn Commits "verloren" sind)
git reflog
git checkout abc123def

# Welche Änderungen sind nicht gepusht?
git log origin/main..HEAD

# Welche neuen Commits von Remote?
git log HEAD..origin/main

# Interactive Rebase (Commits bereinigen)
git rebase -i HEAD~3   # Letzte 3 Commits
```

## Weitere Informationen

```bash
# Hilfe für Befehle
git help add
git add --help

# Git Version
git --version
```

Siehe auch: [Git Workflow](Workflow.md), [Konfiguration](Konfiguration.md)
