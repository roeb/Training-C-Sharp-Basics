# Übung 2: Musik-Player

In dieser Übung implementieren Sie ein Interface für verschiedene Medientypen in einem Musik-Player-System.

## Aufgabenstellung

1. Erstellen Sie ein Interface `IPlayable` mit:
   - Property `Title` (string)
   - Property `Duration` (TimeSpan)
   - Methode `Play()`
   - Methode `Stop()`
   - Methode `GetInfo()` die einen string zurückgibt

2. Implementieren Sie drei Klassen, die IPlayable implementieren:
   - `MP3File`
     - Zusätzliche Property: FileSize (long, in Bytes)
   - `StreamingTrack`
     - Zusätzliche Property: Quality (string, z.B. "High", "Medium", "Low")
   - `Podcast`
     - Zusätzliche Properties: Author (string), Episode (int)

3. Erstellen Sie eine `Playlist` Klasse mit:
   - Liste von IPlayable-Objekten
   - Methode zum Hinzufügen von Tracks
   - Methode zum Abspielen aller Tracks
   - Methode zur Anzeige aller Track-Informationen

## Beispiel-Implementation

```csharp
public interface IPlayable
{
    string Title { get; set; }
    TimeSpan Duration { get; set; }
    void Play();
    void Stop();
    string GetInfo();
}

// Implementieren Sie hier die konkreten Klassen
```

## Erwartete Ausgabe

```
Playlist Info:
1. MP3: Summer Hits (3:45) - 4.2 MB
2. Stream: Classical Mix (5:30) - High Quality
3. Podcast: Tech Talk Ep.5 (25:00) - by John Doe

Playing: Summer Hits...
Playing: Classical Mix...
Playing: Tech Talk...
```

## Lösungshinweise

1. Für das Interface:
   - Properties können im Interface als `{ get; set; }` deklariert werden
   - Methoden werden ohne Implementierung deklariert

2. Für die konkreten Klassen:
   - Jede Klasse muss alle Interface-Member implementieren
   - Verwenden Sie `Console.WriteLine()` für die Play/Stop-Methoden
   - GetInfo() sollte alle relevanten Informationen zurückgeben

3. Für die Playlist-Klasse:

   ```csharp
   public class Playlist
   {
       private List<IPlayable> tracks = new List<IPlayable>();
       
       public void AddTrack(IPlayable track)
       {
           tracks.Add(track);
       }
       
       public void PlayAll()
       {
           foreach(var track in tracks)
           {
               track.Play();
           }
       }
   }
   ```

4. Für die TimeSpan-Verwendung:
   - Erstellen mit `TimeSpan.FromMinutes()` oder `new TimeSpan(0, 3, 45)` für 3:45

## Ressourcen für Übung 2: Musik-Player

### Grundlegende Konzepte

- [Interfaces (C#)](https://learn.microsoft.com/de-de/dotnet/csharp/language-reference/keywords/interface)
- [Properties (C#)](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/classes-and-structs/properties)
- [TimeSpan Struktur](https://learn.microsoft.com/de-de/dotnet/api/system.timespan)

### Collections und Listen

- [List<T> Klasse](https://learn.microsoft.com/de-de/dotnet/api/system.collections.generic.list-1)
- [Collections (C#)](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/concepts/collections)

### String Formatierung und Ausgabe

- [String.Format Methode](https://learn.microsoft.com/de-de/dotnet/api/system.string.format)
- [Console.WriteLine Methode](https://learn.microsoft.com/de-de/dotnet/api/system.console.writeline)

### Zusätzliche Ressourcen

- [Implementieren von Interfaces](https://learn.microsoft.com/de-de/dotnet/csharp/programming-guide/interfaces/explicit-interface-implementation)
- [Object-Oriented Programming in C#](https://learn.microsoft.com/de-de/dotnet/csharp/fundamentals/object-oriented/)
