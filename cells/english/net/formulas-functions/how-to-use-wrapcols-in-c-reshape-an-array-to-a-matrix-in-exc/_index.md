---
category: general
date: 2026-06-17
description: How to use WRAPCOLS in C# to reshape an array to a matrix, write array
  formula to a cell, and load existing Excel files with Aspose.Cells.
draft: false
keywords:
- how to use wrapcols
- reshape array to matrix
- write array formula
- write formula to cell
- load existing excel
language: en
og_description: How to use WRAPCOLS in C# to quickly reshape an array to a matrix,
  write an array formula to a cell, and work with existing Excel files.
og_title: How to Use WRAPCOLS in C# – Reshape an Array to a Matrix
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: How to use WRAPCOLS in C# to reshape an array to a matrix, write array
    formula to a cell, and load existing Excel files with Aspose.Cells.
  headline: How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel
  type: TechArticle
- description: How to use WRAPCOLS in C# to reshape an array to a matrix, write array
    formula to a cell, and load existing Excel files with Aspose.Cells.
  name: How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel
  steps:
  - name: 'Optional: Write a Dynamic Array Reference'
    text: 'If you prefer to reference a range instead of a hard‑coded list, you can
      use:'
  - name: 1. What if I need a different number of rows?
    text: '`WRAPCOLS` only takes the column count; the row count is inferred. To force
      a specific row count, you can combine it with `WRAPROWS` or pad the source array
      with empty strings.'
  - name: 2. Does WRAPCOLS work with text values?
    text: 'Absolutely. Replace the numbers with quoted strings:'
  - name: 3. Can I apply formatting to the generated matrix?
    text: 'After calculation, you can style the range programmatically:'
  - name: 4. How do I handle very large arrays?
    text: Aspose.Cells can process tens of thousands of elements, but keep an eye
      on memory. If you hit limits, consider writing the data in chunks or using `Workbook.Settings.MemorySetting
      = MemorySetting.MemoryPreference;`.
  type: HowTo
tags:
- excel
- csharp
- aspose.cells
title: How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel
url: /net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel

Ever wondered **how to use WRAPCOLS** to turn a flat list of numbers into a tidy table inside Excel? You’re not alone. Whether you’re building a reporting tool or just playing with data, reshaping an array to a matrix can save you a ton of manual copy‑pasting.

In this tutorial we’ll walk through a complete, runnable example that shows you how to **write an array formula to a cell**, calculate the result, and even **load an existing Excel** workbook if you need to. By the end you’ll have a solid, copy‑paste‑ready snippet that works with the latest Aspose.Cells for .NET.

## What You’ll Learn

- The purpose of the `WRAPCOLS` function and when it shines.  
- How to **reshape an array to a matrix** using a single formula.  
- Step‑by‑step code to **write a formula to a cell** and force calculation.  
- Optional techniques for **loading an existing Excel** file before applying the formula.  
- Common pitfalls and tips for extending the approach to larger data sets.

No external documentation required—everything you need is right here.

## Prerequisites

- .NET 6.0 or later (the code also works on .NET Framework 4.7+).  
- Aspose.Cells for .NET installed (`dotnet add package Aspose.Cells`).  
- A basic understanding of C# syntax; if you’re comfortable creating a console app, you’re good to go.

> **Pro tip:** If you’re using Visual Studio, enable *nullable reference types* (`<Nullable>enable</Nullable>`) to catch potential null bugs early.

## Step 1: Set Up the Project and Import Namespaces

First, create a new console project (or drop the code into an existing one). Then add the necessary `using` directives so the compiler knows where `Workbook` and `Worksheet` live.

```csharp
using System;
using Aspose.Cells;   // Main library for Excel manipulation

namespace WrapColsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill in the logic in the next steps
        }
    }
}
```

> **Why this matters:** Importing `Aspose.Cells` gives you access to the high‑performance Excel engine that evaluates `WRAPCOLS` without needing Excel installed on the machine.

## Step 2: Create or Load a Workbook

You can start from scratch or open an existing file. The following snippet shows both options; just comment out the one you don’t need.

```csharp
// Option A – Create a brand‑new workbook
Workbook workbook = new Workbook();   // starts with a single empty worksheet

// Option B – Load an existing Excel file (useful when you have templates)
// string inputPath = @"C:\Data\input.xlsx";
// Workbook workbook = new Workbook(inputPath);
```

> **Edge case:** If the file you’re loading is password‑protected, pass the password as the second argument: `new Workbook(path, "password")`.

## Step 3: Grab the Target Worksheet

Most of the time the first sheet (`Worksheets[0]`) is what you want, but you can also refer to a sheet by name.

```csharp
Worksheet sheet = workbook.Worksheets[0];               // by index
// Worksheet sheet = workbook.Worksheets["DataSheet"]; // by name (if it exists)
```

## Step 4: Write the WRAPCOLS Formula to a Cell

Here’s the heart of the tutorial. `WRAPCOLS` takes an array and a column count, then spills the values row‑wise. We’ll place the formula in **A1** so the matrix starts at the top‑left corner.

```csharp
// Write the WRAPCOLS formula that turns {1,2,3,4,5,6} into 2 rows × 3 columns
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

> **What’s happening?**  
> - The curly‑brace syntax `{1,2,3,4,5,6}` creates an inline array constant.  
> - The second argument (`3`) tells Excel to create three columns, automatically wrapping the remaining items into new rows.  
> - Because we’re using Aspose.Cells, the formula is stored exactly as you’d type it in Excel, and the engine will evaluate it on demand.

### Optional: Write a Dynamic Array Reference

If you prefer to reference a range instead of a hard‑coded list, you can use:

```csharp
// Assume B1:B6 already contains numbers you want to reshape
sheet.Cells["A1"].Formula = "=WRAPCOLS(B1:B6,3)";
```

That way the matrix updates automatically whenever the source range changes.

## Step 5: Force Calculation and Persist the Result

Aspose.Cells doesn’t calculate formulas until you tell it to. Calling `Calculate()` materializes the result, turning the formula output into actual cell values.

```csharp
// Force calculation so the WRAPCOLS output appears in the sheet
workbook.Calculate();

// Save the workbook – adjust the path as needed
string outputPath = @"C:\Data\output.xlsx";
workbook.Save(outputPath);
```

When you open `output.xlsx` in Excel, you’ll see:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

That’s the **reshape array to matrix** effect you were after.

## Full Working Example

Putting all the pieces together, here’s a ready‑to‑run program:

```csharp
using System;
using Aspose.Cells;

namespace WrapColsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create a new workbook (or load an existing one)
            Workbook workbook = new Workbook(); // new Workbook(@"C:\Data\input.xlsx");

            // 2️⃣ Get the first worksheet
            Worksheet sheet = workbook.Worksheets[0];

            // 3️⃣ Write the WRAPCOLS formula – reshape {1..6} into 2×3
            sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

            // 4️⃣ Force calculation so the matrix is materialized
            workbook.Calculate();

            // 5️⃣ Save the result
            string outputPath = @"C:\Data\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

Run the program, open `output.xlsx`, and you’ll see the matrix exactly as shown above.

## Common Questions & Gotchas

### 1. What if I need a different number of rows?

`WRAPCOLS` only takes the column count; the row count is inferred. To force a specific row count, you can combine it with `WRAPROWS` or pad the source array with empty strings.

```csharp
// Example: Force 3 rows, 2 columns (will add blanks if needed)
sheet.Cells["A1"].Formula = "=WRAPROWS({1,2,3,4,5,6},3)";
```

### 2. Does WRAPCOLS work with text values?

Absolutely. Replace the numbers with quoted strings:

```csharp
sheet.Cells["A1"].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",\"Apr\",\"May\",\"Jun\"},3)";
```

### 3. Can I apply formatting to the generated matrix?

After calculation, you can style the range programmatically:

```csharp
Range matrix = sheet.Cells.CreateRange("A1:C2");
Style style = workbook.CreateStyle();
style.Font.Color = System.Drawing.Color.Blue;
style.Font.IsBold = true;
matrix.ApplyStyle(style, new StyleFlag() { Font = true });
```

### 4. How do I handle very large arrays?

Aspose.Cells can process tens of thousands of elements, but keep an eye on memory. If you hit limits, consider writing the data in chunks or using `Workbook.Settings.MemorySetting = MemorySetting.MemoryPreference;`.

## Pro Tips for Production Code

- **Cache the worksheet reference** if you’re writing many formulas in a loop; it reduces lookup overhead.  
- **Disable automatic calculation** (`workbook.Settings.CalculateFormulaOnOpen = false;`) when you plan to batch‑write dozens of formulas, then call `Calculate()` once at the end.  
- **Wrap the file I/O in try/catch** to surface permission errors early:

```csharp
try
{
    workbook.Save(outputPath);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
}
```

- **Validate input** before building the formula string—especially if you concatenate user‑provided values—to avoid malformed formulas.

## Visual Summary

![How to use WRAPCOLS result matrix in Excel](wrapcols-output.png "How to use WRAPCOLS in C# to reshape an array to a matrix")

*The screenshot shows the 2 × 3 matrix produced by the WRAPCOLS formula.*

## Conclusion

We’ve covered **how to use WRAPCOLS** in C# from start to finish: creating or loading a workbook, writing an array formula to a cell, forcing calculation, and saving the result. You now know how to **reshape an array to a matrix**, **write an array formula**, and **load existing Excel** files—all with a handful of lines of clean, maintainable code.

Next, you might explore:


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Load Excel Files Efficiently Using Aspose.Cells in .NET](/cells/english/net/workbook-operations/efficient-excel-load-aspose-cells-net/)
- [How to Load and Modify Excel Files Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/workbook-operations/load-modify-excel-aspose-cells-net/)
- [How to Set Language in Excel Files Using Aspose.Cells .NET for Multilingual Support](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}