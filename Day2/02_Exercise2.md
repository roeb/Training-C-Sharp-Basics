# Übung 2 - Textanalyse

## Aufgabenstellung

Entwickeln Sie ein Konsolenprogramm zur Analyse von Texten, das die Häufigkeit von Wörtern untersucht und verschiedene Auswertungen vornimmt.

## Anforderungen

1. Text einlesen
   - Lassen Sie den Benutzer einen beliebig langen Text eingeben
   - Alternativ: Verwenden Sie einen vorgegebenen Beispieltext
   - Der Text soll in einzelne Wörter zerlegt werden

2. Wörter zählen
   - Erstellen Sie ein Dictionary<string, int>
   - Speichern Sie darin jedes Wort und seine Häufigkeit
   - Groß-/Kleinschreibung soll ignoriert werden
   - Satzzeichen sollen entfernt werden

3. Top 3 Wörter ermitteln
   - Finden Sie die drei am häufigsten verwendeten Wörter
   - Sortieren Sie diese nach Häufigkeit
   - Zeigen Sie Wort und Anzahl an

4. Lange Wörter
   - Erstellen Sie eine Liste aller Wörter mit mehr als 5 Buchstaben
   - Sortieren Sie diese alphabetisch
   - Zeigen Sie die Liste an

## Beispielausgabe

```text
Bitte geben Sie einen Text ein:
Der Hund läuft durch den Garten. Der Hund ist schnell und der Garten ist groß.

Wortanalyse:
"der" kommt 3x vor
"hund" kommt 2x vor
"garten" kommt 2x vor
...

Top 3 häufigste Wörter:
1. der (3x)
2. hund (2x)
3. garten (2x)

Wörter mit mehr als 5 Buchstaben:
- garten
- schnell
```

## Hinweise

- Nutzen Sie string.Split() zum Zerlegen des Textes
- Verwenden Sie string.ToLower() für Groß-/Kleinschreibung
- Nutzen Sie LINQ für Sortierung und Filterung
- Satzzeichen können mit string.Replace() oder Regex entfernt werden

## Beispielcode-Struktur

```csharp
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
    // Ihre Implementierung
}

// Top 3 ermitteln
var top3 = // Ihre LINQ-Abfrage

// Lange Wörter finden
var longWords = // Ihre LINQ-Abfrage
```

## Ressourcen für Übung 2 - Textanalyse

### Grundlegende String-Operationen
- [String.Split Methode](https://learn.microsoft.com/de-de/dotnet/api/system.string.split)
- [String.ToLower Methode](https://learn.microsoft.com/de-de/dotnet/api/system.string.tolower)
- [String.Trim Methode](https://learn.microsoft.com/de-de/dotnet/api/system.string.trim)
- [String.Replace Methode](https://learn.microsoft.com/de-de/dotnet/api/system.string.replace)

### Collections
- [Dictionary<TKey,TValue> Klasse](https://learn.microsoft.com/de-de/dotnet/api/system.collections.generic.dictionary-2)
- [Dictionary Verwendung und Beispiele](https://learn.microsoft.com/de-de/dotnet/api/system.collections.generic.dictionary-2#examples)

### LINQ
- [LINQ Grundlagen](https://learn.microsoft.com/de-de/dotnet/csharp/linq/)
- [OrderBy Operator](https://learn.microsoft.com/de-de/dotnet/api/system.linq.enumerable.orderby)
- [Where Operator](https://learn.microsoft.com/de-de/dotnet/api/system.linq.enumerable.where)
- [Select Operator](https://learn.microsoft.com/de-de/dotnet/api/system.linq.enumerable.select)
- [Take Methode](https://learn.microsoft.com/de-de/dotnet/api/system.linq.enumerable.take) (für Top 3)

### Arrays und Enumerable
- [Array.ToArray Methode](https://learn.microsoft.com/de-de/dotnet/api/system.linq.enumerable.toarray)
- [IEnumerable<T> Interface](https://learn.microsoft.com/de-de/dotnet/api/system.collections.generic.ienumerable-1)

### Optional: Reguläre Ausdrücke
- [Regular Expressions](https://learn.microsoft.com/de-de/dotnet/api/system.text.regularexpressions.regex)
- [Regex.Replace Methode](https://learn.microsoft.com/de-de/dotnet/api/system.text.regularexpressions.regex.replace)