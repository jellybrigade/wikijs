---
title: datenstrukturen
description: 
published: 1
date: 2026-02-21T10:57:29.724Z
tags: 
editor: markdown
dateCreated: 2026-02-21T07:24:43.106Z
---

# Datenstrukturen

## Überblick

```kroki
mermaid

%%{init: {'theme': 'base', 'themeVariables': {'background': '#e8e8e8', 'mainBkg': '#3b9689', 'primaryColor': '#3b9689', 'primaryTextColor': '#fff', 'primaryBorderColor': '#70c7ba', 'lineColor': '#70c7ba', 'edgeLabelBackground': '#d0d0d0', 'nodeTextColor': '#fff', 'clusterBkg': '#d0d0d0'}}}%%
mindmap
  root((Datenstrukturen))
    Einfach
      Integer
      Float
      String
      Char
      Bool
    Zusammengesetzt
      Array
      Record
      List
      Set
      Map
    Anschaulich
      Queue
      Stack
      Hash
      Tree
      Graph
```

## Einfache Datentypen

Einfache Datentypen speichern einen einzelnen Wert.

| Typ | Beschreibung | Beispiel |
|---|---|---|
| `int` | Ganzzahl | `42` |
| `float` / `double` | Kommazahl | `3.14` |
| `String` | Zeichenkette | `"Hallo"` |
| `char` | Einzelnes Zeichen | `'A'` |
| `boolean` | Wahrheitswert | `true`, `false` |

## Zusammengesetzte Datentypen

Zusammengesetzte Typen fassen mehrere Werte zusammen.

| Typ | Beschreibung |
|---|---|
| Array | Feste Anzahl von Elementen desselben Typs, direkter Zugriff per Index |
| List | Dynamische Folge von Elementen, Einfügen und Löschen möglich |
| Record | Zusammenfassung verschiedener Typen unter einem Namen (in Java: Klasse oder Record) |
| Set | Menge ohne Duplikate, keine garantierte Reihenfolge |
| Map | Schlüssel-Wert-Paare, Zugriff über Schlüssel |

## Anschauliche Datenstrukturen

Diese Strukturen beschreiben, wie Daten verwaltet werden — nicht nur gespeichert.

| Struktur | Analogie | Verhalten |
|---|---|---|
| Queue | Warteschlange | First In, First Out (FIFO) |
| Stack | Zettelstapel | Last In, First Out (LIFO) |
| Hash | Wörterbuch / Index | Direkter Zugriff über Schlüssel, sehr schnell |
| Tree | Stammbaum | Hierarchische Struktur mit Eltern- und Kindknoten |
| Graph | Straßennetz / Netzwerk | Knoten verbunden durch Kanten, gerichtet oder ungerichtet |

Weiterführend: [Queue](https://de.wikipedia.org/wiki/Warteschlange_(Datenstruktur)) · [Stack](https://de.wikipedia.org/wiki/Stapelspeicher) · [Hashtabelle](https://de.wikipedia.org/wiki/Hashtabelle) · [Baum](https://de.wikipedia.org/wiki/Baum_(Datenstruktur))

### Stack — Ablauf (LIFO)

```kroki
mermaid

%%{init: {'theme': 'base', 'themeVariables': {'background': '#231f20', 'mainBkg': '#3b9689', 'primaryColor': '#3b9689', 'primaryTextColor': '#fff', 'primaryBorderColor': '#70c7ba', 'lineColor': '#70c7ba', 'edgeLabelBackground': '#282425', 'nodeTextColor': '#fff', 'clusterBkg': '#282425'}}}%%
graph TB
    pp(["Push ↓ / Pop ↑"])
    C["C — zuletzt rein, zuerst raus"]
    B["B"]
    A["A — zuerst rein, zuletzt raus"]
    pp --- C --- B --- A
```

Analogie: Ein Stapel Bücher — man nimmt immer das oberste.

### Queue — Ablauf (FIFO)

```kroki
mermaid

%%{init: {'theme': 'base', 'themeVariables': {'background': '#231f20', 'mainBkg': '#3b9689', 'primaryColor': '#3b9689', 'primaryTextColor': '#fff', 'primaryBorderColor': '#70c7ba', 'lineColor': '#70c7ba', 'edgeLabelBackground': '#282425', 'nodeTextColor': '#fff', 'clusterBkg': '#282425'}}}%%
graph LR
    eq(["Enqueue"]) -->|"hinten"| C["C"] --> B["B"] --> A["A"] -->|"vorne"| dq(["Dequeue"])
```

Analogie: Eine Warteschlange — wer zuerst kommt, wird zuerst bedient.

### Linked List — Aufbau

```kroki
mermaid

%%{init: {'theme': 'base', 'themeVariables': {'background': '#231f20', 'mainBkg': '#3b9689', 'primaryColor': '#3b9689', 'primaryTextColor': '#fff', 'primaryBorderColor': '#70c7ba', 'lineColor': '#70c7ba', 'edgeLabelBackground': '#282425', 'nodeTextColor': '#fff', 'clusterBkg': '#282425'}}}%%
graph LR
    A["A"] -->|"next"| B["B"] -->|"next"| C["C"] -->|"next"| D["D"] -->|"next"| N(["null"])
```

Jedes Element (Knoten) enthält einen Wert und einen Zeiger auf das nächste Element. Im Gegensatz zum Array sind Elemente nicht zusammenhängend im Speicher — Einfügen und Löschen ist an beliebiger Stelle schnell, direkter Index-Zugriff aber langsam.

### Binärbaum — Aufbau

```kroki
mermaid

%%{init: {'theme': 'base', 'themeVariables': {'background': '#231f20', 'mainBkg': '#3b9689', 'primaryColor': '#3b9689', 'primaryTextColor': '#fff', 'primaryBorderColor': '#70c7ba', 'lineColor': '#70c7ba', 'edgeLabelBackground': '#282425', 'nodeTextColor': '#fff', 'clusterBkg': '#282425'}}}%%
graph TD
    n8["8"] --> n3["3"]
    n8 --> n10["10"]
    n3 --> n1["1"]
    n3 --> n6["6"]
    n6 --> n4["4"]
    n6 --> n7["7"]
    n10 --> n14["14"]
    n14 --> n13["13"]
```

- Jeder Knoten hat maximal zwei Kinder (links, rechts)
- Im Binary Search Tree (BST): linkes Kind < Elternknoten < rechtes Kind
- Suche, Einfügen, Löschen in O(log n) — deutlich schneller als lineare Suche


## Zeitkomplexität im Vergleich

Wie schnell ist eine Operation? Angabe in [Big-O-Notation](https://de.wikipedia.org/wiki/Landau-Symbole) (Worst Case).

| Struktur | Zugriff | Suche | Einfügen | Löschen |
|---|---|---|---|---|
| Array | O(1) | O(n) | O(n) | O(n) |
| Linked List | O(n) | O(n) | O(1)* | O(1)* |
| Stack | — | O(n) | O(1) | O(1) |
| Queue | — | O(n) | O(1) | O(1) |
| Hash / Map | O(1) | O(1) | O(1) | O(1) |
| Binärbaum (BST) | O(log n) | O(log n) | O(log n) | O(log n) |

\* bei bekannter Position

## Wann welche Datenstruktur?

| Situation | Geeignete Struktur |
|---|---|
| Reihenfolge wichtig, feste Größe | Array |
| Reihenfolge wichtig, variable Größe | List |
| Schnelle Suche über Schlüssel | Map / Hash |
| Keine Duplikate erlaubt | Set |
| Verarbeitung in Reihenfolge des Eintreffens | Queue |
| Rückgängig-Funktion oder verschachtelter Aufruf | Stack |
| Hierarchische Daten (Ordner, Kategorien) | Tree |
| Netzwerke, Routen, Beziehungen zwischen Objekten | Graph |
| Viele Einfüge-/Löschoperationen, kein Index-Zugriff nötig | Linked List |
