# Übung 2 - "Temperaturrechner und Zahlenanalyse"

## Lösungen

### Teil 1

```csharp
using System;

namespace Temperaturrechner
{
    class Program
    {
        static void Main(string[] args)
        {
            // Deklaration und Initialisierung der Grundvariablen
            double temperaturCelsius = 23.5;
            int anzahlMessungen = 42;
            string messstation = "Berlin-Mitte";
            bool istAktiv = true;

            // Deklaration der Umrechnungsvariablen
            double temperaturFahrenheit;
            double temperaturKelvin;

            // Berechnungen
            temperaturFahrenheit = (temperaturCelsius * 9 / 5) + 32;
            temperaturKelvin = temperaturCelsius + 273.15;

            // Optionale Testausgabe der Werte
            Console.WriteLine($"Temperatur in Celsius: {temperaturCelsius}");
            Console.WriteLine($"Temperatur in Fahrenheit: {temperaturFahrenheit}");
            Console.WriteLine($"Temperatur in Kelvin: {temperaturKelvin}");
        }
    }
}
```

### Teil 2

```csharp
// Deklaration der Variablen (aus Teil 1)
string stationName = "Berlin-Mitte";
bool isActive = true;
int measurementCount = 42;
double celsiusTemp = 23.456;
double fahrenheitTemp = (celsiusTemp * 9/5) + 32;
double kelvinTemp = celsiusTemp + 273.15;

// Formatierte Ausgabe mit String-Interpolation
Console.WriteLine("=== Messstation-Info ===");
Console.WriteLine($"Messstation: {stationName}");

// Variante 1: Mit ternärem Operator
Console.WriteLine($"Status: {(isActive ? "Aktiv" : "Inaktiv")}");

// Variante 2: Alternative mit if/else
/*
string statusText = isActive ? "Aktiv" : "Inaktiv";
Console.WriteLine($"Status: {statusText}");
*/

Console.WriteLine($"Anzahl Messungen: {measurementCount}");
Console.WriteLine("\nTemperaturen:");
// Formatierung mit :F2 für 2 Nachkommastellen
Console.WriteLine($"- Celsius: {celsiusTemp:F2}°C");
Console.WriteLine($"- Fahrenheit: {fahrenheitTemp:F2}°F");
Console.WriteLine($"- Kelvin: {kelvinTemp:F2}K");

// Leerzeile am Ende
Console.WriteLine();
```

### Teil 3

```csharp
using System;

namespace Uebung2
{
    class Program
    {
        static void Main(string[] args)
        {
            // Deklaration und Initialisierung der Grundwerte
            int zahl1 = 17;
            int zahl2 = 5;
            int zahl3 = 2;

            // Berechnungen
            int summe = zahl1 + zahl2 + zahl3;
            int produkt = zahl1 * zahl2 * zahl3;
            double division = (double)zahl1 / zahl2;  // Cast nach double für Dezimalergebnis
            int modulo = zahl1 % zahl3;
            int quadrat = zahl1 * zahl1;

            // Formatierte Ausgabe
            Console.WriteLine("Mathematische Operationen:");
            Console.WriteLine($"{zahl1} + {zahl2} + {zahl3} = {summe}");
            Console.WriteLine($"{zahl1} * {zahl2} * {zahl3} = {produkt}");
            Console.WriteLine($"{zahl1} / {zahl2} = {division:F2}");  // F2 für 2 Nachkommastellen
            Console.WriteLine($"{zahl1} % {zahl3} = {modulo}");
            Console.WriteLine($"{zahl1}² = {quadrat}");

            // Zusatzaufgaben
            double durchschnitt = (zahl1 + zahl2 + zahl3) / 3.0;
            
            double testZahl = 17.89;
            double gerundet = Math.Round(testZahl);
            double nachUnten = Math.Floor(testZahl);
            double nachOben = Math.Ceiling(testZahl);

            int maximum = Math.Max(Math.Max(zahl1, zahl2), zahl3);
            int minimum = Math.Min(Math.Min(zahl1, zahl2), zahl3);
            double wurzel = Math.Sqrt(zahl1);

            Console.WriteLine("\nErweiterte Analysen:");
            Console.WriteLine($"Durchschnitt: {durchschnitt:F2}");
            Console.WriteLine($"\nRundungen von {testZahl}:");
            Console.WriteLine($"- Mathematisch: {gerundet}");
            Console.WriteLine($"- Nach unten: {nachUnten}");
            Console.WriteLine($"- Nach oben: {nachOben}");
            Console.WriteLine($"\nMath-Funktionen:");
            Console.WriteLine($"- Maximum: {maximum}");
            Console.WriteLine($"- Minimum: {minimum}");
            Console.WriteLine($"- Wurzel aus {zahl1}: {wurzel:F2}");
        }
    }
}
```
