---
category: general
date: 2026-03-22
description: Learn how to duplicate pivot in C# using Aspose.Cells. This guide also
  shows how to copy rows and load Excel workbook c# for seamless excel automation
  copy rows.
draft: false
keywords:
- how to duplicate pivot
- how to copy rows
- load excel workbook c#
- excel automation copy rows
language: en
og_description: How to duplicate pivot in C#? Follow this concise tutorial to load
  Excel workbook c#, copy rows, and master excel automation copy rows.
og_title: How to Duplicate Pivot in C# – Complete Guide
tags:
- C#
- Excel Automation
- Aspose.Cells
title: How to Duplicate Pivot in C# – Complete Step‑by‑Step Guide
url: /net/pivot-tables/how-to-duplicate-pivot-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Duplicate Pivot in C# – Complete Step‑by‑Step Guide

Ever wondered **how to duplicate pivot** tables programmatically without manually dragging them in Excel? You're not the only one. In many reporting pipelines the same pivot layout is needed on a fresh set of rows, and doing it by hand is a waste of time.  

The good news? With a few lines of C# you can load an Excel workbook, define the area that holds the pivot, and **how to copy rows** so the pivot appears in a new location—all in one automated run. In this tutorial we’ll also cover **load excel workbook c#** basics and give you a solid foundation for **excel automation copy rows** tasks.

> **What you’ll walk away with**  
> • A complete, runnable example that duplicates a pivot table.  
> • An explanation of why each line matters.  
> • Tips for handling edge cases like hidden worksheets or multiple pivots.

---

## Prerequisites

Before we dive in, make sure you have:

- **.NET 6.0** (or any recent .NET version) installed.  
- **Aspose.Cells for .NET** – the library we’ll use to manipulate Excel files. You can grab it via NuGet:  

```bash
dotnet add package Aspose.Cells
```  

- A source workbook (`Source.xlsx`) that already contains a pivot table in the range **A1:J20** (the range we’ll duplicate).  
- Basic familiarity with C# syntax – nothing fancy, just the usual `using` statements and `Main` method.

If any of these sound unfamiliar, pause a moment and install the package; the rest of the guide assumes the library is ready to go.

---

![Illustration of how to duplicate pivot in C# using Aspose.Cells](https://example.com/duplicate-pivot.png "how to duplicate pivot in C# illustration")

*Image alt text: "how to duplicate pivot in C# example showing source and duplicated pivot rows".*

---

## Step 1: Load Excel Workbook C# – Opening the File

The very first thing you need to do when you want to **load excel workbook c#** is create a `Workbook` instance pointing at your file. This object gives you access to every worksheet, cell, and pivot inside the file.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Load the source workbook
        string sourcePath = @"C:\Data\Source.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // From here on we can work with worksheets, ranges, and pivots.
```

**Why this matters:**  
`Workbook` abstracts the whole Excel file into an in‑memory model. Without loading it first you can’t inspect the pivot’s location or copy rows. Also, the constructor automatically detects the file format (XLS, XLSX, CSV, etc.), so you don’t need extra code for format detection.

---

## Step 2: How to Copy Rows – Defining the Pivot Area

Now that the workbook is in memory, we need to tell Aspose.Cells which rows contain the pivot. In our example the pivot lives in **A1:J20**, which translates to rows **0‑19** (zero‑based indexing). We’ll wrap that in a `CellArea` structure.

```csharp
        // Step 2: Define the cell area that contains the pivot table (A1:J20)
        // Row indices are zero‑based, column indices are also zero‑based.
        CellArea copyRange = new CellArea(startRow: 0, startColumn: 0, endRow: 19, endColumn: 9);
```

**Why we use `CellArea`:**  
It’s a lightweight way to describe a rectangular block. When you later call `CopyRows`, the method reads this object to know exactly which rows to duplicate. If you ever need to adjust the range (say the pivot grows to column K), you only change the `endColumn` value.

---

## Step 3: Access the Target Worksheet

Most workbooks have a single sheet, but the API works the same for multiple sheets. Grab the first worksheet (index 0) – that’s where the original pivot lives.

```csharp
        // Step 3: Get the first worksheet from the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**Pro tip:**  
If you have named sheets, you can also retrieve them by name: `workbook.Worksheets["Sheet1"]`. This helps avoid hard‑coding indices when the workbook structure changes.

---

## Step 4: How to Copy Rows – Duplicating the Pivot Table

Here’s the heart of **how to duplicate pivot**: we copy the rows containing the pivot to a new location. In our case we start at row 31 (zero‑based index 30). The `CopyRows` method copies *both* the data and the underlying pivot cache, so the new rows behave exactly like the original.

```csharp
        // Step 4: Copy the rows of the defined range to a new location (starting at row 31)
        // The third argument is the destination start row (zero‑based).
        worksheet.Cells.CopyRows(copyRange.StartRow, copyRange.EndRow, destinationRow: 30);
```

**What’s happening under the hood?**  
`CopyRows` clones each row, preserving formulas, styles, and pivot definitions. Because the pivot’s cache lives at the workbook level, the duplicated pivot automatically references the same data source – no extra configuration needed.

**Edge case – hidden rows:**  
If any of the rows in the source range are hidden, they stay hidden after copying. If you want to unhide them, call `worksheet.Rows[destRow].IsHidden = false` after the copy.

---

## Step 5: Save the Workbook – Verifying the Duplicate

Finally, write the changes back to disk. You can overwrite the original file or, safer, save to a new name so you can compare the before/after.

```csharp
        // Step 5: Save the workbook – the pivot table is now duplicated in the new rows
        string outputPath = @"C:\Data\CopyWithPivot.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine("Pivot duplicated successfully! Check " + outputPath);
    }
}
```

**Result you should see:**  
Open `CopyWithPivot.xlsx`. You’ll find the original pivot at **A1:J20** and an identical copy starting at **A31:J50**. Both pivots can be refreshed independently, and any slicers attached to the original will still work for the copy because they share the same cache.

---

## Common Questions & Variations

### Can I duplicate multiple pivots at once?

Absolutely. Loop through all pivot tables (`worksheet.PivotTables`) and copy each one’s range to a different destination. Just make sure the destination ranges don’t overlap.

### What if the source workbook is password‑protected?

Aspose.Cells lets you open a protected file by passing the password to the `Workbook` constructor:

```csharp
Workbook workbook = new Workbook(sourcePath, new LoadOptions { Password = "mySecret" });
```

### How to copy rows without affecting formulas?

If you only need the *values* (no formulas), use `CopyRows` with the `CopyOptions` flag:

```csharp
worksheet.Cells.CopyRows(sourceStart, sourceEnd, destStart, new CopyOptions { CopyValues = true });
```

### Is there a way to copy rows to a *different* workbook?

Yes. After copying rows in the source sheet, you can clone the worksheet into another `Workbook` instance via `targetWorkbook.Worksheets.AddCopy(worksheet)`.

---

## Pro Tips for Reliable Excel Automation Copy Rows

- **Validate the range** before copying. A quick `if (copyRange.EndRow >= worksheet.Cells.MaxDataRow)` prevents out‑of‑range errors.  
- **Turn off calculation** while copying large ranges: `workbook.Settings.CalcMode = CalcMode.Manual;` – this speeds up the operation dramatically.  
- **Dispose objects** (`workbook.Dispose()`) if you’re processing many files in a loop to free native resources.  
- **Log the operation** – especially in production pipelines – so you can trace which files were processed and catch failures early.

---

## Conclusion

You now know **how to duplicate pivot** tables in C# using Aspose.Cells, and you’ve seen the full workflow from **load excel workbook c#** to **excel automation copy rows** and finally saving the result. The example is self‑contained, runs out of the box, and can be extended to handle multiple pivots, protected files, or cross‑workbook copying.

Next steps? Try adapting the script to:

- Refresh the duplicated pivot programmatically (`pivotTable.RefreshData();`).  
- Export the duplicated area to a CSV for downstream processing.  
- Integrate the code into an ASP.NET Core API so users can upload a file and receive a duplicated‑pivot version instantly.

Happy coding, and may your Excel automation be ever smooth!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}