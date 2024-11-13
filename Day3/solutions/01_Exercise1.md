# Übung 1 - Taschenrechner-Bibliothek

## Lösung

```csharp
using System;

public class Calculator
{
    public int Add(int a, int b)
    {
        if (a < 0 || b < 0)
            throw new ArgumentException("Negative Zahlen sind nicht erlaubt.");
        return a + b;
    }

    public int Add(int a, int b, int c)
    {
        if (a < 0 || b < 0 || c < 0)
            throw new ArgumentException("Negative Zahlen sind nicht erlaubt.");
        return a + b + c;
    }

    public double Subtract(double a, double b, bool round = false)
    {
        double result = a - b;
        return round ? Math.Round(result) : result;
    }

    public int Multiply(params int[] numbers)
    {
        if (numbers == null || numbers.Length == 0)
            throw new ArgumentException("Mindestens eine Zahl muss übergeben werden.");

        int result = 1;
        foreach (int number in numbers)
        {
            result *= number;
        }
        return result;
    }

    public bool Divide(int dividend, int divisor, out int quotient, out int remainder)
    {
        quotient = 0;
        remainder = 0;

        if (divisor == 0)
            return false;

        quotient = dividend / divisor;
        remainder = dividend % divisor;
        return true;
    }

    public bool TryParse(string input, out double result)
    {
        result = 0;

        if (string.IsNullOrWhiteSpace(input))
            return false;

        // Ersetze Komma durch Punkt für einheitliche Verarbeitung
        input = input.Replace(',', '.');
        return double.TryParse(input, 
            System.Globalization.NumberStyles.Any,
            System.Globalization.CultureInfo.InvariantCulture, 
            out result);
    }
}

class Program
{
    static void Main()
    {
        Calculator calc = new Calculator();

        // Addition testen
        try
        {
            Console.WriteLine($"5 + 3 = {calc.Add(5, 3)}");
            Console.WriteLine($"5 + 3 + 2 = {calc.Add(5, 3, 2)}");
        }
        catch (ArgumentException e)
        {
            Console.WriteLine($"Fehler bei Addition: {e.Message}");
        }

        // Subtraktion testen
        Console.WriteLine($"10.7 - 3.2 = {calc.Subtract(10.7, 3.2)}");
        Console.WriteLine($"10.7 - 3.2 (gerundet) = {calc.Subtract(10.7, 3.2, true)}");

        // Multiplikation testen
        try
        {
            Console.WriteLine($"2 * 3 * 4 = {calc.Multiply(2, 3, 4)}");
        }
        catch (ArgumentException e)
        {
            Console.WriteLine($"Fehler bei Multiplikation: {e.Message}");
        }

        // Division testen
        int quotient, remainder;
        if (calc.Divide(17, 5, out quotient, out remainder))
        {
            Console.WriteLine($"17 ÷ 5 = {quotient} Rest {remainder}");
        }
        else
        {
            Console.WriteLine("Division durch 0 nicht möglich");
        }

        // Parsing testen
        double number;
        if (calc.TryParse("123,45", out number))
        {
            Console.WriteLine($"Parsed: {number}");
        }
        else
        {
            Console.WriteLine("Parsing fehlgeschlagen");
        }
    }
}
