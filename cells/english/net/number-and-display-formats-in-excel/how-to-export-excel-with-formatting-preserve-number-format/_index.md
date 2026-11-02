---
category: general
date: 2026-03-22
description: How to export Excel with formatting and preserve number format. Learn
  to convert Excel range, get formula result, and export Excel with formatting using
  Aspose.Cells.
draft: false
keywords:
- how to export excel
- preserve number format
- convert excel range
- get formula result
- export excel with formatting
language: en
og_description: How to export Excel with formatting and preserve number format. Step‑by‑step
  guide to convert Excel range, get formula result, and export Excel with formatting
  in C#.
og_title: How to Export Excel with Formatting – Preserve Number Format
tags:
- C#
- Aspose.Cells
- Excel automation
title: How to Export Excel with Formatting – Preserve Number Format
url: /net/number-and-display-formats-in-excel/how-to-export-excel-with-formatting-preserve-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Export Excel with Formatting – Preserve Number Format

Ever wondered **how to export Excel** data while keeping every cell’s look exactly as you see it in the workbook? Maybe you need to ship a report to a client, feed a grid control, or just stash the values in a database. The pain point is usually the loss of number formatting or formulas turning into raw strings.  

In this tutorial we’ll walk through a complete, ready‑to‑run C# example that **preserves number format**, **converts an Excel range** to a `DataTable`, **gets the formula result**, and finally **exports Excel with formatting** using Aspose.Cells. By the end you’ll have a single method you can drop into any project and call with a worksheet reference.

> **Quick preview:** the code creates a workbook, writes a value and a formula, tells Aspose.Cells to export the cells as formatted strings, and prints `123.456 | 246.912` – exactly what you’d expect to see in Excel.

---

## What You’ll Need

- **Aspose.Cells for .NET** (the free trial works fine for learning)
- .NET 6.0 or later (the API is the same on .NET Framework)
- A basic C# development environment (Visual Studio, VS Code, Rider… you choose)

No extra NuGet packages beyond Aspose.Cells are required. If you haven’t installed it yet, run:

```bash
dotnet add package Aspose.Cells
```

---

## Step 1 – Create a Workbook and Write Values (including a formula)

First we spin up a fresh workbook and drop a numeric value into **A1**. Then we add a simple formula in **B1** that multiplies the first cell by two. This sets the stage for demonstrating **get formula result** later on.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a numeric value and a formula that uses it
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Continue with export options...
        ExportRangeAsDataTable(worksheet);
    }
}
```

**Why this matters:**  
- `PutValue` stores the raw number, while `PutFormula` stores the calculation.  
- Aspose.Cells keeps the formula **alive**, so when we later ask for the cell’s value we’ll actually get `246.912`, not the string `"=A1*2"`.

---

## Step 2 – Tell Aspose.Cells to Export Values as Formatted Strings

If you simply call `ExportDataTable` with default settings, numeric cells will be returned as their underlying `double` values. That strips away any thousands separators, currency symbols, or custom decimal places you may have set. The `ExportTableOptions` class lets us **preserve number format** and **export as string**.

```csharp
static void ExportRangeAsDataTable(Worksheet worksheet)
{
    // Step 2: Set export options to retrieve values as formatted strings
    ExportTableOptions exportOptions = new ExportTableOptions
    {
        ExportAsString = true,          // Return values as strings
        ExportNumberFormat = true      // Preserve the cell's number format
    };

    // Step 3: Export the range A1:B1 to a DataTable
    DataTable dataTable = worksheet.Cells.ExportDataTable(
        firstRow: 0,
        firstColumn: 0,
        totalRows: 1,
        totalColumns: 2,
        includeColumnNames: true,
        options: exportOptions);

    PrintDataTable(dataTable);
}
```

**Key point:** `ExportNumberFormat = true` is the flag that makes **preserve number format** work. Without it you’d see `"123.456"` and `"246.912"` as raw numbers, which may look fine in code but not when you paste the data into a UI that expects the same formatting as Excel.

---

## Step 3 – Print the Exported Data (Verification)

Now that we have a `DataTable` full of formatted strings, let’s dump the contents to the console. This also demonstrates that we successfully **get formula result** without evaluating the formula ourselves.

```csharp
static void PrintDataTable(DataTable table)
{
    // Step 4: Print the exported values (already formatted)
    foreach (DataRow row in table.Rows)
    {
        // The output will look like: 123.456 | 246.912
        Console.WriteLine($"{row[0]} | {row[1]}");
    }
}
```

Running the program prints:

```
123.456 | 246.912
```

Notice how the second column shows the **formula result**, not the formula text. That’s exactly what you need when you **export Excel with formatting** for downstream processing.

---

## Step 4 – Converting Larger Excel Ranges (Optional)

The example above handles a tiny `A1:B1` slice, but real‑world scenarios often require exporting entire tables. The same method works for any rectangular block – just adjust the `firstRow`, `firstColumn`, `totalRows`, and `totalColumns` arguments.

```csharp
// Example: Export a 10‑row by 5‑column block starting at C3
DataTable bigTable = worksheet.Cells.ExportDataTable(
    firstRow: 2,          // Zero‑based index (C3 = row 2, column 2)
    firstColumn: 2,
    totalRows: 10,
    totalColumns: 5,
    includeColumnNames: true,
    options: exportOptions);
```

**Pro tip:** If your sheet already has a header row, set `includeColumnNames` to `true`. Aspose.Cells will use the first row of the range as column names, which is handy when you later bind the `DataTable` to a UI grid.

---

## Step 5 – Common Pitfalls & How to Avoid Them

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Numbers lose commas or currency symbols** | `ExportAsString` is `false` or `ExportNumberFormat` is omitted | Set both `ExportAsString = true` **and** `ExportNumberFormat = true`. |
| **Formula cells return the formula text** | You didn’t call `CalculateFormula` before export (only needed if the workbook isn’t set to auto‑calculate) | Either enable auto‑calculate (`workbook.CalculateFormula()`) or rely on `ExportAsString` which forces evaluation. |
| **Headers appear as data rows** | `includeColumnNames` set to `false` while your range includes a header row | Set `includeColumnNames = true` to treat the first row as column names. |
| **Large ranges cause memory pressure** | Exporting the entire sheet at once loads everything into memory | Export in chunks (e.g., 500 rows at a time) and merge `DataTable`s if needed. |

---

## Step 6 – Full Working Example (Copy‑Paste Ready)

Below is the entire program, from `using` statements to `Main`. Paste it into a console app and hit **F5** – you’ll see the formatted output instantly.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate cells
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Export options: keep formatting and return strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            ExportNumberFormat = true
        };

        // Export A1:B1 as a DataTable
        DataTable dataTable = worksheet.Cells.ExportDataTable(
            firstRow: 0,
            firstColumn: 0,
            totalRows: 1,
            totalColumns: 2,
            includeColumnNames: true,
            options: exportOptions);

        // Print results
        foreach (DataRow row in dataTable.Rows)
        {
            Console.WriteLine($"{row[0]} | {row[1]}"); // Expected: "123.456 | 246.912"
        }

        // Keep console window open
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**Expected output**

```
123.456 | 246.912

Press any key to exit...
```

That’s the entire **how to export excel** workflow, with formatting intact, formula results evaluated, and a clean `DataTable` ready for any .NET consumer.

---

## Conclusion

We’ve covered everything you need to know about **how to export Excel** data while **preserving number format**, **converting an Excel range** to a `DataTable`, and **getting formula results** without extra parsing. The key is the `ExportTableOptions` configuration – once you set `ExportAsString` and `ExportNumberFormat` to `true`, Aspose.Cells does the heavy lifting for you.

From here you can:

- Plug the `DataTable` into a WPF `DataGrid` or ASP.NET MVC view.
- Write the table to a CSV file while keeping the exact visual representation.
- Extend the approach to multiple sheets or dynamic ranges.

Feel free to experiment with different formats (currency, percentages) and larger blocks of data. If you run into any quirks, refer back to the **common pitfalls** table – it covers the most frequent hiccups when you **export excel with formatting**.

Happy coding, and may your exported spreadsheets always look as polished as the originals!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}