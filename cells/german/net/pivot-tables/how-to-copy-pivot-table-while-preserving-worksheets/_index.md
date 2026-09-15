---
category: general
date: 2026-09-15
description: Erfahren Sie, wie Sie Pivot‑Tabellen kopieren, ein Arbeitsblatt mit Pivot
  kopieren und die Arbeitsmappe als PPTX mit Aspose.Cells in C# speichern. Vollständige
  Schritt‑für‑Schritt‑Anleitung.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy worksheet with pivot
- save workbook as pptx
language: de
lastmod: 2026-09-15
og_description: Wie man Pivot‑Tabellen kopiert, ein Arbeitsblatt mit Pivot kopiert
  und die Arbeitsmappe als PPTX mit Aspose.Cells speichert. Folgen Sie den vollständigen,
  ausführbaren C#‑Beispielen.
og_image_alt: Screenshot showing how to copy pivot table in a C# code editor
og_title: Wie man Pivot-Tabellen kopiert und Arbeitsblätter exportiert – vollständige
  C#‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  headline: How to copy pivot table while preserving worksheets
  type: TechArticle
- description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  name: How to copy pivot table while preserving worksheets
  steps:
  - name: – Load the source workbook that holds the pivot table
    text: '```csharp // Load the workbook that contains the pivot table you want to
      copy Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx"); ```'
  - name: – Create an empty destination workbook
    text: '```csharp // Create a new, empty workbook that will receive the copied
      data Workbook destinationWorkbook = new Workbook(); ```'
  - name: – Copy the rows that include the pivot table
    text: '```csharp // Copy rows 0‑19 (A1:G20) from the first worksheet of the source
      sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20); ```'
  - name: – Copy the columns that contain the pivot table
    text: '```csharp // Copy columns 0‑6 (A‑G) from the same worksheet sourceWorkbook.Worksheets[0].Cells.CopyColumns(0,
      0, 7); ```'
  - name: – Transfer the prepared sheet into the destination workbook
    text: '```csharp // Move the fully prepared worksheet into the destination workbook
      sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]); ```'
  - name: – Save the result – the pivot table remains intact
    text: '```csharp // Save the destination workbook; the pivot table works exactly
      like the original destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
      ```'
  - name: – Load the workbook that includes the textbox
    text: '```csharp // Load the Excel file that contains an editable textbox shape
      Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
      ```'
  - name: – Configure PPTX save options
    text: '```csharp // Create PPTX save options and enable the editable textbox feature
      (available from v25.11) PptxSaveOptions pptxOptions = new PptxSaveOptions {
      ExportEditableTextBox = true }; ```'
  - name: – Save the workbook as PPTX
    text: '```csharp // Export the workbook to a PPTX file; the textbox stays editable
      in PowerPoint workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
      ```'
  - name: – Prepare the SmartMarkerProcessor
    text: '```csharp // Initialise the processor that will fill Smart Markers SmartMarkerProcessor
      smartMarkerProcessor = new SmartMarkerProcessor(); ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Wie man eine Pivot‑Tabelle kopiert und dabei Arbeitsblätter beibehält
url: /de/net/pivot-tables/how-to-copy-pivot-table-while-preserving-worksheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Pivot-Tabellen kopiert und Arbeitsblätter beibehält

Wenn Sie **how to copy pivot table** von einer Arbeitsmappe in eine andere kopieren müssen, ohne den zugrunde liegenden Pivot-Cache zu verlieren, bietet dieser Leitfaden eine sofort einsatzbereite Lösung. Sie sehen außerdem, wie man **copy worksheet with pivot** und **save workbook as pptx** verwendet, während editierbare Textfelder erhalten bleiben. Alle Beispiele verwenden die neueste Aspose.Cells für .NET, sodass Sie den Code in jedes C#‑Projekt einfügen und sofortige Ergebnisse sehen können.

Die programmgesteuerte Arbeit mit Excel-Dateien beinhaltet häufig das Verschieben von Daten zwischen Arbeitsmappen, das Exportieren in Präsentationen oder das Einfügen komplexer Smart Marker. Die drei Code‑Snippets unten decken diese gängigen Szenarien ab und erklären, warum jeder Schritt wichtig ist.

## Voraussetzungen

* .NET 6.0 oder höher installiert  
* Aspose.Cells für .NET (Version 25.11 oder neuer) im Projekt referenziert  
* Ein Ordner namens `YOUR_DIRECTORY`, aus dem die Beispieldateien gelesen und in den sie geschrieben werden  

Keine zusätzlichen NuGet‑Pakete sind erforderlich.

---

## Pivot-Tabelle mit Aspose.Cells kopieren

Das Kopieren eines Bereichs, der eine Pivot‑Tabelle enthält, während der Pivot‑Cache erhalten bleibt, ist ein häufiges Bedürfnis. Die folgenden Schritte zeigen die genaue Reihenfolge, die Sie benötigen.

### Schritt 1 – Laden der Quellarbeitsmappe, die die Pivot‑Tabelle enthält

```csharp
// Load the workbook that contains the pivot table you want to copy
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
```

*Warum*: Aspose.Cells liest die Arbeitsmappe in den Speicher und gibt Ihnen Zugriff auf Arbeitsblätter, Zellen und Pivot‑Tabellen.

### Schritt 2 – Erstellen einer leeren Zielarbeitsmappe

```csharp
// Create a new, empty workbook that will receive the copied data
Workbook destinationWorkbook = new Workbook();
```

*Warum*: Das Beginnen mit einer leeren Arbeitsmappe stellt sicher, dass keine versteckten Stile oder benannten Bereiche den Kopiervorgang beeinträchtigen.

### Schritt 3 – Kopieren der Zeilen, die die Pivot‑Tabelle enthalten

```csharp
// Copy rows 0‑19 (A1:G20) from the first worksheet of the source
sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20);
```

*Warum*: `CopyRows` kopiert die rohen Zellwerte, Formate und zugrunde liegenden Pivot‑Cache‑Verweise. Der Bereich muss die gesamte Pivot‑Tabellenfläche umfassen.

### Schritt 4 – Kopieren der Spalten, die die Pivot‑Tabelle enthalten

```csharp
// Copy columns 0‑6 (A‑G) from the same worksheet
sourceWorkbook.Worksheets[0].Cells.CopyColumns(0, 0, 7);
```

*Warum*: Pivot‑Tabellen erstrecken sich über Zeilen und Spalten; das Kopieren der Spalten stellt sicher, dass das gesamte Tabellenlayout erhalten bleibt.

### Schritt 5 – Übertragen des vorbereiteten Blatts in die Zielarbeitsmappe

```csharp
// Move the fully prepared worksheet into the destination workbook
sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]);
```

*Warum*: Die Methode `Copy` dupliziert das Arbeitsblatt, einschließlich des Pivot‑Caches, sodass die Zielarbeitsmappe eine identische Pivot‑Tabelle anzeigt.

### Schritt 6 – Speichern des Ergebnisses – die Pivot‑Tabelle bleibt unverändert

```csharp
// Save the destination workbook; the pivot table works exactly like the original
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Warum*: Das Persistieren der Arbeitsmappe schreibt alle internen Strukturen und garantiert, dass die Pivot‑Tabelle später aktualisiert werden kann.

**Pro‑Tipp**: Nach dem Kopieren können Sie `destinationWorkbook.Worksheets[0].PivotTables[0].Refresh()` aufrufen, um die Daten zu aktualisieren, falls sich die Quelldaten geändert haben.

---

## Arbeitsblatt mit Pivot kopieren – eine kompakte Alternative

Wenn Sie einfach ein ganzes Arbeitsblatt, das bereits eine Pivot‑Tabelle enthält, duplizieren müssen, können Sie die Zeilen‑/Spalten‑Kopierschritte überspringen und die `Copy`‑Methode auf Arbeitsblattebene direkt verwenden.

```csharp
// Load source workbook
Workbook src = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

// Create destination workbook
Workbook dst = new Workbook();

// Copy the first worksheet (including its pivot table) to the destination
src.Worksheets[0].Copy(dst.Worksheets[0]);

// Save the new file
dst.Save("YOUR_DIRECTORY/WorksheetCopy.xlsx");
```

Dieser Ansatz ist nützlich, wenn das Arbeitsblatt keine zusätzlichen Daten außerhalb des Pivot‑Bereichs enthält. Der Vorgang **copy worksheet with pivot** bewahrt automatisch alle Formatierungen, benannten Bereiche und Pivot‑Caches.

---

## Arbeitsmappe als PPTX mit editierbaren Textfeldern speichern

Das Exportieren eines Excel‑Blatts, das ein editierbares Textfeld enthält, nach PowerPoint kann für Reporting‑Dashboards erforderlich sein. Der untenstehende Code zeigt **save workbook as pptx**, während das Textfeld editierbar bleibt.

### Schritt 1 – Laden der Arbeitsmappe, die das Textfeld enthält

```csharp
// Load the Excel file that contains an editable textbox shape
Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
```

### Schritt 2 – Konfigurieren der PPTX‑Speicheroptionen

```csharp
// Create PPTX save options and enable the editable textbox feature (available from v25.11)
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableTextBox = true
};
```

*Warum*: Das Setzen von `ExportEditableTextBox` weist Aspose.Cells an, das Excel‑Textfeld in eine PowerPoint‑Form zu übersetzen, die nach dem Export editierbar bleibt.

### Schritt 3 – Speichern der Arbeitsmappe als PPTX

```csharp
// Export the workbook to a PPTX file; the textbox stays editable in PowerPoint
workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
```

**Erwartetes Ergebnis**: Öffnen Sie `Result.pptx` in PowerPoint, wählen Sie das Textfeld aus und bearbeiten Sie dessen Inhalt wie jede native Form.

**Häufige Frage**: *Was, wenn ich das Textfeld gesperrt halten muss?*  
Setzen Sie `pptxOptions.ExportEditableTextBox = false`; die Form wird stattdessen in ein statisches Bild umgewandelt.

---

## Export eines Smart Markers, das ein JSON‑Array als Einzelzellenwert enthält

Smart Marker ermöglichen das Befüllen von Excel‑Vorlagen mit komplexen Datenstrukturen. Unten steht ein vollständiges Beispiel, das die **how to copy pivot table**‑artige Datenverarbeitung demonstriert, während ein JSON‑Array in eine einzelne Zelle eingefügt wird.

### Schritt 1 – Vorbereiten des SmartMarkerProcessor

```csharp
// Initialise the processor that will fill Smart Markers
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
```

### Schritt 2 – Einfügen eines Smart Markers in Zelle A1

```csharp
// The marker ${Orders:ArrayAsSingle} tells the processor to write the whole array into one cell
Workbook workbook = new Workbook();
workbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
```

### Schritt 3 – Definieren der Datenquelle mit einem JSON‑ähnlichen Array

```csharp
// Anonymous object that mimics a JSON array
var dataModel = new { Orders = new[] { "A", "B", "C" } };
```

### Schritt 4 – Verarbeiten der Arbeitsmappe

```csharp
// Fill the Smart Marker with the array data; the array becomes a comma‑separated string
smartMarkerProcessor.Process(workbook, dataModel);
```

### Schritt 5 – Speichern der resultierenden Arbeitsmappe

```csharp
// Persist the workbook; cell A1 now contains "A,B,C"
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
```

**Ergebnis‑Verifizierung**: Öffnen Sie `JsonSingleCell.xlsx` und bestätigen Sie, dass Zelle A1 `A,B,C` anzeigt. Dies zeigt, wie man eine Sammlung als Einzelzellenwert behandelt, ein Muster, das häufig beim Export von Daten für nachgelagerte Systeme benötigt wird.

---

## Vollständiges funktionierendes Beispiel

Unten steht ein einzelnes Programm, das die drei Szenarien kombiniert. Sie können den Code in eine Konsolen‑App kopieren, die Dateipfade anpassen und ausführen, um alle drei Ausgaben zu sehen.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1. How to copy pivot table (preserve pivot cache)
        // -------------------------------------------------
        Workbook srcPivot = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Workbook dstPivot = new Workbook();
        srcPivot.Worksheets[0].Cells.CopyRows(0, 0, 20);
        srcPivot.Worksheets[0].Cells.CopyColumns(0, 0, 7);
        srcPivot.Worksheets[0].Copy(dstPivot.Worksheets[0]);
        dstPivot.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");

        // -------------------------------------------------
        // 2. Save workbook as PPTX with editable textbox
        // -------------------------------------------------
        Workbook txtWorkbook = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
        PptxSaveOptions pptxOpts = new PptxSaveOptions { ExportEditableTextBox = true };
        txtWorkbook.Save("YOUR_DIRECTORY/Result.pptx", pptxOpts);

        // -------------------------------------------------
        // 3. Export Smart Marker containing a JSON array
        // -------------------------------------------------
        SmartMarkerProcessor smProcessor = new SmartMarkerProcessor();
        Workbook smWorkbook = new Workbook();
        smWorkbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
        var model = new { Orders = new[] { "A", "B", "C" } };
        smProcessor.Process(smWorkbook, model);
        smWorkbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
    }
}
```

Die Ausführung dieses Programms erzeugt:

* `CopyWithPivot.xlsx` – eine perfekte Kopie der ursprünglichen Pivot‑Tabelle.  
* `Result.pptx` – eine PowerPoint‑Folie mit einem editierbaren Textfeld.  
* `JsonSingleCell.xlsx` – ein Blatt, bei dem das JSON‑Array in einer einzelnen Zelle erscheint.

---

## Fazit

Sie wissen jetzt, wie man **how to copy pivot table** sicher kopiert, wie man **copy worksheet with pivot** in einem einzigen Aufruf dupliziert und wie man **save workbook as pptx** speichert, während editierbare Textfelder erhalten bleiben. Diese Muster decken die häufigsten Excel‑zu‑PowerPoint‑ und Excel‑zu‑JSON‑Workflows ab, denen Sie in Unternehmens‑Automatisierungsprojekten begegnen.

Als Nächstes sollten Sie erkunden:

* Aktualisieren kopierter Pivot‑Tabellen programmgesteuert (`PivotTable.Refresh()`)  
* Exportieren in andere Formate wie PDF oder HTML (`PdfSaveOptions`, `HtmlSaveOptions`)  
* Verwenden erweiterter Smart‑Marker‑Optionen wie benutzerdefinierte Funktionen oder bedingte Formatierung  

Fühlen Sie sich frei, mit verschiedenen Bereichen, mehreren Arbeitsblättern oder größeren JSON‑Strukturen zu experimentieren. Die Aspose.Cells‑API bietet Ihnen feinkörnige Kontrolle, sodass Sie diese Beispiele an jedes reale Szenario anpassen können. Viel Spaß beim Programmieren!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step‑By‑Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}