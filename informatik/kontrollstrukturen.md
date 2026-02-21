# Kontrollstrukturen

Kontrollstrukturen bestimmen den Ablauf eines Programms. Es gibt drei Grundstrukturen (siehe [Phasenmodell](phasenmodell)).

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

Die Bedingung wird **vor** jedem Durchlauf geprüft. Ist sie von Anfang an falsch, wird der Block nie ausgeführt.

```java
// Zahlen 1 bis 5 ausgeben
int i = 1;
while (i <= 5) {
    System.out.println(i);
    i++;
}
```

### Fußgesteuerte Schleife (nicht abweisend)

Die Bedingung wird **nach** jedem Durchlauf geprüft. Der Block wird mindestens einmal ausgeführt.

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
