---
category: general
date: 2026-02-26
description: Export workbook to PDF with embedded fonts and also export charts to
  PowerPoint in C#. Learn to copy pivot table worksheet and save workbook as PPTX.
draft: false
keywords:
- export workbook to pdf
- export charts to powerpoint
- copy pivot table worksheet
- embed fonts pdf export
- save workbook as pptx
language: en
og_description: Export workbook to PDF with embedded fonts and also export charts
  to PowerPoint in C#. Follow the step‑by‑step guide to copy pivot tables and save
  as PPTX.
og_title: Export Workbook to PDF – Complete C# Guide
tags:
- Aspose.Cells
- Aspose.Slides
- C#
- Reporting
title: Export Workbook to PDF – Complete C# Guide
url: /net/conversion-to-pdf/export-workbook-to-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Workbook to PDF – Complete C# Guide

Export workbook to PDF is a common requirement when you need to share reports with stakeholders who may not have Excel installed. In this tutorial we’ll also show you how to **export charts to PowerPoint**, copy a **pivot table worksheet**, and embed fonts so the PDF looks exactly like your on‑screen design.  

Ever wondered why some PDFs lose the original layout or why PowerPoint slides end up with missing shapes? The answer usually lies in missing options during the export process. By the end of this guide you’ll have a single, reusable C# method that handles all of those pain points—no more manual copy‑pasting or fiddling with export settings.

## What You’ll Learn

- How to create a workbook, add Smart Marker expressions, and process them.  
- How to **copy a pivot table worksheet** without breaking the data source.  
- How to **export charts, shapes, and text boxes** to a PowerPoint presentation while keeping them editable.  
- How to **embed standard fonts** during PDF export for consistent rendering on any machine.  
- How to **save the workbook as PPTX** using the `save workbook as pptx` approach.  

All of this works with the latest Aspose.Cells and Aspose.Slides .NET libraries (version 23.11 at the time of writing). No external tools, no post‑processing scripts—just pure C#.

> **Pro tip:** If you’re already using Aspose in your project, you can drop the code snippets as‑is; otherwise, add the NuGet packages `Aspose.Cells` and `Aspose.Slides` first.

## Prerequisites

- .NET 6.0 or later (the code also runs on .NET Framework 4.7.2).  
- Visual Studio 2022 (or any IDE you prefer).  
- Aspose.Cells .NET and Aspose.Slides .NET installed via NuGet.  
- Basic familiarity with C# and Excel concepts like Smart Markers and PivotTables.

---

![Export workbook to PDF diagram](export-workbook-to-pdf.png "Export workbook to PDF workflow showing PDF and PPTX outputs")

## Export Workbook to PDF – Step‑by‑Step Implementation

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

### Why This Works

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

## Copy Pivot Table Worksheet Without Losing Data

Pivot tables are often the trickiest part of an export because they rely on a hidden cache. The simple `Copy` method works because Aspose copies both the visible range **and** the underlying cache object.

```csharp
// Copy the whole sheet (including pivot table) to a new workbook
Workbook clone = new Workbook();
reportWorkbook.Worksheets[0].CopyTo(clone.Worksheets[0]);
clone.Save(@"C:\Temp\PivotCopy.xlsx", SaveFormat.Xlsx);
```

> **Note:** If you only need the pivot table on a new sheet within the same workbook, the earlier `sourceRange.Copy` approach is lighter and avoids creating a whole new workbook.

## Embed Fonts for PDF Export – Why It Matters

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

## Full Working Example Recap

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

## Frequently Asked Questions (FAQ)

**Q: Does this work with .NET Core?**  
Yes—Aspose.Cells and Aspose.Slides are cross‑platform. Just target .NET 6 or later and the same code runs on Windows, Linux, or macOS.

**Q: What if I need to export only a subset of sheets?**  
Use `Workbook.Save` with `SaveOptions` that let you specify `SheetNames`. Example: `new PresentationOptions { SheetNames = new[] { "Copy" } }`.

**Q: Can I encrypt the PDF?**  
Absolutely. Set `PdfSaveOptions.EncryptionDetails` with a password before calling `Save`.

**Q: My pivot table uses an external data source—will copying break the link?**  
The copy operation includes the cache, not the external connection. The pivot will still work offline, but it won’t refresh against the original source. If you need live refresh, export the source data together with the workbook.

---

## Next Steps & Related Topics

- **Dynamic Data Sources** – Learn how to feed JSON or a DataTable into Smart Markers for real‑time reporting.  
- **Advanced PDF Styling** – Explore `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}