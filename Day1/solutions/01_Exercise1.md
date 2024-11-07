# Übung 1 - "Mein erstes C# Programm"

## Lösung

```csharp
using System;

namespace MeineProgramme
{
    class Program
    {
        static void Main(string[] args)
        {
            // Begrüßung und Namenseingabe
            Console.WriteLine("Willkommen beim Baumarkt-Rechner!");
            Console.Write("Wie ist dein Name? ");
            string benutzerName = Console.ReadLine();

            // Eingabe der Raummaße
            Console.Write("Wie lang ist dein Raum (in Meter)? ");
            string laengeEingabe = Console.ReadLine();
            Console.Write("Wie breit ist dein Raum (in Meter)? ");
            string breiteEingabe = Console.ReadLine();

            // Konvertierung der Eingaben
            double laenge = Convert.ToDouble(laengeEingabe);
            double breite = Convert.ToDouble(breiteEingabe);

            // Berechnungen
            double flaeche = laenge * breite;
            double umfang = 2 * (laenge + breite);

            // Grundausgabe
            Console.WriteLine($"\nHallo {benutzerName}, dein Raum hat folgende Maße:");
            Console.WriteLine($"Fläche: {flaeche:F2} Quadratmeter");
            Console.WriteLine($"Umfang: {umfang:F2} Meter");

            // Zusatzaufgaben
            // Berechnung der benötigten Farbeimer
            int benoetigteFarbeimer = (int)Math.Ceiling(flaeche / 10.0);
            Console.WriteLine($"\nDu benötigst {benoetigteFarbeimer} Farbeimer");

            // Kostenberechnung
            Console.Write("\nWie viel kostet ein Farbeimer (in Euro)? ");
            double preisProEimer = Convert.ToDouble(Console.ReadLine());
            double gesamtkosten = benoetigteFarbeimer * preisProEimer;
            Console.WriteLine($"Bei einem Preis von {preisProEimer:F2} € pro Eimer betragen die Gesamtkosten: {gesamtkosten:F2} €");

            // Warten auf Tastendruck
            Console.WriteLine("\nDrücken Sie eine beliebige Taste zum Beenden...");
            Console.ReadKey();
        }
    }
}
```
