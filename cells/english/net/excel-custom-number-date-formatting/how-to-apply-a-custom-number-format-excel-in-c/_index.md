---
category: general
date: 2026-10-26
description: Learn how to set a custom number format excel file in C# by configuring
  significant digits, creating an Excel workbook, and saving it as an XLSX document.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format excel
- set significant digits
- how to set number format
- create excel workbook c#
- save workbook xlsx
language: en
lastmod: 2026-10-26
og_description: Custom number format excel in C# lets you control significant digits,
  create an Excel workbook, and save it as XLSX. Follow this complete tutorial.
og_image_alt: Excel cell A1 displaying a number formatted with 4 significant digits
  using C#
og_title: Custom number format excel in C# – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to set a custom number format excel file in C# by configuring
    significant digits, creating an Excel workbook, and saving it as an XLSX document.
  headline: How to apply a custom number format excel in C#
  type: TechArticle
- description: Learn how to set a custom number format excel file in C# by configuring
    significant digits, creating an Excel workbook, and saving it as an XLSX document.
  name: How to apply a custom number format excel in C#
  steps:
  - name: Using a custom format string instead of global options
    text: 'If you need a format that applies only to a single range, you can assign
      a format string directly:'
  - name: Applying the setting to an entire column
    text: '```csharp // Apply the same significant‑digit rule to column B ws.Cells.Columns[1].ApplyNumberFormatOptions(
      new NumberFormatOptions { SignificantDigits = 4 }); ```'
  - name: Dealing with negative numbers
    text: 'The global `SignificantDigits` option works uniformly for positive and
      negative numbers. If you want a different display for negatives, combine it
      with a custom format:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: How to apply a custom number format excel in C#
url: /net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to apply a custom number format excel in C#

If you need a **custom number format excel** that shows a specific number of significant digits, this guide shows you exactly how to do it in C#. You’ll see how to set significant digits, create an Excel workbook, and save the workbook as an XLSX file—all with a few lines of code.

Working with Excel files programmatically often means you have to control how numbers appear. Using Aspose.Cells for .NET you can define a global number‑format option that forces every numeric cell to respect a given count of significant digits. This tutorial covers the complete workflow, from project setup to verifying the output in Excel.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 or later installed (the code also works with .NET Framework 4.7.2+)
* Visual Studio 2022 or any C# IDE you prefer
* The **Aspose.Cells** NuGet package (`Install-Package Aspose.Cells`) – a fully managed library for Excel manipulation
* Basic familiarity with C# syntax

## Step 1: Create an Excel workbook in C#

The first operation is to instantiate a new `Workbook` object. This object represents the whole Excel file in memory.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook wb = new Workbook();

        // The workbook now contains a default worksheet named "Sheet1"
        // You can access it via the Worksheets collection.
        Worksheet ws = wb.Worksheets[0];
```

**Why this matters:** `Workbook` is the entry point for every Excel operation. By creating it first, you ensure a clean file that you can later save as XLSX.

## Step 2: Configure the number format to set significant digits

Aspose.Cells provides a global setting called `NumberFormatOptions`. By assigning `SignificantDigits = 4`, every numeric cell will display up to four significant digits unless a more specific format overrides it.

```csharp
        // Step 2: Set the global number‑format option to 4 significant digits
        WorkbookSettings.SetNumberFormatOptions(
            new NumberFormatOptions { SignificantDigits = 4 });
```

**Why this matters:** Using `SetNumberFormatOptions` lets you define a **custom number format excel** without writing a format string for each cell. It mirrors the “Significant Digits” option you would find under Excel’s *Format Cells → Number → Custom* dialog.

## Step 3: Write values and verify the custom number format

Now place a numeric value into a cell. The global setting will automatically apply the 4‑digit rule.

```csharp
        // Step 3: Write a numeric value into cell A1 (row 0, column 0)
        ws.Cells[0, 0].PutValue(123.456789);

        // Optional: Add a label so you can see the effect in Excel
        ws.Cells[0, 1].PutValue("Original value:");
        ws.Cells[0, 2].PutValue(123.456789);
```

When you open the saved file, cell **A1** will display `123.5` (rounded to four significant digits). The original value remains unchanged in the underlying data, which you can confirm by looking at the formula bar.

**Edge case tip:** If you store a very large number like `12345678.9`, the same setting will display `1.235E+07` (scientific notation) because Excel chooses the most compact representation while preserving four significant digits.

## Step 4: Save the workbook as XLSX

Finally, persist the workbook to disk. The `Save` method automatically chooses the file format based on the extension.

```csharp
        // Step 4: Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\SigDigits.xlsx";
        wb.Save(outputPath);

        // Inform the user
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Why this matters:** Saving as **XLSX** (`save workbook xlsx`) ensures maximum compatibility with modern versions of Excel, Office 365, and other spreadsheet tools.

## Expected result

Open *C:\Temp\SigDigits.xlsx* in Microsoft Excel. You should see:

| A          | B               | C               |
|------------|-----------------|-----------------|
| **123.5**  | Original value: | **123.456789**  |

*Cell A1* shows the number rounded to four significant digits, while *C1* retains the full precision for comparison.

## Common variations and how to set number format for specific cells

### Using a custom format string instead of global options

If you need a format that applies only to a single range, you can assign a format string directly:

```csharp
ws.Cells["D1"].PutValue(0.0012345);
Style style = wb.CreateStyle();
style.Custom = "0.####"; // shows up to 4 decimal places, not significant digits
ws.Cells["D1"].SetStyle(style);
```

### Applying the setting to an entire column

```csharp
// Apply the same significant‑digit rule to column B
ws.Cells.Columns[1].ApplyNumberFormatOptions(
    new NumberFormatOptions { SignificantDigits = 4 });
```

### Dealing with negative numbers

The global `SignificantDigits` option works uniformly for positive and negative numbers. If you want a different display for negatives, combine it with a custom format:

```csharp
Style negStyle = wb.CreateStyle();
negStyle.Custom = "#,##0.###;[Red]-#,##0.###";
ws.Cells["E1"].PutValue(-9876.54321);
ws.Cells["E1"].SetStyle(negStyle);
```

## Pro tips and pitfalls

* **Pro tip:** Set the number‑format options **before** writing any data. Changing the option after populating cells does not retroactively reformat existing values.
* **Watch out for:** Using `PutValue` with a **string** that looks like a number (e.g., `"123.45"`). Excel will treat it as text, and the custom format will not apply.
* **Performance note:** Global settings are cheap, but applying a style to millions of cells can increase memory usage. Use column‑level formatting when possible.

## Next steps

Now that you can **custom number format excel** files with significant digits, you might explore:

* **How to set number format** for dates and currencies using `Style.Custom`.
* **Creating charts** that respect your custom formats.
* **Exporting to CSV** while preserving numeric precision (`save workbook xlsx` → `wb.Save("file.csv", SaveFormat.Csv)`).

These topics build on the same `Workbook` and `Worksheet` concepts demonstrated here.

---

**Summary**

You learned how to **custom number format excel** by configuring `NumberFormatOptions` to **set significant digits**, creating an Excel workbook in C#, writing values, and **saving the workbook as an XLSX** file. The complete, runnable code above shows every step, explains why each part is necessary, and provides tips for common variations. Feel free to adapt the snippets to your own projects and experiment with other formatting scenarios.


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Custom Number Format Excel in C# – Complete Guide](/cells/english/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/)
- [Create Excel Workbook C# – Limit Significant Digits Excel](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-c-limit-significant-digits-excel/)
- [How to apply number format excel with Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}