---
category: general
date: 2026-09-18
description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables, export
  ranges, and save as PPTX in a few lines of C# code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create powerpoint from excel
- how to copy pivot table
- copy range between workbooks
- how to export excel to pptx
- save workbook as pptx
language: en
lastmod: 2026-09-18
og_description: Create PowerPoint from Excel quickly. Learn how to copy pivot tables,
  export ranges, and save a workbook as PPTX using Aspose.Cells.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel data
og_title: Create PowerPoint from Excel with Aspose.Cells – step‑by‑step guide
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
title: How to create PowerPoint from Excel using Aspose.Cells
url: /net/converting-excel-files-to-other-formats/how-to-create-powerpoint-from-excel-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create PowerPoint from Excel using Aspose.Cells

If you need to create PowerPoint from Excel, this guide shows you a concise, end‑to‑end solution. You’ll see how to copy a pivot table, export a selected range, and save the result as a PPTX file with just a few lines of C#.

Generating a slide deck directly from spreadsheet data removes the manual copy‑paste step that slows down reporting workflows. The tutorial covers everything you need, from project setup to the final PPTX file, and it works with the latest Aspose.Cells for .NET.

## Prerequisites

Before you start, make sure you have:

* **Aspose.Cells for .NET** (version 23.12 or newer). Install it via NuGet: `Install-Package Aspose.Cells`.
* A **.NET 6+** development environment (Visual Studio 2022 or VS Code works).
* An Excel workbook (`Source.xlsx`) that contains the data and the pivot table you want to reuse.
* Write permission to the output folder.

No additional third‑party libraries are required.

## Create PowerPoint from Excel – step‑by‑step

The process consists of four logical steps that map directly to the code example you’ll see later.

### Step 1: Load the source workbook and define the range

You must load the workbook that holds the source data and the pivot table. Selecting a precise range ensures that only the needed cells are transferred, which keeps the resulting slide lightweight.

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

**Why this matters:**  
`CreateRange` creates a `Range` object that can be copied as a whole. By limiting the range to `A1:G20`, you avoid pulling unrelated cells, which could otherwise bloat the PowerPoint file.

### Step 2: Prepare the destination workbook

Aspose.Cells treats a PowerPoint slide as a workbook when you save it in PPTX format. Creating a fresh workbook gives you a clean canvas for the copied range.

```csharp
// Create a new empty workbook that will become the PowerPoint slide
Workbook destinationWorkbook = new Workbook();

// Use the first worksheet of the new workbook
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

**Tip:** If you need multiple slides, you can add additional worksheets and later save each as a separate PPTX file.

### Step 3: Copy the range while preserving the pivot table

The `CopyRange` method accepts a `PasteOptions` object. Setting `CopyPivotTables = true` tells Aspose.Cells to keep the pivot table structure intact, not just the rendered values.

```csharp
// Copy the defined range, preserving the pivot table definition
destinationSheet.Cells.CopyRange(
    sourceRange,
    new PasteOptions { CopyPivotTables = true });
```

**How it works:**  
When `CopyPivotTables` is true, the destination sheet receives both the source data and the pivot cache. This means the pivot table remains fully functional and can be refreshed later if the source data changes.

### Step 4: Save the workbook as a PowerPoint file

Finally, export the workbook to PPTX format. The `SaveFormat.Pptx` flag tells Aspose.Cells to write the worksheet as a PowerPoint slide.

```csharp
// Save the destination workbook as a PowerPoint presentation
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);
```

**Result:**  
`CopyWithPivot.pptx` opens in Microsoft PowerPoint (or any compatible viewer) with a single slide that displays the copied range, including a live pivot table that can be interacted with in PowerPoint.

## Full runnable example

Below is the complete program that you can paste into a new console project and run immediately.

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

**Expected output:**  
Running the program prints “PowerPoint file created successfully.” and produces a file named `CopyWithPivot.pptx`. Opening the file in PowerPoint shows a single slide where the copied Excel range appears exactly as it did in the source worksheet, with an active pivot table that can be refreshed from within PowerPoint.

## Common variations and edge cases

| Situation | What to change |
|-----------|----------------|
| **Multiple pivot tables** | Define separate `Range` objects for each table and call `CopyRange` for each one, or copy the whole sheet if they share the same data source. |
| **Large data sets** | Increase the range (e.g., `"A1:Z5000"`). Consider enabling `PasteOptions.CompressData = true` to reduce PPTX size. |
| **Different slide layouts** | After saving as PPTX, open the file in PowerPoint and apply a custom layout or theme; the data remains editable. |
| **Saving to a stream** | Use `destinationWorkbook.Save(stream, SaveFormat.Pptx)` when you need to return the PPTX via a web API. |
| **Preserving cell formatting** | Set `PasteOptions.PasteType = PasteType.All` to keep fonts, colors, and borders. |

**Pro tip:** Always verify that the destination folder exists before calling `Save`. If the folder is missing, `Save` throws a `DirectoryNotFoundException`.

## Conclusion

You now know how to create PowerPoint from Excel, copy a pivot table, and export the result as a PPTX file using Aspose.Cells. The steps—loading the source workbook, defining a range, copying with `CopyPivotTables`, and saving as PPTX—cover the entire workflow in a reliable, production‑ready manner.

Next, explore **how to export Excel to PPTX** for multiple worksheets, or learn **how to copy range between workbooks** when you need to merge data from several sources before generating the slide deck. Both topics build on the same API surface and can be combined to automate complex reporting pipelines.

Happy coding, and enjoy turning your spreadsheets into polished presentations!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [How to Create and Save Excel Files with Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}