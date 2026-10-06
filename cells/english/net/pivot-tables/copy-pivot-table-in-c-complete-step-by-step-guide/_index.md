---
category: general
date: 2026-03-25
description: Copy pivot table with C# using Aspose.Cells. Learn how to copy pivot,
  export pivot table file and preserve data in minutes.
draft: false
keywords:
- copy pivot table
- how to copy pivot
- export pivot table file
- Aspose.Cells pivot
- C# Excel automation
language: en
og_description: Copy pivot table in C# using Aspose.Cells. This guide shows how to
  copy pivot, export pivot table file and keep all settings intact.
og_title: Copy Pivot Table in C# – Full Programming Tutorial
tags:
- C#
- Excel
- Aspose.Cells
- Data Export
title: Copy Pivot Table in C# – Complete Step‑by‑Step Guide
url: /net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copy Pivot Table in C# – Complete Step‑by‑Step Guide

Ever needed to **copy pivot table** from one workbook to another and wondered whether the pivot logic survives the move? You're not the only one. In many reporting pipelines we generate a master workbook, then ship a lightweight copy that still lets end‑users slice the data. The good news? With a few lines of C# and Aspose.Cells you can do exactly that—no manual fiddling required.

In this tutorial we’ll walk through the whole process: loading the source file, selecting the range that contains the pivot, pasting it into a fresh workbook while preserving the pivot definition, and finally **export pivot table file** for downstream consumption. By the end you’ll know *how to copy pivot* programmatically and have a ready‑to‑run example you can drop into your project.

## Prerequisites

- .NET 6+ (or .NET Framework 4.6+) installed  
- Aspose.Cells for .NET NuGet package (`Install-Package Aspose.Cells`)  
- A source Excel file (`source.xlsx`) that already contains a pivot table (any size works)  
- Basic C# knowledge; no deep Excel internals required  

If you’re missing any of these, just add the NuGet package and open Visual Studio—nothing more.

## What the Code Does (Overview)

1. **Load** the workbook that holds the original pivot.  
2. **Define** a `Range` that encloses the whole pivot (including its cache).  
3. **Create** a brand‑new workbook that will become the destination.  
4. **Paste** the range with `CopyPivotTable = true` so the pivot definition is copied, not just the values.  
5. **Save** the destination file, giving you an **export pivot table file** you can share.

That’s the entire workflow in five tidy steps. Let’s dive into each one.

## Step 1 – Load the Source Workbook that Contains the Pivot Table

First we need to bring the source file into memory. Aspose.Cells makes this a one‑liner.

```csharp
using Aspose.Cells;

// Load the source workbook (replace the path with your actual file)
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet – adjust the index if your pivot lives elsewhere
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
```

*Why this matters:* Loading the workbook gives us access to the underlying pivot cache. If you only copy cell values, the pivot loses its slicer capability. By keeping the workbook object alive, we preserve the full pivot metadata.

## Step 2 – Define the Range That Includes the Pivot Table

A pivot isn’t just a block of cells; it also has hidden cache data. The safest way is to select a rectangle that fully surrounds the visible area. In most cases `A1:E20` works, but you can programmatically discover the exact bounds using `PivotTable` properties.

```csharp
// Example range – adjust to match your pivot's size
Range sourceRange = sourceSheet.Cells.CreateRange("A1:E20");

// (Optional) Dynamically get the used range of the pivot:
PivotTable pivot = sourceSheet.PivotTables[0];
int firstRow = pivot.Row - 1;      // include header row
int firstCol = pivot.Column - 1;   // include field list
int lastRow  = pivot.Row + pivot.RowCount;
int lastCol  = pivot.Column + pivot.ColumnCount;
Range dynamicRange = sourceSheet.Cells.CreateRange(firstRow, firstCol,
                                                    lastRow - firstRow + 1,
                                                    lastCol - firstCol + 1);
```

*Why we choose a range:* The `Paste` method works on a `Range` object. By specifying the exact area, we ensure that both the pivot layout and its cache travel together.

## Step 3 – Create a New Destination Workbook

Now we spin up a blank workbook that will receive the copied pivot. Nothing fancy, just a clean slate.

```csharp
// Initialize an empty workbook – it comes with one default worksheet
Workbook destinationWorkbook = new Workbook();
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

*Tip:* If you need to preserve existing worksheets (e.g., a template), you can add the new workbook as a clone of a template file instead of using the empty constructor.

## Step 4 – Paste the Range While Preserving the Pivot Table

Here’s the heart of the operation. Setting `CopyPivotTable = true` tells Aspose.Cells to transfer the pivot definition, not just the displayed values.

```csharp
destinationSheet.Cells.Paste(
    sourceRange,
    new PasteOptions
    {
        PasteType = PasteType.All,      // copy everything: formulas, formats, etc.
        CopyPivotTable = true           // crucial – keeps the pivot functional
    });
```

*What happens under the hood?* Aspose.Cells recreates the pivot cache in the destination workbook, rewires the pivot’s data source, and retains slicers, filters, and calculated fields. The result is a fully interactive pivot—exactly what you’d expect if you had duplicated the sheet manually in Excel.

## Step 5 – Save the Resulting Workbook (Export Pivot Table File)

Finally we write the destination workbook to disk. The file you get is your **export pivot table file** ready for distribution.

```csharp
destinationWorkbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");
```

Open `copy-pivot.xlsx` in Excel, and you’ll see the pivot table intact, ready to be refreshed or sliced.

## Full Working Example (All Steps Combined)

Below is the complete program you can copy‑paste into a console app. It includes error handling and comments for clarity.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                // 1️⃣ Load source workbook with the pivot table
                Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
                Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

                // 2️⃣ Define the range that fully encloses the pivot
                // Adjust "A1:E20" as needed, or use dynamic detection shown earlier
                Range sourceRange = sourceSheet.Cells.CreateRange("A1:E20");

                // 3️⃣ Create a fresh destination workbook
                Workbook destinationWorkbook = new Workbook();
                Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

                // 4️⃣ Paste the range and keep the pivot definition
                destinationSheet.Cells.Paste(
                    sourceRange,
                    new PasteOptions
                    {
                        PasteType = PasteType.All,
                        CopyPivotTable = true
                    });

                // 5️⃣ Save the new file – this is your exported pivot table file
                destinationWorkbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");

                Console.WriteLine("✅ Pivot table copied successfully! File saved as copy-pivot.xlsx");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❌ An error occurred: {ex.Message}");
            }
        }
    }
}
```

**Expected outcome:** When you open `copy-pivot.xlsx`, the pivot table appears exactly as in `source.xlsx`. You can refresh it, change filters, or even add new data sources without losing functionality.

## Common Questions & Edge Cases

### What if the source workbook has multiple pivots?

Loop through `sourceSheet.PivotTables` and repeat the copy‑paste for each. Just be sure each destination range doesn’t overlap.

```csharp
int destRow = 0;
foreach (PivotTable pt in sourceSheet.PivotTables)
{
    // Calculate a non‑overlapping destination range for each pivot
    Range src = sourceSheet.Cells.CreateRange(pt.Row, pt.Column,
                                              pt.RowCount + 5, pt.ColumnCount + 5);
    destinationSheet.Cells.Paste(src, new PasteOptions { PasteType = PasteType.All, CopyPivotTable = true });
    destRow += pt.RowCount + 10; // move down for the next pivot
}
```

### Does this work with external data sources (e.g., SQL)?

If the original pivot pulls from an external connection, the connection string is also copied. However, the destination workbook must have access to the same data source. You may need to adjust credentials or use `WorkbookSettings` to allow external connections.

### Can I copy only the pivot layout (no data)?

Set `PasteOptions.PasteType = PasteType.Formulas` and keep `CopyPivotTable = true`. This copies the structure while leaving the data cache empty, forcing a refresh on first open.

### What about protecting the sheet?

If the source sheet is protected, unprotect it before copying, or pass the appropriate `Password` to `Worksheet.Unprotect`. After pasting, you can re‑apply protection on the destination sheet.

## Pro Tips & Pitfalls

- **Pro tip:** Always use the latest Aspose.Cells version; older releases had a bug where `CopyPivotTable` ignored slicers.
- **Watch out for:** Large pivot caches can bloat the destination file. If size matters, consider clearing unused fields before copy.
- **Performance tip:** When copying many worksheets, disable `WorkbookSettings.EnableThreadedCalculation` temporarily to speed up the operation.
- **Naming clash:** If the destination workbook already contains a pivot with the same name, Aspose will rename the incoming one (`PivotTable1_1`). Rename manually if you need a specific identifier.

## Visual Summary

![Copy pivot table in C# – diagram showing source workbook → range selection → paste with pivot preservation → destination file](copy-pivot-diagram.png "Copy pivot table workflow illustration")

*Alt text:* **Copy pivot table** workflow diagram illustrating source, range, paste options, and exported file.

## Conclusion

We’ve covered everything you need to **copy pivot table** using C# and Aspose.Cells: loading the source, selecting the correct range, preserving the pivot definition during paste, and finally exporting the result as a standalone file. The snippet above is production‑ready; just plug in your paths and you’re good to go.

Now that you know *how to copy pivot* programmatically, you can automate report distribution, build template generators, or integrate Excel analytics into larger .NET services. Next up you might explore **export pivot table file** to other formats (PDF, CSV) or embed the workbook into a web API for on‑the‑fly analytics.

Got a twist you’d like to share—perhaps copying pivots across different Excel versions or handling PowerPivot models? Drop a comment, and let’s keep the conversation going. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}