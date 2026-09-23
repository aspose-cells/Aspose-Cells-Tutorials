---
category: general
date: 2026-03-29
description: Learn how to copy range, copy pivot tables, how to save workbook and
  how to load workbook in C#. Move pivot tables easily with step‑by‑step code.
draft: false
keywords:
- how to copy range
- copy pivot tables
- how to save workbook
- how to load workbook
- move pivot table
language: en
og_description: How to copy range, copy pivot tables, how to save workbook and how
  to load workbook in C#. Move pivot tables effortlessly with clear code.
og_title: How to copy range with pivot tables in C# – Complete Guide
tags:
- C#
- Aspose.Cells
- Excel automation
title: How to copy range with pivot tables in C# – Complete Guide
url: /net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to copy range with pivot tables in C# – Complete Guide

Ever wondered **how to copy range** that contains a pivot table without breaking the link to its source data? You're not the only one. In many real‑world projects I’ve hit this exact snag—Excel files arrive with sophisticated pivot tables, and the requirement is to reposition them or duplicate the data elsewhere.  

The good news? The solution is pretty straightforward once you know **how to load workbook**, make a copy, and then **how to save workbook** again. In this tutorial we’ll walk through the entire process, including how to **copy pivot tables**, and even a quick tip on **move pivot table** if you need it elsewhere in the same sheet.

By the end of this guide you’ll have a fully‑functional C# snippet that:

1. Loads an existing Excel file.  
2. Copies a range (including the pivot table) to a new location.  
3. Saves the modified workbook to a new file.

No external scripts, no manual fiddling—just clean, repeatable code.

---

## Prerequisites

- **.NET 6+** (any recent version works).  
- **Aspose.Cells for .NET** – the library that provides `Workbook`, `WorksheetCopyOptions`, etc. You can install it via NuGet:

```bash
dotnet add package Aspose.Cells
```

- An input workbook (`input.xlsx`) that already contains a pivot table in the range `A1:G20`.  
- Basic familiarity with C# and Visual Studio (or your favorite IDE).

> **Pro tip:** If you’re using a different Excel library (e.g., EPPlus), the concepts are the same—just swap the API calls.

---

## Step 1 – How to load workbook (Primary Setup)

Before we can copy anything, we need to bring the Excel file into memory.

```csharp
using Aspose.Cells;

// Step 1: Load the source workbook
var sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// Grab the first worksheet – this is where our pivot lives
var sourceWorksheet = sourceWorkbook.Worksheets[0];
```

**Why this matters:**  
Loading the workbook gives you an object model you can manipulate. Without `how to load workbook` correctly, any subsequent copy operation would throw a *FileNotFound* or *InvalidOperation* exception.  

> **Watch out:** If the file is large, consider using `LoadOptions` with `MemorySetting` to control memory usage.

---

## Step 2 – How to copy range (including the pivot)

Now comes the star of the show: copying a range that contains a pivot table. The `CopyRange` method, combined with `WorksheetCopyOptions`, does the heavy lifting.

```csharp
// Step 2: Copy a range that includes a pivot table to a new location
sourceWorksheet.CopyRange(
    "A1:G20",                                   // Source range
    new WorksheetCopyOptions { CopyPivotTables = true }, // Ensure pivot tables travel with the data
    sourceWorksheet,                           // Destination worksheet (same sheet in this case)
    "A25");                                     // Upper‑left corner of the destination
```

**Why we set `CopyPivotTables = true`:**  
By default, copying a range only moves the raw cells. The pivot cache stays behind, and the copied pivot becomes a static table. Setting `CopyPivotTables` preserves the live connection, so the duplicated pivot still refreshes when its source data changes.

**Edge case:** If the destination range overlaps the source, Aspose.Cells will throw an `ArgumentException`. Always pick a non‑overlapping target, or create a new worksheet first.

---

## Step 3 – How to save workbook (Persist the changes)

After the copy, you’ll want to write the changes back to disk. This is where **how to save workbook** comes into play.

```csharp
// Step 3: Save the modified workbook to a new file
sourceWorkbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

**What happens under the hood:**  
`Save` serializes the in‑memory workbook, including the newly‑copied pivot table, into a standard `.xlsx` package. If you need a different format (CSV, PDF, etc.), simply change the file extension or use the overload that accepts `SaveFormat`.

> **Tip:** Use `Workbook.Save(string, SaveOptions)` if you need to protect the file with a password or set other export options.

---

## Full Working Example

Putting it all together, here’s the complete, ready‑to‑run program:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ How to load workbook
        var sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
        var sourceWorksheet = sourceWorkbook.Worksheets[0];

        // 2️⃣ How to copy range (including pivot tables)
        sourceWorksheet.CopyRange(
            "A1:G20",
            new WorksheetCopyOptions { CopyPivotTables = true },
            sourceWorksheet,
            "A25");

        // 3️⃣ How to save workbook
        sourceWorkbook.Save(@"YOUR_DIRECTORY\output.xlsx");

        Console.WriteLine("✅ Range copied and workbook saved successfully!");
    }
}
```

**Expected result:**  
Open `output.xlsx`. You’ll see the original pivot table still sitting in `A1:G20`, and an identical, fully functional copy starting at `A25`. Both pivots point to the same source data, so refreshing one updates the other.

---

## Frequently Asked Questions & Variations

### Can I **move pivot table** instead of copying it?

Absolutely. After copying, simply clear the original range (or use `sourceWorksheet.Cells.ClearRange(0, 0, 19, 6)`) and then rename the destination range if needed. This effectively “moves” the pivot.

### What if the pivot uses an external data source?

`CopyPivotTables = true` copies only the pivot definition, not the external connection itself. Ensure the target workbook has access to the same data source, or recreate the connection after the copy.

### How do I copy to a **different worksheet**?

Just pass the destination worksheet object instead of `sourceWorksheet`:

```csharp
var destWorksheet = sourceWorkbook.Worksheets.Add("CopiedPivot");
sourceWorksheet.CopyRange("A1:G20", new WorksheetCopyOptions { CopyPivotTables = true }, destWorksheet, "A1");
```

### Is there a way to copy **multiple ranges** at once?

You can call `CopyRange` repeatedly or use `CopyRows`/`CopyColumns` for larger blocks. Looping over a list of address strings is a clean approach.

---

## Common Pitfalls & Pro Tips

- **Pivot cache size:** Large pivot caches can balloon the workbook size. If you only need the displayed data, consider `CopyPivotTables = false` and then use `PivotTable.RefreshData()` on the destination.
- **File paths:** Use `Path.Combine` to avoid hard‑coded separators, especially on cross‑platform .NET.
- **Performance:** For massive workbooks, wrap the copy in a `using (var stream = new MemoryStream())` and save to the stream first, then write to disk. This reduces I/O overhead.

---

## Conclusion

You now know **how to copy range** that contains a pivot table, how to **copy pivot tables**, and the exact steps to **how to load workbook** and **how to save workbook** after the operation. Whether you need to **move pivot table** within the same sheet or to another worksheet, the pattern stays the same—load, copy with the right options, and save.

Give it a try with your own files, tweak the destination address, and experiment with different pivot configurations. The more you play around, the more confident you’ll become at automating Excel tasks in C#.

---

![Diagram showing the source range A1:G20 being copied to A25 in the same worksheet – how to copy range with pivot tables](/images/how-to-copy-range-diagram.png "how to copy range with pivot tables")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}