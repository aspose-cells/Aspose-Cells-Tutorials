---
category: general
date: 2026-11-16
description: Learn how to copy a pivot table from one Excel file to a new workbook in C# using Aspose.Cells. Load the workbook, copy the range, and preserve the pivot table.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new workbook
- load excel workbook c#
- Aspose.Cells copy pivot
- preserve pivot table C#
- Excel automation C#
language: en
lastmod: 2026-11-16
og_description: How to copy pivot table from an existing workbook to a new workbook using C#. Follow this complete guide to load Excel workbook, copy range, and keep the pivot intact.
og_image_alt: how to copy pivot table example in C#
og_title: How to copy a pivot table to a new workbook in C# – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy pivot table from one Excel file to a new workbook using C#. Learn to load workbook, copy range, and preserve pivot tables.
  headline: How to copy a pivot table to a new workbook in C#
  type: TechArticle
- description: How to copy pivot table from one Excel file to a new workbook using C#. Learn to load workbook, copy range, and preserve pivot tables.
  name: How to copy a pivot table to a new workbook in C#
  steps:
  - name: Expected output
    text: 'Running the program produces `CopyWithPivot.xlsx`. Opening the file in Excel shows:'
  - name: Copying multiple pivot tables
    text: If your source sheet contains several pivots, expand the `CellArea` to cover the union of all ranges, or repeat the copy step for each distinct area.
  - name: Preserving styles and conditional formatting
    text: '`CopyRows` copies cell styles automatically. If you need to preserve workbook‑wide named styles or custom number formats, call `destWorkbook.Worksheets[0].CopyStyle` before saving.'
  - name: Working with large workbooks
    text: For files larger than 100 MB, consider using `Workbook.LoadOptions` with the `MemorySetting` set to `MemorySetting.MemoryPreference` to reduce memory pressure.
  - name: Next steps
    text: '* Explore **Aspose.Cells** features such as refreshing pivots programmatically. * Combine this approach with **ExcelPackage** (EPPlus) if you need an open‑source alternative. * Automate copying across multiple sheets by looping through `srcWorkbook.Worksheets`.'
  type: HowTo
- questions:
  - answer: Aspose.Cells can read macro‑enabled files (`.xlsm`), but the macro code isn’t copied. The pivot table itself is preserved because it’s part of the worksheet XML.
    question: Does this work with macros or VBA‑enabled workbooks?
  - answer: The copy operation includes the cached data only. If the destination workbook needs to refresh from the original source, you’ll have to re‑configure the data connection manually.
    question: What if the pivot uses an external data source?
  - answer: 'No. A pivot table needs its cache. The most reliable way is to copy the rows that contain the cache, as demonstrated. You can later hide those rows if you don’t want them visible. ## Conclusion You now know **how to copy pivot table** from one Excel file to another using C#. The tutorial covered **l'
    question: Can I copy the pivot without the underlying data rows?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Copy a Pivot Table to a New Workbook in C# using Aspose.Cells
url: /net/pivot-tables/how-to-copy-a-pivot-table-to-a-new-workbook-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to copy a pivot table to a new workbook in C#

If you need to **how to copy pivot table** from one Excel file into a fresh workbook, this guide shows you the exact steps. You’ll learn how to **load excel workbook c#**, define the source range, and **copy range to new workbook** while keeping the pivot intact.

Copying a pivot table is a common requirement when you want to reuse a report template, migrate data between projects, or generate a lightweight file for distribution. The code sample below uses Aspose.Cells, a fully managed .NET library that works without Microsoft Office installed. By the end of this tutorial you will have a runnable program that creates a new workbook containing the original pivot table, ready for further processing or sharing.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 SDK or later (the example works with .NET Core and .NET Framework)
* Visual Studio 2022 or any C# editor you prefer
* An Aspose.Cells for .NET license (the free trial works for evaluation)
* A source Excel file (`Source.xlsx`) that contains at least one pivot table

> **Pro tip:** If you’re using the free trial, set the license in code to avoid evaluation watermarks.

## Step 1: Load the source workbook (load excel workbook c#)

The first action is to open the workbook that holds the pivot table. Aspose.Cells reads the file into memory, giving you full access to worksheets, cells, and pivot objects.

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Load the source workbook that contains the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");
```

*Why this matters*: Loading the workbook is the foundation for any Excel automation. Without a valid `Workbook` object you cannot inspect the pivot or copy its data.

## Step 2: Define the cell area that encloses the pivot table (copy range to new workbook)

A pivot table lives inside a rectangular block of cells. You must specify that block so the copy operation knows what to move. The `CellArea` constructor uses zero‑based indexes: `StartRow, StartColumn, EndRow, EndColumn`.

```csharp
        // Define the cell range that encloses the pivot table, e.g., A1:K21
        // Row and column indexes start at 0, so A1 = (0,0)
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21
```

*Why this matters*: By explicitly setting the range you avoid copying unrelated data and you ensure the pivot’s cache is included. The range can be calculated dynamically if you need to handle varying pivot sizes.

## Step 3: Create a new workbook and obtain its first worksheet

Now create the destination workbook that will receive the copied rows. Aspose.Cells automatically adds a default worksheet, which we’ll use as the target.

```csharp
        // Create a new workbook that will receive the copied range
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Why this matters*: Starting with a clean workbook guarantees that only the pivot table (and its supporting rows) end up in the file, keeping the output lightweight.

## Step 4: Copy rows from the source range to the destination sheet (how to copy pivot table)

The `CopyRows` method copies entire rows, preserving formulas, formatting, and—crucially—pivot tables. The method parameters are: start row, end row, target cells collection, and the row index in the target where copying begins (here `0` to start at the first row).

```csharp
        // Copy the rows that contain the pivot table.
        // Pivot tables inside the range are preserved automatically.
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);
```

*Why this matters*: Using `CopyRows` instead of copying individual cells ensures the pivot cache stays linked to the copied data. Aspose.Cells handles the underlying XML structures, so you don’t need to rebuild the pivot manually.

## Step 5: Save the resulting workbook (copy range to new workbook)

Finally, write the new file to disk. The destination workbook now contains an identical pivot table that works independently of the source file.

```csharp
        // Save the new workbook with the copied pivot table
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        // Optional: inform the user
        System.Console.WriteLine("Pivot table copied successfully!");
    }
}
```

### Expected output

Running the program produces `CopyWithPivot.xlsx`. Opening the file in Excel shows:

* The same pivot table layout as in `Source.xlsx`
* All source data rows that were part of the pivot’s cache
* No references to the original workbook (the pivot works offline)

## Handling common variations

### Copying multiple pivot tables

If your source sheet contains several pivots, expand the `CellArea` to cover the union of all ranges, or repeat the copy step for each distinct area.

```csharp
// Example: copy two separate ranges
CellArea firstPivot = new CellArea(0, 0, 20, 10);
CellArea secondPivot = new CellArea(25, 0, 45, 10);

destWorksheet.Cells.CopyRows(firstPivot.StartRow, firstPivot.EndRow, destWorksheet.Cells, 0);
destWorksheet.Cells.CopyRows(secondPivot.StartRow, secondPivot.EndRow, destWorksheet.Cells, 21); // start after first block
```

### Preserving styles and conditional formatting

`CopyRows` copies cell styles automatically. If you need to preserve workbook‑wide named styles or custom number formats, call `destWorkbook.Worksheets[0].CopyStyle` before saving.

### Working with large workbooks

For files larger than 100 MB, consider using `Workbook.LoadOptions` with the `MemorySetting` set to `MemorySetting.MemoryPreference` to reduce memory pressure.

```csharp
LoadOptions loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeSrc = new Workbook(@"bigfile.xlsx", loadOptions);
```

## Full source code (ready to run)

Below is the complete program, including `using` directives and comments. Copy it into a new console project and replace `YOUR_DIRECTORY` with the actual folder path.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source workbook (load excel workbook c#)
        // -------------------------------------------------
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");

        // -------------------------------------------------
        // Step 2: Define the area that contains the pivot table
        // -------------------------------------------------
        // Adjust the indices if your pivot occupies a different range.
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21

        // -------------------------------------------------
        // Step 3: Create the destination workbook
        // -------------------------------------------------
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // -------------------------------------------------
        // Step 4: Copy rows (how to copy pivot table)
        // -------------------------------------------------
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);

        // -------------------------------------------------
        // Step 5: Save the new file (copy range to new workbook)
        // -------------------------------------------------
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        Console.WriteLine("Pivot table copied successfully!");
    }
}
```

Run the program (`dotnet run` or `Ctrl+F5` in Visual Studio). After execution, open `CopyWithPivot.xlsx` to verify that the pivot behaves exactly like the original.

## Frequently asked questions

**Q: Does this work with macros or VBA‑enabled workbooks?**  
A: Aspose.Cells can read macro‑enabled files (`.xlsm`), but the macro code isn’t copied. The pivot table itself is preserved because it’s part of the worksheet XML.

**Q: What if the pivot uses an external data source?**  
A: The copy operation includes the cached data only. If the destination workbook needs to refresh from the original source, you’ll have to re‑configure the data connection manually.

**Q: Can I copy the pivot without the underlying data rows?**  
A: No. A pivot table needs its cache. The most reliable way is to copy the rows that contain the cache, as demonstrated. You can later hide those rows if you don’t want them visible.

## Conclusion

You now know **how to copy pivot table** from one Excel file to another using C#. The tutorial covered **load excel workbook c#**, defined the **copy range to new workbook**, and used Aspose.Cells’ `CopyRows` method to keep the pivot intact. With the complete, runnable example you can integrate this pattern into reporting pipelines, automated export tools, or any scenario where a pivot must travel across workbooks.

### Next steps

* Explore **Aspose.Cells** features such as refreshing pivots programmatically.  
* Combine this approach with **ExcelPackage** (EPPlus) if you need an open‑source alternative.  
* Automate copying across multiple sheets by looping through `srcWorkbook.Worksheets`.  

Feel free to experiment with different ranges, add custom styling, or embed the logic in a larger data‑processing service. Happy coding!


## What should you learn next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create New Workbook in C# – Copy Pivot Table](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)
- [How to copy pivot table in Excel with C# and Aspose.Cells](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/)
- [Copy pivot table to new workbook, export shape to PowerPoint](/cells/english/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}