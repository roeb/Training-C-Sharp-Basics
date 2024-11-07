# Übung 3 - Telefonbuch-Verwaltung

## Lösung

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Contact
{
    public string Name { get; set; }
    public string PhoneNumber { get; set; }
    public string Email { get; set; }
}

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
        Console.WriteLine("1. Kontakt hinzufügen");
        Console.WriteLine("2. Alle Kontakte anzeigen");
        Console.WriteLine("3. Kontakt suchen");
        Console.WriteLine("4. Beenden");
    }

    static int GetUserChoice()
    {
        int choice;
        while (!int.TryParse(Console.ReadLine(), out choice) || choice < 1 || choice > 4)
        {
            Console.WriteLine("Ungültige Eingabe! Bitte wählen Sie 1-4.");
        }
        return choice;
    }

    static void AddContact()
    {
        Console.WriteLine("\n=== Kontakt hinzufügen ===");
        
        Console.Write("Name: ");
        string name = Console.ReadLine();
        if (string.IsNullOrEmpty(name) || name.Length < 3)
        {
            Console.WriteLine("Fehler: Name muss mindestens 3 Zeichen lang sein!");
            return;
        }

        Console.Write("Telefon: ");
        string phone = Console.ReadLine();
        if (string.IsNullOrEmpty(phone) || !phone.All(c => char.IsDigit(c) || c == '-'))
        {
            Console.WriteLine("Fehler: Telefonnummer darf nur Zahlen und '-' enthalten!");
            return;
        }

        if (contacts.Any(c => c.PhoneNumber == phone))
        {
            Console.WriteLine("Fehler: Diese Telefonnummer existiert bereits!");
            return;
        }

        Console.Write("E-Mail: ");
        string email = Console.ReadLine();
        if (string.IsNullOrEmpty(email) || !email.Contains('@'))
        {
            Console.WriteLine("Fehler: Ungültige E-Mail-Adresse!");
            return;
        }

        contacts.Add(new Contact { Name = name, PhoneNumber = phone, Email = email });
        Console.WriteLine("Kontakt wurde gespeichert!");
    }

    static void ShowContacts()
    {
        Console.WriteLine("\n=== Kontakte anzeigen ===");
        if (contacts.Count == 0)
        {
            Console.WriteLine("Keine Kontakte vorhanden.");
            return;
        }

        for (int i = 0; i < contacts.Count; i++)
        {
            Console.WriteLine($"{i + 1}. {contacts[i].Name}");
            Console.WriteLine($"   Tel: {contacts[i].PhoneNumber}");
            Console.WriteLine($"   E-Mail: {contacts[i].Email}");
        }
    }

    static void SearchContact()
    {
        Console.WriteLine("\n=== Kontakt suchen ===");
        Console.Write("Suchbegriff: ");
        string searchTerm = Console.ReadLine().ToLower();

        var results = contacts.Where(c => 
            c.Name.ToLower().Contains(searchTerm) || 
            c.PhoneNumber.Contains(searchTerm));

        if (!results.Any())
        {
            Console.WriteLine("Keine Kontakte gefunden.");
            return;
        }

        Console.WriteLine("Gefunden:");
        foreach (var contact in results)
        {
            Console.WriteLine($"- {contact.Name} ({contact.PhoneNumber})");
        }
    }
}
```