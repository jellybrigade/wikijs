---
title: zahlenduell
description:
published: 1
date: 2026-02-23T07:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-02-23T07:00:00.000Z
---

# Projekt: Zahlenduell

## Aufgabenstellung

Ein Java-Spiel: Der Computer wählt eine geheime Zahl zwischen 1 und 100. Der Spieler muss sie mit möglichst wenigen Versuchen erraten.

- Programm begrüßt den Benutzer und erklärt den Zahlenraum
- Computer ist Spielleiter: nimmt Eingaben entgegen, antwortet mit „zu hoch" oder „zu niedrig"
- Programm zählt die Versuche mit
- Endet erst, wenn die exakte Zahl eingegeben wird
- Abschluss: Glückwunsch + Statistik (Anzahl Versuche)

## Ablauf

```kroki
mermaid

%%{init: {'theme': 'base', 'themeVariables': {'background': '#231f20', 'mainBkg': '#3b9689', 'primaryColor': '#3b9689', 'primaryTextColor': '#fff', 'primaryBorderColor': '#70c7ba', 'lineColor': '#70c7ba', 'edgeLabelBackground': '#282425', 'nodeTextColor': '#fff', 'clusterBkg': '#282425'}}}%%
flowchart TD
    A[Start] --> B[Geheime Zahl generieren]
    B --> C[Begrüßung ausgeben]
    C --> D[Eingabe einlesen]
    D --> E[Versuche ++]
    E --> F{Vergleich}
    F -->|zu niedrig| G[Ausgabe: höher] --> D
    F -->|zu hoch| H[Ausgabe: niedriger] --> D
    F -->|genau richtig| I[Glückwunsch + Versuche ausgeben]
    I --> J[Ende]
```

## Projektstruktur

```
src/
  main/java/
    App.java
    Zahlenduell.java
  test/java/
    ZahlenduellTest.java
```

## Code

**App.java** — Einstiegspunkt:

```java
public class App {
    public static void main(String[] args) {
        new Zahlenduell().start();
    }
}
```

**Zahlenduell.java** — Spiellogik:

```java
import java.util.Scanner;

public class Zahlenduell {

    int generiereZahl() {
        return (int) (Math.random() * 100) + 1;
    }

    public void start() {
        int geheimeZahl = generiereZahl();
        int versuche = 0;
        Scanner scanner = new Scanner(System.in);

        System.out.println("Willkommen beim Zahlenduell!");
        System.out.println("Ich habe eine Zahl zwischen 1 und 100 gewählt. Errate sie!");

        int eingabe;
        do {
            System.out.print("Dein Tipp: ");
            eingabe = scanner.nextInt();
            versuche++;

            if (eingabe < geheimeZahl) {
                System.out.println("Zu niedrig!");
            } else if (eingabe > geheimeZahl) {
                System.out.println("Zu hoch!");
            }
        } while (eingabe != geheimeZahl);

        System.out.println("Glückwunsch! Du hast die Zahl in " + versuche + " Versuchen gefunden.");
    }
}
```

`generiereZahl()` hat package-private Sichtbarkeit (kein `public`) — damit können Tests aus demselben Package direkt darauf zugreifen.

**ZahlenduellTest.java** — JUnit-Test:

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertTrue;

public class ZahlenduellTest {

    @Test
    void zahlIstZwischen1Und100() {
        Zahlenduell duell = new Zahlenduell();
        for (int i = 0; i < 1000; i++) {
            int zahl = duell.generiereZahl();
            assertTrue(zahl >= 1 && zahl <= 100,
                "Die generierte Zahl " + zahl + " ist nicht zwischen 1 und 100");
        }
    }
}
```

Der Test läuft `generiereZahl()` 1000-mal und prüft jedes Mal, ob das Ergebnis im erlaubten Bereich liegt. So werden auch Randfälle (1 und 100) mit hoher Wahrscheinlichkeit abgedeckt.
