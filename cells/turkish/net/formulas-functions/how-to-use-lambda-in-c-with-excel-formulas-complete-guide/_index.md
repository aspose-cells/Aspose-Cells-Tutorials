---
category: general
date: 2026-03-22
description: C#'de lambda kullanarak Excel formülleriyle nasıl çalışılır. Formülü
  hücreye yazmayı, aralığı diziye dönüştürmeyi, diziyi konsolda görüntülemeyi ve Excel'de
  kotanjantı hesaplamayı öğrenin.
draft: false
keywords:
- how to use lambda
- display array in console
- convert range to array
- write formula to cell
- calculate cotangent in excel
language: tr
og_description: C#'de lambda kullanarak Excel formüllerini manipüle etme, aralığı
  diziye dönüştürme, hücreye formül yazma, diziyi konsolda gösterme ve Excel'de kotanjant
  hesaplama.
og_title: C#'ta Lambda'yı Excel Formülleriyle Nasıl Kullanılır – Adım Adım
tags:
- C#
- Aspose.Cells
- Excel Automation
- Lambda Expressions
title: C#'ta Lambda Kullanımı ve Excel Formülleri – Tam Rehber
url: /tr/net/formulas-functions/how-to-use-lambda-in-c-with-excel-formulas-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use Lambda in C# with Excel Formulas – Complete Guide

Ever wondered **how to use lambda** when you’re automating Excel from C#? You’re not alone. Many developers hit a wall when they need to combine the power of Excel’s new dynamic array functions with C#’s `LAMBDA` capability. The good news? It’s actually pretty straightforward once you see the pieces fit together.

In this tutorial we’ll walk through **writing a formula to a cell**, **converting a range to an array**, **displaying that array in the console**, and even **calculating cotangent in Excel**—all while showing you **how to use lambda** inside a `REDUCE` call. By the end you’ll have a runnable snippet that you can drop into any .NET project that references Aspose.Cells (or a similar library).

---

## What You’ll Learn

- How to **write formula to cell** using C#.
- How to **convert range to array** with the `EXPAND` function.
- How to **display array in console** after calculation.
- How to **calculate cotangent in Excel** using `COT` and `COTH`.
- The exact syntax for **how to use lambda** inside Excel’s `REDUCE` function from C#.

> **Prerequisite:** You need a recent version of .NET (Core 6+ or .NET Framework 4.7+) and the Aspose.Cells for .NET library installed via NuGet.

---

## Step 1: Set Up the Workbook and Write Formula to Cell

The first thing we do is spin up a fresh workbook and grab the first worksheet. Then we **write a formula to a cell** – in this case `A1` will hold the result of an `EXPAND` call.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write formula to A1 – we’ll expand B1:C2 into a 4‑by‑5 array later
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";
```

**Why this matters:** Writing the formula directly from code means you can generate complex spreadsheets on the fly without ever opening Excel. It also sets the stage for the next step where we **convert range to array**.

---

## Step 2: Convert Range to Array with EXPAND

`EXPAND` is Excel’s way of turning a small range into a larger matrix. By placing the formula in `A1`, Excel will spill a 4 × 5 block starting at that cell. From C#, we don’t have to manually copy values – the library will do the heavy lifting when we call `Calculate`.

```csharp
        // The EXPAND formula will spill into A1:E4 (4 rows × 5 columns)
        // No extra code needed – the workbook will handle the spill.
```

**How to use lambda:** Not yet, but stay tuned. First we need the data in the sheet, then we’ll reduce it with a lambda.

---

## Step 3: Use LAMBDA Inside REDUCE – The Core of “How to Use Lambda”

Excel 365 introduced `REDUCE`, which accepts an **initial value**, a **range**, and a **LAMBDA** that tells it how to combine each element. From C# we simply assign the formula string; the lambda lives inside the Excel formula, not in C# code.

```csharp
        // Reduce the spilled array by summing all its values.
        // This demonstrates how to use lambda inside REDUCE.
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";
```

**Explanation:**  
- `0` is the starting accumulator (`acc`).  
- `A1:D4` is the range we want to process (the first four columns of the spill).  
- `LAMBDA(acc, x, acc + x)` tells Excel to add each cell (`x`) to the accumulator.  

That’s the essence of **how to use lambda** for aggregation in a spreadsheet context.

---

## Step 4: Calculate Cotangent in Excel – From Degrees to Hyperbolic

If you need trigonometric results, Excel’s `COT` and `COTH` functions are a breeze. We’ll place them in `G1` and `G2` respectively.

```csharp
        // Demonstrate trigonometric functions – cotangent and hyperbolic cotangent
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected result: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";      // Hyperbolic cotangent of 1
```

**Why this is handy:** Knowing **calculate cotangent in Excel** can save you from writing custom math code, especially when the workbook will be shared with non‑developers.

---

## Step 5: Force Calculation and Retrieve the Expanded Array

Now we tell the workbook to evaluate every formula, then pull the spilled array out of `A1`. This is where we **display array in console**.

```csharp
        // Force calculation of all formulas
        workbook.Calculate();

        // Retrieve the spilled array from A1 as a 2‑D object
        var expanded = worksheet.Cells["A1"].Value;

        // Pretty‑print the 2‑D array to the console
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show the result of the REDUCE lambda
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**What you’ll see:**  
- A nicely formatted 4 × 5 matrix printed line‑by‑line.  
- The sum computed by the `REDUCE` lambda.  
- The two cotangent values.

That completes the flow from **write formula to cell** all the way to **display array in console**.

---

## Full Working Example (Copy‑Paste Ready)

Below is the entire program you can drop into a console app. Remember to add the `Aspose.Cells` NuGet package first (`dotnet add package Aspose.Cells`).

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Write EXPAND formula (convert range to array)
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";

        // Step 3: Use REDUCE with LAMBDA (how to use lambda)
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";

        // Step 4: Calculate cotangent values (calculate cotangent in excel)
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";

        // Step 5: Force calculation
        workbook.Calculate();

        // Step 6: Retrieve and display the expanded array (display array in console)
        var expanded = worksheet.Cells["A1"].Value;
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show REDUCE result
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Expected console output (values will vary based on the default contents of B1:C2, which are 0 by default):**

```
Expanded array from A1 (4×5):
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0

Sum of A1:D4 (via REDUCE lambda): 0
Cotangent of π/4: 1
Hyperbolic cotangent of 1: 1.31303528549933
```

Feel free to populate `B1:C2` with your own numbers before running – the matrix will reflect those values.

---

## Pro Tips & Common Pitfalls

- **Pro tip:** If you need the spilled range to start elsewhere, just change the target cell (`A1`). The `EXPAND` function respects the anchor.
- **Watch out for:** Empty cells in the source range become `0` in the spilled array, which can affect your `REDUCE` sum.
- **Edge case:** When the workbook contains formulas that depend on volatile functions (e.g., `NOW()`), call `workbook.Calculate()` after setting all formulas to ensure everything is up‑to‑date.
- **Performance note:** For huge spills, consider limiting the size in the `EXPAND` call; otherwise you might allocate more memory than needed.
- **Compatibility:** The `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}