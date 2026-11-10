---
category: general
date: 2026-10-01
description: abwechselnde Spaltenfarben in Excel mit C# – lernen Sie, eine Excel-Datei
  aus einer DataTable zu erstellen, die Zellenhintergrundfarbe in C# festzulegen und
  eine DataTable mit formatierten Spalten nach Excel zu importieren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- alternating column colors excel
- set cell background color c#
- create excel file from datatable c#
- import datatable to excel
language: de
lastmod: 2026-10-01
og_description: Wechselnde Spaltenfarben in Excel leicht gemacht. Folgen Sie dieser
  Anleitung, um eine Excel-Datei aus einer DataTable zu erstellen, die Zellhintergrundfarbe
  in C# zu setzen und eine DataTable mit formatierten Spalten nach Excel zu importieren.
og_image_alt: Screenshot of an Excel sheet showing alternating column colors applied
  by C# code
og_title: Wechselnde Spaltenfarben in Excel mit C# hinzufügen – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: alternating column colors excel using C# – learn to create an Excel
    file from a DataTable, set cell background color c#, and import datatable to excel
    with styled columns.
  headline: How to add alternating column colors in Excel using C#
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: Wie man in Excel mit C# abwechselnde Spaltenfarben hinzufügt
url: /de/net/excel-colors-and-background-settings/how-to-add-alternating-column-colors-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man wechselnde Spaltenfarben in Excel mit C# hinzufügt

Wenn Sie **alternating column colors excel** in einem von Ihrer Anwendung erzeugten Bericht benötigen, zeigt Ihnen dieser Leitfaden eine vollständige Lösung. Sie sehen, wie man eine Excel-Datei aus einer `DataTable` erstellt, die Zellenhintergrundfarbe im C#‑Stil festlegt und eine DataTable nach Excel importiert, während für jede Spalte ein unterschiedlicher Stil angewendet wird.

Der Leitfaden deckt alles ab, was Sie benötigen: erforderliche NuGet‑Pakete, ein vollständiges, ausführbares Code‑Beispiel und Erklärungen, warum jeder Schritt wichtig ist. Am Ende haben Sie ein formatiertes Arbeitsbuch, das direkt in Microsoft Excel geöffnet werden kann.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

* .NET 6.0 (oder später) SDK installiert  
* Visual Studio 2022 (oder jede C#‑kompatible IDE)  
* Die **Aspose.Cells for .NET**‑Bibliothek – installieren Sie sie mit  

```bash
dotnet add package Aspose.Cells
```

Aspose.Cells stellt die Klassen `Workbook`, `Worksheet`, `Style` und `BackgroundType` bereit, die im Beispiel verwendet werden.

## Schritt 1: Die Quelldaten als `DataTable` abrufen

Die erste Aufgabe besteht darin, die Daten zu erhalten, die Sie exportieren möchten. In realen Projekten füllen Sie die `DataTable` möglicherweise aus einer Datenbankabfrage, einem API‑Aufruf oder einer beliebigen In‑Memory‑Sammlung.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetData()
{
    // Create a sample DataTable with three columns and five rows
    DataTable table = new DataTable("Sample");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    for (int i = 1; i <= 5; i++)
    {
        table.Rows.Add(i, $"Student {i}", 60 + i * 5);
    }
    return table;
}
```

**Why this matters:**  
Eine `DataTable` ist ein universeller Container, der sich sauber auf ein Excel‑Arbeitsblatt abbilden lässt. Die Verwendung einer `DataTable` ermöglicht Ihnen **create excel file from datatable c#**, ohne für jede Spalte eigene Schleifen schreiben zu müssen.

## Schritt 2: Ein neues Workbook erstellen und das erste Arbeitsblatt abrufen

```csharp
// Initialize a new workbook – this represents the Excel file
Workbook workbook = new Workbook();

// The first worksheet is created by default
Worksheet worksheet = workbook.Worksheets[0];
```

**Explanation:**  
`Workbook` ist das Root‑Objekt; `Worksheets[0]` gibt Ihnen das Standard‑Blatt, in das die Daten eingefügt werden.

## Schritt 3: Einen eindeutigen Stil für jede Spalte vorbereiten (wechselnde Hintergrundfarben)

Um **alternating column colors excel** zu erreichen, erzeugen wir für jede Spalte ein `Style` und weisen eine helle Hintergrundfarbe zu, die zwischen zwei Farbtönen wechselt.

```csharp
// Determine how many columns we have
int columnCount = dataTable.Columns.Count;
Style[] columnStyles = new Style[columnCount];

// Create a style for each column
for (int i = 0; i < columnCount; i++)
{
    // Create a fresh style instance
    Style style = workbook.CreateStyle();

    // Alternate between LightYellow and LightCyan
    style.ForegroundColor = (i % 2 == 0)
        ? System.Drawing.Color.LightYellow
        : System.Drawing.Color.LightCyan;

    // Use a solid fill pattern
    style.Pattern = BackgroundType.Solid;

    columnStyles[i] = style;
}
```

**Why we use a loop:**  
Die Schleife stellt sicher, dass **set cell background color c#** konsequent angewendet wird, selbst wenn sich die Spaltenanzahl zur Laufzeit ändert. Das macht die Lösung robust für dynamische Berichte.

## Schritt 4: Die `DataTable` in das Arbeitsblatt importieren und die Spaltenstile anwenden

Aspose.Cells kann eine `DataTable` direkt importieren, und wir können das Array von Stilen übergeben, um jede Spalte zu färben.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// The second argument (true) tells the API to add column headers
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**What happens under the hood:**  
`ImportDataTable` schreibt zuerst die Kopfzeile, dann jede Datenzeile. Da wir `columnStyles` übergeben haben, erhält jede Zelle in einer bestimmten Spalte den entsprechenden Stil, wodurch die gewünschten wechselnden Farben entstehen.

## Schritt 5: Das formatierte Workbook in einer Datei speichern

```csharp
// Choose an output path – adjust as needed for your environment
string outputPath = @"C:\Temp\StyledTable.xlsx";
workbook.Save(outputPath);

Console.WriteLine($"Workbook saved to {outputPath}");
```

Wenn Sie *StyledTable.xlsx* in Excel öffnen, sehen Sie jede Spalte abwechselnd schattiert, was das Lesen der Tabelle erleichtert.

## Vollständiges, ausführbares Beispiel

Alle Teile zusammengefügt, hier ein eigenständiges Programm, das Sie kopieren, einfügen und ausführen können.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Get the source data
        DataTable dataTable = GetData();

        // Step 2: Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Build alternating column styles
        int columnCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++)
        {
            Style style = workbook.CreateStyle();
            style.ForegroundColor = (i % 2 == 0)
                ? System.Drawing.Color.LightYellow
                : System.Drawing.Color.LightCyan;
            style.Pattern = BackgroundType.Solid;
            columnStyles[i] = style;
        }

        // Step 4: Import DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // Step 5: Save the file
        string outputPath = @"C:\Temp\StyledTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetData()
    {
        DataTable table = new DataTable("Students");
        table.Columns.Add("Id", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        for (int i = 1; i <= 5; i++)
        {
            table.Rows.Add(i, $"Student {i}", 60 + i * 5);
        }
        return table;
    }
}
```

### Erwartete Ausgabe

* Eine Datei namens **StyledTable.xlsx** im Verzeichnis `C:\Temp\`.  
* Das Arbeitsblatt zeigt drei Spalten (`Id`, `Name`, `Score`) mit wechselnden Hintergrundfarben: Spalten 1 und 3 in *LightYellow*, Spalte 2 in *LightCyan*.  
* Alle Zeilen aus der `DataTable` erscheinen unterhalb der Kopfzeile.

## Häufige Fragen und Sonderfälle

| Frage | Antwort |
|----------|--------|
| *Kann ich andere Farben verwenden?* | Ja. Ersetzen Sie `System.Drawing.Color.LightYellow` und `LightCyan` durch einen beliebigen `System.Drawing.Color`‑Wert. |
| *Was, wenn die DataTable viele Spalten hat?* | Die Schleife erstellt automatisch einen Stil für jede Spalte, sodass das Muster ohne Code‑Änderungen skaliert. |
| *Muss ich das Workbook freigeben?* | Aspose.Cells implementiert `IDisposable`. Wenn Sie das `Workbook` in einem `using`‑Block einbetten, werden Ressourcen sofort freigegeben. |
| *Wie wende ich dieselben wechselnden Farben auf Zeilen statt auf Spalten an?* | Erzeugen Sie ein `Style[]` für Zeilen und rufen Sie `worksheet.Cells.ImportDataTable(..., rowStyles)` auf – Aspose.Cells‑Überladungen unterstützen beides. |
| *Kann ich die Datei direkt in einen Stream schreiben (z. B. für eine Web‑API)?* | Ja. Verwenden Sie `workbook.Save(stream, SaveFormat.Xlsx);` anstelle eines Dateipfads. |

## Tipps aus der Praxis

* **Pro tip:** Zwischenspeichern Sie die Stil‑Objekte, wenn Sie in einem Durchlauf viele Arbeitsblätter erzeugen – das Erstellen eines Stils ist relativ günstig, aber deren Wiederverwendung reduziert den Speicherverbrauch.  
* **Watch out for:** Beim Einsatz von `System.Drawing.Color` auf Nicht‑Windows‑Plattformen fügen Sie das NuGet‑Paket `System.Drawing.Common` hinzu und stellen sicher, dass die Laufzeit GDI+ unterstützt.

## Fazit

Sie wissen jetzt, wie Sie **alternating column colors excel** erreichen, indem Sie eine Excel‑Datei aus einer `DataTable` in C# erstellen, Zellenhintergrundfarben mit Aspose.Cells festlegen und **import datatable to excel** mit einem stilisierten Spalten‑Array durchführen. Dieser Ansatz ist schnell, wartbar und funktioniert mit jeder Datenmenge.

### Nächste Schritte

* Erkunden Sie **set cell background color c#** für bedingte Formatierung (z. B. niedrige Werte hervorheben).  
* Kombinieren Sie diese Technik mit **create excel file from datatable c#**, um mehrseitige Berichte zu erzeugen.  
* Schauen Sie sich die Chart‑API von Aspose.Cells an, um visuelle Zusammenfassungen zum selben Arbeitsbuch hinzuzufügen.

Passen Sie die Farben, das Dateiformat oder die Datenquelle gern an die Bedürfnisse Ihres Projekts an. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Spaltenhintergrund in Excel mit C# festlegen – Vollständige Anleitung](/cells/english/net/excel-colors-and-background-settings/set-column-background-in-excel-with-c-complete-guide/)
- [Hintergrundfarbe in Excel hinzufügen – Wechselnde Zeilenstile in C#](/cells/english/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/)
- [Workbook erstellen C# – DataTable nach Excel mit Stilen importieren](/cells/english/net/excel-data-import-export/create-workbook-c-import-datatable-to-excel-with-styles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}