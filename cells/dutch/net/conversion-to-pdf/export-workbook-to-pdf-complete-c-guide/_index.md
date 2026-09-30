---
category: general
date: 2026-02-26
description: Exporteer werkmap naar PDF met ingesloten lettertypen en exporteer ook
  grafieken naar PowerPoint in C#. Leer hoe je een draaitabelblad kopieert en de werkmap
  opslaat als PPTX.
draft: false
keywords:
- export workbook to pdf
- export charts to powerpoint
- copy pivot table worksheet
- embed fonts pdf export
- save workbook as pptx
language: nl
og_description: Exporteer werkmap naar PDF met ingesloten lettertypen en exporteer
  ook grafieken naar PowerPoint in C#. Volg de stapsgewijze handleiding om draaitabellen
  te kopiëren en op te slaan als PPTX.
og_title: Werkmap exporteren naar PDF – Complete C#‑gids
tags:
- Aspose.Cells
- Aspose.Slides
- C#
- Reporting
title: Werkmap exporteren naar PDF – Complete C#‑gids
url: /nl/net/conversion-to-pdf/export-workbook-to-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Werkmap exporteren naar PDF – Complete C#‑gids

Export workbook to PDF is a common requirement when you need to share reports with stakeholders who may not have Excel installed. In this tutorial we’ll also show you how to **export charts to PowerPoint**, copy a **pivot table worksheet**, and embed fonts so the PDF looks exactly like your on‑screen design.  

Ever wondered why some PDFs lose the original layout or why PowerPoint slides end up with missing shapes? The answer usually lies in missing options during the export process. By the end of this guide you’ll have a single, reusable C# method that handles all of those pain points—no more manual copy‑pasting or fiddling with export settings.

## Wat je leert

- Hoe je een workbook maakt, Smart Marker‑expressies toevoegt en ze verwerkt.  
- Hoe je een **pivot‑tabel‑werkblad** kunt **kopiëren** zonder de gegevensbron te breken.  
- Hoe je **grafieken, vormen en tekstvakken** kunt **exporteren naar een PowerPoint‑presentatie** terwijl ze bewerkbaar blijven.  
- Hoe je **standaardlettertypen** kunt **embedden** tijdens PDF‑export voor consistente weergave op elke machine.  
- Hoe je **het workbook opslaat als PPTX** met de `save workbook as pptx`‑aanpak.  

Al dit werkt met de nieuwste Aspose.Cells en Aspose.Slides .NET‑bibliotheken (versie 23.11 op het moment van schrijven). Geen externe tools, geen post‑processing‑scripts—alleen pure C#.

> **Pro tip:** Als je Aspose al in je project gebruikt, kun je de code‑fragmenten direct overnemen; anders voeg je eerst de NuGet‑pakketten `Aspose.Cells` en `Aspose.Slides` toe.

## Voorwaarden

- .NET 6.0 of later (de code werkt ook op .NET Framework 4.7.2).  
- Visual Studio 2022 (of elke IDE die je verkiest).  
- Aspose.Cells .NET en Aspose.Slides .NET geïnstalleerd via NuGet.  
- Basiskennis van C# en Excel‑concepten zoals Smart Markers en PivotTables.

---

![Werkmap exporteren naar PDF diagram](export-workbook-to-pdf.png "Export werkmap naar PDF workflow die PDF- en PPTX-uitvoer toont")

## Export Workbook to PDF – Stap‑voor‑stap implementatie

Below is the full, ready‑to‑run example. It builds a workbook, injects Smart Marker expressions, processes them, copies a pivot table range, and finally saves both a PDF and a PowerPoint file.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides.Export;

namespace ReportExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Build the workbook and add Smart Markers
            // -------------------------------------------------
            var reportWorkbook = new Workbook();
            Worksheet dataSheet = reportWorkbook.Worksheets[0];

            // Header with a variable department name
            dataSheet.Cells["A1"].PutValue("Report for ${$dept=Department}");

            // Conditional text based on department
            dataSheet.Cells["A2"].PutValue("${if $dept == \"Sales\"}Sales Summary${else}Other Summary${/if}");

            // Table header for orders – this will be repeated for each order
            dataSheet.Cells["A5:D5"].PutValue("${Orders.Product}|${Orders.Quantity}|${Orders.Price}");

            // -------------------------------------------------
            // Step 2: Process Smart Markers and name the detail sheet
            // -------------------------------------------------
            reportWorkbook.SmartMarkerProcessor.Options.DetailSheetNewName = "Orders_${$dept}";
            reportWorkbook.SmartMarkerProcessor.Process();

            // -------------------------------------------------
            // Step 3: Copy the range that contains the pivot table
            // -------------------------------------------------
            // Assume the pivot table lives in A1:G30 on the original sheet
            Range sourceRange = dataSheet.Cells.CreateRange("A1", "G30");
            Worksheet copySheet = reportWorkbook.Worksheets.Add("Copy");
            sourceRange.Copy(copySheet.Cells["A1"]);   // Pivot table is duplicated intact

            // -------------------------------------------------
            // Step 4: Export to PowerPoint (keep charts, shapes, text boxes)
            // -------------------------------------------------
            var pptOptions = new PresentationOptions
            {
                ExportCharts = true,
                ExportShapes = true,
                ExportTextBoxes = true
            };
            string pptPath = @"C:\Temp\FinalPresentation.pptx";
            reportWorkbook.Save(pptPath, SaveFormat.Pptx, pptOptions);

            // -------------------------------------------------
            // Step 5: Export to PDF and embed standard fonts
            // -------------------------------------------------
            var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
            string pdfPath = @"C:\Temp\FinalReport.pdf";
            reportWorkbook.Save(pdfPath, pdfOptions);

            Console.WriteLine("Export completed:");
            Console.WriteLine($" • PDF saved to {pdfPath}");
            Console.WriteLine($" • PowerPoint saved to {pptPath}");
        }
    }
}
```

### Waarom dit werkt

1. **Smart Marker processing** lets you populate the workbook from any data source (JSON, DataTables, etc.) without writing loops.  
2. **DetailSheetNewName** creates a separate sheet for each department, giving you a clean, per‑department tab.  
3. **Copying the range** (`sourceRange.Copy`) duplicates the pivot table *including* its cache, so the copied sheet behaves exactly like the original.  
4. **PresentationOptions** with `ExportCharts`, `ExportShapes`, and `ExportTextBoxes` tells Aspose to render those objects as native PowerPoint elements, preserving editability.  
5. **PdfSaveOptions.EmbedStandardFonts** ensures the PDF looks identical on machines that don’t have the original fonts installed.

The result is two files—`FinalReport.pdf` and `FinalPresentation.pptx`—that can be emailed, archived, or displayed in any viewer without losing fidelity.

## Export Charts to PowerPoint (Save Workbook as PPTX)

If your report contains charts, you’ll likely want them editable in PowerPoint. The `PresentationOptions` class is the key. Here’s a focused snippet that shows just the chart‑export part:

```csharp
// Assuming reportWorkbook already contains charts
var pptExportOptions = new PresentationOptions
{
    ExportCharts = true,      // Convert Excel charts to PowerPoint chart objects
    ExportShapes = false,    // Skip shapes if you don’t need them
    ExportTextBoxes = true   // Keep any text boxes editable
};

string pptFile = @"C:\Temp\ChartsOnly.pptx";
reportWorkbook.Save(pptFile, SaveFormat.Pptx, pptExportOptions);
```

**What happens under the hood?** Aspose translates each Excel chart into a native PowerPoint chart, preserving series, axis titles, and formatting. This is far better than exporting the chart as a static image, because your audience can tweak data points later.

## Kopieer Pivot‑tabel‑werkblad zonder gegevensverlies

Pivot tables are often the trickiest part of an export because they rely on a hidden cache. The simple `Copy` method works because Aspose copies both the visible range **and** the underlying cache object.

```csharp
// Copy the whole sheet (including pivot table) to a new workbook
Workbook clone = new Workbook();
reportWorkbook.Worksheets[0].CopyTo(clone.Worksheets[0]);
clone.Save(@"C:\Temp\PivotCopy.xlsx", SaveFormat.Xlsx);
```

> **Note:** If you only need the pivot table on a new sheet within the same workbook, the earlier `sourceRange.Copy` approach is lighter and avoids creating a whole new workbook.

## Lettertypen embedden voor PDF‑export – Waarom het belangrijk is

When you open a PDF on a machine that lacks the original fonts, the text can shift, line breaks change, or characters disappear. Setting `EmbedStandardFonts = true` tells Aspose to embed the most common fonts (Arial, Times New Roman, etc.) directly into the PDF stream.

If you use custom fonts, switch to `PdfSaveOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedAll`. Here’s an example:

```csharp
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    FontEmbeddingMode = FontEmbeddingMode.EmbedAll   // For custom fonts
};
reportWorkbook.Save(@"C:\Temp\CustomFontReport.pdf", pdfOpts);
```

Now every recipient sees the exact same layout you designed—no surprises.

## Volledig werkend voorbeeld – Samenvatting

Putting everything together, the complete program (shown earlier) does the following:

1. **Creates** a workbook with Smart Marker placeholders.  
2. **Processes** the markers, generating a detail sheet named after the department.  
3. **Copies** a range that contains a pivot table to a new worksheet, preserving its functionality.  
4. **Exports** the workbook to PowerPoint, keeping charts, shapes, and text boxes editable.  
5. **Exports** the same workbook to PDF while embedding standard fonts for reliable rendering.

Run the program, open the generated files, and you’ll see:

- **PDF**: Crisp tables, embedded fonts, and the same visual style as the Excel source.  
- **PowerPoint**: Editable charts that you can right‑click → *Edit Data* in PowerPoint, and shapes that remain fully manipulatable.

---

## Veelgestelde vragen (FAQ)

**Q: Werkt dit met .NET Core?**  
Ja—Aspose.Cells en Aspose.Slides zijn cross‑platform. Richt je gewoon op .NET 6 of later en dezelfde code draait op Windows, Linux of macOS.

**Q: Wat als ik alleen een subset van werkbladen wil exporteren?**  
Gebruik `Workbook.Save` met `SaveOptions` waarmee je `SheetNames` kunt opgeven. Voorbeeld: `new PresentationOptions { SheetNames = new[] { "Copy" } }`.

**Q: Kan ik de PDF versleutelen?**  
Absoluut. Stel `PdfSaveOptions.EncryptionDetails` in met een wachtwoord voordat je `Save` aanroept.

**Q: Mijn pivot‑tabel gebruikt een externe gegevensbron—zal kopiëren de koppeling breken?**  
De copy‑operatie omvat de cache, niet de externe verbinding. De pivot werkt nog offline, maar hij wordt niet ververst tegen de originele bron. Als je live‑verversing nodig hebt, exporteer dan de brongegevens samen met het workbook.

## Volgende stappen & gerelateerde onderwerpen

- **Dynamische gegevensbronnen** – Leer hoe je JSON of een DataTable in Smart Markers kunt voeren voor realtime‑rapportage.  
- **Geavanceerde PDF‑styling** – Verken `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}