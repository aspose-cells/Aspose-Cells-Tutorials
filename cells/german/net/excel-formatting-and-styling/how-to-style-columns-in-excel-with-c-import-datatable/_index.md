---
category: general
date: 2026-02-21
description: Erfahren Sie, wie Sie Spalten formatieren, wenn Sie eine DataTable mit
  C# nach Excel importieren. Enthält Tipps zum Einfärben der zweiten Spalte in Excel
  und zum Importieren einer DataTable nach Excel mit C#.
draft: false
keywords:
- how to style columns
- import datatable to excel
- how to import datatable
- color second column excel
- import datatable excel c#
language: de
og_description: Wie man Spalten beim Import einer DataTable nach Excel mit C# formatiert.
  Schritt‑für‑Schritt‑Code, zweite Spalte in Excel einfärben und bewährte Vorgehensweisen.
og_title: Spalten in Excel mit C# formatieren – Komplettanleitung
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: Wie man Spalten in Excel mit C# formatiert – DataTable importieren
url: /de/net/excel-formatting-and-styling/how-to-style-columns-in-excel-with-c-import-datatable/
---

}}

Make sure to keep them unchanged.

Now produce final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Spalten in Excel mit C# formatiert – DataTable importieren

Haben Sie sich jemals gefragt, **wie man Spalten** in einem Excel-Arbeitsblatt formatiert, während man Daten direkt aus einer `DataTable` zieht? Sie sind nicht der Einzige. Viele Entwickler stoßen an Grenzen, wenn sie schnell Farbe hinzufügen wollen – vielleicht Rot für die erste Spalte, Blau für die zweite – ohne nach dem Import jede Zelle manuell zu bearbeiten.  

Die gute Nachricht? Die Lösung besteht aus ein paar Zeilen C#‑Code, und Sie haben ein komplett formatiertes Blatt, sobald die Daten ankommen. In diesem Tutorial behandeln wir außerdem **import datatable to excel**, zeigen Ihnen **color second column excel** und erklären, warum der Ansatz sowohl für .NET Framework als auch für .NET 6+ Projekte funktioniert.

---

## Was Sie lernen werden

- Ein gefülltes `DataTable` abrufen (oder on the fly erstellen).  
- Pro‑Spalte `Style`‑Objekte definieren, um Vordergrundfarben festzulegen.  
- Ein Workbook erstellen, das erste Arbeitsblatt holen und die Tabelle mit angewendeten Stilen importieren.  
- Randfälle wie leere Tabellen, benutzerdefinierte Startzeilen und dynamische Spaltenanzahlen behandeln.  

Am Ende können Sie eine formatierte Excel‑Datei in jede Reporting‑Pipeline einbinden – ohne Nachbearbeitung.

> **Voraussetzung:** Grundlegende Kenntnisse in C# und ein Verweis auf eine Tabellenkalkulationsbibliothek, die `ImportDataTable` unterstützt (z. B. Aspose.Cells, GemBox.Spreadsheet oder EPPlus mit einem Helfer). Der untenstehende Code verwendet **Aspose.Cells**, weil dessen `ImportDataTable`‑Überladung direkt ein `Style[]` akzeptiert.

## Schritt 1: Projekt einrichten und die Excel‑Bibliothek hinzufügen

Bevor wir etwas formatieren können, benötigen wir ein Projekt, das eine Excel‑Manipulationsbibliothek referenziert.

```csharp
// Install-Package Aspose.Cells -Version 24.7
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;   // For Color
```

*Pro‑Tipp:* Wenn Sie .NET 6 verwenden, fügen Sie das Paket mit `dotnet add package Aspose.Cells` hinzu. Die Bibliothek funktioniert unter Windows, Linux und macOS, sodass Sie zukunftssicher sind.

## Schritt 2: Das Quell‑DataTable abrufen oder erstellen

Der Kern des Tutorials konzentriert sich auf das Styling, aber Sie benötigen dennoch ein `DataTable`. Unten finden Sie einen kurzen Helfer, der Beispieldaten erstellt; ersetzen Sie ihn in der Produktion durch Ihren eigenen `GetTable()`‑Aufruf.

```csharp
/// <summary>
/// Returns a DataTable with three columns and five rows of demo data.
/// </summary>
static DataTable GetTable()
{
    var dt = new DataTable("Demo");
    dt.Columns.Add("ID", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Score", typeof(double));

    dt.Rows.Add(1, "Alice", 92.5);
    dt.Rows.Add(2, "Bob", 85.3);
    dt.Rows.Add(3, "Charlie", 78.9);
    dt.Rows.Add(4, "Diana", 88.1);
    dt.Rows.Add(5, "Ethan", 91.4);

    return dt;
}
```

> **Warum das wichtig ist:** Die Verwendung eines `DataTable` hält Ihre Datenquelle agnostisch – egal, ob sie aus SQL, CSV oder einer In‑Memory‑Collection stammt, die Import‑Logik bleibt gleich. Das ist das Fundament von **how to import datatable** effizient.

## Schritt 3: Spaltenstile definieren (Das Herz von „How to Style Columns“)

Jetzt sagen wir dem Arbeitsblatt, wie jede Spalte aussehen soll. Die `Style`‑Klasse ermöglicht das Festlegen von Schriftarten, Farben, Rahmen und mehr. In diesem Beispiel ändern wir nur die Vordergrundfarbe.

```csharp
// Step 3: Define column styles – red for first, blue for second, default for others
Style[] columnStyles = new Style[3]; // Assuming three columns; adjust as needed

// Style for column 0 (first column) – red text
columnStyles[0] = new Style();
columnStyles[0].ForegroundColor = Color.Red;

// Style for column 1 (second column) – blue text
columnStyles[1] = new Style();
columnStyles[1].ForegroundColor = Color.Blue;

// Column 2 (third column) – keep default styling
columnStyles[2] = new Style(); // No changes, but array entry required
```

*Was, wenn Sie mehr Spalten haben?* Erhöhen Sie einfach die Array‑Größe und füllen Sie die gewünschten Stile aus. Nicht formatierte Spalten erben automatisch den Standardstil des Arbeitsblatts.

## Schritt 4: Workbook erstellen und das DataTable mit Stilen importieren

Mit Daten und Stilen bereit, ist es Zeit, alles zusammenzuführen.

```csharp
static void Main()
{
    // Retrieve the data
    DataTable dataTable = GetTable();

    // Initialize a new workbook (in‑memory)
    Workbook workbook = new Workbook();

    // Grab the first worksheet (index 0)
    Worksheet worksheet = workbook.Worksheets[0];

    // Import the DataTable starting at cell A1 (row 0, column 0)
    // The 'true' flag tells Aspose.Cells to include column headers
    worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

    // Optional: Auto‑fit columns for a cleaner look
    worksheet.AutoFitColumns();

    // Save the result to disk
    string outputPath = "StyledDataTable.xlsx";
    workbook.Save(outputPath);

    Console.WriteLine($"Excel file saved to {outputPath}");
}
```

**Was gerade passiert ist?**  
- `ImportDataTable` kopiert Zeilen, Spalten und *optional* die Kopfzeile.  
- Durch Übergeben von `columnStyles` erhält jede Spalte den zuvor definierten `Style`.  
- Der Aufruf besteht aus einer einzigen Zeile, was bedeutet, dass **import datatable excel c#** so einfach ist.

## Schritt 5: Ergebnis überprüfen – Erwartete Ausgabe

Öffnen Sie `StyledDataTable.xlsx` in Excel (oder LibreOffice). Sie sollten sehen:

| **ID** (rot) | **Name** (blau) | **Score** (Standard) |
|--------------|-----------------|----------------------|
| 1            | Alice           | 92.5                 |
| 2            | Bob             | 85.3                 |
| …            | …               | …                    |

- Der Text der ersten Spalte erscheint in **rot**, was die Anforderung „how to style columns“ erfüllt.  
- Der Text der zweiten Spalte ist **blau**, was ebenfalls die Anfrage **color second column excel** abdeckt.

Wenn die Datei ohne Fehler geöffnet wird, haben Sie erfolgreich **how to import datatable** gemeistert, während Sie Spalten formatiert haben.

## Häufige Fragen & Randfälle

### Was, wenn das DataTable leer ist?
`ImportDataTable` erstellt weiterhin die Kopfzeile (wenn Sie `true` übergeben haben). Es werden keine Datenzeilen hinzugefügt, aber die Stile gelten weiterhin für die Kopfzellen.

### Muss der Import an einer anderen Zelle beginnen?
Ändern Sie die Parameter `rowIndex` und `columnIndex` in `ImportDataTable`. Zum Beispiel, um bei `B2` zu beginnen, verwenden Sie `1, 1` anstelle von `0, 0`.

### Möchten Sie Zeilen statt Spalten formatieren?
Sie können nach dem Import über `worksheet.Cells.Rows` iterieren und jeder Zeile ein `Style` zuweisen. Allerdings ist das Styling auf Spaltenebene weitaus performanter, da die Bibliothek den Stil einmal pro Spalte anwendet.

### Verwendung von EPPlus oder ClosedXML?
Diese Bibliotheken bieten keine direkte `ImportDataTable`‑Überladung mit einem Style‑Array. Der Workaround besteht darin, die Tabelle zuerst zu importieren und dann über den Spaltenbereich zu iterieren und `Style.Font.Color.SetColor(...)` zu setzen. Die Logik bleibt gleich, nur ein paar zusätzliche Zeilen.

## Pro‑Tipps für produktionsbereiten Code

- **Stile wiederverwenden:** Das Erstellen eines neuen `Style` für jede Spalte kann verschwenderisch sein. Speichern Sie wiederverwendbare Stile in einem Dictionary, das nach Farbe oder Schriftgewicht indiziert ist.  
- **Keine hartkodierten Spaltenzahlen:** Ermitteln Sie `dataTable.Columns.Count` und bauen Sie das `columnStyles`‑Array dynamisch auf.  
- **Thread‑Sicherheit:** Wenn Sie viele Workbooks parallel erzeugen, instanziieren Sie pro Thread ein separates `Workbook`; Aspose.Cells‑Objekte sind nicht thread‑sicher.  
- **Performance:** Für Tabellen mit mehr als 10 k Zeilen sollten Sie `AutoFitColumns` deaktivieren (es scannt jede Zelle) und die Spaltenbreiten manuell setzen.

## Vollständiges funktionierendes Beispiel (Copy‑Paste‑bereit)

```csharp
// ------------------------------------------------------------
// Full example: How to style columns while importing a DataTable
// ------------------------------------------------------------
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetTable();

        // 2️⃣ Define per‑column styles
        int colCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[colCount];

        // Red for first column
        columnStyles[0] = new Style { ForegroundColor = Color.Red };

        // Blue for second column (if it exists)
        if (colCount > 1)
            columnStyles[1] = new Style { ForegroundColor = Color.Blue };

        // Default style for remaining columns
        for (int i = 2; i < colCount; i++)
            columnStyles[i] = new Style(); // no special formatting

        // 3️⃣ Create workbook and import with styles
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
        sheet.AutoFitColumns();

        // 4️⃣ Save to file
        string path = "StyledDataTable.xlsx";
        workbook.Save(path);
        Console.WriteLine($"File saved: {path}");
    }

    // Helper: sample DataTable
    static DataTable GetTable()
    {
        var dt = new DataTable("Demo");
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        dt.Rows.Add(1, "Alice", 92.5);
        dt.Rows.Add(2, "Bob", 85.3);
        dt.Rows.Add(3, "Charlie", 78.9);
        dt.Rows.Add(4, "Diana", 88.1);
        dt.Rows.Add(5, "Ethan", 91.4);
        return dt;
    }
}
```

Führen Sie das Programm aus, öffnen Sie die erzeugte `StyledDataTable.xlsx`, und Sie sehen sofort die farbigen Spalten. Das ist der gesamte **import datatable excel c#**‑Workflow in Kürze.

## Fazit

Wir haben gerade **how to style columns** behandelt, wenn Sie **import datatable to excel** mit C# verwenden. Durch das Definieren eines `Style[]`‑Arrays und das Übergeben an `ImportDataTable` können Sie die erste Spalte rot, die zweite Spalte blau färben und den Rest unverändert lassen – alles in einer einzigen Codezeile.  

Der Ansatz skaliert: Fügen Sie weitere `Style`‑Objekte für zusätzliche Spalten hinzu, passen Sie Startzeilen an oder tauschen Sie Aspose.Cells gegen eine andere Bibliothek mit ähnlicher API aus. Jetzt können Sie gepflegte Excel‑Berichte erzeugen, ohne die Datei manuell zu bearbeiten.

**Nächste Schritte**, die Sie erkunden könnten:

- Verwenden Sie **conditional formatting**, um Werte dynamisch hervorzuheben (bezieht sich auf „color second column excel“).  
- Exportieren Sie mehrere Arbeitsblätter aus einem einzigen `DataTable`‑Set (ideal für monatliche Dashboards).  
- Kombinieren Sie dies mit **CSV → DataTable**‑Konvertierung, um eine End‑zu‑

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}