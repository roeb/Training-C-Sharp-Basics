# C# Typkonvertierung Demos

## Cast

```csharp
// Cast von Double zu Int
double doubleValue = 9.78;
int intValue = (int)doubleValue; // Resultat: 9
Console.WriteLine(intValue);
```

## Convert

```csharp
// Convert von String zu Int
string stringValue = "123";
int intConverted = Convert.ToInt32(stringValue); // Resultat: 123
Console.WriteLine(intConverted);
```

## Parse

```csharp
// Parse von String zu Int
string numericString = "456";
int intParsed = int.Parse(numericString); // Resultat: 456
Console.WriteLine(intParsed);
```

## TryParse

```csharp
// Sicheres Parsen von String zu Int mit TryParse
string input = "789";
bool success = int.TryParse(input, out int result); 
Console.WriteLine(success); // Ausgabe: True
Console.WriteLine(result); // Ausgabe: 789
```
