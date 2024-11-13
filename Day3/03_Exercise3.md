# Übung 3 - Zahlen-Analyse-Bibliothek

## Aufgabenstellung

Erweitern Sie die Zahlen-Analyse aus Tag 2 durch Extraktion der Logik in separate Methoden und Implementierung verschiedener Analysefunktionen mit unterschiedlichen Parameter-Typen.

## Anforderungen

1. CalculateStatistics
   - Berechnet Minimum, Maximum und Durchschnitt
   - Verwendet out-Parameter für die Ergebnisse
   - Implementierung für int[] und double[]
   - Rückgabewert gibt an, ob Array gültige Zahlen enthält

2. FindNumbers
   - Sucht Zahlen nach bestimmten Kriterien
   - Optionaler Filter als Lambda-Expression
   - Optionales Sortieren der Ergebnisse
   - Rückgabe als neues Array

3. ProcessArray
   - Verarbeitet ein Array direkt (ref Parameter)
   - Optionales Entfernen von Duplikaten
   - Optionales Sortieren
   - Keine Rückgabe (void)

## Validierungsregeln

1. CalculateStatistics
   - Array darf nicht null oder leer sein
   - Initialisierung der out-Parameter mit Standardwerten
   - Korrekte Berechnung auch bei einem Element

2. FindNumbers
   - Null-Check für das Array
   - Filter darf null sein (dann alle Zahlen)
   - Leeres Array als Rückgabe möglich

3. ProcessArray
   - Array muss mit ref übergeben werden
   - Null-Arrays werden zu leeren Arrays
   - Reihenfolge: erst Duplikate entfernen, dann sortieren

## Lösungshinweise

### Methodensignaturen

```csharp
public class NumberAnalyzer
{
    // Statistik-Berechnung mit out-Parametern
    public static bool CalculateStatistics(
        int[] numbers,
        out int min,
        out int max,
        out double avg)

    // Überladung für double[]
    public static bool CalculateStatistics(
        double[] numbers,
        out double min,
        out double max,
        out double avg)

    // Zahlensuche mit optionalen Parametern
    public static int[] FindNumbers(
        int[] numbers,
        Func<int, bool> filter = null,
        bool sortResults = false)

    // Array-Verarbeitung mit ref
    public static void ProcessArray(
        ref int[] numbers,
        bool removeDuplicates = false,
        bool sort = true)
}
```

### Beispielaufruf

```csharp
int[] numbers = { 5, 2, 8, 2, 1, 9 };

// Statistik berechnen
int min, max;
double avg;
if (NumberAnalyzer.CalculateStatistics(numbers, out min, out max, out avg))
{
    Console.WriteLine($"Min: {min}, Max: {max}, Avg: {avg}");
}

// Zahlen filtern
var evenNumbers = NumberAnalyzer.FindNumbers(
    numbers,
    n => n % 2 == 0,  // Nur gerade Zahlen
    true              // Sortiert
);

// Array verarbeiten
NumberAnalyzer.ProcessArray(
    ref numbers,
    removeDuplicates: true,
    sort: true
);
```

## Ressourcen für Übung 3 - Zahlen-Analyse-Bibliothek

### Grundlegende Konzepte

- [out Parameter (C# Referenz)](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/keywords/out-parameter-modifier)
- [ref Parameter (C# Referenz)](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/keywords/ref)
- [Arrays (C# Programmierhandbuch)](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/arrays/)
- [Methodenüberladung (C# Programmierhandbuch)](https://learn.microsoft.com/de-de/dotnet/standard/design-guidelines/member-overloading)

### Fortgeschrittene Konzepte

- [Lambda-Ausdrücke (C# Programmierhandbuch)](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/operators/lambda-expressions)
- [Func<T,TResult> Delegat](https://learn.microsoft.com/de-de/dotnet/api/system.func-2)
- [Optionale Parameter (C# Programmierhandbuch)](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/named-and-optional-arguments)

### Nützliche Array-Methoden

- [Array.Sort Methode](https://learn.microsoft.com/de-de/dotnet/api/system.array.sort)
- [Array.Distinct Methode (LINQ)](https://learn.microsoft.com/de-de/dotnet/api/system.linq.enumerable.distinct)
- [Array-Klasse](https://learn.microsoft.com/de-de/dotnet/api/system.array)
