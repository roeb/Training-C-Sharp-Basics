# Übung 1: Datei-Verarbeitungssystem

## Lösung

```csharp
using System;
using System.IO;

namespace FileProcessingSystem
{
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

    public class FileLogger
    {
        private readonly string _logPath;
        private readonly object _lock = new object();

        public FileLogger(string logPath)
        {
            _logPath = logPath;
        }

        public void LogError(string message, Exception ex)
        {
            var logEntry = $"[{DateTime.Now:yyyy-MM-dd HH:mm:ss}] {ex.GetType().Name}: {message}\n{ex.StackTrace}\n";
            
            lock (_lock)
            {
                File.AppendAllText(_logPath, logEntry);
            }
        }
    }

    public class FileProcessor
    {
        private readonly FileLogger _logger;

        public FileProcessor(FileLogger logger)
        {
            _logger = logger ?? throw new ArgumentNullException(nameof(logger));
        }

        public string ReadTextFile(string path)
        {
            if (string.IsNullOrEmpty(path))
                throw new ArgumentNullException(nameof(path));

            try
            {
                return File.ReadAllText(path);
            }
            catch (FileNotFoundException ex)
            {
                _logger.LogError($"Datei nicht gefunden: {path}", ex);
                throw new FileProcessingException("Datei konnte nicht gefunden werden", path, "Read", ex);
            }
            catch (UnauthorizedAccessException ex)
            {
                _logger.LogError($"Zugriff verweigert: {path}", ex);
                throw new FileProcessingException("Zugriff auf Datei verweigert", path, "Read", ex);
            }
            catch (Exception ex)
            {
                _logger.LogError($"Fehler beim Lesen der Datei: {path}", ex);
                throw new FileProcessingException("Fehler beim Lesen der Datei", path, "Read", ex);
            }
        }

        public void WriteTextFile(string path, string content)
        {
            if (string.IsNullOrEmpty(path))
                throw new ArgumentNullException(nameof(path));

            try
            {
                File.WriteAllText(path, content);
            }
            catch (Exception ex)
            {
                _logger.LogError($"Fehler beim Schreiben der Datei: {path}", ex);
                throw new FileProcessingException("Fehler beim Schreiben der Datei", path, "Write", ex);
            }
        }

        public void AppendToFile(string path, string content)
        {
            if (string.IsNullOrEmpty(path))
                throw new ArgumentNullException(nameof(path));

            try
            {
                File.AppendAllText(path, content);
            }
            catch (Exception ex)
            {
                _logger.LogError($"Fehler beim Anhängen an Datei: {path}", ex);
                throw new FileProcessingException("Fehler beim Anhängen an Datei", path, "Append", ex);
            }
        }

        public void ProcessDirectory(string path)
        {
            if (string.IsNullOrEmpty(path))
                throw new ArgumentNullException(nameof(path));

            try
            {
                foreach (var file in Directory.GetFiles(path, "*.txt"))
                {
                    var content = ReadTextFile(file);
                    var processedContent = content.ToUpper();
                    var outputPath = Path.Combine(path, "processed_" + Path.GetFileName(file));
                    WriteTextFile(outputPath, processedContent);
                }
            }
            catch (Exception ex)
            {
                _logger.LogError($"Fehler bei der Verarbeitung des Verzeichnisses: {path}", ex);
                throw new FileProcessingException("Fehler bei der Verzeichnisverarbeitung", path, "ProcessDirectory", ex);
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var logger = new FileLogger("error_log.txt");
            var processor = new FileProcessor(logger);

            try
            {
                // Beispiel 1: Datei lesen und schreiben
                string content = processor.ReadTextFile("input.txt");
                processor.WriteTextFile("output.txt", content.ToUpper());

                // Beispiel 2: An Datei anhängen
                processor.AppendToFile("log.txt", "Neue Zeile\n");

                // Beispiel 3: Verzeichnis verarbeiten
                processor.ProcessDirectory("testfiles");
            }
            catch (FileProcessingException ex)
            {
                Console.WriteLine($"Fehler bei {ex.Operation} von {ex.FilePath}:");
                Console.WriteLine(ex.Message);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Unerwarteter Fehler: {ex.Message}");
            }
        }
    }
}
```
