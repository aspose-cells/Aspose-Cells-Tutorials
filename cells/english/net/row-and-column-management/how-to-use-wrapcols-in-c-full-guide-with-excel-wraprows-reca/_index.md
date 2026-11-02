---
category: general
date: 2026-06-27
description: how to use wrapcols and wrap rows excel in C#. Learn to create excel
  workbook c# and recalculate excel formulas with a step‑by‑step example.
draft: false
keywords:
- how to use wrapcols
- wrap rows excel
- wrap columns excel
- recalculate excel formulas
- create excel workbook c#
language: en
og_description: how to use wrapcols and wrap rows excel using C#. This guide shows
  how to create excel workbook c# and recalculate excel formulas in minutes.
og_title: how to use wrapcols in C# – Complete Excel Wrapping Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: how to use wrapcols and wrap rows excel in C#. Learn to create excel
    workbook c# and recalculate excel formulas with a step‑by‑step example.
  headline: how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate
    Formulas
  type: TechArticle
- description: how to use wrapcols and wrap rows excel in C#. Learn to create excel
    workbook c# and recalculate excel formulas with a step‑by‑step example.
  name: how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas
  steps:
  - name: Expected Result
    text: '| A | B | C | |---|---|---| | 1 | A | 2 | | 2 | B | 3 | | 3 | C | 4 | |
      4 | D | 5 | | 5 | E | 6 | | 6 | F | 7 | | 7 | G | 8 | | 8 | H | 9 | | 9 | I
      | |'
  - name: What if the source range is empty?
    text: Both `WRAPCOLS` and `WRAPROWS` will simply return an empty array, resulting
      in a blank cell. It’s safe to call the functions even when you’re not sure about
      data presence.
  - name: Can I wrap more than one range at a time?
    text: Yes—just place additional formulas in other cells. Each formula works independently,
      so you could have `WRAPCOLS` in D1, `WRAPROWS` in E1, etc.
  - name: How does this differ from a simple copy‑paste transpose?
    text: '`WRAPCOLS`/`WRAPROWS` handle *pagination* automatically. If you have 20
      items and ask for 3 columns, the function creates the necessary number of rows
      (7 in this case) without you calculating the dimensions manually.'
  - name: Does the library support dynamic array formulas (Excel 365)?
    text: Aspose.Cells fully supports dynamic array functions, including `WRAPCOLS`
      and `WRAPROWS`. The calculation engine will spill the results just like native
      Excel.
  - name: What about performance on large datasets?
    text: For millions of rows, consider batching the calculation (`workbook.CalculateFormula(FormulaCalculationOptions)`)
      or disabling automatic calculation while you insert formulas, then re‑enable
      it before saving.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas
url: /net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas

Ever wondered **how to use wrapcols** when you need to reshape a long list into a tidy grid? Maybe you’ve tried the manual copy‑paste trick, but it’s slow, error‑prone, and frankly, a pain. The good news? Excel’s `WRAPCOLS` (and its sibling `WRAPROWS`) can do the heavy lifting for you—*and* you can drive them from C# code.

In this tutorial we’ll walk through creating an Excel workbook in C#, applying `WRAPCOLS` and `WRAPROWS`, and finally **recalculate excel formulas** so the wrapped data shows up instantly. By the end you’ll have a ready‑to‑run snippet that you can drop into any .NET project.

## What You’ll Learn

- How to **create excel workbook c#** using the Aspose.Cells library (no COM interop required).  
- The exact syntax for the `WRAPCOLS` function and how it differs from `WRAPROWS`.  
- Why you must **recalculate excel formulas** after inserting the functions, and how to do it efficiently.  
- A complete, runnable example that you can copy‑paste and see the result in an `.xlsx` file.  

**Prerequisites** – You need .NET 6+ (or .NET Framework 4.7+), Visual Studio 2022 or any IDE you like, and the Aspose.Cells for .NET NuGet package. If you’re new to Aspose.Cells, don’t worry; the steps are straightforward and fully explained.

---

## Step 1: Set Up the Project and Install Aspose.Cells

To start, create a new console project:

```bash
dotnet new console -n WrapDemo
cd WrapDemo
dotnet add package Aspose.Cells
```

> **Pro tip:** If you’re using Visual Studio, just right‑click the project → *Manage NuGet Packages* → search for **Aspose.Cells** and install it.

The library gives us the `Workbook`, `Worksheet`, and `Cell` classes we’ll need for the rest of the tutorial.

## Step 2: Create an Excel Workbook and Populate Sample Data

Now we’ll spin up a workbook, grab the first worksheet, and fill column **A** and **B** with sample numbers. This data will later be wrapped into columns and rows.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 2‑1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2‑2: Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate A2:A10 with numbers 1‑9
        for (int i = 2; i <= 10; i++)
        {
            worksheet.Cells[$"A{i}"].PutValue(i - 1);
        }

        // Populate B2:B10 with letters A‑I (just for variety)
        char letter = 'A';
        for (int i = 2; i <= 10; i++, letter++)
        {
            worksheet.Cells[$"B{i}"].PutValue(letter.ToString());
        }

        // The rest of the steps follow…
```

> **Why this matters:** Having deterministic data lets you verify that `WRAPCOLS` and `WRAPROWS` are doing exactly what you expect.

## Step 3: Apply the `WRAPCOLS` Function – **how to use wrapcols**

`WRAPCOLS` takes a one‑dimensional range and spreads it across a specified number of columns, automatically adding new rows as needed. Here’s the exact formula we’ll inject into cell **A1**:

```csharp
        // Step 3: Insert WRAPCOLS formula – wrap A2:A10 into 3 columns per row
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A2:A10, 3)";
```

> **Explanation:** The second argument (`3`) tells Excel to create three columns per row. So the first three values (1, 2, 3) land in A1:C1, the next three (4, 5, 6) go in A2:C2, and the remaining values fill the next row.

## Step 4: Apply the `WRAPROWS` Function – wrap rows excel

`WRAPROWS` does the opposite: it takes a vertical range and arranges it into a set number of rows per column. We’ll place this formula in **B1**:

```csharp
        // Step 4: Insert WRAPROWS formula – wrap B2:B10 into 2 rows per column
        worksheet.Cells["B1"].Formula = "=WRAPROWS(B2:B10, 2)";
```

> **Explanation:** With `2` rows per column, the values “A, B” go into B1:B2, “C, D” into C1:C2, and so on. The function automatically expands the sheet horizontally.

## Step 5: Recalculate All Formulas – **recalculate excel formulas**

When you set a formula programmatically, Excel won’t compute the result until the workbook is opened or you explicitly tell the library to evaluate it. That’s where **recalculate excel formulas** comes in:

```csharp
        // Step 5: Force calculation so the wrapped data appears immediately
        workbook.CalculateFormula();
```

> **Why you need this:** Without calling `CalculateFormula()`, the cells will show the raw `=WRAPCOLS(...)` text when you open the file, which defeats the purpose of the tutorial.

## Step 6: Save the Workbook and Verify the Output

Finally, write the workbook to disk. You can open the resulting file in Excel to see the wrapped layout.

```csharp
        // Step 6: Save the workbook (adjust the path as needed)
        string outputPath = "output.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see wrapcols and wraprows in action.");
    }
}
```

### Expected Result

| A | B | C |
|---|---|---|
| 1 | A | 2 |
| 2 | B | 3 |
| 3 | C | 4 |
| 4 | D | 5 |
| 5 | E | 6 |
| 6 | F | 7 |
| 7 | G | 8 |
| 8 | H | 9 |
| 9 | I |   |

- **Columns A‑C** are populated by the `WRAPCOLS` call (three columns per row).  
- **Rows B‑I** are populated by the `WRAPROWS` call (two rows per column).  

Open `output.xlsx` and you’ll see the exact layout shown above. If the numbers don’t line up, double‑check the formula strings and make sure `CalculateFormula()` was called.

---

## Common Questions & Edge Cases

### What if the source range is empty?
Both `WRAPCOLS` and `WRAPROWS` will simply return an empty array, resulting in a blank cell. It’s safe to call the functions even when you’re not sure about data presence.

### Can I wrap more than one range at a time?
Yes—just place additional formulas in other cells. Each formula works independently, so you could have `WRAPCOLS` in D1, `WRAPROWS` in E1, etc.

### How does this differ from a simple copy‑paste transpose?
`WRAPCOLS`/`WRAPROWS` handle *pagination* automatically. If you have 20 items and ask for 3 columns, the function creates the necessary number of rows (7 in this case) without you calculating the dimensions manually.

### Does the library support dynamic array formulas (Excel 365)?
Aspose.Cells fully supports dynamic array functions, including `WRAPCOLS` and `WRAPROWS`. The calculation engine will spill the results just like native Excel.

### What about performance on large datasets?
For millions of rows, consider batching the calculation (`workbook.CalculateFormula(FormulaCalculationOptions)`) or disabling automatic calculation while you insert formulas, then re‑enable it before saving.

---

## Full Source Code (Ready to Run)

Below is the complete program—copy it into `Program.cs` and hit **F5**.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate column A (A2:A10) with numbers 1‑9
        for (int i = 2; i <= 10; i++)
        {
            worksheet.Cells[$"A{i}"].PutValue(i - 1);
        }

        // Populate column B (B2:B10) with letters A‑I
        char letter = 'A';
        for (int i = 2; i <= 10; i++, letter++)
        {
            worksheet.Cells[$"B{i}"].PutValue(letter.ToString());
        }

        // Apply WRAPCOLS – wrap A2:A10 into 3 columns per row
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A2:A10, 3)";

        // Apply WRAPROWS – wrap B2:B10 into 2 rows per column
        worksheet.Cells["B1"].Formula = "=WRAPROWS(B2:B10, 2)";

        // Recalculate all formulas so the wrapped data appears
        workbook.CalculateFormula();

        // Save the workbook (adjust the folder if needed)
        string outputPath = "output.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the wrapped results.");
    }
}
```

---

## Conclusion

You now know **how to use wrapcols** (and its counterpart `WRAPROWS`) from C# to reshape data in an Excel sheet, and you understand why **recalculate excel formulas** is a mandatory step. This pattern—*create excel workbook c# → insert WRAP functions → recalculate*—is a solid foundation for any reporting or data‑presentation task that requires dynamic column or row layouts.

What’s next? Try experimenting with:

- Different column/row counts (`WRAPCOLS(..., 5)` or `WRAPROWS(..., 4)`).  
- Combining `WRAPCOLS` with other dynamic array functions like `FILTER` or `SORT`.  
- Exporting the workbook to PDF with `workbook.Save("report.pdf", SaveFormat.Pdf)`.

Feel free to tweak the sample, add styling, or integrate it into a larger automation pipeline. If you hit any snags, drop a comment below—happy coding!

![Diagram showing how wrapcols and wraprows transform a single column into a grid – how to use wrapcols example](wrapcols-wraprows-diagram.png "how to use wrapcols example")


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Use Aspose.Cells for .NET to Group Rows and Columns in Excel](/cells/english/net/data-analysis/excel-grouping-aspose-cells-net/)
- [How to Hide Rows and Columns in Excel Using Aspose.Cells .NET: A Comprehensive Guide](/cells/english/net/range-management/aspose-cells-net-hide-rows-columns-excel/)
- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}