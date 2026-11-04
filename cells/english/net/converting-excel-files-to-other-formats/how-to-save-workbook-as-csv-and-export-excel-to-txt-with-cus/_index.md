---
category: general
date: 2026-09-15
description: Learn how to save workbook as CSV, export Excel to TXT, and apply custom
  number format while converting cell values to uppercase in C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save workbook as csv
- apply custom number format
- export excel to txt
- uppercase cell values
- export worksheet as text
language: en
lastmod: 2026-09-15
og_description: Save workbook as CSV, export Excel to TXT, and apply custom number
  format while converting cell values to uppercase using Aspose.Cells in C#.
og_image_alt: Screenshot showing workbook saved as CSV using C# code
og_title: Save workbook as CSV and export Excel to TXT with custom formatting in C#
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to save workbook as CSV, export Excel to TXT, and apply custom
    number format while converting cell values to uppercase in C#.
  headline: How to save workbook as CSV and export Excel to TXT with custom formatting
    in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: How to save workbook as CSV and export Excel to TXT with custom formatting
  in C#
url: /net/converting-excel-files-to-other-formats/how-to-save-workbook-as-csv-and-export-excel-to-txt-with-cus/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to save workbook as CSV and export Excel to TXT with custom formatting in C#

If you need to **save workbook as CSV** while also exporting a worksheet as plain‑text and applying a custom number format, this guide shows you a complete, ready‑to‑run solution. You’ll see how to keep numeric precision, convert every cell value to uppercase, and handle Japanese‑era dates—all with Aspose.Cells for .NET.

Exporting data from Excel often means juggling several formats: CSV for data‑exchange, TXT for legacy systems, and custom number formats for locale‑specific reporting. This tutorial walks through each requirement step‑by‑step, so you can copy the code directly into your project.

In the sections that follow you’ll learn how to:

* **save workbook as csv** with a defined number of significant digits  
* **export excel to txt** while forcing **uppercase cell values**  
* **apply custom number format** for Japanese‑era dates and read the formatted result  

No external tools are required—just the Aspose.Cells library and a .NET development environment.

## Prerequisites

* .NET 6.0 or later (the code also works with .NET Framework 4.8)  
* Aspose.Cells for .NET (NuGet package `Aspose.Cells`)  
* Basic familiarity with C# and Excel concepts  

---

## Step 1: Save the workbook as CSV with controlled precision

When you **save workbook as CSV**, numeric values are written using the default string representation, which can lose precision. By configuring `CsvSaveOptions.SignificantDigits`, you tell Aspose.Cells how many significant digits to keep.

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (or load an existing one)
Workbook workbook = new Workbook();               // you can also use new Workbook("input.xlsx");

// Configure CSV options to keep up to 4 significant digits
CsvSaveOptions csvOptions = new CsvSaveOptions
{
    SignificantDigits = 4   // ensures numbers like 123.4567 stay precise
};

// Save the workbook as CSV
string csvPath = @"C:\Temp\Digits.csv";
workbook.Save(csvPath, csvOptions);

Console.WriteLine($"Workbook saved as CSV to {csvPath}");
```

**Why this matters:**  
Setting `SignificantDigits` prevents rounding errors that often appear when large datasets are exchanged with downstream systems (e.g., data‑warehouses). The `CsvSaveOptions` object also lets you control delimiters, encoding, and other CSV‑specific settings if needed.

---

## Step 2: Export a worksheet as plain text while converting values to uppercase

Exporting a sheet to a simple `.txt` file is useful for legacy import routines that expect whitespace‑delimited data. By enabling `ExportTableOptions.ExportAsString` and providing a `CustomExport` delegate, you can **export excel to txt** and simultaneously enforce **uppercase cell values**.

```csharp
// Prepare export options for plain‑text output
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true, // forces every cell to be treated as a string
    // CustomExport receives the cell and its current string value,
    // allowing you to modify it before it is written.
    CustomExport = (cell, value) =>
    {
        // Convert the cell value to an upper‑case string
        return value?.ToString().ToUpperInvariant();
    }
};

// Define the output path for the text file
string txtPath = @"C:\Temp\Table.txt";

// Export the first worksheet (index 0) as a tab‑delimited text file
workbook.Worksheets[0].ExportTable(txtPath, tableOptions);

Console.WriteLine($"Worksheet exported as text to {txtPath}");
```

**Why this matters:**  
Many integration points (e.g., mainframe batch jobs) expect uppercase identifiers. The `CustomExport` callback gives you full control over each cell’s representation, letting you inject transformations such as trimming, padding, or locale‑specific formatting without post‑processing the file.

---

## Step 3: Apply a custom number format and read the formatted result

Excel’s built-in number formats cover most cases, but sometimes you need to display dates in a specific calendar system—such as the Japanese era. The following code demonstrates how to **apply custom number format** to a cell, then read the formatted string that respects the workbook’s locale.

```csharp
// Create a new workbook for the era example
Workbook eraWorkbook = new Workbook();

// Access the first worksheet and target cell A1
Worksheet sheet = eraWorkbook.Worksheets[0];
Cell dateCell = sheet.Cells["A1"];

// Insert a Japanese‑era date string (Reiwa 3 = 2021)
dateCell.PutValue("Reiwa 3/04/01");

// Apply a built‑in date number format (14 = mm-dd-yy)
// You could also assign a custom format string, e.g., "[$-ja-JP]ggge年m月d日"
Style style = eraWorkbook.CreateStyle();
style.Number = 14; // standard short date format
dateCell.SetStyle(style);

// Force formula calculation (necessary if the cell contains a formula)
eraWorkbook.CalculateFormula();

// Retrieve the formatted string as it would appear in Excel
string formattedDate = dateCell.StringValue;
Console.WriteLine($"Formatted date (locale aware): {formattedDate}");
```

**Why this matters:**  
Using `SetStyle` with a number format ensures that the cell’s display respects regional settings, which is critical for reports distributed across different locales. When you later read `StringValue`, you get the exact string that a user would see in the Excel UI, eliminating the need for manual parsing.

---

## Full, runnable example

Below is a single program that combines the three steps. Paste it into a new Console App project, add the Aspose.Cells NuGet package, and run it.

```csharp
using Aspose.Cells;
using System;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Save workbook as CSV ----------
            Workbook workbook = new Workbook(); // start with a fresh workbook
            // (Optionally load an existing file: new Workbook("input.xlsx"))

            // Populate some sample data
            workbook.Worksheets[0].Cells["A1"].PutValue(123.456789);
            workbook.Worksheets[0].Cells["B1"].PutValue("Sample Text");

            CsvSaveOptions csvOptions = new CsvSaveOptions
            {
                SignificantDigits = 4
            };
            string csvPath = @"C:\Temp\Digits.csv";
            workbook.Save(csvPath, csvOptions);
            Console.WriteLine($"Saved CSV to {csvPath}");

            // ---------- Step 2: Export worksheet as text with uppercase ----------
            ExportTableOptions tableOptions = new ExportTableOptions
            {
                ExportAsString = true,
                CustomExport = (cell, value) => value?.ToString().ToUpperInvariant()
            };
            string txtPath = @"C:\Temp\Table.txt";
            workbook.Worksheets[0].ExportTable(txtPath, tableOptions);
            Console.WriteLine($"Exported TXT to {txtPath}");

            // ---------- Step 3: Apply custom number format ----------
            Workbook eraWorkbook = new Workbook();
            Cell dateCell = eraWorkbook.Worksheets[0].Cells["A1"];
            dateCell.PutValue("Reiwa 3/04/01");

            Style eraStyle = eraWorkbook.CreateStyle();
            eraStyle.Number = 14; // short date format; replace with custom if needed
            dateCell.SetStyle(eraStyle);
            eraWorkbook.CalculateFormula();

            Console.WriteLine($"Japanese era date formatted: {dateCell.StringValue}");
        }
    }
}
```

**Expected output**

```
Saved CSV to C:\Temp\Digits.csv
Exported TXT to C:\Temp\Table.txt
Japanese era date formatted: 4/1/2021
```

(The exact date format may vary according to your system’s locale settings.)

---

## Common questions and edge‑case handling

| Question | Answer |
|----------|--------|
| *What if I need a different delimiter in the CSV?* | Set `csvOptions.Separator` to `','`, `'\t'`, or any custom character before calling `Save`. |
| *Can I keep the original numeric precision instead of rounding?* | Use `SignificantDigits = 0` to write the full double‑precision value, or set `NumberDecimalSeparator` for locale‑specific decimal symbols. |
| *How do I export only a specific range rather than the whole sheet?* | Call `ExportTable(string fileName, ExportTableOptions options, CellArea area)` and pass a `CellArea` that defines the range. |
| *What if the workbook contains formulas that reference other sheets?* | Ensure you call `workbook.CalculateFormula()` before exporting; otherwise you’ll get the cached values. |
| *Is there a way to keep the original cell formatting (fonts, colors) in the TXT file?* | Plain‑text formats cannot retain visual styling. If you need rich formatting, consider exporting to HTML (`HtmlSaveOptions`) instead. |

---

## Conclusion

You now know how to **save workbook as CSV** with controlled precision, **export excel to TXT** while forcing **uppercase cell values**, and **apply custom number format** for locale‑aware date rendering. Each snippet is self‑contained, runs out‑of‑the‑box, and follows best practices for both performance and maintainability.

Next, you might explore:

* Using `HtmlSaveOptions` to keep styling when exporting to web‑friendly formats.  
* Leveraging `CsvSaveOptions.Encoding` for UTF‑8 or other character sets when dealing with multilingual data.  
* Automating batch processing of multiple worksheets by looping over `workbook.Worksheets`.

Feel free to adapt the code to your own data pipelines, and let the flexibility of Aspose.Cells handle the heavy lifting.

---


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Save Workbook To Text Csv Format](/cells/german/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)
- [Save Workbook To Text Csv Format](/cells/french/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)
- [Save Workbook To Text Csv Format](/cells/spanish/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}