---
category: general
date: 2026-02-09
description: Create new Excel workbook and learn how to copy pivot tables effortlessly.
  This guide shows how to duplicate pivot table and save workbook as new.
draft: false
keywords:
- create new excel workbook
- how to copy pivot
- duplicate pivot table
- save workbook as new
- how to copy worksheet
language: en
og_description: Create new Excel workbook in C# and copy a pivot table instantly.
  Learn how to duplicate pivot table and save workbook as new with a complete code
  sample.
og_title: Create New Excel Workbook – Step‑by‑Step Pivot Copy
tags:
- excel
- csharp
- aspose.cells
- automation
title: Create New Excel Workbook – Copy & Duplicate Pivot Table
url: /net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create New Excel Workbook – Copy & Duplicate Pivot Table

Ever needed to **create new Excel workbook** that carries over a complex pivot table from an existing file? You're not the only one—many developers hit this roadblock when automating reporting pipelines. The good news is that with a few lines of C# and the Aspose.Cells library you can **how to copy pivot** quickly, **duplicate pivot table**, and **save workbook as new** without opening Excel manually.

In this guide we’ll walk through the entire process, from loading the source workbook to saving the duplicated version. By the end you’ll have a ready‑to‑run snippet that you can drop into any .NET project. No fluff, just a practical solution you can test today.

## What This Tutorial Covers

* **Prerequisites** – .NET 6+ (or .NET Framework 4.6+), Visual Studio, and the Aspose.Cells for .NET NuGet package.
* Step‑by‑step code that **creates new Excel workbook**, copies the pivot, and writes the result to disk.
* Explanations of **why** each line matters, not just **what** it does.
* Tips for handling edge cases such as hidden worksheets or large data ranges.
* A quick look at **how to copy worksheet** if you ever need the whole sheet instead of just the pivot.

Ready? Let’s dive in.

![create new excel workbook illustration](image.png "Diagram showing source workbook, pivot copy, and destination workbook")

## Step 1: Set Up the Project and Install Aspose.Cells

Before we can **create new Excel workbook**, we need a project that references the right library.

```csharp
// Install the Aspose.Cells package via NuGet:
//   dotnet add package Aspose.Cells
using Aspose.Cells;   // Provides Workbook, Worksheet, Range, etc.
using System;        // For basic .NET types
```

*Why this matters:* Aspose.Cells works entirely in memory, so you never have to launch Excel on the server. It also preserves pivot cache information, which is essential for a true **duplicate pivot table**.

> **Pro tip:** If you’re targeting .NET Core, make sure your project’s runtime identifier (RID) matches the platform you’ll deploy to; otherwise you might hit native library loading errors.

## Step 2: Load the Source Workbook that Holds the Pivot

Now we’ll **how to copy pivot** from an existing file. The source workbook can be anywhere on disk, a stream, or even a byte array.

```csharp
// Step 2: Load the source workbook that contains the pivot table
string sourcePath = @"C:\Reports\source.xlsx";
Workbook sourceWorkbook = new Workbook(sourcePath);

// Grab the first worksheet (adjust the index if your pivot lives elsewhere)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that encloses the pivot table – A1:D20 in this example
Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");
```

*Why we pick a range:* A pivot table lives inside a regular cell range, but it also has hidden cache data attached to the sheet. By copying the range **including the pivot**, Aspose.Cells ensures the cache travels with it, giving you a functional **duplicate pivot table** in the destination file.

## Step 3: Create a New Excel Workbook to Receive the Copied Data

Here’s where we actually **create new Excel workbook** that will hold the duplicated pivot.

```csharp
// Step 3: Create a fresh workbook (empty) for the destination
Workbook destinationWorkbook = new Workbook(); // Starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

// Destination starts at A1 – you could offset if you need space for other data
Range destinationRange = destinationSheet.Cells.CreateRange("A1");
```

> **Why a fresh workbook?** Starting from a clean slate guarantees that no residual formatting or hidden objects interfere with the copied pivot. It also makes the resulting file smaller, which is handy for automated email attachments.

## Step 4: Copy the Pivot Range to the New Workbook

Now we perform the actual **how to copy pivot** operation.

```csharp
// Step 4: Copy the range (including the pivot) from source to destination
sourceRange.Copy(destinationRange);
```

That single line does the heavy lifting:

* The cell values, formulas, and formatting are transferred.
* The pivot cache is duplicated, so the new pivot remains fully functional.
* Any relative references inside the pivot adjust automatically to the new location.

### Handling Edge Cases

* **Hidden worksheets:** If the source sheet is hidden, the pivot still copies fine, but you might want to unhide the destination sheet for user visibility:
  ```csharp
  destinationSheet.IsVisible = true;
  ```
* **Large data sets:** For ranges larger than a few thousand rows, consider using `CopyTo` with `CopyOptions` to stream the operation and reduce memory pressure.

## Step 5: Save the Destination Workbook as a New File

Finally, we **save workbook as new** and verify the result.

```csharp
// Step 5: Save the destination workbook with the duplicated pivot table
string destPath = @"C:\Reports\copied.xlsx";
destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

// Quick verification – open the file manually or read a cell value
Console.WriteLine($"Workbook saved to {destPath}");
```

If you open `copied.xlsx` you’ll see an exact replica of the original pivot, ready for further manipulation or distribution.

### Optional: How to Copy Worksheet Instead of Just the Pivot

Sometimes you want the entire sheet, not just the pivot. The same API makes it trivial:

```csharp
// Copy the whole worksheet (including all charts, tables, etc.)
sourceSheet.CopyTo(destinationWorkbook, 0); // Inserts at index 0
destinationWorkbook.Save(@"C:\Reports\full_copy.xlsx");
```

This satisfies the **how to copy worksheet** query and can be handy when you need to preserve additional sheet‑level settings.

## Full Working Example

Putting it all together, here’s a self‑contained console app you can compile and run:

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load source workbook
        string sourcePath = @"C:\Reports\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:D20");

        // 2️⃣ Create destination workbook
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
        Range destinationRange = destinationSheet.Cells.CreateRange("A1");

        // 3️⃣ Copy the pivot (range)
        sourceRange.Copy(destinationRange);

        // 4️⃣ Save as new file
        string destPath = @"C:\Reports\copied.xlsx";
        destinationWorkbook.Save(destPath, SaveFormat.Xlsx);

        Console.WriteLine($"✅ Successfully created new Excel workbook with duplicated pivot table at {destPath}");
    }
}
```

**Expected output:** The console prints a success message, and `copied.xlsx` appears in `C:\Reports` with a functional pivot identical to the one in `source.xlsx`.

## Common Questions & Pitfalls

* **Will formulas inside the pivot break?** No—because the pivot cache travels with the range, all calculated fields stay intact.
* **What if the source pivot uses external data connections?** Those connections are *not* copied. You’ll need to re‑establish them in the destination workbook or convert the pivot to a static table first.
* **Can I copy multiple pivots at once?** Absolutely—just define a larger range that encompasses all pivots, or loop through each `PivotTable` object in `sourceSheet.PivotTables` and copy them individually.
* **Do I need to dispose of the `Workbook` objects?** They implement `IDisposable`, so wrapping them in `using` statements is a good habit, especially in high‑throughput services.

## Conclusion

You now know **how to create new Excel workbook**, copy a pivot, **duplicate pivot table**, and **save workbook as new** using C# and Aspose.Cells. The steps are straightforward: load, create, copy, and save. With the optional **how to copy worksheet** snippet you also have a fallback for full‑sheet duplication.

Next up, you might explore:

* Adding custom formatting to the duplicated pivot.
* Refreshing the pivot cache programmatically after data changes.
* Exporting the workbook to PDF or CSV for downstream systems.

Give it a spin, tweak the range, and let the automation take the grunt work out of your reporting workflow. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}