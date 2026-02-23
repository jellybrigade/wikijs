---
title: gradle
description:
published: 1
date: 2026-02-23T07:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-02-23T07:00:00.000Z
---

# Gradle

## Was ist Gradle?

Gradle ist ein modernes Build-Tool für Java (und andere Sprachen). Es übernimmt dieselben Aufgaben wie Maven — Abhängigkeiten verwalten, kompilieren, testen — ist aber flexibler und nutzt statt XML eine eigene DSL (Groovy oder Kotlin).

Kernelemente:
- `build.gradle` — Konfiguration des Projekts (Abhängigkeiten, Plugins, Tasks)
- `settings.gradle` — Name des Projekts und Einbindung von Teilprojekten
- `gradlew` / `gradlew.bat` — Gradle Wrapper, startet automatisch die richtige Gradle-Version

## Teilprojekte (Multi-Project Build)

Ein Gradle-Build kann aus mehreren Teilprojekten bestehen. Jedes Teilprojekt hat eine eigene `build.gradle`, das Wurzelprojekt hat eine `settings.gradle`, die alle Teilprojekte auflistet:

```groovy
// settings.gradle
rootProject.name = 'mein-projekt'
include 'core', 'api', 'web'
```

Jedes Teilprojekt liegt in einem eigenen Unterordner und kann eigene Abhängigkeiten und Tasks haben.

## Schütz-Repository

Herr Schütz hat ein fertiges Gradle-Projekt, das bereits Konfigurationen für Code-Qualitätswerkzeuge enthält:

| Tool | Zweck |
|---|---|
| SonarQube | Statische Code-Analyse, findet Bugs und Code Smells |
| Checkstyle / Lint | Prüft Coding Style und Formatierung |
| Type Check | Typ-Korrektheit (z. B. mit SpotBugs) |
| Test | JUnit-Tests mit Abdeckungsmessung |

Einfach auschecken und als Basis verwenden:

```sh
git clone <repo-url>
./gradlew build
```
