# Demos für Tag 3

## 1. Grundlegende Methoden und Parameter

### Methodendeklaration und Rückgabewerte

```csharp
// Einfache Methode ohne Rückgabewert
public void BegrüßeBenutzer(string name)
{
    Console.WriteLine($"Hallo {name}!");
}

// Methode mit Rückgabewert
public int AddiereZahlen(int a, int b)
{
    return a + b;
}

// Expression Body Methode (=>)
public double BerechneDurchschnitt(double a, double b) => (a + b) / 2;

// Methode mit mehreren return Statements
public string BestimmeNotenstufe(int punkte)
{
    if (punkte >= 90) return "Sehr gut";
    if (punkte >= 80) return "Gut";
    if (punkte >= 70) return "Befriedigend";
    if (punkte >= 60) return "Ausreichend";
    return "Nicht bestanden";
}
```

### Statische Methoden

```csharp
class Mathematik
{
    // Statische Methode zur Berechnung der Summe von zwei Zahlen
    public static int Addiere(int a, int b)
    {
        return a + b;
    }

    // Statische Methode zur Berechnung der Differenz von zwei Zahlen
    public static int Subtrahiere(int a, int b)
    {
        return a - b;
    }
}
```

### Methodenüberladung

```csharp
public class Rechner
{
    // Überladung mit verschiedenen Parameteranzahlen
    public int Addiere(int a, int b)
    {
        return a + b;
    }

    public int Addiere(int a, int b, int c)
    {
        return a + b + c;
    }

    // Überladung mit verschiedenen Datentypen
    public double Addiere(double a, double b)
    {
        return a + b;
    }

    // Überladung mit verschiedenen Parametertypen
    public string Verbinde(string a, string b)
    {
        return a + b;
    }

    public string Verbinde(string[] texte)
    {
        return string.Join(" ", texte);
    }
}
```

### Optionale Parameter und Named Parameters

```csharp
public class TextFormatter
{
    // Optionale Parameter mit Standardwerten
    public string FormatText(
        string text,
        bool upperCase = false,
        bool addTimestamp = false,
        string prefix = "")
    {
        if (upperCase)
            text = text.ToUpper();
        
        if (addTimestamp)
            text = $"[{DateTime.Now:HH:mm:ss}] {text}";
        
        return prefix + text;
    }
}

// Verwendung:
var formatter = new TextFormatter();

// Alle Parameter
formatter.FormatText("Hallo Welt", true, true, "MSG: ");

// Named Parameters (beliebige Reihenfolge)
formatter.FormatText(
    text: "Hallo Welt",
    prefix: "MSG: ",
    upperCase: true,
    addTimestamp: false
);

// Nur erforderlicher Parameter
formatter.FormatText("Hallo Welt");
```

## 2. Parameter-Modifikatoren

### ref Parameter

```csharp
public class ArrayManipulator
{
    // ref Parameter - Änderungen wirken sich auf das Original aus
    public void VerdoppleArray(ref int[] array)
    {
        for (int i = 0; i < array.Length; i++)
        {
            array[i] *= 2;
        }
    }

    // ref Parameter für einzelnen Wert
    public void Tausche(ref int a, ref int b)
    {
        int temp = a;
        a = b;
        b = temp;
    }
}

// Verwendung:
int[] zahlen = { 1, 2, 3 };
var manipulator = new ArrayManipulator();
manipulator.VerdoppleArray(ref zahlen);
// zahlen ist jetzt { 2, 4, 6 }

int x = 5, y = 10;
manipulator.Tausche(ref x, ref y);
// x ist jetzt 10, y ist jetzt 5
```

### out Parameter

```csharp
public class Statistik
{
    // Multiple out Parameter
    public bool BerechneMathematik(int[] zahlen, 
        out double durchschnitt, 
        out int minimum, 
        out int maximum)
    {
        if (zahlen == null || zahlen.Length == 0)
        {
            durchschnitt = 0;
            minimum = 0;
            maximum = 0;
            return false;
        }

        minimum = zahlen[0];
        maximum = zahlen[0];
        int summe = 0;

        foreach (int zahl in zahlen)
        {
            if (zahl < minimum) minimum = zahl;
            if (zahl > maximum) maximum = zahl;
            summe += zahl;
        }

        durchschnitt = (double)summe / zahlen.Length;
        return true;
    }
}

// Verwendung:
var stats = new Statistik();
int[] zahlen = { 1, 5, 3, 8, 2 };

if (stats.BerechneMathematik(zahlen, 
    out double avg, 
    out int min, 
    out int max))
{
    Console.WriteLine($"Durchschnitt: {avg}");
    Console.WriteLine($"Minimum: {min}");
    Console.WriteLine($"Maximum: {max}");
}
```

### params Parameter

```csharp
public class Logger
{
    // params erlaubt variable Anzahl von Parametern
    public void LogMessage(string format, params object[] args)
    {
        string message = string.Format(format, args);
        Console.WriteLine($"[{DateTime.Now:yyyy-MM-dd HH:mm:ss}] {message}");
    }
}

// Verwendung:
var logger = new Logger();
logger.LogMessage("Benutzer {0} hat sich angemeldet.", "Max");
logger.LogMessage("Werte: {0}, {1}, {2}", 1, "test", true);
logger.LogMessage("Einfache Nachricht");
```

## 3. Extension Methods

```csharp
// Extension Methods müssen in einer statischen Klasse sein
public static class StringExtensions
{
    // Extension Method für string
    public static int WortAnzahl(this string text)
    {
        if (string.IsNullOrWhiteSpace(text))
            return 0;
            
        return text.Split(new[] { ' ' }, 
            StringSplitOptions.RemoveEmptyEntries).Length;
    }

    // Extension Method mit Parameter
    public static string Kürzen(this string text, int maxLänge)
    {
        if (string.IsNullOrEmpty(text)) return text;
        return text.Length <= maxLänge ? text : text.Substring(0, maxLänge) + "...";
    }

    // Extension Method mit out Parameter
    public static bool ExtrahiereZahlen(this string text, 
        out int[] zahlen)
    {
        var matches = System.Text.RegularExpressions.Regex
            .Matches(text, @"\d+");
        
        zahlen = matches
            .Select(m => int.Parse(m.Value))
            .ToArray();
            
        return zahlen.Length > 0;
    }
}

// Verwendung von Extension Methods:
string text = "Dies ist ein Beispieltext mit 12 und 345 Zahlen";

// WortAnzahl
int anzahl = text.WortAnzahl();  // 9

// Kürzen
string gekürzt = text.Kürzen(20);  // "Dies ist ein Beispie..."

// ExtrahiereZahlen
if (text.ExtrahiereZahlen(out int[] zahlen))
{
    Console.WriteLine(string.Join(", ", zahlen));  // 12, 345
}
```

### Expression Body Syntax

```csharp
using System;

class ExpressionBodyDemo
{
    // Expression Body für eine Methode
    public static int Addiere(int a, int b) => a + b;

    // Expression Body für eine Eigenschaft
    private double radius;
    public double Radius
    {
        get => radius;
        set => radius = (value < 0) ? 0 : value;
    }

    // Expression Body für eine berechnete Eigenschaft
    public double Umfang => 2 * Math.PI * radius;

    // Expression Body im Konstruktor
    public ExpressionBodyDemo(double radius) => this.radius = radius;

    // Expression Body im Destruktor
    ~ExpressionBodyDemo() => Console.WriteLine("Destruktor aufgerufen!");

    static void Main()
    {
        // Verwendung der Methodensyntax
        int summe = Addiere(5, 10);
        Console.WriteLine($"Summe: {summe}");

        // Verwendung der Eigenschaft und des Konstruktors
        var kreis = new ExpressionBodyDemo(5);
        Console.WriteLine($"Radius: {kreis.Radius}");
        Console.WriteLine($"Umfang: {kreis.Umfang}");

        kreis.Radius = -3; // Setter in Aktion
        Console.WriteLine($"Radius nach dem Setzen eines negativen Wertes: {kreis.Radius}");
    }
}
```

### Delegate

```csharp
using System;

class DelegateDemo
{
    // Definition des Delegates
    delegate int Operation(int x, int y);

    static void Main()
    {
        // Initialisierung eines Delegates mit einer Methode
        Operation addieren = Addiere;
        int summe = addieren(10, 5);
        Console.WriteLine($"Summe: {summe}"); // Ausgabe: Summe: 15

        // Lambdafunktion mit dem gleichen Delegate verwenden
        Operation multipliziere = (x, y) => x * y;
        int produkt = multipliziere(10, 5);
        Console.WriteLine($"Produkt: {produkt}"); // Ausgabe: Produkt: 50
    }

    // Eine passende Methode für den Delegate
    static int Addiere(int a, int b)
    {
        return a + b;
    }
}
```

```csharp
delegate int Operation(int x, int y);

static int Addiere(int a, int b) => a + b;
static int Multipliziere(int a, int b) => a * b;

static void Main(string[] args)
{
    Operation? op = null;
    string operation = "Multipliziere";

    switch(operation)
    {
        case "Addiere":
            op = Addiere;
            break;

        case "Multipliziere":
            op = Multipliziere;
            break;
    }


    if(op != null)
    {
        Console.WriteLine(op(3, 4)); 
    }
}
```

### Delegate vs. Func

```csharp
using System;

class DelegatesAndFuncsDemo
{
    // Definition eines expliziten Delegates
    delegate int Operation(int x, int y);

    static void Main()
    {
        // Verwendung eines expliziten Delegates
        Operation addieren = (a, b) => a + b;
        Console.WriteLine($"Summe: {addieren(2, 3)}"); // Ausgabe: Summe: 5

        // Verwendung von Func als Alternative zu einem Delegate
        Func<int, int, int> multipliziere = (a, b) => a * b;
        Console.WriteLine($"Produkt: {multipliziere(2, 3)}"); // Ausgabe: Produkt: 6

        // Verwendung von Func in einer Methode
        VerwendeFunc((a, b) => a - b);
    }

    // Methode, die Func akzeptiert
    static void VerwendeFunc(Func<int, int, int> operation)
    {
        int ergebnis = operation(10, 5);
        Console.WriteLine($"Ergebnis der operation: {ergebnis}"); // Ausgabe: Ergebnis der operation: 5
    }
}
```

### `Func<T, TResult>`

`Func` wird verwendet, um Delegaten zu definieren, die eine Methode mit einem Rückgabewert darstellen. Der letzte Typparameter ist der Rückgabewert, und die vorherigen Typparameter sind die Eingabeparameter.

```csharp
using System;

class FuncDemo
{
    static void Main()
    {
        // Func, die zwei ints (a, b) nimmt und eine int (Summe) zurückgibt
        Func<int, int, int> addiere = (a, b) => a + b;

        int ergebnis = addiere(5, 3);
        Console.WriteLine($"Summe: {ergebnis}"); // Ausgabe: Summe: 8
    }
}
```

### `Action<T>`

`Action` wird verwendet, um Delegaten zu definieren, die eine Methode ohne Rückgabewert darstellen. Es kann null bis 16 Eingabeparameter haben.

```csharp
using System;

class ActionDemo
{
    static void Main()
    {
        // Action, die einen string nimmt und nichts zurückgibt
        Action<string> sagHallo = name => Console.WriteLine($"Hallo, {name}!");

        sagHallo("Welt"); // Ausgabe: Hallo, Welt!
    }
}
```

### Where nachbauen

```csharp
internal class Program
{
    static void Main(string[] args)
    {
        List<Person> list = new List<Person>();
        list.Add(new Person() { Name = "Hans", Age = 20 });
        list.Add(new Person() { Name = "Peter", Age = 30 });

        var result = list.MyWhere(p => p.Age < 30);

        foreach (var person in result)
        {
            Console.WriteLine(person.Name);
        }
    }
}

public static class EnumerableExtensions
{
    // Erweiterungsmethode, die die Funktionalität von Where nachbildet
    public static IEnumerable<Person> MyWhere<Person>(this IEnumerable<Person> source, Func<Person, bool> predicate)
    {
        if (source == null) throw new ArgumentNullException(nameof(source));
        if (predicate == null) throw new ArgumentNullException(nameof(predicate));

        foreach (var element in source)
        {
            if (predicate(element))
            {
                yield return element;
            }
        }
    }
}
```

## 4. Kombinierte Demo: Dokumenten-Analyzer

```csharp
public class Dokument
{
    public string Titel { get; set; }
    public string Inhalt { get; set; }
    public DateTime Erstellungsdatum { get; set; }
}

public static class DokumentAnalyzer
{
    // Methode mit optionalen Parametern
    public static void AnalysiereDokument(
        Dokument dok,
        bool zeigeStatistik = true,
        bool zeigeWörter = false)
    {
        Console.WriteLine($"Analyse von: {dok.Titel}");
        
        if (zeigeStatistik)
        {
            BerechneDokumentStatistik(dok.Inhalt,
                out int wortAnzahl,
                out int zeichenAnzahl,
                out double durchschnittlicheWortlänge);

            Console.WriteLine($"Wörter: {wortAnzahl}");
            Console.WriteLine($"Zeichen: {zeichenAnzahl}");
            Console.WriteLine($"Durchschnittliche Wortlänge: {durchschnittlicheWortlänge:F1}");
        }

        if (zeigeWörter)
        {
            var häufigsteWörter = FindeHäufigsteWörter(dok.Inhalt, 5);
            Console.WriteLine("Häufigste Wörter:");
            foreach (var wort in häufigsteWörter)
            {
                Console.WriteLine($"- {wort.Key}: {wort.Value}x");
            }
        }
    }

    // Methode mit out Parametern
    private static void BerechneDokumentStatistik(
        string text,
        out int wortAnzahl,
        out int zeichenAnzahl,
        out double durchschnittlicheWortlänge)
    {
        var wörter = text.Split(new[] { ' ', '\n', '\r', '\t' },
            StringSplitOptions.RemoveEmptyEntries);
            
        wortAnzahl = wörter.Length;
        zeichenAnzahl = text.Length;
        durchschnittlicheWortlänge = wörter.Average(w => w.Length);
    }

    // Methode mit ref Parameter
    public static void BereinigeDokument(ref string text)
    {
        text = text.Replace("  ", " ")
                   .Replace("\r\n", "\n")
                   .Trim();
    }

    // Methode mit params
    public static void FügeSuchmusterHinzu(
        ref string text,
        params string[] muster)
    {
        foreach (var m in muster)
        {
            text += $"\nSuchmuster: {m}";
        }
    }

    // Private Hilfsmethode
    private static Dictionary<string, int> FindeHäufigsteWörter(
        string text,
        int anzahl)
    {
        return text.Split(new[] { ' ', '\n', '\r', '\t' },
                StringSplitOptions.RemoveEmptyEntries)
            .GroupBy(w => w.ToLower())
            .OrderByDescending(g => g.Count())
            .Take(anzahl)
            .ToDictionary(g => g.Key, g => g.Count());
    }
}

// Extension Methods für Dokument
public static class DokumentExtensions
{
    public static bool IstLang(this Dokument dok, int minWörter = 100)
    {
        return dok.Inhalt.Split(' ').Length >= minWörter;
    }

    public static string ExtrahiereZusammenfassung(
        this Dokument dok,
        int maxLänge = 100)
    {
        return dok.Inhalt.Length <= maxLänge
            ? dok.Inhalt
            : dok.Inhalt.Substring(0, maxLänge) + "...";
    }
}

// Verwendung:
var dok = new Dokument
{
    Titel = "Beispieldokument",
    Inhalt = "Dies ist ein längerer Text mit vielen Wörtern. " +
             "Einige Wörter kommen mehrmals vor. " +
             "Text und Wörter sind wichtig in einem Text.",
    Erstellungsdatum = DateTime.Now
};

// Basis-Analyse
DokumentAnalyzer.AnalysiereDokument(dok);

// Detaillierte Analyse
DokumentAnalyzer.AnalysiereDokument(dok, 
    zeigeStatistik: true,
    zeigeWörter: true);

// Dokument bereinigen
string text = dok.Inhalt;
DokumentAnalyzer.BereinigeDokument(ref text);
dok.Inhalt = text;

// Suchmuster hinzufügen
DokumentAnalyzer.FügeSuchmusterHinzu(ref text, 
    "wichtig", 
    "Text",
    "Wörter");

// Extension Methods
bool istLang = dok.IstLang(50);
string zusammenfassung = dok.ExtrahiereZusammenfassung(80);
```

## Live Demo Ablauf

1. **Grundlegende Methoden**
   - Zeige verschiedene Methodendeklarationen
   - Demonstriere Expression Body Syntax
   - Führe Methodenüberladungen vor

2. **Parameter und Modifikatoren**
   - Erkläre optionale Parameter
   - Zeige Named Parameters in Aktion
   - Demonstriere ref, out und params

3. **Extension Methods**
   - Erstelle nützliche String-Extensions
   - Zeige wie sie verwendet werden

4. **Dokumenten-Analyzer**
   - Baue die Klassen Schritt für Schritt auf
   - Zeige wie verschiedene Methodentypen zusammenspielen
   - Demonstriere die Verwendung aller Features
