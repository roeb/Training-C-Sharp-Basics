# Übung 1: Datei-Verarbeitungssystem

In dieser Übung erstellen Sie ein robustes Datei-Verarbeitungssystem mit umfassender Fehlerbehandlung.

## Aufgabenstellung

1. Erstellen Sie eine eigene Exception-Klasse:
   ```csharp
   public class FileProcessingException : Exception
   {
       public string FilePath { get; }
       public string Operation { get; }

       public FileProcessingException(string message, string filePath, string operation, Exception innerException = null) 
           : base(message, innerException)
       {
           FilePath = filePath;
           Operation = operation;
       }
   }
   ```

2. Implementieren Sie eine `FileProcessor` Klasse mit folgenden Methoden:
   - `ReadTextFile(string path)`
   - `WriteTextFile(string path, string content)`
   - `AppendToFile(string path, string content)`
   - `ProcessDirectory(string path)`

3. Implementieren Sie einen `FileLogger`:
   - Logging in eine Datei "error_log.txt"
   - Datum, Uhrzeit, Fehlertyp und Nachricht speichern
   - Verwendung in der FileProcessor-Klasse

4. Behandeln Sie folgende Fehlerszenarien:
   - Datei nicht gefunden
   - Zugriff verweigert
   - Ungültiger Dateipfad
   - Datei bereits in Verwendung
   - Nicht genügend Speicherplatz

## Beispiel-Implementation

```csharp
public class FileProcessor
{
    private readonly FileLogger _logger;

    public FileProcessor(FileLogger logger)
    {
        _logger = logger;
    }

    public string ReadTextFile(string path)
    {
        try
        {
            return File.ReadAllText(path);
        }
        catch (FileNotFoundException ex)
        {
            _logger.LogError($"Datei nicht gefunden: {path}", ex);
            throw new FileProcessingException("Datei konnte nicht gefunden werden", path, "Read", ex);
        }
        catch (Exception ex)
        {
            _logger.LogError($"Fehler beim Lesen der Datei: {path}", ex);
            throw new FileProcessingException("Fehler beim Lesen der Datei", path, "Read", ex);
        }
    }
}
```

## Erwartete Verwendung

```csharp
var logger = new FileLogger("error_log.txt");
var processor = new FileProcessor(logger);

try
{
    string content = processor.ReadTextFile("test.txt");
    processor.WriteTextFile("output.txt", content.ToUpper());
}
catch (FileProcessingException ex)
{
    Console.WriteLine($"Fehler bei {ex.Operation} von {ex.FilePath}: {ex.Message}");
}
```

## Lösungshinweise

1. Für die Exception-Klasse:
   - Verwenden Sie aussagekräftige Eigenschaften
   - Nutzen Sie die base-Konstruktoren
   - Überlegen Sie sich sinnvolle Überladungen

2. Für den FileLogger:
   - Implementieren Sie Thread-Safety
   - Verwenden Sie `StreamWriter` mit `append: true`
   - Formatieren Sie die Log-Einträge einheitlich

3. Für die FileProcessor-Klasse:
   - Validieren Sie Eingabeparameter
   - Verwenden Sie `using` für Ressourcen-Management
   - Implementieren Sie spezifische Fehlerbehandlung

## Hilfreiche MSDN Dokumentation für Übung 1

### Exception Handling & Custom Exceptions
- [Exception Class](https://learn.microsoft.com/de-de/dotnet/api/system.exception)
- [Creating and Throwing Exceptions](https://learn.microsoft.com/de-de/dotnet/standard/exceptions/how-to-create-localized-exception-messages)
- [Exception Handling Best Practices](https://learn.microsoft.com/de-de/dotnet/standard/exceptions/best-practices-for-exceptions)

### File I/O Operations
- [File Class](https://learn.microsoft.com/de-de/dotnet/api/system.io.file)
- [File.ReadAllText Method](https://learn.microsoft.com/de-de/dotnet/api/system.io.file.readalltext)
- [File.WriteAllText Method](https://learn.microsoft.com/de-de/dotnet/api/system.io.file.writealltext)
- [Directory Class](https://learn.microsoft.com/de-de/dotnet/api/system.io.directory)

### Logging und StreamWriter
- [StreamWriter Class](https://learn.microsoft.com/de-de/dotnet/api/system.io.streamwriter)
- [How to: Write Text to a File](https://learn.microsoft.com/de-de/dotnet/standard/io/how-to-write-text-to-a-file)

### Spezifische Exceptions
- [FileNotFoundException](https://learn.microsoft.com/de-de/dotnet/api/system.io.filenotfoundexception)
- [UnauthorizedAccessException](https://learn.microsoft.com/de-de/dotnet/api/system.unauthorizedaccessexception)
- [IOException](https://learn.microsoft.com/de-de/dotnet/api/system.io.ioexception)
- [PathTooLongException](https://learn.microsoft.com/de-de/dotnet/api/system.io.pathtoolongexception)

### Resource Management
- [using Statement](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/statements/using)
- [IDisposable Interface](https://learn.microsoft.com/de-de/dotnet/api/system.idisposable)

### Thread Safety
- [Thread Safety](https://learn.microsoft.com/de-de/dotnet/standard/threading/managed-threading-best-practices)
- [lock Statement](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/statements/lock)
