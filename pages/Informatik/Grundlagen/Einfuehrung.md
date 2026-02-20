# Programmierung: Einführung

## Was ist Programmierung?

**Programmierung = Lösungsschritte für ein Problem so zu formulieren, dass ein Computer es ausführen kann, um bestimmte Aufgaben zu automatisieren.**

### Einfaches Beispiel

**Problem**: Ich habe 1000 Rechnungen. Ich muss die PDF-Namen mit Kundennummern umbenennen.

**Ohne Programmierung**: 1000x manuell umbenennen → Stunden Arbeit, Fehlerquellen

**Mit Programmierung**: Script in 10 Minuten schreiben → läuft automatisch → perfekt

## Die Phasen

```
1. PROBLEM DEFINIEREN
   ↓ (Deutsch/Englisch)
   "Ich will PDF-Dateien automatisch umbenennen"

2. ANALYSE & MODELLIERUNG
   ↓ (Nachdenken, Struktur)
   "Wie läuft das ab? Welche Schritte?"

3. ALGORITHMISCHE BESCHREIBUNG
   ↓ (PAP, Pseudocode, Struktogramm)
   "Schritt 1: Datei öffnen. Schritt 2: Namen ändern. Schritt 3: Speichern."

4. PROGRAMMIEREN / CODEN
   ↓ (Java, Python, JavaScript, etc.)
   ```
   File f = new File("rechnung_123.pdf");
   f.renameTo(new File("kunde_456.pdf"));
   ```

5. ÜBERSETZUNG / COMPILIERUNG
   ↓ (Compiler/Interpreter)
   Computer versteht Maschinensprache

6. AUSFÜHRUNG / INTERPRETIERUNG
   ↓ (CPU führt Code aus)
   Dateien werden umbenannt

7. PROBLEMLÖSUNG?
   ✓ Ja! (oder Bug beheben und wiederholen)
```

## Wichtig: Zerteilen

**Zu großes Problem?** → Teilen!

- Problem in Unterprobleme zerlegen
- Jedes Unterproblem einzeln lösen
- Zusammensetzen

**Beispiel**:
```
Problem: Webshop bauen
├─ Unterproblem: Benutzerverwaltung
├─ Unterproblem: Produktkatalog
├─ Unterproblem: Einkaufswagen
└─ Unterproblem: Zahlungsverarbeitung
```

Jedes wird extra programmiert, dann zusammengefügt.

## Der schwierige Teil

Das schwierigste an KI/Programmierung ist oft nicht das Coden, sondern:

**Das Problem überhaupt erst mal richtig zu formulieren!**

- Was genau soll die Software machen?
- Was ist Input? Was ist Output?
- Welche Edge Cases gibt es?

Einmal klar formuliert → Coden ist meist straightforward.

## Was brauchst du?

1. **Verständnis für Algorithmen**: Wie funktioniert etwas?
2. **Grundstrukturen**: If-Else, Schleifen, Variablen
3. **Datenstrukturen**: Arrays, Maps, Listen
4. **Eine Programmiersprache**: Java, Python, JavaScript, etc.
5. **Debugging-Fähigkeiten**: Wenn es nicht funktioniert

## Dieser Kurs

Wir folgen dem Lehrplan der österreichischen Ausbildung (Applikationsentwicklung):

- Algorithmische Grundlagen
- Datenstrukturen
- Programmiersprachen und Paradigmen
- Praktische Umsetzung in Java

Siehe auch: [Lehrplan](Ressourcen.md)

## Kursuebersicht

- **Dauer**: 8 Wochenstunden insgesamt
- **Format**: Kapitelweise Tests, min 3 Prüfungen
- **Schwierigkeit**: Wird progressiv schwerer
- **Erfolg**: Mitarbeit ist essentiell

## Die zwei großen Blöcke

### 1. Algorithmen
- Wie läuft etwas ab?
- Welche Kontrollstrukturen brauche ich?
- Wie modelliere ich das?

### 2. Datenstrukturen
- Welche Daten speichere ich?
- In welcher Form (Array, List, Map)?
- Wann nutze ich welche Struktur?

Alles andere baut auf diesen zwei auf.

## Nächste Schritte

1. Lies [Ressourcen](Ressourcen.md) für Lernmaterialien
2. Verstehe [Konzepte](../Konzepte/Concept-Map.md)
3. Lerne [Programmiersprachen](../Programmiersprachen/Einfuehrung.md)
4. Implementiere in Java
