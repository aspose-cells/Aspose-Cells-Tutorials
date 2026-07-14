---
category: general
date: 2026-07-13
description: How to use WRAPCOLS in C# to convert array to columns, apply array formula
  Excel, and create Excel workbook programmatically—all with clear steps.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- convert array to columns
- apply array formula excel
- create excel workbook programmatically
- evaluate excel formula c#
language: en
lastmod: 2026-07-13
og_description: How to use WRAPCOLS in C# lets you quickly convert an array to columns,
  apply an array formula Excel style, and evaluate the result programmatically.
og_image_alt: Screenshot showing how to use WRAPCOLS formula in a C# generated Excel
  sheet
og_title: How to Use WRAPCOLS in C# – Fast Excel Workbook Creation
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to use WRAPCOLS in C# to convert array to columns, apply array
    formula Excel, and create Excel workbook programmatically—all with clear steps.
  headline: How to Use WRAPCOLS – Complete Guide for C# Excel Automation
  type: TechArticle
- description: How to use WRAPCOLS in C# to convert array to columns, apply array
    formula Excel, and create Excel workbook programmatically—all with clear steps.
  name: How to Use WRAPCOLS – Complete Guide for C# Excel Automation
  steps:
  - name: What if I need more than two columns?
    text: 'Just change the second argument of WRAPCOLS. For example, `=WRAPCOLS({1,2,3,4,5,6},3)`
      would produce three columns:'
  - name: Can I feed a dynamic range instead of a hard‑coded array?
    text: 'Absolutely. You can build the array string programmatically:'
  - name: What about error handling?
    text: 'If the formula is malformed, `Calculate()` will throw a `CellsException`.
      Wrap the calculation in a try/catch block and log the error:'
  - name: Does this work with older Excel versions?
    text: WRAPCOLS was introduced in Excel 365/2021. When you save the file as an
      older `.xls` format, the formula may be lost. Stick to `.xlsx` if you need the
      function to survive outside the C# engine.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: How to Use WRAPCOLS – Complete Guide for C# Excel Automation
url: /net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use WRAPCOLS – Complete Guide for C# Excel Automation

Ever wondered **how to use WRAPCOLS** when you need to turn a flat list into a neat table inside an Excel file generated from C#? You're not the only one. Whether you're building a reporting engine, exporting survey results, or just playing with data, the WRAPCOLS function can instantly reshape an array into the number of columns you specify.  

In this tutorial we'll walk through the whole process: from **creating an Excel workbook programmatically** to **applying an array formula Excel** style, and finally **evaluating the formula with C#**. By the end you’ll be able to **convert array to columns** in a single line of code, no manual cell‑by‑cell gymnastics required.

> **What you’ll get:** a runnable code sample, explanation of each step, tips for common pitfalls, and suggestions for extending the solution.

---

## Prerequisites

Before we dive in, make sure you have:

- .NET 6.0+ (or any recent .NET runtime)
- A C# IDE (Visual Studio, Rider, or VS Code)
- The **Aspose.Cells for .NET** library (free trial works fine) – it’s the easiest way to manipulate Excel files without needing Excel installed.
- Basic familiarity with C# syntax and Excel formulas.

If you prefer a different library (e.g., EPPlus or ClosedXML), the core ideas stay the same—just swap the API calls.

---

## Step 1: Set Up Your Project and Add the Excel Library

First things first, create a new console app and pull in Aspose.Cells via NuGet:

```bash
dotnet new console -n WrapColsDemo
cd WrapColsDemo
dotnet add package Aspose.Cells
```

> **Pro tip:** Use the `--version` flag to lock to a known stable version, e.g., `Aspose.Cells 24.9`.

Now open `Program.cs`. We'll start by adding the required namespaces:

```csharp
using System;
using Aspose.Cells;   // Main API for workbook manipulation
```

Having the library referenced ensures we can **create excel workbook programmatically** and work with formulas.

---

## Step 2: Create a New Workbook and Target Cell

Next, instantiate a fresh workbook and pick the cell where the WRAPCOLS formula will live. In Excel terms, cell **A1** is row 0, column 0.

```csharp
// Step 2.1: Create a new workbook (blank Excel file)
Workbook workbook = new Workbook();

// Step 2.2: Grab the first worksheet (default)
Worksheet sheet = workbook.Worksheets[0];

// Step 2.3: Define the target cell (A1)
Cell targetCell = sheet.Cells[0, 0];
```

Why do we do this? The `Workbook` object is the container for all sheets, styles, and calculations. By explicitly referencing the cell, we keep the code clear and avoid “magic numbers” later on.

---

## Step 3: Insert the WRAPCOLS Array Formula

Now comes the heart of the tutorial—**how to use WRAPCOLS**. The function takes an array and a column count, then spits out a two‑dimensional range. In Excel syntax it looks like this:

```
=WRAPCOLS({1,2,3,4}, 2)
```

That tells Excel to arrange the numbers 1‑4 into **2 columns**, resulting in:

| A | B |
|---|---|
| 1 | 3 |
| 2 | 4 |

To embed that formula from C#:

```csharp
// Step 3: Apply the WRAPCOLS array formula to A1
targetCell.Formula = "=WRAPCOLS({1,2,3,4},2)";
```

Notice we’re using a **string** that mirrors what you’d type into Excel’s formula bar. This is the **apply array formula excel** step, and Aspose.Cells automatically treats it as an array formula because WRAPCOLS returns a range.

---

## Step 4: Force Calculation So the Formula Is Evaluated

Excel normally recalculates lazily—only when you open the file. Since we want to read the result immediately, we must trigger a calculation:

```csharp
// Step 4: Calculate the workbook so the WRAPCOLS formula resolves
workbook.Calculate();
```

Calling `Calculate()` is the **evaluate excel formula c#** action that forces the engine to compute every formula, including our WRAPCOLS array. Without this call, `targetCell.Value` would still be `null`.

---

## Step 5: Retrieve and Verify the Result

Now that the workbook has been calculated, we can fetch the value(s) from the cells that the array occupied. The top‑left cell (A1) holds the first element, while the adjacent cells contain the rest. Let's read the whole 2 × 2 block:

```csharp
// Step 5: Read the evaluated values from the resulting range
object[,] result = targetCell.GetArrayValue() as object[,];

// Simple sanity check: print the 2x2 matrix to console
if (result != null)
{
    for (int r = 0; r < result.GetLength(0); r++)
    {
        for (int c = 0; c < result.GetLength(1); c++)
        {
            Console.Write($"{result[r, c]}\t");
        }
        Console.WriteLine();
    }
}
else
{
    Console.WriteLine("No array result was returned.");
}
```

When you run the program, the console should display:

```
1   3
2   4
```

That output confirms we successfully **convert array to columns** using WRAPCOLS.

---

## Step 6: Save the Workbook (Optional but Handy)

If you’d like to open the file in Excel and see the formula live, just save it:

```csharp
// Step 6: Persist the workbook to disk (optional)
workbook.Save("WrapColsDemo.xlsx");
Console.WriteLine("Workbook saved as WrapColsDemo.xlsx");
```

Opening the file will show the WRAPCOLS formula in A1 and the populated 2‑column range beneath it. This step is useful for debugging or for delivering the file to end users.

---

## Common Questions & Edge Cases

### What if I need more than two columns?

Just change the second argument of WRAPCOLS. For example, `=WRAPCOLS({1,2,3,4,5,6},3)` would produce three columns:

| A | B | C |
|---|---|---|
| 1 | 3 | 5 |
| 2 | 4 | 6 |

Update the C# line accordingly:

```csharp
targetCell.Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

### Can I feed a dynamic range instead of a hard‑coded array?

Absolutely. You can build the array string programmatically:

```csharp
int[] numbers = Enumerable.Range(1, 10).ToArray();
string arrayLiteral = "{" + string.Join(",", numbers) + "}";
targetCell.Formula = $"=WRAPCOLS({arrayLiteral},2)";
```

That way you **apply array formula excel** on the fly, perfect for reports with variable data sizes.

### What about error handling?

If the formula is malformed, `Calculate()` will throw a `CellsException`. Wrap the calculation in a try/catch block and log the error:

```csharp
try
{
    workbook.Calculate();
}
catch (CellsException ex)
{
    Console.Error.WriteLine($"Formula evaluation failed: {ex.Message}");
}
```

### Does this work with older Excel versions?

WRAPCOLS was introduced in Excel 365/2021. When you save the file as an older `.xls` format, the formula may be lost. Stick to `.xlsx` if you need the function to survive outside the C# engine.

---

## Full Working Example

Putting everything together, here’s the complete, copy‑paste‑ready program:

```csharp
using System;
using System.Linq;
using Aspose.Cells;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.Worksheets[0];
            Cell targetCell = sheet.Cells[0, 0];

            // 2️⃣ Build a dynamic array (optional)
            int[] numbers = Enumerable.Range(1, 8).ToArray(); // {1,2,3,4,5,6,7,8}
            string arrayLiteral = "{" + string.Join(",", numbers) + "}";

            // 3️⃣ Apply WRAPCOLS – convert array to columns (2 columns in this case)
            targetCell.Formula = $"=WRAPCOLS({arrayLiteral},2)";

            // 4️⃣ Force calculation – evaluate excel formula c#
            try
            {
                workbook.Calculate();
            }
            catch (CellsException ex)
            {
                Console.Error.WriteLine($"Failed to evaluate formula: {ex.Message}");
                return;
            }

            // 5️⃣ Retrieve the 2‑column result
            object[,] result = targetCell.GetArrayValue() as object[,];
            if (result != null)
            {
                Console.WriteLine("WRAPCOLS result:");
                for (int r = 0; r < result.GetLength(0); r++)
                {
                    for (int c = 0; c < result.GetLength(1); c++)
                    {
                        Console.Write($"{result[r, c]}\t");
                    }
                    Console.WriteLine();
                }
            }

            // 6️⃣ Save the file for visual inspection (optional)
            workbook.Save("WrapColsDemo.xlsx");
            Console.WriteLine("\nWorkbook saved as WrapColsDemo.xlsx");
        }
    }
}
```

Run `dotnet run` and you should see the matrix printed, followed by a confirmation that the `.xlsx` file exists.

---

## Recap & Next Steps

We’ve covered **how to use WRAPCOLS** to **convert array to columns**, demonstrated the **apply array formula excel** technique from C#, forced a calculation to **evaluate excel formula c#**, and saved the result for downstream consumption.  

If you’re hungry for more:

- **Dynamic column counts:** let the column number be a user‑input variable.
- **Styling the output:** apply fonts, borders, or conditional formatting via Aspose.Cells after the calculation.
- **Combining with other functions:** nest WRAPCOLS inside `LET` or `FILTER`


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Aspose.Cells .NET&#58; How to Create & Style Excel Workbooks Programmatically](/cells/english/net/formatting/aspose-cells-net-create-style-excel-workbooks/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}