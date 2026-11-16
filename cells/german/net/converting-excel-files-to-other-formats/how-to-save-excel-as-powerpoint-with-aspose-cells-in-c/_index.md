---
category: general
date: 2026-11-16
description: Erfahren Sie, wie Sie Excel als PowerPoint speichern und Excel programmgesteuert
  in PowerPoint konvertieren. Dieser Schritt‑für‑Schritt‑Leitfaden behandelt außerdem
  das Exportieren von Excel nach PPTX und das Speichern einer Arbeitsmappe als PPTX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- export excel to pptx
- how to convert excel slide
- save workbook as pptx
language: de
lastmod: 2026-11-16
og_description: Speichern Sie Excel als PowerPoint mit Aspose.Cells. Folgen Sie dieser
  Anleitung, um Excel in PowerPoint zu konvertieren, Excel nach PPTX zu exportieren
  und die Arbeitsmappe in wenigen Minuten als PPTX zu speichern.
og_image_alt: Screenshot showing the result of saving Excel as PowerPoint with editable
  shapes
og_title: Excel als PowerPoint speichern – Vollständiger C#‑Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to save Excel as PowerPoint and convert Excel to PowerPoint
    programmatically. This step‑by‑step guide also covers export Excel to PPTX and
    saving a workbook as PPTX.
  headline: How to save Excel as PowerPoint with Aspose.Cells in C#
  type: TechArticle
tags:
- Excel
- PowerPoint
- Aspose.Cells
- C#
- Export
title: Wie man Excel mit Aspose.Cells in C# als PowerPoint speichert
url: /de/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-with-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Excel als PowerPoint mit Aspose.Cells in C# speichert

Wenn Sie **Excel programmgesteuert als PowerPoint speichern** müssen, bietet Ihnen dieses Tutorial eine vollständige, sofort einsatzbereite Lösung. Egal, ob Sie eine Reporting-Engine oder einen automatisierten Foliengenerator erstellen, die nachfolgenden Schritte ermöglichen es Ihnen, ein Excel-Arbeitsblatt mit nur wenigen Codezeilen in eine editierbare PPTX‑Folie zu konvertieren.

Sie lernen, wie man **Excel nach PowerPoint konvertiert**, das Blatt in eine PPTX‑Datei exportiert und Textfelder sowie Formen editierbar hält – alles ohne die .NET‑Umgebung zu verlassen.

## Voraussetzungen

* .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.7.2+)
* Eine gültige Aspose.Cells‑Lizenz (die kostenlose Testversion eignet sich für Evaluierungen)
* Visual Studio 2022 (oder jede C#‑IDE)
* Eine Excel‑Arbeitsmappe, die die Daten und Formen enthält, die Sie exportieren möchten

## Schritt 1: Aspose.Cells installieren

Fügen Sie das Aspose.Cells‑NuGet‑Paket zu Ihrem Projekt hinzu:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Use the `-v` flag to target a specific version, e.g., `Aspose.Cells.24.5`.

## Schritt 2: Laden Sie die zu exportierende Arbeitsmappe

Der erste Vorgang im **Excel als PowerPoint speichern**‑Ablauf ist das Laden der Quellarbeitsmappe.

```csharp
using Aspose.Cells;
using System;

// Load the workbook that contains the shapes
Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");
```

*Warum das wichtig ist:* Das Laden der Arbeitsmappe gibt Ihnen Zugriff auf ihre Arbeitsblätter, die Seiteneinrichtung und die Zeichenobjekte, die zu editierbaren PowerPoint‑Formen werden.

## Schritt 3: Exportoptionen für eine editierbare PPTX‑Folie konfigurieren

Um **Excel nach PowerPoint zu konvertieren** und dabei die Editierbarkeit zu erhalten, müssen Sie einige Eigenschaften von `ImageOrPrintOptions` festlegen.

```csharp
// Prepare export options to generate an editable PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // Export format
    ExportEditableText = true,        // Keep text boxes editable
    ExportEditableShapes = true       // Keep shapes editable
};
```

*Erklärung:*  
* `SaveFormat = SaveFormat.Pptx` weist Aspose.Cells an, eine PowerPoint‑Datei zu erzeugen.  
* `ExportEditableText` und `ExportEditableShapes` sorgen dafür, dass die resultierende Folie sich wie eine native PowerPoint‑Folie verhält – Sie können ein Textfeld oder eine Form anklicken und direkt in PowerPoint bearbeiten.

## Schritt 4: Exportbereich festlegen und an eine einzelne Folie anpassen

Wenn Sie **Excel nach PPTX exportieren**, möchten Sie in der Regel einen bestimmten Bereich auf der Folie anzeigen. Das Festlegen des Druckbereichs und der Anpassungsoptionen garantiert ein sauberes Ein‑Folie‑Ergebnis.

```csharp
// Define the area of the first worksheet to export
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G30";

// Fit the exported content to a single slide
sheet.PageSetup.FitToPagesTall = 1;
sheet.PageSetup.FitToPagesWide = 1;
```

*Warum das wichtig ist:* `PrintArea` begrenzt den Export auf die Zellen A1 bis G30, während `FitToPagesTall` und `FitToPagesWide` alles in eine Folie komprimieren und unerwünschte zusätzliche Seiten verhindern.

## Schritt 5: Das Arbeitsblatt als editierbare PPTX‑Datei speichern

Jetzt können Sie endlich **die Arbeitsmappe als PPTX speichern** und den **Excel als PowerPoint speichern**‑Prozess abschließen.

```csharp
// Save the worksheet as an editable PPTX file
workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
Console.WriteLine("Export completed: EditableShapes.pptx");
```

Nachdem Sie das Programm ausgeführt haben, öffnen Sie `EditableShapes.pptx` in Microsoft PowerPoint. Sie sehen eine Folie, die den ausgewählten Excel‑Bereich widerspiegelt, und alle Textfelder sowie Formen sind vollständig editierbar.

### Erwartete Ausgabe

* Eine Datei namens `EditableShapes.pptx` im Verzeichnis `C:\Output\`.
* Eine PowerPoint‑Folie, die den Bereich A1:G30 enthält.
* Textfelder, Diagramme und Formen, die Sie per Doppelklick direkt in PowerPoint bearbeiten können.

## Vollständiger Quellcode (zum Kopieren bereit)

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the shapes
            Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");

            // Step 2: Prepare export options to generate an editable PPTX slide
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportEditableText = true,   // keep text boxes editable
                ExportEditableShapes = true  // keep shapes editable
            };

            // Step 3: Define the area of the first worksheet to export
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";

            // Step 4: Fit the exported content to a single slide
            sheet.PageSetup.FitToPagesTall = 1;
            sheet.PageSetup.FitToPagesWide = 1;

            // Step 5: Save the worksheet as an editable PPTX file
            workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
            Console.WriteLine("Export completed: EditableShapes.pptx");
        }
    }
}
```

## Häufige Fragen und Sonderfall‑Behandlung

| Frage | Antwort |
|----------|--------|
| **Was ist, wenn ich mehrere Arbeitsblätter habe?** | Durchlaufen Sie `workbook.Worksheets` und wiederholen Sie die Schritte 3‑5 für jedes Blatt, wobei Sie den Ausgabedateinamen ändern (z. B. `Sheet1.pptx`, `Sheet2.pptx`). |
| **Kann ich die gesamte Arbeitsmappe in ein einziges PowerPoint‑Deck exportieren?** | Ja. Setzen Sie `ExportAllSheets = true` bei `ImageOrPrintOptions`. Jedes Arbeitsblatt wird zu einer separaten Folie. |
| **Meine Formen erscheinen als Bilder, nicht als editierbare Objekte.** | Stellen Sie sicher, dass `ExportEditableShapes = true` ist und dass Sie Aspose.Cells 24.5+ verwenden (frühere Versionen besitzen diese Funktion nicht). |
| **Das erzeugte PPTX ist zu groß.** | Reduzieren Sie den Druckbereich oder verringern Sie die Bildauflösung über `exportOptions.ImageResolution`. |
| **Benötige ich eine Lizenz für den Produktionseinsatz?** | Eine kostenpflichtige Lizenz entfernt das Evaluations‑Wasserzeichen und schaltet die volle Leistung frei. Die kostenlose Testversion eignet sich für Tests. |

## Tipps für robusten Produktionscode

* **Dateipfade validieren** bevor Sie `Workbook` oder `Save` aufrufen, um `FileNotFoundException` zu vermeiden.  
* **Den Export in einen try/catch‑Block einbetten**, um Lizenzfehler (`Aspose.Cells.LicenseException`) zu behandeln.  
* **Die Arbeitsmappe freigeben** (`workbook.Dispose()`), wenn sie nicht mehr benötigt wird, um nicht verwaltete Ressourcen freizugeben.  
* **Asynchrone I/O verwenden** (`FileStream` mit `await`), wenn Sie viele große Arbeitsblätter in einem Webservice exportieren.

## Nächste Schritte

Jetzt, da Sie wissen, wie man **Excel als PowerPoint speichert**, können Sie verwandte Themen erkunden:

* **Excel nach PPTX mit benutzerdefinierten Folienlayouts exportieren** – `SlideSize` anpassen und eine Master‑Folie hinzufügen.  
* **Excel‑Folie in PDF konvertieren** – `SaveFormat.Pdf` für eine druckbare Version verwenden.  
* **Stapelweise einen Ordner mit Arbeitsmappen konvertieren** – die oben gezeigte Schleife mit `Directory.GetFiles` kombinieren.  

Experimentieren Sie mit verschiedenen Druckbereichen, Skalierungsoptionen und PowerPoint‑Designs, um die Ausgabe an das Branding Ihrer Organisation anzupassen.

---

*Viel Spaß beim Programmieren! Wenn Ihnen diese Anleitung geholfen hat, **Excel nach PowerPoint zu konvertieren**, teilen Sie sie gerne mit Kollegen oder öffnen Sie ein Issue im Aspose.Cells‑GitHub‑Repository für weitere Unterstützung.*

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man Excel als PowerPoint mit C# und Aspose.Cells speichert](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/)
- [Wie man PPTX aus Excel speichert – Vollständiger Leitfaden zum Export von Excel‑Blättern nach PowerPoint](/cells/english/java/integration-interoperability/how-to-save-pptx-from-excel-complete-guide-to-export-excel-s/)
- [Excel nach PowerPoint konvertieren – Vollständiger Schritt‑für‑Schritt‑Leitfaden](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-full-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}