# Imperative Programmierung

## Definition

**Imperativ** (von lat. imperare = befehlen) bedeutet:

> "Sag dem Computer exakt was zu tun ist"

Fokus auf **WIE** (Schritte), nicht **WAS** (Ziel).

## Charakteristiken

### 1. Explizite Anweisungen

```java
// Imperativ: Sag GENAU was zu tun ist
int sum = 0;
int[] numbers = {1, 2, 3, 4, 5};
for (int i = 0; i < numbers.length; i++) {
  sum += numbers[i];  // Schritt für Schritt
}
System.out.println(sum);
```

### 2. Zustandsänderungen (Mutation)

Variablen ändern ihren Wert:

```java
int x = 5;
x = x + 3;  // x ändert von 5 auf 8
x = x * 2;  // x ändert von 8 auf 16
```

### 3. Kontrollfoss-Fokus

If-Else, Schleifen, Funktionen:

```java
if (userLoggedIn) {
  openDashboard();
} else {
  showLoginForm();
}

for (int i = 0; i < 10; i++) {
  // Wiederhole
}

while (running) {
  update();
  render();
}
```

## Vorteile

- ✓ **Direkt**: Ausdrückt genau was passiert
- ✓ **Kontrolliert**: Volle Kontrolle über Ausführung
- ✓ **Performant**: Gut für Low-Level Operationen
- ✓ **Intuitiv**: Ähnlich wie alltägliche Anweisungen

## Nachteile

- ✗ **Verbose**: Viel Code für einfache Logik
- ✗ **Fehleranfällig**: Leicht Fehler in Schritte
- ✗ **Schwierig zu testen**: Zustand kompliziert
- ✗ **Parallelisierung**: Nebenläufigkeit schwierig

## Beispiel: Problem lösen (Imperativ)

**Aufgabe**: Finde die Summe aller geraden Zahlen in einer Liste.

```java
// Imperativ
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
int sum = 0;

for (int i = 0; i < numbers.size(); i++) {
  if (numbers.get(i) % 2 == 0) {  // Nur gerade
    sum += numbers.get(i);         // Addiere
  }
}

System.out.println(sum);  // Output: 12 (2+4+6)
```

**WIE: Iterate, check, add**

## Vergleich: Imperativ vs Deklarativ

```java
// Imperativ (WIE?)
int sum = 0;
for (int num : numbers) {
  if (num % 2 == 0) {
    sum += num;
  }
}

// Deklarativ / Funktional (WAS?)
int sum = numbers.stream()
  .filter(n -> n % 2 == 0)
  .mapToInt(n -> n)
  .sum();
```

Beide geben gleich result, aber unterschiedliche Ansätze!

## Imperativ in Java

Java ist primär **imperativ**:

```java
class BankAccount {
  private double balance = 0;  // Zustand

  void deposit(double amount) {
    balance += amount;  // Zustand ändern
  }

  void withdraw(double amount) {
    if (amount <= balance) {
      balance -= amount;  // Zustand ändern
    }
  }
}

// Imperativ Nutzung
BankAccount acc = new BankAccount();
acc.deposit(100);    // Anweisung 1
acc.withdraw(30);    // Anweisung 2
System.out.println(acc.getBalance());  // 70
```

## Zusammenfassung

**Imperativ**:
- WIE (Schritte zur Lösung)
- Explizite Anweisungen
- Zustandsänderung
- Kontrollfluss-fokussiert

**Gut für**: Systemnahe Programmierung, Algorithmen, Kontrolle

**Nicht ideal für**: Funktionale Programmierung, Nebenläufigkeit, Deklarative Systeme

Siehe auch: [Programmiermodelle Überblick](Einfuehrung.md), [Prozedural](Prozedural.md)
