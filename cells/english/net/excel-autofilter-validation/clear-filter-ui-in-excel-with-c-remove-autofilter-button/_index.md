---
category: general
date: 2026-02-09
description: Clear filter UI in Excel with C# by removing the AutoFilter button. Learn
  how to hide filter button, show header row, and keep your sheets tidy.
draft: false
keywords:
- clear filter UI
- remove autofilter excel
- how to remove autofilter
- show header row
- hide filter button
language: en
og_description: Clear filter UI in Excel using C#. This guide shows how to hide the
  filter button, show the header row, and keep worksheets clean.
og_title: Clear filter UI in Excel with C# – Remove AutoFilter Button
tags:
- excel
- csharp
- epplus
- automation
title: Clear filter UI in Excel with C# – Remove AutoFilter Button
url: /net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Clear filter UI in Excel with C# – Remove AutoFilter Button

Ever needed to **clear filter UI** in an Excel sheet but weren’t sure which line of code actually hides that little drop‑down arrow? You’re not the only one. The filter button can be an eyesore when you ship a report to end‑users who never need to change the view.  

In this tutorial we’ll walk through a complete, runnable example that **removes the AutoFilter button** from a table, makes sure the header row stays visible, and even touches on how to *hide filter button* for good. By the end you’ll know exactly **how to remove AutoFilter** in C# and why each step matters.

## What You’ll Need

- .NET 6+ (or .NET Framework 4.7.2+) – any recent runtime works.
- The **EPPlus** NuGet package (version 6.x or later) – it gives us `ExcelWorksheet`, `ExcelTable`, etc.
- A simple Excel file with a table named **SalesTable** (feel free to create one in a few clicks).

That’s it. No COM interop, no extra DLLs, just a handful of `using` statements and a few lines of code.

## Clear filter UI: Removing the AutoFilter Button

The core of the solution lives in three tiny statements. Let’s break them down so you understand *why* they’re needed, not just *what* they do.

### Step 1 – Grab a reference to the table

```csharp
// Step 1: Get a reference to the "SalesTable" in the first worksheet
ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
```

Why this matters: EPPlus works with **tables** (`ExcelTable`), not raw ranges. By pulling the table object we gain access to the `AutoFilter` property, which controls the UI element you see on the sheet. If you try to manipulate the worksheet directly, you’ll only affect values, not the filter button.

### Step 2 – Remove the AutoFilter button row

```csharp
// Step 2: Remove the AutoFilter button row (clears any applied filter UI)
salesTable.AutoFilter = null;
```

Setting `AutoFilter` to `null` tells EPPlus to delete the underlying filter row. This is the *clear filter UI* operation that most developers look for when they ask “**how to remove autofilter**”. It’s a clean, one‑liner approach that works on any Excel version EPPlus supports.

### Step 3 – Keep the header row visible

```csharp
// Step 3: Ensure the header row remains visible after removing the filter
salesTable.ShowHeader = true;
```

When you drop the filter UI, Excel can sometimes hide the header row if the table’s `ShowHeader` flag is false. By explicitly setting it to `true` we guarantee the column titles stay on screen – a subtle but important detail for a polished final report.

### Full, runnable example

Below is a minimal console app that opens an existing workbook, performs the three steps, and saves the result. Copy‑paste, hit **F5**, and watch the filter button disappear.

```csharp
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

class Program
{
    static void Main()
    {
        // EPPlus requires a license context for non‑commercial use.
        ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

        // 1️⃣ Load the workbook (replace with your own path)
        var filePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        using var package = new ExcelPackage(new FileInfo(filePath));

        // 2️⃣ Get a reference to the table named "SalesTable"
        ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
        if (salesTable == null)
        {
            Console.WriteLine("Table 'SalesTable' not found in the first worksheet.");
            return;
        }

        // 3️⃣ Remove the AutoFilter button (clear filter UI)
        salesTable.AutoFilter = null;

        // 4️⃣ Ensure the header row stays visible (show header row)
        salesTable.ShowHeader = true;

        // 5️⃣ Save the changes to a new file so you don’t overwrite the original
        var outputPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
        package.SaveAs(new FileInfo(outputPath));

        Console.WriteLine($"Filter button removed. Saved to {outputPath}");
    }
}
```

**Expected result:** Open *SalesReport_NoFilter.xlsx* – the filter arrows are gone, but the column headings remain. No more “click‑to‑filter” UI clutter.

> **Pro tip:** If you have **multiple tables** and want to hide the filter button for all of them, loop through `worksheet.Tables` and apply the same three lines inside the loop.

## How to remove AutoFilter in Excel using C# – a deeper dive

You might wonder, “What if the workbook already has a filter applied? Does setting `AutoFilter = null` also clear the filtered rows?” The answer is **yes**. EPPlus clears both the UI and the underlying filter criteria, leaving the data in its original order.  

If you only want to *hide* the button but keep the filter active, you can instead set the `AutoFilter` property to a **new empty filter**:

```csharp
salesTable.AutoFilter = new ExcelAutoFilter(); // hides button, retains filter logic
```

That variation is handy when you want to *hide filter button* for a polished look but still let power users toggle filters through VBA or the ribbon.

### Edge case: Tables without a header row

Some legacy reports use plain ranges instead of tables. In that scenario, EPPlus won’t expose an `ExcelTable` object, so the code above will throw. The workaround is to **convert the range to a table** first:

```csharp
var range = worksheet.Cells["A1:D100"];
var table = worksheet.Tables.Add(range, "TempTable");
table.ShowHeader = true;    // ensure header is visible
table.AutoFilter = null;    // clear filter UI
```

Now you’ve *removed autofilter excel* style UI even on a range that started out without a formal table.

## Show header row after hiding filter button – why it matters

A common complaint is that after you hide the filter UI, the header row sometimes disappears, especially when the workbook was originally created with “Hide Header” turned on. By explicitly setting `salesTable.ShowHeader = true;` we avoid that surprise.  

If you ever need to **hide filter button** but keep the header hidden (maybe you’re generating a raw data dump), simply set `salesTable.ShowHeader = false;` after clearing the filter. The code is symmetrical, which makes it easy to toggle based on a configuration flag.

## Hide filter button – practical tips and pitfalls

- **Version compatibility:** EPPlus 6+ works with `.xlsx` files only. If you’re dealing with the older `.xls` format, you’ll need a different library (e.g., NPOI) because the *clear filter UI* API isn’t available.
- **Performance:** Loading a huge workbook just to hide one button can be slow. Consider using `ExcelPackage.Load(stream, true)` to open in **read‑only** mode, apply the change, then save.
- **Testing:** Always validate the output file manually the first time. Automated UI tests can verify that the filter arrows are truly gone (`worksheet.Tables[0].AutoFilter == null`).
- **Licensing:** EPPlus switched to a dual license in version 5. For commercial projects you’ll need a paid license or switch to an alternative library.

## Full source file for copy‑paste

Below is the exact file you can drop into a new console project. No hidden dependencies, everything is self‑contained.

```csharp
// File: Program.cs
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

namespace ExcelFilterCleaner
{
    class Program
    {
        static void Main()
        {
            // License context – required for EPPlus 5+
            ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

            // Path to the original workbook (adjust as needed)
            string sourcePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
            if (!File.Exists(sourcePath))
            {
                Console.WriteLine($"Source file not found: {sourcePath}");
                return;
            }

            // Load workbook
            using var package = new ExcelPackage(new FileInfo(sourcePath));

            // Assume the first worksheet contains the table
            var worksheet = package.Workbook.Worksheets[0];
            const string tableName = "SalesTable";

            // Grab the table; abort if missing
            var salesTable = worksheet.Tables[tableName];
            if (salesTable == null)
            {
                Console.WriteLine($"Table '{tableName}' not found.");
                return;
            }

            // ---- Clear filter UI ----
            salesTable.AutoFilter = null;   // removes the filter button row
            salesTable.ShowHeader = true;   // guarantees the header row stays visible

            // Save to a new file so the original stays untouched
            string destPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
            package.SaveAs(new FileInfo(destPath));

            Console.WriteLine($"Successfully cleared filter UI. Output: {destPath}");
        }
    }
}
```

Run `dotnet add package EPPlus --version 6.0.8` (or the latest) before building, and you’ll have a clean sheet ready for distribution.

## Conclusion

We’ve just shown you **how to remove AutoFilter** and **clear filter UI** in an Excel workbook using C#. The three‑line core (`AutoFilter = null;`, `ShowHeader = true;`) does the heavy lifting, while the surrounding boilerplate makes the solution

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}