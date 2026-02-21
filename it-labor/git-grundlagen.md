# Git-Grundlagen

Git ist ein verteiltes Versionskontrollsystem. Es speichert Snapshots (Commits) des Source Codes und ermöglicht die Zusammenarbeit mehrerer Entwickler an einem Projekt.

[![How Git Works: Explained in 4 Minutes](https://img.youtube.com/vi/e9lnsKot_SQ/maxresdefault.jpg)](https://www.youtube.com/watch?v=e9lnsKot_SQ)

## Workflow

```kroki
mermaid

%%{init: {'theme': 'base', 'flowchart': {'padding': 60, 'useMaxWidth': false}, 'themeVariables': {'background': '#231f20', 'mainBkg': '#3b9689', 'primaryColor': '#3b9689', 'primaryTextColor': '#fff', 'primaryBorderColor': '#70c7ba', 'lineColor': '#70c7ba', 'edgeLabelBackground': '#282425', 'nodeTextColor': '#fff', 'clusterBkg': '#282425'}}}%%
flowchart LR
    RR[Remote Repository]
    LR_[Local Repository]
    SA[Staging Area]
    WD[Working Directory]

    RR -->|git clone| LR_
    LR_ -->|checkout| WD
    WD -->|git add| SA
    SA -->|git commit| LR_
    LR_ -->|git push| RR
    RR -->|git pull| LR_
```

## Einstieg: clone vs. init

| Befehl | Verwendung |
|---|---|
| `git clone <url>` | Kopiert ein bestehendes Remote-Repository lokal. Führt intern `init` und `checkout` aus. |
| `git init` | Erstellt ein neues, leeres Repository im aktuellen Verzeichnis (`.git`-Ordner). |

Nach `git init` muss das Remote-Repository manuell verknüpft werden:

```bash
git remote add origin <ssh-url>
```

`origin` ist nur ein konventioneller Name — das Remote kann beliebig benannt werden.

## Wichtige Befehle

| Befehl | Beschreibung |
|---|---|
| `git add <datei>` | Datei in die Staging Area aufnehmen |
| `git add .` | Alle geänderten Dateien stagen |
| `git commit -m "Nachricht"` | Commit mit Nachricht erstellen |
| `git push` | Commits ins Remote-Repository übertragen |
| `git push -u origin main` | Push + Upstream setzen (danach reicht `git push`) |
| `git pull` | Änderungen aus dem Remote-Repository holen und mergen |
| `git clone <url>` | Repository lokal klonen |

## git pull vs. git fetch

`git pull` holt Änderungen vom Remote und führt sie sofort mit dem lokalen Branch zusammen (entspricht `fetch` + `merge` in einem Schritt). `git fetch` holt nur die Änderungen, ohne sie einzuspielen — nützlich, um zuerst nachzusehen, was sich geändert hat, bevor man merged.

## Branches

Branches erlauben paralleles Arbeiten an verschiedenen Features oder Fixes, ohne den `main`-Branch zu beeinflussen. Mit `git branch <name>` wird ein neuer Branch erstellt, mit `git checkout -b <name>` erstellt und direkt gewechselt.

## SSH

Für die Verbindung zum Remote-Repository wird ein SSH-Schlüssel benötigt. Dieser muss einmalig auf dem eigenen Rechner generiert und im Git-Provider (GitHub, GitLab etc.) hinterlegt werden.

Anleitung: [SSH Key generieren — GitHub Docs](https://docs.github.com/de/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
