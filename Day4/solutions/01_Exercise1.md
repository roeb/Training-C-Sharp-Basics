# Übung 1 - Fahrzeug-Klasse

## Lösung

```csharp
public class Vehicle
{
    public string Brand { get; set; }
    public string Model { get; set; }
    private int year;
    public int Year
    {
        get { return year; }
        set
        {
            if (value > DateTime.Now.Year)
                throw new ArgumentException("Jahr kann nicht in der Zukunft liegen");
            if (value < 1886)
                throw new ArgumentException("Jahr kann nicht vor 1886 liegen");
            year = value;
        }
    }
    public bool IsRunning { get; private set; }
    public double FuelLevel { get; private set; }

    public Vehicle(string brand, string model, int year)
    {
        Brand = brand;
        Model = model;
        Year = year;
        IsRunning = false;
        FuelLevel = 0;
    }

    public void StartEngine()
    {
        if (FuelLevel > 0)
        {
            IsRunning = true;
        }
        else
        {
            throw new InvalidOperationException("Kein Kraftstoff vorhanden");
        }
    }

    public void StopEngine()
    {
        IsRunning = false;
    }

    public string GetVehicleInfo()
    {
        return $"{Brand} {Model} ({Year}) - Motor läuft: {IsRunning} - Tankstand: {FuelLevel:F1}L";
    }

    public void AddFuel(double amount)
    {
        if (amount <= 0)
            throw new ArgumentException("Kraftstoffmenge muss positiv sein");
        
        if (FuelLevel + amount > 60) // Beispiel für maximale Tankgröße
            throw new InvalidOperationException("Tank würde überlaufen");
        
        FuelLevel += amount;
    }
}
```

### Beispiel für die Verwendung der vollständigen Lösung:

```csharp
try
{
    Vehicle car = new Vehicle("BMW", "X3", 2022);
    car.AddFuel(45.5);
    car.StartEngine();
    Console.WriteLine(car.GetVehicleInfo());
    car.StopEngine();
    Console.WriteLine(car.GetVehicleInfo());
}
catch (Exception ex)
{
    Console.WriteLine($"Fehler: {ex.Message}");
}
