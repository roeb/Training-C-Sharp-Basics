# C# Grundlagenschulung - Abschlussprojekt

## Lösung: "Konsolen-Anwendung für eine Mediathek"

```csharp
using System;
using System.Collections.Generic;

namespace MediathekProjekt
{
    // Abstrakte Basisklasse
    abstract class Medium
    {
        public string Titel { get; set; }
        public int Erscheinungsjahr { get; set; }

        protected Medium(string titel, int erscheinungsjahr)
        {
            Titel = titel;
            Erscheinungsjahr = erscheinungsjahr;
        }

        public override string ToString()
        {
            return $"Titel: {Titel}, Erscheinungsjahr: {Erscheinungsjahr}";
        }
    }

    // Buch-Klasse
    class Buch : Medium
    {
        public string Autor { get; set; }
        public string ISBN { get; set; }

        public Buch(string titel, int erscheinungsjahr, string autor, string isbn)
            : base(titel, erscheinungsjahr)
        {
            Autor = autor;
            ISBN = isbn;
        }

        public override string ToString()
        {
            return $"Buch - {base.ToString()}, Autor: {Autor}, ISBN: {ISBN}";
        }
    }

    // Zeitung-Klasse
    class Zeitung : Medium
    {
        public string Herausgeber { get; set; }
        public int AusgabeNr { get; set; }

        public Zeitung(string titel, int erscheinungsjahr, string herausgeber, int ausgabeNr)
            : base(titel, erscheinungsjahr)
        {
            Herausgeber = herausgeber;
            AusgabeNr = ausgabeNr;
        }

        public override string ToString()
        {
            return $"Zeitung - {base.ToString()}, Herausgeber: {Herausgeber}, AusgabeNr: {AusgabeNr}";
        }
    }

    // CD-Klasse
    class CD : Medium
    {
        public string Künstler { get; set; }
        public int Titelanzahl { get; set; }

        public CD(string titel, int erscheinungsjahr, string künstler, int titelanzahl)
            : base(titel, erscheinungsjahr)
        {
            Künstler = künstler;
            Titelanzahl = titelanzahl;
        }

        public override string ToString()
        {
            return $"CD - {base.ToString()}, Künstler: {Künstler}, Titelanzahl: {Titelanzahl}";
        }
    }

    // DVD-Klasse
    class DVD : Medium
    {
        public string Regisseur { get; set; }
        public double Spieldauer { get; set; }

        public DVD(string titel, int erscheinungsjahr, string regisseur, double spieldauer)
            : base(titel, erscheinungsjahr)
        {
            Regisseur = regisseur;
            Spieldauer = spieldauer;
        }

        public override string ToString()
        {
            return $"DVD - {base.ToString()}, Regisseur: {Regisseur}, Spieldauer: {Spieldauer} Stunden";
        }
    }

    class Program
    {
        static List<Medium> mediathek = new List<Medium>();

        static void Main(string[] args)
        {
            bool running = true;

            while (running)
            {
                Console.WriteLine("\nMediathek Menü:");
                Console.WriteLine("1. Medium hinzufügen");
                Console.WriteLine("2. Alle Medien anzeigen");
                Console.WriteLine("3. Medium nach Titel suchen");
                Console.WriteLine("4. Beenden");
                Console.Write("Auswahl: ");

                switch (Console.ReadLine())
                {
                    case "1":
                        MediumHinzufuegen();
                        break;
                    case "2":
                        AlleMedienAnzeigen();
                        break;
                    case "3":
                        MediumSuchen();
                        break;
                    case "4":
                        running = false;
                        break;
                    default:
                        Console.WriteLine("Ungültige Auswahl. Bitte versuchen Sie es erneut.");
                        break;
                }
            }
        }

        static void MediumHinzufuegen()
        {
            Console.WriteLine("\nWelches Medium möchten Sie hinzufügen?");
            Console.WriteLine("1. Buch");
            Console.WriteLine("2. Zeitung");
            Console.WriteLine("3. CD");
            Console.WriteLine("4. DVD");
            Console.Write("Auswahl: ");

            string auswahl = Console.ReadLine();
            Console.Write("Titel: ");
            string titel = Console.ReadLine();

            Console.Write("Erscheinungsjahr: ");
            if (!int.TryParse(Console.ReadLine(), out int erscheinungsjahr))
            {
                Console.WriteLine("Ungültiges Erscheinungsjahr. Vorgang abgebrochen.");
                return;
            }

            switch (auswahl)
            {
                case "1":
                    Console.Write("Autor: ");
                    string autor = Console.ReadLine();
                    Console.Write("ISBN: ");
                    string isbn = Console.ReadLine();
                    mediathek.Add(new Buch(titel, erscheinungsjahr, autor, isbn));
                    break;
                case "2":
                    Console.Write("Herausgeber: ");
                    string herausgeber = Console.ReadLine();
                    Console.Write("AusgabeNr: ");
                    if (!int.TryParse(Console.ReadLine(), out int ausgabeNr))
                    {
                        Console.WriteLine("Ungültige AusgabeNr. Vorgang abgebrochen.");
                        return;
                    }
                    mediathek.Add(new Zeitung(titel, erscheinungsjahr, herausgeber, ausgabeNr));
                    break;
                case "3":
                    Console.Write("Künstler: ");
                    string künstler = Console.ReadLine();
                    Console.Write("Titelanzahl: ");
                    if (!int.TryParse(Console.ReadLine(), out int titelanzahl))
                    {
                        Console.WriteLine("Ungültige Titelanzahl. Vorgang abgebrochen.");
                        return;
                    }
                    mediathek.Add(new CD(titel, erscheinungsjahr, künstler, titelanzahl));
                    break;
                case "4":
                    Console.Write("Regisseur: ");
                    string regisseur = Console.ReadLine();
                    Console.Write("Spieldauer (in Stunden): ");
                    if (!double.TryParse(Console.ReadLine(), out double spieldauer))
                    {
                        Console.WriteLine("Ungültige Spieldauer. Vorgang abgebrochen.");
                        return;
                    }
                    mediathek.Add(new DVD(titel, erscheinungsjahr, regisseur, spieldauer));
                    break;
                default:
                    Console.WriteLine("Ungültige Auswahl. Vorgang abgebrochen.");
                    break;
            }
        }

        static void AlleMedienAnzeigen()
        {
            Console.WriteLine("\nAlle Medien in der Mediathek:");
            foreach (var medium in mediathek)
            {
                Console.WriteLine(medium.ToString());
            }
        }

        static void MediumSuchen()
        {
            Console.Write("\nGeben Sie den Titel ein, nach dem Sie suchen möchten: ");
            string suchbegriff = Console.ReadLine().ToLower();

            foreach (var medium in mediathek)
            {
                if (medium.Titel.ToLower().Contains(suchbegriff))
                {
                    Console.WriteLine(medium.ToString());
                }
            }
        }
    }
}
```
