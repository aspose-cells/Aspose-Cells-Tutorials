---
category: general
date: 2026-09-18
description: Erstellen Sie PowerPoint aus Excel mit Aspose.Cells – Pivot‑Tabellen
  kopieren, Bereiche exportieren und als PPTX in wenigen Zeilen C#‑Code speichern.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create powerpoint from excel
- how to copy pivot table
- copy range between workbooks
- how to export excel to pptx
- save workbook as pptx
language: de
lastmod: 2026-09-18
og_description: Erstellen Sie schnell PowerPoint-Präsentationen aus Excel. Erfahren
  Sie, wie Sie Pivot‑Tabellen kopieren, Bereiche exportieren und eine Arbeitsmappe
  mit Aspose.Cells als PPTX speichern.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel data
og_title: PowerPoint aus Excel mit Aspose.Cells erstellen – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  headline: How to create PowerPoint from Excel using Aspose.Cells
  type: TechArticle
- description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  name: How to create PowerPoint from Excel using Aspose.Cells
  steps:
  - name: Load the source workbook and define the range
    text: You must load the workbook that holds the source data and the pivot table.
      Selecting a precise range ensures that only the needed cells are transferred,
      which keeps the resulting slide lightweight.
  - name: Prepare the destination workbook
    text: Aspose.Cells treats a PowerPoint slide as a workbook when you save it in
      PPTX format. Creating a fresh workbook gives you a clean canvas for the copied
      range.
  - name: Copy the range while preserving the pivot table
    text: The `CopyRange` method accepts a `PasteOptions` object. Setting `CopyPivotTables
      = true` tells Aspose.Cells to keep the pivot table structure intact, not just
      the rendered values.
  - name: Save the workbook as a PowerPoint file
    text: Finally, export the workbook to PPTX format. The `SaveFormat.Pptx` flag
      tells Aspose.Cells to write the worksheet as a PowerPoint slide.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel to PowerPoint
title: Wie man PowerPoint aus Excel mit Aspose.Cells erstellt
url: /de/net/converting-excel-files-to-other-formats/how-to-create-powerpoint-from-excel-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man PowerPoint aus Excel mit Aspose.Cells erstellt

Wenn Sie PowerPoint aus Excel erstellen müssen, zeigt Ihnen diese Anleitung eine kompakte End‑zu‑End‑Lösung. Sie sehen, wie Sie eine Pivot‑Tabelle kopieren, einen ausgewählten Bereich exportieren und das Ergebnis mit nur wenigen Zeilen C# als PPTX‑Datei speichern.

Das direkte Erzeugen einer Präsentation aus Tabellendaten eliminiert den manuellen Kopier‑Einfügen‑Schritt, der Reporting‑Workflows verlangsamt. Das Tutorial deckt alles ab, was Sie benötigen – von der Projekt‑Einrichtung bis zur finalen PPTX‑Datei – und funktioniert mit dem neuesten Aspose.Cells für .NET.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

* **Aspose.Cells für .NET** (Version 23.12 oder neuer). Installieren Sie es via NuGet: `Install-Package Aspose.Cells`.
* Eine **.NET 6+** Entwicklungsumgebung (Visual Studio 2022 oder VS Code funktioniert).
* Eine Excel‑Arbeitsmappe (`Source.xlsx`), die die Daten und die Pivot‑Tabelle enthält, die Sie wiederverwenden möchten.
* Schreibrechte für den Ausgabepfad.

Weitere Drittanbieter‑Bibliotheken sind nicht erforderlich.

## PowerPoint aus Excel erstellen – Schritt für Schritt

Der Prozess besteht aus vier logischen Schritten, die direkt dem Code‑Beispiel entsprechen, das Sie später sehen werden.

### Schritt 1: Laden der Quell‑Arbeitsmappe und Definieren des Bereichs

Sie müssen die Arbeitsmappe laden, die die Quelldaten und die Pivot‑Tabelle enthält. Die Auswahl eines genauen Bereichs stellt sicher, dass nur die benötigten Zellen übertragen werden, wodurch die resultierende Folie leicht bleibt.

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// Select the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that contains the pivot table and surrounding data
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

**Warum das wichtig ist:**  
`CreateRange` erzeugt ein `Range`‑Objekt, das als Ganzes kopiert werden kann. Durch die Begrenzung des Bereichs auf `A1:G20` vermeiden Sie das Einbeziehen nicht verwandter Zellen, die sonst die PowerPoint‑Datei aufblähen könnten.

### Schritt 2: Vorbereiten der Ziel‑Arbeitsmappe

Aspose.Cells behandelt eine PowerPoint‑Folie als Arbeitsmappe, wenn Sie sie im PPTX‑Format speichern. Das Erstellen einer neuen Arbeitsmappe gibt Ihnen eine saubere Leinwand für den kopierten Bereich.

```csharp
// Create a new empty workbook that will become the PowerPoint slide
Workbook destinationWorkbook = new Workbook();

// Use the first worksheet of the new workbook
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

**Tipp:** Wenn Sie mehrere Folien benötigen, können Sie zusätzliche Arbeitsblätter hinzufügen und später jedes als separate PPTX‑Datei speichern.

### Schritt 3: Kopieren des Bereichs unter Beibehaltung der Pivot‑Tabelle

Die Methode `CopyRange` akzeptiert ein `PasteOptions`‑Objekt. Das Setzen von `CopyPivotTables = true` weist Aspose.Cells an, die Pivot‑Tabellenstruktur intakt zu lassen, nicht nur die gerenderten Werte.

```csharp
// Copy the defined range, preserving the pivot table definition
destinationSheet.Cells.CopyRange(
    sourceRange,
    new PasteOptions { CopyPivotTables = true });
```

**Wie es funktioniert:**  
Wenn `CopyPivotTables` true ist, erhält das Ziel‑Sheet sowohl die Quelldaten als auch den Pivot‑Cache. Das bedeutet, dass die Pivot‑Tabelle vollständig funktionsfähig bleibt und später bei Änderungen der Quelldaten aktualisiert werden kann.

### Schritt 4: Speichern der Arbeitsmappe als PowerPoint‑Datei

Abschließend exportieren Sie die Arbeitsmappe ins PPTX‑Format. Das Flag `SaveFormat.Pptx` teilt Aspose.Cells mit, das Arbeitsblatt als PowerPoint‑Folie zu schreiben.

```csharp
// Save the destination workbook as a PowerPoint presentation
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);
```

**Ergebnis:**  
`CopyWithPivot.pptx` öffnet sich in Microsoft PowerPoint (oder einem kompatiblen Viewer) mit einer einzigen Folie, die den kopierten Bereich anzeigt, einschließlich einer Live‑Pivot‑Tabelle, die in PowerPoint interagierbar ist.

## Vollständiges ausführbares Beispiel

Unten finden Sie das komplette Programm, das Sie in ein neues Konsolen‑Projekt einfügen und sofort ausführen können.

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook and select the range containing the pivot table
            Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
            Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
            Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

            // 2️⃣ Create a fresh workbook that will become the PowerPoint slide
            Workbook destinationWorkbook = new Workbook();
            Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

            // 3️⃣ Copy the range, preserving the pivot table definition
            destinationSheet.Cells.CopyRange(
                sourceRange,
                new PasteOptions { CopyPivotTables = true });

            // 4️⃣ Export the workbook as a PPTX file
            destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);

            Console.WriteLine("PowerPoint file created successfully.");
        }
    }
}
```

**Erwartete Ausgabe:**  
Beim Ausführen des Programms wird “PowerPoint file created successfully.” ausgegeben und eine Datei namens `CopyWithPivot.pptx` erzeugt. Öffnet man die Datei in PowerPoint, sieht man eine einzelne Folie, auf der der kopierte Excel‑Bereich exakt wie im Quell‑Arbeitsblatt erscheint, mit einer aktiven Pivot‑Tabelle, die innerhalb von PowerPoint aktualisiert werden kann.

## Häufige Varianten und Sonderfälle

| Situation | Was zu ändern ist |
|-----------|-------------------|
| **Mehrere Pivot‑Tabellen** | Definieren Sie separate `Range`‑Objekte für jede Tabelle und rufen Sie `CopyRange` für jede auf, oder kopieren Sie das gesamte Blatt, wenn sie dieselbe Datenquelle nutzen. |
| **Große Datensätze** | Erweitern Sie den Bereich (z. B. `"A1:Z5000"`). Erwägen Sie, `PasteOptions.CompressData = true` zu aktivieren, um die PPTX‑Größe zu reduzieren. |
| **Unterschiedliche Folien‑Layouts** | Nach dem Speichern als PPTX öffnen Sie die Datei in PowerPoint und wenden ein benutzerdefiniertes Layout oder Design an; die Daten bleiben editierbar. |
| **Speichern in einen Stream** | Verwenden Sie `destinationWorkbook.Save(stream, SaveFormat.Pptx)`, wenn Sie das PPTX über eine Web‑API zurückgeben müssen. |
| **Beibehaltung der Zellformatierung** | Setzen Sie `PasteOptions.PasteType = PasteType.All`, um Schriftarten, Farben und Rahmen zu erhalten. |

**Pro‑Tipp:** Überprüfen Sie immer, ob der Zielordner existiert, bevor Sie `Save` aufrufen. Fehlt der Ordner, wirft `Save` eine `DirectoryNotFoundException`.

## Fazit

Sie wissen jetzt, wie Sie PowerPoint aus Excel erstellen, eine Pivot‑Tabelle kopieren und das Ergebnis als PPTX‑Datei mit Aspose.Cells exportieren. Die Schritte – Laden der Quell‑Arbeitsmappe, Definieren eines Bereichs, Kopieren mit `CopyPivotTables` und Speichern als PPTX – decken den gesamten Workflow zuverlässig und produktionsreif ab.

Als Nächstes können Sie **wie man Excel nach PPTX exportiert** für mehrere Arbeitsblätter erkunden oder **wie man Bereiche zwischen Arbeitsmappen kopiert**, wenn Sie Daten aus mehreren Quellen zusammenführen müssen, bevor Sie das Präsentationsdeck erzeugen. Beide Themen bauen auf derselben API‑Oberfläche auf und lassen sich kombinieren, um komplexe Reporting‑Pipelines zu automatisieren.

Viel Spaß beim Coden und beim Verwandeln Ihrer Tabellen in professionelle Präsentationen!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man Pivot‑Tabellen in C# kopiert – Excel nach PPTX konvertieren, Bereich kopieren & Textfeld erstellen](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Neue Arbeitsmappe erstellen – Wie man ein Arbeitsblatt mit einer Pivot‑Tabelle kopiert](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Wie man Excel‑Dateien mit Aspose.Cells für .NET erstellt und speichert: Ein vollständiger Leitfaden](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}