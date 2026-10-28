---
category: general
date: 2026-09-11
description: Kopieren Sie die Pivot‑Tabelle und exportieren Sie Excel nach PPTX mit
  Aspose.Cells. Erfahren Sie, wie Sie editierbare PPTX‑Dateien erzeugen und die Arbeitsmappe
  in C# als PPTX speichern.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- export excel to pptx
- generate editable pptx
- save workbook as pptx
- export excel sheet pptx
language: de
lastmod: 2026-09-11
og_description: Pivot-Tabelle kopieren und Excel nach PPTX in C# mit Aspose.Cells
  exportieren. Erstellen Sie eine editierbare PPTX und speichern Sie die Arbeitsmappe
  als PPTX mit wenigen Codezeilen.
og_image_alt: Screenshot of copy pivot table code and generated editable PPTX slide
og_title: Pivot‑Tabelle kopieren und Excel nach PPTX exportieren – vollständige C#‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Copy pivot table and export Excel to PPTX using Aspose.Cells. Learn
    to generate editable PPTX and save workbook as PPTX in C#.
  headline: Copy pivot table and export Excel to PPTX with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel
- PPTX
- Pivot Table
title: Pivot‑Tabelle kopieren und Excel nach PPTX mit Aspose.Cells exportieren
url: /de/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopieren einer Pivot‑Tabelle und Export von Excel nach PPTX mit Aspose.Cells

Wenn Sie eine Pivot‑Tabelle von einem Arbeitsblatt in ein anderes kopieren und anschließend die Excel‑Datei in eine PowerPoint‑Präsentation exportieren müssen, zeigt Ihnen dieser Leitfaden, wie das geht. Mit Aspose.Cells können Sie ein bearbeitbares PPTX erzeugen und die Arbeitsmappe mit nur wenigen Zeilen C#‑Code als PPTX speichern.

Das Tutorial behandelt jeden Schritt, der nötig ist, um eine Pivot‑Tabelle zu verschieben, ihre Funktionalität zu erhalten und eine PPTX‑Datei zu erzeugen, bei der Diagramme und Formen editierbar bleiben. Es werden keine externen Werkzeuge benötigt – nur die Aspose.Cells‑Bibliothek und eine .NET‑Entwicklungsumgebung.

## Was Sie erreichen werden

* **Copy pivot table** von einem Quellblatt zu einem Zielblatt, wobei alle Datenverbindungen erhalten bleiben.  
* **Export Excel to PPTX** sodass die resultierende Folie in PowerPoint bearbeitet werden kann.  
* **Generate editable PPTX** bei dem Diagramme, Tabellen und Formen nicht zu Bildern flachgelegt werden.  
* **Save workbook as PPTX** mit demselben Aspose.Cells‑API‑Aufruf.  

### Voraussetzungen

* .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.6+).  
* Aspose.Cells for .NET (NuGet‑Paket `Aspose.Cells`).  
* Grundlegendes Verständnis von C#‑Konsolenanwendungen.  

> **Profi‑Tipp:** Installieren Sie das NuGet‑Paket über die CLI, um sicherzustellen, dass Sie die neueste Version haben:  
> ```bash
> dotnet add package Aspose.Cells
> ```

## So kopieren Sie eine Pivot‑Tabelle zwischen Arbeitsblättern

Der erste Vorgang besteht darin, die Pivot‑Tabelle zu verschieben und dabei ihre Definition zu bewahren. Aspose.Cells stellt eine `CopyRange`‑Methode mit einem `CopyOptions`‑Objekt bereit, das das Flag `CopyPivotTable` enthält.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Load the workbook that contains the source and destination worksheets.
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Identify the worksheets by name.
Worksheet sourceSheet = workbook.Worksheets["Source"];
Worksheet destinationSheet = workbook.Worksheets["Destination"];

// Define the range that encloses the pivot table on the source sheet.
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

// Copy the range to the destination sheet, preserving the pivot table.
destinationSheet.Cells.CopyRange(
    sourceRange,
    0,                     // destination row index
    0,                     // destination column index
    new CopyOptions { CopyPivotTable = true });
```

**Warum das funktioniert:**  
`CopyRange` kopiert Zellendaten, Formatierungen und, wenn `CopyPivotTable` true ist, den Cache und die Metadaten der Pivot‑Tabelle. Der Zielbereich beginnt bei Zelle `A1` (Zeile 0, Spalte 0), Sie können jedoch die Offsets ändern, um die Pivot‑Tabelle an anderer Stelle zu platzieren.

**Typischer Sonderfall:** Wenn das Zielblatt bereits eine Pivot‑Tabelle mit demselben Namen enthält, benennt Aspose.Cells die eingehende Tabelle automatisch um, um einen Namenskonflikt zu vermeiden.

## Exportieren von Excel nach PPTX und Erzeugen eines bearbeitbaren PPTX

Nachdem die Pivot‑Tabelle an ihrem Platz ist, können Sie die gesamte Arbeitsmappe in eine PPTX‑Datei exportieren. Die Klasse `ImageOrPrintOptions` ermöglicht die Angabe von `ExportImageFormat = ImageFormat.Pptx`, wodurch Aspose.Cells die Ausgabe als PowerPoint‑Präsentation statt als Rasterbild behandelt.

```csharp
// Configure export options to produce an editable PPTX.
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ExportImageFormat = ImageFormat.Pptx
};

// Save the workbook as an editable PPTX file.
workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);
```

**Warum das funktioniert:**  
Wenn `ExportImageFormat` auf `Pptx` gesetzt ist, übersetzt Aspose.Cells jedes Arbeitsblatt in eine Folie. Formen, Diagramme und Pivot‑Tabellen werden als native PowerPoint‑Objekte geschrieben, sodass Sie sie in PowerPoint doppelklicken und die zugrunde liegenden Daten bearbeiten können.

**Tipp für große Arbeitsmappen:** Wenn Sie nur einen Teil der Blätter benötigen, entfernen Sie die nicht zu exportierenden Blätter mit `workbook.Worksheets.RemoveAt(index)` bevor Sie `Save` aufrufen. Das reduziert die Größe der PPTX‑Datei.

## Vollständiges, ausführbares Beispiel

Unten finden Sie das komplette Programm, das die vorherigen Schritte zusammenführt. Ersetzen Sie `YOUR_DIRECTORY` durch den tatsächlichen Pfad auf Ihrem Rechner.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Export;

class Example
{
    static void Main()
    {
        // 1. Load the workbook that contains the source and destination worksheets.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Identify the source and destination worksheets.
        Worksheet sourceSheet = workbook.Worksheets["Source"];
        Worksheet destinationSheet = workbook.Worksheets["Destination"];

        // 3. Define the range that holds the pivot table.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // 4. Copy the range, preserving the pivot table.
        destinationSheet.Cells.CopyRange(
            sourceRange,
            0,
            0,
            new CopyOptions { CopyPivotTable = true });

        // 5. Set up export options to generate an editable PPTX.
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
        {
            ExportImageFormat = ImageFormat.Pptx
        };

        // 6. Save the workbook as a PPTX document.
        workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);

        Console.WriteLine("Pivot table copied and workbook exported to PPTX successfully.");
    }
}
```

### Erwartete Ausgabe

Beim Ausführen des Programms wird Folgendes ausgegeben:

```
Pivot table copied and workbook exported to PPTX successfully.
```

Wenn Sie `output.pptx` in Microsoft PowerPoint öffnen, sehen Sie eine Folie, die die kopierte Pivot‑Tabelle als editierbares Diagramm enthält. Ein Doppelklick auf das Diagramm öffnet den PowerPoint‑Diagrammeditor, sodass Sie Reihen, Achsen und Datenbeschriftungen ändern können, ohne zu Excel zurückzukehren.

## Umgang mit typischen Fallstricken

| Problem | Ursache | Lösung |
|---------|---------|--------|
| Pivot‑Tabelle erscheint als statisches Bild | `CopyPivotTable`‑Flag fehlt oder `ExportImageFormat` ist auf `Png` gesetzt | Stellen Sie sicher, dass `CopyPivotTable = true` und `ExportImageFormat = ImageFormat.Pptx`. |
| Zielblatt zeigt leere Zellen | Quellbereich deckt nicht das gesamte Pivot‑Tabellen‑Gebiet ab | Erweitern Sie den Bereich (z. B. `"A1:H30"`), um alle Pivot‑Felder einzuschließen. |
| Exportiertes PPTX ist riesig | Unnötige Arbeitsblätter sind enthalten | Entfernen Sie unerwünschte Blätter vor dem Aufruf von `Save`. |
| PowerPoint kann das Diagramm nicht bearbeiten | Verwendung einer älteren Aspose.Cells‑Version ohne PPTX‑Unterstützung | Aktualisieren Sie auf die neueste Aspose.Cells‑Version (siehe Release‑Notes). |

## Nächste Schritte und verwandte Themen

* **Export Excel sheet to PPTX with custom slide layouts** – erkunden Sie `WorksheetToPdfConverter` für feinere Kontrolle über das Aussehen der Folien.  
* **Export Excel to PDF** – ersetzen Sie `ImageFormat.Pptx` durch `ImageFormat.Pdf`, um stattdessen ein PDF zu erzeugen.  
* **Programmatically modify PPTX after export** – nutzen Sie die `Aspose.Slides`‑Bibliothek, um Animationen oder Sprecher‑Notizen hinzuzufügen.  

Durch das Beherrschen von **copy pivot table**, **export excel to pptx** und **generate editable pptx** können Sie End‑zu‑End‑Reporting‑Pipelines erstellen, die Daten aus Tabellenkalkulationen direkt in Präsentationsdecks überführen, ohne die Editierbarkeit zu verlieren.

---


## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Create a Pivot Table in Excel Using Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}