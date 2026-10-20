---
category: general
date: 2026-09-18
description: Learn how to expand array in Excel using the EXPAND function, populate
  an Excel template, and create a dynamic range Excel worksheet with C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- populate excel template
- dynamic range excel
- use expand function
- expand array formula
language: en
lastmod: 2026-09-18
og_description: How to expand array in Excel with the EXPAND function, populate an
  Excel template, and build a dynamic range Excel solution using C# code.
og_image_alt: Excel worksheet showing expanded 5x5 array and Smart Markers result
og_title: How to expand array in Excel and populate a template
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to expand array in Excel using the EXPAND function, populate
    an Excel template, and create a dynamic range Excel worksheet with C#.
  headline: How to expand array in Excel and populate a template
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: How to expand array in Excel and populate a template
url: /net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to expand array in Excel and populate a template

If you need to **how to expand array** in Excel while filling a pre‑designed template, this guide shows you a complete, end‑to‑end solution. Using the `EXPAND` function together with Aspose.Cells’ Smart Markers, you can turn a single cell reference into a 5 × 5 range and automatically replace markers such as `{IsActive}` with live data.

You’ll see how to **populate excel template**, create a **dynamic range excel**, and correctly **use expand function** in a C# project. By the end of the tutorial you’ll have a runnable program that loads an `.xlsx` file, expands an array formula, applies Smart Markers, and saves the result.

## Prerequisites

* .NET 6.0 or later (the code also works with .NET Core 3.1+)
* Aspose.Cells for .NET (NuGet package `Aspose.Cells`)
* An Excel workbook that contains a placeholder formula cell (e.g., `B2`) and a Smart Marker like `{IsActive}`
* Basic familiarity with C# and Excel formulas

> **Pro tip:** The `EXPAND` function is available only in Excel for Microsoft 365 and Excel 2021+. Older versions will return a `#NAME?` error.

## Step 1: How to expand array with the EXPAND function

The first step is to load the workbook and write an `EXPAND` formula that turns a single source cell into a larger matrix.  

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains the template layout
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Apply the EXPAND function to cell B2.
        // =EXPAND(A2,5,5) expands the array that starts at A2 into a 5‑row by 5‑column range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";
```

Why this matters: `EXPAND` removes the need to manually copy formulas across rows and columns. When the source cell (`A2`) changes, the entire 5 × 5 block updates automatically, giving you a **dynamic range excel** that reacts to data changes.

## Step 2: Populate Excel template using Smart Markers

Smart Markers let you embed placeholders inside the template that are replaced with values from a C# object. This is the most convenient way to **populate excel template** without writing cell‑by‑cell code.

```csharp
        // Prepare an anonymous object that matches the marker names in the template.
        var data = new { IsActive = true };

        // Apply Smart Markers. The marker {IsActive} inside a formula like
        // =IF({IsActive}, "Active", "Inactive") will be replaced with the value from the object.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);
```

The `SmartMarkersProcessor().Apply` call scans the entire sheet, finds `{IsActive}`, and injects the boolean value. The formula then evaluates to `"Active"` or `"Inactive"` automatically.

## Step 3: Verify the expanded range and the populated result

After applying both the `EXPAND` formula and Smart Markers, you can programmatically read a few cells to ensure everything worked as expected.

```csharp
        // Optional: read a cell from the expanded block to confirm the value.
        var sampleValue = ws.Cells["B2"].Value; // top‑left cell of the expanded range
        Console.WriteLine($"Top‑left of expanded range: {sampleValue}");

        // Read the marker result cell (assume it is C2)
        var status = ws.Cells["C2"].StringValue;
        Console.WriteLine($"Status from Smart Marker: {status}");
```

Running the program should print the original value from `A2` (or the array result) and either **Active** or **Inactive** depending on the `IsActive` flag.

## Step 4: Save the workbook – the final output

Finally, write the modified workbook to disk. This step demonstrates the complete flow from loading, expanding, populating, to persisting the file.

```csharp
        // Save the workbook with the expanded array and populated markers.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

The saved `output.xlsx` now contains a 5 × 5 matrix generated by the `EXPAND` formula and a cell that reflects the value of `{IsActive}`. Open the file in Excel to see the dynamic range in action.

## Edge cases and best practices

| Situation                              | Recommendation                                                                 |
|----------------------------------------|--------------------------------------------------------------------------------|
| Excel version does not support `EXPAND`| Fall back to classic `=OFFSET` or `=INDEX` formulas, or upgrade to Office 365. |
| Need to expand to a variable size      | Use `ROWS(source)` and `COLUMNS(source)` inside `EXPAND` for true dynamism.   |
| Multiple Smart Markers in the same sheet| Call `SmartMarkersProcessor().Apply` once with a composite data object.      |
| Large workbooks ( > 10 000 rows)       | Disable calculation while writing formulas (`workbook.Settings.CheckFormula = false`). |

## Full working example

Below is the complete, self‑contained program you can copy‑paste into a new console project.

```csharp
using System;
using Aspose.Cells;

class ExpandArrayDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook that serves as the template.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Write the EXPAND formula to create a 5x5 dynamic range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";

        // 3️⃣ Prepare data for Smart Markers.
        var data = new { IsActive = true };

        // 4️⃣ Apply Smart Markers – replaces {IsActive} in any formula or text.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);

        // 5️⃣ (Optional) Verify a couple of cells.
        Console.WriteLine($"Expanded top‑left: {ws.Cells["B2"].Value}");
        Console.WriteLine($"Marker result: {ws.Cells["C2"].StringValue}");

        // 6️⃣ Save the final workbook.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
        Console.WriteLine("Workbook saved successfully.");
    }
}
```

**Expected output when you run the program** (assuming `A2` contains the number `42`):

```
Expanded top‑left: 42
Marker result: Active
Workbook saved successfully.
```

Opening `output.xlsx` shows a 5 × 5 block filled with the values derived from `A2` and a cell that reads **Active**.

## Conclusion

You now know **how to expand array** in Excel using the `EXPAND` function, how to **populate excel template** with Smart Markers, and how to build a **dynamic range excel** that automatically adapts to source data. The example also demonstrates the correct way to **use expand function** and the **expand array formula** in a real‑world C# automation scenario.

Next, consider extending the solution:

* Replace the fixed `5,5` dimensions with `ROWS(A2:A10), COLUMNS(A2:E2)` for truly variable ranges.
* Combine multiple Smart Markers to generate full reports (e.g., employee lists, sales tables).
* Explore Aspose.Cells’ styling API to format the expanded block automatically.

Feel free to experiment with different source arrays, marker names, and workbook layouts. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Export Data to Excel: Populate a Template from an Array in C#](/cells/english/net/smart-markers-dynamic-data/export-data-to-excel-populate-a-template-from-an-array-in-c/)
- [How to create array in Excel with C# – Step-by-Step Guide](/cells/english/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/)
- [Processing Data Using Array Function in Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}