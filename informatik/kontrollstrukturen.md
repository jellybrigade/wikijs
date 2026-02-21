# Kontrollstrukturen

Kontrollstrukturen bestimmen den Ablauf eines Programms. Es gibt drei Grundstrukturen (siehe [Phasenmodell](phasenmodell.md)).

## Sequenz (Anweisungsfolge)

Anweisungen werden der Reihe nach ausgeführt.

```java
int a = 5;
int b = 3;
int summe = a + b;
```

## Selektion (Auswahlstruktur)

### Einfache Alternative

```java
if (bedingung) {
    // Anweisung A
} else if (andereBedingung) {
    // Anweisung B
} else {
    // Anweisung C
}
```

### Mehrfache Alternative

```java
switch (ausdruck) {
    case A1:
        // Anweisung 1
        break;
    case A2:
        // Anweisung 2
        break;
    default:
        // Anweisung Else
        break;
}
```

`switch` eignet sich, wenn eine Variable gegen mehrere feste Werte geprüft wird. `if-else` ist flexibler und erlaubt beliebige Bedingungen.

## Iteration (Wiederholungsstruktur)

### Kopfgesteuerte Schleife (abweisend)

Die Bedingung wird **vor** jedem Durchlauf geprüft. Ist sie von Anfang an falsch, wird der Block nie ausgeführt.

```java
while (bedingung) {
    // Anweisung
}
```

### Fußgesteuerte Schleife (nicht abweisend)

Die Bedingung wird **nach** jedem Durchlauf geprüft. Der Block wird mindestens einmal ausgeführt.

```java
do {
    // Anweisung
} while (bedingung);
```

### Zählschleife

`for` ist eine kompakte Kurzform für eine kopfgesteuerte Schleife mit Zähler.

```java
for (int i = 0; i < n; i++) {
    // Anweisung
}
```

Äquivalent als `while`:

```java
int i = 0;
while (i < n) {
    // Anweisung
    i++;
}
```
