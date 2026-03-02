---
category: general
date: 2026-03-01
description: How to create workbook in C# quickly—learn to write value to cell, set
  cell number format, and format cell number with simple steps.
draft: false
keywords:
- how to create workbook
- write value to cell
- format cell number
- set cell number format
- how to write cell
language: en
og_description: How to create workbook in C#? This guide shows you how to write value
  to cell, set cell number format, and format cell number in just a few lines of code.
og_title: How to Create Workbook in C# – Write Value & Format Number
tags:
- C#
- Aspose.Cells
- Excel Automation
title: How to Create Workbook in C# – Write Value & Format Number
url: /net/excel-workbook/how-to-create-workbook-in-c-write-value-format-number/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Create Workbook in C# – Write Value & Format Number

How to create workbook in C# is a common task when you need to generate Excel files on the fly. In this guide we’ll walk you through how to write value to cell and format cell number so the final sheet looks polished.

If you’ve ever stared at a blank spreadsheet and wondered why the numbers keep showing too many decimals, you’re not alone. We’ll cover everything from initializing the workbook object to setting a custom number format, and we’ll throw in a few tips for edge‑cases you might run into later.

## What You’ll Learn

- **Initialize** a new `Workbook` instance.  
- **Write value to cell** using the `PutValue` method.  
- **Set cell number format** with a `Style` object, achieving a clean two‑digit display.  
- Verify the result by reading the cell back or opening the file in Excel.  

No external libraries beyond the standard Aspose.Cells (or any similar API) are required, and the code runs on .NET 6+ without extra configuration.

---

## How to Create Workbook – Initialize the Object

First things first: you need a workbook object to hold your sheets. Think of the `Workbook` as the whole Excel file, while each `Worksheet` is a single tab.

```csharp
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

*Why this matters:* Creating the workbook allocates the internal structures that later hold rows, columns, and formatting. Without this object, there’s nowhere to write a value to cell.

> **Pro tip:** If you plan to work with an existing file, replace `new Workbook()` with `new Workbook("template.xlsx")` to load a template and preserve its styles.

## Write Value to Cell

Now that we have a workbook, let’s drop a number into cell **A1** of the first worksheet.

```csharp
// Step 2: Access cell A1 in the first worksheet
Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

// Step 3: Insert a numeric value into the cell
cellA1.PutValue(123.456789);
```

*Why we use `PutValue`*: This method automatically detects the data type, so you don’t have to cast or convert manually. It also respects the cell’s existing style, which is handy when you later **set cell number format**.

### Quick Check

If you read the cell back, you’ll see the raw value:

```csharp
double raw = cellA1.DoubleValue; // raw == 123.456789
```

That’s the number before any formatting is applied.

## Set Cell Number Format

Displaying a raw double with many decimals isn’t always user‑friendly. Let’s limit it to two significant digits.

```csharp
// Step 4: Apply a style that formats the number with two significant digits
cellA1.SetStyle(new Style() { Number = 2 });
```

The `Number` property corresponds to Excel’s built‑in number format IDs. `2` means “Number with two decimal places”. If you need a different format—say currency or a date—you’d use another ID or a custom format string.

### Alternative: Custom Format String

```csharp
Style customStyle = workbook.CreateStyle();
customStyle.Custom = "#,##0.00"; // forces two decimals with thousand separator
cellA1.SetStyle(customStyle);
```

*Why choose a custom style?* It gives you full control, especially when the built‑in IDs don’t cover your regional settings.

## Verify Output (Optional but Recommended)

After applying the style, you can save the workbook and open it in Excel to confirm the appearance.

```csharp
// Save the workbook to a file
workbook.Save("FormattedWorkbook.xlsx");

// Or, for quick verification in code:
string displayed = cellA1.StringValue; // "123.46"
Console.WriteLine($"Displayed value: {displayed}");
```

You should see **123.46** in cell A1—exactly two decimal places, thanks to the format we set.

---

### Full Working Example

Putting it all together, here’s a self‑contained program you can copy‑paste into a console app.

```csharp
using System;
using Aspose.Cells;   // Ensure you have the Aspose.Cells NuGet package

class Program
{
    static void Main()
    {
        // Initialize the workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet and cell A1
        Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

        // Write a numeric value
        cellA1.PutValue(123.456789);

        // Apply a two‑decimal number format
        cellA1.SetStyle(new Style() { Number = 2 });

        // Save to disk (optional)
        workbook.Save("FormattedWorkbook.xlsx");

        // Output the displayed text for verification
        Console.WriteLine($"Cell A1 shows: {cellA1.StringValue}");
    }
}
```

**Expected output when you run the program:**

```
Cell A1 shows: 123.46
```

Open `FormattedWorkbook.xlsx` in Excel and you’ll see the same formatted value.

---

## Common Variations & Edge Cases

### 1. Different Number Formats

| Goal | Format ID | Code Snippet |
|------|-----------|--------------|
| Currency (two decimals) | 5 | `cellA1.SetStyle(new Style() { Number = 5 });` |
| Percentage (no decimals) | 10 | `cellA1.SetStyle(new Style() { Number = 10 });` |
| Scientific notation | 11 | `cellA1.SetStyle(new Style() { Number = 11 });` |

If none of the built‑in IDs fit, fall back to a custom string as shown earlier.

### 2. Culture‑Specific Decimal Separators

Some locales use commas for decimals. You can enforce a culture‑aware format:

```csharp
Style cultureStyle = workbook.CreateStyle();
cultureStyle.Custom = "#,##0.00"; // works for most European locales
cellA1.SetStyle(cultureStyle);
```

### 3. Writing Text Instead of Numbers

When you need to **how to write cell** with a string, just pass a string to `PutValue`:

```csharp
cellA1.PutValue("Total Revenue");
```

No number format is required, but you can still apply font styling.

### 4. Large Datasets

If you’re populating thousands of rows, batch‑style insertion (`Cells.ImportArray`) is faster than looping `PutValue`. The formatting approach stays the same; you just apply the style to a range:

```csharp
Range range = workbook.Worksheets[0].Cells.CreateRange("B2:B1001");
range.ApplyStyle(new Style() { Number = 2 });
```

---

## Frequently Asked Questions

**Q: Does this work with .NET Core?**  
A: Absolutely. Aspose.Cells supports .NET Standard 2.0 and later, so you can target .NET 5, .NET 6, or .NET 7 without changes.

**Q: What if I need more than two decimal places?**  
A: Change the `Number` property to the appropriate built‑in ID (e.g., `3` for three decimals) or tweak the custom format string (`"#,##0.000"`).

**Q: Can I apply the format to an entire column at once?**  
A: Yes. Use `Cells["A:A"]` to get the whole column and then `SetStyle`.

---

## Conclusion

You now know **how to create workbook** objects in C#, **write value to cell**, and **set cell number format** so numbers appear exactly how you want. By mastering these basics you’ll be equipped to generate professional‑looking Excel reports, invoices, or data exports with minimal effort.

Next up, you might explore **format cell number** for dates, percentages, or conditional formatting—each builds on the same principles we covered. Dive into the Aspose.Cells documentation for deeper styling options, or try combining multiple worksheets into a single workbook for richer reports.

Happy coding, and remember: a well‑formatted spreadsheet is just

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}