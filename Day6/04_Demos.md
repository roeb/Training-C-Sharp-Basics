# Demos für Tag 6

## 1. Grundlegendes Exception Handling

### Basis Try-Catch

```csharp
public class ExceptionBasics
{
    public void DemoBasicTryCatch()
    {
        try
        {
            Console.Write("Geben Sie eine Zahl ein: ");
            string input = Console.ReadLine();
            int number = int.Parse(input);
            Console.WriteLine($"Ihre Zahl: {number}");
        }
        catch (FormatException ex)
        {
            Console.WriteLine($"Fehler: Ungültiges Format. {ex.Message}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Allgemeiner Fehler: {ex.Message}");
        }
    }

    public void DemoMultipleExceptions()
    {
        try
        {
            string[] namen = { "Anna", "Ben", "Clara" };
            Console.Write("Index eingeben: ");
            int index = int.Parse(Console.ReadLine());
            Console.WriteLine($"Name: {namen[index]}");
        }
        catch (FormatException)
        {
            Console.WriteLine("Fehler: Bitte geben Sie eine Zahl ein.");
        }
        catch (IndexOutOfRangeException)
        {
            Console.WriteLine("Fehler: Index außerhalb des gültigen Bereichs.");
        }
        finally
        {
            Console.WriteLine("Programm beendet.");
        }
    }
}
```

### Exception-Hierarchie und When-Klausel

```csharp
public class ExceptionHierarchy
{
    public void DemoExceptionFiltering()
    {
        try
        {
            ProcessNumber(-5);
        }
        catch (ArgumentException ex) when (ex.ParamName == "number")
        {
            Console.WriteLine("Spezifischer Parameter-Fehler");
        }
        catch (ArgumentException ex)
        {
            Console.WriteLine("Allgemeiner Parameter-Fehler");
        }
    }

    private void ProcessNumber(int number)
    {
        if (number < 0)
        {
            throw new ArgumentException("Zahl muss positiv sein.", "number");
        }
    }
}
```

## 2. Eigene Exception-Klassen

```csharp
// Custom Exception
public class ProductException : Exception
{
    public string ProductCode { get; }

    public ProductException(string message) 
        : base(message)
    {
    }

    public ProductException(string message, string productCode) 
        : base(message)
    {
        ProductCode = productCode;
    }

    public ProductException(string message, Exception innerException)
        : base(message, innerException)
    {
    }
}

// Verwendung
public class ProductManager
{
    public void UpdateStock(string productCode, int quantity)
    {
        try
        {
            if (string.IsNullOrEmpty(productCode))
            {
                throw new ProductException("Produktcode darf nicht leer sein.");
            }

            if (quantity < 0)
            {
                throw new ProductException(
                    $"Ungültige Menge: {quantity}",
                    productCode);
            }

            // Weitere Logik...
        }
        catch (ProductException ex)
        {
            Console.WriteLine($"Produktfehler: {ex.Message}");
            if (ex.ProductCode != null)
            {
                Console.WriteLine($"Betroffenes Produkt: {ex.ProductCode}");
            }
        }
    }
}
```

## 3. Exception Best Practices

```csharp
public class ExceptionBestPractices
{
    // 1. Spezifische Exceptions verwenden
    public void DemoSpecificExceptions()
    {
        try
        {
            // Mehrere mögliche Exceptions
            using var reader = new StreamReader("config.txt");
            var config = reader.ReadToEnd();
            var settings = JsonSerializer.Deserialize<Dictionary<string, string>>(config);
        }
        catch (FileNotFoundException ex)
        {
            Console.WriteLine("Konfigurationsdatei nicht gefunden.");
            // Logging hier
        }
        catch (JsonException ex)
        {
            Console.WriteLine("Ungültiges JSON-Format in der Konfigurationsdatei.");
            // Logging hier
        }
    }

    // 2. Exception-Filter für bessere Kontrolle
    public void DemoExceptionFilter()
    {
        try
        {
            ProcessData("test.txt");
        }
        catch (IOException ex) when (IsRetryable(ex))
        {
            // Wiederholbare Fehler
            Console.WriteLine("Temporärer Fehler, versuche erneut...");
        }
        catch (IOException ex)
        {
            // Nicht wiederholbare Fehler
            Console.WriteLine("Permanenter Fehler, keine Wiederholung möglich.");
        }
    }

    private bool IsRetryable(IOException ex)
    {
        return ex.HResult == -2147024864; // "File in use" error
    }

    // 3. Finally für Ressourcen-Cleanup
    public void DemoResourceCleanup()
    {
        StreamWriter writer = null;
        try
        {
            writer = new StreamWriter("log.txt");
            writer.WriteLine("Log-Eintrag");
        }
        catch (IOException ex)
        {
            Console.WriteLine($"Fehler beim Schreiben: {ex.Message}");
        }
        finally
        {
            writer?.Dispose();
        }
    }

    // 4. Using-Statement als Alternative
    public void DemoUsing()
    {
        try
        {
            using var writer = new StreamWriter("log.txt");
            writer.WriteLine("Log-Eintrag");
        }
        catch (IOException ex)
        {
            Console.WriteLine($"Fehler beim Schreiben: {ex.Message}");
        }
    }
}
```

## 4. Debugging-Techniken

```csharp
public class DebuggingDemo
{
    public void DemoDebugging()
    {
        // 1. Debug.WriteLine für Debugging-Ausgaben
        Debug.WriteLine("Debugging-Information");

        // 2. Conditional Compilation
#if DEBUG
        Console.WriteLine("Nur im Debug-Modus sichtbar");
#endif

        // 3. Debug.Assert für Annahmen
        int alter = -5;
        Debug.Assert(alter >= 0, "Alter kann nicht negativ sein!");

        // 4. Trace für detailliertes Logging
        Trace.TraceInformation("Information");
        Trace.TraceWarning("Warnung");
        Trace.TraceError("Fehler");
    }

    // 5. Methode mit verschiedenen Debug-Punkten
    public void KomplexeBerechnung(int wert)
    {
        Debug.WriteLine($"Starte Berechnung mit Wert: {wert}");

        try
        {
            // Breakpoint hier setzen
            var zwischenergebnis = wert * 2;
            Debug.WriteLine($"Zwischenergebnis: {zwischenergebnis}");

            // Weitere Berechnungen...
            var endergebnis = zwischenergebnis + 10;
            Debug.WriteLine($"Endergebnis: {endergebnis}");
        }
        catch (Exception ex)
        {
            Debug.WriteLine($"Fehler in Berechnung: {ex.Message}");
            throw;
        }
    }
}
```

## Using zur Ausführung von Dispose bei einem Streamreader

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Der Pfad zur Datei, die gelesen werden soll
        string filePath = "example.txt";

        // Verwende die using-Anweisung, um sicherzustellen, dass StreamReader ordnungsgemäß entsorgt wird
        using (StreamReader reader = new StreamReader(filePath))
        {
            string line;

            // Lies die Datei zeilenweise, bis das Ende der Datei erreicht ist
            while ((line = reader.ReadLine()) != null)
            {
                Console.WriteLine(line);
            }
        } // Hier wird der StreamReader automatisch geschlossen und die Ressourcen werden freigegeben

        Console.WriteLine("Datei wurde erfolgreich gelesen.");
    }
}
```

## 5. Kombinierte Demo: Datei-Verarbeitungssystem

```csharp
// Custom Exceptions
public class FileProcessingException : Exception
{
    public string FilePath { get; }

    public FileProcessingException(string message, string filePath) 
        : base(message)
    {
        FilePath = filePath;
    }

    public FileProcessingException(string message, string filePath, Exception inner)
        : base(message, inner)
    {
        FilePath = filePath;
    }
}

public class FileProcessor
{
    private readonly string logPath;
    
    public FileProcessor(string logPath)
    {
        this.logPath = logPath;
    }

    public void ProcessFile(string inputPath, string outputPath)
    {
        Debug.WriteLine($"Starte Verarbeitung von: {inputPath}");

        try
        {
            // Validierung
            if (!File.Exists(inputPath))
            {
                throw new FileProcessingException(
                    "Eingabedatei nicht gefunden", 
                    inputPath);
            }

            // Verarbeitung
            string[] lines = File.ReadAllLines(inputPath);
            Debug.WriteLine($"Gelesen: {lines.Length} Zeilen");

            // Transformation
            var processedLines = lines
                .Where(l => !string.IsNullOrWhiteSpace(l))
                .Select(ProcessLine)
                .ToList();

            // Speichern
            File.WriteAllLines(outputPath, processedLines);
            LogSuccess($"Datei erfolgreich verarbeitet: {inputPath}");
        }
        catch (FileProcessingException)
        {
            // Bereits behandelte Ausnahmen weiterleiten
            throw;
        }
        catch (Exception ex)
        {
            var message = $"Fehler bei der Verarbeitung von {inputPath}";
            LogError(message, ex);
            throw new FileProcessingException(message, inputPath, ex);
        }
    }

    private string ProcessLine(string line)
    {
        try
        {
            // Beispiel-Verarbeitung
            return line.Trim().ToUpper();
        }
        catch (Exception ex)
        {
            throw new FileProcessingException(
                $"Fehler bei der Zeilenverarbeitung: {line}", 
                "N/A", 
                ex);
        }
    }

    private void LogSuccess(string message)
    {
        try
        {
            using var writer = File.AppendText(logPath);
            writer.WriteLine($"{DateTime.Now:yyyy-MM-dd HH:mm:ss} - SUCCESS: {message}");
        }
        catch (Exception ex)
        {
            Debug.WriteLine($"Fehler beim Logging: {ex.Message}");
        }
    }

    private void LogError(string message, Exception ex)
    {
        try
        {
            using var writer = File.AppendText(logPath);
            writer.WriteLine($"{DateTime.Now:yyyy-MM-dd HH:mm:ss} - ERROR: {message}");
            writer.WriteLine($"Exception: {ex.GetType().Name}");
            writer.WriteLine($"Message: {ex.Message}");
            writer.WriteLine($"StackTrace: {ex.StackTrace}");
            writer.WriteLine(new string('-', 50));
        }
        catch (Exception logEx)
        {
            Debug.WriteLine($"Fehler beim Logging: {logEx.Message}");
        }
    }
}

// Verwendung
public class Program
{
    public static void Main()
    {
        var processor = new FileProcessor("processing.log");

        try
        {
            processor.ProcessFile("input.txt", "output.txt");
            Console.WriteLine("Verarbeitung erfolgreich abgeschlossen.");
        }
        catch (FileProcessingException ex)
        {
            Console.WriteLine($"Fehler bei der Dateiverarbeitung:");
            Console.WriteLine($"Datei: {ex.FilePath}");
            Console.WriteLine($"Fehler: {ex.Message}");
            if (ex.InnerException != null)
            {
                Console.WriteLine($"Ursprünglicher Fehler: {ex.InnerException.Message}");
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Unerwarteter Fehler: {ex.Message}");
        }
    }
}
```

## Live Demo Ablauf

1. **Exception Handling Basics**
   - Zeige try-catch Grundlagen
   - Demonstriere verschiedene Exception-Typen
   - Führe finally-Block vor

2. **Custom Exceptions**
   - Erstelle eigene Exception-Klasse
   - Zeige Vererbungshierarchie
   - Demonstriere Verwendung

3. **Best Practices**
   - Zeige spezifische Exception-Behandlung
   - Demonstriere Exception-Filter
   - Führe Ressourcen-Management vor

4. **Debugging**
   - Setze Breakpoints
   - Zeige Watch-Fenster
   - Demonstriere Step-Through
   - Nutze Debug.WriteLine

5. **Datei-Verarbeitungssystem**
   - Implementiere System Schritt für Schritt
   - Zeige Fehlerbehandlung in Aktion
   - Demonstriere Logging
