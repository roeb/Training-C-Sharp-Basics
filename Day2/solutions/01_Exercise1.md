# Übung 1 - Zahlenanalyse

## Lösung

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main(string[] args)
    {
        // Array für die Zahlen erstellen
        int[] numbers = new int[10];

        // Zahlen einlesen
        Console.WriteLine("Bitte geben Sie 10 Zahlen ein:");
        
        for (int i = 0; i < numbers.Length; i++)
        {
            bool validInput = false;
            while (!validInput)
            {
                Console.Write($"{i + 1}. Zahl: ");
                string input = Console.ReadLine();

                if (int.TryParse(input, out int number))
                {
                    numbers[i] = number;
                    validInput = true;
                }
                else
                {
                    Console.WriteLine("Ungültige Eingabe! Bitte geben Sie eine ganze Zahl ein.");
                }
            }
        }

        // Ursprüngliche Reihenfolge ausgeben
        Console.WriteLine("\nUrsprüngliche Reihenfolge:");
        Console.WriteLine(string.Join(", ", numbers));

        // Sortierte Reihenfolge ausgeben
        int[] sortedNumbers = (int[])numbers.Clone();
        Array.Sort(sortedNumbers);
        Console.WriteLine("\nSortierte Reihenfolge:");
        Console.WriteLine(string.Join(", ", sortedNumbers));

        // Statistik berechnen und anzeigen
        int min = numbers[0];
        int max = numbers[0];
        double sum = 0;

        for (int i = 0; i < numbers.Length; i++)
        {
            if (numbers[i] < min)
                min = numbers[i];
            if (numbers[i] > max)
                max = numbers[i];
            sum += numbers[i];
        }

        double average = sum / numbers.Length;

        Console.WriteLine("\nStatistik:");
        Console.WriteLine($"Minimum: {min}");
        Console.WriteLine($"Maximum: {max}");
        Console.WriteLine($"Durchschnitt: {average:F2}");

        // Gerade Zahlen finden und ausgeben
        List<int> evenNumbers = new List<int>();
        
        for (int i = 0; i < numbers.Length; i++)
        {
            if (numbers[i] % 2 == 0)
            {
                evenNumbers.Add(numbers[i]);
            }
        }

        Console.WriteLine("\nGerade Zahlen:");
        if (evenNumbers.Count > 0)
        {
            Console.WriteLine(string.Join(", ", evenNumbers));
        }
        else
        {
            Console.WriteLine("Keine geraden Zahlen gefunden.");
        }

        Console.ReadKey();
    }
}

```