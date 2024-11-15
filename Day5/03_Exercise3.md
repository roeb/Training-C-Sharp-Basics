# Übung 3: Bankkonto-System

In dieser Übung implementieren Sie ein Bankkonto-System, das sowohl Vererbung als auch Interfaces nutzt.

## Aufgabenstellung

1. Erstellen Sie ein Interface `ITransferable`:

   ```csharp
   public interface ITransferable
   {
       bool Transfer(Account target, decimal amount);
       void Deposit(decimal amount);
       bool Withdraw(decimal amount);
   }
   ```

2. Erstellen Sie eine abstrakte Basisklasse `Account`:
   - Properties:
     - AccountNumber (string)
     - Balance (decimal)
     - Owner (string)
   - Abstrakte Methode: CalculateInterest()

3. Implementieren Sie zwei Kontotypen:
   - `CheckingAccount` (Girokonto)
     - Überziehungsrahmen (Overdraft) als zusätzliche Property
     - Implementierung von ITransferable
     - Niedrigerer Zinssatz (z.B. 0.01%)

   - `SavingsAccount` (Sparkonto)
     - Mindesteinlage (MinimumBalance) als zusätzliche Property
     - Implementierung von ITransferable
     - Höherer Zinssatz (z.B. 1.5%)

4. Erstellen Sie eine `Bank` Klasse:
   - Liste aller Konten
   - Methode zum Hinzufügen von Konten
   - Methode zur Anzeige aller Kontostände

## Beispiel-Implementation

```csharp
public abstract class Account
{
    public string AccountNumber { get; set; }
    public decimal Balance { get; protected set; }
    public string Owner { get; set; }

    public abstract decimal CalculateInterest();
}

// Implementieren Sie hier die konkreten Kontotypen
```

## Erwartete Ausgabe

```text
Kontoübersicht:
Girokonto (DE123): 1500,00 € (Überziehungsrahmen: 1000,00 €)
Sparkonto (DE456): 5000,00 € (Mindesteinlage: 100,00 €)

Überweise 500,00 € von Girokonto zu Sparkonto...

Neue Kontoübersicht:
Girokonto (DE123): 1000,00 € (Überziehungsrahmen: 1000,00 €)
Sparkonto (DE456): 5500,00 € (Mindesteinlage: 100,00 €)
```

## Lösungshinweise

1. Für die Account-Klasse:
   - Verwenden Sie Properties mit private set für Balance
   - Implementieren Sie Basis-Validierungen für Geldbeträge

2. Für die konkreten Kontoklassen:
   - Überprüfen Sie bei Abhebungen den Überziehungsrahmen/Mindesteinlage
   - Implementieren Sie unterschiedliche Zinssätze

3. Für die Transfer-Methode:

   ```csharp
   public bool Transfer(Account target, decimal amount)
   {
       if (Withdraw(amount))
       {
           target.Deposit(amount);
           return true;
       }
       return false;
   }
   ```

## MSDN Documentation Resources für Übung 3: Bankkonto-System

### Grundlegende Konzepte

1. **Interfaces**
   - [Interfaces - Grundlagen und Best Practices](https://learn.microsoft.com/de-de/dotnet/csharp/fundamentals/types/interfaces)
   - [Interface-Implementierung](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/interfaces/explicit-interface-implementation)

2. **Abstrakte Klassen**
   - [Abstrakte und versiegelte Klassen und Klassenmember](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members)
   - [Abstract Modifier](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/keywords/abstract)

3. **Properties**
   - [Properties](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/properties)
   - [Auto-Implemented Properties](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/auto-implemented-properties)

4. **Vererbung**
   - [Vererbung in C#](https://learn.microsoft.com/de-de/dotnet/csharp/fundamentals/object-oriented/inheritance)
   - [Polymorphismus](https://learn.microsoft.com/de-de/dotnet/csharp/fundamentals/object-oriented/polymorphism)

### Datentypen und Collections

5. **Decimal-Typ**
   - [Decimal Struktur](https://learn.microsoft.com/de-de/dotnet/api/system.decimal)
   - [Numerische Typen](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/builtin-types/floating-point-numeric-types)

6. **List<T>**
   - [List<T> Klasse](https://learn.microsoft.com/de-de/dotnet/api/system.collections.generic.list-1)
   - [Collections (C#)](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/concepts/collections)

### Zugriffsmodifizierer

7. **Access Modifiers**
   - [Zugriffsmodifizierer](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/access-modifiers)
   - [Protected Zugriffsmodifizierer](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/keywords/protected)
