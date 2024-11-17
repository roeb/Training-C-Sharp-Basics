# Demos für Tag 5

## 1. Vererbung: Wetter-System

```csharp
// Basisklasse für Wetterstation
public class WeatherStation
{
    public string Location { get; set; }
    protected double temperature;
    protected double humidity;

    public virtual void MeasureConditions()
    {
        Console.WriteLine($"Messe Wetterbedingungen in {Location}");
    }

    public virtual string GetWeatherReport()
    {
        return $"Standort: {Location}, Temperatur: {temperature}°C, Luftfeuchtigkeit: {humidity}%";
    }
}

// Erweiterte Wetterstation mit Luftdruck
public class ProfessionalStation : WeatherStation
{
    private double pressure;

    public override void MeasureConditions()
    {
        base.MeasureConditions();
        Console.WriteLine("Führe zusätzliche Luftdruckmessung durch");
    }

    public override string GetWeatherReport()
    {
        return $"{base.GetWeatherReport()}, Luftdruck: {pressure} hPa";
    }

    public void CalibrateSensors()
    {
        Console.WriteLine("Kalibriere professionelle Sensoren...");
    }
}

// Mobile Wetterstation
public class MobileStation : WeatherStation
{
    public string CurrentGPS { get; private set; }

    public void UpdateLocation(string gps)
    {
        CurrentGPS = gps;
        Console.WriteLine($"Standort aktualisiert: {gps}");
    }

    public override void MeasureConditions()
    {
        Console.WriteLine($"Prüfe GPS-Signal: {CurrentGPS}");
        base.MeasureConditions();
    }
}

// Verwendung:
WeatherStation basic = new WeatherStation { Location = "Berlin" };
ProfessionalStation pro = new ProfessionalStation { Location = "Hamburg" };
MobileStation mobile = new MobileStation { Location = "Mobil-1" };

basic.MeasureConditions();
pro.MeasureConditions();
pro.CalibrateSensors();
mobile.UpdateLocation("52.520008,13.404954");
mobile.MeasureConditions();
```

### Vererbung Beispiel Auto

```csharp
public class Vehicle
{
    public void Drive() => Console.WriteLine("Driving");
}

public class Car : Vehicle
{
    public string Brand { get; set; }
    public string Model { get; set; }

    public Car(string brand, string model)
    {
        Brand = brand;
        Model = model;
    }

    public void Tanken() => Console.WriteLine("Tanken!");
}

public class PKW : Car { 
    private int Seats;
    private int Passengers;

    public PKW(string brand, string model, int seats) : base(brand, model)
    {
        Seats = seats;
        Passengers = 0;
    }

    public void AddPerson() => Passengers++;
    public void RemovePerson() => Passengers--;

    public void GetOpenSeats() => Console.WriteLine(Seats - Passengers);
}
```

## 2. Interfaces: Drucker-System

```csharp
public interface IPrintable
{
    void StartPrint();
    bool IsBusy { get; }
    int GetPagesRemaining();
}

public interface INetworkDevice
{
    bool Connect(string network);
    void Disconnect();
    bool IsConnected { get; }
}

// Netzwerkdrucker
public class NetworkPrinter : IPrintable, INetworkDevice
{
    private bool isBusy;
    private bool isConnected;
    private int pagesInQueue;

    public bool IsBusy => isBusy;
    public bool IsConnected => isConnected;

    public void StartPrint()
    {
        if (!isConnected)
        {
            Console.WriteLine("Drucker ist nicht verbunden!");
            return;
        }

        isBusy = true;
        Console.WriteLine("Netzwerkdrucker startet Druckvorgang...");
    }

    public int GetPagesRemaining()
    {
        return pagesInQueue;
    }

    public bool Connect(string network)
    {
        Console.WriteLine($"Verbinde mit Netzwerk: {network}");
        isConnected = true;
        return true;
    }

    public void Disconnect()
    {
        isConnected = false;
        Console.WriteLine("Netzwerkverbindung getrennt");
    }

    public void AddToQueue(int pages)
    {
        pagesInQueue += pages;
    }
}

// USB-Drucker
public class USBPrinter : IPrintable
{
    private bool isBusy;
    private int pagesInQueue;

    public bool IsBusy => isBusy;

    public void StartPrint()
    {
        isBusy = true;
        Console.WriteLine("USB-Drucker startet Druckvorgang...");
    }

    public int GetPagesRemaining()
    {
        return pagesInQueue;
    }
}

// Verwendung:
NetworkPrinter networkPrinter = new NetworkPrinter();
USBPrinter usbPrinter = new USBPrinter();

// Als IPrintable behandeln
IPrintable printer1 = networkPrinter;
IPrintable printer2 = usbPrinter;

// Netzwerkfunktionen nur für NetworkPrinter
if (printer1 is INetworkDevice networkDevice)
{
    networkDevice.Connect("OFFICE-NET");
}

printer1.StartPrint();
printer2.StartPrint();
```

## 3. Polymorphismus: Report-System

```csharp
public abstract class ReportGenerator
{
    protected string reportName;
    protected DateTime reportDate;

    protected ReportGenerator(string name)
    {
        reportName = name;
        reportDate = DateTime.Now;
    }

    // Template Method Pattern
    public void GenerateReport()
    {
        PrepareData();
        CreateHeader();
        CreateContent();
        CreateFooter();
        Finalize();
    }

    protected abstract void PrepareData();
    protected abstract void CreateContent();

    protected virtual void CreateHeader()
    {
        Console.WriteLine($"=== {reportName} ===");
        Console.WriteLine($"Erstellt am: {reportDate:d}");
        Console.WriteLine("==================");
    }

    protected virtual void CreateFooter()
    {
        Console.WriteLine("==================");
        Console.WriteLine($"Ende des Reports");
    }

    protected virtual void Finalize()
    {
        Console.WriteLine("Report generiert.\n");
    }
}

public class SalesReport : ReportGenerator
{
    private readonly decimal totalSales;

    public SalesReport(decimal sales) : base("Verkaufsbericht")
    {
        totalSales = sales;
    }

    protected override void PrepareData()
    {
        Console.WriteLine("Lade Verkaufsdaten...");
    }

    protected override void CreateContent()
    {
        Console.WriteLine($"Gesamtumsatz: {totalSales:C}");
        Console.WriteLine("Top-Verkäufer: Max Mustermann");
    }
}

public class InventoryReport : ReportGenerator
{
    private readonly int itemCount;

    public InventoryReport(int items) : base("Inventurbericht")
    {
        itemCount = items;
    }

    protected override void PrepareData()
    {
        Console.WriteLine("Prüfe Lagerbestand...");
    }

    protected override void CreateContent()
    {
        Console.WriteLine($"Artikel im Lager: {itemCount}");
        Console.WriteLine("Niedrigster Bestand: Produkt A");
    }

    protected override void CreateFooter()
    {
        base.CreateFooter();
        Console.WriteLine("Bitte bei niedrigem Bestand nachbestellen!");
    }
}

// Verwendung:
List<ReportGenerator> reports = new List<ReportGenerator>
{
    new SalesReport(50000),
    new InventoryReport(1500)
};

foreach (var report in reports)
{
    report.GenerateReport();
}
```

## 4. Kombinierte Demo: Restaurant-System

```csharp
// Interfaces
public interface IOrderable
{
    string Name { get; }
    decimal Price { get; }
    int PreparationTime { get; }
    void Prepare();
}

public interface ICustomizable
{
    void AddExtra(string extra);
    List<string> GetExtras();
}

// Abstrakte Basisklasse
public abstract class MenuItem : IOrderable
{
    public string Name { get; protected set; }
    public decimal Price { get; protected set; }
    public abstract int PreparationTime { get; }

    protected MenuItem(string name, decimal price)
    {
        Name = name;
        Price = price;
    }

    public abstract void Prepare();

    public virtual string GetDescription()
    {
        return $"{Name} - {Price:C}";
    }
}

// Konkrete Klassen
public class MainDish : MenuItem, ICustomizable
{
    private readonly List<string> extras = new();

    public override int PreparationTime => 20;

    public MainDish(string name, decimal price) : base(name, price) { }

    public override void Prepare()
    {
        Console.WriteLine($"Bereite Hauptgericht zu: {Name}");
        foreach (var extra in extras)
        {
            Console.WriteLine($"- Füge {extra} hinzu");
        }
    }

    public void AddExtra(string extra)
    {
        extras.Add(extra);
        Price += 1.50m; // Aufpreis für Extras
    }

    public List<string> GetExtras()
    {
        return extras;
    }
}

public class Dessert : MenuItem
{
    public override int PreparationTime => 10;

    public Dessert(string name, decimal price) : base(name, price) { }

    public override void Prepare()
    {
        Console.WriteLine($"Bereite Dessert zu: {Name}");
    }
}

// Order Management
public class Order
{
    private readonly List<IOrderable> items = new();
    public int TableNumber { get; }

    public Order(int tableNumber)
    {
        TableNumber = tableNumber;
    }

    public void AddItem(IOrderable item)
    {
        items.Add(item);
        Console.WriteLine($"Artikel hinzugefügt: {item.Name}");
    }

    public decimal GetTotal()
    {
        return items.Sum(item => item.Price);
    }

    public void PrepareOrder()
    {
        Console.WriteLine($"\nBereite Bestellung für Tisch {TableNumber} vor:");
        foreach (var item in items)
        {
            item.Prepare();
        }
        Console.WriteLine($"Gesamtpreis: {GetTotal():C}\n");
    }
}

// Verwendung:
public class RestaurantDemo
{
    public static void RunDemo()
    {
        // Erstelle Bestellung
        var order = new Order(5);

        // Hauptgericht mit Extras
        var mainDish = new MainDish("Schnitzel", 15.90m);
        mainDish.AddExtra("Extra Pommes");
        mainDish.AddExtra("Kräuterbutter");
        order.AddItem(mainDish);

        // Dessert
        var dessert = new Dessert("Tiramisu", 6.50m);
        order.AddItem(dessert);

        // Bestellung zubereiten
        order.PrepareOrder();

        // Polymorphe Liste von Gerichten
        List<MenuItem> menu = new List<MenuItem>
        {
            new MainDish("Pizza", 12.90m),
            new Dessert("Eis", 4.50m),
            new MainDish("Pasta", 11.90m)
        };

        // Menü anzeigen
        Console.WriteLine("Aktuelle Speisekarte:");
        foreach (var item in menu)
        {
            Console.WriteLine(item.GetDescription());
        }
    }
}
```

## Live Demo Ablauf

1. **Wetter-System**
   - Zeige Vererbungshierarchie
   - Demonstriere Überschreiben von Methoden
   - Führe verschiedene Wetterstationen vor

2. **Drucker-System**
   - Implementiere Drucker-Interfaces
   - Zeige Unterschiede zwischen Druckertypen
   - Demonstriere Interface-Prüfung

3. **Report-System**
   - Erstelle verschiedene Berichtstypen
   - Zeige Template Method Pattern
   - Demonstriere polymorphes Verhalten

4. **Restaurant-System**
   - Implementiere Menü-Items und Bestellungen
   - Zeige Zusammenspiel von Interfaces und Vererbung
   - Demonstriere Bestellabwicklung
