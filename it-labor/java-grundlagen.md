---
title: java-grundlagen
description:
published: 1
date: 2026-02-23T07:00:00.000Z
tags:
editor: markdown
dateCreated: 2026-02-23T07:00:00.000Z
---

# Java — Grundlagen

## Hello World

Das erste Java-Programm:

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

Zeile für Zeile:

- `public class Main` — Jedes Java-Programm besteht aus mindestens einer **Klasse**. Der Klassenname muss mit dem Dateinamen übereinstimmen (`Main.java`).
- `public static void main(String[] args)` — Die **main-Methode** ist der Einstiegspunkt: hier startet das Programm. `void` bedeutet, sie gibt nichts zurück.
- `System.out.println(...)` — Gibt Text in der Konsole aus und springt danach in eine neue Zeile. `System.out.print(...)` macht dasselbe ohne Zeilenumbruch.

---

## Variablen

Eine Variable ist ein benannter Speicherplatz für einen Wert. In Java hat jede Variable einen festen **Typ**, der beim Deklarieren angegeben wird.

### Deklaration und Zuweisung

Das Anlegen einer Variable läuft in zwei Schritten:

```java
int alter;       // 1. Deklaration — reserviert Speicher
alter = 20;      // 2. Zuweisung   — schreibt einen Wert hinein
```

Beides geht auch in einer Zeile:

```java
int alter = 20;
```

### Primitive Typen

Primitive Typen speichern ihren Wert **direkt im Stack**.

Der **Stack** ist ein kleiner, schneller Speicherbereich. Lokale Variablen landen dort. Wenn eine Methode endet, werden ihre Stack-Variablen automatisch entfernt. Er funktioniert wie ein Stapel: Werte werden oben draufgelegt und von oben entnommen.

| Typ | Bedeutung | Beispiele |
|---|---|---|
| `int` | Ganze Zahl | `int alter = 20;` · `int punkte = -5;` · `int anzahl = 1000;` |
| `double` | Kommazahl | `double preis = 9.99;` · `double pi = 3.14159;` · `double temp = -2.5;` |
| `char` | Einzelnes Zeichen | `char buchstabe = 'A';` · `char ziffer = '7';` · `char leer = ' ';` |
| `boolean` | Wahrheitswert | `boolean aktiv = true;` · `boolean fertig = false;` · `boolean voll = alter >= 18;` |

Es gibt noch weitere primitive Typen (`byte`, `short`, `long`, `float`), die im Unterricht selten vorkommen.

### Referenztypen

Referenztypen speichern keine Werte direkt — sie speichern eine **Speicheradresse**, die auf ein Objekt im **Heap** zeigt.

Der **Heap** ist ein großer Speicherbereich für Objekte. Objekte können beliebig groß sein und bleiben so lange bestehen, bis Java sie automatisch aufräumt (*Garbage Collection*). Eine Variable vom Referenztyp enthält also nur die Adresse — das eigentliche Objekt liegt woanders im Speicher.

| Typ | Bedeutung | Beispiele |
|---|---|---|
| `String` | Text | `String name = "Anna";` · `String stadt = "Wien";` · `String leer = "";` |
| Array | Liste fixer Länge | `int[] zahlen = {1, 2, 3};` · `String[] namen = {"Anna", "Bob"};` · `double[] w = new double[5];` |
| Objekte | Instanzen von Klassen | `Scanner sc = new Scanner(System.in);` · `Random rng = new Random();` |

Weitere Referenztypen sind z. B. `ArrayList`, `HashMap` und alle selbst geschriebenen Klassen.

**Warum ist `String` großgeschrieben?**
Primitive Typen (`int`, `double`, …) sind eingebaute Sprachkonstrukte — sie werden kleingeschrieben. `String` ist eine Klasse aus der Java-Standardbibliothek, und Klassennamen werden in Java immer mit einem Großbuchstaben geschrieben.

### String-Verkettung (Concatenation)

Strings lassen sich mit `+` zusammensetzen:

```java
String vorname = "Max";
String nachname = "Mustermann";
String vollname = vorname + " " + nachname;       // "Max Mustermann"
System.out.println("Hallo, " + vollname + "!");   // "Hallo, Max Mustermann!"
```

Wird ein primitiver Wert mit `+` an einen String gehängt, wird er automatisch in Text umgewandelt:

```java
int alter = 20;
System.out.println("Alter: " + alter);   // "Alter: 20"
```

---

## Arithmetik

### Grundoperatoren

| Operator | Bedeutung | Beispiel | Ergebnis |
|---|---|---|---|
| `+` | Addition | `5 + 3` | `8` |
| `-` | Subtraktion | `5 - 3` | `2` |
| `*` | Multiplikation | `5 * 3` | `15` |
| `/` | Division | `5 / 2` | `2` (!) |
| `%` | Modulo (Rest) | `5 % 2` | `1` |

### Integer-Division

Wenn beide Operanden `int` sind, schneidet Java bei der Division den Nachkommaanteil einfach ab — es wird nicht gerundet:

```java
int a = 5 / 2;     // 2, nicht 2.5
int b = 7 / 3;     // 2
```

Um ein genaues Ergebnis zu bekommen, muss mindestens ein Operand ein `double` sein:

```java
double c = 5 / 2;     // 2.0 — immer noch Integer-Division! Ergebnis wird danach zu double
double d = 5 / 2.0;   // 2.5 — korrekt
double e = 5.0 / 2;   // 2.5 — auch korrekt
```

### Operator-Priorität (PEMDAS)

Java rechnet nach denselben Regeln wie in der Mathematik:

1. **P**arentheses — Klammern zuerst
2. **E**xponents — Potenzen (in Java: `Math.pow()`)
3. **M**ultiplication / **D**ivision — `*`, `/`, `%` — von links nach rechts
4. **A**ddition / **S**ubtraction — `+`, `-` — von links nach rechts

Beispiel:

```java
double result = 3 + 4 * (8 - 2) / 2;
// Schritt 1: (8 - 2) = 6
// Schritt 2:  4 * 6  = 24
// Schritt 3: 24 / 2  = 12   (Integer-Division: alles int → 12, kein Rest)
// Schritt 4:  3 + 12 = 15
// result = 15.0
```

Mit `2.0` statt `2`:

```java
double result = 3 + 4 * (8 - 2) / 2.0;
// Schritt 3: 24 / 2.0 = 12.0  (double-Division, Ergebnis bleibt double)
// Schritt 4:  3 + 12.0 = 15.0
```

Hier zufällig gleich — bei ungeraden Zwischenergebnissen macht der Unterschied oft was aus.

### Zuweisungsoperatoren

Kurzschreibweisen für häufige Operationen:

| Kurzform | Langform |
|---|---|
| `x += y` | `x = x + y` |
| `x -= y` | `x = x - y` |
| `x *= y` | `x = x * y` |
| `x /= y` | `x = x / y` |
| `x %= y` | `x = x % y` |
| `x++` | `x = x + 1` |
| `x--` | `x = x - 1` |

---

## Benutzereingabe (Scanner)

### Scanner einrichten

Der `Scanner` liest Eingaben von der Konsole. Er kommt aus dem Package `java.util` und muss importiert werden:

```java
import java.util.Scanner;

Scanner scanner = new Scanner(System.in);
```

`System.in` ist der Standard-Eingabekanal (Tastatur). Der Scanner "wickelt" ihn ein und stellt Methoden zum bequemen Lesen bereit.

### Eingabemethoden

```java
String zeile  = scanner.nextLine();    // liest eine ganze Zeile (bis Enter)
String wort   = scanner.next();        // liest ein Wort (bis Leerzeichen oder Enter)
int    zahl   = scanner.nextInt();     // liest eine ganze Zahl
double komma  = scanner.nextDouble();  // liest eine Kommazahl
```

Gibt der Benutzer bei `nextInt()` eine Kommazahl wie `25.3` ein, wirft Java eine `InputMismatchException` — der Scanner erwartet eine ganze Zahl. In diesem Fall `nextDouble()` verwenden.

### Das `\n`-Problem im Input-Buffer

Wenn `nextInt()` oder `nextDouble()` eine Zahl liest, bleibt das abschließende `\n` (Enter-Taste) im Puffer liegen. Ein nachfolgendes `nextLine()` liest dann sofort dieses unsichtbare Zeilenende — und gibt einen leeren String zurück, bevor der Benutzer etwas eingeben konnte:

```java
int alter = scanner.nextInt();
// Puffer enthält jetzt noch: \n

String name = scanner.nextLine();   // liest sofort das \n — name = ""  ← Bug!
```

Lösung: nach `nextInt()` / `nextDouble()` einmal `nextLine()` aufrufen, um den Puffer zu leeren:

```java
int alter = scanner.nextInt();
scanner.nextLine();              // \n wegwerfen
String name = scanner.nextLine(); // jetzt korrekt
```

### Leere Eingabe prüfen

```java
String eingabe = scanner.nextLine();
if (eingabe.isEmpty()) {
    System.out.println("Keine Eingabe.");
}
```

`isEmpty()` gibt `true` zurück, wenn der String die Länge 0 hat (`""`).

### Scanner schließen

```java
scanner.close();
```

Gibt die zugrunde liegende Ressource frei. Gehört ans Ende des Programms, wenn der Scanner nicht mehr gebraucht wird.

---

## If-Bedingungen

```java
if (bedingung) {
    // wird ausgeführt, wenn bedingung true ist
} else if (andereBedingung) {
    // wird ausgeführt, wenn erste false und diese true ist
} else {
    // wird ausgeführt, wenn alle Bedingungen false sind
}
```

Beispiel:

```java
int punkte = 75;

if (punkte >= 90) {
    System.out.println("Sehr gut");
} else if (punkte >= 75) {
    System.out.println("Gut");
} else if (punkte >= 60) {
    System.out.println("Befriedigend");
} else {
    System.out.println("Nicht bestanden");
}
```

Vergleichsoperatoren: `==`, `!=`, `<`, `>`, `<=`, `>=`
Logische Operatoren: `&&` (und), `||` (oder), `!` (nicht)

---

## Math-Klasse und Random

### Math-Klasse

`Math` ist eine Klasse aus der Standardbibliothek — kein Import nötig. Alle Methoden sind statisch, d. h. es wird kein Objekt gebraucht.

```java
double wurzel = Math.sqrt(16);      // 4.0   — Quadratwurzel
double potenz = Math.pow(2, 8);     // 256.0 — 2 hoch 8
int    betrag = Math.abs(-42);      // 42    — absoluter Betrag
double zufall = Math.random();      // Zufallszahl: 0.0 ≤ x < 1.0
```

Zufallszahl in einem bestimmten Bereich:

```java
int zahl = (int) (Math.random() * 100) + 1;   // 1 bis 100
```

`(int)` ist ein **Cast** — er schneidet den Nachkommaanteil ab (kein Runden).

### Random-Klasse

Für mehrere Zufallszahlen ist `java.util.Random` bequemer:

```java
import java.util.Random;

Random rng = new Random();

int    ganzzahl = rng.nextInt(100);       // 0 bis 99
int    bereich  = rng.nextInt(100) + 1;   // 1 bis 100
double komma    = rng.nextDouble();        // 0.0 bis <1.0
```

---

## Formatierte Ausgabe (printf)

`System.out.printf()` gibt Text mit Platzhaltern aus:

```java
System.out.printf("Hallo, %s! Du bist %d Jahre alt.%n", "Anna", 20);
// Ausgabe: Hallo, Anna! Du bist 20 Jahre alt.
```

### Format-Specifiers

| Specifier | Typ | Beispiel | Ausgabe |
|---|---|---|---|
| `%d` | `int` | `printf("%d", 42)` | `42` |
| `%f` | `double` | `printf("%f", 3.14)` | `3.140000` |
| `%.2f` | `double`, 2 Nachkommastellen | `printf("%.2f", 3.14159)` | `3.14` |
| `%s` | `String` | `printf("%s", "Hi")` | `Hi` |
| `%c` | `char` | `printf("%c", 'A')` | `A` |
| `%n` | Zeilenumbruch | `printf("Zeile%n")` | `Zeile` + Umbruch |

`%.2f` — der Punkt steht für "Nachkommastellen", die Zahl dahinter gibt die Anzahl an.

```java
double preis = 4.5;
int anzahl = 3;
System.out.printf("%.2f € × %d = %.2f €%n", preis, anzahl, preis * anzahl);
// Ausgabe: 4.50 € × 3 = 13.50 €
```

---

## String-Methoden

```java
String s = "Hallo, Welt!";

s.length()             // 12      — Anzahl Zeichen
s.charAt(0)            // 'H'     — Zeichen an Position 0
s.indexOf("Welt")      // 7       — erste Position des Teilstrings (-1 wenn nicht gefunden)
s.lastIndexOf("l")     // 10      — letzte Position von "l"
s.toUpperCase()        // "HALLO, WELT!"
s.toLowerCase()        // "hallo, welt!"
s.contains("Welt")     // true
s.startsWith("Ha")     // true
s.endsWith("!")        // true
s.substring(7, 11)     // "Welt"  — von Index 7 bis 10 (Endindex exklusiv)
```

**Wichtig:** Strings sind in Java unveränderlich (*immutable*). Methoden wie `toUpperCase()` verändern den Original-String nicht — sie geben einen neuen String zurück:

```java
String original = "hallo";
original.toUpperCase();                    // wirkungslos
String gross = original.toUpperCase();     // korrekt: Ergebnis speichern
```

---

## Substrings

```java
String s = "Hallo, Welt!";

s.substring(7);        // "Welt!" — ab Index 7 bis zum Ende
s.substring(7, 11);    // "Welt"  — von Index 7 bis 10 (Endindex exklusiv)
```

Kombination mit `indexOf()` — praktisch für strukturierte Strings:

```java
String email = "max.mustermann@gmail.com";

String domain = email.substring(email.indexOf("@") + 1);
// indexOf("@") = 15  →  + 1 = 16  →  ab Index 16
// domain = "gmail.com"

String lokalteil = email.substring(0, email.indexOf("@"));
// lokalteil = "max.mustermann"
```

---

## Ternärer Operator

Kurzform für eine einfache if-else-Zuweisung:

```java
// Langform:
String ergebnis;
if (punkte >= 60) {
    ergebnis = "Bestanden";
} else {
    ergebnis = "Nicht bestanden";
}

// Kurzform:
String ergebnis = punkte >= 60 ? "Bestanden" : "Nicht bestanden";
```

Syntax: `bedingung ? wertWennTrue : wertWennFalse`

Gut lesbar bei einfachen Fällen. Bei verschachtelter Logik lieber normale if-else-Form.

---

## Switch Statement

Switch vergleicht eine Variable gegen mehrere feste Werte:

```java
int tag = 3;

switch (tag) {
    case 1:
        System.out.println("Montag");
        break;
    case 2:
        System.out.println("Dienstag");
        break;
    case 3:
        System.out.println("Mittwoch");
        break;
    case 4:
        System.out.println("Donnerstag");
        break;
    case 5:
        System.out.println("Freitag");
        break;
    default:
        System.out.println("Wochenende");
}
```

- `break` beendet den Switch-Block. Fehlt es, fällt Java in den nächsten `case` durch (*fall-through*) — fast immer ein Bug.
- `default` wird ausgeführt, wenn kein `case` passt. Optional, aber empfohlen.

Switch funktioniert mit `int`, `char`, `String` und Enums.

---

## Zugriffsmodifikatoren

Java kontrolliert, wer auf Klassen, Methoden und Variablen zugreifen darf — mit **Zugriffsmodifikatoren** (Access Modifiers). Das ist ein zentrales Konzept der objektorientierten Programmierung.

| Modifier | Sichtbarkeit |
|---|---|
| `private` | Nur innerhalb **derselben Klasse** |
| `package-private` *(kein Modifier)* | Innerhalb desselben **Packages** |
| `protected` | Im Package **und** in Unterklassen |
| `public` | **Überall** zugänglich |

### Faustregel: Variablen immer `private`

Attribute (Felder) einer Klasse sollten **immer `private`** sein. Nur die eigene Klasse darf direkt auf ihren internen Zustand zugreifen. Nach außen werden Werte über Methoden (Getter/Setter) zugänglich gemacht.

```java
public class Konto {
    private double kontostand;   // private — nur Konto darf direkt darauf zugreifen

    public double getKontostand() {
        return kontostand;       // nach außen über Methode zugänglich
    }

    public void einzahlen(double betrag) {
        if (betrag > 0) {
            kontostand += betrag;
        }
    }
}
```

Wäre `kontostand` public, könnte jede andere Klasse den Wert direkt setzen — auch auf ungültige Werte wie `-9999`. `private` schützt den internen Zustand.

### Vergleich mit dem lg1-Projekt

In `ZahlenRaten.java` sind alle Methoden `public`, weil sie von außen (z. B. von der Testklasse oder der `main`-Methode) aufgerufen werden müssen:

```java
public int generiereZahl() { ... }   // public — Testklasse ruft sie auf
public int genauGeraten(...) { ... } // public — Testklasse ruft sie auf
public void start() { ... }          // public — Einstiegspunkt von außen
```

Wenn eine Hilfsmethode nur intern gebraucht wird, sollte sie `private` sein — dann ist sofort klar, dass sie ein Implementierungsdetail ist und nicht Teil der öffentlichen Schnittstelle.

### Methoden: public vs. private

| | `public` | `private` |
|---|---|---|
| Wer darf aufrufen? | Jeder | Nur die Klasse selbst |
| Wann verwenden? | Schnittstelle nach außen | Interne Hilfslogik |
| Testbar von außen? | Ja | Nein — wird indirekt durch `public`-Methoden getestet |
