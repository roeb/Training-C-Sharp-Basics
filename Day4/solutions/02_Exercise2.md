# Übung 2 - Taschenrechner-OOP

## Lösung

```csharp
public class Calculator
{
    private double _firstNumber;
    private double _secondNumber;
    private double _result;
    private string _currentOperation;

    public double Result 
    { 
        get { return _result; } 
        private set { _result = value; }
    }

    public string CurrentOperation
    {
        get { return _currentOperation; }
        private set { _currentOperation = value; }
    }

    public Calculator()
    {
        Clear();
    }

    public Calculator(double firstNumber, double secondNumber)
    {
        _firstNumber = firstNumber;
        _secondNumber = secondNumber;
        Clear();
    }

    public void SetNumbers(double first, double second)
    {
        _firstNumber = first;
        _secondNumber = second;
    }

    public void Add()
    {
        Result = _firstNumber + _secondNumber;
        CurrentOperation = "Addition";
    }

    public void Subtract()
    {
        Result = _firstNumber - _secondNumber;
        CurrentOperation = "Subtraktion";
    }

    public void Multiply()
    {
        Result = _firstNumber * _secondNumber;
        CurrentOperation = "Multiplikation";
    }

    public void Divide()
    {
        if (_secondNumber == 0)
        {
            throw new DivideByZeroException("Division durch 0 ist nicht erlaubt");
        }
        Result = _firstNumber / _secondNumber;
        CurrentOperation = "Division";
    }

    public void Clear()
    {
        Result = 0;
        CurrentOperation = "Keine Operation";
    }
}
```

### Beispiel für die Verwendung der vollständigen Lösung:

```csharp
try
{
    Calculator calc = new Calculator();
    
    // Addition
    calc.SetNumbers(10, 5);
    calc.Add();
    Console.WriteLine($"10 + 5 = {calc.Result}");
    
    // Division
    calc.SetNumbers(20, 4);
    calc.Divide();
    Console.WriteLine($"20 / 4 = {calc.Result}");
    
    // Division durch 0
    calc.SetNumbers(15, 0);
    calc.Divide(); // Wirft eine Exception
}
catch (DivideByZeroException ex)
{
    Console.WriteLine($"Fehler: {ex.Message}");
}
