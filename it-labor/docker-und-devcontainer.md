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

%%{init: {'theme': 'base', 'flowchart': {'htmlLabels': false}, 'themeVariables': {'background': '#231f20', 'mainBkg': '#3b9689', 'primaryColor': '#3b9689', 'primaryTextColor': '#fff', 'primaryBorderColor': '#70c7ba', 'lineColor': '#70c7ba', 'edgeLabelBackground': '#282425', 'nodeTextColor': '#fff', 'clusterBkg': '#282425'}}}%%
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

## Maven und Gradle

Maven und Gradle sind die Build-Tools im Unterricht — sie verwalten Abhängigkeiten, kompilieren den Code und führen Tests aus.

→ [Maven und Gradle — ausführliche Erklärung](maven-und-gradle.md)

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

## JUnit

JUnit ist das Standard-Testframework für Java. Tests sind normale Java-Klassen, die mit `@Test` markierte Methoden enthalten.

### Einbinden (Maven)

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter</artifactId>
    <version>5.x</version>
    <scope>test</scope>
</dependency>
```

`<scope>test</scope>` bedeutet: die Abhängigkeit ist nur beim Kompilieren und Ausführen von Tests vorhanden, nicht im fertigen Programm.

### Aufbau eines Tests

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

class RechnerTest {

    @Test
    void addierenGibtRichtigesErgebnis() {
        Rechner r = new Rechner();
        assertEquals(5, r.addieren(2, 3));
    }
}
```

### Wichtige Annotationen und Assertions

| | Bedeutung |
|---|---|
| `@Test` | Markiert eine Testmethode |
| `@BeforeEach` | Läuft vor jedem Test (z. B. Objekte initialisieren) |
| `assertEquals(erwartet, tatsächlich)` | Prüft auf Gleichheit |
| `assertTrue(bedingung)` | Prüft, dass eine Bedingung wahr ist |
| `assertFalse(bedingung)` | Prüft, dass eine Bedingung falsch ist |
| `assertNull(objekt)` | Prüft, dass ein Objekt `null` ist |

### Tests ausführen

```sh
mvn test          # Maven
./gradlew test    # Gradle
```

VSCode zeigt Testergebnisse auch direkt im Editor an (grüner Haken / rotes Kreuz neben der Testmethode).

## Klassen und Methoden in Java

Eine **Klasse** ist ein Bauplan für Objekte. Sie beschreibt, welche Eigenschaften (Attribute) und welches Verhalten (Methoden) ein Objekt dieses Typs hat. Im TDD-Beispiel oben ist `Taschenrechner` eine Klasse.

Eine **Methode** ist eine Funktion, die zu einer Klasse gehört und eine Operation beschreibt, die ein Objekt ausführen kann. `addieren(int a, int b)` ist eine Methode der Klasse `Taschenrechner`.

Mehr zum Thema: [Programmierparadigmen — Objektorientiert](../informatik/programmierparadigmen.md)

## Funktion vs. Prozedur

| Begriff | Java-Signatur | Rückgabewert |
|---|---|---|
| **Funktion** | `int generiereZahl()` | Ja — liefert einen Wert zurück |
| **Prozedur** | `void start()` | Nein — führt nur Aktionen aus |

In Java gibt es keine formale Unterscheidung im Sprachstandard — beides sind Methoden. Der Unterschied liegt im Rückgabetyp: `void` = Prozedur, alles andere = Funktion.
