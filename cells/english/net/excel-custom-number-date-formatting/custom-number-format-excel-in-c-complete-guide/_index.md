---
category: general
date: 2026-03-22
description: Custom number format excel tutorial showing how to import datatable to
  excel, set column background color, format column as currency and save workbook
  as xlsx.
draft: false
keywords:
- custom number format excel
- import datatable to excel
- set column background color
- format column as currency
- save workbook as xlsx
language: en
og_description: Custom number format excel tutorial that walks you through importing
  a DataTable, setting column background color, formatting a column as currency, and
  saving the workbook as xlsx.
og_title: Custom Number Format Excel in C# – Step‑by‑Step Guide
tags:
- C#
- Excel automation
- Aspose.Cells
- Data export
title: Custom Number Format Excel in C# – Complete Guide
url: /net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Custom Number Format Excel – Full‑Stack C# Tutorial

Ever wondered how to apply a **custom number format excel** style directly from C#? Maybe you’ve tried dumping a DataTable into a spreadsheet only to see plain numbers, no colors, and no currency formatting. That’s a common pain point—especially when you need a polished report for stakeholders.

In this guide we’ll solve that problem together: you’ll learn how to **import datatable to excel**, **set column background color**, **format column as currency**, and finally **save workbook as xlsx** with a custom number format that makes your figures pop. No vague references, just a complete, runnable solution you can copy‑paste into your project.

---

## What You’ll Build

By the end of this tutorial you’ll have a self‑contained C# console app that:

1. Retrieves a `DataTable` (you can replace the stub with your own query).  
2. Creates a new Excel workbook using Aspose.Cells (or any compatible library).  
3. Applies a blue, bold font to the first column, a light‑yellow background to the second, and a currency format (`$#,##0.00`) to the third.  
4. Saves the file as `DataTableWithStyleArray.xlsx` in a folder you choose.

You’ll see exactly how each line contributes to the final Excel file, and we’ll discuss why those choices matter for maintainability and performance.

---

## Prerequisites

- .NET 6.0 or later (the code works with .NET Framework 4.7+ as well).  
- Aspose.Cells for .NET (free trial or licensed version). Install via NuGet:

```bash
dotnet add package Aspose.Cells
```

- Basic familiarity with `DataTable` and C# console applications.

---

## Step 1: Retrieve the Source Data as a DataTable

First, we need some data to export. In a real‑world scenario you’d probably call a repository or run a SQL query. For illustration we’ll create a simple table in‑memory.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetSampleData()
{
    var table = new DataTable("Sales");
    table.Columns.Add("Product", typeof(string));
    table.Columns.Add("Quantity", typeof(int));
    table.Columns.Add("Revenue", typeof(decimal));

    table.Rows.Add("Widget A", 120, 3450.75m);
    table.Rows.Add("Widget B", 85, 2190.00m);
    table.Rows.Add("Widget C", 60, 1580.40m);

    return table;
}
```

> **Why this matters:** Using a `DataTable` gives you a tabular, schema‑aware source that maps cleanly onto Excel rows and columns. It also lets you reuse the same export logic for any dataset without rewriting code.

---

## Step 2: Create a New Workbook and Grab the First Worksheet

Now we spin up an Excel workbook. The `Workbook` class represents the entire file; its `Worksheets[0]` is the default sheet where we’ll drop our data.

```csharp
// Initialize a fresh workbook
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet
Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** If you need multiple sheets, just call `workbook.Worksheets.Add("SheetName")` and repeat the styling steps for each.

---

## Step 3: Define Column Styles – Font, Background, and Number Format

Styling in Aspose.Cells is done via `Style` objects. We’ll build an array where each element corresponds to a column in the DataTable.

```csharp
// Prepare an array to hold three distinct styles
Style[] columnStyles = new Style[3];

// 1️⃣ First column – blue, bold font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = System.Drawing.Color.Blue;
columnStyles[0].Font.IsBold = true;

// 2️⃣ Second column – light‑yellow background
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
columnStyles[1].Pattern = BackgroundType.Solid;

// 3️⃣ Third column – custom currency format (custom number format excel)
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Custom = "$#,##0.00";
```

> **Why a style array?** Passing an array to `ImportDataTable` lets you apply a distinct style to each column in a single call, which is both concise and performant. It also guarantees that the formatting stays in sync with the data order.

---

## Step 4: Import the DataTable While Applying the Styles

Here’s the heart of the operation: we feed the `DataTable` into the worksheet, tell Aspose to include the header row, and hand over our `columnStyles` array.

```csharp
// Import data starting at cell A1 (row 0, column 0)
worksheet.Cells.ImportDataTable(
    GetSampleData(),   // source DataTable
    true,              // include column names as header
    0, 0,              // start row, start column
    columnStyles);     // apply the style array
```

> **What happens under the hood?** Aspose iterates through each column, writes the header, then writes each row value. While doing so it applies the corresponding `Style` from the array, so you end up with a blue header for “Product”, a yellow‑shaded “Quantity”, and a nicely formatted “Revenue” column.

---

## Step 5: Save the Workbook as an XLSX File

Finally, we persist the workbook to disk. The `Save` method automatically chooses the XLSX format based on the file extension.

```csharp
// Choose a folder that exists on your machine
string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";

// Ensure the directory exists (optional safety check)
System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);

// Save the workbook
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

> **Tip:** If you need to stream the file (e.g., for a web API), use `workbook.Save(stream, SaveFormat.Xlsx)` instead of a file path.

---

## Full Working Example

Below is the complete program you can paste into a new console project. It compiles and runs as‑is, producing a styled Excel file.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Get data
            DataTable dataTable = GetSampleData();

            // Step 2 – Create workbook & worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 3 – Prepare column styles
            Style[] columnStyles = new Style[3];

            // Font style for first column (blue, bold)
            columnStyles[0] = workbook.CreateStyle();
            columnStyles[0].Font.Color = System.Drawing.Color.Blue;
            columnStyles[0].Font.IsBold = true;

            // Background style for second column (light yellow)
            columnStyles[1] = workbook.CreateStyle();
            columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
            columnStyles[1].Pattern = BackgroundType.Solid;

            // Currency format for third column (custom number format excel)
            columnStyles[2] = workbook.CreateStyle();
            columnStyles[2].Custom = "$#,##0.00";

            // Step 4 – Import data with styles
            worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

            // Step 5 – Save as XLSX
            string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";
            System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }

        // Helper method to build a demo DataTable
        static DataTable GetSampleData()
        {
            var table = new DataTable("Sales");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Revenue", typeof(decimal));

            table.Rows.Add("Widget A", 120, 3450.75m);
            table.Rows.Add("Widget B", 85, 2190.00m);
            table.Rows.Add("Widget C", 60, 1580.40m);

            return table;
        }
    }
}
```

### Expected Result

When you open `DataTableWithStyleArray.xlsx` you’ll see:

| **Product** (blue, bold) | **Quantity** (light‑yellow) | **Revenue** (currency) |
|--------------------------|-----------------------------|------------------------|
| Widget A                 | 120                         | $3,450.75              |
| Widget B                 | 85                          | $2,190.00              |
| Widget C                 | 60                          | $1,580.40              |

The **custom number format excel** you specified (`$#,##0.00`) ensures every revenue cell displays a dollar sign, thousands separator, and two decimal places—exactly what finance teams expect.

---

## Frequently Asked Questions & Edge Cases

### Can I use this with a different Excel library?

Absolutely. The concept—creating a style per column and applying it during import—translates to EPPlus, ClosedXML, or NPOI. The API calls differ, but the pattern stays the same.

### What if my DataTable has more columns than styles?

Aspose will apply the default style to any column without a matching entry in the `columnStyles` array. To avoid surprises, either size the array to `dataTable.Columns.Count` or generate styles dynamically in a loop.

### How do I set a custom number format for dates?

Just set `style.Custom = "dd‑mm‑yyyy"` (or any valid Excel format string). The same array‑based approach works for dates, percentages, or scientific notation.

### Is there a way to auto‑size columns after import?

Yes—call `worksheet.AutoFitColumns();` after the import. It runs a quick width calculation based on cell contents.

### What about large data sets (100k+ rows)?

`ImportDataTable` is optimized for bulk operations, but you might hit memory limits. In that case, consider streaming rows manually with `Cells[i, j].PutValue(...)` and re‑using a single `Style` object to reduce overhead.

---

## Pro Tips & Common Pitfalls

- **Avoid hard‑coding paths** in production code; use `Environment.GetFolderPath` or configuration settings.  
- **Dispose of the workbook** if you’re in a long‑running service—wrap it in a `using` block to free native resources.  
- **Watch out for culture‑specific separators**. The custom format `$#,##0.00` forces a period as decimal separator regardless of the OS locale, which is usually what you want for financial reports.  
- **Remember to reference System.Drawing** (or `System.Drawing.Common` on .NET Core) for the color structs used in styling.  
- **Test the output on different Excel versions**; older versions might interpret some custom formats slightly differently.

---

## Conclusion

We’ve covered everything you need to **custom number format excel** files from C#: pulling data from a `DataTable`, **import datatable to excel**, applying a **set column background color**, using **format column as currency**, and finally **save workbook as x

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}