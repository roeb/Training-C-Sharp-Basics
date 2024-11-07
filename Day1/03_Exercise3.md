# Übung 3 - String-Manipulation und Formatierung

## Aufgabenstellung:

Erstellen Sie eine Konsolenanwendung, die verschiedene String-Manipulationen und Formatierungen demonstriert.

### Teil 1 - Personendaten

1. Deklarieren Sie Variablen für:
   - Vor- und Nachname (string)
   - Alter (int)
   - Körpergröße in Meter (double)
   - Gehalt (decimal)

2. Lesen Sie diese Werte von der Konsole ein
   - Verwenden Sie Convert oder Parse für die Typkonvertierung
   - Fangen Sie mögliche Fehleingaben ab (optional)

3. Geben Sie die Daten in folgenden Formaten aus:
   - "Mein Name ist {Vorname} {Nachname}."
   - "Ich bin {Alter} Jahre alt und {Größe}m groß." (Größe mit 2 Dezimalstellen)
   - "Mein Gehalt beträgt {Gehalt:C2}" (als Währungsbetrag)

### Teil 2 - String-Manipulation

1. Erstellen Sie aus Vor- und Nachname:
   - Initialen (z.B. "Max Mustermann" → "M.M.")
   - Den Namen in Großbuchstaben
   - Den Namen in Kleinbuchstaben
   - Die Anzahl der Buchstaben im Gesamtnamen (ohne Leerzeichen)

### Teil 3 - Formatierte Tabelle

Erstellen Sie eine Ausgabe in folgendem Format:

```text
+----------------+------------------+
| Name           | Max Mustermann   |
| Alter          | 30 Jahre         |
| Größe          | 1,80 m           |
| Gehalt         | 50.000,00 €      |
| Initialen      | M.M.             |
+----------------+------------------+
```

## Lösungshinweise für Übung 3

### Teil 1 - Personendaten

- Für die Konsoleneingabe: Console.ReadLine() verwenden
- Für Konvertierungen bieten sich an:
  - double.Parse() oder Convert.ToDouble() für die Größe
  - Beachten Sie die Kultureinstellungen wegen Dezimaltrennzeichen
- Bei der String-Interpolation auf das $-Zeichen vor dem String achten
- Für Dezimalstellen bei Zahlen kann man :F2 als Formatierungsanweisung nutzen
- Für Währungsbeträge eignet sich :C als Formatierungsanweisung

### Teil 2 - String-Manipulation

- Denken Sie daran, dass Strings ein Array von Zeichen sind
- Nützliche String-Methoden:
  - Substring()
  - ToUpper() / ToLower()
  - Replace()
  - Split()
- Für die Initialen:
  - Überlegen Sie, wie Sie den ersten Buchstaben jedes Namens extrahieren können
  - String-Verkettung mit + oder StringBuilder beachten

### Teil 3 - Formatierte Tabelle

- Für gleichmäßige Spaltenbreiten:
  - Die ToString()-Methode kann mit PadRight() oder PadLeft() kombiniert werden
  - Alternativ kann die {0,-20} Syntax in string.Format verwendet werden
- Konstanten für die Tabellenbreite definieren macht den Code übersichtlicher
