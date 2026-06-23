---
category: general
date: 2026-03-21
description: How to export Excel data with column names, preserve number format, and
  read specific rows using Aspose.Cells in C#. Learn to read Excel worksheet and export
  specific rows efficiently.
draft: false
keywords:
- how to export excel
- preserve number format
- export with column names
- read excel worksheet
- export specific rows
language: en
og_description: How to export Excel data with column names, preserve number format,
  and read specific rows using Aspose.Cells. A full, runnable example for C# developers.
og_title: How to Export Excel Data in C# – Complete Programming Guide
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: How to Export Excel Data in C# – Step‑by‑Step Guide
url: /net/excel-data-export-retrieval/how-to-export-excel-data-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Export Excel Data in C# – Complete Programming Guide

Ever wondered **how to export excel** data without losing the original formatting? Maybe you’ve tried a quick copy‑paste and ended up with dates looking like “44728” or missing column headers. That’s frustrating, right? In this tutorial you’ll see a clean, end‑to‑end way to read an Excel worksheet, preserve number format, export with column names, and even pick just the rows you need.

We’ll be using the Aspose.Cells library because it gives you fine‑grained control over export options. By the end of this guide you’ll have a reusable snippet that can be dropped into any .NET project, and you’ll understand why each option matters. No external docs required—everything you need is right here.

---

## What You’ll Learn

- **Read Excel worksheet** into memory with Aspose.Cells.
- **Export specific rows** (e.g., rows 0‑49) while keeping column names.
- **Preserve number format** so currency, dates, and percentages stay intact.
- How to **export with column names** and include cell comments if you need them.
- A complete, ready‑to‑run C# example plus tips for common pitfalls.

### Prerequisites

- .NET 6.0 or later (the code works with .NET Framework 4.6+ as well).
- Aspose.Cells for .NET installed via NuGet (`Install-Package Aspose.Cells`).
- An Excel file (`input.xlsx`) placed in a folder you can reference.

> **Pro tip:** If you’re on a CI pipeline, consider pulling the NuGet package from a private feed to avoid licensing surprises.

---

## Step 1 – Install Aspose.Cells and Add Namespaces

First, make sure the Aspose.Cells package is in your project. Open the Package Manager Console and run:

```powershell
Install-Package Aspose.Cells
```

Then add the required `using` directives at the top of your C# file:

```csharp
using Aspose.Cells;
using System.Data;
using System;
```

These imports give you access to `Workbook`, `Worksheet`, `ExportTableOptions`, and `DataTable`—the core pieces for **reading an Excel worksheet** and exporting data.

---

## Step 2 – Load the Workbook (Read the Excel File)

Now we actually **read the Excel worksheet**. The `Workbook` constructor takes a path to the file, and Aspose.Cells will handle both `.xlsx` and older `.xls` formats.

```csharp
// Step 2: Load the workbook containing the data
string filePath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(filePath);
```

> **Why this matters:** Loading the workbook once and re‑using the same `Worksheet` object is far more efficient than opening the file repeatedly, especially for large spreadsheets.

---

## Step 3 – Configure Export Options (Preserve Number Format & Column Names)

Here’s where we tell Aspose.Cells *how* to export. The `ExportTableOptions` class lets us fine‑tune the output. We’ll enable three flags:

1. `ExportAsString = true` – forces every cell to become a string, which guarantees that numbers keep their visual representation.
2. `IncludeCellComments = true` – copies any comments attached to cells (handy for documentation).
3. `PreserveNumberFormat = true` – retains the original number format (currency symbols, date patterns, etc.).

```csharp
// Step 3: Configure export options to control how the table is exported
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export all values as strings
    IncludeCellComments = true,     // Preserve any cell comments
    PreserveNumberFormat = true     // Keep the original number formatting
};
```

> **Edge case:** If you set `ExportAsString` to `false` but still want to keep number formats, you may end up with raw numeric values (e.g., 44728 for a date). Keeping both flags on avoids that surprise.

---

## Step 4 – Grab the First Worksheet (Read Excel Worksheet)

Most simple files have the data you need on the first sheet, so we’ll fetch it by index. If you need a different sheet, just replace `0` with the appropriate zero‑based index or use `workbook.Worksheets["SheetName"]`.

```csharp
// Step 4: Get the first worksheet from the workbook
Worksheet firstWorksheet = workbook.Worksheets[0];
```

> **Why it’s useful:** Directly accessing the worksheet object gives you full control over its `Cells` collection, which is essential for **export specific rows** later on.

---

## Step 5 – Export a Range of Cells (Export Specific Rows)

Now the heart of the tutorial: exporting rows 0‑49 and columns 0‑4 (i.e., the first 50 rows and first five columns) into a `DataTable`. We’ll also ask Aspose.Cells to include column names as the first row of the `DataTable`.

```csharp
// Step 5: Export a range of cells (rows 0‑49, columns 0‑4) to a DataTable using the options
DataTable exportedTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 50,
    totalColumns: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

### What This Does

- **`startRow: 0`** – begins at the very top of the sheet.
- **`totalRows: 50`** – grabs the first 50 rows (i.e., **export specific rows**).
- **`totalColumns: 5`** – limits the export to the first five columns.
- **`includeColumnNames: true`** – ensures the `DataTable` column headers match the Excel header row, satisfying the **export with column names** requirement.
- **`exportOptions`** – applies the settings from Step 3, so your numeric values stay looking like “$1,234.56” rather than “1234.56”.

---

## Step 6 – Verify the Export (What the Result Looks Like)

Let’s print the first few rows to the console so you can see that the formatting survived.

```csharp
// Step 6: Display a few rows to verify the export
Console.WriteLine("=== Exported DataTable Preview ===");
foreach (DataRow row in exportedTable.Rows)
{
    // Join each column with a tab for readability
    Console.WriteLine(string.Join("\t", row.ItemArray));
}
```

**Expected output (example):**

```
=== Exported DataTable Preview ===
Date        Description    Amount   Tax   Total
01/02/2024  Widget A       $120.00  $12  $132.00
01/03/2024  Widget B       $200.00  $20  $220.00
...
```

Notice how the dates appear in `MM/dd/yyyy` format and the currency retains the `$` symbol—thanks to **preserve number format**.

---

## Common Pitfalls & How to Avoid Them

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| Dates turn into large numbers | `ExportAsString` left `false` | Keep `ExportAsString = true` or convert cells manually |
| Missing column headers | `includeColumnNames` set to `false` | Set it to `true` when you need **export with column names** |
| Comments disappear | `IncludeCellComments` not enabled | Turn on `IncludeCellComments` in `ExportTableOptions` |
| Exporting the wrong sheet | Using `Worksheets[0]` on a multi‑sheet file | Specify the sheet name: `workbook.Worksheets["Data"]` |
| Out‑of‑range exception | `totalRows` exceeds actual rows | Use `Math.Min(totalRows, worksheet.Cells.MaxDataRow + 1)` |

---

## Bonus: Exporting the Whole Sheet While Still Preserving Formats

If you later decide you need the entire sheet, just replace the `totalRows` and `totalColumns` with the sheet’s maximum dimensions:

```csharp
int maxRows = firstWorksheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int maxCols = firstWorksheet.Cells.MaxDataColumn + 1;

DataTable fullTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: maxRows,
    totalColumns: maxCols,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

Now you have a **read excel worksheet** routine that works for any size, while still **preserving number format** and **exporting with column names**.

---

## Full Working Example (Copy‑Paste Ready)

Below is the complete program you can drop into a console app. It includes all the steps, imports, and a simple verification printout.

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);

            // 2️⃣ Set export options (preserve number format, include comments, export as strings)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                IncludeCellComments = true,
                PreserveNumberFormat = true
            };

            // 3️⃣ Grab the first worksheet (read excel worksheet)
            Worksheet sheet = workbook.Worksheets[0];

            // 4️⃣ Export rows 0‑49, columns 0‑4 (export specific rows) with column headers
            DataTable table = sheet.Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: 50,
                totalColumns: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // 5️⃣ Show a preview
            Console.WriteLine("=== Exported DataTable Preview ===");
            foreach (DataRow row in table.Rows)
            {
                Console.WriteLine(string.Join("\t", row.ItemArray));
            }

            // Keep console open
            Console.WriteLine("\nExport complete. Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

Save this as `Program.cs`, run `dotnet run`, and you should see the formatted preview in your terminal.

---

## Conclusion

We’ve just walked through **how to export excel** data using Aspose.Cells, covering everything from loading the workbook to preserving number format, exporting with column names, and limiting the export to specific rows. The code is self‑contained, fully runnable, and includes practical safeguards for the most common edge cases.

Ready for the next challenge? Try exporting directly to a CSV while still keeping the original number formatting, or push the `DataTable` into an Entity Framework Core context for bulk database inserts. Both scenarios build on the same fundamentals we covered here.

If you found this guide helpful

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}