---
category: general
date: 2026-03-18
description: Erfahren Sie, wie Sie in einem Arbeitsblatt mit C# wechselnde Zeilenfarben
  anwenden. Enthält das Festlegen der Zeilenhintergrundfarbe, das Hinzufügen eines
  hellgelben Hintergrunds und das abwechselnde Färben der Zeilen.
draft: false
keywords:
- apply alternating row colors
- set row background color
- add light yellow background
- set alternating row shading
- color rows alternately
language: de
og_description: Verwenden Sie abwechselnde Zeilenfarben in C#, um die Lesbarkeit zu
  verbessern. Dieser Leitfaden zeigt, wie man die Zeilenhintergrundfarbe festlegt,
  einen hellgelben Hintergrund hinzufügt und Zeilen abwechselnd färbt.
og_title: Wechselnde Zeilenfarben in C# anwenden – Vollständiges Tutorial
tags:
- C#
- DataTable
- Spreadsheet styling
- UI design
title: Wechselnde Zeilenfarben in C# anwenden – Schritt‑für‑Schritt‑Anleitung
url: /de/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Alternierende Zeilenfarben in C# anwenden – Komplettes Tutorial

Haben Sie schon einmal **alternierende Zeilenfarben** in einem datengetriebenen Arbeitsblatt anwenden wollen, wussten aber nicht, wo Sie anfangen sollten? Sie sind nicht allein — die meisten Entwickler stoßen darauf, wenn sie zum ersten Mal Tabellen etwas freundlicher gestalten wollen. Die gute Nachricht? Mit nur wenigen Zeilen C# können Sie **die Zeilenhintergrundfarbe setzen**, ein **leichtes Gelb als Hintergrund hinzufügen** und erhalten ein poliertes Raster, das die Lesbarkeit sofort verbessert.

In diesem Tutorial führen wir Sie durch den gesamten Prozess, vom Laden einer `DataTable` in den Speicher bis zum Stylen jeder Zeile mit einem dezenten Gelb‑Weiß‑Streifen. Am Ende können Sie **Zeilen abwechselnd einfärben** und sehen ein paar praktische Varianten für unterschiedliche Farbtöne oder dynamisches Theming.

## Was Sie benötigen

Bevor wir loslegen, stellen Sie sicher, dass Sie Folgendes zur Hand haben:

- Ein .NET‑Projekt, das .NET 6 oder höher targetiert (der Code funktioniert auch mit .NET Framework 4.7+).  
- Eine Tabellenkalkulations‑Bibliothek, die Style‑Objekte unterstützt – das Beispiel verwendet eine generische `Workbook`/`Worksheet`‑API, die Bibliotheken wie **Aspose.Cells**, **GemBox.Spreadsheet** oder **ClosedXML** nachahmt.  
- Eine `DataTable`‑Quelle – kann aus einer Datenbankabfrage, einem CSV‑Import oder einer beliebigen In‑Memory‑Collection stammen.  

Keine zusätzlichen NuGet‑Pakete außer der eigentlichen Tabellenkalkulations‑Bibliothek. Wenn Sie Aspose.Cells verwenden, lautet der Namespace `Aspose.Cells`; bei ClosedXML ist es `ClosedXML.Excel`. Passen Sie die Aufrufe von `CreateStyle` und `ImportDataTable` entsprechend an.

## Schritt 1: Die Quelldaten als DataTable abrufen

Erstmal das Wichtigste – holen Sie die Daten, die Sie anzeigen möchten. In realen Anwendungen bedeutet das meist einen Datenbank‑Call, aber zur Übersichtlichkeit stubben wir eine Hilfsmethode namens `GetData()`, die eine befüllte `DataTable` zurückgibt.

```csharp
// Step 1: Retrieve the source data as a DataTable
DataTable dataTable = GetData();   // Replace with your actual data retrieval logic
```

> **Warum das wichtig ist:** Die `DataTable` definiert die Zeilen und Spalten, die später die alternierende Schattierung erhalten. Ist die Tabelle leer, gibt es nichts zu stylen – prüfen Sie also immer, dass `Rows.Count` > 0 ist, bevor Sie fortfahren.

### Pro‑Tipp
Wenn Sie Daten aus Entity Framework ziehen, können Sie nach Ausführen eines `SqlCommand` `DataTable.Load(reader)` verwenden. Das hält den Code übersichtlich und vermeidet manuelle Spaltendefinitionen.

## Schritt 2: Ein Array anlegen, das für jede Zeile einen Style hält

Als Nächstes benötigen wir einen Container, der genau so viele Elemente wie Zeilen hat. Die meisten Tabellen‑APIs erlauben das Übergeben eines Style‑Arrays an die Import‑Methode, also erstellen wir ein `Style[]`, das exakt der Zeilenanzahl entspricht.

```csharp
// Step 2: Allocate an array to hold a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];
```

> **Erklärung:** Durch das Vor‑Allokieren des Arrays vermeiden wir das Erzeugen eines neuen Style‑Objekts in jeder Iteration, was bei tausenden Zeilen einen Performance‑Vorteil bringt.

## Schritt 3: Alternierende Zeilenfarben anwenden (Hellgelb / Weiß)

Jetzt kommt das Kernstück: **alternierende Zeilenfarben anwenden**. Wir durchlaufen jede Zeile, erzeugen eine frische Style‑Instanz aus dem Workbook und setzen den Hintergrund basierend auf dem Zeilen‑Index. Gerade Zeilen erhalten eine hellgelbe Füllung, ungerade bleiben weiß.

```csharp
// Step 3: Create alternating background colors (light yellow / white) for the rows
for (int rowIndex = 0; rowIndex < dataTable.Rows.Count; rowIndex++)
{
    // Create a new style instance from the workbook
    rowStyles[rowIndex] = wb.CreateStyle();

    // Apply a light yellow background to even rows, white to odd rows
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow   // add light yellow background
        : Color.White;        // set row background color to white

    rowStyles[rowIndex].Pattern = BackgroundType.Solid; // set alternating row shading
}
```

### Warum das funktioniert
- **`rowIndex % 2 == 0`** prüft, ob die Zeile gerade ist.  
- **`Color.LightYellow`** liefert einen sanften, unaufdringlichen Farbton, der perfekt für Datentabellen ist.  
- **`BackgroundType.Solid`** sorgt dafür, dass die Füllung die gesamte Zelle bedeckt und damit den **set row background color**‑Effekt erzielt.  

Sie können `Color.LightYellow` durch jede andere Nuance ersetzen (z. B. `Color.LightCyan`), wenn Ihnen ein anderer Look lieber ist. Die gleiche Logik lässt sich auch nutzen, um **Zeilen abwechselnd zu färben** basierend auf anderen Kriterien, etwa Status‑Flags.

## Schritt 4: Die DataTable mit den vorbereiteten Styles in das Arbeitsblatt importieren

Zum Schluss schieben wir alles ins Arbeitsblatt. Die meisten Bibliotheken bieten eine Überladung von `ImportDataTable`, die ein Style‑Array akzeptiert. Das `true`‑Flag weist die API an, Spaltenüberschriften zu schreiben, und die Koordinaten `0, 0` starten in der linken oberen Zelle.

```csharp
// Step 4: Import the DataTable into the worksheet, applying the prepared row styles
ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

> **Ergebnis:** Das Arbeitsblatt zeigt nun Ihre Daten mit einem sauberen **alternierenden Zeilen‑Shading**‑Muster – hellgelb in geraden Zeilen, weiß in ungeraden. Benutzer können das Raster scannen, ohne dass die Augen hin‑ und herspringen.

### Erwartete Ausgabe
Öffnen Sie die resultierende Tabelle, sehen Sie etwa Folgendes:

| ID | Name   | Menge |
|----|--------|-------|
| **1** | Apfel   | 50    |
| **2** | Banane  | 30    |
| **3** | Kirsche | 20    |
| **4** | Dattel  | 15    |

Zeilen 1, 3, 5… haben einen **hellgelben Hintergrund**, während Zeilen 2, 4, 6… **weiß** bleiben. Die Kopfzeile (Zeile 0) übernimmt den Standard‑Style, sofern Sie sie nicht separat anpassen.

## Optionale Varianten & Sonderfälle

### 1. Eine andere Farbpalette verwenden
Falls Hellgelb nicht zu Ihrem Branding passt, ersetzen Sie einfach `Color.LightYellow` durch eine andere `System.Drawing.Color`. Für ein blau‑graues Thema könnten Sie etwa verwenden:

```csharp
rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
    ? Color.FromArgb(220, 235, 247) // soft blue
    : Color.White;
```

### 2. Dynamische Schattierung basierend auf Daten
Manchmal möchte man Zeilen hervorheben, die einer Bedingung entsprechen (z. B. niedriger Lagerbestand). Kombinieren Sie die Modulo‑Prüfung mit einem eigenen Test:

```csharp
int quantity = Convert.ToInt32(dataTable.Rows[rowIndex]["Quantity"]);
if (quantity < 20)
{
    rowStyles[rowIndex].ForegroundColor = Color.Salmon; // urgent low‑stock color
}
else
{
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow
        : Color.White;
}
```

### 3. Styles nur auf bestimmte Spalten anwenden
Wenn Sie die **set row background color**‑Funktion nur für ausgewählte Spalten benötigen, erstellen Sie für jede Spalte einen separaten Style und weisen Sie ihn nach dem Import über die Zell‑Range‑API zu.

```csharp
// Example for column B only
var colBStyle = wb.CreateStyle();
colBStyle.ForegroundColor = Color.LightYellow;
colBStyle.Pattern = BackgroundType.Solid;

// Apply after import
ws.Cells[$"B2:B{dataTable.Rows.Count + 1}"].SetStyle(colBStyle);
```

### 4. Performance‑Tipp für große Tabellen
Bei > 10 000 Zeilen sollten Sie ein einzelnes Style‑Objekt pro Farbe wiederverwenden, anstatt für jede Zeile ein neues zu erzeugen. Das Array enthält dann nur Referenzen auf die beiden geteilten Styles, was den Speicherverbrauch drastisch senkt.

```csharp
Style yellowStyle = wb.CreateStyle();
yellowStyle.ForegroundColor = Color.LightYellow;
yellowStyle.Pattern = BackgroundType.Solid;

Style whiteStyle = wb.CreateStyle();
whiteStyle.ForegroundColor = Color.White;
whiteStyle.Pattern = BackgroundType.Solid;

for (int i = 0; i < dataTable.Rows.Count; i++)
    rowStyles[i] = (i % 2 == 0) ? yellowStyle : whiteStyle;
```

## Vollständiges funktionierendes Beispiel

Unten finden Sie ein eigenständiges Programm, das Sie in eine Konsolen‑App einfügen können. Es nutzt eine fiktive `Workbook`/`Worksheet`‑API; ersetzen Sie die Typen durch die Ihrer gewählten Bibliothek.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using YourSpreadsheetLib;     // Replace with actual namespace

class Program
{
    static void Main()
    {
        // Initialize workbook & worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Step 1: Retrieve data
        DataTable dataTable = GetData();

        // Step 2: Allocate style array
        Style[] rowStyles = new Style[dataTable.Rows.Count];

        // Step 3: Apply alternating row colors
        for (int i = 0; i < dataTable.Rows.Count; i++)
        {
            rowStyles[i] = wb.CreateStyle();
            rowStyles[i].ForegroundColor = (i % 2 == 0)
                ? Color.LightYellow   // add light yellow background
                : Color.White;        // set row background color
            rowStyles[i].Pattern = BackgroundType.Solid; // set alternating row shading
        }

        // Step 4: Import with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // Save to file
        wb.Save("AlternatingRows.xlsx");
        Console.WriteLine("Workbook saved with alternating row colors.");
    }

    // Sample data generator
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(1, "Apple", 50);
        dt.Rows.Add(2, "Banana", 30);
        dt.Rows.Add(3, "Cherry", 20);
        dt.Rows.Add(4, "Date", 15);
        dt.Rows.Add(5, "Elderberry", 5);
        return dt;
    }
}
```

**Ausgabe:** Eine Datei namens `AlternatingRows.xlsx`, bei der jede Zeile abwechselnd mit einer hellgelben Füllung und Weiß erscheint, wodurch die Tabelle augenfreundlicher wird.

## Häufig gestellte Fragen

**F: Funktioniert dieser Ansatz mit Excel‑ähnlicher bedingter Formatierung?**  
A: Ja. Unterstützt Ihre Bibliothek bedingte Regeln, können Sie dieselbe Logik in eine Regel übersetzen, die `MOD(ROW(),2)=0` prüft. Die hier gezeigte code‑basierte Methode ist jedoch portabler für Bibliotheken ohne integrierte bedingte Formatierung.

**F: Was, wenn ich **Zeilen abwechselnd färben** in einer PDF‑Tabelle statt in einem Excel‑Sheet brauche?**  
A: Die meisten PDF‑Tabellengeneratoren (z. B. iTextSharp, PdfSharp) erlauben das Setzen eines `BackgroundColor` pro Zeile. Die gleiche Modulo‑Berechnung gilt—

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}