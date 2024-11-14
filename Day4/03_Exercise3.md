# Übung 3 - Bankkonto

Erstelle eine Klasse `BankAccount` für die Verwaltung eines Bankkontos mit Geschäftslogik und Validierungen.

## Anforderungen

### Properties und Felder

- AccountNumber (string) - nur lesbar
- Owner (string)
- Balance (decimal) - nur lesbar
- IsLocked (bool) - nur lesbar

### Konstruktor

- Soll AccountNumber und Owner als Parameter haben
- Initial Balance auf 0 setzen
- Initial IsLocked auf false setzen

### Methoden

- Deposit(decimal amount): Einzahlung
- Withdraw(decimal amount): Auszahlung
- Lock(): Konto sperren
- Unlock(): Konto entsperren
- GetAccountInfo(): Kontoinformationen als String

## Validierungen

- AccountNumber muss genau 10 Zeichen lang sein
- Einzahlungen müssen positiv sein
- Auszahlungen dürfen das Konto nicht überziehen
- Bei gesperrtem Konto sind keine Transaktionen möglich

## Beispiel Verwendung

```csharp
BankAccount account = new BankAccount("1234567890", "Max Mustermann");
account.Deposit(1000);
Console.WriteLine(account.Balance); // Ausgabe: 1000

account.Withdraw(500);
Console.WriteLine(account.Balance); // Ausgabe: 500

account.Lock();
// account.Withdraw(200); // Würde Exception werfen
```

## Lösungshinweise

### 1. Klassenstruktur

```csharp
public class BankAccount
{
    private readonly string _accountNumber;
    private decimal _balance;
    
    // Properties hier definieren
    // Tipp: Verwende private set für Balance und IsLocked
}
```

### 2. Validierungen

```csharp
private void ValidateTransaction(decimal amount)
{
    if (IsLocked)
    {
        // Prüfe Kontostatus
    }
    if (amount <= 0)
    {
        // Prüfe Betrag
    }
    // Weitere Validierungen...
}
```

### 3. Transaktionen

- Implementiere Validierungen vor jeder Transaktion
- Werfe aussagekräftige Exceptions bei Fehlern
- Aktualisiere Balance nur bei erfolgreicher Validierung

## Hilfreiche MSDN Dokumentation für Übung 3 - Bankkonto

### Grundlegende Konzepte

- [Properties (C# Programming Guide)](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/properties)
- [Using Properties (C#)](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/using-properties)
- [Access Modifiers (C# Programming Guide)](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/access-modifiers)
- [Constructors (C# Programming Guide)](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/constructors)

### Datentypen und String-Operationen

- [decimal Struct](https://learn.microsoft.com/en-us/dotnet/api/system.decimal)
- [String Methods](https://learn.microsoft.com/en-us/dotnet/api/system.string#methods)
- [String.Length Property](https://learn.microsoft.com/en-us/dotnet/api/system.string.length)

### Exception Handling

- [Exception Class](https://learn.microsoft.com/en-us/dotnet/api/system.exception)
- [ArgumentException Class](https://learn.microsoft.com/en-us/dotnet/api/system.argumentexception)
- [InvalidOperationException Class](https://learn.microsoft.com/en-us/dotnet/api/system.invalidoperationexception)
- [Exception Handling (C# Programming Guide)](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/exceptions/)

### Best Practices

- [Properties and Fields Guidelines](https://learn.microsoft.com/en-us/dotnet/standard/design-guidelines/property)
- [Exception Handling Guidelines](https://learn.microsoft.com/en-us/dotnet/standard/design-guidelines/exception-throwing)
