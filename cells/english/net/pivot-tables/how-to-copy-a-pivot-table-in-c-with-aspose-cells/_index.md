---
category: general
date: 2026-09-27
description: Learn how to copy a pivot table in C# using Aspose.Cells. Includes copy
  rows with formatting, copy pivot table to another sheet, and export pivot table
  to a new workbook.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy rows with formatting
- copy pivot table to another sheet
- how to copy excel rows
- export pivot table to new workbook
language: en
lastmod: 2026-09-27
og_description: How to copy a pivot table in C# using Aspose.Cells. Follow the step‑by‑step
  guide to copy rows with formatting, move a pivot table to another sheet, and export
  it to a new workbook.
og_image_alt: Excel sheet showing a copied pivot table after using Aspose.Cells
og_title: How to copy a pivot table in C# – full Aspose.Cells guide
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to copy a pivot table in C# using Aspose.Cells. Includes
    copy rows with formatting, copy pivot table to another sheet, and export pivot
    table to a new workbook.
  headline: How to copy a pivot table in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot table
title: How to copy a pivot table in C# with Aspose.Cells
url: /net/pivot-tables/how-to-copy-a-pivot-table-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to copy a pivot table in C# with Aspose.Cells

If you need to **copy a pivot table** from one worksheet to another, learning **how to copy pivot table** in C# with Aspose.Cells can save you hours of manual work. The approach also lets you **copy rows with formatting**, keep the pivot cache intact, and even **export pivot table to a new workbook** when you need a standalone file.

This tutorial walks you through the complete workflow:

* create a workbook,  
* copy the pivot‑table range while preserving formatting,  
* place the copied data on a new sheet, and  
* save the result as a separate file.

You’ll see why the built‑in `CopyRows` method is the most reliable way to **copy pivot table to another sheet**, and you’ll get tips for handling edge cases such as hidden rows or external data sources.

## Prerequisites

Before you start, make sure you have:

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 or later | Aspose.Cells supports .NET 6+ and gives the best performance. |
| Visual Studio 2022 (or any C# IDE) | You need an editor that can restore NuGet packages. |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | This library provides the `CopyRows` API used in the example. |
| A source Excel file (`source.xlsx`) that contains a pivot table in the range `A1:G20` | The code copies this specific range; adjust the range if your pivot table is larger. |

Install the library with the NuGet CLI or Package Manager Console:

```bash
dotnet add package Aspose.Cells
```

## Step 1: Load the workbook that contains the pivot table

The first line creates a `Workbook` object that represents the entire Excel file. Loading the file once gives you read/write access to every worksheet.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Why this step matters** – Without loading the workbook, none of the subsequent `CopyRows` calls can reference the source data or the pivot cache.

## Step 2: Prepare source and destination worksheets

You need a destination sheet where the copied pivot table will live. The code below fetches the first worksheet (where the original pivot table resides) and adds a new sheet named **Copy**.

```csharp
// Get the source worksheet (index 0 = first sheet)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a new worksheet that will receive the copied rows
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
```

> **Pro tip:** If the destination sheet already exists, call `Worksheets.RemoveAt(index)` first to avoid duplicate names.

## Step 3: Define the cell area that encloses the pivot table

A `CellArea` object describes the top‑left and bottom‑right cells of the range you want to move. In this example the pivot table occupies `A1:G20`. Adjust the coordinates for larger tables.

```csharp
// Define the range that includes the pivot table (A1:G20)
CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");
```

## Step 4: Copy rows with formatting and preserve the pivot cache

The `CopyRows` method copies **rows** from the source sheet to the destination sheet. By passing `CopyOptions.CopyAll` you ensure that values, formatting, charts, and embedded objects—all of which are part of a pivot table—are transferred.

```csharp
// Copy the rows from the source area to the destination sheet
sourceSheet.CopyRows(
    sourceArea.StartRow,          // start row in the source sheet
    destinationSheet,            // target worksheet
    0,                            // start row in the destination sheet
    sourceArea.RowCount,          // number of rows to copy
    CopyOptions.CopyAll);        // copy everything (values, formats, objects, etc.)
```

### Why `CopyRows` works better than `Copy` for pivot tables

* `CopyRows` respects the internal pivot cache, so the copied pivot table remains functional.
* It preserves **copy rows with formatting** exactly as they appear in the original sheet.
* Unlike a simple `Copy` of a range, it also moves hidden rows and any associated slicers.

## Step 5: Save the workbook with the copied pivot table

Finally, write the modified workbook to disk. The new file contains the original sheet plus a **Copy** sheet that holds a fully functional duplicate of the original pivot table.

```csharp
// Save the workbook to a new file
workbook.Save(@"YOUR_DIRECTORY\pivot_copied.xlsx");
```

### Expected result

When you open `pivot_copied.xlsx`:

* Sheet **Sheet1** still contains the original data and pivot table.
* Sheet **Copy** shows an identical pivot table with the same layout, filters, and formatting.
* All formulas and data connections remain intact because the pivot cache was copied together with the rows.

## How to copy pivot table to another sheet in the same workbook

If you only need the pivot table in a different existing sheet (e.g., “Report”), replace the destination creation step with a reference to the target sheet:

```csharp
Worksheet destinationSheet = workbook.Worksheets["Report"]; // existing sheet
sourceSheet.CopyRows(sourceArea.StartRow, destinationSheet, 0,
                     sourceArea.RowCount, CopyOptions.CopyAll);
```

This snippet demonstrates **copy pivot table to another sheet** without creating a new worksheet.

## Export pivot table to new workbook

Sometimes you want the pivot table in a completely separate file. After the copy operation, you can remove all worksheets except the one that holds the copied pivot table and then save:

```csharp
// Keep only the copied sheet
for (int i = workbook.Worksheets.Count - 1; i >= 0; i--)
{
    if (workbook.Worksheets[i].Name != "Copy")
        workbook.Worksheets.RemoveAt(i);
}

// Save as a new workbook containing only the pivot table
workbook.Save(@"YOUR_DIRECTORY\pivot_only.xlsx");
```

Now `pivot_only.xlsx` contains a single sheet with the duplicated pivot table, fulfilling the **export pivot table to new workbook** requirement.

## How to copy excel rows without losing formatting

The same `CopyRows` call works for any range, not just pivot tables. If you need to **copy excel rows** that include conditional formatting, data validation, or merged cells, use the same method:

```csharp
// Example: copy rows 30‑40 from Sheet1 to Sheet2
sourceSheet.CopyRows(29, // zero‑based index for row 30
                     workbook.Worksheets["Sheet2"],
                     0,
                     11, // rows 30‑40 = 11 rows
                     CopyOptions.CopyAll);
```

Because `CopyOptions.CopyAll` transfers everything, the destination rows look exactly like the source rows.

## Common pitfalls and how to avoid them

| Pitfall | Symptom | Fix |
|---------|---------|-----|
| Source range does not include the whole pivot table | The copied pivot table appears truncated. | Verify the `CellArea` covers all rows/columns of the pivot table. |
| Destination sheet already contains data | Overwritten rows cause data loss. | Choose a fresh sheet or start copying at a higher row index. |
| Pivot table uses an external data source | The copy loses its connection. | After copying, call `pivotTable.RefreshData()` to re‑establish the link. |
| Hidden rows are omitted | Some rows disappear in the copy. | `CopyRows` automatically copies hidden rows; ensure you are not using `CopyOptions.CopyValuesOnly`. |

## Full, runnable example

Below is a self‑contained program you can paste into a new console project. It demonstrates every step discussed above.

```csharp
using System;
using Aspose.Cells;

namespace PivotTableCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains the pivot table
            string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2️⃣ Get source and destination worksheets
            Worksheet sourceSheet = workbook.Worksheets[0]; // first sheet
            Worksheet destinationSheet = workbook.Worksheets.Add("Copy");

            // 3️⃣ Define the cell area that holds the pivot table (A1:G20)
            CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");

            // 4️⃣ Copy rows with formatting and keep the pivot cache
            sourceSheet.CopyRows(
                sourceArea.StartRow,      // start row index (0‑based)
                destinationSheet,        // target sheet
                0,                        // start row in destination
                sourceArea.RowCount,      // number of rows to copy
                CopyOptions.CopyAll);    // copy everything

            // 5️⃣ Save the workbook with the copied pivot table
            string destPath = @"YOUR_DIRECTORY\pivot_copied.xlsx";
            workbook.Save(destPath);

            Console.WriteLine("Pivot table copied successfully to " + destPath);
        }
    }
}
```

**Running the program** creates `pivot_copied.xlsx` with a duplicate of the original pivot table on a new sheet named **Copy**.

## Conclusion

You now know **how to copy a pivot table** in C# using


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy Pivot Table in C# – Complete Step‑by‑Step Guide](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [How to copy range with pivot tables in C# – Complete Guide](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}