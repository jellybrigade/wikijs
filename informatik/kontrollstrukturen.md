# Kontrollstrukturen

Kontrollstrukturen bestimmen den Ablauf eines Programms. Es gibt drei Grundstrukturen (siehe [Phasenmodell](phasenmodell.md)).

## Algorithmus

Ein **Algorithmus** ist eine eindeutige, endliche Schrittfolge zur Lösung eines Problems.

### Merkmale

| Merkmal | Bedeutung |
|---|---|
| Endlich | Besteht aus einer begrenzten Anzahl von Schritten |
| Eindeutig | Jeder Schritt ist klar und unmissverständlich definiert |
| Deterministisch | Bei gleichen Eingaben immer das gleiche Ergebnis |
| Terminiert | Kommt nach endlicher Zeit zu einem Ende |
| Ausführbar | Jeder Schritt ist tatsächlich durchführbar |

### Bausteine

Jeder Algorithmus besteht aus einer Kombination von:

- **Sequenzen** — Abfolgen von Anweisungen
- **Verzweigungen** — Bedingungen (Ja/Nein)
- **Schleifen** — Wiederholungen

## PAP — Programmablaufplan

Ein PAP ist eine **grafische Darstellung von Programmabläufen** mit genormten Symbolen. Er wird verwendet, um Algorithmen vor der Implementierung zu planen und zu visualisieren.

### Symbole

| Symbol | Name | Verwendung |
|---|---|---|
| Rechteck | Verarbeitung | Anweisung oder Berechnung |
| Parallelogramm | Ein-/Ausgabe | Daten einlesen oder ausgeben |
| Raute | Verzweigung | Bedingung mit Ja/Nein-Zweig |
| Oval / abgerundetes Rechteck | Grenzstelle | Start oder Ende des Programms |
| Kleiner Kreis | Verbinder | Verbindet zwei Stellen im Plan (z. B. Seitenumbruch) |
| Rechteck mit doppelten Seitenlinien | Unterprogramm | Aufruf eines Teilprogramms |
| Trapez | Manuelle Verarbeitung | Manueller Eingriff (z. B. Benutzereingabe) |

### Tools

| Tool | Plattform |
|---|---|
| PAP Designer | Windows |
| [app.diagrams.net](https://app.diagrams.net) | Web |

## Sequenz (Anweisungsfolge)

Anweisungen werden der Reihe nach ausgeführt.

```java
// Fläche eines Rechtecks berechnen
int breite = 5;
int hoehe = 3;
int flaeche = breite * hoehe;
```

## Selektion (Auswahlstruktur)

### Einfache Alternative

```java
// Note ausgeben
if (punkte >= 90) {
    System.out.println("Sehr gut");
} else if (punkte >= 75) {
    System.out.println("Gut");
} else {
    System.out.println("Nicht bestanden");
}
```

### Mehrfache Alternative

```java
// Wochentag ausgeben
switch (tag) {
    case 1:
        System.out.println("Montag");
        break;
    case 2:
        System.out.println("Dienstag");
        break;
    default:
        System.out.println("Anderer Tag");
        break;
}
```

`switch` eignet sich, wenn eine Variable gegen mehrere feste Werte geprüft wird. `if-else` ist flexibler und erlaubt beliebige Bedingungen.

## Iteration (Wiederholungsstruktur)

### Kopfgesteuerte Schleife (abweisend)

Die Bedingung wird **vor** jedem Durchlauf geprüft. Ist sie von Anfang an falsch, wird der Block nie ausgeführt — der Schleifeninhalt kann **0-mal** ausgeführt werden.

> Im PAP: Die Bedingungsraute steht **vor** dem Wiederholungsteil.

```java
// Zahlen 1 bis 5 ausgeben
int i = 1;
while (i <= 5) {
    System.out.println(i);
    i++;
}
```

### Fußgesteuerte Schleife (nicht abweisend)

Die Bedingung wird **nach** jedem Durchlauf geprüft. Der Block wird **mindestens einmal** ausgeführt.

> Im PAP: Die Bedingungsraute steht **nach** dem Wiederholungsteil.

> **Achtung:** Eine Schleife im PAP hat entweder eine Kopfbedingung **oder** eine Fußbedingung — niemals beides.

```java
// Eingabe wiederholen bis gültig
int eingabe;
do {
    eingabe = scanner.nextInt();
} while (eingabe < 0);
```

### Zählschleife

`for` ist eine kompakte Kurzform für eine kopfgesteuerte Schleife mit Zähler.

```java
// Summe von 1 bis 10 berechnen
int summe = 0;
for (int i = 1; i <= 10; i++) {
    summe += i;
}
```

Äquivalent als `while`:

```java
int summe = 0;
int i = 1;
while (i <= 10) {
    summe += i;
    i++;
}
```
