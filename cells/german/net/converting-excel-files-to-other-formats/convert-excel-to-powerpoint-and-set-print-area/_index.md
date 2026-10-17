---
category: general
date: 2026-10-10
description: Excel nach PowerPoint konvertieren und Druckbereich in C# mit Aspose.Cells
  festlegen – erfahren Sie, wie Sie Excel exportieren, den Druckbereich festlegen
  und eine PPTX‑Datei erstellen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- set print area excel
- how to export excel
- how to set print area
- convert excel to pptx
language: de
lastmod: 2026-10-10
og_description: Excel mit Aspose.Cells in PowerPoint konvertieren. Dieses Tutorial
  zeigt, wie man den Druckbereich festlegt, Excel exportiert und eine PPTX‑Datei in
  C# erstellt.
og_image_alt: Screenshot of code that converts Excel to PowerPoint while setting the
  print area
og_title: Excel in PowerPoint konvertieren – vollständige Anleitung für C#‑Entwickler
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert Excel to PowerPoint and set print area in C# with Aspose.Cells
    – learn how to export Excel, set print area, and generate a PPTX file.
  headline: Convert Excel to PowerPoint and set print area
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Excel in PowerPoint konvertieren und Druckbereich festlegen
url: /de/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel in PowerPoint konvertieren und Druckbereich festlegen

Wenn Sie **Excel in PowerPoint konvertieren** müssen, zeigt Ihnen diese Anleitung genau, wie Sie dies in C# erledigen. Indem Sie zuerst einen Druckbereich festlegen, bestimmen Sie, welche Zellen auf jeder Folie erscheinen, und die endgültige PPTX-Datei entspricht Ihren Layout‑Erwartungen. Die Lösung beantwortet außerdem „how to export Excel“ und „how to set print area“ mit demselben Code‑Grundgerüst.

In diesem Tutorial werden Sie:

* Ein vorhandenes Arbeitsbuch laden.
* Den Druckbereich für ein Arbeitsblatt festlegen (der **set print area excel** Schritt).
* Konvertierungsoptionen für die PowerPoint‑Ausgabe konfigurieren.
* Eine **convert excel to pptx** Datei in einem einzigen Methodenaufruf erzeugen.

Der gesamte erforderliche Code ist enthalten, sodass Sie ihn sofort kopieren, einfügen und ausführen können.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie Folgendes haben:

| Requirement | Why it matters |
|-------------|----------------|
| **.NET 6.0 oder höher** | Das Beispiel richtet sich an .NET 6+, aber jede .NET‑Version, die C# 10 unterstützt, funktioniert. |
| **Aspose.Cells für .NET** | Diese Bibliothek stellt `Workbook`, `ImageOrPrintOptions` und die Methode `ConvertToPdf` (für PPTX verwendet) bereit. Installieren Sie sie via NuGet: `dotnet add package Aspose.Cells` |
| **Eine Eingabe‑Excel‑Datei** | Das Tutorial verwendet `input.xlsx`. Platzieren Sie sie in einem Ordner, den Sie im Code referenzieren können. |
| **Schreibberechtigung für den Ausgabepfad** | Das Programm schreibt `output.pptx`. Stellen Sie sicher, dass das Verzeichnis existiert und beschreibbar ist. |

> **Profi‑Tipp:** Wenn Sie mit mehreren Arbeitsblättern arbeiten, wiederholen Sie den Druckbereich‑Schritt für jedes Blatt vor der Konvertierung.

## Schritt 1: Erstellen Sie ein neues C#‑Konsolenprojekt

Öffnen Sie ein Terminal‑ oder PowerShell‑Fenster und führen Sie aus:

```bash
dotnet new console -n ExcelToPowerPointDemo
cd ExcelToPowerPointDemo
dotnet add package Aspose.Cells
```

Dies erstellt ein neues Projekt namens **ExcelToPowerPointDemo** und fügt das Aspose.Cells‑Paket hinzu, das die Kernabhängigkeit für **how to export Excel** in andere Formate darstellt.

## Schritt 2: Schreiben Sie den Konvertierungscode

Ersetzen Sie den Inhalt von `Program.cs` durch das vollständige Beispiel unten. Der Code demonstriert **convert excel to powerpoint**, zeigt **how to set print area** und erzeugt eine **convert excel to pptx** Datei.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook (how to export Excel)
            // -----------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
            Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");

            // -----------------------------------------------------------------
            // 2️⃣ Define the print area for the first worksheet (set print area excel)
            // -----------------------------------------------------------------
            // The range "A1:G30" will be the only part visible on the slide.
            // Adjust the range to match the data you want to show.
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";
            Console.WriteLine($"Print area set to {sheet.PageSetup.PrintArea} on sheet \"{sheet.Name}\".");

            // -----------------------------------------------------------------
            // 3️⃣ Configure conversion options for PowerPoint output
            // -----------------------------------------------------------------
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                // SaveFormat.Pptx tells Aspose.Cells to generate a PowerPoint file.
                SaveFormat = SaveFormat.Pptx,
                // Optional: set the slide size or DPI if needed.
                // HorizontalResolution = 300,
                // VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 4️⃣ Convert the worksheet to a PowerPoint presentation (convert excel to powerpoint)
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);
            Console.WriteLine($"Successfully created PowerPoint file at: {outputPath}");
        }
    }
}
```

### Warum jeder Teil wichtig ist

* **Laden des Arbeitsbuchs** – Dies ist der erste Schritt in jedem **how to export Excel**‑Szenario. `Workbook` liest die Datei in den Speicher und gibt Ihnen vollen Zugriff auf Arbeitsblätter, Zellen und Formatierungen.
* **Festlegen des Druckbereichs** – Durch Zuweisen von `PageSetup.PrintArea` teilen Sie Aspose.Cells mit, welche Zellen gerendert werden sollen. Das ist der Kern von **set print area excel**; ohne diesen Schritt würde das gesamte Blatt exportiert, was zu riesigen, unlesbaren Folien führen kann.
* **Auswahl von `SaveFormat.Pptx`** – Das Objekt `ImageOrPrintOptions` ermöglicht das Umschalten der Ausgabeformate. Das Setzen von `SaveFormat` auf `Pptx` startet die **convert excel to pptx**‑Pipeline.
* **Aufruf von `ConvertToPdf`** – Trotz des Methodennamens liefert die Bibliothek bei `SaveFormat` = `Pptx` eine PowerPoint‑Datei. Dies ist der empfohlene Weg, um **convert excel to powerpoint** in einem einzigen Aufruf zu erledigen.

## Schritt 3: Das Programm ausführen

Im Projektordner führen Sie aus:

```bash
dotnet run
```

Wenn alles korrekt konfiguriert ist, sollten Sie eine Konsolenausgabe ähnlich der folgenden sehen:

```
Loaded workbook with 1 worksheet(s).
Print area set to A1:G30 on sheet "Sheet1".
Successfully created PowerPoint file at: YOUR_DIRECTORY\output.pptx
```

Öffnen Sie `output.pptx` in Microsoft PowerPoint oder einem kompatiblen Viewer. Jede Folie entspricht der gedruckten Seite des Arbeitsblatts, begrenzt auf den von Ihnen definierten Bereich.

## Umgang mit mehreren Arbeitsblättern

Wenn Ihr Arbeitsbuch mehr als ein Blatt enthält und Sie jedes Blatt in einem eigenen Foliensatz haben möchten, iterieren Sie über die Sammlung:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet ws = workbook.Worksheets[i];
    ws.PageSetup.PrintArea = "A1:G30"; // adjust per sheet if needed
    string slidePath = $@"YOUR_DIRECTORY\output_sheet{i + 1}.pptx";
    ws.ConvertToPdf(conversionOptions, slidePath);
    Console.WriteLine($"Created {slidePath}");
}
```

Dieses Muster zeigt **how to export Excel** Daten Blatt für Blatt, während Sie dennoch **setting print area** einzeln festlegen.

## Sonderfälle und bewährte Vorgehensweisen

| Situation | Recommended approach |
|-----------|----------------------|
| **Sehr große Arbeitsblätter** | Reduzieren Sie den Druckbereich oder erhöhen Sie `HorizontalResolution`/`VerticalResolution`, um die PPTX‑Größe handhabbar zu halten. |
| **Unterschiedliche Seitenorientierungen** | Setzen Sie `sheet.PageSetup.Orientation = PageOrientationType.Landscape;` vor der Konvertierung. |
| **Benutzerdefinierte Foliengröße** | Verwenden Sie `conversionOptions.OnePagePerSheet = false;` und passen Sie `conversionOptions.Width` / `conversionOptions.Height` an. |
| **Fehlende Eingabedatei** | Umwickeln Sie den Ladevorgang mit einem `try { … } catch (FileNotFoundException)`‑Block, um eine klare Fehlermeldung auszugeben. |
| **Nicht‑ASCII‑Zeichen** | Stellen Sie sicher, dass das Arbeitsbuch mit UTF‑8‑Kodierung gespeichert ist; Aspose.Cells verarbeitet Unicode automatisch. |

## Vollständiger Quellcode zur Referenz

Unten finden Sie das gesamte Programm, einschließlich `using`‑Direktiven und Kommentaren. Speichern Sie es als `Program.cs` im Projekt, das in **Schritt 1** erstellt wurde.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the Excel file you want to convert.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";

            // 1️⃣ Load the workbook (how to export Excel)
            Workbook workbook = new Workbook(inputPath);

            // Select the first worksheet – you can loop for multiple sheets.
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Set the print area (set print area excel)
            sheet.PageSetup.PrintArea = "A1:G30";

            // 3️⃣ Prepare conversion options for PowerPoint output.
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx   // This triggers convert excel to pptx
            };

            // 4️⃣ Convert the worksheet to PowerPoint (convert excel to powerpoint)
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);

            Console.WriteLine("Conversion complete.");
        }
    }
}
```

## Erwartete Ausgabe

Das Ausführen des Programms erzeugt eine PowerPoint‑Datei (`output.pptx`), die Folgendes enthält:

* Eine Folie pro gedruckter Seite des Arbeitsblatts.
* Nur die Zellen innerhalb von **A1:G30** sind auf jeder Folie sichtbar.
* Erhaltene Formatierung (Schriftarten, Farben, Rahmen) wie in Excel.

Öffnen Sie die Datei in PowerPoint, um zu überprüfen, dass das Layout dem definierten Druckbereich entspricht.

## Fazit

Sie wissen jetzt, wie Sie **Excel in PowerPoint konvertieren** und dabei präzise **set print area excel** mit Aspose.Cells in C# verwenden. Das Tutorial behandelte **how to export Excel**, zeigte **how to set print area** und präsentierte das vollständige **convert excel to pptx**.

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu beherrschen und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man einen Druckbereich in Excel mit Aspose.Cells für .NET festlegt](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Druckbereich in Excel festlegen und nach PowerPoint exportieren – Schritt‑für‑Schritt‑Anleitung](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Druckbereich festlegen Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}