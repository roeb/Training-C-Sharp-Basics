# Demos: Namespaces und Using-Direktiven

## Demo 1: Grundlegende Namespace-Struktur

```csharp
// Demo1.cs
namespace MeineFirma
{
    public class Kunde
    {
        public string Name { get; set; }
    }
}

// Verwendung:
class Program
{
    static void Main()
    {
        // Vollqualifiziert ohne using
        MeineFirma.Kunde kunde = new MeineFirma.Kunde();
        kunde.Name = "Max Mustermann";
    }
}
```

## Demo 2: Using-Direktiven

```csharp
// Demo2.cs
using System;  // Für Console
using MeineFirma;  // Für unsere eigenen Klassen

class Program
{
    static void Main()
    {
        // Dank using-Direktive können wir direkt die Klasse verwenden
        Kunde kunde = new Kunde();
        kunde.Name = "Max Mustermann";
        Console.WriteLine($"Kundenname: {kunde.Name}");
    }
}
```

## Demo 3: Namespace-Aliase

```csharp
// Demo3.cs
using System;
using MF = MeineFirma;  // Alias für längere Namespace-Namen
using Konsole = System.Console;  // Alias für häufig verwendete Klassen

class Program
{
    static void Main()
    {
        // Verwendung mit Alias
        MF.Kunde kunde = new MF.Kunde();
        kunde.Name = "Max Mustermann";
        Konsole.WriteLine($"Kundenname: {kunde.Name}");
    }
}
```

## Demo 4: Verschachtelte Namespaces

```csharp
// Demo4.cs
namespace MeineFirma
{
    namespace Verwaltung
    {
        public class Mitarbeiter
        {
            public string Name { get; set; }
            public int PersonalNummer { get; set; }
        }
    }

    namespace Buchhaltung
    {
        public class Rechnung
        {
            public decimal Betrag { get; set; }
            public string RechnungsNummer { get; set; }
        }
    }
}

// Alternative Schreibweise (moderner):
namespace MeineFirma.Verwaltung
{
    public class Abteilung
    {
        public string Name { get; set; }
    }
}

// Verwendung:
using MeineFirma.Verwaltung;
using MeineFirma.Buchhaltung;

class Program
{
    static void Main()
    {
        var mitarbeiter = new Mitarbeiter { Name = "Anna Schmidt", PersonalNummer = 1001 };
        var rechnung = new Rechnung { Betrag = 199.99m, RechnungsNummer = "RE2023-001" };
        var abteilung = new Abteilung { Name = "Entwicklung" };
    }
}
```

## Demo 5: Namespaces und Namenskonflikte

```csharp
// Demo5.cs
namespace MeineFirma.Shop
{
    public class Kunde
    {
        public string KundenNummer { get; set; }
    }
}

namespace MeineFirma.CRM
{
    public class Kunde
    {
        public string Kundenkontakt { get; set; }
    }
}

// Verwendung mit Konfliktlösung:
class Program
{
    static void Main()
    {
        // Explizite Namespace-Angabe bei Namenskonflikten
        MeineFirma.Shop.Kunde shopKunde = new MeineFirma.Shop.Kunde();
        MeineFirma.CRM.Kunde crmKunde = new MeineFirma.CRM.CRM();

        // Oder mit Alias
        using Shop = MeineFirma.Shop;
        using CRM = MeineFirma.CRM;

        Shop.Kunde kunde1 = new Shop.Kunde();
        CRM.Kunde kunde2 = new CRM.Kunde();
    }
}
```

## Präsentationstipps

1. **Schrittweise Vorgehensweise:**
   - Beginnen Sie mit Demo 1, um die Grundstruktur zu zeigen
   - Demonstrieren Sie den Vorteil von using-Direktiven in Demo 2
   - Zeigen Sie die Aliase als Vereinfachung in Demo 3
   - Erklären Sie die Organisation mit verschachtelten Namespaces in Demo 4
   - Verdeutlichen Sie den Umgang mit Namenskonflikten in Demo 5

2. **Wichtige Punkte zum Hervorheben:**
   - Namespaces dienen der Organisation und Vermeidung von Namenskonflikten
   - Using-Direktiven vereinfachen den Code und machen ihn lesbarer
   - Aliase sind nützlich bei langen Namespace-Namen oder Namenskonflikten
   - Moderne C#-Syntax für verschachtelte Namespaces (mit Punktnotation)

3. **Praktische Tipps:**
   - Zeigen Sie die IntelliSense-Unterstützung in Visual Studio
   - Demonstrieren Sie die automatische using-Direktiven-Ergänzung
   - Erklären Sie Best Practices für die Namespace-Organisation
   - Weisen Sie auf häufige Fehler und deren Vermeidung hin
