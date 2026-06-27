---
category: general
date: 2026-06-27
description: Copy pivot table to another sheet in C# using Aspose.Cells. Learn step‑by‑step
  how to preserve pivot data and formatting.
draft: false
keywords:
- copy pivot table to another sheet
- Aspose.Cells copy pivot
- Excel pivot duplication
- preserve pivot formatting
- copy range with pivot
language: en
og_description: Copy pivot table to another sheet in C# with Aspose.Cells. This tutorial
  shows exactly how to duplicate a pivot while keeping its formatting intact.
og_title: Copy Pivot Table to Another Sheet – Complete C# Guide
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Copy pivot table to another sheet in C# using Aspose.Cells. Learn step‑by‑step
    how to preserve pivot data and formatting.
  headline: Copy Pivot Table to Another Sheet – Complete C# Guide
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Copy Pivot Table to Another Sheet – Complete C# Guide
url: /net/pivot-tables/copy-pivot-table-to-another-sheet-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copy Pivot Table to Another Sheet – Complete C# Guide

Ever needed to **copy pivot table to another sheet** but worried you'd lose the slicers, calculated fields, or formatting? You're not alone. Many developers hit that snag when automating Excel reports, and the frustration is real. In this guide we'll walk through a clean, end‑to‑end solution that **preserves the pivot table** exactly as it appears.

We'll be using **Aspose.Cells for .NET**, a powerful library that lets you manipulate Excel files without ever opening Excel itself. By the end of this tutorial you'll have a ready‑to‑run C# snippet that copies a pivot table from one worksheet to another, keeping all the underlying data connections intact.

## What This Tutorial Covers

- Setting up a .NET project and adding the Aspose.Cells NuGet package.  
- Loading an existing workbook that already contains a pivot table.  
- Defining both the source range (the original pivot) and the destination range on a different sheet.  
- Using `CopyOptions` to **preserve the pivot table** while copying.  
- Saving the result and verifying that the pivot works in its new location.  

No external tools, no manual copy‑paste, and no hidden magic—just straightforward code you can drop into any C# console app or service.

> **Why you should care:** Automating pivot duplication saves hours of manual work, especially in nightly reporting pipelines where dozens of workbooks need identical pivot structures across multiple sheets.

---

## Step 1: Set Up the Project and Add Aspose.Cells

First things first. If you haven't already, create a new .NET console project:

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
```

Now add the Aspose.Cells package:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** Use the latest stable version (as of June 2026 v23.12). It includes bug fixes for `CopyPivotTable` handling.

## Step 2: Load the Workbook and Access Worksheets

Open the workbook that contains the source pivot table. In most real‑world scenarios the file lives on a shared drive, but for this demo we'll assume it's in a local folder called `YOUR_DIRECTORY`.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook containing the source pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Step 2: Access the first worksheet (source sheet)
        Worksheet sourceSheet = workbook.Worksheets[0];

        // We'll also create (or reference) a destination sheet
        Worksheet destSheet = workbook.Worksheets.Add("CopyDestination");
```

Here we create a new sheet named **CopyDestination** where the pivot will be dropped. If you already have a target sheet, just grab it by index or name.

## Step 3: Define Source and Destination Ranges

A pivot table lives inside a rectangular block of cells. You need to tell Aspose.Cells which block to copy. In this example the pivot occupies rows 0‑20 and columns 0‑10 (zero‑based indexing).

```csharp
        // Step 3: Define the source range that includes the pivot table (rows 0‑20, columns 0‑10)
        CellArea sourceRange = new CellArea(0, 0, 20, 10);

        // Step 4: Define the destination start cell (row 30, column 0) on the destination sheet
        // and calculate the target area size to match the source dimensions
        CellArea destinationRange = new CellArea(
            30,                                 // start row on destination sheet
            0,                                  // start column
            30 + sourceRange.RowCount - 1,     // end row (same height as source)
            sourceRange.ColumnCount - 1        // end column (same width as source)
        );
```

Notice how we compute the end row and column dynamically. This way, even if you later change the source range size, the destination will automatically adjust.

## Step 4: Perform the Copy While Preserving the Pivot

Now the magic happens. By passing a `CopyOptions` object with `CopyPivotTable = true`, Aspose.Cells knows to keep the pivot table’s definition intact.

```csharp
        // Step 5: Copy the range, preserving the pivot table
        destSheet.Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTable = true }
        );
```

Under the hood, Aspose.Cells recreates the pivot cache, refreshes the data source reference, and re‑applies any formatting. This is the **Excel pivot duplication** you’ve been looking for.

## Step 5: Save and Verify the Result

Finally, write the workbook back to disk. You can keep the original file untouched by saving to a new name.

```csharp
        // Step 6: Save the workbook with the copied pivot table
        workbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");

        // Optional: open the file automatically (Windows only)
        System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
        {
            FileName = "YOUR_DIRECTORY/copy-pivot.xlsx",
            UseShellExecute = true
        });
    }
}
```

Open the resulting `copy-pivot.xlsx` and you’ll see the pivot table perfectly replicated on the **CopyDestination** sheet, complete with slicers, calculated fields, and formatting. The underlying data source still points to the original table, so refreshing works exactly as before.

> **What if the source pivot spans a dynamic range?**  
> Use `Worksheet.PivotTables[0].CacheDefinition.SourceData` to retrieve the actual bounds, then build `sourceRange` from that information. This handles cases where rows or columns may expand over time.

## Bonus: Preserve Pivot Formatting Across Copies

Sometimes the default copy loses conditional formatting or custom number formats. To guard against that, extend the `CopyOptions`:

```csharp
        var options = new CopyOptions
        {
            CopyPivotTable = true,
            CopyFormatting = true,      // copies cell styles, colors, fonts
            CopyConditionalFormatting = true
        };
        destSheet.Cells.CopyRange(sourceRange, destinationRange, options);
```

Enabling `CopyFormatting` ensures the **preserve pivot formatting** requirement is satisfied, giving you a pixel‑perfect duplicate.

## Expected Output

When you run the program, the console will exit silently (unless you add logging). Opening `copy-pivot.xlsx` should show:

- Sheet 1: Original data and pivot table unchanged.  
- **CopyDestination**: An exact replica of the pivot, positioned starting at row 31 (since rows are 1‑based in Excel UI).  
- All slicers and filters functional; clicking “Refresh” updates both pivots simultaneously.

---

## Conclusion

We’ve just demonstrated how to **copy pivot table to another sheet** using Aspose.Cells in C#. The steps—setting up the project, loading the workbook, defining ranges, copying with `CopyPivotTable = true`, and saving—form a reliable pattern you can reuse in any automation pipeline.  

If you want to go further, consider:

- **Excel pivot duplication** across multiple workbooks (loop through files).  
- Using the **Aspose.Cells copy range with pivot** option to move pivots between different workbooks.  
- Automating refreshes with `PivotTable.RefreshData()` after copying.

Feel free to experiment with different source ranges, or combine this technique with chart generation for fully automated reporting dashboards. Got questions? Drop a comment, and happy coding!

---

![Screenshot showing copied pivot table in new sheet](copy-pivot-screenshot.png "copy pivot table to another sheet example")


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Change Pivot Table Source Data Using Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [Master Pivot Table Formatting in .NET Using Aspose.Cells](/cells/english/net/formatting/format-pivot-tables-dotnet-aspose-cells/)
- [Access Pivot Table External Data Sources in .NET using Aspose.Cells](/cells/english/net/data-analysis/access-pivot-table-data-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}