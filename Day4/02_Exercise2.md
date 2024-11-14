# Übung 2 - Taschenrechner-OOP

Wandle den prozeduralen Taschenrechner in eine objektorientierte Version um.

## Anforderungen

### Klasse Calculator erstellen mit:

#### Private Felder

- `_firstNumber` (double)
- `_secondNumber` (double)
- `_result` (double)

#### Properties

- `Result` (double, nur lesbar)
- `CurrentOperation` (string, nur lesbar)

#### Konstruktor

- Standardkonstruktor ohne Parameter
- Überladener Konstruktor mit zwei Parametern (firstNumber, secondNumber)

#### Methoden

- `Add()`: Addiert die beiden Zahlen
- `Subtract()`: Subtrahiert die zweite von der ersten Zahl
- `Multiply()`: Multipliziert die beiden Zahlen
- `Divide()`: Dividiert die erste durch die zweite Zahl
- `SetNumbers(double first, double second)`: Setzt neue Zahlen
- `Clear()`: Setzt alle Werte zurück

## Beispiel Verwendung

```csharp
Calculator calc = new Calculator(10, 5);

calc.Add();
Console.WriteLine($"10 + 5 = {calc.Result}"); // Ausgabe: 15

calc.SetNumbers(20, 4);
calc.Divide();
Console.WriteLine($"20 / 4 = {calc.Result}"); // Ausgabe: 5
```

## Lösungshinweise

### 1. Klassenstruktur

```csharp
public class Calculator
{
    // Private Felder für die Zahlen und das Ergebnis
    private double _firstNumber;
    private double _secondNumber;
    private double _result;

    // Properties hier definieren
    public double Result 
    { 
        get { return _result; } 
    }
}
```

### 2. Konstruktoren

```csharp
// Standardkonstruktor
public Calculator()
{
    Clear();
}

// Überladener Konstruktor
public Calculator(double firstNumber, double secondNumber)
{
    // Initialisiere die Zahlen
    // Setze Standardwerte
}
```

### 3. Methoden

- Bei Division durch 0 eine Exception werfen
- Nach jeder Operation das Ergebnis in `_result` speichern
- `Clear()` setzt alle Werte auf 0 zurück

## Ressourcen für Übung 2 - Taschenrechner-OOP

### Grundlegende OOP-Konzepte
- [Klassen und Objekte in C#](https://learn.microsoft.com/de-de/dotnet/csharp/fundamentals/object-oriented/)
- [Einführung in Klassen](https://learn.microsoft.com/de-de/dotnet/csharp/fundamentals/types/classes)

### Properties und Felder
- [Properties](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/properties)
- [Using Properties](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/using-properties)
- [Auto-Implemented Properties](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/auto-implemented-properties)

### Konstruktoren
- [Konstruktoren](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/constructors)
- [Using Constructors](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/using-constructors)

### Zugriffsmodifizierer
- [Access Modifiers](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/access-modifiers)
- [Accessibility Levels](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/keywords/accessibility-levels)

### Methoden
- [Methods](https://learn.microsoft.com/de-de/dotnet/csharp/methods)
- [Method Parameters](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/methods#method-parameters)

### Exception Handling
- [Exception Handling](https://learn.microsoft.com/de-de/dotnet/csharp/fundamentals/exceptions/)
- [DivideByZeroException Class](https://learn.microsoft.com/de-de/dotnet/api/system.dividebyzeroexception)
- [try-catch](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/statements/try-catch)
