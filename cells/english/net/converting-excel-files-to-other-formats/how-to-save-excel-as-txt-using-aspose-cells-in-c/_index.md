---
category: general
date: 2026-10-13
description: Learn how to save Excel as TXT with Aspose.Cells. This guide covers export
  Excel to TXT, write value to cell, and set significant digits in just a few steps.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as txt
- export excel to txt
- write value to cell
- set significant digits
- export spreadsheet as txt
language: en
lastmod: 2026-10-13
og_description: Save Excel as TXT with Aspose.Cells. Learn how to export Excel to
  TXT, write value to cell, and set significant digits in just a few lines of C# code.
og_image_alt: Screenshot showing a workbook saved as a TXT file using save excel as
  txt
og_title: Save Excel as TXT – step‑by‑step guide for .NET developers
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to save Excel as TXT with Aspose.Cells. This guide covers
    export Excel to TXT, write value to cell, and set significant digits in just a
    few steps.
  headline: How to save Excel as TXT using Aspose.Cells in C#
  type: TechArticle
- questions:
  - answer: It rounds to the nearest value based on the specified number of significant
      digits, ensuring the output is mathematically accurate to that precision.
    question: Does `SignificantDigits` round or truncate?
  - answer: 'Yes. Replace the file path with a `MemoryStream` instance: `workbook.Save(stream,
      txtOptions);`. This is handy for web APIs that need to return the TXT content
      without touching the file system.'
    question: Can I export directly to a memory stream?
  - answer: 'Use `txtOptions.ExportFormattedValues = true`. This forces Aspose.Cells
      to write the cell’s displayed text rather than the raw value. ## Conclusion
      You now know how to **save Excel as TXT** with full control over precision,
      formatting, and output location. By following the four steps—create a workbo'
    question: What if I need to keep the original formatting (e.g., dates)?
  type: FAQPage
tags:
- Excel
- TXT
- Aspose.Cells
- .NET
title: How to save Excel as TXT using Aspose.Cells in C#
url: /net/converting-excel-files-to-other-formats/how-to-save-excel-as-txt-using-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to save Excel as TXT using Aspose.Cells in C#

If you need to **save Excel as TXT** quickly, this tutorial shows the complete process in under five minutes. You’ll see how to export Excel to TXT, write value to cell, and set significant digits so the text file contains exactly the data you expect.

Exporting a spreadsheet as TXT is useful when downstream systems only accept plain‑text input, when you need to generate logs, or when you want a human‑readable dump of calculations. The example below works with Aspose.Cells v25.10 or later and runs on any .NET 6+ runtime.

## Prerequisites

Before you start, make sure you have:

* A licensed copy of **Aspose.Cells for .NET** (the free trial works for testing).
* .NET 6 SDK or later installed.
* An IDE such as Visual Studio 2022, VS Code, or Rider.
* Basic C# knowledge—no advanced Excel automation experience required.

You can install the Aspose.Cells NuGet package with:

```bash
dotnet add package Aspose.Cells
```

## Step 1: Create a workbook and access its first worksheet (save excel as txt)

The first thing you do when you want to **save Excel as TXT** is to create a `Workbook` object. This object represents the entire Excel file in memory.

```csharp
using Aspose.Cells;

// Create a new workbook (an empty Excel file)
Workbook workbook = new Workbook();

// Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

> **Why this matters:** The `Workbook` class is the entry point for all spreadsheet operations. By starting with a fresh workbook you avoid any hidden formatting that could affect the plain‑text output.

## Step 2: Write a high‑precision number into a cell (write value to cell)

Now you need to **write value to cell** A1. The `PutValue` method automatically detects the data type and stores it as a numeric value.

```csharp
// Write a high‑precision number into cell A1
worksheet.Cells["A1"].PutValue(12345.6789012345);
```

> **Tip:** If you later need to write strings, dates, or formulas, the same `PutValue` method works—just pass the appropriate .NET type.

## Step 3: Configure the export options to keep only the needed precision (set significant digits)

When exporting to a TXT file, you often want to limit the number of digits to keep the file size small or to match a downstream specification. The `TxtSaveOptions` class provides a `SignificantDigits` property for this purpose.

```csharp
// Configure TXT save options to retain only 6 significant digits
TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
{
    SignificantDigits = 6   // New option in v25.10
};
```

> **Why you should set significant digits:** Without this setting, Aspose.Cells writes the full double‑precision value, which can produce long strings like `12345.6789012345`. Setting `SignificantDigits = 6` trims the output to `12345.7`, matching most reporting requirements.

## Step 4: Export the workbook as a TXT file (export excel to txt)

Finally, you **export Excel to TXT** by calling `Workbook.Save` with the previously configured options.

```csharp
// Save the workbook as a TXT file using the configured options
string outputPath = @"C:\Temp\LimitedDigits.txt";
workbook.Save(outputPath, txtSaveOptions);
```

When the code finishes, `LimitedDigits.txt` contains:

```
12345.7
```

> **Result verification:** Open the file in any text editor (Notepad, VS Code) to confirm that only six significant digits are present and that no extra commas or tab delimiters appear.

## Full, runnable example

Below is a self‑contained console application that you can copy, paste, and run immediately.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Write a high‑precision number to cell A1
            worksheet.Cells["A1"].PutValue(12345.6789012345);

            // 3️⃣ Set up TXT save options with 6 significant digits
            TxtSaveOptions txtOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                SignificantDigits = 6
            };

            // 4️⃣ Save as TXT
            string path = @"C:\Temp\LimitedDigits.txt";
            workbook.Save(path, txtOptions);

            Console.WriteLine($"Workbook exported to TXT at: {path}");
        }
    }
}
```

**Explanation of each block**

| Block | Purpose |
|-------|---------|
| `using Aspose.Cells;` | Imports the Aspose.Cells namespace required for `Workbook`, `Worksheet`, and `TxtSaveOptions`. |
| `Workbook workbook = new Workbook();` | Instantiates an empty Excel workbook in memory. |
| `worksheet.Cells["A1"].PutValue(...);` | **write value to cell** A1 with a double‑precision number. |
| `TxtSaveOptions` | Configures **set significant digits** behavior for the TXT export. |
| `workbook.Save(..., txtOptions);` | Executes the **export excel to txt** operation, creating the plain‑text file. |

## Edge cases and additional tips

| Scenario | How to handle |
|----------|---------------|
| **Large worksheets** (many rows/columns) | Use `txtOptions.Encoding = Encoding.UTF8` if you need Unicode support, and consider streaming the file with `Workbook.Save(Stream, txtOptions)` to avoid high memory usage. |
| **Custom delimiters** (comma‑separated values) | `TxtSaveOptions` also exposes `Separator`—set it to `','` to produce CSV‑style output while still using the TXT format. |
| **Preserving formulas** | Set `txtOptions.ExportFormulas = true` to write the formula text instead of the calculated value. |
| **Locale‑specific decimal separators** | Adjust `txtOptions.DecimalSeparator` to `','` for European locales. |
| **Multiple worksheets** | Loop through `workbook.Worksheets` and call `Save` for each, appending a worksheet name to the file name. |

## Frequently asked questions

**Q: Does `SignificantDigits` round or truncate?**  
A: It rounds to the nearest value based on the specified number of significant digits, ensuring the output is mathematically accurate to that precision.

**Q: Can I export directly to a memory stream?**  
A: Yes. Replace the file path with a `MemoryStream` instance: `workbook.Save(stream, txtOptions);`. This is handy for web APIs that need to return the TXT content without touching the file system.

**Q: What if I need to keep the original formatting (e.g., dates)?**  
A: Use `txtOptions.ExportFormattedValues = true`. This forces Aspose.Cells to write the cell’s displayed text rather than the raw value.

## Conclusion

You now know how to **save Excel as TXT** with full control over precision, formatting, and output location. By following the four steps—create a workbook, **write value to cell**, **set significant digits**, and **export Excel to TXT**—you can integrate plain‑text export into any .NET application.

Next, explore related topics such as **export spreadsheet as TXT with custom delimiters**, **convert Excel to CSV**, or **use Aspose.Cells to generate JSON reports**. Each of those builds on the same core concepts demonstrated here, giving you a versatile toolkit for data interchange across platforms.

Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Save Excel as Text – Complete C# Guide to Export Excel to TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Create New Workbook and Export Excel to TXT with Precision](/cells/english/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/)
- [Create new workbook – Export Excel to TXT with Full Precision](/cells/english/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}