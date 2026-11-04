---
category: general
date: 2026-10-01
description: Learn to delete rows from an Excel table and change the Excel table name
  using C#. Step‑by‑step guide with full code and best practices.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows excel table
- change excel table name
- load excel workbook c#
- remove rows from excel table
- update excel table name
language: en
lastmod: 2026-10-01
og_description: Delete rows from an Excel table and change the Excel table name in
  C#. Follow this complete tutorial to load a workbook, modify the table, and save
  the result.
og_image_alt: Screenshot showing C# code that deletes rows from an Excel table and
  updates the table name
og_title: Delete rows from an Excel table and change its name in C# – complete guide
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn to delete rows from an Excel table and change the Excel table
    name using C#. Step‑by‑step guide with full code and best practices.
  headline: How to delete rows from an Excel table and change its name in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: How to delete rows from an Excel table and change its name in C#
url: /net/tables-and-lists/how-to-delete-rows-from-an-excel-table-and-change-its-name-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to delete rows from an Excel table and change its name in C#

If you need to **delete rows from an Excel table** while working with C#, this guide shows the exact steps required. You will see how to **load an Excel workbook in C#**, remove specific rows from a table, and then **update the Excel table name** so the file remains consistent.

The tutorial covers everything you need to know: required NuGet packages, complete runnable code, and common pitfalls such as table‑structure violations. By the end of the article you can modify any Excel table programmatically without manual intervention.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 SDK or later installed.
* Visual Studio 2022 (or any C# IDE) configured for .NET development.
* The **Aspose.Cells for .NET** library added via NuGet (`Install-Package Aspose.Cells`).
* An existing Excel workbook (`Table.xlsx`) that contains at least one worksheet with a table.

These items provide the environment needed to **load Excel workbook c#** code and execute the operations reliably.

## Step 1: Load the workbook containing the table

The first operation is opening the workbook file. Aspose.Cells reads the entire workbook into memory, giving you full control over worksheets, tables, and cell data.

```csharp
using Aspose.Cells;

string inputPath = @"C:\Data\Table.xlsx";

// Load the workbook from disk
Workbook workbook = new Workbook(inputPath);
```

*Why this matters*: Loading the workbook is the foundation for any subsequent table manipulation. The `Workbook` object exposes the `Worksheets` collection, which you will use to locate the target table.

## Step 2: Access the first worksheet and its first table

Most Excel files store tables in the first worksheet, but you can adjust the index if needed. The following code retrieves the first `Table` object.

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Retrieve the first table on that worksheet
Table table = sheet.Tables[0];
```

If the worksheet does not contain a table, `sheet.Tables.Count` will be zero and you should handle that case. Attempting to access `sheet.Tables[0]` when no tables exist throws an exception, which is why a guard clause is recommended in production code.

## Step 3: Delete rows from the Excel table

To **remove rows from an Excel table**, call `DeleteRows(startRow, totalRows)`. The `startRow` parameter is zero‑based relative to the table’s first data row (the row after the header).

```csharp
// Delete two rows starting from the second data row (index 1)
int startRow = 1;   // second row within the table
int rowsToDelete = 2;

table.DeleteRows(startRow, rowsToDelete);
```

### Why use `DeleteRows` instead of deleting worksheet rows?

`DeleteRows` updates the table’s internal range, preserving formulas, styles, and defined names that belong to the table. Directly deleting worksheet rows could break the table structure and raise an exception.

**Edge case**: If the deletion would leave the table with no data rows, Aspose.Cells throws an `ArgumentException`. Guard against this by checking `table.RowCount` before deletion.

```csharp
if (table.RowCount - rowsToDelete < 1)
{
    throw new InvalidOperationException("Cannot delete all data rows from the table.");
}
```

## Step 4: Change the Excel table name

After rows are removed, you may want to give the table a more descriptive identifier. The `Name` property sets the table’s defined name, which is used in formulas and VBA.

```csharp
// Assign a new name to the table
string newTableName = "SalesData2026";

if (workbook.Worksheets.GetDefinedNames().Any(d => d.Text == newTableName))
{
    throw new InvalidOperationException($"The name '{newTableName}' already exists as a defined name.");
}

table.Name = newTableName;
```

*Why rename?* A clear table name improves readability in formulas (`=SUM(SalesData2026[Amount])`) and avoids name collisions when multiple tables share similar purposes.

## Step 5: Save the modified workbook (optional)

Persist the changes by saving to a new file or overwriting the original. Saving to a new location is safer during development.

```csharp
string outputPath = @"C:\Data\ModifiedTable.xlsx";
workbook.Save(outputPath);
```

The `Save` method writes the updated workbook, including the changed table range and the new table name, to disk.

## Full working example

Putting all steps together yields a self‑contained program you can run immediately.

```csharp
using System;
using System.Linq;
using Aspose.Cells;

class ExcelTableModifier
{
    static void Main()
    {
        // ----- Step 1: Load workbook -----
        string inputPath = @"C:\Data\Table.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // ----- Step 2: Access worksheet and table -----
        Worksheet sheet = workbook.Worksheets[0];
        if (sheet.Tables.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        Table table = sheet.Tables[0];

        // ----- Step 3: Delete rows -----
        int startRow = 1;      // second data row (zero‑based)
        int rowsToDelete = 2;

        if (table.RowCount - rowsToDelete < 1)
        {
            Console.WriteLine("Deletion would remove all data rows; operation aborted.");
            return;
        }

        table.DeleteRows(startRow, rowsToDelete);
        Console.WriteLine($"{rowsToDelete} rows removed starting at index {startRow}.");

        // ----- Step 4: Change table name -----
        string newTableName = "SalesData2026";

        bool nameExists = workbook.Worksheets.GetDefinedNames()
                               .Any(d => d.Text.Equals(newTableName, StringComparison.OrdinalIgnoreCase));

        if (nameExists)
        {
            Console.WriteLine($"The name '{newTableName}' already exists. Choose a different name.");
            return;
        }

        table.Name = newTableName;
        Console.WriteLine($"Table renamed to '{newTableName}'.");

        // ----- Step 5: Save workbook -----
        string outputPath = @"C:\Data\ModifiedTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Modified workbook saved to '{outputPath}'.");
    }
}
```

**Expected output** (assuming the file and table exist):

```
2 rows removed starting at index 1.
Table renamed to 'SalesData2026'.
Modified workbook saved to 'C:\Data\ModifiedTable.xlsx'.
```

Running the program updates the Excel file exactly as described: rows are removed, the table name changes, and the result is saved without manual editing.

## Common questions and troubleshooting

| Question | Answer |
|----------|--------|
| *What happens if the table spans merged cells?* | `DeleteRows` respects merged ranges. If a merged cell crosses the deletion boundary, Aspose.Cells automatically adjusts the merge. Verify the result visually if you rely on complex merges. |
| *Can I delete rows from a table that is part of a pivot cache?* | Deleting rows from a source table that feeds a pivot table does **not** automatically refresh the pivot cache. Call `pivotTable.RefreshData()` after modifying the source table. |
| *Is it possible to delete rows based on a condition (e.g., value < 0)?* | Yes. Iterate through `table.ListObjects` or `table.Rows` to locate matching rows, then collect their indices and call `DeleteRows` for each range. |
| *Do I need to dispose of the `Workbook` object?* | `Workbook` implements `IDisposable`. Wrap it in a `using` block for deterministic resource release, especially when processing large files. |
| *How does this differ from using EPPlus?* | EPPlus also supports table manipulation but uses a different API (`ExcelTable`). The concepts of loading a workbook, deleting rows, and renaming the table are analogous. Choose the library that matches your licensing requirements. |

## Best practices when modifying Excel tables in C#

* **Validate indexes** – Table row indexes are zero‑based; off‑by‑one errors cause unexpected deletions.
* **Check for name collisions** – Excel does not allow duplicate defined names; always verify uniqueness before assigning a new name.
* **Back up original files** – Automated scripts can corrupt data; keep a copy of the source workbook.
* **Use `using` statements** – Guarantees that file handles are released promptly:

```csharp
using (Workbook wb = new Workbook(inputPath))
{
    // modify workbook
}
```

* **Test with edge cases** – Tables with a single data row, tables that span the entire worksheet, and tables linked to charts should be verified after changes.

## Conclusion

You now know how to **delete rows from an Excel table** and **change the Excel table name** using C#. The complete solution loads the workbook, accesses the target table, removes the desired rows, renames the table, and saves the result. Apply these techniques to automate report generation, data cleansing, or any workflow that requires programmatic Excel table management.

Next, explore related topics such as **updating cell values in an Excel table**, **adding new rows programmatically**, and **exporting table data to CSV**. Mastering these operations will give you full control over Excel files from within your C# applications.


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Rename Table in Excel with C# – Step‑by‑Step Guide](/cells/english/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/)
- [Create Excel Table in C# – Step‑by‑Step Guide](/cells/english/net/tables-and-lists/create-excel-table-in-c-step-by-step-guide/)
- [Get First Table from Excel Workbook in C# – Complete Guide](/cells/english/net/excel-autofilter-validation/get-first-table-from-excel-workbook-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}