# Übung 2 - String-Helfer

## Lösung

```csharp
using System;
using System.Text;
using System.Text.RegularExpressions;
using System.Linq;
using System.Globalization;

public static class StringExtensions
{
    /// <summary>
    /// Wandelt die ersten Buchstaben jedes Wortes in Großbuchstaben um.
    /// </summary>
    public static string ToTitleCase(this string input)
    {
        if (string.IsNullOrEmpty(input)) return input;

        return CultureInfo.CurrentCulture.TextInfo.ToTitleCase(input.ToLower());
    }

    /// <summary>
    /// Zählt die Anzahl der Wörter im String.
    /// </summary>
    public static int CountWords(this string input)
    {
        if (string.IsNullOrWhiteSpace(input)) return 0;

        return input.Split(new[] {' '}, StringSplitOptions.RemoveEmptyEntries).Length;
    }

    /// <summary>
    /// Prüft, ob der String eine gültige E-Mail-Adresse ist.
    /// </summary>
    public static bool IsValidEmail(this string input)
    {
        if (string.IsNullOrEmpty(input)) return false;

        try
        {
            var addr = new System.Net.Mail.MailAddress(input);
            return addr.Address == input;
        }
        catch
        {
            return false;
        }
    }

    /// <summary>
    /// Kürzt den String auf eine maximale Länge und fügt "..." am Ende hinzu, wenn gekürzt wurde.
    /// </summary>
    public static string Truncate(this string input, int maxLength, string suffix = "...")
    {
        if (string.IsNullOrEmpty(input) || maxLength <= 0) return input;

        if (input.Length <= maxLength) return input;

        int truncateLength = maxLength - suffix.Length;
        if (truncateLength <= 0) return input.Substring(0, maxLength);

        return input.Substring(0, truncateLength) + suffix;
    }

    /// <summary>
    /// Entfernt alle Sonderzeichen aus dem String, behält Buchstaben, Zahlen und Leerzeichen.
    /// </summary>
    public static string RemoveSpecialCharacters(this string input, string allowedChars = "")
    {
        if (input == null) return string.Empty;

        var regexPattern = @"[^a-zA-Z0-9\s" + Regex.Escape(allowedChars) + "]";
        return Regex.Replace(input, regexPattern, "");
    }
}

// Beispielaufruf
class Program
{
    static void Main()
    {
        string text = "hello world";
        Console.WriteLine(text.ToTitleCase());  // "Hello World"

        string sentence = "this is   a   test";
        Console.WriteLine(sentence.CountWords());  // 4

        string email = "test@example.com";
        Console.WriteLine(email.IsValidEmail());  // true

        string longText = "This is a very long text";
        Console.WriteLine(longText.Truncate(10));  // "This is..."

        string special = "Hello, World! 123";
        Console.WriteLine(special.RemoveSpecialCharacters());  // "Hello World 123"
    }
}
```