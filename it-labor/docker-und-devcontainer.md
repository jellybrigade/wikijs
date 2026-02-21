# Docker und Devcontainer

## Was ist Docker?

Docker ist eine Plattform zum Erstellen, Verteilen und Ausführen von Anwendungen in isolierten Containern. Ein Container enthält alles, was eine Anwendung zum Laufen braucht — Laufzeitumgebung, Abhängigkeiten und Konfiguration — und verhält sich auf jedem System gleich.

## Docker auf Windows vs. Linux

Unter Linux läuft Docker nativ. Unter Windows läuft Docker Desktop über eine WSL-Integration: Es verbindet sich mit einem Ubuntu-WSL-Image als virtuelle Maschine. Die Einstellung dafür findet sich unter Resources → WSL Integration.

## Dockerfile vs. docker-compose.yml

| Datei | Verwendung |
|---|---|
| `Dockerfile` | Definiert einen einzelnen Container |
| `docker-compose.yml` | Orchestriert mehrere Container gemeinsam |

```kroki
mermaid

%%{init: {'theme': 'base', 'flowchart': {'padding': 25}, 'themeVariables': {'background': '#231f20', 'mainBkg': '#3b9689', 'primaryColor': '#3b9689', 'primaryTextColor': '#fff', 'primaryBorderColor': '#70c7ba', 'lineColor': '#70c7ba', 'edgeLabelBackground': '#282425', 'nodeTextColor': '#fff', 'clusterBkg': '#282425'}}}%%
flowchart LR
    DF[Dockerfile]
    DC[docker-compose.yml]
    IMG[Image]
    C[Container]
    MC[Mehrere Container]

    DF -->|docker build| IMG
    IMG -->|docker run| C
    DC -->|docker compose up| MC
```

## Devcontainer

Ein Devcontainer ist ein von Microsoft definierter Standard auf Basis von Docker. Er beschreibt die vollständige Entwicklungsumgebung in `.devcontainer/devcontainer.json`. Damit hat jeder Entwickler im Team dieselbe Umgebung — Betriebssystem, Tools, Extensions.

VSCode erkennt die Konfiguration automatisch und bietet an, das Projekt im Container zu öffnen. Alle Änderungen (Dateien, Git, Terminal) finden dann im Container statt — unabhängig vom Host-System.

## Maven

Maven ist ein Build-Tool für Java-Projekte. Es verwaltet Abhängigkeiten, kompiliert den Code und führt Tests aus.

Ein **Maven Archetype** ist eine vorgefertigte Projektstruktur — ähnlich einem Template. Damit wird ein neues Projekt mit dem korrekten Verzeichnis-Layout, einer `pom.xml` und Beispieldateien erstellt, ohne alles manuell anlegen zu müssen.

### Neues Maven-Projekt in VSCode

1. Command Palette öffnen (`Ctrl+Shift+P`)
2. **Update Maven Archetype Catalogue** — beim ersten Mal den Katalog aktualisieren, damit alle verfügbaren Archetypes geladen werden
3. **Maven: Create Maven Project** auswählen
4. Archetype wählen: **maven-archetype-quickstart** — der Standard für ein einfaches Java-Projekt mit `src/main/java` und `src/test/java`
5. Group ID eingeben (z. B. `at.schule`), Artifact ID (Projektname), Version bestätigen
6. Speicherort wählen — Maven legt den Projektordner automatisch an

## Test-Driven Development (TDD)

Beim TDD wird zuerst der Test geschrieben, dann der Code. Der Zyklus lautet Red → Green → Refactor: Der Test schlägt zuerst fehl (Red), dann wird der minimale Code geschrieben, damit er besteht (Green), dann wird der Code aufgeräumt (Refactor).

Beispiel aus dem Unterricht:

```java
// TestTaschenrechner.java
Taschenrechner t = new Taschenrechner();
assertEquals(2, t.addieren(1, 1));

// Taschenrechner.java
public int addieren(int a, int b) {
    return a + b;
}
```

## Klassen und Methoden in Java

Eine **Klasse** ist ein Bauplan für Objekte. Sie beschreibt, welche Eigenschaften (Attribute) und welches Verhalten (Methoden) ein Objekt dieses Typs hat. Im TDD-Beispiel oben ist `Taschenrechner` eine Klasse.

Eine **Methode** ist eine Funktion, die zu einer Klasse gehört und eine Operation beschreibt, die ein Objekt ausführen kann. `addieren(int a, int b)` ist eine Methode der Klasse `Taschenrechner`.

Mehr zum Thema: [Programmierparadigmen — Objektorientiert](../informatik/programmierparadigmen.md)
