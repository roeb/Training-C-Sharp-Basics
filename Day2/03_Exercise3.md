# Übung 3 - Telefonbuch-Verwaltung

## Aufgabenstellung

Entwickeln Sie eine Konsolenanwendung zur Verwaltung eines einfachen Telefonbuchs mit Grundfunktionen zum Hinzufügen, Suchen und Anzeigen von Kontakten.

## Anforderungen

1. Hauptmenü erstellen
   ```text
   === Telefonbuch ===
   1. Kontakt hinzufügen
   2. Alle Kontakte anzeigen
   3. Kontakt suchen
   4. Beenden
   ```

2. Kontaktverwaltung
   - Kontakte mit Name, Telefonnummer und E-Mail speichern
   - Keine doppelten Telefonnummern erlauben
   - Eingaben auf Gültigkeit prüfen

3. Suchfunktion
   - Nach Namen oder Telefonnummer suchen
   - Teilweise Übereinstimmungen erlauben
   - Groß-/Kleinschreibung ignorieren

## Datenstruktur

```csharp
class Contact
{
    public string Name { get; set; }
    public string PhoneNumber { get; set; }
    public string Email { get; set; }
}

// Liste für die Kontakte
List<Contact> contacts = new List<Contact>();
```

## Beispielausgabe

```text
=== Kontakt hinzufügen ===
Name: Max Mustermann
Telefon: 0123-456789
E-Mail: max@example.com
Kontakt wurde gespeichert!

=== Kontakte anzeigen ===
1. Max Mustermann
   Tel: 0123-456789
   E-Mail: max@example.com
2. Anna Schmidt
   Tel: 0987-654321
   E-Mail: anna@example.com

=== Kontakt suchen ===
Suchbegriff: max
Gefunden:
- Max Mustermann (0123-456789)
```

## Validierungsregeln

- Name: mindestens 3 Zeichen
- Telefon: nur Zahlen und '-' erlaubt
- E-Mail: muss '@' enthalten
- Keine leeren Eingaben

## Beispielcode-Struktur

```csharp
class Program
{
    static List<Contact> contacts = new List<Contact>();

    static void Main(string[] args)
    {
        bool running = true;
        while (running)
        {
            ShowMenu();
            switch (GetUserChoice())
            {
                case 1:
                    AddContact();
                    break;
                case 2:
                    ShowContacts();
                    break;
                case 3:
                    SearchContact();
                    break;
                case 4:
                    running = false;
                    break;
            }
        }
    }

    static void ShowMenu()
    {
        Console.WriteLine("\n=== Telefonbuch ===");
        // Implementierung
    }

    static int GetUserChoice()
    {
        // Implementierung der Benutzereingabe
    }

    static void AddContact()
    {
        Console.WriteLine("\n=== Kontakt hinzufügen ===");
        // Implementierung
    }

    static void ShowContacts()
    {
        Console.WriteLine("\n=== Kontakte anzeigen ===");
        // Implementierung
    }

    static void SearchContact()
    {
        Console.WriteLine("\n=== Kontakt suchen ===");
        // Implementierung
    }
}
```
