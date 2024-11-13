# Übung 3 - Zahlen-Analyse-Bibliothek

## Lösung

```csharp
using System;
using System.Linq;

public class NumberAnalyzer
{
    public static bool CalculateStatistics(
        int[] numbers,
        out int min,
        out int max,
        out double avg)
    {
        min = max = 0;
        avg = 0.0;

        if (numbers == null || numbers.Length == 0)
            return false;

        min = numbers[0];
        max = numbers[0];
        long sum = numbers[0];

        for (int i = 1; i < numbers.Length; i++)
        {
            if (numbers[i] < min) min = numbers[i];
            if (numbers[i] > max) max = numbers[i];
            sum += numbers[i];
        }

        avg = (double)sum / numbers.Length;
        return true;
    }

    public static bool CalculateStatistics(
        double[] numbers,
        out double min,
        out double max,
        out double avg)
    {
        min = max = avg = 0.0;

        if (numbers == null || numbers.Length == 0)
            return false;

        min = numbers[0];
        max = numbers[0];
        double sum = numbers[0];

        for (int i = 1; i < numbers.Length; i++)
        {
            if (numbers[i] < min) min = numbers[i];
            if (numbers[i] > max) max = numbers[i];
            sum += numbers[i];
        }

        avg = sum / numbers.Length;
        return true;
    }

    public static int[] FindNumbers(
        int[] numbers,
        Func<int, bool> filter = null,
        bool sortResults = false)
    {
        if (numbers == null)
            return new int[0];

        var result = filter == null 
            ? numbers.ToList() 
            : numbers.Where(filter).ToList();

        if (sortResults)
            result.Sort();

        return result.ToArray();
    }

    public static void ProcessArray(
        ref int[] numbers,
        bool removeDuplicates = false,
        bool sort = true)
    {
        if (numbers == null)
            numbers = new int[0];

        if (removeDuplicates)
            numbers = numbers.Distinct().ToArray();

        if (sort)
            Array.Sort(numbers);
    }
}

class Program
{
    static void Main()
    {
        // Test CalculateStatistics
        int[] numbers = { 5, 2, 8, 2, 1, 9 };
        int min, max;
        double avg;
        
        if (NumberAnalyzer.CalculateStatistics(numbers, out min, out max, out avg))
        {
            Console.WriteLine($"Statistik:");
            Console.WriteLine($"Min: {min}, Max: {max}, Durchschnitt: {avg:F2}");
        }

        // Test FindNumbers
        var evenNumbers = NumberAnalyzer.FindNumbers(
            numbers,
            n => n % 2 == 0,
            true
        );
        Console.WriteLine("\nGerade Zahlen (sortiert):");
        Console.WriteLine(string.Join(", ", evenNumbers));

        // Test ProcessArray
        int[] testArray = { 5, 2, 8, 2, 1, 9 };
        Console.WriteLine("\nOriginal Array:");
        Console.WriteLine(string.Join(", ", testArray));
        
        NumberAnalyzer.ProcessArray(
            ref testArray,
            removeDuplicates: true,
            sort: true
        );
        
        Console.WriteLine("Nach Verarbeitung (keine Duplikate, sortiert):");
        Console.WriteLine(string.Join(", ", testArray));
    }
}
