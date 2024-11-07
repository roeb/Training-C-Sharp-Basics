# Übung 2 - Textanalyse

## Lösung

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

class Program
{
    static void Main()
    {
        // Dictionary für Worthäufigkeiten
        Dictionary<string, int> wordCount = new Dictionary<string, int>();

        // Text einlesen
        Console.WriteLine("Bitte geben Sie einen Text ein:");
        string text = Console.ReadLine();

        // Text in Wörter zerlegen und bereinigen
        string[] words = text.ToLower()
                        .Split(' ')
                        .Select(w => w.Trim('.', ',', '!', '?'))
                        .Where(w => !string.IsNullOrEmpty(w))
                        .ToArray();

        // Häufigkeiten zählen
        foreach (string word in words)
        {
            if (wordCount.ContainsKey(word))
            {
                wordCount[word]++;
            }
            else
            {
                wordCount[word] = 1;
            }
        }

        // Ausgabe der Wortanalyse
        Console.WriteLine("\nWortanalyse:");
        foreach (var pair in wordCount)
        {
            Console.WriteLine($"\"{pair.Key}\" kommt {pair.Value}x vor");
        }

        // Top 3 ermitteln und ausgeben
        var top3 = wordCount.OrderByDescending(x => x.Value).Take(3);
        
        Console.WriteLine("\nTop 3 häufigste Wörter:");
        int rank = 1;
        foreach (var pair in top3)
        {
            Console.WriteLine($"{rank}. {pair.Key} ({pair.Value}x)");
            rank++;
        }

        // Lange Wörter finden und ausgeben
        var longWords = words.Where(w => w.Length > 5)
                            .Distinct()
                            .OrderBy(w => w);

        Console.WriteLine("\nWörter mit mehr als 5 Buchstaben:");
        foreach (var word in longWords)
        {
            Console.WriteLine($"- {word}");
        }
    }
}
```