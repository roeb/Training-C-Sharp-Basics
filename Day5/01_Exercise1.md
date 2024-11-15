# Übung 1: Geometrische Formen

In dieser Übung erstellen Sie eine Klassenhierarchie für geometrische Formen.

## Aufgabenstellung

1. Erstellen Sie eine abstrakte Basisklasse `Shape` mit:
   - Eigenschaft `Name` (string)
   - Abstrakte Methode `CalculateArea()` (double)
   - Abstrakte Methode `CalculatePerimeter()` (double)

2. Implementieren Sie zwei konkrete Klassen:
   - `Circle` (Kreis)
     - Zusätzliche Eigenschaft: Radius (double)
     - Implementierung der Flächenberechnung (π * r²)
     - Implementierung der Umfangberechnung (2 * π * r)

   - `Rectangle` (Rechteck)
     - Eigenschaften: Length und Width (double)
     - Implementierung der Flächenberechnung (Länge * Breite)
     - Implementierung der Umfangberechnung (2 * (Länge + Breite))

3. Erstellen Sie in der Main-Methode:
   - Ein Array vom Typ Shape
   - Je eine Instanz von Circle und Rectangle
   - Berechnen und Ausgeben von Fläche und Umfang für beide Formen

## Beispiel-Implementation

```csharp
public abstract class Shape
{
    public string Name { get; set; }
    public abstract double CalculateArea();
    public abstract double CalculatePerimeter();
}

// Implementieren Sie hier die Circle und Rectangle Klassen
```

## Erwartete Ausgabe

```
Kreis:
- Fläche: 78.54 (bei Radius 5)
- Umfang: 31.42

Rechteck:
- Fläche: 20 (bei Länge 5, Breite 4)
- Umfang: 18
```

## Lösungshinweise

1. Für die Shape-Klasse:
   - Verwenden Sie das `abstract` Keyword für die Klasse und die Methoden
   - Die Eigenschaft Name kann als normale Property implementiert werden

2. Für die Circle-Klasse:
   - Verwenden Sie `Math.PI` für die Kreiszahl π
   - Denken Sie an das `override` Keyword bei den implementierten Methoden
   - Beispiel für die Flächenberechnung: `return Math.PI * Radius * Radius;`

3. Für die Rectangle-Klasse:
   - Implementieren Sie zuerst die Properties für Length und Width
   - Die Berechnungen sind einfache arithmetische Operationen
   - Beispiel für den Umfang: `return 2 * (Length + Width);`

4. Für die Main-Methode:

   ```csharp
   Shape[] shapes = new Shape[2];
   shapes[0] = new Circle { Name = "Kreis", Radius = 5 };
   shapes[1] = new Rectangle { Name = "Rechteck", Length = 5, Width = 4 };

   foreach(var shape in shapes)
   {
       Console.WriteLine($"{shape.Name}:");
       Console.WriteLine($"- Fläche: {shape.CalculateArea():F2}");
       Console.WriteLine($"- Umfang: {shape.CalculatePerimeter():F2}\n");
   }
   ```

5. Tipps für die Formatierung:
   - Verwenden Sie `:F2` bei der String-Formatierung für 2 Dezimalstellen
   - Nutzen Sie `$` für String-Interpolation

## MSDN Dokumentation Ressourcen für Übung 1

### Grundlegende Konzepte

1. [Abstrakte Klassen und abstrakte Methoden](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members)
   - Erklärung und Verwendung des `abstract` Keywords
   - Implementierung abstrakter Methoden

2. [Properties in C#](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/properties)
   - Syntax und Verwendung von Properties
   - Auto-implemented Properties

### Mathematische Operationen

3. [Math Klasse](https://learn.microsoft.com/de-de/dotnet/api/system.math)
   - `Math.PI` für Kreisberechnungen
   - Mathematische Konstanten und Methoden

### Arrays und Vererbung

4. [Arrays (C# Programmierhandbuch)](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/arrays/)
   - Array-Deklaration und -Initialisierung
   - Array von Objekten

5. [Vererbung in C#](https://learn.microsoft.com/de-de/dotnet/csharp/fundamentals/object-oriented/inheritance)
   - Basisklassen und abgeleitete Klassen
   - `override` Keyword

### Formatierung und Ausgabe

6. [String-Interpolation](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/tokens/interpolated)
   - Verwendung von `$` Strings
   - Formatierungsoptionen (z.B. `:F2` für 2 Dezimalstellen)

7. [Standardnummerierungsformate](https://learn.microsoft.com/de-de/dotnet/standard/base-types/standard-numeric-format-strings)
   - "F" Format für Festkommazahlen
   - Formatierungsoptionen für numerische Ausgaben
