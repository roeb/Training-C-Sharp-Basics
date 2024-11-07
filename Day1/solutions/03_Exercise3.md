# Übung 3 - String-Manipulation und Formatierung

## Lösungen

### Teil 1

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        // Variablen deklarieren
        string vorname, nachname;
        int alter;
        double groesse;
        decimal gehalt;

        // Eingabe der Daten
        Console.WriteLine("Bitte geben Sie Ihre Daten ein:");
        
        Console.Write("Vorname: ");
        vorname = Console.ReadLine();

        Console.Write("Nachname: ");
        nachname = Console.ReadLine();

        // Eingabe Alter mit Fehlerbehandlung
        while (true)
        {
            Console.Write("Alter: ");
            if (int.TryParse(Console.ReadLine(), out alter))
                break;
            Console.WriteLine("Ungültige Eingabe! Bitte geben Sie eine ganze Zahl ein.");
        }

        // Eingabe Größe mit Fehlerbehandlung
        while (true)
        {
            Console.Write("Größe (in m): ");
            if (double.TryParse(Console.ReadLine(), out groesse))
                break;
            Console.WriteLine("Ungültige Eingabe! Bitte geben Sie eine Zahl ein (z.B. 1,80).");
        }

        // Eingabe Gehalt mit Fehlerbehandlung
        while (true)
        {
            Console.Write("Gehalt: ");
            if (decimal.TryParse(Console.ReadLine(), out gehalt))
                break;
            Console.WriteLine("Ungültige Eingabe! Bitte geben Sie eine Zahl ein.");
        }

        Console.WriteLine("\nAusgabe mit String-Interpolation:");
        
        // Ausgabe mit String-Interpolation
        Console.WriteLine($"Mein Name ist {vorname} {nachname}.");
        Console.WriteLine($"Ich bin {alter} Jahre alt und {groesse:F2}m groß.");
        Console.WriteLine($"Mein Gehalt beträgt {gehalt:C2}");
    }
}
```

### Teil 2

```csharp
// Annahme: vorname und nachname wurden bereits eingelesen
string vorname = "Max";
string nachname = "Mustermann";

// Initialen erstellen
string initialen = $"{vorname[0]}.{nachname[0]}.";
// Alternative Methode:
// string initialen = vorname.Substring(0,1) + "." + nachname.Substring(0,1) + ".";

// Namen in Groß- und Kleinbuchstaben
string grossbuchstaben = $"{vorname} {nachname}".ToUpper();
string kleinbuchstaben = $"{vorname} {nachname}".ToLower();

// Anzahl der Buchstaben (ohne Leerzeichen)
string komplettName = $"{vorname}{nachname}";
int anzahlBuchstaben = komplettName.Length;
// Alternative Methode:
// int anzahlBuchstaben = $"{vorname} {nachname}".Replace(" ", "").Length;

// Ausgabe
Console.WriteLine("\nString-Manipulationen:");
Console.WriteLine($"Initialen: {initialen}");
Console.WriteLine($"Name in Großbuchstaben: {grossbuchstaben}");
Console.WriteLine($"Name in Kleinbuchstaben: {kleinbuchstaben}");
Console.WriteLine($"Anzahl Buchstaben: {anzahlBuchstaben}");
```

### Teil 3

```csharp
// Konstanten für das Tabellenlayout
const int COL1_WIDTH = 16;  // Breite der ersten Spalte
const int COL2_WIDTH = 18;  // Breite der zweiten Spalte
const string HORIZONTAL_LINE = "+----------------+------------------+";

// Hilfsmethode zum Erstellen einer Tabellenzeile
static string CreateTableRow(string label, string value)
{
    return $"| {label.PadRight(COL1_WIDTH - 2)} | {value.PadRight(COL2_WIDTH - 2)} |";
}

// Ausgabe der formatierten Tabelle
Console.WriteLine(HORIZONTAL_LINE);
Console.WriteLine(CreateTableRow("Name", $"{vorname} {nachname}"));
Console.WriteLine(CreateTableRow("Alter", $"{alter} Jahre"));
Console.WriteLine(CreateTableRow("Größe", $"{groesse:F2} m"));
Console.WriteLine(CreateTableRow("Gehalt", $"{gehalt:C2}"));
Console.WriteLine(CreateTableRow("Initialen", initialen));
Console.WriteLine(HORIZONTAL_LINE);
```
