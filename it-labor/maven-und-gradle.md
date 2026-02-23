---
title: maven-und-gradle
description:
published: 1
date: 2026-02-23T07:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-02-23T07:00:00.000Z
---

# Maven und Gradle

Beide sind **Build-Tools** für Java. Ein Build-Tool übernimmt Aufgaben, die man sonst manuell erledigen müsste:

- Abhängigkeiten (Libraries) herunterladen und einbinden
- Code kompilieren
- Tests ausführen
- Fertiges Programm zusammenbauen (`.jar`)

## Maven

Maven ist das ältere, weit verbreitete Build-Tool. Die gesamte Konfiguration steht in einer XML-Datei namens `pom.xml` im Projektwurzel.

### Projektstruktur

Maven schreibt eine feste Ordnerstruktur vor:

```
mein-projekt/
├── pom.xml
└── src/
    ├── main/java/       ← eigener Code
    └── test/java/       ← Tests
```

### pom.xml

Die `pom.xml` beschreibt das Projekt und seine Abhängigkeiten:

```xml
<project>
  <groupId>at.schule</groupId>      <!-- Organisations-ID, wie ein Package-Name -->
  <artifactId>zahlenduell</artifactId>  <!-- Projektname -->
  <version>1.0</version>

  <dependencies>
    <dependency>
      <groupId>org.junit.jupiter</groupId>
      <artifactId>junit-jupiter</artifactId>
      <version>5.10.0</version>
      <scope>test</scope>    <!-- nur für Tests, nicht im fertigen Programm -->
    </dependency>
  </dependencies>
</project>
```

### Neues Maven-Projekt in VSCode

1. Command Palette öffnen (`Ctrl+Shift+P`)
2. Beim ersten Mal: **Update Maven Archetype Catalogue** — lädt alle verfügbaren Vorlagen
3. **Maven: Create Maven Project** auswählen
4. Archetype wählen: **maven-archetype-quickstart** — erstellt die Standardstruktur mit `src/main/java` und `src/test/java`
5. Group ID und Artifact ID eingeben, Speicherort wählen

### Wichtige Befehle

```sh
mvn compile       # kompiliert den Code
mvn test          # führt alle Tests aus
mvn package       # baut eine .jar-Datei
mvn clean         # löscht kompilierte Dateien (target/)
```

---

## Gradle

Gradle ist das modernere Build-Tool. Es kann dieselben Aufgaben wie Maven, ist aber flexibler. Statt XML nutzt es eine eigene Konfigurationssprache (Groovy oder Kotlin).

### Projektstruktur

Gradle verwendet dieselbe Ordnerstruktur wie Maven (`src/main/java`, `src/test/java`), aber andere Konfigurationsdateien:

```
mein-projekt/
├── build.gradle      ← Konfiguration (Abhängigkeiten, Plugins)
├── settings.gradle   ← Projektname, Teilprojekte
├── gradlew           ← Gradle Wrapper (Linux/Mac)
└── gradlew.bat       ← Gradle Wrapper (Windows)
```

Der **Gradle Wrapper** (`gradlew`) ist ein Skript, das die richtige Gradle-Version automatisch herunterlädt und startet. Man braucht Gradle selbst nicht installiert zu haben — `./gradlew` reicht.

### build.gradle

```groovy
plugins {
    id 'java'
}

dependencies {
    testImplementation 'org.junit.jupiter:junit-jupiter:5.10.0'
}

test {
    useJUnitPlatform()
}
```

### Wichtige Befehle

```sh
./gradlew build       # kompiliert und testet
./gradlew test        # nur Tests
./gradlew compileJava # nur kompilieren
./gradlew clean       # löscht Build-Dateien
```

Unter Windows: `gradlew.bat` statt `./gradlew`.

### Teilprojekte

Ein Gradle-Projekt kann aus mehreren Teilprojekten bestehen. Das ist sinnvoll, wenn ein größeres Projekt in unabhängige Module aufgeteilt wird (z. B. `core`, `api`, `web`).

```
mein-projekt/
├── settings.gradle
├── core/
│   └── build.gradle
└── api/
    └── build.gradle
```

```groovy
// settings.gradle
rootProject.name = 'mein-projekt'
include 'core', 'api'
```

Jedes Teilprojekt hat eine eigene `build.gradle` mit eigenen Abhängigkeiten.

### Schütz-Repository

Herr Schütz hat ein fertiges Gradle-Projekt mit vorkonfigurierten Code-Qualitätswerkzeugen:

| Tool | Zweck |
|---|---|
| SonarQube | Statische Code-Analyse, findet Bugs und Code Smells |
| Checkstyle / Lint | Prüft Coding Style und Formatierung |
| SpotBugs | Typ- und Bug-Prüfung |
| JUnit | Tests mit Abdeckungsmessung |

Einfach auschecken und als Basis verwenden:

```sh
git clone <repo-url>
./gradlew build
```

---

## Maven vs. Gradle im Vergleich

| | Maven | Gradle |
|---|---|---|
| Konfiguration | XML (`pom.xml`) | Groovy/Kotlin (`build.gradle`) |
| Geschwindigkeit | Langsamer | Schneller (inkrementell, Cache) |
| Verbreitung | Sehr weit verbreitet | Modern, wächst stark |
| Einstieg | Einfacher (viel Doku) | Etwas steiler |
| Teilprojekte | Möglich | Besser integriert |

Für den Unterricht werden beide verwendet — Maven zum Einstieg (VSCode-Integration), Gradle für das Schütz-Repo.
