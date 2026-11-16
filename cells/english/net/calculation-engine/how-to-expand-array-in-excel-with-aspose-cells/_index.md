---
category: general
date: 2026-11-16
description: Learn how to generate and expand an array in Excel using Aspose.Cells, dynamic array functions, and a lambda reducer, then write the Excel file from C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- create excel workbook
- how to use lambda
- dynamic array functions
- write excel file
language: en
lastmod: 2026-11-16
og_description: How to expand array in Excel using Aspose.Cells, dynamic array functions,
  and a lambda reducer. Follow the complete C# example to write the Excel file.
og_image_alt: Diagram illustrating how to expand array in an Excel worksheet
og_title: How to expand array in Excel with Aspose.Cells – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to expand array in Excel using Aspose.Cells, dynamic array
    functions, and a lambda reducer, then write the Excel file from C#.
  headline: How to expand array in Excel with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. `EXPAND` pads missing columns with blank cells. The same works for
      rows.
    question: Can I expand to more columns than the source provides?
  - answer: '`EXPAND` will treat the source as a single row; you can still specify
      rows and columns to reshape it.'
    question: What if the source array is horizontal (`{1,2,3,4,5}`)?
  - answer: The lambda must return a value compatible with the accumulator type. For
      text concatenation you could use `LAMBDA(acc, val, acc & val)`.
    question: Does `REDUCE` work with non‑numeric data?
  - answer: Only when you need the computed values before saving. Excel will recalculate
      on open if you skip it.
    question: Do I need to call `CalculateFormula` for every change?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: Generate and expand array in Excel using Aspose.Cells
url: /net/calculation-engine/how-to-expand-array-in-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to expand array in Excel with Aspose.Cells

If you need to **how to expand array** in an Excel worksheet from C#, this tutorial shows the exact steps. You’ll create an Excel workbook, use dynamic array functions like `EXPAND` and `REDUCE`, apply a **lambda** accumulator, and finally **write Excel file** to disk. The approach works with Aspose.Cells 23.10 or later and requires no manual Excel installation.

By the end of this guide you will have a fully functional `ExpandReduceDemo.xlsx` that demonstrates the power of dynamic array formulas in a programmatic context.

## What you’ll need

- .NET 6.0 (or any .NET version supported by Aspose.Cells)
- Aspose.Cells for .NET package (`dotnet add package Aspose.Cells`)
- A code editor or IDE (Visual Studio, VS Code, Rider, etc.)

No additional COM interop or Office installation is required because Aspose.Cells handles the file format internally.

## Step 1: Create Excel workbook

The first task is to **create excel workbook** in memory. Aspose.Cells provides the `Workbook` class, which represents an entire XLSX file.

```csharp
using System;
using Aspose.Cells;

class ExpandReduceDemo
{
    static void Main()
    {
        // Step 1: instantiate a new workbook and get the default worksheet
        Workbook workbook = new Workbook();              // creates an empty .xlsx structure
        Worksheet sheet = workbook.Worksheets[0];        // the first (and only) sheet by default
```

> **Why this matters:** Instantiating a `Workbook` gives you a clean canvas. The default worksheet is already prepared, so you don’t need to add one manually unless you want multiple sheets.

## Step 2: Insert a vertical array constant

Excel’s dynamic array engine can work with literal array constants. We’ll place the vertical array `{1;2;3;4;5}` into cell **A1**.

```csharp
        // Step 2: put a vertical array constant into A1
        sheet.Cells["A1"].PutValue("{1;2;3;4;5}");
```

> **Tip:** The semicolon (`;`) separates rows in the constant, while a comma (`,`) would separate columns. This mirrors Excel’s own syntax.

## Step 3: Expand the array into a matrix

Now we answer the core question – **how to expand array** – using the `EXPAND` function. The formula expands the single‑column array into a 5‑row × 2‑column matrix, starting at **B1**.

```csharp
        // Step 3: use EXPAND to create a 5‑row by 2‑column matrix
        sheet.Cells["B1"].Formula = "EXPAND(A1,5,2)";
```

> **Why EXPAND?** `EXPAND(source, rows, cols)` forces the source range to occupy the specified size, padding with blanks if necessary. It’s the most readable way to generate a larger matrix from a single array.

## Step 4: Reduce the matrix with a lambda accumulator

The `REDUCE` function iterates over a range and aggregates values using a **lambda** expression. Here we sum each column value into a single column, placing the result in **D1**.

```csharp
        // Step 4: REDUCE the expanded matrix using a lambda accumulator
        sheet.Cells["D1"].Formula = "REDUCE(A1, B1:E5, LAMBDA(acc, val, acc+val))";
```

> **How to use lambda:** The `LAMBDA(acc, val, acc+val)` receives the current accumulator (`acc`) and the next cell value (`val`). It returns the new accumulator, effectively performing a running total. This demonstrates **how to use lambda** in Excel formulas from code.

## Step 5: Calculate formulas so results appear

Aspose.Cells does not automatically evaluate formulas when you set them. Calling `CalculateFormula` forces the engine to compute every formula in the workbook.

```csharp
        // Step 5: recalculate all formulas so the results are materialized
        workbook.CalculateFormula();
```

> **Note:** If you open the generated file in Excel, the values will already be visible because they have been pre‑calculated.

## Step 6: Write Excel file to disk

Finally, **write excel file** using the `Save` method. Choose a folder you have write permission for.

```csharp
        // Step 6: save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\ExpandReduceDemo.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Expected outcome

| A | B | C | D |
|---|---|---|---|
| {1;2;3;4;5} | 1 |  | 15 |
|            | 2 |  |    |
|            | 3 |  |    |
|            | 4 |  |    |
|            | 5 |  |    |

- **Column B** and **C** contain the 5 × 2 matrix produced by `EXPAND`.
- **Cell D1** shows `15`, the sum of all numbers, calculated by the `REDUCE` + **lambda** formula.

## Common questions and edge cases

- **Can I expand to more columns than the source provides?**  
  Yes. `EXPAND` pads missing columns with blank cells. The same works for rows.

- **What if the source array is horizontal (`{1,2,3,4,5}`)?**  
  `EXPAND` will treat the source as a single row; you can still specify rows and columns to reshape it.

- **Does `REDUCE` work with non‑numeric data?**  
  The lambda must return a value compatible with the accumulator type. For text concatenation you could use `LAMBDA(acc, val, acc & val)`.

- **Do I need to call `CalculateFormula` for every change?**  
  Only when you need the computed values before saving. Excel will recalculate on open if you skip it.

## Pro tips

- **Performance:** For large workbooks, call `workbook.CalculateFormula` once after all formulas are set, rather than after each cell.
- **Version safety:** `EXPAND` and `REDUCE` are available in Excel 365 and later. Aspose.Cells implements them regardless of the target Excel version because the calculation engine is built‑in.
- **Debugging formulas:** Use `sheet.Cells["B1"].Formula` to read back the exact string you set; this helps when you build formulas dynamically.

## Conclusion

You now know **how to expand array** in Excel using Aspose.Cells, leverage **dynamic array functions**, apply a **lambda** with `REDUCE`, and **write excel file** from C#. This end‑to‑end example can be adapted to more complex data transformations, such as matrix transposition, cumulative totals, or custom aggregations.

---

*Next steps:*  
- Explore other dynamic functions like `FILTER`, `SORT`, and `UNIQUE`.  
- Combine multiple `LAMBDA` expressions to build reusable user‑defined functions.  
- Integrate the workbook generation into ASP.NET Core APIs for on‑the‑fly report creation.


## What should you learn next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step‑by‑step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to create Excel workbook C# with a dynamic array formula]({{< relref "/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/" >}})
- [How to expand array in Excel and populate a template]({{< relref "/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/" >}})
- [How to Expand Array in C# with Aspose.Cells – Step‑by‑Step Guide]({{< relref "/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/" >}})

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}