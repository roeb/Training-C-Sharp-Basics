# Demos für Tag 2

## 1. Kontrollstrukturen

### If/Else Demos

```csharp
// Grundlegende if/else Struktur
int alter = 18;
if (alter >= 18)
{
    Console.WriteLine("Volljährig");
}
else
{
    Console.WriteLine("Minderjährig");
}

// Mehrfache Bedingungen
double note = 2.3;
if (note <= 1.5)
{
    Console.WriteLine("Sehr gut");
}
else if (note <= 2.5)
{
    Console.WriteLine("Gut");
}
else if (note <= 3.5)
{
    Console.WriteLine("Befriedigend");
}
else
{
    Console.WriteLine("Ausreichend oder schlechter");
}

// Verschachtelte if-Anweisungen
bool istRegistriert = true;
bool istAdmin = false;

if (istRegistriert)
{
    if (istAdmin)
    {
        Console.WriteLine("Admin-Bereich");
    }
    else
    {
        Console.WriteLine("Benutzer-Bereich");
    }
}
```

### Switch Demos

```csharp
// Klassisches switch
int tag = 3;
switch (tag)
{
    case 1:
        Console.WriteLine("Montag");
        break;
    case 2:
        Console.WriteLine("Dienstag");
        break;
    case 3:
        Console.WriteLine("Mittwoch");
        break;
    default:
        Console.WriteLine("Anderer Tag");
        break;
}

// Switch mit pattern matching
object obj = "Hello";
switch (obj)
{
    case string s when s.Length > 5:
        Console.WriteLine($"Langer String: {s}");
        break;
    case string s:
        Console.WriteLine($"Kurzer String: {s}");
        break;
    case int i:
        Console.WriteLine($"Zahl: {i}");
        break;
    default:
        Console.WriteLine("Unbekannter Typ");
        break;
}

// Switch Expression (C# 8.0+)
string GetDayType(DayOfWeek day) => day switch
{
    DayOfWeek.Saturday or DayOfWeek.Sunday => "Wochenende",
    _ => "Arbeitstag"
};
```

### Schleifen Demos

```csharp
// For-Schleife
Console.WriteLine("For-Schleife:");
for (int i = 0; i < 5; i++)
{
    Console.WriteLine($"Durchlauf {i + 1}");
}

// Foreach-Schleife
string[] farben = { "Rot", "Grün", "Blau" };
Console.WriteLine("\nForeach-Schleife:");
foreach (string farbe in farben)
{
    Console.WriteLine(farbe);
}

// While-Schleife
Console.WriteLine("\nWhile-Schleife:");
int count = 0;
while (count < 3)
{
    Console.WriteLine($"Count: {count}");
    count++;
}

// Do-While-Schleife
Console.WriteLine("\nDo-While-Schleife:");
int nummer = 1;
do
{
    Console.WriteLine($"Nummer: {nummer}");
    nummer++;
} while (nummer <= 3);

// Break und Continue
Console.WriteLine("\nBreak und Continue:");
for (int i = 0; i < 5; i++)
{
    if (i == 2) continue; // Überspringt 2
    if (i == 4) break;    // Beendet bei 4
    Console.WriteLine(i);
}
```

## 2. Arrays und Collections

### Array Demos

```csharp
// Eindimensionales Array
int[] zahlen = new int[5];
zahlen[0] = 1;
zahlen[1] = 2;
zahlen[2] = 3;
zahlen[3] = 4;
zahlen[4] = 5;

// Alternative Initialisierung
int[] zahlenKurz = { 1, 2, 3, 4, 5 };

// Mehrdimensionales Array
int[,] matrix = new int[2, 3] 
{
    { 1, 2, 3 },
    { 4, 5, 6 }
};

// Array durchlaufen
foreach (int zahl in zahlen)
{
    Console.WriteLine(zahl);
}

// Matrix durchlaufen
for (int i = 0; i < matrix.GetLength(0); i++)
{
    for (int j = 0; j < matrix.GetLength(1); j++)
    {
        Console.Write($"{matrix[i,j]} ");
    }
    Console.WriteLine();
}
```

### List Demo

```csharp
// List<T> Grundlagen
List<string> namen = new List<string>();
namen.Add("Anna");
namen.Add("Ben");
namen.Add("Clara");

// Alternative Initialisierung
List<string> namenKurz = new List<string> { "Anna", "Ben", "Clara" };

// List Operationen
namen.Remove("Ben");           // Element entfernen
bool hatAnna = namen.Contains("Anna");  // Prüfen ob Element existiert
namen.Sort();                 // Liste sortieren
namen.Reverse();             // Liste umdrehen

// List durchlaufen
foreach (string name in namen)
{
    Console.WriteLine(name);
}
```

### Dictionary Demo

```csharp
// Dictionary<TKey, TValue> Grundlagen
Dictionary<string, int> altersListe = new Dictionary<string, int>();
altersListe.Add("Anna", 25);
altersListe["Ben"] = 30;
altersListe["Clara"] = 35;

// Wert abrufen
if (altersListe.TryGetValue("Anna", out int alter))
{
    Console.WriteLine($"Anna ist {alter} Jahre alt");
}

// Dictionary durchlaufen
foreach (KeyValuePair<string, int> eintrag in altersListe)
{
    Console.WriteLine($"{eintrag.Key} ist {eintrag.Value} Jahre alt");
}
```

### LINQ Grundlagen Demo

```csharp
List<int> zahlen = new List<int> { 1, 5, 3, 8, 2, 9, 4, 7, 6 };

// Where - Filtert Elemente
var geradeZahlen = zahlen.Where(z => z % 2 == 0);
Console.WriteLine("Gerade Zahlen:");
foreach (int z in geradeZahlen)
{
    Console.WriteLine(z);  // 8, 2, 4, 6
}

// OrderBy - Sortiert Elemente
var sortiertZahlen = zahlen.OrderBy(z => z);
Console.WriteLine("\nSortierte Zahlen:");
foreach (int z in sortiertZahlen)
{
    Console.WriteLine(z);  // 1, 2, 3, 4, 5, 6, 7, 8, 9
}

// Select - Transformiert Elemente
var verdoppelt = zahlen.Select(z => z * 2);
Console.WriteLine("\nVerdoppelte Zahlen:");
foreach (int z in verdoppelt)
{
    Console.WriteLine(z);  // 2, 10, 6, 16, 4, 18, 8, 14, 12
}
```

## 3. Kombinierte Demo: Einkaufsliste

```csharp
class Produkt
{
    public string Name { get; set; }
    public double Preis { get; set; }
    public int Menge { get; set; }
}

class Einkaufsliste
{
    private List<Produkt> produkte = new List<Produkt>();

    public void ProduktHinzufügen(string name, double preis, int menge)
    {
        var produkt = new Produkt 
        { 
            Name = name, 
            Preis = preis, 
            Menge = menge 
        };
        produkte.Add(produkt);
    }

    public void ListeAnzeigen()
    {
        if (produkte.Count == 0)
        {
            Console.WriteLine("Die Einkaufsliste ist leer!");
            return;
        }

        Console.WriteLine("Einkaufsliste:");
        foreach (var produkt in produkte.OrderBy(p => p.Name))
        {
            Console.WriteLine($"- {produkt.Name}: {produkt.Menge}x {produkt.Preis:C}");
        }

        var gesamtpreis = produkte.Sum(p => p.Preis * p.Menge);
        Console.WriteLine($"\nGesamtpreis: {gesamtpreis:C}");
    }

    public void TeureProdukteSuchen(double preisgrenze)
    {
        var teureProdukte = produkte
            .Where(p => p.Preis > preisgrenze)
            .OrderByDescending(p => p.Preis);

        Console.WriteLine($"\nProdukte über {preisgrenze:C}:");
        foreach (var produkt in teureProdukte)
        {
            Console.WriteLine($"- {produkt.Name}: {produkt.Preis:C}");
        }
    }
}

// Verwendung
var liste = new Einkaufsliste();
liste.ProduktHinzufügen("Äpfel", 2.99, 5);
liste.ProduktHinzufügen("Brot", 3.49, 2);
liste.ProduktHinzufügen("Milch", 1.79, 3);
liste.ProduktHinzufügen("Käse", 4.99, 1);

liste.ListeAnzeigen();
liste.TeureProdukteSuchen(3.00);
```

## Live Demo Ablauf

1. **Kontrollstrukturen**
   - Demonstriere if/else mit verschiedenen Bedingungen
   - Zeige switch mit pattern matching
   - Führe verschiedene Schleifentypen vor
   - Erkläre break/continue anhand praktischer Beispiele

2. **Arrays und Collections**
   - Erstelle und manipuliere Arrays
   - Zeige List<T> Operationen
   - Demonstriere Dictionary Verwendung
   - Führe LINQ-Grundlagen vor

3. **Einkaufslisten-Demo**
   - Implementiere die Klassen Schritt für Schritt
   - Zeige wie verschiedene Konzepte zusammenspielen
   - Demonstriere LINQ-Abfragen auf der Liste
   - Füge interaktiv neue Produkte hinzu
