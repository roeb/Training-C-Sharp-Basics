# Übung 3 - Bankkonto

## Lösung

```csharp
public class BankAccount
{
    private readonly string _accountNumber;
    private decimal _balance;
    private bool _isLocked;

    public string AccountNumber 
    { 
        get { return _accountNumber; }
    }
    
    public string Owner { get; set; }
    
    public decimal Balance 
    { 
        get { return _balance; }
        private set { _balance = value; }
    }
    
    public bool IsLocked
    {
        get { return _isLocked; }
        private set { _isLocked = value; }
    }

    public BankAccount(string accountNumber, string owner)
    {
        if (string.IsNullOrEmpty(accountNumber) || accountNumber.Length != 10)
            throw new ArgumentException("Kontonummer muss 10 Zeichen lang sein");
            
        if (string.IsNullOrEmpty(owner))
            throw new ArgumentException("Kontoinhaber darf nicht leer sein");

        _accountNumber = accountNumber;
        Owner = owner;
        Balance = 0;
        IsLocked = false;
    }

    private void ValidateTransaction(decimal amount)
    {
        if (IsLocked)
            throw new InvalidOperationException("Konto ist gesperrt");
            
        if (amount <= 0)
            throw new ArgumentException("Betrag muss positiv sein");
    }

    public void Deposit(decimal amount)
    {
        ValidateTransaction(amount);
        Balance += amount;
    }

    public void Withdraw(decimal amount)
    {
        ValidateTransaction(amount);
        
        if (amount > Balance)
            throw new InvalidOperationException("Nicht genügend Guthaben");
            
        Balance -= amount;
    }

    public void Lock()
    {
        IsLocked = true;
    }

    public void Unlock()
    {
        IsLocked = false;
    }

    public string GetAccountInfo()
    {
        return $"Konto: {AccountNumber}\n" +
               $"Inhaber: {Owner}\n" +
               $"Kontostand: {Balance:C}\n" +
               $"Status: {(IsLocked ? "Gesperrt" : "Aktiv")}";
    }
}
```

### Beispiel für die Verwendung der vollständigen Lösung:

```csharp
try
{
    BankAccount account = new BankAccount("1234567890", "Max Mustermann");
    
    account.Deposit(1000);
    Console.WriteLine(account.GetAccountInfo());
    
    account.Withdraw(500);
    Console.WriteLine($"Neuer Kontostand: {account.Balance:C}");
    
    account.Lock();
    account.Deposit(200); // Wirft Exception wegen gesperrtem Konto
}
catch (Exception ex)
{
    Console.WriteLine($"Fehler: {ex.Message}");
}
```
