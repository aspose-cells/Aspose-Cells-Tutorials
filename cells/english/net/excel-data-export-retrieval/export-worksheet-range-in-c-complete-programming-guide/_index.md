---
category: general
date: 2026-05-04
description: Export worksheet range using C# with custom formatting. Learn how to
  export excel range and how to customize cell export in a few easy steps.
draft: false
keywords:
- export worksheet range
- how to export excel range
- how to customize cell export
- C# Excel export
- worksheet export options
language: en
og_description: Export worksheet range with C#. This guide shows how to export excel
  range and customize cell export quickly and reliably.
og_title: Export worksheet range in C# – Complete Programming Guide
tags:
- C#
- Excel
- Data Export
title: Export worksheet range in C# – Complete Programming Guide
url: /net/excel-data-export-retrieval/export-worksheet-range-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export worksheet range in C# – Complete Programming Guide

Ever needed to **export worksheet range** but the default output just wasn’t what you wanted? You’re not the only one—many developers hit that wall when they try to pull a block of cells into a CSV or JSON file. The good news? With a few lines of C# you can not only **export excel range** but also **customize cell export** to match any downstream format.

In this tutorial we’ll walk through a real‑world scenario: taking cells *A1:D10* from an Excel workbook, turning every value into a bracketed string, and writing the result to a file. By the end you’ll know exactly **how to export worksheet range** with full control over each cell’s representation, plus a handful of tips for edge cases you might run into later.

## What You’ll Need

- .NET 6 or later (the code works with .NET Framework 4.7+ as well)  
- The **GemBox.Spreadsheet** NuGet package (or any library that offers `ExportTableOptions`; the API shown is from GemBox)  
- A basic understanding of C# syntax – nothing fancy, just the usual `using` statements and object creation  

If you’ve got those, you’re ready to dive in.

## Step 1: Set Up the Export Options – Primary Control Point  

The first thing you do is create an `ExportTableOptions` instance and tell it to treat every cell as a string. This is the foundation for **how to export excel range** while keeping the data type consistent.

```csharp
using GemBox.Spreadsheet;

public class WorksheetExporter
{
    public void ExportRange(string sourcePath, string destinationPath)
    {
        // Load the workbook.
        var workbook = ExcelFile.Load(sourcePath);
        var worksheet = workbook.Worksheets[0]; // assume first sheet

        // Step 1: Create export options and enable string export.
        var exportOptions = new ExportTableOptions
        {
            ExportAsString = true // forces every cell to be exported as text
        };
```

*Why force string export?*  
When you later customize each cell, you’ll be injecting brackets and possibly other symbols. Keeping everything as a string prevents type‑conversion surprises (e.g., dates turning into serial numbers).

## Step 2: Hook Into the CellExport Event – Customizing Each Cell  

Now comes the fun part: **how to customize cell export**. GemBox raises a `CellExport` event for every cell that’s about to be written. By handling it you can wrap the value in brackets, prepend a prefix, or even skip a cell entirely.

```csharp
        // Step 2: Customize each cell's exported value.
        exportOptions.CellExport += (sender, e) =>
        {
            // e.Value holds the original cell content.
            // We'll wrap it in square brackets.
            e.Value = $"[{e.Value}]";
        };
```

*Pro tip:* If you only want to modify numeric cells, check `e.Value.GetType()` before applying the brackets. That tiny guard can save you from unintentionally mangling header text.

## Step 3: Export the Desired Range – The Core Action  

With options ready, you call `ExportTable`. The method takes the workbook you loaded, the address of the range you want, and the options you just configured.

```csharp
        // Step 3: Export the range A1:D10 using the configured options.
        worksheet.ExportTable(workbook, "A1:D10", exportOptions, destinationPath);
    }
}
```

The overload we used writes directly to a file (CSV by default). If you prefer an in‑memory string, swap the last argument for a `StringWriter` and read the result afterwards.

### Full Working Example

Below is a self‑contained console app you can paste into a new project and run instantly (just replace the file paths).

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License key (free version works with limited rows/columns).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        var exporter = new WorksheetExporter();
        exporter.ExportRange(
            sourcePath: @"C:\Temp\Sample.xlsx",
            destinationPath: @"C:\Temp\ExportedRange.csv");

        Console.WriteLine("Export completed. Check C:\\Temp\\ExportedRange.csv");
    }
}
```

**Expected output (CSV snippet):**

```
[Header1],[Header2],[Header3],[Header4]
[123],[456],[789],[012]
[ABC],[DEF],[GHI],[JKL]
...
```

Every cell from *A1* through *D10* is now wrapped in square brackets, exactly as we defined in the `CellExport` handler.

## Handling Common Edge Cases  

### 1. Empty Cells  
If a cell is empty, `e.Value` will be `null`. Trying to format it with string interpolation throws an exception. Guard against it:

```csharp
exportOptions.CellExport += (s, e) =>
{
    var raw = e.Value?.ToString() ?? string.Empty;
    e.Value = $"[{raw}]";
};
```

### 2. Large Ranges  
Exporting millions of rows can hit memory limits. In that scenario, stream the output instead of loading the whole workbook into memory:

```csharp
using (var writer = new StreamWriter(destinationPath))
{
    worksheet.ExportTable(workbook, "A1:D1000000", exportOptions, writer);
}
```

### 3. Different Delimiters  
CSV isn’t the only format you might need. Change the delimiter by adjusting `ExportTableOptions.CsvSeparator`:

```csharp
exportOptions.CsvSeparator = '\t'; // Tab‑delimited
```

## Frequently Asked Questions  

**Q: Does this work with .xlsx files created by Excel 365?**  
Absolutely. GemBox reads the modern OpenXML format without extra configuration.

**Q: Can I export multiple non‑contiguous ranges at once?**  
Not directly via a single `ExportTable` call. Loop over each range string (`"A1:D10"`, `"F1:H5"` etc.) and concatenate the outputs yourself.

**Q: What if I need to apply different formatting per column?**  
Inside the `CellExport` handler you have access to `e.ColumnIndex`. Use a `switch` statement to apply column‑specific logic.

## Wrap‑Up  

We’ve covered **how to export worksheet range** with full control over each cell’s appearance, demonstrated **how to export excel range** using `ExportTableOptions`, and showed **how to customize cell export** via the `CellExport` event. The complete solution lives in a few dozen lines of C#, yet it’s flexible enough for production‑grade scenarios.

Next steps? Try swapping the bracket wrapper for a JSON‑friendly format, or experiment with conditional logic that skips hidden rows. You might also explore exporting directly to a `MemoryStream` for web‑API responses—no temporary files required.

If you’ve followed along, you now have a solid, reusable pattern for exporting any worksheet range exactly the way you need. Happy coding, and feel free to drop a comment if you hit a snag!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}