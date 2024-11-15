# Übung 2: Musik-Player

## Lösung

```csharp
using System;
using System.Collections.Generic;

namespace MusicPlayer
{
    public interface IPlayable
    {
        string Title { get; set; }
        TimeSpan Duration { get; set; }
        void Play();
        void Stop();
        string GetInfo();
    }

    public class MP3File : IPlayable
    {
        public string Title { get; set; }
        public TimeSpan Duration { get; set; }
        public long FileSize { get; set; }

        public void Play()
        {
            Console.WriteLine($"Playing MP3: {Title}...");
        }

        public void Stop()
        {
            Console.WriteLine($"Stopped MP3: {Title}");
        }

        public string GetInfo()
        {
            return $"MP3: {Title} ({Duration:mm\\:ss}) - {FileSize / 1048576.0:F1} MB";
        }
    }

    public class StreamingTrack : IPlayable
    {
        public string Title { get; set; }
        public TimeSpan Duration { get; set; }
        public string Quality { get; set; }

        public void Play()
        {
            Console.WriteLine($"Streaming: {Title} ({Quality})...");
        }

        public void Stop()
        {
            Console.WriteLine($"Stopped streaming: {Title}");
        }

        public string GetInfo()
        {
            return $"Stream: {Title} ({Duration:mm\\:ss}) - {Quality} Quality";
        }
    }

    public class Podcast : IPlayable
    {
        public string Title { get; set; }
        public TimeSpan Duration { get; set; }
        public string Author { get; set; }
        public int Episode { get; set; }

        public void Play()
        {
            Console.WriteLine($"Playing Podcast: {Title} Episode {Episode}...");
        }

        public void Stop()
        {
            Console.WriteLine($"Stopped Podcast: {Title}");
        }

        public string GetInfo()
        {
            return $"Podcast: {Title} Ep.{Episode} ({Duration:mm\\:ss}) - by {Author}";
        }
    }

    public class Playlist
    {
        private List<IPlayable> tracks = new List<IPlayable>();

        public void AddTrack(IPlayable track)
        {
            tracks.Add(track);
        }

        public void PlayAll()
        {
            foreach (var track in tracks)
            {
                track.Play();
                System.Threading.Thread.Sleep(1000); // Pause zwischen Tracks
                track.Stop();
            }
        }

        public void ShowPlaylist()
        {
            Console.WriteLine("Playlist Info:");
            for (int i = 0; i < tracks.Count; i++)
            {
                Console.WriteLine($"{i + 1}. {tracks[i].GetInfo()}");
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var playlist = new Playlist();

            playlist.AddTrack(new MP3File 
            { 
                Title = "Summer Hits",
                Duration = TimeSpan.FromMinutes(3.75),
                FileSize = 4400000 // ~4.2 MB
            });

            playlist.AddTrack(new StreamingTrack
            {
                Title = "Classical Mix",
                Duration = TimeSpan.FromMinutes(5.5),
                Quality = "High"
            });

            playlist.AddTrack(new Podcast
            {
                Title = "Tech Talk",
                Duration = TimeSpan.FromMinutes(25),
                Author = "John Doe",
                Episode = 5
            });

            playlist.ShowPlaylist();
            Console.WriteLine("\nPlaying all tracks:");
            playlist.PlayAll();
        }
    }
}
```
