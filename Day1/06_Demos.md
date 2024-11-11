# NuGet Demo: Serilog zur Protokollierung verwenden

## Projekt einrichten

1. **Neues Projekt erstellen:**
   - C#-Konsolenanwendung in Visual Studio anlegen.
   - Projektname: `NuGetSerilogDemo`.

## NuGet-Pakete installieren

2. **NuGet-Paket-Manager öffnen:**
   - Menü: Tools > NuGet-Paket-Manager > Paket-Manager-Konsole.

3. **Serilog installieren:**
   ```shell
   Install-Package Serilog
   Install-Package Serilog.Sinks.Console
   ```

## Serilog konfigurieren und verwenden

4. **Code hinzufügen:**

```csharp
using Serilog;

class Program
{
    static void Main()
    {
        // Serilog konfigurieren
        Log.Logger = new LoggerConfiguration()
            .WriteTo.Console()
            .CreateLogger();

        // Log-Meldungen
        Log.Information("Dies ist eine Informationsmeldung");
        Log.Warning("Dies ist eine Warnmeldung");
        Log.Error("Dies ist eine Fehlermeldung");

        // Alle Logs flushen
        Log.CloseAndFlush();
    }
}
```
