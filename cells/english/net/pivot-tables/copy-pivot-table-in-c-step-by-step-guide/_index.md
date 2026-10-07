---
category: general
date: 2026-03-18
description: Copy pivot table in C# with Aspose.Cells. Learn how to copy excel range,
  duplicate excel pivot, copy range to new sheet and copy pivot to sheet in minutes.
draft: false
keywords:
- copy pivot table
- copy excel range
- duplicate excel pivot
- copy range to new
- copy pivot to sheet
language: en
og_description: Copy pivot table in C# using Aspose.Cells. Learn to duplicate excel
  pivot, copy excel range to new location, and copy pivot to sheet with full code
  examples.
og_title: Copy pivot table in C# – Complete Programming Guide
tags:
- Aspose.Cells
- C#
- Excel automation
title: Copy pivot table in C# – Step‑by‑Step Guide
url: /net/pivot-tables/copy-pivot-table-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copy pivot table in C# – Complete Programming Guide

Ever needed to **copy pivot table** from one part of a workbook to another, but weren't sure how to do it without losing the underlying data connections? You're not alone. Many developers hit this snag when automating Excel reports, especially when the pivot lives inside a larger data block. The good news? With Aspose.Cells you can copy the pivot table **exactly as it appears**, and you’ll also learn how to **copy excel range**, **duplicate excel pivot**, and even **copy pivot to sheet** with just a few lines of C#.

In this tutorial we’ll walk through a real‑world scenario: moving a pivot that occupies *A1:J20* to a new area *M1:V20* in the same worksheet. By the end you’ll have a runnable program, understand why each step matters, and know how to adapt the code for other ranges or even separate worksheets. No external docs needed—everything’s right here.

---

## Prerequisites

Before we dive in, make sure you have:

- **Aspose.Cells for .NET** (version 23.9 or later). You can grab it via NuGet: `Install-Package Aspose.Cells`.
- A basic C# development environment (Visual Studio 2022, Rider, or VS Code with the C# extension).
- An Excel file (`source.xlsx`) that contains a pivot table within the range *A1:J20*.

That’s all. If you’re comfortable creating a console app, you’re ready to roll.

---

## How to copy pivot table in Aspose.Cells

The core of the solution is a single call to `Worksheet.Cells.CopyRange`. This method not only copies raw cell values but also preserves pivot tables, charts, and other rich objects automatically. Let’s break it down.

### Step 1: Load the source workbook

First we need to bring the workbook into memory.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Why this matters:** Loading the workbook creates an in‑memory representation that Aspose.Cells can manipulate without launching Excel. It’s fast, thread‑safe, and works on servers.

### Step 2: Grab the first worksheet

Most examples use the first sheet, but you can target any index or name.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = sourceWorkbook.Worksheets[0];
```

> **Tip:** If you need to **copy pivot to sheet** instead of the same sheet, just change the `worksheet` reference to another `Worksheet` object.

### Step 3: Define the source and target ranges

We’ll use `CellArea` structs to describe the blocks we’re moving.

```csharp
        // Define the source range (A1:J20) that contains the pivot table
        CellArea sourceRange = new CellArea(0, 0, 19, 9);   // rows 0‑19, columns 0‑9

        // Define the target range (M1:V20) where the data will be copied
        CellArea targetRange = new CellArea(0, 12, 19, 21); // rows 0‑19, columns 12‑21
```

> **Explanation:** Row and column indices are zero‑based. Column 0 = **A**, column 12 = **M**, and so on. Adjust these numbers if your pivot lives elsewhere.

### Step 4: Perform the copy operation

Now the magic happens. Setting the last boolean parameter to `true` tells Aspose.Cells to copy all objects—including the pivot.

```csharp
        // Copy the source range to the target range; pivot tables are copied automatically
        worksheet.Cells.CopyRange(
            sourceRange.StartRow, sourceRange.StartColumn,
            sourceRange.EndRow, sourceRange.EndColumn,
            targetRange.StartRow, targetRange.StartColumn,
            true);
```

> **Why `true`?** The flag indicates “copy all objects”. If you set it to `false`, only plain cell values would move, and the pivot would be lost.

### Step 5: Save the workbook

Finally, write the modified workbook back to disk.

```csharp
        // Save the workbook with the copied range
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copy-pivot.xlsx");
    }
}
```

> **Result:** `copy-pivot.xlsx` now contains the original pivot at *A1:J20* **and** an identical copy at *M1:V20*. Open the file in Excel to verify that both pivots are functional and retain their data connections.

---

## Copy Excel range to a new location – a quick variation

Sometimes you only need to **copy excel range** without worrying about pivots. The same `CopyRange` method does the trick; just set the last argument to `false`.

```csharp
worksheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    false); // plain values only
```

> **When to use:** If you’re moving raw data for a temporary calculation sheet, disabling object copy saves memory and speeds up the operation.

---

## Duplicate excel pivot across multiple sheets

What if you want to **duplicate excel pivot** on a different worksheet? The pattern stays the same; you just reference another `Worksheet` for the destination.

```csharp
// Assume we have a second sheet already created
Worksheet destSheet = sourceWorkbook.Worksheets.Add("PivotCopy");

// Copy the pivot (and its data source) to the new sheet starting at A1
destSheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    0, 0, // destination at A1
    true);
```

> **Edge case:** If the source pivot uses a table that lives on the original sheet, Aspose.Cells will also copy the underlying table definition, ensuring the new pivot works out‑of‑the‑box.

---

## Common pitfalls and how to avoid them

| Pitfall | Why it happens | Fix |
|---------|----------------|-----|
| **Pivot loses its cache** | Using `CopyRange` with `false` or a custom copy routine that ignores objects. | Always pass `true` when you need the pivot itself. |
| **Target cells already contain data** | Overwrites silently, potentially corrupting existing formulas. | Clear the target area first: `worksheet.Cells.ClearRange(targetRange.StartRow, targetRange.StartColumn, targetRange.EndRow, targetRange.EndColumn, true);` |
| **Source range doesn’t include the whole pivot** | Pivot tables span more rows/columns than you expect (e.g., hidden rows). | Use `worksheet.PivotTables[0].DataRange` to programmatically fetch the exact bounds. |
| **Copying between workbooks** | `CopyRange` works only within the same workbook. | Use `sourceWorksheet.Cells.CopyRange` to a temporary range, then `destWorkbook.Worksheets.AddCopy(sourceWorksheet);` |

---

## Expected output & verification

After running the program:

1. Open `copy-pivot.xlsx`.
2. You’ll see two identical pivot tables—one at **A1:J20**, another at **M1:V20**.
3. Refresh any pivot; both should reflect the same underlying data.
4. If you duplicated to another sheet, the new sheet will contain a functional copy as well.

A quick way to verify via code:

```csharp
int pivotCount = worksheet.PivotTables.Count; // should be 2 after copy
Console.WriteLine($"Pivot tables on the sheet: {pivotCount}");
```

---

## Pro tip: Automate range detection

Hard‑coding `CellArea` works for static reports, but production code often needs to locate the pivot dynamically.

```csharp
// Find the first pivot table on the sheet
PivotTable pt = worksheet.PivotTables[0];
CellArea ptRange = pt.DataRange;

// Use the detected range for copying
worksheet.Cells.CopyRange(
    ptRange.StartRow, ptRange.StartColumn,
    ptRange.EndRow, ptRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    true);
```

> **Why bother?** This makes your solution resilient to layout changes—no more “Oops, the pivot moved to B2” errors.

---

![copy pivot table example](copy-pivot.png){alt="copy pivot table example"}

*The screenshot (placeholder) shows the original pivot on the left and the duplicated one on the right.*

---

## Recap

We’ve just covered how to **copy pivot table** in C# using Aspose.Cells, explored ways to **copy excel range**, **duplicate excel pivot**, and even **copy pivot to sheet** across worksheets. The key takeaways are:

- Use `Worksheet.Cells.CopyRange` with the `true` flag to preserve rich objects.
- Define source and target `CellArea` objects with zero‑based indices.
- Adjust the destination worksheet if you need to **copy pivot to sheet**.
- Mind edge cases like existing data, hidden rows, and cross‑workbook scenarios.

---

## What’s next?

- **Dynamic pivot discovery**: Build a helper that scans a workbook for all pivots and replicates them automatically.
- **Export to PDF/HTML**: After copying, you might want to render the sheet to a report format—Aspose.Cells handles that too.
- **Performance tuning**: For massive workbooks, consider disabling calculation before copying and re‑enabling it afterward.

Feel free to experiment: change the target coordinates, copy to a brand‑new workbook, or even loop over multiple worksheets to create a consolidated report. The possibilities are endless, and with the foundation you now have, you’ll be able to adapt the code to virtually any Excel automation task.

Happy coding, and may your pivots always stay perfectly in sync!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}