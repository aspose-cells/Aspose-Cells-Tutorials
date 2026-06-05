---
category: general
date: 2026-06-05
description: Create Excel workbook in C# quickly and learn how to set cell number
  format, export Excel cell, and convert cell value to string with two‑decimal precision.
draft: false
keywords:
- create excel workbook
- set cell number format
- format number with two decimals
- how to export excel cell
- convert cell value to string
language: en
og_description: Create Excel workbook in C# and master setting cell number format,
  exporting Excel cell as a string, and formatting numbers with two decimals.
og_title: Create Excel Workbook in C# – Full Step‑by‑Step Guide
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  headline: Create Excel Workbook in C# – Complete Programming Guide
  type: TechArticle
- description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  name: Create Excel Workbook in C# – Complete Programming Guide
  steps:
  - name: What if the cell already has a style?
    text: The `GetStyle` method returns a copy of the existing style, so any previous
      formatting (font, color, etc.) is retained. You only overwrite the `Custom`
      property, leaving everything else untouched.
  - name: How does culture affect the decimal separator?
    text: 'Aspose.Cells respects the thread’s `CultureInfo`. If you need a comma instead
      of a dot, set:'
  - name: Can I export a range of cells at once?
    text: Yes—use `Worksheet.ExportDataTable` or `Worksheet.ExportString` with a range
      address. The `ExportTableOptions` you defined for a single cell can be reused
      for the whole range.
  - name: What if I don’t want the value rounded but truncated?
    text: 'Change the custom format to `"0.00"` with a rounding mode, or manually
      truncate before putting the value:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: Create Excel Workbook in C# – Complete Programming Guide
url: /net/excel-workbook/create-excel-workbook-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel Workbook in C# – Complete Programming Guide

Ever wondered how to **create Excel workbook** in C# without wrestling with COM interop or messy CSV tricks? You're not alone. Many developers need a clean, .NET‑native way to spin up an .xlsx file, slap a number into a cell, and then export that value as a nicely formatted string.  

In this tutorial we’ll walk through exactly that—starting from an empty workbook, setting the cell number format, formatting the number with two decimals, and finally learning **how to export Excel cell** data as a string. By the end you’ll also see how to **convert cell value to string** without losing precision.

> **Pro tip:** The approach below uses the **Aspose.Cells for .NET** library, which is a battle‑tested, commercial‑grade API. If you’re after a free alternative, EPPlus or ClosedXML work similarly, but the code snippets will differ slightly.

## Prerequisites

Before we dive in, make sure you have:

- .NET 6.0 SDK (or any recent .NET version) installed.
- Visual Studio 2022 or VS Code with the C# extension.
- The **Aspose.Cells** NuGet package (`Install-Package Aspose.Cells`).

No other dependencies are required—everything else lives inside the library.

## Step 1: Install Aspose.Cells and Set Up the Project

Open your terminal (or Package Manager Console) and run:

```powershell
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

This creates a fresh console app named `ExcelDemo` and pulls in the `Aspose.Cells` assembly.  

Why this step matters: without the library, you can’t **create Excel workbook** objects or manipulate cells in a type‑safe way.

## Step 2: Create the Workbook and Grab the First Worksheet

Now open `Program.cs` and replace the default code with the snippet below. It shows the very first thing you do when you **create Excel workbook**—instantiate the `Workbook` class and get a reference to the default sheet.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates a new .xlsx in memory
        Worksheet ws = workbook.Worksheets[0];           // first (default) sheet

        // The rest of the steps will follow here...
```

> **Why?** The `Workbook` object is the in‑memory representation of an Excel file. By default it contains one worksheet, which we access via the zero‑based index.

## Step 3: Put a Numeric Value into a Specific Cell

Let’s target row 5, column 2 (zero‑based indices) and insert a decimal number. This demonstrates **format number with two decimals** later on.

```csharp
        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];          // corresponds to cell C6 in Excel UI
        cell.PutValue(12345.6789);          // raw value with many decimal places
```

The `PutValue` method stores the raw double. At this point, Excel would display the full precision unless we apply a format.

## Step 4: Set Cell Number Format (Two Decimal Places)

Here’s where we **set cell number format**. We’ll use the `Style` object to define a custom number format `"0.00"`—exactly two decimals.

```csharp
        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();               // clone existing style
        style.Custom = "0.00";                       // forces two digits after the dot
        cell.SetStyle(style);                        // apply the style back to the cell
```

Why use a style instead of string conversion? Keeping the cell as a numeric type preserves its calculable nature (you can still sum, average, etc.) while displaying exactly what you need.

## Step 5: Export the Cell Value as a Formatted String

Sometimes you need the **how to export excel cell** value as plain text—perhaps to write it into a log file or send it over a web API. Aspose.Cells lets you attach export options to a cell, telling the library to render the value as a string using the same number format.

```csharp
        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // forces string output
            NumberFormat = "0.00"           // matches the style we set earlier
        };
        cell.ExportOptions = exportOptions; // attach options to the cell
```

Now when we read the cell’s value through the export API, we’ll receive a string that already respects the two‑decimal rule.

## Step 6: Retrieve the Formatted String (Convert Cell Value to String)

Let’s actually perform the export and see the result. The `ExportString` method returns the cell’s content as a string, applying any `ExportTableOptions` we attached.

```csharp
        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");
```

When you run the program, the console prints:

```
Formatted cell value: 12345.68
```

Notice the rounding from `12345.6789` to `12345.68`—that’s the effect of **format number with two decimals**.

## Step 7: (Optional) Save the Workbook to Disk

If you also want to see the result inside an actual `.xlsx` file, just call `Save`:

```csharp
        // Optional: write the workbook to a file so you can open it in Excel
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

Opening `DemoWorkbook.xlsx` shows the same number in cell **C6**, formatted with two decimal places.

## Edge Cases & Common Questions

### What if the cell already has a style?

The `GetStyle` method returns a copy of the existing style, so any previous formatting (font, color, etc.) is retained. You only overwrite the `Custom` property, leaving everything else untouched.

### How does culture affect the decimal separator?

Aspose.Cells respects the thread’s `CultureInfo`. If you need a comma instead of a dot, set:

```csharp
System.Threading.Thread.CurrentThread.CurrentCulture = new System.Globalization.CultureInfo("fr-FR");
```

The same `"0.00"` format will now render `12 345,68`.

### Can I export a range of cells at once?

Yes—use `Worksheet.ExportDataTable` or `Worksheet.ExportString` with a range address. The `ExportTableOptions` you defined for a single cell can be reused for the whole range.

### What if I don’t want the value rounded but truncated?

Change the custom format to `"0.00"` with a rounding mode, or manually truncate before putting the value:

```csharp
double raw = Math.Truncate(12345.6789 * 100) / 100; // yields 12345.67
cell.PutValue(raw);
```

## Full Working Example (Copy‑Paste Ready)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];
        cell.PutValue(12345.6789);

        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();
        style.Custom = "0.00";
        cell.SetStyle(style);

        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "0.00"
        };
        cell.ExportOptions = exportOptions;

        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");

        // Optional: save the workbook for visual verification
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

**Expected console output**

```
Formatted cell value: 12345.68
```

Open `DemoWorkbook.xlsx` → go to cell **C6** → you’ll see the same number with two decimal places.

## Conclusion

We’ve just covered everything you need to **create Excel workbook** in C#, **set cell number format**, **format number with two decimals**, understand **how to export Excel cell** data, and **convert cell value to string** for downstream processing.  

The key takeaways are:

1. Use `Workbook` and `Worksheet` to spin up an Excel file in memory.  
2. Apply a custom style (`"0.00"`) to enforce two‑decimal display.  
3. Attach `ExportTableOptions` to a cell when you need a string representation that respects the same format.  

From here you can experiment—add more cells, apply conditional formatting, or even generate charts. If you’re curious about styling fonts or adding formulas, check out the Aspose.Cells documentation on **cell styling** and **formula evaluation**.

Got more questions about Excel automation in C#? Drop a comment, and happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Master Workbook Operations in Aspose.Cells .NET&#58; Load Excel Files and Trace Cell Precedents Effectively](/cells/english/net/workbook-operations/aspose-cells-net-master-workbook-operations/)
- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Master Aspose.Cells for .NET&#58; Advanced Excel Workbook and Cell Management](/cells/english/net/advanced-features/excel-aspose-cells-net-create-manage/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}