# C# Grundlagenschulung - Abschlussprojekt

## Projekttitel: "Konsolen-Anwendung für eine Mediathek"

In diesem Abschlussprojekt werden Sie eine Konsolen-Anwendung entwickeln, die eine kleine Mediathek repräsentiert. Diese Mediathek umfasst verschiedene Medienarten wie Bücher, Zeitungen, CDs und DVDs. Nutzer der Anwendung sollen Medien hinzufügen, anzeigen und durchsuchen können.

## Aufgabenstellung

1. **Projektstruktur einrichten**
   - Erstellen Sie ein neues C# Konsolenprojekt in Ihrer bevorzugten Entwicklungsumgebung.

2. **Vererbung und Polymorphismus**
   - Erstellen Sie eine abstrakte Basisklasse `Medium` mit den gemeinsamen Eigenschaften `Titel` und `Erscheinungsjahr`.
   - Erstellen Sie Unterklassen für jedes Medium: `Buch`, `Zeitung`, `CD` und `DVD`.
     - Jede Unterklasse soll spezifische Eigenschaften enthalten:
       - `Buch`: Autor, ISBN
       - `Zeitung`: Herausgeber, AusgabeNr
       - `CD`: Künstler, Titelanzahl
       - `DVD`: Regisseur, Spieldauer

3. **Konstruktoren**
   - Implementieren Sie für jede Klasse einen Konstruktor, der die spezifischen Eigenschaften initialisiert.

4. **Sammlung von Medien**
   - Verwenden Sie eine geeignete Datenstruktur, um verschiedene Medien zu speichern (z.B. eine Liste von `Medium`-Objekten).
   - Implementieren Sie Methoden, um Medien zur Liste hinzuzufügen und die Liste auf der Konsole anzuzeigen.

5. **Benutzerinteraktion**
   - Implementieren Sie ein Menü, über das der Nutzer folgende Optionen auswählen kann:
     - Medium hinzufügen
     - Alle Medien anzeigen
     - Medium nach Titel durchsuchen
     - Beenden

6. **Medium hinzufügen**
   - Erstellen Sie eine Methode, die den Benutzer auffordert, den Medientyp auszuwählen und dann die entsprechenden Details für das Medium einzugeben. Erstellen Sie entsprechend ein neues Objekt der gewählten Unterklasse.

7. **Alle Medien anzeigen**
   - Implementieren Sie eine Methode, die alle in der Mediathek befindlichen Medien auf der Konsole ausgibt. Nutzen Sie hierfür Polymorphismus, um eine einheitliche Darstellung zu erreichen.

8. **Medium suchen**
   - Erstellen Sie eine Methode, die den Benutzer nach einem Titel fragt und dann alle Medien anzeigt, deren Titel teilweise oder vollständig mit dem eingegebenen Suchbegriff übereinstimmen.

9. **Fehlerbehandlung**
   - Stellen Sie sicher, dass die Anwendung bei fehlerhaften Eingaben (z.B. leere Eingaben oder falsche Auswahl im Menü) valide bleibt und entsprechende Fehlermeldungen anzeigt.

## Lösungshinweise

- **Abstrakte Klassen und Vererbung**: Definieren Sie eine abstrakte Klasse `Medium` und leiten Sie die spezifischen Medienklassen davon ab. Nutzen Sie Abstraktion, um gemeinsam genutzte Funktionalitäten zu kapseln.

- **Listen und Sammlungen**: Eine `List<Medium>` eignet sich gut, um Polymorphismus zu nutzen. Sie können hier sowohl Bücher, Zeitungen, CDs als auch DVDs speichern.

- **Benutzerinteraktion**: Einfache Eingaben und Ausgaben können mit `Console.ReadLine()` und `Console.WriteLine()` realisiert werden. Nutzen Sie Schleifen und `switch`-Statements zur Steuerung des Menüs.

- **Polymorphismus**: Beim Anzeigen von Medien nutzen Sie die `ToString()`-Methode, um eine textuelle Repräsentation für jedes Medium anzubieten. Überschreiben Sie diese Methode in den Unterklassen, um Medienspezifika darzustellen.

- **Verarbeitung der Eingaben**: Denken Sie daran, `if-else` oder `switch`-Statements einzusetzen, um Benutzeraktionen zu behandeln. Bei der Eingabe von spezifischen Details eines Mediums verifizieren Sie die Eingaben auf ihre Richtigkeit.

## C# Grundlagenschulung - Abschlussprojekt Ressourcen

### Grundlegende Konzepte

- [Konsolenanwendungen mit .NET](https://learn.microsoft.com/de-de/dotnet/core/tutorials/with-visual-studio?pivots=dotnet-7-0)
- [Console.WriteLine Methode](https://learn.microsoft.com/de-de/dotnet/api/system.console.writeline)
- [Console.ReadLine Methode](https://learn.microsoft.com/de-de/dotnet/api/system.console.readline)

### Klassen und Vererbung

- [Abstrakte Klassen und Klassenmember](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members)
- [Vererbung in C#](https://learn.microsoft.com/de-de/dotnet/csharp/fundamentals/object-oriented/inheritance)
- [Polymorphismus](https://learn.microsoft.com/de-de/dotnet/csharp/fundamentals/object-oriented/polymorphism)

### Eigenschaften und Konstruktoren

- [Eigenschaften (Properties)](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/properties)
- [Konstruktoren](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/constructors)
- [Using-Anweisung](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/statements/using)

### Collections

- [List<T> Klasse](https://learn.microsoft.com/de-de/dotnet/api/system.collections.generic.list-1)
- [Collections (C#)](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/concepts/collections)

### String-Operationen

- [String-Methoden](https://learn.microsoft.com/de-de/dotnet/api/system.string)
- [String.Contains Methode](https://learn.microsoft.com/de-de/dotnet/api/system.string.contains)
- [String.ToLower Methode](https://learn.microsoft.com/de-de/dotnet/api/system.string.tolower)

### Fehlerbehandlung

- [Exception und Fehlerbehandlung](https://learn.microsoft.com/de-de/dotnet/csharp/fundamentals/exceptions/)
- [Try-Catch](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/statements/try-catch-finally)
- [ArgumentException](https://learn.microsoft.com/de-de/dotnet/api/system.argumentexception)

### Weitere nützliche Ressourcen

- [Object.ToString Methode](https://learn.microsoft.com/de-de/dotnet/api/system.object.tostring)
- [Switch-Anweisung](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/statements/selection-statements#the-switch-statement)
- [Schleifen in C#](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/statements/iteration-statements)
