# Programmiersprachen: Einführung

## Was ist eine Programmiersprache?

Eine **Programmiersprache** ist ein formales System, das der Computer versteht.

```
Deutsch (du):  "Kaffee machen"
              ↓ Übersetzung (Compiler/Interpreter)
Maschinencode: 0101 1100 1010 ...
              ↓ CPU führt aus
Aktion: Kaffee wird gemacht!
```

## Klassifizierungen

Es gibt mehrere Wege, Programmiersprachen zu klassifizieren:

### 1. Nach Maschinennähe

```
Maschinennähe ↑
              │
        Maschinensprache      (0101, direkt für CPU)
              │
        Assembler             (mov ax, bx)
              │
      Hochsprachenprogrammierung
              │
    (C, Java, Python, JavaScript)
              ↓
        Einfachheit
```

### 2. Nach Programmiermodell/Paradigma

- **Imperativ**: "Tu dies, dann das" (C, Java, Python)
- **Prozedural**: Mit Funktionen (Pascal, C)
- **Objektorientiert**: Mit Klassen (Java, C++, Python)
- **Funktional**: Funktionen sind First-class (Lisp, Haskell, JavaScript)
- **Logisch**: Fakten und Regeln (Prolog)

### 3. Nach Generationen (weniger relevant)

- 1. Generation: Maschinensprache
- 2. Generation: Assembler
- 3. Generation: Hochsprachen (C, Java, Python)
- 4. Generation: SQL, Shells
- 5. Generation: KI-Sprachen (Prolog)

## Überblick: Häufige Sprachen

| Sprache | Paradigma | Einsatz | Schwierigkeit |
|---------|-----------|---------|-----------------|
| **Java** | OO | Backend, Android | Mittel |
| **Python** | Multi | Datascience, Scripting | Einfach |
| **C/C++** | OO/Prozedural | Systeme, Performance | Schwer |
| **JavaScript** | OO/Funktional | Frontend, Node.js | Mittel |
| **Go** | Prozedural | Microservices, Cloud | Mittel |
| **Rust** | Prozedural | Systeme, Performance | Schwer |

## Die zentrale Frage

Wie funktioniert es, vom Source Code zur ausführbaren Anwendung?

```
SOURCE CODE (text file, z.B. main.java)
    ↓
    ├─ COMPILER → Maschinencode / Bytecode
    ├─ INTERPRETER → Direktausführung
    └─ HYBRID → Beides
```

Und genau hier unterscheiden sich Sprachen!

Siehe: [Compiler vs Interpreter](Compiler-Interpreter.md)

## Eignung für diesen Kurs

Wir nutzen **Java** weil:

- ✓ Stark typisiert (Fehler früh sichtbar)
- ✓ OOP Fokus (Konzepte klar)
- ✓ Professionell (wirklich genutzt)
- ✓ Große Community
- ✓ Portabel (läuft überall)

Aber die Konzepte (Schleifen, Funktionen, OOP) gelten für ALLE Sprachen!

## Nächste Schritte

1. Verstehe [Maschinennähe](Maschinennaeche.md)
2. Lerne [Compiler vs Interpreter](Compiler-Interpreter.md)
3. Explore [Programmiermodelle](../Programmiermodelle/Einfuehrung.md)
