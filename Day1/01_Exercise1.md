# Übung 1 - "Mein erstes C# Programm"

## Aufgabenstellung

Erstellen Sie ein Konsolenprogramm, das als persönlicher Taschenrechner für den Baumarkt dient.

Die Lernziele:

- Erstellen und Strukturieren eines C# Projekts
- Umgang mit Basis-Datentypen
- Ein- und Ausgabe über die Konsole
- Grundlegende mathematische Operationen
- String-Formatierung
- Typkonvertierung

### Teil 1 - Projekt erstellen 

1. Erstellen Sie ein neues C# Konsolenprojekt mit dem Namen "BaumarktRechner"
2. Ändern Sie den Namespace auf "MeineProgramme"
3. Fügen Sie einen aussagekräftigen Kommentar mit Ihrem Namen als Autor am Anfang der Program.cs ein

### Teil 2 - Benutzereingaben 

1. Geben Sie einen Willkommenstext aus: "Willkommen beim Baumarkt-Rechner!"
2. Fragen Sie nach dem Namen des Benutzers und speichern Sie diesen in einer Variable
3. Begrüßen Sie den Benutzer mit seinem Namen
4. Fragen Sie nach der Länge des Raums in Metern
5. Fragen Sie nach der Breite des Raums in Metern
6. Speichern Sie beide Werte in geeigneten Variablen

### Teil 3 - Berechnungen und Ausgabe 

1. Berechnen Sie die Fläche des Raums
2. Berechnen Sie den Umfang des Raums
3. Geben Sie beide Ergebnisse formatiert aus:
   - "Hallo [Name], dein Raum hat folgende Maße:"
   - "Fläche: [X] Quadratmeter"
   - "Umfang: [X] Meter"

### Zusatzaufgaben (falls Zeit übrig ist)

1. Runden Sie die Ergebnisse auf 2 Nachkommastellen
2. Fügen Sie eine Berechnung hinzu, wie viele Farbeimer benötigt werden (1 Eimer reicht für 10m²)
3. Fragen Sie den Preis pro Farbeimer ab und berechnen Sie die Gesamtkosten

### Beispielausgabe

```
Willkommen beim Baumarkt-Rechner!
Wie ist dein Name? Max
Hallo Max!
Wie lang ist dein Raum (in Meter)? 4,5
Wie breit ist dein Raum (in Meter)? 3,2
Hallo Max, dein Raum hat folgende Maße:
Fläche: 14,40 Quadratmeter
Umfang: 15,40 Meter
Du benötigst 2 Farbeimer
Bei einem Preis von 24,99 € pro Eimer betragen die Gesamtkosten: 49,98 €
```

### Hinweise für die Teilnehmer

- Verwenden Sie Console.WriteLine() für Ausgaben
- Verwenden Sie Console.ReadLine() für Eingaben
- Denken Sie an die Konvertierung von string zu double bei den Eingaben
- Nutzen Sie String-Interpolation ($"...") für formatierte Ausgaben

