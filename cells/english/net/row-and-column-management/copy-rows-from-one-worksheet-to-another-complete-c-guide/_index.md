---
category: general
date: 2026-07-29
description: Copy rows from one worksheet to another and learn how to load Excel workbook
  programmatically using Aspose.Cells in a step‑by‑step tutorial.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy rows from one worksheet to another
- load excel workbook programmatically
- Aspose.Cells copy rows
- C# Excel automation
- worksheet data transfer
language: en
lastmod: 2026-07-29
og_description: Copy rows from one worksheet to another using Aspose.Cells. Learn
  to load Excel workbook programmatically and preserve pivot tables in just a few
  lines of C#.
og_image_alt: Screenshot showing C# code that copies rows from one worksheet to another
  while preserving pivot tables
og_title: Copy rows from one worksheet to another – C# Excel Automation Guide
schemas:
- author: Aspose
  dateModified: '2026-07-29'
  description: Copy rows from one worksheet to another and learn how to load Excel
    workbook programmatically using Aspose.Cells in a step‑by‑step tutorial.
  headline: Copy rows from one worksheet to another – Complete C# Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Replace `destinationWorkbook.Worksheets[0]` with `destinationWorkbook.Worksheets["TargetSheet"]`
      (create the sheet first if it doesn’t exist).
    question: Can I copy to a specific worksheet instead of the first one?
  - answer: Use `CopyRows` with the overload that accepts a `CopyRowsOptions` object
      and set `PasteType` to `PasteType.Values`.
    question: What if I need to copy only values, not formulas?
  - answer: Aspose.Cells supports **streaming** via `LoadOptions` with `MemorySetting.MemoryPreference`.
      Load the source workbook with a lower memory footprint and the copy operation
      will still be efficient.
    question: How do I handle large files without exhausting memory?
  - answer: When you set the `true` flag, the pivot cache is duplicated, so the new
      workbook’s pivots reference the copied data, not the original file.
    question: Do pivot tables stay linked to the original data source?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Copy rows from one worksheet to another – Complete C# Guide
url: /net/row-and-column-management/copy-rows-from-one-worksheet-to-another-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copy rows from one worksheet to another – Complete C# Guide

Ever needed to **copy rows from one worksheet to another** but weren’t sure how to keep the formulas and pivot tables intact? You’re not alone. In many reporting pipelines we have to pull a slice of data from a master sheet and drop it into a fresh workbook for downstream processing. The good news? With Aspose.Cells you can do it programmatically, and the whole operation takes just a handful of lines.

In this tutorial we’ll walk through loading an Excel workbook programmatically, selecting a range, and then copying those rows to a brand‑new workbook while preserving any embedded pivot tables. By the end you’ll have a reusable snippet that you can drop into any C# project—no manual copy‑pasting required.

## What You’ll Achieve

- **Load Excel workbook programmatically** using Aspose.Cells’ `Workbook` class.  
- Define a **cell area** that contains the rows you want to move.  
- **Copy rows from one worksheet to another** with a single method call that keeps pivot tables alive.  
- Save the result to a new file ready for distribution or further processing.

### Prerequisites

- .NET 6.0 or later (the code works on .NET Core and .NET Framework alike).  
- A valid Aspose.Cells license (or a temporary evaluation key).  
- Two folders on disk: one for the source workbook (`Source.xlsx`) and one for the destination (`Destination.xlsx`).  

If you’ve got those, let’s dive in.

## Step 1: Load Excel workbook programmatically

First thing’s first—before you can copy anything you need to bring the source file into memory. Aspose.Cells makes this a breeze:

```csharp
using Aspose.Cells;

// Load the source workbook from disk
Workbook sourceWorkbook = new Workbook(@"C:\Data\Source.xlsx");
```

> **Why this matters:** Loading the workbook programmatically gives you full control over the file’s contents without ever opening Excel on the server. It also avoids COM interop headaches and works in headless environments like CI pipelines.

## Step 2: Define the source range that contains the rows

Next, pinpoint exactly which rows you want to transfer. The `CellArea` object lets you specify a rectangular block using the top‑left and bottom‑right cell addresses:

```csharp
// Define the area A1:H20 – adjust as needed
CellArea sourceRange = CellArea.CreateCellArea("A1", "H20");
```

> **Pro tip:** If your data size changes dynamically, you can calculate `EndRow` with `sourceWorksheet.Cells.MaxDataRow` to always capture the full table.

## Step 3: Create a fresh workbook for the destination

Now spin up an empty workbook that will receive the copied rows. This workbook starts with a single worksheet by default:

```csharp
// Create a new, empty workbook
Workbook destinationWorkbook = new Workbook();
```

> **Why a new workbook?** Starting clean ensures you don’t accidentally overwrite existing data and gives you a predictable environment for testing.

## Step 4: Copy rows from one worksheet to another (preserving pivot tables)

Here’s the heart of the tutorial. The `CopyRows` method copies the selected rows and, when you pass `true` as the last argument, it also copies any pivot tables that live inside the range:

```csharp
// Perform the copy operation
destinationWorkbook.Worksheets[0].Cells.CopyRows(
    sourceWorkbook.Worksheets[0],      // source worksheet
    sourceRange.StartRow,              // first row to copy (0‑based)
    sourceRange.EndRow,                // last row to copy (inclusive)
    destinationWorkbook.Worksheets[0].Cells, // target worksheet
    0,                                 // target start row (top of sheet)
    true);                             // preserve pivot tables
```

### What’s happening under the hood?

- **Source worksheet**: `sourceWorkbook.Worksheets[0]` points to the first sheet in the source file.  
- **Row indices**: Aspose.Cells uses zero‑based indexing, so `StartRow` and `EndRow` correspond to the rows you defined in `sourceRange`.  
- **Destination start row**: We start at row 0 in the new sheet, effectively placing the copied block at the very top.  
- **`true` flag**: This is the magic switch that tells Aspose.Cells to clone any pivot tables found inside the copied rows, preserving their cache and connections.

> **Edge case warning:** If the source range contains merged cells that span outside the defined area, those merges will be truncated. To keep them intact, expand the range to fully cover the merged region.

## Step 5: Save the destination workbook

Finally, write the new file to disk. You can choose any folder you like; just make sure the process has write permissions:

```csharp
// Save the result
destinationWorkbook.Save(@"C:\Data\Destination.xlsx");
```

When you open `Destination.xlsx` you’ll see rows A1‑H20 duplicated, complete with any pivot tables that were originally embedded. The rest of the workbook remains empty, ready for you to add more sheets or data later.

## Full Working Example

Putting it all together, here’s the complete, runnable program:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook programmatically
        Workbook sourceWorkbook = new Workbook(@"C:\Data\Source.xlsx");

        // 2️⃣ Define the source range (adjust as needed)
        CellArea sourceRange = CellArea.CreateCellArea("A1", "H20");

        // 3️⃣ Create a new destination workbook
        Workbook destinationWorkbook = new Workbook();

        // 4️⃣ Copy rows from one worksheet to another, preserving pivot tables
        destinationWorkbook.Worksheets[0].Cells.CopyRows(
            sourceWorkbook.Worksheets[0],
            sourceRange.StartRow,
            sourceRange.EndRow,
            destinationWorkbook.Worksheets[0].Cells,
            0,
            true);

        // 5️⃣ Save the result
        destinationWorkbook.Save(@"C:\Data\Destination.xlsx");

        Console.WriteLine("Rows successfully copied! Check C:\\Data\\Destination.xlsx");
    }
}
```

**Expected output** (console):

```
Rows successfully copied! Check C:\Data\Destination.xlsx
```

Open the destination file and verify that the data, formatting, and pivot tables look exactly like they did in the source. If you see any missing data, double‑check that the `sourceRange` fully encloses the relevant rows.

## Common Questions & Tips

- **Can I copy to a specific worksheet instead of the first one?**  
  Absolutely. Replace `destinationWorkbook.Worksheets[0]` with `destinationWorkbook.Worksheets["TargetSheet"]` (create the sheet first if it doesn’t exist).

- **What if I need to copy only values, not formulas?**  
  Use `CopyRows` with the overload that accepts a `CopyRowsOptions` object and set `PasteType` to `PasteType.Values`.

- **How do I handle large files without exhausting memory?**  
  Aspose.Cells supports **streaming** via `LoadOptions` with `MemorySetting.MemoryPreference`. Load the source workbook with a lower memory footprint and the copy operation will still be efficient.

- **Do pivot tables stay linked to the original data source?**  
  When you set the `true` flag, the pivot cache is duplicated, so the new workbook’s pivots reference the copied data, not the original file.

## Wrapping Up

You now know how to **copy rows from one worksheet to another** while keeping any pivot tables intact, and you’ve seen how to **load Excel workbook programmatically** using Aspose.Cells. This pattern is a solid foundation for building automated reporting pipelines, data migration scripts, or any scenario where you need to splice Excel data on the fly.

What’s next? Try extending the snippet to:

- Loop over multiple source ranges and aggregate them into a single destination file.  
- Apply conditional formatting after the copy to highlight key metrics.  
- Export the final workbook to PDF or CSV for downstream consumption.

Feel free to experiment, and if you hit a snag, drop a comment below. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Copy Rows in Excel Using Aspose.Cells for .NET&#58; A C# Guide](/cells/english/net/worksheet-management/copy-rows-excel-aspose-cells-net-guide/)
- [Copy Worksheet from One Workbook to Another using Aspose.Cells](/cells/english/net/worksheet-value-operations/copy-worksheet-between-workbooks/)
- [How to Export Visible Excel Rows Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}