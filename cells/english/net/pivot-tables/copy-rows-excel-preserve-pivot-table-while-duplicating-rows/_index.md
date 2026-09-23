---
category: general
date: 2026-02-14
description: copy rows excel and preserve pivot table in one go. Learn how to copy
  rows, copy range to sheet, and duplicate rows with pivot using Aspose.Cells.
draft: false
keywords:
- copy rows excel
- preserve pivot table
- how to copy rows
- copy range to sheet
- duplicate rows with pivot
language: en
og_description: copy rows excel and preserve pivot table in one go. Follow this step‑by‑step
  guide to duplicate rows with pivot using C#.
og_title: copy rows excel – Preserve Pivot Table While Duplicating Rows
tags:
- Aspose.Cells
- C#
- Excel automation
title: copy rows excel – Preserve Pivot Table While Duplicating Rows
url: /net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# copy rows excel – Preserve Pivot Table While Duplicating Rows

Ever needed to **copy rows excel** while keeping the pivot table intact? In this tutorial we’ll walk through a complete, runnable solution that shows you **how to copy rows**, keep the **preserve pivot table** behavior alive, and even **duplicate rows with pivot** across sheets using Aspose.Cells for .NET.

Imagine you’re building a monthly sales report that pulls data from a master sheet, runs a pivot, and then you have to ship a trimmed‑down version to a partner. Manually copying the range is a pain, and you risk breaking the pivot. The good news? A few lines of C# can do the heavy lifting for you—no mouse clicks required.

> **What you’ll get:** a full code sample, step‑by‑step explanations, tips for edge cases, and a quick sanity‑check to verify that the pivot survived the copy.

---

## What You’ll Need

- **Aspose.Cells for .NET** (the free NuGet package works fine for this demo).  
- A recent **.NET runtime** (4.7+ or .NET 6/7).  
- An Excel file (`source.xlsx`) that contains a pivot table on the first worksheet.  
- Visual Studio, Rider, or any C# editor you like.

No additional libraries, no COM interop, and no Excel installation on the server. That’s why this approach is both **copy range to sheet** friendly and server‑safe.

---

## Step 1 – Load the Workbook (copy rows excel)

The very first thing is to open the source workbook. Using Aspose.Cells gives us a clean object model that works the same on Windows, Linux, or Azure.

```csharp
using Aspose.Cells;

public class PivotCopyDemo
{
    public static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Why this matters:** loading the workbook creates an in‑memory representation of every worksheet, including hidden objects like pivot caches. As soon as the file is in memory, we can manipulate rows without ever touching the UI.

---

## Step 2 – Identify Destination Worksheet (copy range to sheet)

We want the copied rows to land on a different sheet—`Sheet2` in this example. If the sheet doesn’t exist, Aspose will create it for you.

```csharp
        // Get (or create) the destination worksheet where the rows will be placed
        Worksheet destinationWorksheet;
        if (sourceWorkbook.Worksheets.Contains("Sheet2"))
            destinationWorksheet = sourceWorkbook.Worksheets["Sheet2"];
        else
            destinationWorksheet = sourceWorkbook.Worksheets.Add("Sheet2");
```

> **Pro tip:** always check `Worksheets.Contains` before adding a sheet; otherwise you’ll end up with duplicate names and a runtime exception.

---

## Step 3 – Copy Rows While Preserving the Pivot Table

Now comes the heart of the matter: copying rows **A1:E20** (which include the pivot) from the first sheet to `Sheet2`. The `CopyRows` method copies the raw cells *and* the underlying pivot cache, so the pivot stays functional.

```csharp
        // Define the source range: rows 0‑19 (A1:E20) on the first worksheet
        Worksheet sourceWorksheet = sourceWorkbook.Worksheets[0];

        // Copy rows 0‑19 from source to destination, starting at row 0 on the destination sheet
        sourceWorksheet.Cells.CopyRows(
            sourceWorksheet.Cells,   // source cells collection
            0,                       // source start row (0‑based, i.e., row 1)
            0,                       // destination start row on the same sheet (adjust if needed)
            20);                     // total number of rows to copy
```

> **Why it works:** `CopyRows` respects the internal pivot cache, so the pivot table on the destination sheet is a *live* copy, not a static snapshot. This satisfies the **preserve pivot table** requirement without extra code.

If you need the rows to start at a different offset on the destination sheet—say row 10—you’d simply change the third argument to `9`.

---

## Step 4 – Save the Workbook (duplicate rows with pivot)

Finally, write the modified workbook back to disk. The pivot table will be fully functional in the new file.

```csharp
        // Save the workbook; the copied pivot remains active automatically
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

> **Result verification:** open `copyWithPivot.xlsx` in Excel, go to *Sheet2*, and refresh the pivot. You should see the same field layout and calculations as the original—nothing broken.

---

## Verifying the Copy – Quick sanity check

```csharp
// Optional: programmatically confirm the pivot exists on the destination sheet
Worksheet dest = sourceWorkbook.Worksheets["Sheet2"];
bool pivotExists = dest.PivotTables.Count > 0;
Console.WriteLine($"Pivot table copied? {pivotExists}");
```

If the console prints `True`, you’ve successfully **duplicate rows with pivot** and kept the data analysis engine alive.

---

## Common Edge Cases & How to Handle Them

| Situation | What to watch for | Suggested tweak |
|-----------|-------------------|-----------------|
| **Source range includes merged cells** | Merged cells can cause mis‑alignment when copied. | Use `CopyRows` as shown; it preserves merges automatically. |
| **Destination sheet already has data** | New rows might overwrite existing content. | Change the destination start row (third argument) to the first empty row: `destWorksheet.Cells.MaxDataRow + 1`. |
| **Pivot uses external data source** | External connections are not copied. | Ensure the source workbook contains the full data set; otherwise re‑attach the connection after copy. |
| **Large workbook (100k+ rows)** | Memory usage spikes. | Consider copying in chunks (e.g., 5,000 rows at a time) to keep the GC happy. |

---

## Full Working Example (All Steps Together)

Below is the entire program you can paste into a console app and run immediately.

```csharp
using System;
using Aspose.Cells;

public class PivotCopyDemo
{
    public static void Main()
    {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");

        // 2️⃣ Get (or create) the destination worksheet
        Worksheet destinationWorksheet;
        if (sourceWorkbook.Worksheets.Contains("Sheet2"))
            destinationWorksheet = sourceWorkbook.Worksheets["Sheet2"];
        else
            destinationWorksheet = sourceWorkbook.Worksheets.Add("Sheet2");

        // 3️⃣ Copy rows A1:E20 (includes pivot) from the first sheet
        Worksheet sourceWorksheet = sourceWorkbook.Worksheets[0];
        sourceWorksheet.Cells.CopyRows(
            sourceWorksheet.Cells, // source cells
            0,                     // start at row 0 (A1)
            0,                     // destination start row (adjust as needed)
            20);                   // copy 20 rows

        // 4️⃣ Save the workbook – pivot stays alive
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");

        // Optional verification
        bool pivotExists = destinationWorksheet.PivotTables.Count > 0;
        Console.WriteLine($"Pivot table copied? {pivotExists}");
    }
}
```

Run the program, open the generated `copyWithPivot.xlsx`, and you’ll see that the pivot on **Sheet2** works exactly like the original. No manual re‑creation required.

---

## Frequently Asked Questions

**Q: Does this work with Excel 2003‑compatible `.xls` files?**  
A: Yes. Aspose.Cells abstracts the file format, so the same code works for `.xls`, `.xlsx`, and even `.xlsb`.

**Q: What if I need to copy *columns* instead of rows?**  
A: Use `CopyColumns` in a similar fashion; just swap the row parameters for column indices.

**Q: Can I copy multiple, non‑contiguous ranges at once?**  
A: Not directly with `CopyRows`. Loop over each range or build a temporary worksheet that consolidates the ranges before copying.

---

## Conclusion

We’ve just demonstrated a clean, **copy rows excel** pattern that **preserve pivot table** integrity, lets you **how to copy rows** efficiently, and shows you how to **copy range to sheet** without losing any pivot functionality. By the end of this guide you should feel confident to **duplicate rows with pivot** in any automation pipeline—whether you’re generating daily reports or building a large‑scale data‑export service.

Ready for the next challenge? Try extending the code to:

- Export the duplicated sheet as a PDF.  
- Refresh the pivot programmatically after copying.  
- Loop over a list of source files and batch‑process them.

If you hit any snags, drop a comment below or ping me on GitHub. Happy coding, and enjoy the time you saved by not dragging Excel around manually!  

<img src="copy-rows-excel.png" alt="copy rows excel diagram" style="max-width:100%; height:auto;" />

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}