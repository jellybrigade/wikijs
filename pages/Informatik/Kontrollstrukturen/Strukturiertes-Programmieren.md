# Strukturiertes Programmieren

## Definition

**Strukturiertes Programmieren** bedeutet: Code mit nur strukturierten Kontrolstrukturen schreiben (keine GOTO-ähnlichen Sprünge).

Basis: Böhm-Jacopini Theorem

## Prinzipien

### 1. Top-Down Ansatz

Teile große Probleme in kleinere Subprobleme auf:

```
Problem: Universität Management System
├─ Subproblem 1: Studentenverwaltung
│  ├─ Student registrieren
│  ├─ Student löschen
│  └─ Student suchen
├─ Subproblem 2: Kursverwaltung
│  ├─ Kurs erstellen
│  ├─ Studenten anmelden
│  └─ Noten eintragen
└─ Subproblem 3: Prüfungsverwaltung
```

Implementiere jedes Subproblem einzeln, dann zusammensetzen.

### 2. Funktionale Zerlegung

Jede Funktion hat eine **Aufgabe**:

```java
// ✗ Schlecht (macht zu viel)
void processData() {
  readFile();
  validateData();
  transformData();
  saveData();
  sendEmail();
  generateReport();
  // Was macht diese Funktion?
}

// ✓ Gut (eine Aufgabe pro Funktion)
void processStudentData() {
  List<Student> students = readStudentFile();
  validateStudents(students);
  saveStudents(students);
  notifyStudents(students);
}

void readStudentFile() { /* ... */ }
void validateStudents(List<Student> s) { /* ... */ }
void saveStudents(List<Student> s) { /* ... */ }
void notifyStudents(List<Student> s) { /* ... */ }
```

**Single Responsibility Principle (SRP)**: Eine Funktion = eine Verantwortung.

### 3. Klare Kontrollfluss

Code sollte linear von oben nach unten lesbar sein:

```java
// ✗ Schwierig (Spaghetti)
for (int i = 0; i < items.size(); i++) {
  if (items.get(i).isValid()) {
    if (items.get(i).isActive()) {
      if (items.get(i).getValue() > 100) {
        if (items.get(i).getStatus().equals("PENDING")) {
          process(items.get(i));
        }
      }
    }
  }
}

// ✓ Klar (Guard Clauses)
for (Item item : items) {
  if (!item.isValid()) continue;
  if (!item.isActive()) continue;
  if (item.getValue() <= 100) continue;
  if (!item.getStatus().equals("PENDING")) continue;

  process(item);
}
```

**Guard Clauses**: Ungültige Fälle früh herausfiltern, dann "happy path".

### 4. Nesting Limit

Max 3 Nesting-Level:

```java
// ✗ Zu verschachtelt
for (int i = 0; i < 10; i++) {
  if (i > 5) {
    while (true) {
      if (condition) {
        for (int j = 0; j < 5; j++) {
          // Wo bin ich?? (4 Level)
        }
      }
    }
  }
}

// ✓ Besser (Funktionen extrahieren)
for (int i = 0; i < 10; i++) {
  processItem(i);
}

void processItem(int i) {
  if (i <= 5) return;
  // Level 1
  while (true) {
    if (!condition) break;
    // Level 2
    handleMultipleValues();
  }
}

void handleMultipleValues() {
  for (int j = 0; j < 5; j++) {
    // Level 1 (in dieser Funktion)
  }
}
```

### 5. Aussagekräftige Namen

```java
// ✗ Unklar
int p = 5;
if (a > p) {
  c = a * r;
  s += c;
}

// ✓ Klar
int priceThreshold = 5;
if (productPrice > priceThreshold) {
  int commission = productPrice * commissionRate;
  totalSales += commission;
}
```

## Techniken

### Guard Clauses (Early Return)

```java
// Früh invalide Fälle rauswerfen

public boolean isEligible(Student s) {
  if (s.getAge() < 18) return false;
  if (!s.hasHighSchoolDiploma()) return false;
  if (s.hasDisqualifyingRecord()) return false;

  // Happy path bleibt (unkompliziert)
  return true;
}
```

### Extraktion zu Funktionen

Komplexe Bedingungen extrahieren:

```java
// ✗ Schwierig
if (student.getGPA() >= 3.0 &&
    student.getAttendance() > 90 &&
    student.getTuitionPaid() &&
    student.getAge() >= 18) {
  enrollInProgram(student);
}

// ✓ Klar
if (isEligible(student)) {
  enrollInProgram(student);
}

private boolean isEligible(Student student) {
  return student.getGPA() >= 3.0 &&
         student.getAttendance() > 90 &&
         student.getTuitionPaid() &&
         student.getAge() >= 18;
}
```

### Loop-Extraktion

```java
// ✗ Kompliziert
List<Integer> results = new ArrayList<>();
for (Item item : items) {
  if (item.isValid()) {
    int transformed = transform(item);
    if (transformed > 0) {
      results.add(transformed);
    }
  }
}

// ✓ Modern (Java Streams)
List<Integer> results = items.stream()
  .filter(Item::isValid)
  .map(this::transform)
  .filter(x -> x > 0)
  .collect(Collectors.toList());
```

## Best Practices Checkliste

- [ ] Jede Funktion hat eine klare Aufgabe (SRP)
- [ ] Nesting maximal 3 Level
- [ ] Guard clauses für invalide Eingaben
- [ ] Namen sind aussagekräftig
- [ ] Kontrolfluss ist linear/lesbar
- [ ] Keine GOTO-ähnlichen Sprünge
- [ ] Kurze Funktionen (< 20 Zeilen ideal)
- [ ] Keine Spaghetti-Code-Struktur

## Zusammenfassung

Strukturiertes Programmieren = **Lesbar, wartbar, verständlich**

1. Teile Probleme auf (Top-Down)
2. Eine Funktion = eine Aufgabe
3. Klarer Kontrollfluss
4. Nicht zu tief verschachtelt
5. Aussagekräftige Namen

Siehe auch: [Böhm-Jacopini](Boehm-Jacopini.md), [Kontrollstrukturen](Sequenz.md)
