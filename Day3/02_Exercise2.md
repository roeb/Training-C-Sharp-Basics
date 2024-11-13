# Übung 2 - String-Helfer

## Aufgabenstellung

Implementieren Sie eine Sammlung von Extension Methods für den Typ string, die häufig benötigte String-Manipulationen durchführen.

## Anforderungen

1. ToTitleCase
   - Wandelt erste Buchstaben jedes Wortes in Großbuchstaben um
   - Andere Buchstaben bleiben unverändert
   - Berücksichtigt Leerzeichen als Wortgrenzen

2. CountWords
   - Zählt die Anzahl der Wörter im String
   - Wörter sind durch Leerzeichen getrennt
   - Mehrere aufeinanderfolgende Leerzeichen als ein Trenner

3. IsValidEmail
   - Prüft, ob der String eine gültige E-Mail-Adresse ist
   - Muss @ und einen Punkt nach dem @ enthalten
   - Keine Leerzeichen erlaubt

4. Truncate
   - Kürzt den String auf eine maximale Länge
   - Fügt "..." am Ende hinzu, wenn gekürzt wurde
   - Berücksichtigt die Länge der Auslassungspunkte

5. RemoveSpecialCharacters
   - Entfernt alle Sonderzeichen aus dem String
   - Behält Buchstaben, Zahlen und Leerzeichen
   - Optional: Zusätzliche erlaubte Zeichen können angegeben werden

## Validierungsregeln

1. ToTitleCase
   - Null oder leere Strings werden unverändert zurückgegeben
   - Zahlen und Sonderzeichen bleiben unverändert
   - Mehrere Leerzeichen bleiben erhalten

2. CountWords
   - Leere Strings oder null ergeben 0
   - Strings nur aus Leerzeichen ergeben 0
   - Satzzeichen werden nicht als Wortgrenzen gezählt

3. IsValidEmail
   - Mindestens ein Zeichen vor dem @
   - Mindestens ein Zeichen zwischen @ und Punkt
   - Mindestens ein Zeichen nach dem Punkt

4. Truncate
   - Maximale Länge muss positiv sein
   - Bei zu kurzer maximaler Länge keine Auslassungspunkte
   - Originallänge berücksichtigen

5. RemoveSpecialCharacters
   - Null-Strings werden als leerer String zurückgegeben
   - Leerzeichen bleiben erhalten
   - Erlaubte Zeichen dürfen nicht null sein

## Lösungshinweise

### Methodensignaturen

```csharp
public static class StringExtensions
{
    // Erste Buchstaben groß schreiben
    public static string ToTitleCase(this string input)

    // Wörter zählen
    public static int CountWords(this string input)

    // E-Mail validieren
    public static bool IsValidEmail(this string input)

    // Text kürzen
    public static string Truncate(
        this string input, 
        int maxLength, 
        string suffix = "...")

    // Sonderzeichen entfernen
    public static string RemoveSpecialCharacters(
        this string input, 
        string allowedChars = "")
}
```

### Beispielaufruf

```csharp
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
```

### Implementierungshinweise

- Um den ersten Buchstaben eines Wortes in Gro0buchstaben darzustellen, solltest du die mal die Klasse `CultureInfo.CurrentCulture.TextInfo.ToTitleCas` anschauen. Dort findest du eine passende Methode.

- Damit du einen String teilen kannst, schau dir mal die `Split` Funktion näher an.

- Du kannst herrausfinden ob es ich um eine gülte Emailadresse handelt wenn du `System.Net.Mail.MailAddress` nutzt und dort deine Emailadresse hineingibst.

- Um Sonderzeichen zu entfernen kannst du einen Regex wie diesen nutzen:
   ```csharp
   var regexPattern = @"[^a-zA-Z0-9\s" + Regex.Escape(allowedChars) + "]";
   ```

## Ressourcen für Übung 2 - String-Helfer


### Grundlegendes Konzept

- [Extension Methods (C# Programming Guide)](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/extension-methods)
- [How to implement extension methods (C# Programming Guide)](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/how-to-implement-and-call-a-custom-extension-method)

### String Manipulation

- [String Methods](https://learn.microsoft.com/de-de/dotnet/api/system.string?view=net-7.0#methods)
- [String.Split Method](https://learn.microsoft.com/de-de/dotnet/api/system.string.split?view=net-7.0)
- [String.Substring Method](https://learn.microsoft.com/de-de/dotnet/api/system.string.substring?view=net-7.0)

### Text Transformation

- [TextInfo.ToTitleCase Method](https://learn.microsoft.com/de-de/dotnet/api/system.globalization.textinfo.totitlecase?view=net-7.0)
- [CultureInfo Class](https://learn.microsoft.com/de-de/dotnet/api/system.globalization.cultureinfo?view=net-7.0)

### Email Validierung

- [MailAddress Class](https://learn.microsoft.com/de-de/dotnet/api/system.net.mail.mailaddress?view=net-7.0)
- [MailAddress Constructor](https://learn.microsoft.com/de-de/dotnet/api/system.net.mail.mailaddress.-ctor?view=net-7.0)

### Regular Expressions

- [Regular Expression Language - Quick Reference](https://learn.microsoft.com/de-de/dotnet/standard/base-types/regular-expression-language-quick-reference)
- [Regex Class](https://learn.microsoft.com/de-de/dotnet/api/system.text.regularexpressions.regex?view=net-7.0)
- [Regex.Escape Method](https://learn.microsoft.com/de-de/dotnet/api/system.text.regularexpressions.regex.escape?view=net-7.0)

### Zusätzliche Hilfsmethoden

- [String.IsNullOrEmpty Method](https://learn.microsoft.com/de-de/dotnet/api/system.string.isnullorempty?view=net-7.0)
- [String.IsNullOrWhiteSpace Method](https://learn.microsoft.com/de-de/dotnet/api/system.string.isnullorwhitespace?view=net-7.0)
