---
category: general
date: 2026-10-26
description: Druckbereich festlegen und ein Excel‑Blatt in C# als PNG exportieren.
  Lernen Sie die Bildexportoptionen kennen, wie man PNG exportiert und ein druckfähiges
  Bild aus einer Arbeitsmappe erhält.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area
- excel sheet to png
- how to export png
- export excel image
- image export options
language: de
lastmod: 2026-10-26
og_description: Druckbereich festlegen und ein Excel‑Blatt in C# nach PNG exportieren.
  Dieses Schritt‑für‑Schritt‑Tutorial behandelt Bildexportoptionen und erklärt, wie
  man PNG aus einer Arbeitsmappe exportiert.
og_image_alt: Screenshot showing an Excel worksheet with the print area set and exported
  as a PNG image
og_title: Druckbereich festlegen und Excel‑Tabelle nach PNG exportieren – C#‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Set print area and export an Excel sheet to PNG in C#. Learn image
    export options, how to export PNG, and get a printable image from a workbook.
  headline: Set print area and export Excel sheet to PNG in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Druckbereich festlegen und Excel‑Blatt als PNG exportieren in C#
url: /de/net/rendering-and-export/set-print-area-and-export-excel-sheet-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Druckbereich festlegen und Excel‑Blatt nach PNG exportieren in C#

Wenn Sie **den Druckbereich festlegen** müssen, bevor Sie ein Excel‑Blatt nach PNG exportieren, zeigt Ihnen diese Anleitung, wie das geht. Sie sehen ein vollständiges C#‑Beispiel, das die Bildexportoptionen konfiguriert, den Druckbereich des Arbeitsblatts anpasst und das Ergebnis als Bild speichert.

Das Exportieren eines Excel‑Blatts nach PNG ist ein häufiges Bedürfnis, wenn Sie einen Schnappschuss eines Arbeitsblatts in einen Bericht, eine E‑Mail oder eine Webseite einbetten möchten. Der untenstehende Code funktioniert mit jeder Arbeitsmappe, die eine Pivot‑Tabelle enthält, aber die Technik lässt sich ebenso auf reguläre Datenbereiche anwenden. Es werden keine externen Werkzeuge benötigt – nur die Aspose.Cells‑Bibliothek für .NET.

## Voraussetzungen

- .NET 6.0 oder höher (das Beispiel zielt auf .NET 6 ab, aber jede aktuelle .NET‑Version funktioniert)
- Aspose.Cells für .NET (Installation über NuGet: `Install-Package Aspose.Cells`)
- Grundlegende Kenntnisse in C# und Excel‑Konzepten wie Arbeitsblättern und Druckbereichen

## Schritt 1: Bildexportoptionen konfigurieren

Zuerst erstellen Sie eine Instanz von `ImageOrPrintOptions`. Dieses Objekt teilt Aspose.Cells mit, wie das Blatt als Bild gerendert werden soll.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

// Define image export options (PNG format)
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    // Export quality settings can be adjusted here
    ImageFormat = ImageFormat.Png,
    // Optional: set resolution (DPI) for higher‑quality PNGs
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**Warum das wichtig ist:** `ImageOrPrintOptions` steuert das Ausgabeformat, die Auflösung und weitere Renderdetails. Die Verwendung von PNG gewährleistet verlustfreie Qualität, was ideal für Berichte ist, die scharfen Text und Grafiken benötigen.

## Schritt 2: Arbeitsmappe laden und das Ziel‑Arbeitsblatt zugreifen

```csharp
// Load an existing workbook (replace with your file path)
Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

// Access the first worksheet in the workbook
Worksheet worksheet = wb.Worksheets[0];
```

**Warum das wichtig ist:** Sie müssen mit einem bestimmten `Worksheet`‑Objekt arbeiten, da der Druckbereich eine Einstellung auf Arbeitsblattebene ist.

## Schritt 3: Den Bereich ermitteln, den Sie drucken möchten

In vielen Szenarien befinden sich die für Sie relevanten Daten in einer Pivot‑Tabelle. Der folgende Code extrahiert den Datenbereich der ersten Pivot‑Tabelle im Blatt.

```csharp
// Get the data range of the first pivot table on the worksheet
CellArea pivotDataRange = worksheet.PivotTables[0].PivotDataRange;
```

Falls Ihr Arbeitsblatt keine Pivot‑Tabelle enthält, können Sie `pivotDataRange` durch einen beliebigen `CellArea` ersetzen, den Sie manuell erstellen, z. B.:

```csharp
CellArea customRange = new CellArea(0, 0, 20, 10); // A1:K21
```

## Schritt 4: **Druckbereich festlegen**, um den ausgewählten Bereich anzupassen

```csharp
// Set the worksheet's print area to match the pivot table's data range
worksheet.PageSetup.PrintArea = pivotDataRange.RefersTo;
```

**Warum das wichtig ist:** Der Druckbereich gibt Excel (und Aspose.Cells) an, welche Zellen beim Rendern des Blatts zu einem Bild einbezogen werden sollen. Durch die Angleichung des Druckbereichs an den Pivot‑Datenbereich vermeiden Sie leere Ränder und stellen sicher, dass das exportierte PNG nur die relevanten Daten enthält.

## Schritt 5: Das Arbeitsblatt als PNG‑Bild exportieren

```csharp
// Export the worksheet to an image using the defined options
// and assign the resulting image to the first picture shape on the sheet
worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);

// Optionally, save the image to a file for external use
worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);
```

**Warum das wichtig ist:** `worksheet.ToImage` berücksichtigt den zuvor festgelegten Druckbereich, sodass die PNG‑Datei exakt die von Ihnen definierten Zellen enthält. Das Bild einer Bildform zuzuweisen ermöglicht es, es bei Bedarf wieder in die Arbeitsmappe einzufügen, während das Speichern auf die Festplatte Ihnen eine eigenständige Datei liefert.

## Vollständiges funktionierendes Beispiel

Wenn Sie alle Schritte zusammenführen, erhalten Sie ein eigenständiges Programm, das Sie sofort ausführen können.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

class ExportExcelToPng
{
    static void Main()
    {
        // 1️⃣ Configure image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 2️⃣ Load the workbook
        Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

        // 3️⃣ Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // 4️⃣ Get the data range of the first pivot table (or define your own)
        CellArea dataRange = worksheet.PivotTables[0].PivotDataRange;

        // 5️⃣ **Set print area** to the data range
        worksheet.PageSetup.PrintArea = dataRange.RefersTo;

        // 6️⃣ Export the worksheet as PNG
        worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);
        worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);

        Console.WriteLine("Export complete: WorksheetExport.png created.");
    }
}
```

### Erwartete Ausgabe

Beim Ausführen des Programms wird `C:\Temp\WorksheetExport.png` erstellt. Öffnet man die Datei, sieht man ein scharfes PNG‑Bild, das nur die durch den **festgelegten Druckbereich** definierten Zellen enthält (in diesem Beispiel die Pivot‑Tabellendaten). Das Bild kann in Word‑Dokumente, PowerPoint‑Folien oder Webseiten eingefügt werden, ohne dass weitere Konvertierungsschritte nötig sind.

## Umgang mit mehreren Arbeitsblättern oder Pivot‑Tabellen

- **Mehrere Arbeitsblätter:** Durchlaufen Sie `wb.Worksheets` und wiederholen Sie die Schritte 3‑5 für jedes Blatt, das Sie exportieren möchten.
- **Mehrere Pivot‑Tabellen:** Wählen Sie die passende `PivotTables[index]` aus oder iterieren Sie über `worksheet.PivotTables`, um jede Tabelle einzeln zu exportieren.
- **Keine Pivot‑Tabelle:** Erstellen Sie manuell einen `CellArea` (siehe den Kommentar in Schritt 3) und weisen Sie ihn `PrintArea` zu.

## Praktische Tipps (E‑E‑A‑T)

- **Profi‑Tipp:** Setzen Sie `HorizontalResolution` und `VerticalResolution` auf 300 DPI für druckfertige PNGs; niedrigere Werte reduzieren die Dateigröße für die Web‑Nutzung.
- **Achten Sie auf leere Bildformen:** Wenn das Arbeitsblatt keine Bildformen enthält, fügen Sie vor dem Zuweisen des Bildes eine hinzu:

```csharp
if (worksheet.Pictures.Count == 0)
{
    worksheet.Pictures.Add(0, 0, 0, 0);
}
```

- **Performance:** Die Wiederverwendung einer einzelnen `ImageOrPrintOptions`‑Instanz für mehrere Arbeitsblätter vermeidet unnötige Allokationen.
- **Kompatibilität:** Aspose.Cells 23.9+ unterstützt .NET 6 und neuere Versionen vollständig; ältere Versionen können Anpassungen der API‑Namen erfordern.

## Fazit

Sie wissen jetzt, wie Sie **den Druckbereich festlegen** und ein Excel 

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in dieser Anleitung gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man Excel nach PNG exportiert – vollständige Schritt‑für‑Schritt‑Anleitung](/cells/english/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/)
- [Wie man einen Excel‑Bereich als Bild mit C# und Aspose.Cells exportiert](/cells/english/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/)
- [Excel‑Blatt nach PNG – Pivot‑Tabelle als PNG in C# exportieren](/cells/english/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}