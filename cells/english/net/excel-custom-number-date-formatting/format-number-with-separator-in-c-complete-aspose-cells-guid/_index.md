---
category: general
date: 2026-03-30
description: Learn how to format number with separator using Aspose.Cells in C#. Includes
  set custom number format, add thousands separator, format decimal places, and how
  to format cell.
draft: false
keywords:
- format number with separator
- set custom number format
- add thousands separator
- format decimal places
- how to format cell
language: en
og_description: Format number with separator in C#. This guide shows how to set custom
  number format, add thousands separator, format decimal places, and how to format
  cell using Aspose.Cells.
og_title: Format Number with Separator in C# – Aspose.Cells Tutorial
tags:
- C#
- Aspose.Cells
- Number Formatting
title: Format Number with Separator in C# – Complete Aspose.Cells Guide
url: /net/excel-custom-number-date-formatting/format-number-with-separator-in-c-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Format Number with Separator in C# – Complete Aspose.Cells Guide

Ever needed to **format number with separator** in a spreadsheet but weren’t sure which API call to use? You're not the only one—developers constantly wrestle with thousands separators, decimal places, and custom patterns when exporting data.  

Good news: Aspose.Cells makes it a piece of cake. In this tutorial we’ll walk through a real‑world example that **sets a custom number format**, **adds a thousands separator**, **formats decimal places**, and shows **how to format cell** output as a string. By the end you’ll have a ready‑to‑run snippet you can drop into any .NET project.

## What This Guide Covers

* The exact NuGet package you need and how to install it.  
* Step‑by‑step code that creates a workbook, writes a numeric value, and applies a custom format.  
* Why `ExportTableOptions.ExportAsString` is the preferred way to retrieve a formatted value.  
* Common pitfalls—like forgetting to enable `ExportAsString` or using the wrong format mask.  
* How to tweak the format mask if you need a different number of decimal places or a different separator style.

No external documentation links are required; everything you need is right here. Let’s dive in.

---

## Prerequisites

| Requirement | Reason |
|-------------|--------|
| .NET 6.0 or later | Aspose.Cells 23.10+ targets .NET Standard 2.0+, so .NET 6 is safe and current. |
| Visual Studio 2022 (or any C# IDE) | Makes debugging and package management painless. |
| Aspose.Cells for .NET NuGet package | Provides the `Workbook`, `Worksheet`, and `ExportTableOptions` classes we’ll use. |

You can install the package via the Package Manager Console:

```powershell
Install-Package Aspose.Cells
```

That’s it—no extra DLLs, no COM interop, just a single NuGet reference.

---

## Step 1: Initialise a New Workbook (How to Format Cell)

The first thing we do is create a fresh `Workbook` instance. Think of it as an empty Excel file ready to receive data.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is where we’ll format the cell.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Why this matters:** `Workbook` is the entry point for every operation in Aspose.Cells. By grabbing the first worksheet (`Worksheets[0]`) we get a clean canvas without having to name a sheet.

---

## Step 2: Write a Numeric Value into the Target Cell

Next, we put a raw number into cell **A1**. The value itself isn’t formatted yet—it’s just a double.

```csharp
        // Step 2: Insert a raw numeric value.
        worksheet.Cells["A1"].PutValue(12345.6789);
```

> **Pro tip:** Use `PutValue` instead of `PutString` when you intend to apply numeric formatting later. This preserves the underlying data type, allowing Excel‑compatible calculations.

---

## Step 3: Set Custom Number Format (Add Thousands Separator & Format Decimal Places)

Now comes the heart of the tutorial: defining a format mask that tells Aspose.Cells how to display the number. The mask `#,##0.00` does three things:

1. **`#,##0`** – adds a thousands separator (comma by default).  
2. **`.00`** – forces exactly two decimal places.  

If you need a different number of decimals, just change the number of `0`s after the decimal point.

```csharp
        // Step 3: Configure the custom number format.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // Return the value as a formatted string.
            NumberFormat = "#,##0.00"       // Add thousands separator and fix to 2 decimals.
        };
```

> **Why we use `ExportAsString`**: By default, `ExportString` returns the raw value. Setting `ExportAsString = true` forces the API to apply the `NumberFormat` mask before converting to text. This is essential when you need the exact string representation for reports, JSON payloads, or UI display.

---

## Step 4: Export the Formatted Text (How to Format Cell)

With the options ready, we call `ExportString` on the same cell. The method respects the mask we just defined and hands back a nicely formatted string.

```csharp
        // Step 4: Export the formatted value.
        string formattedCellText = worksheet.Cells["A1"].ExportString(exportOptions);

        // Step 5: Show the result.
        Console.WriteLine(formattedCellText); // Expected output: 12,345.68
    }
}
```

Running the program prints **`12,345.68`** to the console—exactly the format we asked for.

> **Edge case:** If the source number has more than two decimal places, the mask rounds it. If you need truncation instead of rounding, you’ll have to pre‑process the value with `Math.Truncate` before calling `PutValue`.

---

## Step 5: Tweaking the Format – Common Variations

### 5.1 Change Decimal Precision

Want three decimal places? Just replace the mask:

```csharp
NumberFormat = "#,##0.000"   // → 12,345.679
```

### 5.2 Use a Different Thousands Separator

Some locales prefer a space or a period. You can embed the character directly:

```csharp
NumberFormat = "# ##0.00"    // Uses a non‑breaking space as separator.
```

Or rely on the workbook’s culture settings:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("de-DE");
NumberFormat = "#.##0,00";   // German style: 12.345,68
```

### 5.3 Prefix or Suffix (Currency, Percent)

Add a dollar sign or a percent sign right in the mask:

```csharp
NumberFormat = "$#,##0.00";   // → $12,345.68
NumberFormat = "0.00%";       // → 1,234,568.00%
```

> **Note:** The mask is case‑sensitive. `$` and `%` are literal symbols; they don’t affect the underlying numeric value.

---

## Step 6: Full Working Example (Copy‑Paste Ready)

Below is the complete program you can copy into a new console app. It includes all the steps, comments, and the final output verification.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise workbook and worksheet.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write raw numeric value to A1.
        worksheet.Cells["A1"].PutValue(12345.6789);

        // 3️⃣ Define custom format: thousands separator + two decimals.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00"
        };

        // 4️⃣ Export the formatted string.
        string result = worksheet.Cells["A1"].ExportString(exportOptions);

        // 5️⃣ Display the outcome.
        Console.WriteLine(result); // Output: 12,345.68

        // Optional: keep console open.
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

Run the program (`dotnet run` from the terminal or press F5 in Visual Studio) and you’ll see the formatted number printed exactly as shown.

---

## Frequently Asked Questions (FAQ)

**Q: Does this work with older versions of Excel?**  
A: Yes. The format mask follows Excel’s native number‑format syntax, so any version that understands `#,##0.00` will render the same string.

**Q: What if I need to format a range of cells?**  
A: Loop over the desired range and apply the same `ExportTableOptions` to each cell, or set the `Style.Custom` property on the range and then call `ExportString` on a single cell.

**Q: Can I export directly to CSV with these formats applied?**  
A: Absolutely. Use `Workbook.Save("output.csv", SaveFormat.CSV);` after setting the format on each cell. Aspose.Cells respects the cell’s `Style` when generating CSV.

---

## Conclusion

We’ve just shown how to **format number with separator** in C# using Aspose.Cells, covering everything from **set custom number format** to **add thousands separator**, **format decimal places**, and the essential **how to format cell** for string export. The code is fully self‑contained, works with .NET 6+, and can be adapted for any locale or precision requirement.

Next, you might explore:

* Applying the same technique to dates and times (`NumberFormat = "dd‑MMM‑yyyy"`).  
* Automating bulk exports where each column needs a different mask.  
* Integrating the formatted strings into PDF reports with Aspose.Words.

Give those a try, and you’ll quickly become the go‑to person for spreadsheet formatting in your team. Happy coding!   (Image: ![Screenshot showing formatted number with separator in Aspose.Cells](image-placeholder.png){alt="Formatted number with separator displayed in Aspose.Cells output"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}