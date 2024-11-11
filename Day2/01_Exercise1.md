# Übung 1 - Zahlenanalyse

## Aufgabenstellung

Erstellen Sie ein Konsolenprogramm zur Analyse von Zahlen mit den unten beschriebenen Anforderungen.

## Anforderungen

1. Erstellen Sie ein Array für 10 Integer-Werte
2. Lesen Sie 10 Zahlen vom Benutzer ein
   - Verwenden Sie eine Schleife
   - Prüfen Sie ob die Eingabe eine gültige Zahl ist
   - Bei ungültiger Eingabe: Fehlermeldung und erneute Eingabe
3. Geben Sie die Zahlen in folgenden Varianten aus:
   - Ursprüngliche Reihenfolge
   - Sortierte Reihenfolge (aufsteigend)
4. Berechnen und zeigen Sie folgende Statistiken:
   - Kleinste Zahl
   - Größte Zahl
   - Durchschnitt (mit 2 Nachkommastellen)
5. Erstellen Sie eine Liste mit allen geraden Zahlen
   - Verwenden Sie List<int>
   - Geben Sie diese Liste aus

## Beispielausgabe

```text
Bitte geben Sie 10 Zahlen ein:
1. Zahl: 23
2. Zahl: 12
...
10. Zahl: 45

Ursprüngliche Reihenfolge:
23, 12, ..., 45

Sortierte Reihenfolge:
12, ..., 45

Statistik:
Minimum: 12
Maximum: 45
Durchschnitt: 28,50

Gerade Zahlen:
12, ...
```

## Hinweise

- Nutzen Sie Array.Sort() zum Sortieren
- Verwenden Sie für die Durchschnittsberechnung double
- Nutzen Sie foreach für die Ausgaben
- Verwenden Sie string.Join() für kommagetrennte Ausgaben
- Für die Zahlenprüfung: int.TryParse()

## Zusatzaufgaben (optional)

1. Zählen Sie, wie oft jede Zahl vorkommt
2. Berechnen Sie die Standardabweichung
3. Ermöglichen Sie die Eingabe einer beliebigen Anzahl von Zahlen
4. Speichern Sie die Ergebnisse in einer Datei

## Beispielcode-Struktur

```csharp
int[] numbers = new int[10];

// Einlesen der Zahlen
for (int i = 0; i < numbers.Length; i++)
{
    bool validInput = false;
    while (!validInput)
    {
        Console.Write($"{i + 1}. Zahl: ");
        // Hier Ihre Implementierung
    }
}

// Ausgabe ursprüngliche Reihenfolge
Console.WriteLine("\nUrsprüngliche Reihenfolge:");
// Ihre Implementierung

// Sortierung und Ausgabe
Console.WriteLine("\nSortierte Reihenfolge:");
// Ihre Implementierung

// Statistik
Console.WriteLine("\nStatistik:");
// Ihre Implementierung

// Gerade Zahlen
Console.WriteLine("\nGerade Zahlen:");
// Ihre Implementierung
```

## MSDN Dokumentation Ressourcen für Übung 1

### Arrays
- [Array Klasse (System.Array)](https://learn.microsoft.com/de-de/dotnet/api/system.array)
- [Array.Sort Methode](https://learn.microsoft.com/de-de/dotnet/api/system.array.sort)

### Eingabe und Konvertierung
- [Console.ReadLine Methode](https://learn.microsoft.com/de-de/dotnet/api/system.console.readline)
- [int.TryParse Methode](https://learn.microsoft.com/de-de/dotnet/api/system.int32.tryparse)

### Listen
- [List<T> Klasse](https://learn.microsoft.com/de-de/dotnet/api/system.collections.generic.list-1)
- [List<T>.Add Methode](https://learn.microsoft.com/de-de/dotnet/api/system.collections.generic.list-1.add)

### Schleifen und Iteration
- [foreach Statement](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/statements/iteration-statements#the-foreach-statement)
- [for Statement](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/statements/iteration-statements#the-for-statement)

### String Operationen
- [string.Join Methode](https://learn.microsoft.com/de-de/dotnet/api/system.string.join)
- [String Formatierung](https://learn.microsoft.com/de-de/dotnet/standard/base-types/formatting-types)

### Mathematische Operationen
- [Math.Min Methode](https://learn.microsoft.com/de-de/dotnet/api/system.math.min)
- [Math.Max Methode](https://learn.microsoft.com/de-de/dotnet/api/system.math.max)