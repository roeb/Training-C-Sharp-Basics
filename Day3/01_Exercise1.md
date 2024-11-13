# Übung 1 - Taschenrechner-Bibliothek

## Aufgabenstellung

Entwickeln Sie eine Taschenrechner-Bibliothek mit verschiedenen Methoden, die unterschiedliche Parameter-Arten und Überladungen demonstriert.

## Anforderungen

1. Add-Methoden
   - Zwei Überladungen implementieren
   - Version für 2 Parameter
   - Version für 3 Parameter
   - Ganzzahlige Addition

2. Subtract-Methode
   - Dezimalzahlen unterstützen
   - Optionaler Parameter für Rundung
   - Bei Rundung auf ganze Zahl runden

3. Multiply-Methode
   - Beliebig viele Parameter akzeptieren
   - params Array verwenden
   - Ganzzahlige Multiplikation

4. Divide-Methode
   - Division mit Rest durchführen
   - out Parameter für Quotient und Rest
   - Division durch 0 abfangen

5. TryParse-Methode
   - String in Zahl konvertieren
   - Verschiedene Zahlenformate unterstützen
   - out Parameter für Ergebnis

## Validierungsregeln

1. Add-Methoden
   - Keine negativen Zahlen erlaubt
   - Überprüfung auf Überlauf nicht erforderlich

2. Subtract-Methode
   - Negative Ergebnisse erlaubt
   - Rundung nur bei aktiviertem Parameter

3. Multiply-Methode
   - Mindestens eine Zahl erforderlich
   - Überprüfung auf Überlauf nicht erforderlich

4. Divide-Methode
   - Division durch 0 erkennen
   - Korrekte Berechnung von Quotient und Rest

5. TryParse-Methode
   - Punkt und Komma als Dezimaltrennzeichen
   - Leere Eingaben abfangen

## Lösungshinweise

### Methodensignaturen

```csharp
public class Calculator
{
    // Addition mit Überladungen
    public int Add(int a, int b)
    public int Add(int a, int b, int c)

    // Subtraktion mit optionalem Parameter
    public double Subtract(double a, double b, bool round = false)

    // Multiplikation mit params
    public int Multiply(params int[] numbers)

    // Division mit out Parametern
    public bool Divide(int dividend, int divisor, 
                      out int quotient, out int remainder)

    // String-Konvertierung mit out
    public bool TryParse(string input, out double result)
}
```

### Beispielaufruf

```csharp
Calculator calc = new Calculator();

// Addition testen
Console.WriteLine(calc.Add(5, 3));        // 8
Console.WriteLine(calc.Add(5, 3, 2));     // 10

// Subtraktion mit Rundung
Console.WriteLine(calc.Subtract(10.7, 3.2));         // 7.5
Console.WriteLine(calc.Subtract(10.7, 3.2, true));   // 8.0

// Multiplikation mit mehreren Zahlen
Console.WriteLine(calc.Multiply(2, 3, 4));           // 24

// Division mit Rest
int quotient, remainder;
if (calc.Divide(17, 5, out quotient, out remainder))
{
    Console.WriteLine($"17 ÷ 5 = {quotient} Rest {remainder}");
}

// Zahlen-Parsing
double number;
if (calc.TryParse("123,45", out number))
{
    Console.WriteLine($"Parsed: {number}");
}
```

## Hilfreiche MSDN Dokumentation für die Taschenrechner-Übung

### Methoden und Parameter
- [Methodenüberladung (Method Overloading)](https://learn.microsoft.com/de-de/dotnet/standard/programming-guide/classes-and-structs/methods#method-overloading)
- [Optionale Parameter](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/named-and-optional-arguments#optional-arguments)
- [params Schlüsselwort](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/keywords/params)
- [out Parameter](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/keywords/out-parameter-modifier)

### Numerische Typen und Operationen
- [Ganzzahlige numerische Typen](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/builtin-types/integral-numeric-types)
- [Gleitkomma-Typen](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/builtin-types/floating-point-numeric-types)
- [Arithmetische Operatoren](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/operators/arithmetic-operators)

### String-Verarbeitung und Konvertierung
- [double.TryParse Methode](https://learn.microsoft.com/de-de/dotnet/api/system.double.tryparse)
- [Zahlenformatierung](https://learn.microsoft.com/de-de/dotnet/standard/base-types/formatting-types)
- [CultureInfo für Zahlenformate](https://learn.microsoft.com/de-de/dotnet/api/system.globalization.cultureinfo)

### Fehlerbehandlung
- [Exception Handling](https://learn.microsoft.com/de-de/dotnet/csharp/fundamentals/exceptions/)
- [DivideByZeroException](https://learn.microsoft.com/de-de/dotnet/api/system.dividebyzeroexception)

### Allgemeine Konzepte
- [Klassen und Methoden](https://learn.microsoft.com/de-de/dotnet/csharp/fundamentals/types/classes)
- [Validierung von Parametern](https://learn.microsoft.com/de-de/dotnet/standard/design-guidelines/parameter-validation)