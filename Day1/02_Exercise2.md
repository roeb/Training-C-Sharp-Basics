# Übung 2 - "Temperaturrechner und Zahlenanalyse"

## Aufgabenstellung

Erstellen Sie ein Konsolenprogramm, das verschiedene Berechnungen mit Zahlen und Temperaturen durchführt.

### Teil 1 - Variablen und Berechnungen

1. Deklarieren Sie folgende Variablen mit geeigneten Datentypen:

    Temperatur in Celsius (Kommazahl)<br />
    Anzahl der Messungen (Ganzzahl)<br />
    Name der Messstation (Text)<br />
    Ist die Messung aktiv? (Boolean)
2. Weisen Sie den Variablen sinnvolle Werte zu.
3. Erstellen Sie Variablen für:
    Temperatur in Fahrenheit<br />
    Temperatur in Kelvin
4. Berechnen Sie die Umrechnungen:
    Celsius in Fahrenheit: (°C × 9/5) + 32<br />
    Celsius in Kelvin: °C + 273.15

### Teil 2 - Formatierte Ausgabe

1. Erstellen Sie eine "Messstation-Info" Ausgabe mit allen Werten:

    ```text
    Messstation: [Name]
    Status: [Aktiv/Inaktiv]
    Anzahl Messungen: [X]
    Temperaturen:
    - Celsius: [X]°C
    - Fahrenheit: [X]°F
    - Kelvin: [X]K
    ```

2. Formatieren Sie alle Temperaturwerte auf 2 Nachkommastellen
3. Verwenden Sie String-Interpolation
4. Fügen Sie eine Leerzeile zwischen den Ausgabeblöcken ein

### Teil 3 - Mathematische Operationen

1. Deklarieren Sie drei Integer-Variablen mit den Werten 17, 5 und 2
2. Führen Sie folgende Berechnungen durch und speichern Sie die Ergebnisse in passenden Variablen:
    - Addition aller Zahlen
    - Multiplikation aller Zahlen
    - Division der ersten durch die zweite Zahl (mit Nachkommastellen!)
    - Modulo (Rest) der ersten durch die dritte Zahl
    - Quadrat der ersten Zahl


3. Geben Sie alle Ergebnisse formatiert aus:

    ```text
    Mathematische Operationen:
    17 + 5 + 2 = [Ergebnis]
    17 * 5 * 2 = [Ergebnis]
    17 / 5 = [Ergebnis]
    17 % 2 = [Ergebnis]
    17² = [Ergebnis]
    ```

### Zusatzaufgaben (falls Zeit übrig ist)

1. Berechnen Sie den Durchschnitt der drei Zahlen
2. Runden Sie eine Kommazahl ihrer Wahl auf:
    - Die nächste Ganzzahl
    - Die nächste Ganzzahl nach unten
    - Die nächste Ganzzahl nach oben

3. Verwenden Sie die Math-Klasse um:
    - Den größten Wert der drei Zahlen zu finden
    - Den kleinsten Wert der drei Zahlen zu finden
    - Die Quadratwurzel einer Zahl zu berechnen

Beispielausgabe für Zusatzaufgaben:

```text
Erweiterte Analysen:
Durchschnitt: [X]
Rundungen von 17,89:
- Mathematisch: [X]
- Nach unten: [X]
- Nach oben: [X]
Math-Funktionen:
```

## Lösungshinweise für Übung 2 - "Temperaturrechner und Zahlenanalyse"

Allgemeine Tipps:

- Strukturieren Sie Ihren Code in logische Abschnitte mit Leerzeilen
- Nutzen Sie aussagekräftige Variablennamen
- Kommentieren Sie komplexere Berechnungen

Teil 1 - Variablen und Berechnungen:

- Für Temperaturen eignet sich der Datentyp double oder decimal
- Für Ganzzahlen verwenden Sie int
- Für Text string
- Für Wahr/Falsch bool
- Bei der Temperaturumrechnung achten Sie auf die Klammerung und Verwendung von Dezimalzahlen (z.B. 9.0 statt 9)

Teil 2 - Formatierte Ausgabe:

- String-Interpolation beginnt mit dem $-Zeichen
- Formatierung von Dezimalstellen: $"{wert:F2}" für 2 Nachkommastellen
- Console.WriteLine() erzeugt automatisch einen Zeilenumbruch
- Der bool-Wert kann direkt in einem if-Statement verwendet werden
- Für Leerzeilen: Console.WriteLine();

Teil 3 - Mathematische Operationen:

- Bei der Division von int-Werten wird standardmäßig ganzzahlig dividiert
- Für Dezimaldivision muss mindestens eine Zahl als Dezimalzahl vorliegen
- Modulo-Operator ist das %-Zeichen
- Für Quadrat können Sie:
  * Die Zahl mit sich selbst multiplizieren
  * Math.Pow() verwenden

Zusatzaufgaben:

- Die Math-Klasse bietet viele nützliche Methoden:
  * Math.Round() - normales Runden
  * Math.Floor() - abrunden
  * Math.Ceiling() - aufrunden
  * Math.Max() - Maximum von zwei Zahlen
  * Math.Min() - Minimum von zwei Zahlen
  * Math.Sqrt() - Quadratwurzel

Häufige Fehler und deren Vermeidung:

1. Division durch 0 vermeiden
2. Bei Berechnungen auf korrekte Datentypen achten
3. Bei der Formatierung auf korrekte Syntax der String-Interpolation achten
4. Dezimaltrennzeichen beachten (Punkt oder Komma je nach Systemeinstellung)
