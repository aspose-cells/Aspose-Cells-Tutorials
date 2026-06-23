---
category: general
date: 2026-03-30
description: Create Excel workbook C# using Aspose.Cells. Learn to apply lambda function
  Excel, sequence function Excel, expand array Excel, and save workbook as xlsx.
draft: false
keywords:
- create excel workbook c#
- lambda function excel
- save workbook as xlsx
- sequence function excel
- expand array excel
language: en
og_description: Create Excel workbook C# quickly. This guide shows how to use lambda
  function Excel, sequence function Excel, expand array Excel, and save workbook as
  xlsx.
og_title: Create Excel Workbook C# – Lambda, SEQUENCE & EXPAND Guide
tags:
- Aspose.Cells
- C#
- Excel automation
title: Create Excel Workbook C# – Lambda, SEQUENCE & EXPAND Guide
url: /net/formulas-functions/create-excel-workbook-c-lambda-sequence-expand-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel Workbook C# – Lambda, SEQUENCE & EXPAND Guide

Ever needed to **create Excel workbook C#** for an automated report, but weren’t sure which API calls to use? You’re not alone—many developers hit the same wall when they first dive into programmatic Excel generation. In this guide you’ll see a complete, runnable example that covers everything from the new **SEQUENCE function Excel** to the powerful **LAMBDA function Excel**, and even how to **expand array Excel** results.  

We’ll also show you the exact steps to **save workbook as xlsx** so you can hand the file off to anyone who uses Excel. By the end of this tutorial you’ll have a solid, production‑ready snippet that you can drop into any .NET project. No vague “see the docs” links—just code that works today.

## What You’ll Need

- **.NET 6.0 or later** – the example targets .NET 6, but any recent version works.  
- **Aspose.Cells for .NET** – install via NuGet (`Install-Package Aspose.Cells`).  
- A basic understanding of C# syntax (variables, objects, and lambda expressions).  
- An IDE you’re comfortable with (Visual Studio, Rider, or VS Code).  

That’s it. No extra COM interop, no Office installed on the server—Aspose.Cells handles everything in memory.

## Create Excel Workbook C# – Step‑by‑Step Implementation

Below we break the process into bite‑size steps. Each step has a clear header, a short code excerpt, and an explanation of **why** we’re doing it. Feel free to copy the full block at the end and run it as a console app.

### Step 1 – Initialize a New Workbook

First things first: we need a blank workbook object that represents the Excel file in memory.

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // empty workbook
Worksheet sheet = workbook.Worksheets[0];         // default first sheet
```

*Why this matters:* `Workbook` is the entry point for all Aspose.Cells operations. By grabbing the first `Worksheet` we get a canvas where we can write formulas, values, or formatting.  

> **Pro tip:** If you need multiple sheets, just call `workbook.Worksheets.Add()` and keep a reference to each.

### Step 2 – Use the SEQUENCE function Excel to Generate Data

The **sequence function excel** creates a dynamic array of numbers without any VBA. We’ll place it in cell `A1` and let Excel expand it automatically.

```csharp
// Step 2: Generate a 5‑row, 1‑column array from a SEQUENCE
sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)"; // 1..3 padded with blanks
```

*Why this matters:* `SEQUENCE(3)` yields `[1,2,3]`. Wrapping it with `EXPAND` forces the result into a 5‑row range, filling the extra rows with blanks. This demonstrates both **sequence function excel** and **expand array excel** in one go.

### Step 3 – Aggregate Numbers with LAMBDA function Excel

Now let’s showcase the **lambda function excel** capability. We’ll sum the numbers 1‑5 using the new `REDUCE` function, which internally relies on a lambda.

```csharp
// Step 3: Aggregate a sequence (sum 1..5) using REDUCE/LAMBDA
sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))"; // result = 15
```

*Why this matters:* `REDUCE` iterates over the array produced by `SEQUENCE(5)`, feeding each element (`b`) into the lambda alongside the accumulator (`a`). The lambda `a+b` adds them up, leaving `15` in `B1`. This is a clean, formula‑only way to perform reductions without looping in C#.

### Step 4 – Apply Trigonometric Functions Directly in Cells

Excel’s built‑in math functions are handy for quick calculations. We’ll put a cotangent and a hyperbolic cotangent in adjacent cells.

```csharp
// Step 4: Trigonometric functions directly in Excel cells
sheet["C1"].Formula = "COT(PI()/4)";   // evaluates to 1
sheet["D1"].Formula = "COTH(1)";      // hyperbolic cotangent of 1
```

*Why this matters:* Demonstrates that you can mix classic math functions with the newer dynamic‑array formulas. No need to compute these values in C# unless you have a specific performance reason.

### Step 5 – Calculate All Formulas

Aspose.Cells doesn’t automatically evaluate formulas when you set them. You have to ask it to calculate.

```csharp
// Step 5: Force calculation so that cells store the results
workbook.CalculateFormula();
```

*Why this matters:* After this call, each cell’s `Value` property contains the evaluated result, ready to be saved or read back.

### Step 6 – Save the Workbook as Xlsx

Finally, we persist the workbook to disk using the **save workbook as xlsx** pattern.

```csharp
// Step 6: Save the workbook to an Excel file (XLSX format)
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "NewFunctions.xlsx");

workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

*Why this matters:* The `Save` method automatically detects the file extension. By using “.xlsx” we ensure the file is compatible with modern Excel versions. The path points to the desktop for easy access during testing.

### Full Working Example

Below is the complete program you can paste into a new console project. It includes all the steps above, plus a tiny verification block that prints the calculated values to the console.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Initialize workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // SEQUENCE + EXPAND
        sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)";

        // REDUCE with LAMBDA
        sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))";

        // Trig functions
        sheet["C1"].Formula = "COT(PI()/4)";
        sheet["D1"].Formula = "COTH(1)";

        // Calculate formulas
        workbook.CalculateFormula();

        // Verify results (optional)
        Console.WriteLine("A1‑A5 (expanded SEQUENCE):");
        for (int i = 0; i < 5; i++)
        {
            Console.WriteLine($"  Row {i + 1}: {sheet.Cells[i, 0].Value ?? "blank"}");
        }
        Console.WriteLine($"B1 (sum 1‑5): {sheet["B1"].Value}");
        Console.WriteLine($"C1 (cot(π/4)): {sheet["C1"].Value}");
        Console.WriteLine($"D1 (coth(1)): {sheet["D1"].Value}");

        // Save workbook
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "NewFunctions.xlsx");
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

**Expected output in the console**

```
A1‑A5 (expanded SEQUENCE):
  Row 1: 1
  Row 2: 2
  Row 3: 3
  Row 4: blank
  Row 5: blank
B1 (sum 1‑5): 15
C1 (cot(π/4)): 1
D1 (coth(1)): 1.31303528549933
Workbook saved to: C:\Users\YourName\Desktop\NewFunctions.xlsx
```

And when you open *NewFunctions.xlsx* you’ll see the same numbers laid out in the first four columns.

![create excel workbook c# screenshot of the resulting spreadsheet](/images/create-excel-workbook-csharp.png)

## Edge Cases, Tips, and Common Questions

- **What if I need more than one sheet?**  
  Just call `workbook.Worksheets.Add()` and repeat the formula assignments on each new `Worksheet` object.  

- **Can I use older Excel versions?**  
  The dynamic‑array functions (`SEQUENCE`, `EXPAND`, `REDUCE`) require Excel 365 or Excel 2021+. If you target older versions, stick to classic formulas or compute the values in C# before writing them.  

- **Performance concerns?**  
  For thousands of rows, setting formulas on a range and then calling `CalculateFormula` is usually faster than looping and assigning values one‑by‑one.  

- **Saving to a stream instead of a file?**  
  `work

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}