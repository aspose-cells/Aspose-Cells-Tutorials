---
category: general
date: 2026-11-25
description: Learn how to delete rows from Excel table in C# and also delete multiple
  rows from Excel sheet efficiently.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from excel table
- delete multiple rows from excel sheet
language: en
lastmod: 2026-11-25
og_description: Delete rows from Excel table in C# and learn to delete multiple rows
  from Excel sheet with clean code.
og_image_alt: Screenshot of C# code deleting rows from an Excel table
og_title: Delete rows from Excel table in C# – complete guide
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to delete rows from Excel table in C# and also delete multiple
    rows from Excel sheet efficiently.
  headline: How to delete rows from Excel table with C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# and also delete multiple
    rows from Excel sheet efficiently.
  name: How to delete rows from Excel table with C#
  steps:
  - name: Add Aspose.Cells to your project
    text: 'Open the **Package Manager Console** and run:'
  - name: Load the workbook and locate the table
    text: '```csharp using Aspose.Cells;'
  - name: Delete the desired data rows
    text: The `DeleteRows` method expects a **zero‑based** row index relative to the
      table, **including** the header row. Because the header cannot be removed, you
      must start at index 1 for the first data row.
  - name: Save the modified workbook
    text: '```csharp // Save the workbook to a new file to preserve the original workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
      } } ```'
  - name: Full working example
    text: '```csharp using Aspose.Cells;'
  - name: Edge cases and best practices
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Deleting rows beyond the last row | Check `worksheet.Rows.Count` before calling
      `RemoveAt`. | | Removing all rows except the header | Delete data rows in a
      loop or use `DeleteRows(1, table.DataRa'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
- data manipulation
title: How to delete rows from Excel table with C#
url: /net/row-and-column-management/how-to-delete-rows-from-excel-table-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to delete rows from Excel table with C#

If you need to delete rows from Excel table using C#, this guide shows you exactly how to do it. You will also see how to delete multiple rows from Excel sheet without affecting other data.

Working with Excel programmatically often requires removing outdated or invalid records. Deleting rows directly in a worksheet can be risky because the header row of a structured table must stay intact. This tutorial walks you through a safe approach that respects the table’s header and lets you delete any number of data rows in one call.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 or later installed  
* Visual Studio 2022 (or any compatible IDE)  
* The **Aspose.Cells** NuGet package (version 23.10 or newer) – this library provides the `Workbook`, `Worksheet`, and `ListObject` classes used in the examples  

You do not need Microsoft Office installed on the development machine because Aspose.Cells works with the file format directly.

## Delete rows from Excel table – step‑by‑step

The following sections describe each step required to delete rows from an Excel table safely. The primary keyword appears in this heading to satisfy SEO requirements.

### Step 1: Add Aspose.Cells to your project

Open the **Package Manager Console** and run:

```powershell
Install-Package Aspose.Cells
```

The package adds the necessary assemblies and resolves the `Workbook`, `Worksheet`, and `ListObject` types.

### Step 2: Load the workbook and locate the table

```csharp
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Load the workbook that contains the table
        var workbook = new Workbook(@"C:\Data\table_with_header.xlsx");

        // Access the first worksheet (index 0)
        var worksheet = workbook.Worksheets[0];

        // Retrieve the first ListObject (structured table) on the sheet
        var table = worksheet.ListObjects[0];
```

*Why this matters*: The `ListObject` represents a true Excel table, which maintains its own header row. By working with the `ListObject`, you avoid accidental header removal.

### Step 3: Delete the desired data rows

The `DeleteRows` method expects a **zero‑based** row index relative to the table, **including** the header row. Because the header cannot be removed, you must start at index 1 for the first data row.

```csharp
        // Delete two data rows starting after the header (index 1)
        // Parameters: startRow (relative to the table), numberOfRows
        table.DeleteRows(1, 2);
```

If you attempted `table.DeleteRows(0, 2)`, Aspose.Cells would throw an exception because the header row (index 0) is protected. Starting at index 1 ensures only data rows are removed.

### Step 4: Save the modified workbook

```csharp
        // Save the workbook to a new file to preserve the original
        workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
    }
}
```

Running the program removes the two rows immediately below the header while leaving the table structure intact.

### Full working example

```csharp
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // 1. Load workbook
        var workbook = new Workbook(@"C:\Data\table_with_header.xlsx");

        // 2. Access first worksheet
        var worksheet = workbook.Worksheets[0];

        // 3. Get the first table (ListObject)
        var table = worksheet.ListObjects[0];

        // 4. Delete two rows after the header (cannot delete header itself)
        table.DeleteRows(1, 2);

        // 5. Save the result
        workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
    }
}
```

**Expected output**: The file `table_with_header_modified.xlsx` contains the original table header, followed by all rows except the two that were removed. No other worksheets are altered.

## Delete multiple rows from Excel sheet

Sometimes you need to delete rows that are **not** part of a structured table. The secondary keyword appears in this heading. The approach differs slightly because you work with the worksheet’s `Rows` collection instead of a `ListObject`.

```csharp
using Aspose.Cells;

class SheetRowDeletion
{
    static void Main()
    {
        var workbook = new Workbook(@"C:\Data\plain_sheet.xlsx");
        var worksheet = workbook.Worksheets[0];

        // Delete rows 5 through 9 (inclusive) – zero‑based index
        // The second argument is the count of rows to remove
        worksheet.Rows.RemoveAt(4, 5);

        workbook.Save(@"C:\Data\plain_sheet_modified.xlsx");
    }
}
```

**Why this works**: `Rows.RemoveAt(startIndex, count)` removes a contiguous block of rows directly from the worksheet. There is no header protection, so you can start at any index. The method is efficient because it updates the internal data structures in a single operation, which is ideal when you need to delete multiple rows from an Excel sheet.

### Edge cases and best practices

| Situation                               | Recommended handling |
|----------------------------------------|----------------------|
| Deleting rows beyond the last row      | Check `worksheet.Rows.Count` before calling `RemoveAt`. |
| Removing all rows except the header    | Delete data rows in a loop or use `DeleteRows(1, table.DataRange.RowCount - 1)`. |
| Preserving cell formatting             | Deleting via `ListObject` automatically shifts formatting; for raw sheets, copy formatting before removal if needed. |
| Large worksheets ( > 10 000 rows)      | Perform deletions in descending order to avoid index shifting, or use `DeleteRows` on the table if possible. |

**Pro tip**: When you need to delete rows based on a condition (e.g., rows where a column value is empty), iterate through the table’s `DataRange` backwards and call `DeleteRows` for each matching row. Deleting backwards prevents index misalignment.

## Common questions

*Does this work with .xlsx files created by Excel 365?*  
Yes. Aspose.Cells supports the full Office Open XML specification, so the same code works for any modern `.xlsx` file.

*What if the workbook contains multiple tables?*  
Retrieve the desired table by name: `var table = worksheet.ListObjects["MyTable"];` then apply `DeleteRows` as shown.

*Can I delete rows without using a third‑party library?*  
You could use the Microsoft.Office.Interop.Excel COM interop, but that requires Excel to be installed on the server and introduces COM‑related overhead. Aspose.Cells provides a lightweight, server‑safe alternative.

## Conclusion

You now know how to delete rows from Excel table safely and how to delete multiple rows from Excel sheet using C#. The primary technique relies on the `ListObject.DeleteRows` method, which respects the table header, while the secondary technique uses `Rows.RemoveAt` for plain sheets. Apply these patterns to clean up data, automate report generation, or implement bulk‑edit features in your applications.

**Next steps**

* Explore other Aspose.Cells features such as inserting rows, copying styles, or filtering data.  
* Try the same operations with **ClosedXML** if you prefer an open‑source library; the API is similar but uses `IXLTable` and `IXLRows`.  
* Combine row‑deletion logic with LINQ queries to build more complex data‑cleaning pipelines.

Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [how to delete rows in Excel with C# – protect table header](/cells/english/net/row-and-column-management/how-to-delete-rows-in-excel-with-c-protect-table-header/)
- [How to use Aspose.Cells to delete rows in an Excel table while keeping the](/cells/english/net/row-and-column-management/how-to-use-aspose-cells-to-delete-rows-in-an-excel-table-whi/)
- [Load Excel File C# – How to Delete Rows and Remove Specific Rows](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}