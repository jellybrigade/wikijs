# Kontrollstrukturen: Überblick

## Was sind Kontrollstrukturen?

**Kontrollstrukturen** bestimmen die **Reihenfolge** in der Anweisungen ausgeführt werden.

Ohne Kontrollstrukturen wäre alles linear:

```
Schritt 1
Schritt 2
Schritt 3
Schritt 4
... (langweilig!)
```

Mit Kontrollstrukturen:

```
Schritt 1
FALLS Bedingung: Schritt 2a
SONST: Schritt 2b
WIEDERHOLE: Schritte 3-5
Schritt 6
```

## Die 3 Grundstrukturen (Böhm-Jacopini Theorem)

### 1. Sequenz (Anweisungsfolge)

Nacheinander, keine Verzweigung:

```
Aktion 1 → Aktion 2 → Aktion 3
```

Code:
```java
x = 5;
y = x + 3;
System.out.println(y);
```

### 2. Selektion (Auswahlstruktur)

Abhängig von Bedingung:

```
    WENN Bedingung
    ├─ JA: Weg A
    └─ NEIN: Weg B
```

Code:
```java
if (x > 5) {
  System.out.println("x ist groß");
} else {
  System.out.println("x ist klein");
}
```

### 3. Iteration (Wiederholungsstruktur)

Wiederhole solange Bedingung erfüllt:

```
    WIEDERHOLE solange Bedingung
    ├─ Aktion
    └─ Bedingung neu überprüfen
```

Code:
```java
while (i < 10) {
  System.out.println(i);
  i++;
}
```

## Wichtiger Satz

**Böhm-Jacopini Theorem:**

> Mit nur diese 3 Grundstrukturen können wir JEDEN Algorithmus implementieren!
> GO TO ist überflüssig.

Das heißt: Du brauchst keine komplexen Kontrollfluss-Tricks!

Strukturierte Kontrollstrukturen = lesbarer, wartbarer Code.

## Übersicht aller Kontrollstrukturen in Java

### If-Else (Selektion)

```java
if (condition) {
  // Code wenn true
} else if (otherCondition) {
  // Code wenn otherCondition true
} else {
  // Code sonst
}
```

### Switch-Case (Multiple Selektion)

```java
switch (day) {
  case 1: System.out.println("Montag"); break;
  case 2: System.out.println("Dienstag"); break;
  default: System.out.println("Anderer Tag");
}
```

### While (Kopfgesteuerte Schleife)

```java
while (condition) {
  // Wird ausgeführt solange condition true
  // Kann 0x ausgeführt werden
}
```

### Do-While (Fußgesteuerte Schleife)

```java
do {
  // Wird mindestens 1x ausgeführt
} while (condition);
```

### For (Zählschleife)

```java
for (int i = 0; i < 10; i++) {
  // i läuft von 0 bis 9
}

// Auch über Objekte
for (String item : list) {
  // Für jeden item in list
}
```

## Entscheidungsbaum

```
Brauchst du Kontrollfluss?

├─ Einfach zwei Wege?
│  └─ if-else
│
├─ Mehrere Wege (>2)?
│  └─ if-else-if-else oder switch
│
├─ Unbekannte Wiederholungen?
│  └─ while oder do-while
│
└─ Bekannte Anzahl Wiederholungen?
   └─ for
```

## Beispiel: Güteklasse berechnen

```java
int note = 85;

// Selektion: Welche Klasse?
if (note >= 90) {
  System.out.println("A");
} else if (note >= 80) {
  System.out.println("B");
} else if (note >= 70) {
  System.out.println("C");
} else {
  System.out.println("F");
}

// Mit Switch
switch (note / 10) {
  case 9: System.out.println("A"); break;
  case 8: System.out.println("B"); break;
  case 7: System.out.println("C"); break;
  default: System.out.println("F");
}
```

## Nesting (Verschachtelung)

Kontrollstrukturen können geschachtelt werden:

```java
for (int i = 0; i < 5; i++) {
  for (int j = 0; j < 5; j++) {
    if (i == j) {
      System.out.println("Diagonal");
    }
  }
}
```

**Vorsicht**: Zu viel Nesting = unlesbarer Code!

Regel: Max 3 Nesting-Level.

## Zusammenfassung

- **Sequenz**: Linear
- **Selektion**: If-Else, Switch
- **Iteration**: For, While, Do-While
- **Böhm-Jacopini**: Diese 3 genügen für alles
- **Strukturiert**: Sauberer als GO TO

Siehe auch: [Selektion](Selektion.md), [Iteration](Iteration.md)
