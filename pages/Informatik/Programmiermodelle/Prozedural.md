# Prozedurale Programmierung

## Definition

**Prozedural** = **Imperativ** + **Funktionen/Prozeduren**

> Organisiere Code in wiederverwendbare Funktionen/Prozeduren

## Charakteristiken

### 1. Funktionen als Zentrale Abstraktion

```pascal
PROCEDURE calculateGrade(score INTEGER) RETURNS STRING
BEGIN
  IF score >= 90 THEN
    RETURN "A"
  ELSE IF score >= 80 THEN
    RETURN "B"
  ELSE
    RETURN "C"
  END IF
END PROCEDURE

PROCEDURE main()
BEGIN
  grade = calculateGrade(95)
  PRINT grade  // Output: "A"
END PROCEDURE
```

### 2. Daten und Logik getrennt

```java
// Daten
class Student {
  String name;
  int age;
  double[] grades;
}

// Logik in Funktionen
double calculateAverage(Student s) {
  double sum = 0;
  for (double grade : s.grades) {
    sum += grade;
  }
  return sum / s.grades.length;
}

void printStudentInfo(Student s) {
  System.out.println(s.name);
  System.out.println("Average: " + calculateAverage(s));
}

// Nutzung
Student alice = new Student();
alice.name = "Alice";
alice.grades = new double[]{85, 90, 88};
printStudentInfo(alice);
```

Daten (`Student`) sind getrennt von Logik (`calculateAverage`, `printStudentInfo`).

## Kontrollfuss

Procedural nutzt Kontrollstrukturen zum Koordinieren:

```java
void processAllStudents(List<Student> students) {
  for (Student s : students) {
    if (isEligibleForGraduation(s)) {
      generateDiploma(s);
      sendNotification(s);
    }
  }
}
```

## Procedural vs Imperativ

| Aspekt | Imperativ | Procedural |
|--------|-----------|-----------|
| **Fokus** | Anweisungen | Funktionen |
| **Code Struktur** | Sequenzen | Modular |
| **Wiederverwendung** | Copy-Paste | Funktions-Aufrufe |
| **Daten & Logik** | Gemischt | Getrennt |
| **Beispiele** | COBOL | Pascal, C |

## Beispiel: Payroll System

```java
// Daten
class Employee {
  String name;
  double hourlyRate;
  double hoursWorked;
}

// Logik (Funktionen/Prozeduren)
double calculateGrossPay(Employee e) {
  return e.hourlyRate * e.hoursWorked;
}

double calculateTax(double grossPay) {
  return grossPay * 0.15;  // 15% tax
}

double calculateNetPay(Employee e) {
  double gross = calculateGrossPay(e);
  double tax = calculateTax(gross);
  return gross - tax;
}

void generatePayslip(Employee e) {
  System.out.println("Employee: " + e.name);
  System.out.println("Gross Pay: " + calculateGrossPay(e));
  System.out.println("Tax: " + calculateTax(calculateGrossPay(e)));
  System.out.println("Net Pay: " + calculateNetPay(e));
}

// Hauptprogramm
void main() {
  Employee bob = new Employee();
  bob.name = "Bob";
  bob.hourlyRate = 20;
  bob.hoursWorked = 40;

  generatePayslip(bob);
}
```

## Modularisierung

**Die Kraft der Prozeduralen Programmierung: Modularität**

```java
// Groß → Zerlegen → Klein

// Groß (zu komplex)
void processApplication(User u) {
  // Alles hier drin (100 Zeilen)
  validateData();
  checkBackground();
  verifyFunds();
  updateDatabase();
  sendEmail();
  generateReport();
  // ...
}

// Klein (modulare Funktionen)
void processApplication(User u) {
  if (!isValidApplicant(u)) return;
  if (!hasCleanBackground(u)) return;
  if (!hasSufficientFunds(u)) return;

  updateDatabase(u);
  sendConfirmation(u);
  generateReport(u);
}

// Jede Funktion hat eine Aufgabe
boolean isValidApplicant(User u) { /* ... */ }
boolean hasCleanBackground(User u) { /* ... */ }
boolean hasSufficientFunds(User u) { /* ... */ }
void updateDatabase(User u) { /* ... */ }
void sendConfirmation(User u) { /* ... */ }
void generateReport(User u) { /* ... */ }
```

## Procedural vs OOP

**Procedural**: Daten & Logik getrennt

```java
// Data
class Person {
  String name;
  int age;
}

// Logic
void printPerson(Person p) {
  System.out.println("Name: " + p.name);
  System.out.println("Age: " + p.age);
}
```

**OOP**: Daten & Logik zusammen (in Klasse)

```java
// Beides in einer Klasse
class Person {
  String name;
  int age;

  void printInfo() {  // Methode (Teil der Klasse)
    System.out.println("Name: " + name);
    System.out.println("Age: " + age);
  }
}
```

## Vorteile

- ✓ **Modular**: Funktionen können wiederverwendet werden
- ✓ **Wartbar**: Änderungen an einer Funktion = überall sichtbar
- ✓ **Testbar**: Funktionen einzeln testbar
- ✓ **Strukturiert**: Logik ist organisiert

## Nachteile

- ✗ **Daten-Zustand**: Daten können überall geändert werden
- ✗ **Nicht so Objekt-orientiert**: Keine Encapsulation
- ✗ **Skaliert nicht gut**: Große Systeme fragmentiert

## Zusammenfassung

**Procedural = Imperativ mit Funktionen**

- Daten (Records/Structs) getrennt
- Logik in Prozeduren/Funktionen
- Funktion-Aufrufe für Wiederverwendung
- Kontrollfluss-fokussiert

**Zeitlich**: Vor OOP (1970er-90er)
**Sprachen**: Pascal, C, Delphi, (Java auch teilweise)
**Heute**: Oft vermischt mit OOP

Siehe auch: [Imperativ](Imperativ.md), [Objektorientiert](Objektorientiert.md)
