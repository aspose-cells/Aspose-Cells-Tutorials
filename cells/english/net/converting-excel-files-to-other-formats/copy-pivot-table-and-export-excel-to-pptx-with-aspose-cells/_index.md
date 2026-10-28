---
category: general
date: 2026-09-11
description: Copy pivot table and export Excel to PPTX using Aspose.Cells. Learn to
  generate editable PPTX and save workbook as PPTX in C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- export excel to pptx
- generate editable pptx
- save workbook as pptx
- export excel sheet pptx
language: en
lastmod: 2026-09-11
og_description: Copy pivot table and export Excel to PPTX in C# using Aspose.Cells.
  Generate editable PPTX and save workbook as PPTX with a few lines of code.
og_image_alt: Screenshot of copy pivot table code and generated editable PPTX slide
og_title: Copy pivot table and export Excel to PPTX – complete C# guide
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
title: Copy pivot table and export Excel to PPTX with Aspose.Cells
url: /net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copy pivot table and export Excel to PPTX with Aspose.Cells

If you need to copy a pivot table from one worksheet to another and then export the Excel file to a PowerPoint presentation, this guide shows you how. Using Aspose.Cells you can generate an editable PPTX and save the workbook as PPTX in just a few lines of C# code.

The tutorial covers every step required to move a pivot table, preserve its functionality, and produce a PPTX file where the chart and shapes remain editable. No external tools are needed—only the Aspose.Cells library and a .NET development environment.

## What you’ll achieve

* **Copy pivot table** from a source sheet to a destination sheet while keeping all data connections intact.  
* **Export Excel to PPTX** so the resulting slide can be edited in PowerPoint.  
* **Generate editable PPTX** where charts, tables, and shapes are not flattened into images.  
* **Save workbook as PPTX** using the same Aspose.Cells API call.  

### Prerequisites

* .NET 6.0 or later (the code also works with .NET Framework 4.6+).  
* Aspose.Cells for .NET (NuGet package `Aspose.Cells`).  
* A basic understanding of C# console applications.  

> **Pro tip:** Install the NuGet package via the CLI to guarantee you have the latest version:  
> ```bash
> dotnet add package Aspose.Cells
> ```

## How to copy pivot table between worksheets

The first operation is moving the pivot table while preserving its definition. Aspose.Cells provides a `CopyRange` method with a `CopyOptions` object that includes the `CopyPivotTable` flag.

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

**Why this works:**  
`CopyRange` copies cell data, formatting, and, when `CopyPivotTable` is true, the pivot table’s cache and metadata. The destination range starts at cell `A1` (row 0, column 0) but you can change the offsets to place the pivot table elsewhere.

**Common edge case:** If the destination sheet already contains a pivot table with the same name, Aspose.Cells will rename the incoming one automatically, preventing a name clash.

## Export Excel to PPTX and generate editable PPTX

After the pivot table is in place, you can export the whole workbook to a PPTX file. The `ImageOrPrintOptions` class lets you specify `ExportImageFormat = ImageFormat.Pptx`, which tells Aspose.Cells to treat the output as a PowerPoint presentation rather than a raster image.

```csharp
// Configure export options to produce an editable PPTX.
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ExportImageFormat = ImageFormat.Pptx
};

// Save the workbook as an editable PPTX file.
workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);
```

**Why this works:**  
When `ExportImageFormat` is set to `Pptx`, Aspose.Cells translates each worksheet into a slide. Shapes, charts, and pivot tables are written as native PowerPoint objects, so you can double‑click them in PowerPoint and edit the underlying data.

**Tip for large workbooks:** If you only need a subset of sheets, set `workbook.Worksheets.RemoveAt(index)` for the sheets you don’t want to export before calling `Save`. This reduces the PPTX file size.

## Full, runnable example

Below is the complete program that ties the previous steps together. Replace `YOUR_DIRECTORY` with the actual path on your machine.

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

### Expected output

Running the program prints:

```
Pivot table copied and workbook exported to PPTX successfully.
```

When you open `output.pptx` in Microsoft PowerPoint, you will see a slide that contains the copied pivot table as an editable chart. Double‑clicking the chart opens the PowerPoint chart editor, allowing you to modify series, axes, and data labels without reverting to Excel.

## Handling typical pitfalls

| Issue | Cause | Fix |
|-------|-------|-----|
| Pivot table appears as a static image | `CopyPivotTable` flag omitted or `ExportImageFormat` set to `Png` | Ensure `CopyPivotTable = true` and `ExportImageFormat = ImageFormat.Pptx`. |
| Destination sheet shows blank cells | Source range does not cover the entire pivot table area | Expand the range (e.g., `"A1:H30"`) to include all pivot fields. |
| Exported PPTX is huge | Unnecessary worksheets are included | Remove unwanted sheets before calling `Save`. |
| PowerPoint cannot edit the chart | Using an older version of Aspose.Cells that lacks PPTX support | Upgrade to the latest Aspose.Cells version (check the release notes). |

## Next steps and related topics

* **Export Excel sheet to PPTX with custom slide layouts** – explore `WorksheetToPdfConverter` for finer control over slide appearance.  
* **Export Excel to PDF** – replace `ImageFormat.Pptx` with `ImageFormat.Pdf` to generate a PDF instead.  
* **Programmatically modify PPTX after export** – use the `Aspose.Slides` library to add animations or speaker notes.  

By mastering **copy pivot table**, **export excel to pptx**, and **generate editable pptx**, you can build end‑to‑end reporting pipelines that move data from spreadsheets straight into presentation decks without losing editability.

---


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Create a Pivot Table in Excel Using Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}