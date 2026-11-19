---
category: general
date: 2026-11-19
description: Erfahren Sie, wie Sie mit CopyOptions in Aspose.Cells einen Bereich kopieren
  und dabei Formatierungen sowie Pivot-Tabellen beibehalten, während Sie einen Excel‑Bereich
  mit Formatierung kopieren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range using copyoptions
- copy excel range with formatting
- Aspose.Cells copy range
- preserve pivot tables Aspose
- Excel automation C#
language: de
lastmod: 2026-11-19
og_description: Das Kopieren von Bereichen mit CopyOptions in Aspose.Cells ermöglicht
  das Duplizieren von Excel‑Daten bei vollständiger Formatierung und erhaltenen Pivot‑Tabellen,
  wodurch eine zuverlässige Arbeitsmappenbearbeitung gewährleistet wird.
og_image_alt: Screenshot of C# code that copies an Excel range using Aspose.Cells
  CopyOptions
og_title: Bereich mit CopyOptions in Aspose.Cells kopieren – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  headline: How to copy range using CopyOptions in Aspose.Cells
  type: TechArticle
- description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  name: How to copy range using CopyOptions in Aspose.Cells
  steps:
  - name: Why `CopyOptions` matters
    text: '* **Performance** – The library performs a single internal operation rather
      than copying cells one‑by‑one. * **Accuracy** – All visual aspects (fonts, colors,
      borders) survive the move, which eliminates visual drift in generated reports.
      * **Reliability** – Pivot tables remain functional because the'
  - name: What if the destination area overlaps the source?
    text: 'Aspose.Cells throws an `ArgumentException`. To avoid this, calculate a
      destination that does not intersect the source, or copy to a different worksheet:'
  - name: How to copy between different workbooks?
    text: 'Create a second `Workbook` instance for the target file and use the same
      `CopyOptions` object:'
  - name: Does `CopyOptions` also copy merged cells?
    text: Yes. The `CopyStyle` flag includes merged‑cell information. If you need
      finer control, set `options.CopyMergedCells = true` (available in newer versions).
  - name: What about large ranges (thousands of rows)?
    text: The operation is memory‑efficient, but you may want to increase the `WorkbookSettings`
      `MemorySetting` to `MemorySetting.MemoryPreference` for very large files.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Wie man einen Bereich mit CopyOptions in Aspose.Cells kopiert
url: /de/net/range-management/how-to-copy-range-using-copyoptions-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man einen Bereich mit CopyOptions in Aspose.Cells kopiert

Wenn Sie **einen Bereich mit CopyOptions kopieren** möchten, zeigt Ihnen diese Anleitung genau, wie Sie einen Zellblock duplizieren, wobei alle Formatierungen und eingebetteten Pivot‑Tabellen erhalten bleiben. Viele Entwickler haben Schwierigkeiten, den Stil beim Verschieben von Daten zwischen Arbeitsblättern zu bewahren – die Klasse `CopyOptions` löst dieses Problem ohne zusätzliche manuelle Schritte.

In diesem Tutorial lernen Sie:

* Quell‑ und Zielbereiche in einer Excel‑Arbeitsmappe zu definieren.  
* `CopyOptions` zu verwenden, um Zellformatierung, Spaltenbreiten und Pivot‑Tabellen beizubehalten.  
* Das Ergebnis in einer neuen Datei zu speichern, die für nachgelagerte Verarbeitung bereitsteht.

Das Beispiel funktioniert mit jeder `.xlsx`‑Datei und erfordert nur die Aspose.Cells‑Bibliothek für .NET.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

* .NET 6.0 oder höher installiert.  
* Eine gültige Aspose.Cells‑für‑.NET‑Lizenz (oder einen kostenlosen Evaluierungsschlüssel).  
* Visual Studio 2022 oder eine andere C#‑IDE Ihrer Wahl.  

Keine zusätzlichen NuGet‑Pakete sind über `Aspose.Cells` hinaus erforderlich.

## Schritt 1: Projekt einrichten und Namespaces importieren

Erstellen Sie eine neue Konsolenanwendung und fügen Sie den Aspose.Cells‑Verweis hinzu:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Your code will go here
        }
    }
}
```

Die Direktive `using Aspose.Cells;` gibt Ihnen Zugriff auf `Workbook`, `CellArea` und `CopyOptions`.

## Schritt 2: Die Arbeitsmappe laden, die Sie ändern möchten

```csharp
// Step 2: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`Workbook` repräsentiert die gesamte Excel‑Datei. Ersetzen Sie `YOUR_DIRECTORY` durch den Ordner, der Ihre Quelldatei enthält.

## Schritt 3: Quell‑ und Zielbereiche definieren

```csharp
// Step 3: Define the source range (A1:H30)
CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");

// Step 3b: Define the destination range (A35:H64)
CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");
```

`CellArea.CreateCellArea` erstellt ein rechteckiges Gebiet basierend auf den Adressen der oberen linken und unteren rechten Zelle. Passen Sie die Koordinaten an die Größe des zu kopierenden Blocks an.

## Schritt 4: Den Bereich kopieren und dabei Formatierung sowie Pivot‑Tabellen erhalten

```csharp
// Step 4: Copy the range using CopyOptions
CopyOptions options = new CopyOptions
{
    // Preserve all cell styles, number formats, and column widths
    CopyStyle = true,
    // Keep formulas unchanged (they will still reference the original sheet)
    CopyFormula = true,
    // Preserve any pivot tables that intersect the copied area
    CopyPivotTables = true,
    // Retain data validation and conditional formatting
    CopyDataValidation = true,
    CopyConditionalFormatting = true
};

workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
```

Das `CopyOptions`‑Objekt teilt Aspose.Cells genau mit, was beibehalten werden soll. Das Setzen von `CopyPivotTables = true` ist der Schlüssel, um **einen Bereich mit CopyOptions zu kopieren**, wenn Ihre Quelle Pivot‑Tabellen enthält. Die anderen Flags sorgen dafür, dass **Excel‑Bereich mit Formatierung kopiert** wird – es ist kein zusätzlicher Code nötig, um nach dem Kopieren Stile erneut anzuwenden.

### Warum `CopyOptions` wichtig ist

* **Performance** – Die Bibliothek führt einen einzigen internen Vorgang aus, anstatt Zellen einzeln zu kopieren.  
* **Genauigkeit** – Alle visuellen Aspekte (Schriftarten, Farben, Rahmen) bleiben erhalten, wodurch visuelle Abweichungen in generierten Berichten vermieden werden.  
* **Zuverlässigkeit** – Pivot‑Tabellen bleiben funktionsfähig, weil ihr Cache und ihre Quellverweise dupliziert werden.

## Schritt 5: Die geänderte Arbeitsmappe speichern

```csharp
// Step 5: Save the workbook with the copied range
workbook.Save("YOUR_DIRECTORY/output.xlsx");
Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
```

Nach dem Aufruf von `Save` enthält die Datei `output.xlsx` die ursprünglichen Daten plus den duplizierten Block am Zielort, komplett mit Formatierung und Pivot‑Tabellen.

## Vollständiger Quellcode zum Nachschlagen

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // Define source and destination ranges
            CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");
            CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");

            // Configure copy options to preserve everything
            CopyOptions options = new CopyOptions
            {
                CopyStyle = true,
                CopyFormula = true,
                CopyPivotTables = true,
                CopyDataValidation = true,
                CopyConditionalFormatting = true
            };

            // Perform the copy operation
            workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);

            // Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");
            Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
        }
    }
}
```

Beim Ausführen dieses Programms wird ausgegeben:

```
Range copied successfully. Output saved to output.xlsx
```

Öffnen Sie `output.xlsx` in Excel – Sie sehen den Block A1:H30, der an A35:H64 dupliziert wurde, mit allen Zellfarben, Rahmen, Zahlenformaten und etwaigen Pivot‑Tabellen unverändert.

## Häufige Fragen und Sonderfälle

### Was, wenn sich der Zielbereich mit dem Quellbereich überschneidet?

Aspose.Cells wirft eine `ArgumentException`. Vermeiden Sie dies, indem Sie ein Ziel berechnen, das nicht mit der Quelle schneidet, oder in ein anderes Arbeitsblatt kopieren:

```csharp
Worksheet destSheet = workbook.Worksheets.Add("CopySheet");
destSheet.Cells.CopyRange(sourceRange, CellArea.CreateCellArea("A1", "H30"), options);
```

### Wie kopiert man zwischen verschiedenen Arbeitsmappen?

Erstellen Sie eine zweite `Workbook`‑Instanz für die Zieldatei und verwenden Sie dasselbe `CopyOptions`‑Objekt:

```csharp
Workbook target = new Workbook();
target.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
target.Save("target.xlsx");
```

### Kopiert `CopyOptions` auch zusammengeführte Zellen?

Ja. Das Flag `CopyStyle` beinhaltet Informationen zu zusammengeführten Zellen. Wenn Sie feinere Kontrolle benötigen, setzen Sie `options.CopyMergedCells = true` (verfügbar in neueren Versionen).

### Was ist bei sehr großen Bereichen (tausende Zeilen) zu beachten?

Der Vorgang ist speichereffizient, aber Sie können `WorkbookSettings.MemorySetting` auf `MemorySetting.MemoryPreference` setzen, wenn Sie mit sehr großen Dateien arbeiten.

## Profi‑Tipps

* **Verwenden Sie dieselbe `CopyOptions`‑Instanz** für mehrere Kopiervorgänge – das reduziert den Overhead bei der Objektallokation.  
* **Validieren Sie Bereiche** vor dem Kopieren: `if (!CellArea.IsValid(sourceRange) || !CellArea.IsValid(destinationRange))` hilft, tipbezogene Fehler früh zu erkennen.  
* **Deaktivieren Sie die Berechnung** (`workbook.Settings.CalcMode = CalculationMode.Manual`) während des Kopierens großer Datenmengen, um den Vorgang zu beschleunigen, und rufen Sie anschließend `workbook.CalculateFormula()` auf, falls Sie aktualisierte Ergebnisse benötigen.

## Fazit

Sie wissen jetzt, wie man **einen Bereich mit CopyOptions in Aspose.Cells kopiert** und dabei ein vollständiges **Excel‑Bereich mit Formatierung kopiert**, während Pivot‑Tabellen und andere erweiterte Features erhalten bleiben. Dieser Ansatz eliminiert manuelle Stil‑Wiederanwendungen und sorgt dafür, dass Ihre Excel‑Automatisierung robust und wartbar bleibt.

Nächste Schritte, die Sie erkunden können:

* `CopyOptions` verwenden, um ganze Arbeitsblätter zu duplizieren.  
* Die Kopier‑Operation mit `WorksheetCollection.AddCopy` für template‑basierte Berichtserstellung kombinieren.  
* Den Code in eine ASP.NET Core API integrieren, um Excel‑Transformationen „on the fly“ bereitzustellen.

Probieren Sie verschiedene Quell‑/Zielkoordinaten aus und teilen Sie Ihre Ergebnisse in den Kommentaren!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren Projekten erkunden können.

- [Excel Aspose Cells .NET Bereichsdaten kopieren](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells .NET Bereichsdaten kopieren](/cells/french/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells .NET Bereichsdaten kopieren](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}