---
category: general
date: 2026-03-18
description: How to export Excel data to a DataTable in C# with code that handles
  specific cells, converts Excel to DataTable, and formats numbers. Learn export specific
  cells and more.
draft: false
keywords:
- how to export excel
- convert excel to datatable
- export specific cells
- excel to datatable c#
- excel range to datatable
language: en
og_description: How to export Excel data to a DataTable in C#. This tutorial shows
  how to export specific cells, convert Excel to DataTable, and format numbers with
  ease.
og_title: How to Export Excel to a DataTable in C# – Complete Guide
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: How to Export Excel to a DataTable in C# – Step‑by‑Step Guide
url: /net/excel-data-import-export/how-to-export-excel-to-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Export Excel to a DataTable in C# – Step‑by‑Step Guide

Ever wondered **how to export Excel** data into a `DataTable` without losing formatting? You’re not the only one—developers constantly need to pull a slice of a spreadsheet into memory for reporting, validation, or bulk‑insert operations. The good news? With a few lines of C# you can export a precise range (say *A1:F11*), force every cell to be treated as a string, and even apply a custom number format.

In this tutorial we’ll cover everything you need to know: from loading the workbook, configuring **export specific cells**, converting the range to a `DataTable`, and handling edge cases like empty rows or locale‑dependent numbers. By the end you’ll have a reusable method that works with **excel to datatable c#** scenarios in production code.

> **Prerequisites** – You’ll need the Aspose.Cells for .NET library (or any similar API that offers `ExportDataTable`). The example assumes .NET 6+, but the concepts apply to earlier versions as well.

---

## What You’ll Learn

- How to **convert Excel to DataTable** using Aspose.Cells.
- Exporting a custom range (`excel range to datatable`) while treating all values as strings.
- Applying a two‑decimal‑place number format (`#,#00.00`) during export.
- Common pitfalls (null rows, hidden columns) and how to avoid them.
- A ready‑to‑copy, fully runnable code sample.

---

## Prerequisites and Setup

Before we dive into the code, make sure you have:

1. **Aspose.Cells for .NET** installed via NuGet:

   ```bash
   dotnet add package Aspose.Cells
   ```

2. An Excel file (`input.xlsx`) placed in a folder you can reference, e.g. `YOUR_DIRECTORY/input.xlsx`.
3. A project that targets .NET 6 or later (the `using` statements shown below work out of the box).

> **Pro tip:** If you’re using a different library (e.g., EPPlus or ClosedXML), the concept stays the same—load the workbook, select a range, and call a method that returns a `DataTable`.

---

## Step 1: Load the Workbook and Grab the First Worksheet

The first thing you need is a `Workbook` object that represents your Excel file. Once you have it, you can access any worksheet by index or name.

```csharp
using Aspose.Cells;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];

            // Continue with export options...
        }
    }
}
```

**Why this matters:** Loading the workbook early lets you inspect its structure (hidden sheets, protection) before you decide which cells to export. If the file is large, consider using `LoadOptions` to stream only needed parts.

---

## Step 2: Configure Export Options – Treat All Values as Strings

When you export data for downstream processing (e.g., bulk insert into SQL), you often want a **consistent string representation**. This avoids type‑mismatch errors later on.

```csharp
// Configure export behavior
ExportTableOptions exportOptions = new ExportTableOptions
{
    // Force every cell to be returned as a string, regardless of its original type
    ExportAsString = true,

    // Apply a two‑decimal‑place format to numeric cells
    NumberFormat = "#,##0.00"
};
```

**Explanation:**  
- `ExportAsString = true` tells Aspose.Cells to ignore the native cell type and return the formatted text.  
- `NumberFormat = "#,##0.00"` ensures numbers like `1234.5` become `"1,234.50"`—useful for financial reports.

If you need the original data types, simply set `ExportAsString` to `false` and handle conversion yourself.

---

## Step 3: Export a Specific Range (A1:F11) to a DataTable

Now comes the core of **export specific cells**. The `ExportDataTable` method takes start/end row/column indices (zero‑based) plus a flag for header inclusion.

```csharp
// Export cells A1:F11 (rows 0‑10, columns 0‑5) including the header row
DataTable table = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    endRow: 10,
    endColumn: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

**What you get:** A `DataTable` with 11 rows (including the header) and 6 columns (`A`‑`F`). All values are strings formatted per `exportOptions`.

---

## Step 4: Verify the Result – Print to Console

It’s always a good idea to sanity‑check the output before you hand the table off to another component.

```csharp
// Simple console dump
foreach (DataRow row in table.Rows)
{
    foreach (var item in row.ItemArray)
    {
        Console.Write($"{item}\t");
    }
    Console.WriteLine();
}
```

You should see something like:

```
Id      Name        Qty     Price   Total   Date
1       Widget A    10      2.50    25.00   2026-01-01
2       Widget B    5       3.75    18.75   2026-01-02
...
```

Notice how the numeric columns display two decimal places, exactly as we specified.

---

## Full Working Example (Copy‑Paste Ready)

Below is the complete program that ties everything together. Drop it into a new console project, adjust the file path, and run—no additional configuration needed.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load workbook and select worksheet
            // -------------------------------------------------
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -------------------------------------------------
            // 2️⃣ Set export options – strings + number format
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                NumberFormat = "#,##0.00"
            };

            // -------------------------------------------------
            // 3️⃣ Export range A1:F11 (rows 0‑10, cols 0‑5)
            // -------------------------------------------------
            DataTable table = worksheet.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                endRow: 10,
                endColumn: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // -------------------------------------------------
            // 4️⃣ Output to console for verification
            // -------------------------------------------------
            Console.WriteLine("=== Exported DataTable ===");
            foreach (DataRow row in table.Rows)
            {
                foreach (var cell in row.ItemArray)
                {
                    Console.Write($"{cell}\t");
                }
                Console.WriteLine();
            }

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Key takeaways from the code:**

- The `ExportTableOptions` object is reusable; you can pass it to multiple `ExportDataTable` calls if you need to export several ranges.
- Indexing starts at **0**, so `A1` maps to `(0,0)`.
- Setting `includeColumnNames` to `true` automatically uses the first row as column headers—great for downstream `DataTable` operations.

---

## Handling Edge Cases & Common Questions

### What if the worksheet has hidden rows or columns?

Aspose.Cells respects visibility by default. If you need to export hidden data, set `exportOptions.ExportHiddenRows = true` and `ExportHiddenColumns = true`.

### My Excel file contains formulas—will I get the calculated values?

Yes. By default `ExportDataTable` returns the **displayed value** (the result of the formula). If you want the raw formula text, set `exportOptions.ExportFormulas = true`.

### How do I skip completely empty rows?

After the export, you can prune the `DataTable`:

```csharp
foreach (DataRow row in table.Rows.Cast<DataRow>()
                                   .Where(r => r.ItemArray.All(c => c == DBNull.Value || string.IsNullOrWhiteSpace(c.ToString()))).ToList())
{
    table.Rows.Remove(row);
}
```

### Can I export a non‑contiguous range (e.g., A1:B5 and D1:E5)?

Aspose.Cells doesn’t support disjoint ranges in a single call. Instead, export each block separately and then merge the resulting `DataTable`s manually.

---

## Performance Tips

- **Reuse `ExportTableOptions`** for multiple exports; creating a new instance each time adds negligible overhead but clutters the code.
- **Stream large files** with `LoadOptions` to avoid loading the entire workbook into memory.
- **Avoid `DataTable`** if you only need a quick CSV export—`ExportDataTable` is convenient but not the most memory‑efficient for massive sheets.

---

## Conclusion

We’ve walked through **how to export Excel** data into a `DataTable` while controlling formatting, handling specific cell ranges, and ensuring every value arrives as a string. The full example demonstrates a clean, production‑ready approach that you can adapt for **convert excel to datatable**, **export specific cells**, or any **excel range to datatable** scenario you encounter.

Feel free to experiment: change the range, toggle `ExportAsString`, or pipe the `DataTable` straight into Entity Framework for bulk inserts. The sky’s the limit once you have this solid foundation.

---

### Next Steps & Related Topics

- **Importing DataTable back into Excel** – learn the reverse operation with `ImportDataTable`.
- **Bulk inserting a DataTable into SQL Server** – use `SqlBulkCopy` for lightning‑fast loads.
- **Working with EPPlus or ClosedXML** – see how the same task looks with alternative libraries.
- **Formatting cells on export** – explore `ExportTableOptions` further for date formats, custom culture settings, and more.

Got questions or a different use‑case? Drop a comment, and let’s keep the conversation rolling. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}