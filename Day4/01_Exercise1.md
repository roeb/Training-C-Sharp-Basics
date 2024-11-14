# Übung 1 - Fahrzeug-Klasse

Erstelle eine Klasse `Vehicle` mit folgenden Anforderungen:

## Properties

- Brand (string)
- Model (string)
- Year (int)
- IsRunning (bool)

## Konstruktor

- Soll Brand, Model und Year als Parameter haben
- IsRunning initial auf false setzen

## Methoden

- StartEngine(): Setzt IsRunning auf true
- StopEngine(): Setzt IsRunning auf false
- GetVehicleInfo(): Gibt einen formatierten String mit allen Fahrzeuginformationen zurück

## Beispiel Verwendung

```csharp
// Fahrzeug erstellen
Vehicle car = new Vehicle("BMW", "X3", 2022);

// Motor starten
car.StartEngine();
Console.WriteLine(car.IsRunning); // Ausgabe: True

// Fahrzeuginfo ausgeben
Console.WriteLine(car.GetVehicleInfo()); 
// Ausgabe: BMW X3 (2022) - Motor läuft: True
```

## Zusatzaufgabe

- Füge eine Validierung für das Jahr hinzu (nicht in der Zukunft und nicht vor 1886)
- Erweitere die Klasse um eine Property für den Kraftstoffstand (FuelLevel)
- Füge eine Methode zum Tanken hinzu (AddFuel)

## Lösungshinweise

### 1. Klassenstruktur

```csharp
public class Vehicle
{
    // Properties hier definieren
    // Tipp: Verwende { get; set; } für einfache Properties
}
```

### 2. Konstruktor

```csharp
public Vehicle(string brand, string model, int year)
{
    // Initialisiere hier die Properties
    // Denk daran: IsRunning muss initial false sein
}
```

### 3. GetVehicleInfo Methode

- Verwende String-Interpolation mit $"..."
- Beispiel für String-Interpolation: $"{Property1} {Property2}"
- Alternativ: string.Format() oder + Operator

### 4. Zusatzaufgabe - Jahresvalidierung

```csharp
// Im Property für Year:
set
{
    if (/* Prüfe hier die Bedingungen */)
    {
        // Setze den Wert
    }
    else
    {
        throw new ArgumentException("Ungültiges Jahr");
    }
}
```

## Hilfreiche MSDN Dokumentation für die Fahrzeug-Klasse Übung

### Grundlegende Konzepte
- [Klassen und Objekte in C#](https://learn.microsoft.com/de-de/dotnet/csharp/fundamentals/object-oriented/classes)
- [Eigenschaften (Properties)](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/properties)
- [Konstruktoren](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/constructors)

### String-Formatierung
- [String-Interpolation](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/tokens/interpolated)
- [String.Format Methode](https://learn.microsoft.com/de-de/dotnet/api/system.string.format)

### Für die Zusatzaufgabe
- [Exception Handling](https://learn.microsoft.com/de-de/dotnet/csharp/fundamentals/exceptions/)
- [ArgumentException Klasse](https://learn.microsoft.com/de-de/dotnet/api/system.argumentexception)
- [Property Validierung](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/how-to-implement-a-lightweight-class-with-auto-implemented-properties)

### Zusätzliche Konzepte
- [Access Modifiers (Zugriffsmodifizierer)](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/access-modifiers)
- [Auto-Implemented Properties](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/auto-implemented-properties)
