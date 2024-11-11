# Demos für Tag 1

## 1. VB.NET vs C# Vergleich

### Beispiel 1: Case Sensitivity

```vb
' VB.NET
Dim MyVariable As String = "Hello"
Console.WriteLine(myvariable)  ' Funktioniert in VB.NET
```

```csharp
// C#
string MyVariable = "Hello";
Console.WriteLine(myvariable);  // Compilerfehler in C#! Case sensitive
```

### Beispiel 2: Blockstruktur

```vb
' VB.NET
If age >= 18 Then
    Console.WriteLine("Volljährig")
End If
```

```csharp
// C#
if (age >= 18)
{
    Console.WriteLine("Volljährig");
}
```

### Beispiel 3: Properties

```vb
' VB.NET
Public Property Name As String
    Get
        Return _name
    End Get
    Set(value As String)
        _name = value
    End Set
End Property
```

```csharp
// C#
public string Name
{
    get { return _name; }
    set { _name = value; }
}

// Oder noch kürzer in C#:
public string Name { get; set; }
```

## 2. Visual Studio Features Demo

### Beispiel 1: IntelliSense und Code Completion

```csharp
using System;

class Program
{
    static void Main()
    {
        string text = "Hello";
        // Tippe 'text.' und zeige IntelliSense
        // text.Length
        // text.ToUpper()
        // etc.
    }
}
```

### Beispiel 2: Quick Actions und Refactoring

```csharp
// 1. Schreibe: Console.WriteLine("Hello")
// 2. Zeige Glühbirne für 'using System' Vorschlag
// 3. Extrahiere in separate Methode mit Ctrl+R, Ctrl+M
```

## 3. Grundlegende Syntax

### Beispiel 1: Variablen und Datentypen

```csharp
// Explizite Typisierung
int alter = 25;
double gewicht = 75.5;
string name = "Max";
bool istStudent = true;

// Implizite Typisierung mit var
var zahl = 42;        // int
var text = "Hallo";   // string
var preis = 19.99;    // double
```

### Beispiel 2: String-Formatierung

```csharp
string name = "Anna";
int alter = 30;

// Traditionelle Formatierung
Console.WriteLine("Name: {0}, Alter: {1}", name, alter);

// String-Interpolation (modern)
Console.WriteLine($"Name: {name}, Alter: {alter}");

// Mit Formatierung
double preis = 19.99;
Console.WriteLine($"Preis: {preis:C}");  // Währungsformat
Console.WriteLine($"Preis: {preis:F2}"); // 2 Dezimalstellen
```

### Beispiel 3: Typkonvertierung

```csharp
// Implizite Konvertierung (sicher)
int zahl = 100;
long grosseZahl = zahl;  // int -> long

// Explizite Konvertierung (Cast)
double d = 123.45;
int i = (int)d;  // Nachkommastellen werden abgeschnitten

// Parse und TryParse
string eingabe = "42";
int ergebnis = int.Parse(eingabe);

// Sicheres Parsen mit TryParse
string userEingabe = "123";
if (int.TryParse(userEingabe, out int resultat))
{
    Console.WriteLine($"Erfolgreich geparst: {resultat}");
}
else
{
    Console.WriteLine("Ungültige Eingabe");
}
```

### Beispiel 4: Operatoren

```csharp
int a = 10;
int b = 3;

// Arithmetische Operatoren
Console.WriteLine($"Addition: {a + b}");      // 13
Console.WriteLine($"Subtraktion: {a - b}");   // 7
Console.WriteLine($"Multiplikation: {a * b}"); // 30
Console.WriteLine($"Division: {a / b}");       // 3
Console.WriteLine($"Modulo: {a % b}");        // 1

// Inkrement/Dekrement
int x = 5;
Console.WriteLine($"x++: {x++}"); // Zeigt 5, dann erhöht auf 6
Console.WriteLine($"++x: {++x}"); // Erhöht auf 7, dann zeigt 7
```

### Beispiel 5: Enums und ihre Verwendung

```csharp
// Definition eines Enums
public enum Wochentag
{
    Montag = 1,
    Dienstag,    // automatisch 2
    Mittwoch,    // automatisch 3
    Donnerstag,
    Freitag,
    Samstag,
    Sonntag
}

// Verwendung von Enums
Wochentag heute = Wochentag.Mittwoch;
Console.WriteLine($"Heute ist {heute}");              // Gibt "Mittwoch" aus
Console.WriteLine($"Tag Nummer: {(int)heute}");       // Gibt "3" aus

// Enum Parsing
Wochentag tag = Enum.Parse<Wochentag>("Freitag");    // String zu Enum
bool istWochenende = tag == Wochentag.Samstag || tag == Wochentag.Sonntag;

// Alle Enum-Werte durchlaufen
foreach (Wochentag tag in Enum.GetValues(typeof(Wochentag)))
{
    Console.WriteLine($"- {tag}");
}
```

### Beispiel 6: Var - Sinnvolle Verwendung vs. Grenzen

#### Sinnvolle Verwendung von var

```csharp
// 1. Bei offensichtlichem Typ durch Initialisierung
var alter = 25;                  // Klar erkennbar als int
var name = "Max";               // Klar erkennbar als string
var liste = new List<string>(); // Vermeidet Typwiederholung

// 2. Bei komplexen Typen (verbessert Lesbarkeit)
var dictionary = new Dictionary<string, List<CustomerData>>();
// Besser als: Dictionary<string, List<CustomerData>> dictionary = new Dictionary<string, List<CustomerData>>();

// 3. Bei LINQ-Abfragen
var ergebnis = from p in products
               where p.Price > 100
               select new { p.Name, p.Price };

// 4. Bei Tuple-Rückgaben
var (vorname, nachname) = GetPersonDetails();
```

#### Wo var vermieden werden sollte

```csharp
// 1. Bei nicht offensichtlichen Typen
var result = GetData();          // Unklar, welcher Typ zurückgegeben wird
var value = Calculate(x, y);     // Typ nicht direkt ersichtlich

// 2. Bei Numerischen Typen mit spezifischen Anforderungen
decimal preis = 19.99m;          // Besser als: var preis = 19.99m
int anzahl = 5;                  // Besser als: var anzahl = 5
// Hier ist die explizite Typisierung besser, da sie die Intention klar macht

// 3. Bei Interface-Typen
IEnumerable<string> namen = GetNames();  // Besser als: var namen = GetNames()
// Explizite Interface-Deklaration macht die Verwendungsabsicht klar

// 4. Bei Typen, die für das Verständnis wichtig sind
DateTime geburtsdatum = DateTime.Now;    // Besser als: var geburtsdatum = DateTime.Now
TimeSpan zeitspanne = TimeSpan.FromHours(2); // Besser als: var zeitspanne = TimeSpan.FromHours(2)
```

## Live Demo Ablauf

1. **VB.NET vs C# Vergleich**
   - Erstelle zwei Projekte (VB.NET und C#)
   - Zeige die Syntax-Unterschiede live
   - Demonstriere Case Sensitivity Fehler

2. **Visual Studio Features**
   - Zeige IntelliSense während der Code-Eingabe
   - Demonstriere Code-Navigation
   - Nutze verschiedene Shortcuts
   - Zeige Debug-Features

3. **Syntax Grundlagen**
   - Erstelle ein neues Konsolenprojekt
   - Implementiere die Beispiele Schritt für Schritt
   - Zeige Compiler-Fehler und wie man sie behebt
   - Demonstriere verschiedene String-Formatierungen
   - Führe Typkonvertierungen vor

4. **Enums und Var**
   - Zeige die verschiedenen Möglichkeiten mit Enums
   - Demonstriere die Vor- und Nachteile von var
   - Zeige praktische Beispiele, wo var sinnvoll ist
   - Zeige Fälle, wo var zu Verwirrung führen kann
