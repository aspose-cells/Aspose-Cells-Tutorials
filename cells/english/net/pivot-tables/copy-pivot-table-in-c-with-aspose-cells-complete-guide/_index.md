---
category: general
date: 2026-08-11
description: Copy pivot table using C# and Aspose.Cells. Learn how to load an Excel
  workbook, duplicate a pivot table, and preserve its formatting quickly.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- duplicate pivot table excel
- move pivot table cell
- load excel workbook c#
- preserve pivot formatting
language: en
lastmod: 2026-08-11
og_description: Copy pivot table in C# with Aspose.Cells. This guide shows you how
  to load an Excel workbook, duplicate a pivot table, and keep all formatting intact.
og_image_alt: Excel worksheet after copy pivot table operation
og_title: Copy pivot table in C# – step‑by‑step Aspose.Cells tutorial
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Copy pivot table using C# and Aspose.Cells. Learn how to load an Excel
    workbook, duplicate a pivot table, and preserve its formatting quickly.
  headline: Copy pivot table in C# with Aspose.Cells – complete guide
  type: TechArticle
- description: Copy pivot table using C# and Aspose.Cells. Learn how to load an Excel
    workbook, duplicate a pivot table, and preserve its formatting quickly.
  name: Copy pivot table in C# with Aspose.Cells – complete guide
  steps:
  - name: Load Excel workbook C#
    text: Loading the workbook is the first action when you **load excel workbook
      c#**. Aspose.Cells reads the file into memory, giving you access to worksheets,
      cells, and pivot tables.
  - name: Identify and copy the pivot table range
    text: A pivot table lives inside a rectangular cell range. To **move pivot table
      cell** safely, you must copy the whole range, not just individual cells.
  - name: Save the workbook with the copied pivot table
    text: After copying, you simply save the workbook. The new file will contain both
      the original and the duplicated pivot table.
  - name: Full working example
    text: 'Putting the three steps together gives you a complete, runnable program:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Copy pivot table in C# with Aspose.Cells – complete guide
url: /net/pivot-tables/copy-pivot-table-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copy pivot table in C# with Aspose.Cells – complete guide

If you need to **copy pivot table** from one spot to another in an Excel workbook using C#, this tutorial shows you how. You’ll see a concise, end‑to‑end solution that loads the workbook, duplicates the pivot table, and preserves every formatting detail.

Working with Excel programmatically often means handling complex objects like pivot tables. In this guide you’ll learn to **duplicate pivot table excel** style without losing filters, calculated fields, or styling. The only prerequisite is a reference to the Aspose.Cells library, which gives you full control over Excel files from .NET.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 or later (the code also works on .NET Framework 4.7+)
* A valid Aspose.Cells for .NET license (you can use the free evaluation version for testing)
* An Excel file (`Source.xlsx`) that contains a pivot table you want to copy
* A development environment such as Visual Studio 2022

## How to copy pivot table with Aspose.Cells

The core steps are:

1. **Load Excel workbook C#** – open the source file.
2. **Select the range that contains the pivot table** – include the entire pivot area.
3. **Copy the range to a new location** – the pivot table remains intact.
4. **Save the workbook** – the new file contains the duplicated pivot table.

Each step is explained below with full code.

### Step 1: Load Excel workbook C#

Loading the workbook is the first action when you **load excel workbook c#**. Aspose.Cells reads the file into memory, giving you access to worksheets, cells, and pivot tables.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the source workbook that holds the original pivot table
        string sourcePath = @"C:\Data\Source.xlsx";

        // Load the workbook into memory
        Workbook workbook = new Workbook(sourcePath);
```

> **Why this matters:** Loading the workbook creates a `Workbook` object that represents the entire Excel file. All subsequent operations work on this in‑memory representation, which is faster than repeatedly accessing the file system.

### Step 2: Identify and copy the pivot table range

A pivot table lives inside a rectangular cell range. To **move pivot table cell** safely, you must copy the whole range, not just individual cells.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Define the range that encloses the pivot table.
        // Adjust "A1:G20" to match your actual pivot area.
        Range sourceRange = worksheet.Cells.CreateRange("A1:G20");

        // Copy the range to a new location, e.g., starting at I1.
        // The copy operation keeps the pivot table definition and formatting.
        sourceRange.Copy(worksheet.Cells, "I1");
```

> **Why this works:** `Range.Copy` duplicates not only the cell values but also the underlying pivot cache and formatting. This is the recommended way to **duplicate pivot table excel** without rebuilding the pivot manually.

### Step 3: Save the workbook with the copied pivot table

After copying, you simply save the workbook. The new file will contain both the original and the duplicated pivot table.

```csharp
        // Path for the new workbook that will contain the copied pivot table
        string destinationPath = @"C:\Data\CopyPivot.xlsx";

        // Save the workbook; all pivot information is preserved.
        workbook.Save(destinationPath);

        Console.WriteLine("Pivot table copied successfully to " + destinationPath);
    }
}
```

> **Why you should preserve formatting:** The `preserve pivot formatting` requirement is automatically satisfied because Aspose.Cells retains style information during the copy operation. No extra styling code is needed.

### Full working example

Putting the three steps together gives you a complete, runnable program:

```csharp
using System;
using Aspose.Cells;

class CopyPivotTableDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook that contains the pivot table
        string sourceFile = @"C:\Data\Source.xlsx";
        Workbook workbook = new Workbook(sourceFile);

        // 2️⃣ Identify the pivot table range and copy it
        Worksheet sheet = workbook.Worksheets[0];
        Range pivotRange = sheet.Cells.CreateRange("A1:G20"); // adjust as needed
        pivotRange.Copy(sheet.Cells, "I1"); // copies the pivot table intact

        // 3️⃣ Save the workbook with the duplicated pivot table
        string targetFile = @"C:\Data\CopyPivot.xlsx";
        workbook.Save(targetFile);

        Console.WriteLine($"Copy pivot table operation completed. File saved at: {targetFile}");
    }
}
```

**Expected result:**  
Open `CopyPivot.xlsx` in Excel. You will see the original pivot table unchanged and a second, identical pivot table starting at cell `I1`. All filters, calculated fields, and visual styles match the source.

## Common variations and edge cases

| Situation | How to handle it |
|-----------|------------------|
| **Pivot table spans a dynamic range** | Use `PivotTable.PivotTableRange` to obtain the exact address at runtime instead of hard‑coding `"A1:G20"`. |
| **You need to move the pivot table to another worksheet** | Call `sourceRange.Copy(otherWorksheet.Cells, "A1")` after creating `Worksheet otherWorksheet = workbook.Worksheets[workbook.Worksheets.Add()]`. |
| **Preserving only formatting, not data** | After copying, clear the data values with `targetRange.Clear(ClearOptions.Contents)` while leaving styles untouched. |
| **Large workbooks cause memory pressure** | Use `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` to let Aspose.Cells stream data. |
| **You want to rename the duplicated pivot table** | Access the new pivot via `sheet.PivotTables[sheet.PivotTables.Count - 1]` and set its `Name` property. |

These tips help you **move pivot table cell** positions, **duplicate pivot table excel** files, and keep the **preserve pivot formatting** requirement intact.

## Pro tips for reliable copying

* **Pro tip:** Always verify the source range includes the entire pivot cache. Missing a column can break the copied pivot.
* **Watch out for merged cells** inside the range; they may cause `Copy` to throw an exception. Unmerge before copying or adjust the range.
* **Performance tip:** If you only need to copy the pivot definition (no data), use `PivotTable.Clone` instead of copying the whole range.

## Conclusion

You now know how to **copy pivot table** programmatically in C# using Aspose.Cells while **preserve pivot formatting**, **load excel workbook c#**, and even **move pivot table cell** positions across worksheets. The complete solution loads the workbook, duplicates the pivot range, and saves a new file with both tables intact.

Next, you might explore **duplicate pivot table excel** scenarios such as copying between different workbooks, or automating report generation with multiple pivot tables. For deeper customization, check out Aspose.Cells’ PivotTable API to modify filters, calculated fields, or chart connections.

Happy coding, and feel free to experiment with the code to fit your specific Excel automation needs!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Create a Pivot Table in Excel Using Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)
- [Efficiently Change Excel Pivot Table Layouts Using Aspose.Cells for .NET](/cells/english/net/data-analysis/change-excel-pivot-table-layouts-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}