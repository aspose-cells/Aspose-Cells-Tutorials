---
category: general
date: 2026-04-07
description: Fügen Sie Excel‑Zeilen Hintergrundfarben mit C# hinzu. Erfahren Sie,
  wie Sie wechselnde Zeilenfarben anwenden, einheitliche Hintergrundstile festlegen
  und eine Datentabelle in Excel in einem einzigen Workflow importieren.
draft: false
keywords:
- add background color excel
- apply alternating row colors
- style excel rows
- set solid background
- import datatable to excel
language: de
og_description: Hintergrundfarbe zu Excel‑Zeilen mit C# hinzufügen. Dieser Leitfaden
  zeigt, wie man abwechselnde Zeilenfarben anwendet, einen einheitlichen Hintergrund
  festlegt und Datentabellen effizient nach Excel importiert.
og_title: Hintergrundfarbe zu Excel hinzufügen – Wechselnde Zeilenstile in C#
tags:
- C#
- Excel
- DataTable
- Styling
title: Hintergrundfarbe zu Excel hinzufügen – Alternierende Zeilenstile in C#
url: /de/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hintergrundfarbe zu Excel hinzufügen – Wechselnde Zeilenstile in C#

Haben Sie jemals **add background color excel** Zeilen hinzufügen müssen, waren sich aber nicht sicher, wie das ohne tausend Zeilen umständlichen Code geht? Sie sind nicht allein — die meisten Entwickler stoßen an diese Grenze, wenn sie zum ersten Mal versuchen, ihre Tabellenkalkulationen mehr als nur einen rohen Datenabwurf aussehen zu lassen.  

Die gute Nachricht? In nur wenigen Minuten können Sie **apply alternating row colors** anwenden, einen **solid background** setzen und sogar **import datatable to excel** verwenden, mit einem sauberen, wiederverwendbaren Muster in C#.  

In diesem Tutorial führen wir Sie durch den gesamten Prozess, vom Laden von Daten in ein `DataTable` bis hin zur Formatierung jeder Zeile mit einem hell‑gelb‑weißen Streifenmuster. Keine externen Bibliotheken außer einem soliden Excel‑Handling‑Paket (wie **ClosedXML** oder **GemBox.Spreadsheet**) sind erforderlich, und Sie werden sehen, warum dieser Ansatz sowohl performant als auch leicht zu warten ist.

## Was Sie lernen werden

- Wie man Daten abruft und in ein Excel‑Arbeitsblatt einfügt.
- Wie man **style excel rows** mit wechselnden Hintergrundfarben formatiert.
- Die Funktionsweise von **set solid background** mithilfe des `Style`‑Objekts.
- Wie man **import datatable to excel** verwendet und dabei Zeilenstile beibehält.
- Tipps zum Umgang mit Sonderfällen wie leeren Tabellen oder benutzerdefinierten Farbschemata.

> **Pro tip:** Wenn Sie bereits ein Workbook‑Objekt (`wb`) aus einer Bibliothek verwenden, die die Erstellung von Stilen unterstützt, können Sie dieselben `Style`‑Instanzen über mehrere Arbeitsblätter hinweg wiederverwenden — spart Speicher und hält Ihren Code ordentlich.

---

## Schritt 1: Daten abrufen – Vorbereitung des DataTable

Bevor irgendeine Formatierung stattfinden kann, benötigen wir eine Datenquelle für die Zeilen. In den meisten realen Szenarien stammt diese aus einer Datenbank, einer API oder einer CSV‑Datei. Zur Veranschaulichung erstellen wir einfach ein einfaches `DataTable` im Speicher.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using GemBox.Spreadsheet;      // Or ClosedXML, whichever you prefer

// Simulated data fetch – replace with your own data access logic
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with sample rows
    for (int i = 1; i <= 10; i++)
        table.Rows.Add(i, $"Student {i}", Math.Round(new Random().NextDouble() * 100, 2));

    return table;
}
```

**Why this matters:** Die Verwendung eines `DataTable` gibt Ihnen einen tabellarischen, schema‑bewussten Container, den die Excel‑Bibliothek direkt importieren kann, wodurch das Schreiben von Zell‑für‑Zell‑Schleifen entfällt.

---

## Schritt 2: Zeilenstile erstellen – **Apply alternating row colors**

Jetzt erstellen wir ein Array von `Style`‑Objekten — eines pro Zeile — damit jede Zeile ihren eigenen Hintergrund erhalten kann. Das Muster, das wir verwenden, ist ein klassisches Hellgelb für gerade Zeilen und Weiß für ungerade Zeilen.

```csharp
// Assume 'wb' is an existing Workbook instance
Workbook wb = new Workbook();

// Retrieve data
DataTable dataTable = GetData();

// Allocate a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style instance
    rowStyles[i] = wb.CreateStyle();

    // Choose background colour based on row index
    rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;

    // Ensure the colour is actually applied
    rowStyles[i].Pattern = BackgroundType.Solid;   // <-- **set solid background**
}
```

**Explanation:**  
- `wb.CreateStyle()` gibt Ihnen ein sauberes Stilobjekt, das Sie anpassen können, ohne andere zu beeinflussen.  
- Der ternäre Operator `(i % 2 == 0)` entscheidet, ob die Zeile gerade (hellgelb) oder ungerade (weiß) ist.  
- Das Setzen von `Pattern = BackgroundType.Solid` ist der entscheidende Schritt, der **set solid background** bewirkt; ohne ihn würde die Farbe ignoriert werden.

---

## Schritt 3: Ziel‑Arbeitsblatt holen

Die meisten Bibliotheken stellen eine Arbeitsblattsammlung bereit. Wir arbeiten mit dem ersten, aber Sie können jeden beliebigen Index oder Namen anvisieren.

```csharp
Worksheet worksheet = wb.Worksheets[0];   // First worksheet in the workbook
```

Wenn das Workbook brandneu ist, erstellt die Bibliothek in der Regel ein Standardblatt für Sie. Andernfalls können Sie eines explizit hinzufügen:

```csharp
// Alternative: create a new sheet named "Report"
Worksheet worksheet = wb.Worksheets.Add("Report");
```

---

## Schritt 4: DataTable mit Zeilenstilen importieren – **Import datatable to excel**

Mit den fertigen Stilen ist der letzte Schritt, das `DataTable` in das Blatt zu übertragen und dabei den entsprechenden Stil auf jede Zeile anzuwenden.

```csharp
// Parameters: (DataTable, includeHeaders, startRow, startColumn, stylesArray)
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

**What’s happening under the hood?**  
- `true` weist die Methode an, Spaltenüberschriften als erste Zeile zu schreiben.  
- `0, 0` markiert die obere linke Ecke (A1) als Einfügepunkt.  
- `rowStyles` ordnet jedem `Style` die passende Datenzeile zu und liefert uns die zuvor vorbereiteten wechselnden Farben.

---

## Schritt 5: Arbeitsmappe speichern

Das letzte Puzzleteil ist, die Arbeitsmappe in einer Datei zu speichern, damit Sie sie in Excel öffnen und das Ergebnis sehen können.

```csharp
// Choose a format – XLSX is the modern default
wb.Save("StudentScores.xlsx");

// Optional: open automatically (Windows only)
System.Diagnostics.Process.Start("StudentScores.xlsx");
```

Öffnen Sie die Datei und Sie sollten ein ordentlich formatiertes Blatt sehen:

- Kopfzeile fett (Standard‑Bibliotheksstil).  
- Zeile 1, 3, 5… mit einem sauberen weißen Hintergrund.  
- Zeile 2, 4, 6… mit einer dezenten hell‑gelben Füllung, die das Scannen erleichtert.

### Erwarteter Ausgabeschnappschuss

| Id | Name      | Score |
|----|-----------|-------|
| 1  | Student 1 | 78.45 |
| 2  | Student 2 | 62.13 |
| 3  | Student 3 | 91.27 |
| …  | …         | …     |

Zeilen 2, 4, 6, … erscheinen mit einem hell‑gelben Hintergrund — genau der **apply alternating row colors** Effekt, den wir anstrebten.

![Add background color excel example](https://example.com/excel-background.png "Add background color excel example")

*(Alt-Text enthält das primäre Schlüsselwort für SEO.)*

---

## Umgang mit Sonderfällen & Variationen

### Leere DataTable

Wenn `dataTable.Rows.Count` null ist, ist das `rowStyles`‑Array leer und `ImportDataTable` schreibt trotzdem die Kopfzeile (wenn `includeHeaders` `true` ist). Es wird keine Ausnahme ausgelöst, aber Sie sollten vielleicht verhindern, dass fast eine leere Datei erzeugt wird:

```csharp
if (dataTable.Rows.Count == 0)
{
    Console.WriteLine("No data to export – workbook will contain only headers.");
}
```

### Benutzerdefinierte Farbschemata

Möchten Sie statt Gelb/Weiß ein blaues/graues Streifenmuster? Ersetzen Sie einfach die `Color`‑Werte:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightBlue : Color.LightGray;
```

Ziehen Sie die Farben gern aus einer Konfigurationsdatei, damit Nicht‑Entwickler die Palette anpassen können, ohne Code zu ändern.

### Wiederverwendung von Stilen über mehrere Arbeitsblätter

Wenn Sie mehrere Tabellen in dieselbe Arbeitsmappe exportieren, können Sie das Stil‑Array einmal erzeugen und wiederverwenden:

```csharp
Style[] sharedStyles = CreateAlternatingStyles(dataTable.Rows.Count);
worksheet1.Cells.ImportDataTable(dt1, true, 0, 0, sharedStyles);
worksheet2.Cells.ImportDataTable(dt2, true, 0, 0, sharedStyles);
```

Achten Sie nur darauf, dass beide Tabellen die gleiche Zeilenanzahl haben, oder erzeugen Sie ein neues Array pro Blatt.

---

## Vollständiges funktionierendes Beispiel

Wenn wir alles zusammenfügen, erhalten Sie ein eigenständiges Programm, das Sie in eine Konsolen‑App kopieren und einfügen können.

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;   // Install-Package GemBox.Spreadsheet

class Program
{
    static void Main()
    {
        // License free for small projects – remove for commercial use
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Initialise workbook
        Workbook wb = new Workbook();

        // 3️⃣ Create alternating row styles
        Style[] rowStyles = CreateAlternatingStyles(dataTable.Rows.Count);

        // 4️⃣ Get (or create) the target worksheet
        Worksheet ws = wb.Worksheets.Add("Report");

        // 5️⃣ Import data with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // 6️⃣ Save the file
        wb.Save("Report.xlsx");
        Console.WriteLine("Excel file created – check Report.xlsx");
    }

    // Helper: generate a DataTable with sample data
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        var rnd = new Random();
        for (int i = 1; i <= 12; i++)
            dt.Rows.Add(i, $"Student {i}", Math.Round(rnd.NextDouble() * 100, 2));

        return dt;
    }

    // Helper: create style array for alternating colors
    static Style[] CreateAlternatingStyles(int rowCount)
    {
        var wb = new Workbook();               // Temporary workbook for style creation
        var styles = new Style[rowCount];
        for (int i = 0; i < rowCount; i++)
        {
            styles[i] = wb.CreateStyle();
            styles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;
            styles[i].Pattern = BackgroundType.Solid;   // **set solid background**
        }
        return styles;
    }
}
```

Führen Sie das Programm aus, öffnen Sie `Report.xlsx`, und Sie sehen den wechselnden Hintergrund genau wie beschrieben.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}