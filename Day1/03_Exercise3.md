# Übung 3 - String-Manipulation und Formatierung

## Aufgabenstellung:

Erstellen Sie eine Konsolenanwendung, die verschiedene String-Manipulationen und Formatierungen demonstriert.

### Teil 1 - Personendaten

1. Deklarieren Sie Variablen für:
   - Vor- und Nachname (string)
   - Alter (int)
   - Körpergröße in Meter (double)
   - Gehalt (decimal)

2. Lesen Sie diese Werte von der Konsole ein
   - Verwenden Sie Convert oder Parse für die Typkonvertierung
   - Fangen Sie mögliche Fehleingaben ab (optional)

3. Geben Sie die Daten in folgenden Formaten aus:
   - "Mein Name ist {Vorname} {Nachname}."
   - "Ich bin {Alter} Jahre alt und {Größe}m groß." (Größe mit 2 Dezimalstellen)
   - "Mein Gehalt beträgt {Gehalt:C2}" (als Währungsbetrag)

### Teil 2 - String-Manipulation

1. Erstellen Sie aus Vor- und Nachname:
   - Initialen (z.B. "Max Mustermann" → "M.M.")
   - Den Namen in Großbuchstaben
   - Den Namen in Kleinbuchstaben
   - Die Anzahl der Buchstaben im Gesamtnamen (ohne Leerzeichen)

### Teil 3 - Formatierte Tabelle

Erstellen Sie eine Ausgabe in folgendem Format:

```text
+----------------+------------------+
| Name           | Max Mustermann   |
| Alter          | 30 Jahre         |
| Größe          | 1,80 m           |
| Gehalt         | 50.000,00 €      |
| Initialen      | M.M.             |
+----------------+------------------+
```

## Lösungshinweise für Übung 3

### Teil 1 - Personendaten

- Für die Konsoleneingabe: Console.ReadLine() verwenden
- Für Konvertierungen bieten sich an:
  - double.Parse() oder Convert.ToDouble() für die Größe
  - Beachten Sie die Kultureinstellungen wegen Dezimaltrennzeichen
- Bei der String-Interpolation auf das $-Zeichen vor dem String achten
- Für Dezimalstellen bei Zahlen kann man :F2 als Formatierungsanweisung nutzen
- Für Währungsbeträge eignet sich :C als Formatierungsanweisung

### Teil 2 - String-Manipulation

- Denken Sie daran, dass Strings ein Array von Zeichen sind
- Nützliche String-Methoden:
  - Substring()
  - ToUpper() / ToLower()
  - Replace()
  - Split()
- Für die Initialen:
  - Überlegen Sie, wie Sie den ersten Buchstaben jedes Namens extrahieren können
  - String-Verkettung mit + oder StringBuilder beachten

### Teil 3 - Formatierte Tabelle

- Für gleichmäßige Spaltenbreiten:
  - Die ToString()-Methode kann mit PadRight() oder PadLeft() kombiniert werden
  - Alternativ kann die {0,-20} Syntax in string.Format verwendet werden
- Konstanten für die Tabellenbreite definieren macht den Code übersichtlicher

## Nützliche MSDN Dokumentation für Übung 3

### String-Grundlagen und Formatierung
- [String Klasse (System.String)](https://learn.microsoft.com/de-de/dotnet/api/system.string)
- [String Formatierung](https://learn.microsoft.com/de-de/dotnet/standard/base-types/formatting-types)
- [String Interpolation](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/tokens/interpolated)
- [Composite Formatting](https://learn.microsoft.com/de-de/dotnet/standard/base-types/composite-formatting)

### String-Methoden
- [ToUpper() Methode](https://learn.microsoft.com/de-de/dotnet/api/system.string.toupper)
- [ToLower() Methode](https://learn.microsoft.com/de-de/dotnet/api/system.string.tolower)
- [Substring() Methode](https://learn.microsoft.com/de-de/dotnet/api/system.string.substring)
- [Replace() Methode](https://learn.microsoft.com/de-de/dotnet/api/system.string.replace)
- [Split() Methode](https://learn.microsoft.com/de-de/dotnet/api/system.string.split)
- [PadLeft() Methode](https://learn.microsoft.com/de-de/dotnet/api/system.string.padleft)
- [PadRight() Methode](https://learn.microsoft.com/de-de/dotnet/api/system.string.padright)

### Konsoleneingabe und -ausgabe
- [Console.ReadLine() Methode](https://learn.microsoft.com/de-de/dotnet/api/system.console.readline)
- [Console.WriteLine() Methode](https://learn.microsoft.com/de-de/dotnet/api/system.console.writeline)

### Typkonvertierung
- [Convert Klasse](https://learn.microsoft.com/de-de/dotnet/api/system.convert)
- [Parse() Methode](https://learn.microsoft.com/de-de/dotnet/api/system.int32.parse)
- [TryParse() Methode](https://learn.microsoft.com/de-de/dotnet/api/system.int32.tryparse)

### Zahlenformatierung
- [Numerische Formatstrings](https://learn.microsoft.com/de-de/dotnet/standard/base-types/standard-numeric-format-strings)
- [Währungsformatierung](https://learn.microsoft.com/de-de/dotnet/standard/base-types/standard-numeric-format-strings#currency-format-specifier-c)

### Ausnahmebehandlung
- [Try-Catch Blöcke](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/statements/try-catch-finally)
- [FormatException Klasse](https://learn.microsoft.com/de-de/dotnet/api/system.formatexception)