# Demos für Tag 4

## 1. Grundlegende Klassen und Objekte

### Erste Klasse: Person

```csharp
// Einfache Klasse mit Feldern
public class Person
{
    // Felder (Fields)
    private string name;
    private int alter;
    
    // Methode
    public void Vorstellen()
    {
        Console.WriteLine($"Hallo, ich bin {name} und {alter} Jahre alt.");
    }
    
    // Methoden zum Setzen der Felder
    public void SetName(string neuerName)
    {
        name = neuerName;
    }
    
    public void SetAlter(int neuesAlter)
    {
        if (neuesAlter >= 0)
        {
            alter = neuesAlter;
        }
    }
}

// Verwendung:
Person person = new Person();
person.SetName("Max");
person.SetAlter(25);
person.Vorstellen();
```

### Statische Dienstprogrammklasse

```csharp
public static class MathUtilities
{
    /// <summary>
    /// Addiert zwei Zahlen.
    /// </summary>
    public static double Add(double a, double b) => a + b;

    /// <summary>
    /// Subtrahiert eine Zahl von einer anderen.
    /// </summary>
    public static double Subtract(double a, double b) => a - b;

    /// <summary>
    /// Multipliziert zwei Zahlen.
    /// </summary>
    public static double Multiply(double a, double b) => a * b;

    /// <summary>
    /// Dividiert eine Zahl durch eine andere.
    /// </summary>
    public static double Divide(double a, double b) => a / b;
}

// Verwendung
class Program
{
    static void Main()
    {
        double sum = MathUtilities.Add(5, 3);
        Console.WriteLine($"Summe: {sum}"); // Ausgabe: Summe: 8
    }
}
```

### Statische Klasse als Konstantenlager

In diesem Beispiel wird die statische Klasse `Constants` genutzt, um unveränderliche Werte zu speichern, auf die überall im Code zugegriffen werden kann:

```csharp
public static class Constants
{
    public const double Pi = 3.14159;
    public const string AppName = "Meine Anwendung";
    public const int MaxUsers = 100;
}

// Verwendung
class Program
{
    static void Main()
    {
        Console.WriteLine($"Anwendungsname: {Constants.AppName}");
        Console.WriteLine($"Pi-Wert: {Constants.Pi}");
        Console.WriteLine($"Maximale Benutzer: {Constants.MaxUsers}");
    }
}
```

### Verbesserte Version mit Properties

```csharp
public class Person
{
    // Auto-implemented Properties
    public string Name { get; set; }
    public int Alter { get; set; }
    
    // Property mit Validierung
    private int alter;
    public int AlterMitValidierung
    {
        get { return alter; }
        set 
        { 
            if (value >= 0)
            {
                alter = value;
            }
        }
    }
    
    // Read-only Property
    public bool IstErwachsen
    {
        get { return Alter >= 18; }
    }
    
    public void Vorstellen()
    {
        Console.WriteLine($"Hallo, ich bin {Name} und {Alter} Jahre alt.");
        Console.WriteLine($"Ich bin {(IstErwachsen ? "erwachsen" : "minderjährig")}.");
    }
}

// Verwendung:
Person person = new Person();
person.Name = "Max";
person.Alter = 25;
person.Vorstellen();
```

## 2. Properties und Felder im Detail

### Produkt-Klasse mit verschiedenen Property-Typen

```csharp
public class Produkt
{
    // Private Felder
    private string name;
    private decimal preis;
    private int lagerbestand;
    
    // Full Property mit Validierung
    public string Name
    {
        get { return name; }
        set 
        { 
            if (!string.IsNullOrWhiteSpace(value))
            {
                name = value;
            }
        }
    }
    
    // Property mit Formatierung
    public decimal Preis
    {
        get { return preis; }
        set 
        { 
            if (value >= 0)
            {
                preis = Math.Round(value, 2);
            }
        }
    }
    
    // Auto-Property mit private set
    public int Artikelnummer { get; private set; }
    
    // Computed Property
    public bool IstVerfügbar
    {
        get { return lagerbestand > 0; }
    }
    
    // Property mit Backing Field und Events
    public int Lagerbestand
    {
        get { return lagerbestand; }
        set 
        { 
            if (value >= 0)
            {
                if (value == 0 && lagerbestand > 0)
                {
                    Console.WriteLine("Achtung: Produkt nicht mehr verfügbar!");
                }
                lagerbestand = value;
            }
        }
    }
    
    // Expression-bodied Property
    public string PreisFormatiert => $"{Preis:C}";
}

// Verwendung:
Produkt produkt = new Produkt();
produkt.Name = "Laptop";
produkt.Preis = 999.99m;
produkt.Lagerbestand = 5;

Console.WriteLine($"Produkt: {produkt.Name}");
Console.WriteLine($"Preis: {produkt.PreisFormatiert}");
Console.WriteLine($"Verfügbar: {produkt.IstVerfügbar}");

produkt.Lagerbestand = 0; // Löst Warnung aus
```

## 3. Records

Erstelle ein neues `record` in `Program.cs`:

```csharp
public record Person(string FirstName, string LastName);

// Optional: Mit Eigenschaften
public record Animal
{
    public string Name { get; init; }
    public string Species { get; init; }
}
```

Implementiere die `Main`-Methode, um ein Record zu erstellen:

```csharp
class Program
{
    static void Main(string[] args)
    {
        var person1 = new Person("Jane", "Doe");
        var person2 = new Person("Jane", "Doe");

        // Vergleichen von Records
        Console.WriteLine($"Sind die Personen gleich? {person1 == person2}"); // True

        // Kopieren mit Anpassung
        var person3 = person1 with { LastName = "Smith" };
        Console.WriteLine($"Person3: {person3}");

        // Ausgabe eines Records
        Console.WriteLine($"Person1: {person1}");
    }
}
```

## Tuples

```csharp
using System;

class TupleDemo
{
    static void Main()
    {
        // Erstellen eines unbenannten Tuples
        var tuple = (1, "Hallo", true);

        // Zugriff auf Tuple-Elemente über ItemX
        Console.WriteLine("Unbenannte Tuple:");
        Console.WriteLine($"Item1: {tuple.Item1}");
        Console.WriteLine($"Item2: {tuple.Item2}");
        Console.WriteLine($"Item3: {tuple.Item3}");

        // Erstellen eines benannten Tuples
        var benannterTuple = (ID: 42, Name: "Alice", IstAktiv: false);

        // Zugriff auf Tuple-Elemente über benannte Felder
        Console.WriteLine("\nBenannte Tuple:");
        Console.WriteLine($"ID: {benannterTuple.ID}");
        Console.WriteLine($"Name: {benannterTuple.Name}");
        Console.WriteLine($"IstAktiv: {benannterTuple.IstAktiv}");

        // Rückgabe mehrerer Werte aus einer Methode
        var ergebnisse = AddiereUndMultipliziere(3, 5);
        Console.WriteLine($"\nSumme: {ergebnisse.Summe}, Produkt: {ergebnisse.Produkt}");
    }

    // Methode gibt ein Tuple zurück
    static (int Summe, int Produkt) AddiereUndMultipliziere(int a, int b)
    {
        return (Summe: a + b, Produkt: a * b);
    }
}
```

---

## 4. Konstruktoren

### Bankkonto-Klasse mit verschiedenen Konstruktoren

```csharp
public class Bankkonto
{
    // Properties
    public string Kontonummer { get; private set; }
    public string Inhaber { get; private set; }
    public decimal Kontostand { get; private set; }
    public string Währung { get; private set; }
    
    // Standardkonstruktor
    public Bankkonto()
    {
        Kontonummer = GenerierKontonummer();
        Währung = "EUR";
        Kontostand = 0;
    }
    
    // Konstruktor mit Parametern
    public Bankkonto(string inhaber, decimal startguthaben)
        : this() // Ruft Standardkonstruktor auf
    {
        Inhaber = inhaber;
        if (startguthaben >= 0)
        {
            Kontostand = startguthaben;
        }
    }
    
    // Überladener Konstruktor mit Währung
    public Bankkonto(string inhaber, decimal startguthaben, string währung)
        : this(inhaber, startguthaben)
    {
        if (!string.IsNullOrWhiteSpace(währung))
        {
            Währung = währung.ToUpper();
        }
    }
    
    // Private Hilfsmethode
    private string GenerierKontonummer()
    {
        return "DE" + DateTime.Now.Ticks.ToString().Substring(0, 8);
    }
    
    // Geschäftsmethoden
    public void Einzahlen(decimal betrag)
    {
        if (betrag > 0)
        {
            Kontostand += betrag;
            Console.WriteLine($"Einzahlung: {betrag:C} {Währung}");
            ZeigeKontostand();
        }
    }
    
    public bool Abheben(decimal betrag)
    {
        if (betrag > 0 && Kontostand >= betrag)
        {
            Kontostand -= betrag;
            Console.WriteLine($"Abhebung: {betrag:C} {Währung}");
            ZeigeKontostand();
            return true;
        }
        Console.WriteLine("Abhebung nicht möglich!");
        return false;
    }
    
    private void ZeigeKontostand()
    {
        Console.WriteLine($"Aktueller Kontostand: {Kontostand:C} {Währung}");
    }
}

// Verwendung verschiedener Konstruktoren:
var konto1 = new Bankkonto();
var konto2 = new Bankkonto("Max Mustermann", 1000);
var konto3 = new Bankkonto("John Doe", 5000, "USD");

// Kontobewegungen
konto2.Einzahlen(500);
konto2.Abheben(200);
konto2.Abheben(2000); // Nicht möglich
```

## Destruktoren

```csharp
using System;
using System.IO;

class FileManager
{
    private FileStream _fileStream;

    public FileManager(string filePath)
    {
        // Datei öffnen und zuweisen
        _fileStream = new FileStream(filePath, FileMode.OpenOrCreate);
        Console.WriteLine("Datei geöffnet.");
    }

    // Destruktor zur Freigabe der Dateiressource
    ~FileManager()
    {
        // Überprüfung auf null zur Vermeidung doppelter Freigabe
        if (_fileStream != null)
        {
            _fileStream.Dispose();
            Console.WriteLine("Dateihandle freigegeben im Destruktor.");
        }
    }

    // Methode zur Schreiben von Daten in die Datei
    public void WriteData(string data)
    {
        if (_fileStream == null)
            throw new ObjectDisposedException(nameof(FileManager));

        byte[] bytes = System.Text.Encoding.UTF8.GetBytes(data);
        _fileStream.Write(bytes, 0, bytes.Length);
    }
}

class Program
{
    static void Main()
    {
        FileManager fileManager = new FileManager("beispiel.txt");

        // Schreibe einige Daten in die Datei
        fileManager.WriteData("Hallo, Welt!");

        // Am Ende des Programms wird der Destruktor von FileManager aufgerufen
    }
}
```

## Ohne Destruktor aber mit Using

```csharp
using System;
using System.IO;

class FileManager : IDisposable
{
    private FileStream _fileStream;

    public FileManager(string filePath)
    {
        // Datei öffnen und zuweisen
        _fileStream = new FileStream(filePath, FileMode.OpenOrCreate);
        Console.WriteLine("Datei geöffnet.");
    }

    // Dispose-Methode zur Freigabe der Ressourcen
    public void Dispose()
    {
        Dispose(true);
        GC.SuppressFinalize(this);
    }

    // Geschützte Dispose-Methode zur eigentlichen Freigabe, erlaubt ggf. erweiterte Klassen
    protected virtual void Dispose(bool disposing)
    {
        if (disposing)
        {
            // Verwalte Ressourcen freigeben
            if (_fileStream != null)
            {
                _fileStream.Dispose();
                _fileStream = null; // Sicherstellen, dass es nicht erneut freigegeben wird
                Console.WriteLine("Dateihandle freigegeben.");
            }
        }

        // Nicht verwaltete Ressourcen freigeben, falls vorhanden
    }

    // Methode zum Schreiben von Daten in die Datei
    public void WriteData(string data)
    {
        if (_fileStream == null)
            throw new ObjectDisposedException(nameof(FileManager));

        byte[] bytes = System.Text.Encoding.UTF8.GetBytes(data);
        _fileStream.Write(bytes, 0, bytes.Length);
    }
}

class Program
{
    static void Main()
    {
        // Verwendung des using-Statements für automatische Ressourcenfreigabe
        using (var fileManager = new FileManager("beispiel.txt"))
        {
            // Schreibe einige Daten in die Datei
            fileManager.WriteData("Hallo, Welt!");
        } // Hier wird Dispose automatisch aufgerufen
    }
}
```

## 5. Kombinierte Demo: Bibliotheksverwaltung

```csharp
public class Buch
{
    // Properties
    public string ISBN { get; }
    public string Titel { get; private set; }
    public string Autor { get; private set; }
    private int _seitenzahl;
    public int Seitenzahl
    {
        get => _seitenzahl;
        set
        {
            if (value > 0)
                _seitenzahl = value;
        }
    }
    
    // Berechnetes Property
    public bool IstLangesBuch => Seitenzahl > 500;
    
    // Konstruktoren
    public Buch(string isbn, string titel, string autor)
    {
        ISBN = isbn;
        Titel = titel;
        Autor = autor;
    }
    
    public Buch(string isbn, string titel, string autor, int seitenzahl)
        : this(isbn, titel, autor)
    {
        Seitenzahl = seitenzahl;
    }
}

public class Bibliothek
{
    private List<Buch> bücher;
    public string Name { get; }
    
    // Property mit Backing Field und Validierung
    private string _standort;
    public string Standort
    {
        get => _standort;
        set
        {
            if (!string.IsNullOrWhiteSpace(value))
                _standort = value;
        }
    }
    
    // Readonly Property
    public int AnzahlBücher => bücher.Count;
    
    // Konstruktor
    public Bibliothek(string name)
    {
        Name = name;
        bücher = new List<Buch>();
    }
    
    // Methoden
    public void BuchHinzufügen(Buch buch)
    {
        if (buch != null && !bücher.Any(b => b.ISBN == buch.ISBN))
        {
            bücher.Add(buch);
            Console.WriteLine($"Buch '{buch.Titel}' wurde hinzugefügt.");
        }
    }
    
    public void ZeigeBücherListe()
    {
        Console.WriteLine($"\nBücherliste der Bibliothek {Name}:");
        foreach (var buch in bücher)
        {
            Console.WriteLine($"- {buch.Titel} von {buch.Autor}" +
                            $" ({buch.Seitenzahl} Seiten)");
        }
        Console.WriteLine($"Gesamt: {AnzahlBücher} Bücher");
    }
    
    public void ZeigeLangeBücher()
    {
        var langeBücher = bücher.Where(b => b.IstLangesBuch).ToList();
        Console.WriteLine("\nLange Bücher (>500 Seiten):");
        foreach (var buch in langeBücher)
        {
            Console.WriteLine($"- {buch.Titel} ({buch.Seitenzahl} Seiten)");
        }
    }
}

// Verwendung:
var bibliothek = new Bibliothek("Stadtbibliothek");
bibliothek.Standort = "Hauptstraße 1";

var buch1 = new Buch("978-3-86680-192-9", "Der Herr der Ringe", "J.R.R. Tolkien", 1200);
var buch2 = new Buch("978-3-12-345678-9", "Clean Code", "Robert C. Martin", 464);
var buch3 = new Buch("978-3-86680-192-8", "Die unendliche Geschichte", "Michael Ende", 800);

bibliothek.BuchHinzufügen(buch1);
bibliothek.BuchHinzufügen(buch2);
bibliothek.BuchHinzufügen(buch3);

bibliothek.ZeigeBücherListe();
bibliothek.ZeigeLangeBücher();
```

## Live Demo Ablauf

1. **Grundlegende Klassen**
   - Erstelle einfache Person-Klasse
   - Zeige Unterschied zwischen Feldern und Properties
   - Demonstriere Zugriff auf private Felder

2. **Properties**
   - Implementiere verschiedene Property-Typen
   - Zeige Validierung in Properties
   - Demonstriere computed Properties

3. **Konstruktoren**
   - Erstelle verschiedene Konstruktoren
   - Zeige Konstruktor-Verkettung
   - Demonstriere Parameter-Validierung

4. **Bibliotheksverwaltung**
   - Baue die Klassen Schritt für Schritt auf
   - Zeige Zusammenspiel von Properties und Konstruktoren
   - Demonstriere Objektinteraktion
