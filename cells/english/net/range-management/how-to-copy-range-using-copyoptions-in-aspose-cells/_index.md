---
category: general
date: 2026-11-19
description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
  formatting and pivot tables while copying an Excel range with formatting.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range using copyoptions
- copy excel range with formatting
- Aspose.Cells copy range
- preserve pivot tables Aspose
- Excel automation C#
language: en
lastmod: 2026-11-19
og_description: Copy range using CopyOptions in Aspose.Cells lets you duplicate Excel
  data with full formatting and pivot tables preserved, enabling reliable workbook
  manipulation.
og_image_alt: Screenshot of C# code that copies an Excel range using Aspose.Cells
  CopyOptions
og_title: Copy range using CopyOptions in Aspose.Cells – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  headline: How to copy range using CopyOptions in Aspose.Cells
  type: TechArticle
- description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  name: How to copy range using CopyOptions in Aspose.Cells
  steps:
  - name: Why `CopyOptions` matters
    text: '* **Performance** – The library performs a single internal operation rather
      than copying cells one‑by‑one. * **Accuracy** – All visual aspects (fonts, colors,
      borders) survive the move, which eliminates visual drift in generated reports.
      * **Reliability** – Pivot tables remain functional because the'
  - name: What if the destination area overlaps the source?
    text: 'Aspose.Cells throws an `ArgumentException`. To avoid this, calculate a
      destination that does not intersect the source, or copy to a different worksheet:'
  - name: How to copy between different workbooks?
    text: 'Create a second `Workbook` instance for the target file and use the same
      `CopyOptions` object:'
  - name: Does `CopyOptions` also copy merged cells?
    text: Yes. The `CopyStyle` flag includes merged‑cell information. If you need
      finer control, set `options.CopyMergedCells = true` (available in newer versions).
  - name: What about large ranges (thousands of rows)?
    text: The operation is memory‑efficient, but you may want to increase the `WorkbookSettings`
      `MemorySetting` to `MemorySetting.MemoryPreference` for very large files.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: How to copy range using CopyOptions in Aspose.Cells
url: /net/range-management/how-to-copy-range-using-copyoptions-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to copy range using CopyOptions in Aspose.Cells

If you need to **copy range using CopyOptions** in Aspose.Cells, this guide shows you exactly how to duplicate a block of cells while keeping all formatting and embedded pivot tables intact. Many developers struggle with preserving style when moving data between worksheets, and the `CopyOptions` class solves that problem without extra manual steps.

In this tutorial you will learn to:

* Define source and destination areas in an Excel workbook.  
* Use `CopyOptions` to retain cell formatting, column widths, and pivot tables.  
* Save the result to a new file ready for downstream processing.

The example works with any `.xlsx` file and requires only the Aspose.Cells for .NET library.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 or later installed.  
* A valid Aspose.Cells for .NET license (or a free evaluation key).  
* Visual Studio 2022 or any C# IDE you prefer.  

No additional NuGet packages are needed beyond `Aspose.Cells`.

## Step 1: Set up the project and import namespaces

Create a new console application and add the Aspose.Cells reference:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Your code will go here
        }
    }
}
```

The `using Aspose.Cells;` directive gives you access to `Workbook`, `CellArea`, and `CopyOptions`.

## Step 2: Load the workbook you want to modify

```csharp
// Step 2: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`Workbook` represents the entire Excel file. Replace `YOUR_DIRECTORY` with the folder that contains your source file.

## Step 3: Define the source and destination ranges

```csharp
// Step 3: Define the source range (A1:H30)
CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");

// Step 3b: Define the destination range (A35:H64)
CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");
```

`CellArea.CreateCellArea` builds a rectangular area based on the top‑left and bottom‑right cell addresses. You can adjust the coordinates to match the size of the block you need to copy.

## Step 4: Copy the range while preserving formatting and pivot tables

```csharp
// Step 4: Copy the range using CopyOptions
CopyOptions options = new CopyOptions
{
    // Preserve all cell styles, number formats, and column widths
    CopyStyle = true,
    // Keep formulas unchanged (they will still reference the original sheet)
    CopyFormula = true,
    // Preserve any pivot tables that intersect the copied area
    CopyPivotTables = true,
    // Retain data validation and conditional formatting
    CopyDataValidation = true,
    CopyConditionalFormatting = true
};

workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
```

The `CopyOptions` object tells Aspose.Cells exactly what to keep. Setting `CopyPivotTables = true` is the key to **copy range using CopyOptions** when your source includes pivot tables. The other flags ensure that **copy excel range with formatting** is achieved automatically—no extra code is required to re‑apply styles after the copy.

### Why `CopyOptions` matters

* **Performance** – The library performs a single internal operation rather than copying cells one‑by‑one.  
* **Accuracy** – All visual aspects (fonts, colors, borders) survive the move, which eliminates visual drift in generated reports.  
* **Reliability** – Pivot tables remain functional because their cache and source references are duplicated.

## Step 5: Save the modified workbook

```csharp
// Step 5: Save the workbook with the copied range
workbook.Save("YOUR_DIRECTORY/output.xlsx");
Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
```

After calling `Save`, the file `output.xlsx` contains the original data plus the duplicated block at the destination location, complete with formatting and pivot tables.

## Full source code for reference

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // Define source and destination ranges
            CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");
            CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");

            // Configure copy options to preserve everything
            CopyOptions options = new CopyOptions
            {
                CopyStyle = true,
                CopyFormula = true,
                CopyPivotTables = true,
                CopyDataValidation = true,
                CopyConditionalFormatting = true
            };

            // Perform the copy operation
            workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);

            // Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");
            Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
        }
    }
}
```

Running this program prints:

```
Range copied successfully. Output saved to output.xlsx
```

Open `output.xlsx` in Excel – you’ll see the block A1:H30 duplicated at A35:H64, with all cell colors, borders, number formats, and any pivot tables intact.

## Common questions and edge‑case handling

### What if the destination area overlaps the source?

Aspose.Cells throws an `ArgumentException`. To avoid this, calculate a destination that does not intersect the source, or copy to a different worksheet:

```csharp
Worksheet destSheet = workbook.Worksheets.Add("CopySheet");
destSheet.Cells.CopyRange(sourceRange, CellArea.CreateCellArea("A1", "H30"), options);
```

### How to copy between different workbooks?

Create a second `Workbook` instance for the target file and use the same `CopyOptions` object:

```csharp
Workbook target = new Workbook();
target.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
target.Save("target.xlsx");
```

### Does `CopyOptions` also copy merged cells?

Yes. The `CopyStyle` flag includes merged‑cell information. If you need finer control, set `options.CopyMergedCells = true` (available in newer versions).

### What about large ranges (thousands of rows)?

The operation is memory‑efficient, but you may want to increase the `WorkbookSettings` `MemorySetting` to `MemorySetting.MemoryPreference` for very large files.

## Pro tips

* **Reuse the same `CopyOptions`** instance for multiple copy operations – it reduces object allocation overhead.  
* **Validate ranges** before copying: `if (!CellArea.IsValid(sourceRange) || !CellArea.IsValid(destinationRange))` helps catch typo‑related errors early.  
* **Turn off calculation** (`workbook.Settings.CalcMode = CalculationMode.Manual`) while copying large data sets to speed up the process, then call `workbook.CalculateFormula()` after the copy if you need updated results.

## Conclusion

You now know how to **copy range using CopyOptions** in Aspose.Cells, achieving a full **copy excel range with formatting** while preserving pivot tables and other advanced features. This approach eliminates manual style re‑application and ensures your Excel automation remains robust and maintainable.

Next steps you might explore:

* Use `CopyOptions` to duplicate entire worksheets.  
* Combine the copy operation with `WorksheetCollection.AddCopy` for template‑based report generation.  
* Integrate the code into an ASP.NET Core API to provide on‑the‑fly Excel transformations.

Feel free to experiment with different source/destination coordinates, and share your results in the comments!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Excel Aspose Cells Dotnet Copy Range Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/french/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}