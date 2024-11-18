# Übung 3: Bankkonto-System

## Lösung

```csharp
using System;
using System.Collections.Generic;

namespace BankingSystem
{
    public interface ITransferable
    {
        bool Transfer(Account target, decimal amount);
        void Deposit(decimal amount);
        bool Withdraw(decimal amount);
    }

    public abstract class Account
    {
        public string AccountNumber { get; set; }
        public decimal Balance { get; protected set; }
        public string Owner { get; set; }

        public Account(double balance) => Balance = balance;

        public abstract decimal CalculateInterest();
        public abstract void Deposit(decimal amount);

        public override string ToString()
        {
            return $"{GetType().Name} ({AccountNumber}): {Balance:F2} €";
        }
    }

    public class CheckingAccount : Account, ITransferable
    {
        public decimal Overdraft { get; set; }

        public CheckingAccount(decimal balance) : base(balance) {}

        public bool Transfer(Account target, decimal amount)
        {
            if (Withdraw(amount))
            {
                target.Deposit(amount);
                return true;
            }
            return false;
        }

        public override void Deposit(decimal amount)
        {
            if (amount > 0)
            {
                Balance += amount;
            }
        }

        public bool Withdraw(decimal amount)
        {
            if (amount > 0 && Balance - amount >= -Overdraft)
            {
                Balance -= amount;
                return true;
            }
            return false;
        }

        public override decimal CalculateInterest()
        {
            return Balance * 0.0001m; // 0.01%
        }

        public override string ToString()
        {
            return $"{base.ToString()} (Überziehungsrahmen: {Overdraft:F2} €)";
        }
    }

    public class SavingsAccount : Account, ITransferable
    {
        public decimal MinimumBalance { get; set; }

        public SavingsAccount(decimal balance) : base(balance) {}

        public bool Transfer(Account target, decimal amount)
        {
            if (Withdraw(amount))
            {
                target.Deposit(amount);
                return true;
            }
            return false;
        }

        public override void Deposit(decimal amount)
        {
            if (amount > 0)
            {
                Balance += amount;
            }
        }

        public bool Withdraw(decimal amount)
        {
            if (amount > 0 && (Balance - amount) >= MinimumBalance)
            {
                Balance -= amount;
                return true;
            }
            return false;
        }

        public override decimal CalculateInterest()
        {
            return Balance * 0.015m; // 1.5%
        }

        public override string ToString()
        {
            return $"{base.ToString()} (Mindesteinlage: {MinimumBalance:F2} €)";
        }
    }

    public class Bank
    {
        private List<Account> accounts = new List<Account>();

        public void AddAccount(Account account)
        {
            accounts.Add(account);
        }

        public void ShowAccounts()
        {
            Console.WriteLine("Kontoübersicht:");
            foreach (var account in accounts)
            {
                Console.WriteLine(account);
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var bank = new Bank();

            var checkingAccount = new CheckingAccount
            {
                AccountNumber = "DE123",
                Owner = "Max Mustermann",
                Balance = 1500m,
                Overdraft = 1000m
            };

            var savingsAccount = new SavingsAccount
            {
                AccountNumber = "DE456",
                Owner = "Max Mustermann",
                Balance = 5000m,
                MinimumBalance = 100m
            };

            bank.AddAccount(checkingAccount);
            bank.AddAccount(savingsAccount);

            bank.ShowAccounts();

            Console.WriteLine("\nÜberweise 500,00 € von Girokonto zu Sparkonto...\n");
            checkingAccount.Transfer(savingsAccount, 500m);

            bank.ShowAccounts();
        }
    }
}
```
