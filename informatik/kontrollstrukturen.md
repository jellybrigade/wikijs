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

![Beispiel-Ablaufprogramm](../assets/images/Beispiel-Ablaufprogramm.jpg)

## Warum PAP und Struktogramm?

Beide Darstellungsformen beschreiben denselben Algorithmus — aus unterschiedlichen Perspektiven.

| | PAP (Programmablaufplan) | Struktogramm (Nassi-Shneidermann) |
|---|---|---|
| **Entstehung** | 1930er Jahre; in den 1960ern standardisiert | 1970er Jahre, als Reaktion auf "Spaghetti-Code" |
| **Ausrichtung** | Flussorientiert — folgt dem Kontrollfluss | Blockorientiert — zeigt die Struktur des Codes |
| **Zweck** | Visualisierung von Prozessen und einfachen Algorithmen | Erzwingt strukturierte Programmierung (nur erlaubte Kontrollstrukturen) |
| **Heute** | Noch gelegentlich in der Industrie | Kaum noch in Verwendung, eher in der Schule |

In der modernen Softwareentwicklung hat **UML** (Unified Modeling Language) beide weitgehend abgelöst — mit speziellen Diagrammtypen für Klassenstrukturen, Abläufe, Zustände und mehr.

> **Prüfungsrelevant:** Die Umwandlung PAP → Struktogramm und Struktogramm → PAP kommt zum Test. Beide Richtungen üben.

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

## Zusammengesetzte Bedingungen

Eine Bedingung ist immer entweder `true` oder `false`. Mit logischen Operatoren lassen sich mehrere Bedingungen verknüpfen:

| Operator | Name | Bedeutung |
|---|---|---|
| `&&` | Logisches UND | `true`, wenn **beide** Bedingungen `true` sind |
| `\|\|` | Logisches ODER | `true`, wenn **mindestens eine** Bedingung `true` ist |
| `!` | Logisches NICHT | Kehrt den Wahrheitswert um |

```java
// ((B1 && B2) || B3)
boolean b1 = punkte >= 50;
boolean b2 = anwesenheit >= 80;
boolean b3 = sondergenehmigung;

if ((b1 && b2) || b3) {
    System.out.println("Bestanden");
}
```

### Auswertungsreihenfolge

Java wertet zusammengesetzte Bedingungen in dieser Reihenfolge aus:

1. `!` — zuerst
2. `&&` — dann
3. `||` — zuletzt

Bei `B1 && B2 || B3 && !B4` wird also zuerst `!B4` ausgewertet, dann beide `&&`-Verbindungen, dann das `||`. **Klammernsetzung schadet nicht** — gerade wenn es komplexer wird, macht eine explizite Klammer die Absicht sofort klar.

### Praxisbeispiele

**Einlasskontrolle (UND-Logik):** Beide Bedingungen müssen erfüllt sein.

```java
// Über 18 AND (Ticket OR Gästeliste)
if (alter >= 18 && (hatTicket || stehtAufGaesteliste)) {
    System.out.println("Einlass gewährt");
}
```

**Ausnahmeregel (ODER-Logik):** Es wird nach *einem Grund* gesucht, jemanden reinzulassen — sobald einer gefunden ist, wird abgebrochen.

```java
// Besitzer OR Gästeliste OR Ticket
if (istBesitzer || stehtAufGaesteliste || hatTicket) {
    System.out.println("Einlass gewährt");
} else {
    System.out.println("Kein Einlass");
}
```

**Null-Check bei ArrayList:** Die Reihenfolge kann einen Unterschied machen — nicht nur logisch, sondern auch für die Stabilität des Programms.

```java
ArrayList<String> list = new ArrayList<>();

// FALSCH — wenn list null ist, wirft list.size() eine NullPointerException
// bevor die null-Prüfung überhaupt erreicht wird:
if (list.size() > 0 && list != null) { ... }

// RICHTIG — null zuerst prüfen:
if (list != null && list.size() > 0) { ... }
```

Java wertet `&&` von links nach rechts aus (*Short-Circuit-Evaluation*): Ist die linke Seite `false`, wird die rechte gar nicht mehr ausgewertet. Das spart Zeit — und verhindert Fehler. Bei `||` gilt das Gleiche in die andere Richtung — ist die linke Seite bereits `true`, wird die rechte übersprungen.

**Spielkauf (kombinierte Logik):** Bedingungen mit `&&` und `||` lassen sich verschachteln. Short-Circuit greift auf beiden Ebenen:

```java
// Kaufen erlaubt, wenn: (Alter > 16 UND Spiel nicht indiziert) ODER Zertifikat vorhanden
if ((alter > 16 && !aufIndex) || hatZertifikat) {
    kaufen();
} else {
    nichtKaufen();
}
// Sobald hatZertifikat == true, wird (alter > 16 && !aufIndex) gar nicht mehr geprüft.
```

### Entscheidungstabellen

Entscheidungstabellen sind das **mächtigste Mittel**, um komplexe Abhängigkeiten zwischen Bedingungen und Aktionen **übersichtlich, vollständig und widerspruchsfrei** darzustellen. Sie zeigen auf einen Blick, welche Kombinationen welche Aktionen auslösen — und ob es Lücken oder Widersprüche gibt.

**Vorgehen:**
1. Bedingungen und Aktionen identifizieren
2. Vollständige Tabelle aufstellen (alle Kombinationen)
3. Tabelle reduzieren
4. Else-Regel anwenden

#### Wie viele Regeln?

Bei Ja/Nein-Bedingungen: **2^n** (n = Anzahl der Bedingungen).
Bei gemischten Wertebereichen: **Produkt aller Varianten** — z.B. 2 × Ja/Nein-Bedingungen + 1 × A/B/C-Bedingung: 2² × 3¹ = 12 Regeln.

#### Beispiel: Spielkauf

Bedingungen: B1 Zertifikat?, B2 Alter > 16?, B3 Auf Index?
Aktionen: Kaufen, Nicht kaufen
Anzahl Regeln: 2³ = 8

Systematisches Befüllen: 4× J / 4× N → 2× J / 2× N → abwechselnd J / N:

| Bedingungen       | R1 | R2 | R3 | R4 | R5 | R6 | R7 | R8 |
|---|---|---|---|---|---|---|---|---|
| B1: Zertifikat?   | J  | J  | J  | J  | N  | N  | N  | N  |
| B2: Alter > 16?   | J  | J  | N  | N  | J  | J  | N  | N  |
| B3: Auf Index?    | J  | N  | J  | N  | J  | N  | J  | N  |
| **Kaufen**        | x  | x  | x  | x  |    | x  |    |    |
| **Nicht kaufen**  |    |    |    |    | x  |    | x  | x  |

> **Wichtigste Regel zuerst:** Wer ein Zertifikat hat, darf immer kaufen. Diese Regel kommt nach oben — sobald B1 = J, müssen B2 und B3 nicht mehr geprüft werden.

#### Reduktion

**Regel:** Zwei Regeln lassen sich zusammenfassen, wenn sie **dieselbe Aktion** auslösen und sich nur in **einer Bedingung** unterscheiden. Diese Bedingung wird dann mit `-` (= „Don't care") markiert.

**Schritt 1:** R1/R2 unterscheiden sich nur in B3, ebenso R3/R4 und R7/R8:

| Bedingungen       | R1/R2 | R3/R4 | R5 | R6 | R7/R8 |
|---|---|---|---|---|---|
| B1: Zertifikat?   | J     | J     | N  | N  | N     |
| B2: Alter > 16?   | J     | N     | J  | J  | N     |
| B3: Auf Index?    | -     | -     | J  | N  | -     |
| **Kaufen**        | x     | x     |    | x  |       |
| **Nicht kaufen**  |       |       | x  |    | x     |

**Schritt 2:** R1/R2 und R3/R4 unterscheiden sich nur in B2:

| Bedingungen       | R1–R4 | R5 | R6 | R7/R8 |
|---|---|---|---|---|
| B1: Zertifikat?   | J     | N  | N  | N     |
| B2: Alter > 16?   | -     | J  | J  | N     |
| B3: Auf Index?    | -     | J  | N  | -     |
| **Kaufen**        | x     |    | x  |       |
| **Nicht kaufen**  |       | x  |    | x     |

> Diese Tabelle ist die **Testtabelle** — sie listet alle relevanten Testfälle auf.

#### Else-Regel

Führen mehrere Regeln zur **selben Aktion** und haben sie keine eigene Bedingungskombination, werden sie zur **Else-Regel** zusammengefasst. Hier: R5 und R7/R8 führen immer zu „Nicht kaufen":

| Bedingungen       | Spezial (R1–R4) | Normal (R6) | ELSE |
|---|---|---|---|
| B1: Zertifikat?   | J               | N           | -    |
| B2: Alter > 16?   | -               | J           | -    |
| B3: Auf Index?    | -               | N           | -    |
| **Kaufen**        | x               | x           |      |
| **Nicht kaufen**  |                 |             | x    |

#### Implementierung

```java
if (hatZertifikat) {
    kaufen();
} else if (alter > 16 && !aufIndex) {
    kaufen();
} else {
    nichtKaufen();
}
```

Oder kompakt mit Short-Circuit:

```java
if (hatZertifikat || (alter > 16 && !aufIndex)) {
    kaufen();
} else {
    nichtKaufen();
}
```

### Aufgaben

| Aufgabe | Bedingung |
|---|---|
| Rabatt nur für Kunden mit Treuekonto **und** Einkaufswert über 100 € | `hatTreuekonto && einkaufswert > 100` |
| Schüler darf am Ausflug teilnehmen, wenn er eine Einverständniserklärung hat **oder** volljährig ist | `hatEinverstaendnis \|\| istVolljährig` |

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

### Schleifen vorzeitig beenden

Mit drei Schlüsselwörtern kann man den normalen Ablauf einer Schleife unterbrechen:

| Schlüsselwort | Wirkung |
|---|---|
| `break` | Beendet die Schleife sofort |
| `continue` | Überspringt den Rest des aktuellen Durchlaufs, startet den nächsten |
| `return` | Beendet die gesamte Methode (und damit auch die Schleife) |

> **Wichtig:** `return` gehört in Funktionen, nicht in Schleifen. Wer nur die Schleife verlassen will, verwendet `break`. `return` beendet die gesamte Methode — das ist selten die Absicht, wenn man sich mitten in einer Schleife befindet.

```java
// break: Schleife abbrechen, sobald Wert gefunden
for (int i = 0; i < zahlen.length; i++) {
    if (zahlen[i] == gesuchteZahl) {
        System.out.println("Gefunden bei Index " + i);
        break; // Schleife sofort verlassen
    }
}

// continue: Negative Zahlen überspringen
for (int zahl : zahlen) {
    if (zahl < 0) continue; // direkt zur nächsten Iteration springen
    System.out.println(zahl);
}
```
