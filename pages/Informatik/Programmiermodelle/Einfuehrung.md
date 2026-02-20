# Programmiermodelle: Übersicht

## Was sind Programmiermodelle?

Ein **Programmiermodell** (oder Paradigma) ist eine Philosophie zum Programmieren:

> Wie denke ich über ein Problem?
> Wie struktur ich meinen Code?
> Welche Abstraktion nutze ich?

## Die 5 Hauptmodelle

### 1. Imperativ (Befehlsorientiert)

> "Sag dem Computer EXAKT was zu tun ist"

```
Schritt 1: x = 5
Schritt 2: y = 3
Schritt 3: z = x + y
Schritt 4: Gib z aus
```

**Fokus**: Wie wird es gemacht? (Commands, Kontrollflos)

**Sprachen**: C, Pascal, Assembler

### 2. Prozedural

> "Organisiere Code in Prozeduren/Funktionen"

```java
int add(int a, int b) {
  return a + b;
}

result = add(5, 3);
```

**Fokus**: Modularisierung durch Funktionen

**Sprachen**: C, Pascal, Delphi

### 3. Objektorientiert (OOP)

> "Alles ist ein Objekt. Programmiere wie in der realen Welt"

```java
class Student {
  String name;
  int alter;

  void lernen() {
    System.out.println("Lerne...");
  }
}

Student alice = new Student("Alice", 18);
alice.lernen();
```

**Fokus**: Objekte, Klassen, Encapsulation, Vererbung, Polymorphismus

**Sprachen**: Java, C++, C#, Python

**Zu klären in Praxis**: Unterschied zwischen Klasse und Methode

### 4. Funktional

> "Code ist eine Abbildung von Input zu Output. Keine Seiteneffekte."

```lisp
(defun add (a b)
  (+ a b))

(defun apply-twice (f x)
  (f (f x)))

(apply-twice add 5)  ; → (add (add 5 5) 5)
```

**Fokus**: Funktionen sind First-Class, Pure Functions, Immutabilität

**Sprachen**: Lisp, Haskell, Scala, JavaScript (teilweise)

### 5. Logisch

> "Definiere Fakten und Regeln. Lasse den Computer die Lösungen finden"

```prolog
parent(tom, bob).
parent(tom, liz).

grandparent(X, Z) :- parent(X, Y), parent(Y, Z).

?- grandparent(tom, X).  % Findet alle Enkel von tom
```

**Fokus**: Deklarativ (Was, nicht Wie), Constraint Satisfaction

**Sprachen**: Prolog

## Multiparadigmen

Die meisten modernen Sprachen unterstützen mehrere Paradigmen:

**Java**: OOP (primär) + Funktional (seit Java 8 mit Lambdas)

```java
// OOP
class Calculator { ... }

// Funktional (Lambda)
List<Integer> numbers = Arrays.asList(1, 2, 3);
numbers.forEach(n -> System.out.println(n));  // ← Lambda
```

**Python**: OOP + Funktional + Prozedural

```python
# OOP
class Dog:
    def bark(self): pass

# Funktional
map(lambda x: x * 2, [1, 2, 3])

# Prozedural
def calculate(): pass
```

## Wahl des Paradigmas

Welches Paradigma für welches Problem?

| Paradigma | Gut für | Beispiel |
|-----------|---------|---------|
| **Imperativ** | Einfache Scripts | Automation |
| **Prozedural** | Kleine Programme | System Tools |
| **OOP** | Große Systeme | Business Apps, Games |
| **Funktional** | Datenverarbeitung | Machine Learning, Data Analysis |
| **Logisch** | Knowledge Systems | Expert Systems, Constraints |

## Fokus für diesen Kurs

Wir nutzen **Java** → Fokus auf **OOP + etwas Funktional**.

- Klassen als zentrale Abstraktion
- Vererbung und Polymorphismus
- Lambdas und Streams (funktionales Denken)

Aber: Die Kontrollstrukturen (If, Loops) sind in ALLEN Paradigmen gleich!

Siehe auch: [Objektorientiert](Objektorientiert.md), [Funktional-Logisch](Funktional-Logisch.md)
