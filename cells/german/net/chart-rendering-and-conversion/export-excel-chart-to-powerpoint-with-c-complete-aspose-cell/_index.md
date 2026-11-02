---
category: general
date: 2026-08-04
description: Exportieren Sie ein Excel‑Diagramm nach PowerPoint mit Aspose.Cells in
  C#. Befolgen Sie diese Schritt‑für‑Schritt‑Anleitung zur Excel‑zu‑PowerPoint‑Konvertierung
  und behalten Sie die Formen editierbar.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel chart to powerpoint
- Aspose.Cells PPTX export
- editable shapes in PowerPoint
- Excel to PowerPoint conversion
- C# chart export
language: de
lastmod: 2026-08-04
og_description: Exportieren Sie ein Excel‑Diagramm nach PowerPoint mit Aspose.Cells
  in C#. Erfahren Sie, wie Sie eine bearbeitbare PPTX erstellen, Diagrammdaten erhalten
  und die Konvertierung von Excel nach PowerPoint automatisieren.
og_image_alt: Screenshot of an Excel chart rendered as an editable PowerPoint slide
og_title: Excel‑Diagramm mit C# nach PowerPoint exportieren – vollständiges Aspose.Cells‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  headline: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  type: TechArticle
- description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  name: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  steps:
  - name: Expected output
    text: '| File name | Content on slide | |--------------------------|------------------------------------------|
      | `ShapesExport.pptx` | The chart from `Shapes.xlsx` rendered as an editable
      PowerPoint chart, with axis labels, legends, and data series intact. |'
  - name: Exporting multiple worksheets
    text: If you need a slide for each worksheet, loop through `workbook.Worksheets`
      and call `Save` with a unique file name for each iteration.
  - name: Controlling slide layout
    text: Aspose.Slides lets you add a custom slide layout after the export. Create
      a new presentation, import the generated slide, and then apply a master theme.
  - name: Handling charts with external data sources
    text: If a chart references a data range outside the defined print area, extend
      the `PrintArea` to include those cells. Otherwise the chart may lose data series
      during export.
  - name: Licensing considerations
    text: 'Aspose libraries work in evaluation mode with a watermark. To remove the
      watermark, set the license before any API call:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- PowerPoint
title: Excel‑Diagramm mit C# nach PowerPoint exportieren – vollständige Aspose.Cells‑Anleitung
url: /de/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel‑Diagramm mit C# nach PowerPoint exportieren – vollständiger Aspose.Cells‑Leitfaden

Wenn Sie **Excel‑Diagramm nach PowerPoint exportieren** müssen, zeigt Ihnen dieses Tutorial, wie Sie dies mit Aspose.Cells und Aspose.Slides in C# erledigen. Sie erhalten eine vollständig editierbare PPTX, die Diagrammdaten und -formen beibehält, sodass die Konvertierung für weitere Designarbeiten bereit ist.

Das Exportieren von Diagrammen aus Excel nach PowerPoint ist ein häufiges Bedürfnis beim Aufbau automatisierter Reporting‑Pipelines, Vertriebspräsentationen oder Schulungsmaterialien. In diesem Leitfaden lernen Sie die genauen Schritte, um eine **Excel‑zu‑PowerPoint‑Konvertierung** durchzuführen, bei der alle Diagrammelemente editierbar bleiben. Kein manuelles Kopieren‑Einfügen ist erforderlich, und der Code funktioniert sowohl mit .NET 6+ als auch mit dem klassischen .NET‑Framework.

## Voraussetzungen

- Eine gültige Aspose.Cells‑Lizenz (oder ein kostenloser Evaluierungsschlüssel)  
- Aspose.Slides für .NET zum Projekt hinzugefügt (die Bibliothek verarbeitet die PPTX‑Ausgabe)  
- .NET 6 SDK oder höher installiert  
- Eine Excel‑Arbeitsmappe, die mindestens ein Diagramm enthält (für dieses Beispiel verwenden wir `Shapes.xlsx`)  

Sie können die NuGet‑Pakete mit den folgenden Befehlen installieren:

```bash
dotnet add package Aspose.Cells
dotnet add package Aspose.Slides
```

## Schritt 1: Excel‑Arbeitsmappe laden

Der erste Vorgang besteht darin, die Arbeitsmappe zu öffnen, die das zu exportierende Diagramm enthält. Die Klasse `Workbook` repräsentiert die gesamte Excel‑Datei.

```csharp
using Aspose.Cells;
using Aspose.Slides;   // required for PPTX output

// Load the Excel workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

**Warum das wichtig ist:** Das Laden der Arbeitsmappe gibt Ihnen Zugriff auf ihre Arbeitsblätter, Diagramme und Formatierungen. Aspose.Cells liest die Datei, ohne dass Microsoft Office installiert sein muss, wodurch die Lösung leichtgewichtig und serverfreundlich bleibt.

## Schritt 2: Arbeitsblatt auswählen und Druckbereich festlegen

Ein Arbeitsblatt kann viele Diagramme enthalten, aber Sie exportieren in der Regel einen bestimmten Bereich. Das Festlegen des `PrintArea` teilt Aspose.Cells mit, welche Zellen (einschließlich Diagrammen) gerendert werden sollen.

```csharp
// Choose the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Define the area that contains the chart and any supporting data
worksheet.PageSetup.PrintArea = "A1:G30";
```

**Warum das wichtig ist:** Durch die Beschränkung des Exports auf einen definierten Druckbereich vermeiden Sie unnötige leere Folien und halten die PPTX‑Dateigröße klein. Der Bereich kann angepasst werden, um exakt den Bereich Ihres Diagramms abzudecken.

## Schritt 3: Exportoptionen für eine editierbare PPTX konfigurieren

Aspose.Cells verwendet die Klasse `ImageOrPrintOptions`, um das Ausgabeformat und die Editierbarkeit zu steuern. Das Setzen von `ImageFormat` auf `ImageFormat.Pptx` erzeugt eine PowerPoint‑Datei, während `ExportEditableShapes = true` Diagrammobjekte als editierbare Formen beibehält.

```csharp
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Pptx,   // Target format
    ExportEditableShapes = true       // Keep shapes/textboxes editable
};

// Attach the options to the worksheet's print settings
worksheet.PageSetup.PrintOptions = exportOptions;
```

**Warum das wichtig ist:** Das Flag `ExportEditableShapes` ist der Schlüssel zu einem Ergebnis mit **editierbaren Formen in PowerPoint**. Ohne dieses Flag würde das Diagramm als Bild gerastert, wodurch die Möglichkeit verloren geht, Datenpunkte oder das Styling später zu ändern.

## Schritt 4: Arbeitsblatt als PowerPoint‑Präsentation speichern

Rufen Sie schließlich die Methode `Save` des `Workbook`‑Objekts auf. Das Enum `SaveFormat.Pptx` weist Aspose.Cells an, eine PowerPoint‑Datei zu erzeugen.

```csharp
// Export the selected worksheet to a PPTX file
workbook.Save("YOUR_DIRECTORY/ShapesExport.pptx", SaveFormat.Pptx);
```

Wenn der Code fertig ist, öffnen Sie `ShapesExport.pptx` in PowerPoint. Sie sehen eine Folie, die das ursprüngliche Excel‑Diagramm als natives PowerPoint‑Diagrammobjekt enthält. Doppelklicken Sie das Diagramm, um Daten zu bearbeiten, Farben zu ändern oder Animationen hinzuzufügen – genau wie wenn Sie das Diagramm direkt in PowerPoint erstellt hätten.

### Erwartete Ausgabe

| Dateiname                | Inhalt auf der Folie                     |
|--------------------------|------------------------------------------|
| `ShapesExport.pptx`      | Das Diagramm aus `Shapes.xlsx` wird als editierbares PowerPoint‑Diagramm dargestellt, mit Achsenbeschriftungen, Legenden und Datenreihen unverändert. |

## Vollständiges, ausführbares Beispiel

Unten finden Sie das vollständige Programm, das Sie kopieren, einfügen und ausführen können. Es enthält alle notwendigen `using`‑Anweisungen, Fehlerbehandlung und Kommentare.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;   // Required for PPTX output

class ExcelToPowerPoint
{
    static void Main()
    {
        // Path to the source Excel file – adjust as needed
        const string excelPath = "YOUR_DIRECTORY/Shapes.xlsx";
        // Path for the generated PowerPoint file
        const string pptxPath = "YOUR_DIRECTORY/ShapesExport.pptx";

        try
        {
            // Load the workbook
            Workbook workbook = new Workbook(excelPath);

            // Use the first worksheet (you can change the index or name)
            Worksheet worksheet = workbook.Worksheets[0];

            // Define the area that contains the chart
            worksheet.PageSetup.PrintArea = "A1:G30";

            // Set export options for PPTX with editable shapes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Pptx,
                ExportEditableShapes = true
            };
            worksheet.PageSetup.PrintOptions = exportOptions;

            // Save as PPTX
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export successful. PPTX saved to: {pptxPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**Erklärung jedes Blocks**

| Block | Zweck |
|-------|-------|
| `using`‑Direktiven | Importieren die Namespaces von Aspose.Cells und Aspose.Slides. |
| `Workbook workbook = new Workbook(excelPath);` | Lädt die Excel‑Datei, ohne dass Office installiert sein muss. |
| `worksheet.PageSetup.PrintArea = "A1:G30";` | Beschränkt den Export auf den Bereich, der das Diagramm enthält. |
| `ImageOrPrintOptions` | Konfiguriert die PPTX‑Ausgabe und aktiviert den **Aspose.Cells PPTX‑Export** mit editierbaren Formen. |
| `workbook.Save(pptxPath, SaveFormat.Pptx);` | Schreibt die PowerPoint‑Datei auf die Festplatte. |
| `try / catch` | Bietet grundlegende Fehlerbehandlung für fehlende Dateien oder Lizenzprobleme. |

Das Ausführen dieses Programms erzeugt eine PowerPoint‑Folie, die Sie in Microsoft PowerPoint, Google Slides (nach Konvertierung) oder einem beliebigen kompatiblen Viewer öffnen können.

## Häufige Variationen und Sonderfälle

### Export mehrerer Arbeitsblätter

Wenn Sie für jedes Arbeitsblatt eine Folie benötigen, iterieren Sie über `workbook.Worksheets` und rufen `Save` mit einem eindeutigen Dateinamen für jede Iteration auf.

```csharp
int index = 1;
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.PageSetup.PrintOptions = exportOptions;
    string fileName = $"Slide{index++}.pptx";
    workbook.Save(fileName, SaveFormat.Pptx);
}
```

### Folienlayout steuern

Aspose.Slides ermöglicht es Ihnen, nach dem Export ein benutzerdefiniertes Folienlayout hinzuzufügen. Erstellen Sie eine neue Präsentation, importieren Sie die erzeugte Folie und wenden Sie anschließend ein Master‑Theme an.

```csharp
using Aspose.Slides.Export;

// Load the PPTX created by Aspose.Cells
Presentation pres = new Presentation(pptxPath);

// Apply a built‑in layout (e.g., Title and Content)
pres.Slides[0].LayoutSlide = pres.LayoutSlides[(int)SlideLayoutType.TitleAndContent];

// Save the final presentation
pres.Save("FinalPresentation.pptx", SaveFormat.Pptx);
```

### Umgang mit Diagrammen, die externe Datenquellen verwenden

Wenn ein Diagramm einen Datenbereich außerhalb des definierten Druckbereichs referenziert, erweitern Sie den `PrintArea`, um diese Zellen einzuschließen. Andernfalls kann das Diagramm während des Exports Datenreihen verlieren.

### Lizenzierungsüberlegungen

Aspose‑Bibliotheken funktionieren im Evaluierungsmodus mit einem Wasserzeichen. Um das Wasserzeichen zu entfernen, setzen Sie die Lizenz vor jedem API‑Aufruf:

```csharp
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

Machen Sie dasselbe für Aspose.Slides, wenn Sie dessen erweiterte Funktionen nutzen.

## Profi‑Tipps

- **Exportoptionen wiederverwenden:** Erstellen Sie eine einzelne `ImageOrPrintOptions`‑Instanz und weisen Sie sie jedem Arbeitsblatt zu, um den Code DRY zu halten.  
- **Batch‑Verarbeitung:** Für groß angelegte Berichte kombinieren Sie diese Exportlogik mit einem Hintergrund‑Worker oder einer Azure‑Function, um PPTX‑Dateien bei Bedarf zu erzeugen.  
- **Performance:** Wenn Sie nur das Diagrammbild (nicht editierbar) benötigen, setzen Sie `ExportEditableShapes = false`. Dies reduziert den Speicherverbrauch und beschleunigt die Konvertierung.  
- **Testing:** Überprüfen Sie die erzeugte PPTX sowohl auf Windows‑ als auch auf macOS‑PowerPoint‑Installationen, da einige Rendering‑Eigenheiten zwischen den Plattformen variieren.

## Fazit

Sie haben nun eine vollständige End‑zu‑End‑Lösung für **Excel‑Diagramm nach PowerPoint exportieren** mit C#. Das Tutorial behandelte das Laden der Arbeitsmappe, das Auswählen des Druckbereichs, das Konfigurieren des **Aspose.Cells PPTX‑Exports** mit **editierbaren Formen in PowerPoint** und das Speichern des Ergebnisses als vollständig editierbare PPTX‑Datei.  

Ab hier können Sie weitere **Excel‑zu‑PowerPoint‑Konvertierungs**‑Szenarien erkunden, wie Batch‑Export, benutzerdefinierte Folienlayouts oder die Integration des Prozesses in eine Web‑API. Experimentieren Sie mit verschiedenen Diagrammtypen, fügen Sie Bilder hinzu oder kombinieren Sie mehrere Arbeitsblätter zu einer einzigen Präsentation, um die Ausgabe an Ihre Geschäftsanforderungen anzupassen.

Bereit, Ihren Reporting‑Workflow zu automatisieren? Versuchen Sie, die Quelldatei zu wechseln, den Druckbereich anzupassen und den Code in Ihre bestehenden .NET‑Dienste zu integrieren. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man Excel mit Aspose.Cells für .NET nach PowerPoint konvertiert: Ein vollständiger Leitfaden](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Wie man Excel‑Diagramme mit Aspose.Cells für .NET nach PDF exportiert: Eine Schritt‑für‑Schritt‑Anleitung](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Excel‑Zellen mit Aspose.Cells .NET in ein Bild exportieren: Eine Schritt‑für‑Schritt‑Anleitung](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}