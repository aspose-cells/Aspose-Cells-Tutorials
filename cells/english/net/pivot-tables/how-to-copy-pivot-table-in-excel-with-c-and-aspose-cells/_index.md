---
category: general
date: 2026-10-04
description: Learn how to copy pivot table from one workbook to another using C#.
  This guide also covers how to copy rows, duplicate pivot table, and copy Excel range
  efficiently.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- how to copy rows
- duplicate pivot table
language: en
lastmod: 2026-10-04
og_description: Copy pivot table in Excel using C#. Follow this complete tutorial
  to duplicate pivot tables, copy rows, and copy Excel range with Aspose.Cells.
og_image_alt: Screenshot showing a duplicated pivot table in an Excel worksheet after
  using C# code
og_title: Copy pivot table in Excel with C# – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to copy pivot table from one workbook to another using C#.
    This guide also covers how to copy rows, duplicate pivot table, and copy Excel
    range efficiently.
  headline: How to copy pivot table in Excel with C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: How to copy pivot table in Excel with C# and Aspose.Cells
url: /net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to copy pivot table in Excel with C# and Aspose.Cells

If you need to **copy pivot table** from one workbook to another, this tutorial shows you a complete, runnable solution. You’ll see exactly how to load a source file, define the range that contains the pivot, copy the rows (including the pivot definition), and save the result. Whether you’re automating a reporting pipeline or building a migration tool, the steps below let you duplicate a pivot table with just a few lines of C#.

Copying a pivot table is more than copying cell values; the underlying cache and field settings must travel together. The example uses the **Aspose.Cells** library because it handles pivot metadata automatically, so you don’t have to rebuild the cache manually. By the end of this guide you’ll be able to **how to copy pivot**, **copy excel range**, and **how to copy rows** safely.

## Prerequisites

Before you start, make sure you have:

- .NET 6.0 or later installed (the code also works with .NET Framework 4.7+).
- A valid Aspose.Cells for .NET license or a temporary evaluation license.
- Two Excel files: `Source.xlsx` containing the pivot table you want to duplicate, and an empty folder where `CopyWithPivot.xlsx` will be written.
- Visual Studio 2022 (or any IDE that supports C#).

## Step 1: Set up the project and add Aspose.Cells

Create a new console project and add the Aspose.Cells NuGet package:

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
dotnet add package Aspose.Cells
```

The package provides the `Workbook`, `Worksheet`, and `CellArea` classes used in the code below.

## Step 2: Load the source workbook that contains the pivot table

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the source workbook that holds the pivot you want to duplicate
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");
```

> **Why this matters:** Loading the workbook creates an in‑memory representation of all worksheets, including any hidden pivot caches. Without loading the file, you cannot reference the pivot’s range.

## Step 3: Define the cell area that covers the pivot table

You must tell Aspose.Cells which rows and columns belong to the pivot. The `CellArea` struct lets you specify a rectangular block.

```csharp
        // Define the rectangle that encloses the pivot table (adjust as needed)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,      // first row (zero‑based)
            StartColumn = 0,   // first column
            EndRow = 30,       // last row of the pivot
            EndColumn = 10     // last column of the pivot
        };
```

> **Tip:** If you’re not sure about the exact size, open the source file in Excel, select the pivot, and note the range shown in the Name Box (e.g., `A1:K31`). Convert the Excel coordinates to zero‑based indices for the code.

## Step 4: Create a new destination workbook and get its first worksheet

```csharp
        // Create an empty workbook that will receive the copied pivot
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

> **Why this step is required:** The destination workbook must exist before you can copy rows. Aspose.Cells automatically creates a default worksheet, which we’ll use as the target.

## Step 5: Copy the rows (including the pivot table) from source to destination

The `CopyRows` method copies both cell values and the underlying pivot cache.

```csharp
        // Copy rows from source to destination, preserving the pivot definition
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,      // source cells
            sourceRange.StartRow,                 // first row to copy
            sourceRange.EndRow - sourceRange.StartRow + 1, // number of rows
            destWorksheet.Cells,                  // target cells
            sourceRange.StartRow);                // target start row
```

> **How this works:**  
> - `CopyRows` takes the source worksheet, the starting row, and the count of rows to copy.  
> - It also receives the destination worksheet and the row where the copy should begin.  
> - Because the source range includes the pivot table, the method transfers the pivot’s cache, field list, and layout intact. This is the core of **how to copy pivot** without losing functionality.

### Edge case: copying a pivot that spans multiple worksheets

If the pivot’s source data lives on a different sheet than the pivot itself, the cache still follows the copy because Aspose.Cells stores the cache in the workbook, not the sheet. However, you must ensure the destination workbook contains the same source data range; otherwise the pivot will show `#REF!` errors. In such cases, copy the source data range first, then the pivot rows.

## Step 6: Save the workbook that now contains the copied pivot table

```csharp
        // Persist the destination workbook to disk
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

Running the program produces `CopyWithPivot.xlsx` with an exact replica of the original pivot table, including all slicers, filters, and calculated fields.

### Expected output

When you open `CopyWithPivot.xlsx`:

- The pivot table appears in the same position (e.g., A1:K31) as in `Source.xlsx`.
- All row and column labels, totals, and formatting are preserved.
- Refreshing the pivot shows the same data as the source, confirming that the cache was copied correctly.

## How to copy rows without a pivot (copy excel range)

If you only need to **copy excel range** without any pivot data, you can use the same `CopyRows` method but point to a range that does not contain a pivot. For example:

```csharp
// Copy a simple data table from rows 5‑15, columns A‑D
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    4,            // start at row 5 (zero‑based)
    11,           // copy 11 rows (5‑15 inclusive)
    destWorksheet.Cells,
    0);           // paste at the top of the destination sheet
```

This demonstrates **how to copy rows** for generic data, reinforcing the versatility of the same API.

## Duplicate pivot table in the same workbook (alternative approach)

Sometimes you want to **duplicate pivot table** within the same workbook rather than creating a new file. You can achieve this by copying rows to a different location:

```csharp
// Duplicate pivot table to start at row 40 in the same worksheet
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    sourceRange.StartRow,
    sourceRange.EndRow - sourceRange.StartRow + 1,
    destWorksheet.Cells,
    40); // destination start row (zero‑based)
```

After saving, the workbook will contain two identical pivots—useful for side‑by‑side comparison or creating backup copies.

## Common pitfalls and how to avoid them

| Pitfall | Why it happens | Fix |
|---------|----------------|-----|
| Pivot shows `#REF!` after copy | Source data range not present in destination workbook | Copy the source data range first, or use `CopyRows` on the source data sheet before copying the pivot |
| Formatting lost | Only values were copied (e.g., using `Copy` instead of `CopyRows`) | Always use `CopyRows` which preserves style, formatting, and pivot metadata |
| Unexpected row offset | Destination start row mismatched with source start row | Verify that `destWorksheet.Cells` start row matches the intended location |
| Large workbooks cause memory pressure | `CopyRows` loads entire worksheets into memory | Process the copy in chunks or use streaming APIs if working with >100,000 rows |

## Full, runnable example

Below is the complete program you can paste into `Program.cs` and run immediately (replace `YOUR_DIRECTORY` with an actual path on your machine).

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook containing the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");

        // 2️⃣ Define the area that encloses the pivot (adjust to your sheet)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 30,
            EndColumn = 10
        };

        // 3️⃣ Create the destination workbook (empty) and get its first sheet
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // 4️⃣ Copy rows—including the pivot cache—into the destination
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,
            sourceRange.StartRow,
            sourceRange.EndRow - sourceRange.StartRow + 1,
            destWorksheet.Cells,
            sourceRange.StartRow);

        // 5️⃣ Save the result
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

Run the program with `dotnet run`. After execution, open `CopyWithPivot.xlsx` to verify that the pivot table appears exactly as in the source file.

## Conclusion

You now know how to **copy pivot table** from one Excel workbook to another using C# and Aspose.Cells. The guide covered the complete workflow—from loading the source file, defining the pivot’s cell area, copying rows, and saving the destination workbook. You also learned **how to copy rows**, **copy excel range**, and **duplicate pivot table** within the same file, plus common pitfalls and best‑practice tips.

Ready for the next step? Try adding code to programmatically refresh the copied pivot, or explore exporting the pivot to PDF with Aspose.Cells. Experiment with different source ranges, and you’ll quickly master Excel automation in .NET.

---


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Copy Pivot Table in C# – Complete Step‑by‑Step Guide](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [copy rows excel – Preserve Pivot Table While Duplicating Rows](/cells/english/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}