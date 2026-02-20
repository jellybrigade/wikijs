# Funktional & Logisch Programmieren

## Funktionale Programmierung

### Definition

> Betrachte Programme als Abbildungen von Input zu Output
> Fokus auf **WAS** (Ziel), nicht **WIE** (Schritte)

### Charakteristiken

#### 1. Pure Functions (Reine Funktionen)

**Keine Seiteneffekte**: Gleicher Input → Gleicher Output, immer.

```java
// ✓ Pure Function
int add(int a, int b) {
  return a + b;
}

// ✗ Impure (hat Seiteneffekte)
int counter = 0;
int increment() {
  counter++;  // ← Seiteneffekt! Ändert externe Variable
  return counter;
}
```

#### 2. Immutabilität

Variablen ändern sich nicht nach Erstellung:

```java
// ✓ Immutable
final List<Integer> numbers = Arrays.asList(1, 2, 3);
// Nicht möglich: numbers.add(4);

// ✗ Mutable
List<Integer> numbers = new ArrayList<>(Arrays.asList(1, 2, 3));
numbers.add(4);  // Ändert Liste
```

#### 3. First-Class Functions

Funktionen sind Werte (können als Argumente übergeben werden):

```java
// Lambda (anonyme Funktion)
Function<Integer, Integer> double = (x) -> x * 2;

List<Integer> numbers = Arrays.asList(1, 2, 3);
numbers.forEach(double);  // Funktion als Argument
```

#### 4. Deklarativ (WAS, nicht WIE)

```java
// Imperative (WIE)
List<Integer> result = new ArrayList<>();
for (Integer n : numbers) {
  if (n % 2 == 0) {
    result.add(n * 2);
  }
}

// Functional (WAS)
List<Integer> result = numbers.stream()
  .filter(n -> n % 2 == 0)
  .map(n -> n * 2)
  .collect(Collectors.toList());
```

### Funktionale Sprachen

- **Lisp**: Uralt, still Entwicklung
- **Haskell**: Pure functional
- **Scala**: Functional + OOP
- **Clojure**: Lisp auf JVM

### Vorteil

- ✓ **Nebenläufigkeit**: Keine Datenstatus-Probleme
- ✓ **Testbar**: Pure Functions einfach zu testen
- ✓ **Verständlich**: Input → Output Mapping

### Nachteil

- ✗ **Verbose**: Manchmal mehr Code als imperativ
- ✗ **Performance**: Funktionale Sprachen oft langsamer

## Logische Programmierung

### Definition

> Definiere Fakten und Regeln. Lasse den Computer Lösungen finden.
> Fokus auf **Was ist wahr**, nicht **wie ausrechnen**

### Charakteristiken

#### 1. Fakten

```prolog
parent(tom, bob).      % Fakt: tom ist Parent von bob
parent(tom, liz).      % Fakt: tom ist Parent von liz
parent(bob, ann).      % Fakt: bob ist Parent von ann
```

#### 2. Regeln

```prolog
% Regel: X ist Großvater von Z wenn X Parent von Y und Y Parent von Z
grandparent(X, Z) :- parent(X, Y), parent(Y, Z).

% Regel: X und Y sind Geschwister wenn gleiche Parent
sibling(X, Y) :- parent(Z, X), parent(Z, Y), X \= Y.
```

#### 3. Queries (Abfragen)

```prolog
?- grandparent(tom, X).   % Finde alle Enkel von tom
% Answer: X = ann

?- sibling(bob, X).       % Finde alle Geschwister von bob
% Answer: X = liz
```

### Wie funktioniert's?

1. Computer sucht alle Fakten/Regeln
2. Probiert alle möglichen Kombinationen
3. Gibt Lösungen die Regeln erfüllen

```prolog
Frage: grandparent(tom, X)?

Computer:
├─ Findet: parent(tom, Y) → Y = bob oder Y = liz
├─ Checkt parent(Y, Z):
│  ├─ parent(bob, X) → parent(bob, ann) ✓
│  └─ parent(liz, X) → Keine Fakten → ✗
└─ Antwort: X = ann
```

### Logische Sprachen

- **Prolog**: The Standard
- **Datalog**: Eingeschränktes Prolog (Datenbanken)

### Vorteil

- ✓ **Deklarativ**: Schreib was, nicht wie
- ✓ **Clever**: Computer findet Lösungen
- ✓ **Constraints**: Gut für Constraint-Probleme

### Nachteil

- ✗ **Langsam**: Brute-Force Suche
- ✗ **Unintuitiv**: Nicht wie Standard-Programmierung
- ✗ **Debugging**: Schwierig zu debug

## Vergleich: Alle Paradigmen

```java
// Aufgabe: Summe aller geraden Zahlen

// Imperativ (WIE?)
int sum = 0;
for (int i = 0; i < numbers.size(); i++) {
  if (numbers.get(i) % 2 == 0) {
    sum += numbers.get(i);
  }
}

// Prozedural (Funktionen)
int sum = calculateSumOfEvens(numbers);

// Funktional (WAS?)
int sum = numbers.stream()
  .filter(n -> n % 2 == 0)
  .reduce(0, Integer::sum);

// Logisch (Prolog - konzeptuell)
sum_evens([], 0).
sum_evens([H|T], Sum) :-
  0 is H mod 2,
  sum_evens(T, Rest),
  Sum is H + Rest.
sum_evens([H|T], Sum) :-
  1 is H mod 2,
  sum_evens(T, Sum).
```

## Praktisch in Kurse

**Hauptsächlich**:
- Imperativ/Prozedural (Grundlagen)
- Objektorientiert (Java)
- Etwas Funktional (Java Streams)

**Weniger**:
- Rein Funktional (zu abstrakt)
- Logisch (zu spezialisiert)

Aber: Die Konzepte sind wichtig zu verstehen!

## Zusammenfassung

| Paradigma | Fokus | Sprachen | Gut für |
|-----------|-------|----------|---------|
| Imperativ | WIE (Schritte) | C, Java | Systeme |
| Prozedural | Funktionen | Pascal, C | Module |
| OOP | Objekte | Java, C++ | Große Systeme |
| Funktional | WAS (Mapping) | Lisp, Haskell | Daten |
| Logisch | Fakten & Regeln | Prolog | Constraints |

Siehe auch: [Programmiermodelle Überblick](Einfuehrung.md)
