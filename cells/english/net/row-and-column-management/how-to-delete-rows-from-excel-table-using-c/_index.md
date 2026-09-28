---
category: general
date: 2026-09-27
description: Learn how to delete rows from Excel table in C# with a step‑by‑step guide
  that also shows how to load Excel workbook C# quickly.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from Excel table
- load Excel workbook C#
language: en
lastmod: 2026-09-27
og_description: Delete rows from Excel table in C# with a clear example. This tutorial
  also covers how to load Excel workbook C# and handle common edge cases.
og_image_alt: Screenshot illustrating delete rows from Excel table using C# code
og_title: Delete rows from Excel table in C# – complete code guide
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  headline: How to delete rows from Excel table using C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  name: How to delete rows from Excel table using C#
  steps:
  - name: What if the table has a different name or position?
    text: '* **Named table:** Use `ws.ListObjects["MyTableName"]` instead of the index.
      * **Multiple tables:** Loop through `ws.ListObjects` and pick the one that matches
      a condition (e.g., column header names). * **Dynamic row count:** You can compute
      `rowCount` at runtime by inspecting `ws.ListObjects[0].Dat'
  - name: Edge‑case handling
    text: '| Situation | Recommended code change | |----------------------------------------|--------------------------------------------------------------|
      | Table is empty or has fewer rows | Check `ws.ListObjects[0].DataRange.RowCount`
      before deleting. | | Rows to delete exceed table size | Clamp `rowCount`'
  - name: How do I delete rows from **all** tables in a workbook?
    text: '```csharp foreach (Worksheet sheet in workbook.Worksheets) { foreach (ListObject
      tbl in sheet.ListObjects) { // Example: delete the first data row of each table
      if (tbl.DataRange.RowCount > 1) tbl.DeleteRows(1, 1); } } ```'
  - name: Can I delete rows based on a **cell value**?
    text: 'Yes. Scan the `DataRange` for matching cells, collect their zero‑based
      indices, then delete in descending order:'
  - name: What if I need to **preserve formatting**?
    text: '`DeleteRows` removes the entire row from the table but retains the table’s
      style for remaining rows. If you need to keep specific formatting on a row you’re
      deleting, copy the style to another row before deletion.'
  - name: Does this work with **.xls** (Excel 97‑2003) files?
    text: Yes. Aspose.Cells automatically detects the file format, so the same code
      works with `.xls`. Just change the file extension in the `Workbook` constructor.
  - name: Next steps
    text: '* Explore **ClosedXML** or **EPPlus** if you prefer a fully open‑source
      stack. * Combine row deletion with **data validation** to clean spreadsheets
      before importing into a database. * Automate the process for a folder of workbooks
      using `Directory.GetFiles` and a loop.'
  type: HowTo
tags:
- Excel
- C#
- .NET
title: How to delete rows from Excel table using C#
url: /net/row-and-column-management/how-to-delete-rows-from-excel-table-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Delete rows from Excel table in C# – complete programming guide

If you need to **delete rows from Excel table** in a .xlsx file, this tutorial shows you exactly how to do it with C#. You’ll see a concise, runnable example that loads an Excel workbook, removes specific rows from the first table, and saves the result. The approach works with the popular Aspose.Cells library and can be adapted to other .NET Excel APIs.

Removing rows from a table is a common task when cleaning imported data, trimming report sections, or automating spreadsheet updates. By the end of this guide you’ll be able to **load Excel workbook C#**, locate a table (ListObject), delete any rows you choose, and write the modified file back to disk.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 or later installed (the code also works with .NET Framework 4.7+).
* A reference to the **Aspose.Cells** NuGet package (or any compatible library that exposes `Workbook`, `Worksheet`, and `ListObject` types).
* An input file named `input.xlsx` placed in a folder you can reference from your project.
* Basic familiarity with C# syntax and Visual Studio (or your preferred IDE).

> **Pro tip:** If you prefer an open‑source alternative, the same logic can be applied with **ClosedXML** – just replace the Aspose‑specific classes with `XLWorkbook`, `IXLWorksheet`, and `IXLTable`.

## Step 1: Load the Excel workbook in C#

The first operation is to read the source file into memory. Loading the workbook is cheap for typical spreadsheet sizes and gives you full access to worksheets, tables, and cell values.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook
// Replace YOUR_DIRECTORY with the actual folder path, e.g. @"C:\Data"
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

*Why this matters:* `Workbook` parses the Open XML structure of the .xlsx file, exposing a collection of `Worksheet` objects. If the file cannot be found, Aspose throws a `FileNotFoundException`, so ensure the path is correct.

## Step 2: Access the target worksheet

Most spreadsheets contain multiple sheets; you need to pick the one that holds the table you want to modify. Here we use the first sheet (`Worksheets[0]`), which is a safe default for simple files.

```csharp
// Step 2: Access the first worksheet
Worksheet ws = workbook.Worksheets[0];
```

*Why this matters:* `Worksheet` is the container for tables (`ListObjects`). Accessing the correct sheet prevents accidental changes to unrelated data.

## Step 3: Delete rows from Excel table

Excel tables are represented by `ListObject` objects. The first table on the sheet is `ListObjects[0]`. The `DeleteRows(startIndex, rowCount)` method removes rows **relative to the table’s data area**, not the worksheet’s absolute row numbers.  

In this example we delete the second and third rows of the table (the header is row 0, so we start at index 1).

```csharp
// Step 3: Delete rows 1 and 2 from the first table (ListObject)
// The first row (index 0) is the header, so we start at index 1
ws.ListObjects[0].DeleteRows(1, 2);
```

### What if the table has a different name or position?

* **Named table:** Use `ws.ListObjects["MyTableName"]` instead of the index.
* **Multiple tables:** Loop through `ws.ListObjects` and pick the one that matches a condition (e.g., column header names).
* **Dynamic row count:** You can compute `rowCount` at runtime by inspecting `ws.ListObjects[0].DataRange.RowCount`.

### Edge‑case handling

| Situation                              | Recommended code change                                      |
|----------------------------------------|--------------------------------------------------------------|
| Table is empty or has fewer rows      | Check `ws.ListObjects[0].DataRange.RowCount` before deleting. |
| Rows to delete exceed table size       | Clamp `rowCount` to `DataRange.RowCount - startIndex`.       |
| Need to delete rows based on a condition (e.g., value in column C) | Iterate `DataRange.Rows` and collect matching indices, then delete in reverse order to keep indices stable. |

## Step 4: Save the modified workbook

After the deletion, write the workbook back to a new file (or overwrite the original if you prefer). Saving creates a fresh .xlsx that reflects the updated table.

```csharp
// Step 4: Save the modified workbook
workbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

*Why this matters:* `Save` serializes the in‑memory representation to disk. If you need to preserve the original file, always write to a different path.

## Full, runnable example

Putting all steps together gives you a self‑contained program you can copy, paste, and run.

```csharp
using System;
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Adjust the folder path as needed
        const string folder = @"YOUR_DIRECTORY";

        // Load the workbook (load Excel workbook C#)
        Workbook workbook = new Workbook($"{folder}\\input.xlsx");

        // Access the first worksheet
        Worksheet ws = workbook.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (ws.ListObjects.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Delete rows 1 and 2 from the first table (skip header)
        ListObject table = ws.ListObjects[0];
        int rowsToDelete = Math.Min(2, table.DataRange.RowCount - 1); // guard against short tables
        if (rowsToDelete > 0)
        {
            table.DeleteRows(1, rowsToDelete);
            Console.WriteLine($"Deleted {rowsToDelete} row(s) from table \"{table.Name}\".");
        }
        else
        {
            Console.WriteLine("Table does not have enough rows to delete.");
        }

        // Save the result
        workbook.Save($"{folder}\\output.xlsx");
        Console.WriteLine("Workbook saved as output.xlsx");
    }
}
```

**Expected output** (console):

```
Deleted 2 row(s) from table "Table1".
Workbook saved as output.xlsx
```

Open `output.xlsx` – the first table now lacks the rows you removed, while the header row remains intact.

## Common questions and variations

### How do I delete rows from **all** tables in a workbook?

```csharp
foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (ListObject tbl in sheet.ListObjects)
    {
        // Example: delete the first data row of each table
        if (tbl.DataRange.RowCount > 1)
            tbl.DeleteRows(1, 1);
    }
}
```

### Can I delete rows based on a **cell value**?

Yes. Scan the `DataRange` for matching cells, collect their zero‑based indices, then delete in descending order:

```csharp
var rowsToRemove = new List<int>();
for (int i = 0; i < table.DataRange.RowCount; i++)
{
    var cell = table.DataRange[i, 2]; // column C (zero‑based)
    if (cell.StringValue == "Obsolete")
        rowsToRemove.Add(i);
}

// Delete rows from bottom to top to keep indices valid
rowsToRemove.Sort((a, b) => b.CompareTo(a));
foreach (int rowIdx in rowsToRemove)
    table.DeleteRows(rowIdx, 1);
```

### What if I need to **preserve formatting**?

`DeleteRows` removes the entire row from the table but retains the table’s style for remaining rows. If you need to keep specific formatting on a row you’re deleting, copy the style to another row before deletion.

### Does this work with **.xls** (Excel 97‑2003) files?

Yes. Aspose.Cells automatically detects the file format, so the same code works with `.xls`. Just change the file extension in the `Workbook` constructor.

## Performance tips

* **Batch deletions:** Deleting many rows one by one can be slower. Use a single `DeleteRows(start, count)` call when possible.
* **Avoid UI thread blocking:** If you integrate this into a desktop app, run the workbook manipulation on a background thread to keep the UI responsive.
* **Dispose properly:** Although Aspose.Cells uses managed memory, wrap the `Workbook` in a `using` block if you’re dealing with large files to free resources promptly.

## Conclusion

You now have a complete, production‑ready example that **deletes rows from Excel table** using C#. The guide covered how to **load Excel workbook C#**, locate the desired `ListObject`, safely remove rows, and save the updated file. With the edge‑case handling and performance advice included, you can adapt this pattern to more complex scenarios such as conditional deletions, multiple tables, or alternative .NET Excel libraries.

### Next steps

* Explore **ClosedXML** or **EPPlus** if you prefer a fully open‑source stack.
* Combine row deletion with **data validation** to clean spreadsheets before importing into a database.
* Automate the process for a folder of workbooks using `Directory.GetFiles` and a loop.

Feel free to experiment with different row ranges, table names, and conditional logic. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Load Excel File C# – How to Delete Rows and Remove Specific Rows](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)
- [How to Insert and Delete Rows in Excel with Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [How to Delete Blank Rows in Excel Using Aspose.Cells .NET for Data Cleanup](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}