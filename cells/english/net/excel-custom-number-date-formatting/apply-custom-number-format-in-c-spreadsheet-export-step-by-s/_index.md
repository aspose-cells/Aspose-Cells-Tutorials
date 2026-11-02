---
category: general
date: 2026-04-07
description: Apply custom number format to a spreadsheet cell and learn how to format
  number in spreadsheet while exporting cell value with C#. Quick, complete guide.
draft: false
keywords:
- apply custom number format
- format number in spreadsheet
- how to format numeric cell
- how to export cell value
language: en
og_description: Apply custom number format to a spreadsheet cell and export it as
  a formatted string. Learn how to format number in spreadsheet and export cell value.
og_title: Apply Custom Number Format – Complete C# Export Tutorial
tags:
- C#
- Spreadsheet
- Number Formatting
title: Apply Custom Number Format in C# Spreadsheet Export – Step‑by‑Step Guide
url: /net/excel-custom-number-date-formatting/apply-custom-number-format-in-c-spreadsheet-export-step-by-s/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Apply Custom Number Format in C# Spreadsheet Export – Complete Tutorial

Ever needed to **apply custom number format** to a cell and then pull that formatted string out of a spreadsheet? You’re not alone. Many developers hit a wall when they discover the raw value comes out instead of the pretty‑looking, locale‑aware string they expect. In this guide we’ll show you exactly how to format number in spreadsheet cells and how to export cell value as a formatted string using a popular C# spreadsheet library.

By the end of the walkthrough you’ll be able to **apply custom number format** to any numeric cell, export the result with `ExportTable`, and see the exact output you’d expect to show in a UI or a report. No external docs needed—everything’s right here.

## Prerequisites

- .NET 6.0 or later (the code works on .NET Framework 4.7+ as well)
- A reference to the spreadsheet library that provides `Workbook`, `Worksheet`, and `ExportTableOptions` (e.g., **Aspose.Cells** or **GemBox.Spreadsheet**; the API shown matches Aspose.Cells)
- Basic C# knowledge—if you can write a `Console.WriteLine`, you’re good to go

> **Pro tip:** If you’re using a different library, the property names are usually similar (`NumberFormat`, `ExportAsString`). Just map them accordingly.

## What the tutorial covers

1. Creating a workbook and selecting the first worksheet.  
2. Inserting a numeric value into a cell.  
3. Setting up `ExportTableOptions` to **apply custom number format** and return a string.  
4. Exporting the cell and printing the formatted result.  
5. Edge‑case handling – what if the cell contains a formula or a null value?

Let’s jump in.

![apply custom number format example](https://example.com/image.png "apply custom number format")

## Step 1 – Create a workbook and get the first worksheet

The first thing you need is a workbook object. Think of it as the Excel file you’d open in the Office app. Once you have it, grab the first sheet—most tutorials start there because it keeps the example concise.

```csharp
// Step 1: Initialize the workbook and fetch the first worksheet
Workbook workbook = new Workbook();                 // creates an in‑memory workbook
Worksheet worksheet = workbook.Worksheets[0];      // first sheet (index 0)
```

**Why this matters:** A fresh workbook gives you a clean slate, ensuring no hidden formatting interferes with our custom number format later on.

## Step 2 – Put a numeric value into cell B2 (the cell we will export)

Now we need something to format. Cell **B2** is a convenient spot—easy to reference and far enough from the default A1 corner to avoid accidental overwrites.

```csharp
// Step 2: Insert a raw numeric value
worksheet.Cells["B2"].Value = 1234.56;   // raw double, no formatting yet
```

**What if the value is a formula?**  
If you later replace the raw value with a formula (e.g., `=SUM(A1:A10)`), the export routine will still respect the number format we apply in the next step, because formatting is attached to the cell, not the value type.

## Step 3 – Configure export options to receive the value as a formatted string

Here’s the heart of the tutorial: we tell the library to **apply custom number format** while exporting. The `NumberFormat` string follows the same pattern you’d use in Excel’s “Custom” category.

```csharp
// Step 3: Set up options for exporting as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,                         // forces string output
    NumberFormat = "#,##0.00;(#,##0.00)"           // custom format: 1,234.56 or (1,234.56) for negatives
};
```

- `ExportAsString = true` ensures the method returns a `string` instead of a raw double.  
- `NumberFormat = "#,##0.00;(#,##0.00)"` mirrors Excel’s pattern: commas for thousands, two decimal places, and parentheses for negative numbers.

> **Why use a custom format?** It guarantees consistency across cultures (e.g., US vs. European number separators) and lets you embed business‑specific styling like accounting parentheses.

## Step 4 – Export the cell using the configured options

Now we actually pull the value out of the worksheet, letting the library do the heavy lifting of applying the format we defined.

```csharp
// Step 4: Export the formatted value from B2
string formattedResult = worksheet.Cells.ExportTable(
    worksheet.Cells["B2"],   // the source cell
    exportOptions);         // our custom options
```

**Edge case – empty cell:** If `B2` were empty, `formattedResult` would be `null`. You can guard against that with a simple null‑check before printing.

## Step 5 – Display the formatted string

Finally, we write the result to the console. In a real app you might push this string into a PDF, an email, or a UI label.

```csharp
// Step 5: Show the result
Console.WriteLine(formattedResult);   // Expected output: 1,234.56
```

**Expected output**

```
1,234.56
```

If you change the raw value to `-9876.54`, the same format would give you `(9,876.54)`—exactly what many accounting reports require.

## Full, runnable example

Below is the complete program you can copy‑paste into a new console project. It compiles and runs as‑is, assuming you’ve added the appropriate NuGet package for the spreadsheet library.

```csharp
using System;
using Aspose.Cells;   // Replace with your library’s namespace if different

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Insert numeric value into B2
        worksheet.Cells["B2"].Value = 1234.56;

        // 3️⃣ Set export options – apply custom number format
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00;(#,##0.00)"   // custom format
        };

        // 4️⃣ Export the cell as a formatted string
        string formattedResult = worksheet.Cells.ExportTable(
            worksheet.Cells["B2"], exportOptions);

        // 5️⃣ Output the result
        Console.WriteLine(formattedResult);   // → 1,234.56
    }
}
```

### Quick sanity check

- **Does it compile?** Yes—just ensure the `Aspose.Cells` (or equivalent) DLL is referenced.
- **Will it work with other cultures?** The format string is culture‑agnostic; the library respects the pattern you give it. If you need locale‑specific separators, you can prepend `CultureInfo` handling before export.

## Common questions & variations

### How to **format number in spreadsheet** using a different pattern?

Replace the `NumberFormat` string. For example, to show a percentage with one decimal place:

```csharp
NumberFormat = "0.0%";
```

### What if I need to **how to export cell value** as HTML instead of plain text?

Most libraries have an overload that accepts an export type. You’d set `ExportAsString = true` and add `ExportHtml = true` (or similar). The principle stays the same: define the format, then choose the output representation.

### Can I apply the format to a whole range, not just one cell?

Absolutely. You can assign `NumberFormat` to a `Style` object and then apply that style to a `Range`. The export call remains unchanged; it will pick up the style automatically.

```csharp
Style style = workbook.CreateStyle();
style.Custom = "#,##0.00;(#,##0.00)";
Range range = worksheet.Cells.CreateRange("A1:C10");
range.ApplyStyle(style, new StyleFlag { NumberFormat = true });
```

### What happens when the cell contains a formula?

The export routine evaluates the formula first, then formats the resulting numeric value. No extra code is needed—just be sure `Calculate` has been called if you disabled automatic calculation.

```csharp
worksheet.Cells["B2"].Formula = "=SUM(A1:A5)";
worksheet.Calculate();   // forces evaluation
```

## Conclusion

You now know how to **apply custom number format** to a spreadsheet cell, **format number in spreadsheet** contexts, and **how to export cell value** as a ready‑to‑display string. The concise code sample above covers every step—from workbook creation to final output—so you can drop it straight into a production project.

Ready for the next challenge? Try combining this technique with **how to format numeric cell** for dates, currency symbols, or conditional formatting. Or explore exporting multiple cells as a CSV while preserving each cell’s custom format. The sky’s the limit, and with these fundamentals you’ve got a solid foundation.

Happy coding, and don’t forget to experiment—sometimes the best answers surface when you tweak the format string just a little bit!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}