# Programmierparadigmen

Ein Programmierparadigma ist das grundlegende Denkmodell, nach dem ein Programm aufgebaut wird. Verschiedene Sprachen können mehrere Paradigmen unterstützen.

## Vergleich

| Paradigma | Kernidee | Vertreter |
|---|---|---|
| Imperativ | Anweisung für Anweisung, Sprungbefehle | Assembler, Fortran |
| Prozedural | Aufteilung in Unterprogramme, Daten getrennt von Logik | Pascal, Delphi, C |
| Objektorientiert | Alles ist ein Objekt mit Zustand und Verhalten | Java, C#, Python |
| Funktional | Funktionen als Werte, keine Seiteneffekte | Lisp, Scala, Haskell |
| Logisch | Fakten und Regeln, Ergebnis wird hergeleitet | Prolog |

## Imperativ

Das älteste Paradigma: Das Programm ist eine Folge von Anweisungen, die der Computer der Reihe nach ausführt. Sprünge (`goto`) ermöglichen Verzweigungen. Führt ohne Disziplin zu unübersichtlichem "Spaghetti Code" — der Hauptgrund für die strukturierte Programmierung (siehe [Phasenmodell](phasenmodell.md)).

## Prozedural

Eine Weiterentwicklung des imperativen Paradigmas. Das Programm wird in **Prozeduren** (Unterprogramme) aufgeteilt, die vom Hauptprogramm aufgerufen werden. Daten und Logik sind getrennt. Das macht Programme übersichtlicher und wiederverwendbar.

## Objektorientiert

Das Programm besteht aus **Objekten**, die Daten (Attribute) und Verhalten (Methoden) kapseln. Jedes Objekt ist eine Instanz einer **Klasse** und hat drei Eigenschaften:

- **Identität** — jedes Objekt ist eindeutig unterscheidbar, auch wenn zwei Objekte dieselben Attributwerte haben
- **Zustand** — die aktuellen Werte der Attribute
- **Verhalten** — die Methoden, die das Objekt ausführen kann

Aufbau einer Klasse:

| Teil | Beschreibung |
|---|---|
| Attribut | Eigenschaft des Objekts, typisch `private` |
| Methode | Funktion, die auf dem Objekt operiert |
| Konstruktor | Spezielle Methode zum Erstellen einer Instanz |

Beispiel-Analogie aus dem Unterricht: Die Klasse `Schueler` hat Attribute wie `name`, `alter`, `geschlecht` und Methoden wie `lernen()`, `schlafen()`. Zwei Instanzen dieser Klasse (zwei Schüler) teilen dieselbe Struktur, haben aber unterschiedliche Attributwerte.

Das zentrale Prinzip ist **Kapselung (Encapsulation):** Attribute sind nach außen verborgen (`private`), der Zugriff erfolgt nur über Methoden.

**Vererbung** ermöglicht es einer Klasse, Eigenschaften und Methoden einer anderen Klasse zu übernehmen und zu erweitern — ohne den Code zu duplizieren.

Weiterführend: [Vererbung (Wikipedia)](https://de.wikipedia.org/wiki/Vererbung_(Programmierung)) · [Polymorphismus (Wikipedia)](https://de.wikipedia.org/wiki/Polymorphie_(Programmierung))

## Funktional

Im funktionalen Paradigma sind Funktionen gleichwertige Werte — sie können als Argumente übergeben, zurückgegeben und gespeichert werden (First-Class Functions). Das Paradigma basiert auf dem Konzept mathematischer Funktionen: Der Rückgabewert hängt ausschließlich von den übergebenen Argumenten ab, nicht von einem externen Zustand.

- Variablen sind **unveränderlich** — einmal gesetzt, nicht mehr änderbar
- Keine Seiteneffekte: Eine Funktion verändert nichts außerhalb ihres Scopes
- Der Fokus liegt auf dem **Ergebnis** (was berechnet wird), nicht auf dem Prozess (wie)
- Schleifen und klassische bedingte Anweisungen werden vermieden — stattdessen Rekursion und Ausdrücke

Vertreter: Lisp, Scala, Haskell

## Logisch

Logische Programme bestehen aus **Fakten** und **Regeln**. Anstatt einen Lösungsweg zu beschreiben, wird das Problem als logische Aussage formuliert — das System leitet die Antwort selbst her. Prolog ist die bekannteste logische Sprache und findet Anwendung in KI und natürlicher Sprachverarbeitung.
