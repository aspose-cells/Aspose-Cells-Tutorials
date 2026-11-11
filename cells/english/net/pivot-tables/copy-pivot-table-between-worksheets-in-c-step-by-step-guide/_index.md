---
category: general
date: 2026-10-01
description: Copy pivot table in C# using Aspose.Cells. Learn how to load Excel workbook,
  define ranges, and copy range to worksheet while preserving the pivot.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- load excel workbook c#
- copy range to worksheet
language: en
lastmod: 2026-10-01
og_description: Copy pivot table in C# with Aspose.Cells. This tutorial shows how
  to load an Excel workbook, copy range to worksheet, and retain the pivot table.
og_image_alt: Screenshot of C# code copying a pivot table between worksheets
og_title: Copy pivot table in C# – complete programming guide
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Copy pivot table in C# using Aspose.Cells. Learn how to load Excel
    workbook, define ranges, and copy range to worksheet while preserving the pivot.
  headline: Copy pivot table between worksheets in C# – step‑by‑step guide
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Copy pivot table between worksheets in C# – step‑by‑step guide
url: /net/pivot-tables/copy-pivot-table-between-worksheets-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copy pivot table between worksheets in C# – step‑by‑step guide

If you need to **copy pivot table** from one sheet to another in a .xlsx file, this guide shows you exactly how to do it with C#. You will learn how to **load Excel workbook C#**, define matching ranges, and **copy range to worksheet** while keeping the pivot intact. The solution works with Aspose.Cells .NET, a library that preserves pivot definitions during copy operations.

## Load Excel workbook in C#

Before you can manipulate any data, you must load the source workbook into memory. Aspose.Cells provides the `Workbook` class, which reads the file and builds an object model representing worksheets, cells, and pivot tables.

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Path to the source workbook that contains the original pivot table
        const string sourcePath = @"YOUR_DIRECTORY\Input.xlsx";

        // Load the workbook – this is the step that answers “load excel workbook c#”
        Workbook workbook = new Workbook(sourcePath);
        // The workbook now holds all worksheets, including any pivot tables.
```

**Why this matters:** Loading the workbook once gives you a single source of truth. All subsequent operations work on this in‑memory representation, which is faster than repeatedly opening the file.

## Define source and destination ranges

A pivot table lives inside a rectangular block of cells. To copy it, you create a `Range` object that encloses the entire block. The same dimensions must exist on the target sheet; otherwise the copy will truncate data.

```csharp
        // Step 2: Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.Worksheets[0];

        // Step 3: Define the exact range that includes the pivot table.
        // Adjust "A1:G20" to match the actual size of your pivot.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

> **Tip:** If you are unsure about the range, use `sourceSheet.PivotTables[0].DataRange.FirstCell.Name` and `LastCell.Name` to build the address programmatically.

## Add a new worksheet and prepare the destination range

Now create a fresh worksheet that will host the copied pivot. The destination range must have the same address as the source range.

```csharp
        // Step 4: Add a new worksheet for the copy
        Worksheet destinationSheet = workbook.Worksheets.Add();

        // Create a matching range on the new sheet
        Range destinationRange = destinationSheet.Cells.CreateRange("A1:G20");
```

**Why this step is required:** Pivot tables are tied to a worksheet context. Copying the range without a destination sheet would throw an exception because the target cells do not exist.

## Copy range to worksheet while preserving the pivot

Aspose.Cells’ `Range.Copy` method copies not only raw values but also underlying objects such as pivot tables, charts, and named ranges. This is the core of **how to copy pivot** without losing its definition.

```csharp
        // Step 5: Perform the copy – the pivot table definition travels with the cells
        sourceRange.Copy(destinationRange);
```

> **Pro tip:** After the copy, you can verify that the pivot appears in `destinationSheet.PivotTables`. The `Copy` method retains the source pivot’s data source, filters, and layout.

## Save the workbook with the copied pivot table

Finally, write the modified workbook to a new file. The resulting file contains the original sheet plus a duplicate sheet with an identical pivot table.

```csharp
        // Step 6: Save the workbook under a new name
        const string outputPath = @"YOUR_DIRECTORY\CopyWithPivot.xlsx";
        workbook.Save(outputPath);

        // Optional: Inform the user
        System.Console.WriteLine($"Pivot table copied successfully to {outputPath}");
    }
}
```

When you open `CopyWithPivot.xlsx` in Excel, you will see two sheets: the original and the new one, each showing the same pivot table with the same filters and calculated fields.

## Common pitfalls and best practices

| Issue | Why it happens | How to avoid it |
|-------|----------------|-----------------|
| **Range does not cover the whole pivot** | The pivot’s data source may extend beyond the selected cells, causing missing fields. | Use the pivot’s `DataRange` property to generate the address automatically. |
| **Destination sheet already contains a pivot with the same name** | Aspose.Cells throws a naming conflict. | Rename the destination pivot after copying: `destinationSheet.PivotTables[0].Name = "PivotCopy";` |
| **Large workbooks cause memory pressure** | Loading the entire workbook into memory can be heavy. | Use `LoadOptions` to load only required worksheets if you do not need the whole file. |
| **Copying across different Excel versions** | Some older versions do not support certain pivot features. | Save the result as `.xlsx` (Office Open XML) to guarantee compatibility. |

## Extending the solution

Once you have a reliable **copy pivot table** routine, you can build more sophisticated workflows:

* **Batch copy:** Loop through all worksheets that contain pivots and duplicate them into a summary workbook.
* **Dynamic range detection:** Replace the hard‑coded `"A1:G20"` with code that discovers the pivot’s extents automatically.
* **Pivot refresh:** After copying, call `destinationSheet.PivotTables[0].RefreshData();` to ensure the pivot reflects any changes in the underlying data source.

## Expected output

Running the program with a valid `Input.xlsx` produces `CopyWithPivot.xlsx`. Opening the file shows:

```
Sheet1 (original)          Sheet2 (copy)
+----------------------+   +----------------------+
| Pivot Table: Sales   |   | Pivot Table: Sales   |
| – Region, Product    |   | – Region, Product    |
| – Sum of Amount      |   | – Sum of Amount      |
+----------------------+   +----------------------+
```

Both sheets display identical pivot layouts, filters, and calculated fields.

## Conclusion

You now know how to **copy pivot table** between worksheets in C# using Aspose.Cells. The tutorial covered loading the workbook, defining matching ranges, performing the copy, and saving the result—all while preserving the pivot’s full definition. Apply the same pattern to automate reporting, create template sheets, or build data‑migration tools.

**Next steps:**  
* Explore the **how to copy pivot** variations for multiple pivots in one sheet.  
* Combine this technique with **load Excel workbook C#** automation scripts to process batches of files.  
* Experiment with the **copy range to worksheet** method on charts, tables, and conditional formats for a complete workbook cloning solution.  

Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [How to copy range with pivot tables in C# – Complete Guide](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}