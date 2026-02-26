# Das lg1-Lehrgang-Projekt

Im IT-Labor arbeitet jeder mit einem eigenen Repository: `lg1-<name>`. Es basiert auf dem gleichen Grundgerüst — einer **Gradle-Multi-Projekt-Struktur** für Java-Aufgaben mit automatischen Tests.

## Ordnerstruktur

```
lg1-marcelschachner/
├── Aufgabe01/                  ← erste Aufgabe (ein Teilprojekt)
│   └── src/
│       ├── main/java/fbs/lg1/ ← eigener Java-Code hier
│       └── test/java/fbs/lg1/ ← Tests hier
├── build.gradle                ← gemeinsame Konfiguration (nicht anfassen)
├── settings.gradle             ← welche Aufgaben gibt es?
├── gradlew                     ← Gradle Wrapper (Linux/Mac)
├── gradlew.bat                 ← Gradle Wrapper (Windows)
└── script.sh                   ← neue Aufgabe anlegen
```

---

## Der Gradle Wrapper (`gradlew`)

`gradlew` ist ein Shell-Skript, das **Gradle automatisch herunterlädt und startet** — in der richtigen Version. Man braucht Gradle nicht selbst zu installieren.

```sh
./gradlew test           # alle Tests in allen Aufgaben ausführen
./gradlew Aufgabe01:test # nur Tests von Aufgabe01
./gradlew listTasks      # alle Aufgaben auflisten
./gradlew checkAllTasks  # alle Tests nacheinander ausführen
```

Unter Windows: `gradlew.bat` statt `./gradlew`.

Die verwendete Gradle-Version steht in `gradle/wrapper/gradle-wrapper.properties`.

---

## `settings.gradle` — Teilprojekte registrieren

```groovy
rootProject.name = 'java-lehrgang-1'
include 'Aufgabe01'
```

Jede neue Aufgabe muss hier eingetragen werden. Das passiert automatisch, wenn man `script.sh` verwendet.

---

## `build.gradle` (Root) — gemeinsame Konfiguration

Die Root-`build.gradle` definiert für **alle** Aufgaben gemeinsam:

- **Java-Version:** Java 21
- **Abhängigkeiten:** JUnit 5 (Tests), Mockito (Mocking), AssertJ (Assertions)
- **Test-Ausgabe:** Detaillierte Zusammenfassung nach jedem Testlauf
- **Hilfsbefehle:** `listTasks` und `checkAllTasks`

Man muss diese Datei nicht ändern — sie ist das Fundament.

Jede Aufgabe hat zusätzlich eine eigene minimale `build.gradle`:

```groovy
// Aufgabe01/build.gradle
description = 'Zahlenraten Spiel'
```

Damit taucht die Aufgabe mit ihrer Beschreibung in der Übersicht auf.

---

## Aufgabe01 — Struktur eines Teilprojekts

```
Aufgabe01/
└── src/
    ├── main/java/fbs/lg1/
    │   └── ZahlenRaten.java       ← eigener Code
    └── test/java/fbs/lg1/
        └── ZahlenRatenTest.java   ← Tests
```

**Package:** Alle Klassen gehören zum Package `fbs.lg1`. Das muss in jeder Datei in der ersten Zeile stehen:

```java
package fbs.lg1;
```

**Tests** werden in der Testklasse mit `@Test` markiert und rufen Methoden der Hauptklasse auf:

```java
@Test
void zahlIstZwischen1Und100() {
    ZahlenRaten raten = new ZahlenRaten();
    int zahl = raten.generiereZahl();
    assertTrue(zahl >= 1 && zahl <= 100);
}
```

---

## `script.sh` — neue Aufgabe anlegen

Das Skript erstellt automatisch die komplette Ordnerstruktur für eine neue Aufgabe:

```sh
./script.sh Aufgabe02 'Fibonacci-Rechner'
```

Das legt an:
- `Aufgabe02/build.gradle` mit der Beschreibung
- `Aufgabe02/src/main/java/fbs/lg1/Aufgabe02.java` — Template-Klasse
- `Aufgabe02/src/test/java/fbs/lg1/Aufgabe02Test.java` — Template-Testklasse
- Trägt `Aufgabe02` in `settings.gradle` ein

Optional: eigener Klassenname als drittes Argument.

```sh
./script.sh Aufgabe02 'Fibonacci-Rechner' FibonacciRechner
# → erstellt FibonacciRechner.java und FibonacciRechnerTest.java
```

---

## Workflow: neue Aufgabe bearbeiten

1. `./script.sh AufgabeXX 'Beschreibung'` — Struktur anlegen
2. Testklasse öffnen — Testmethoden schreiben (TDD: erst der Test)
3. `./gradlew AufgabeXX:test` — Test schlägt fehl (Red)
4. Hauptklasse implementieren
5. `./gradlew AufgabeXX:test` — Test besteht (Green)
6. Aufräumen, committen

→ Mehr zu TDD: [Docker und Devcontainer — TDD](docker-und-devcontainer.md)
