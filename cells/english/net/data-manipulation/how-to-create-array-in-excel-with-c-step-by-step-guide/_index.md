---
category: general
date: 2026-02-09
description: How to create array in Excel with C# explained in minutes – learn to
  generate sequence numbers, use COT, and save workbook as XLSX.
draft: false
keywords:
- how to create array
- create excel workbook c#
- generate sequence numbers
- save workbook as xlsx
- how to use cot
language: en
og_description: How to create array in Excel with C# is covered step-by-step, including
  generating sequence numbers, using COT, and saving the workbook as XLSX.
og_title: How to create array in Excel with C# – Quick Guide
tags:
- C#
- Excel
- Aspose.Cells
title: How to create array in Excel with C# – Step-by-Step Guide
url: /net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create array in Excel with C# – Step-by-Step Guide

Ever wondered **how to create array** in Excel using C# without spending hours digging through docs? You're not alone. Many developers hit a wall when they need a dynamic spill range, a quick trigonometric value, or simply a clean XLSX file saved to disk. In this tutorial we’ll solve that problem right away—by building a tiny workbook that writes an expanding array formula, plugs in a cotangent calculation, and saves everything as an XLSX file.  

We'll also sprinkle in a few extra tricks: generating sequence numbers, mastering the `COT` function, and making sure the file lands where you want it. By the end you’ll have a reusable snippet you can drop into any .NET project. No fluff, just code that works.

> **Pro tip:** The example uses the popular **Aspose.Cells** library, but the concepts translate to other Excel‑automation packages (EPPlus, ClosedXML) with only minor changes.

---

## What You’ll Need

- **.NET 6** or later (the code compiles on .NET Framework 4.7+ as well)  
- **Aspose.Cells for .NET** – you can grab it from NuGet (`Install-Package Aspose.Cells`)  
- A text editor or IDE (Visual Studio, Rider, VS Code…)  
- Write permission to a folder where the output file will be saved  

That’s it—no extra configuration, no COM interop, just a clean managed assembly.

---

## Step 1: How to create array in Excel – Initialize the Workbook

The very first thing when you want **how to create array** in an Excel sheet is to spin up a workbook object. Think of the workbook as the blank canvas; the worksheet is where you’ll paint your formulas.

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // <- fresh workbook
        Worksheet worksheet = workbook.Worksheets[0];    // first (and only) sheet

        // The rest of the steps follow...
```

Why use `Workbook()` without parameters? It gives you an in‑memory workbook with a default sheet, which is perfect for quick, programmatic tasks. If you need to open an existing file, simply pass the file path to the constructor.

---

## Step 2: Generate sequence numbers with EXPAND and SEQUENCE

Now that we have a sheet, let’s answer the **generate sequence numbers** part of the puzzle. Excel’s new dynamic array functions (`SEQUENCE`, `EXPAND`) let us create a 3‑row vertical list and automatically spill it into a 3 × 5 range.

```csharp
        // Write a dynamic array formula that expands a 3‑row sequence into a 3×5 spill range
        // EXPAND pads the result to 5 columns, SEQUENCE generates numbers 1‑3 vertically
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

**What’s happening here?**  
- `SEQUENCE(3,1,1,1)` → produces a vertical array `{1;2;3}`.  
- `EXPAND(...,5,1)` → takes that three‑row column and stretches it to five columns, filling the extra cells with blanks.  

When you open the resulting `output.xlsx`, you’ll see a 3 × 5 block starting at **A1** where the first column contains 1, 2, 3 and the remaining four columns are empty. This technique is the backbone of **how to create array**‑style spill ranges without manually writing each cell.

---

## Step 3: How to use COT – Adding a Trigonometric Formula

If you’re also curious about **how to use cot** inside an Excel formula, the `COT` function is a handy way to get the cotangent of an angle expressed in radians. Let’s calculate `cot(π/4)`, which should evaluate to **1**.

```csharp
        // Write a simple trigonometric formula that calculates cotangent of 45° (π/4)
        // COT(π/4) evaluates to 1
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

Notice we used `PI()` to get the radian value of 180°, then divided by 4 to reach 45°. Excel does the heavy lifting, and the cell **B1** will show `1` once the workbook is opened. This demonstrates **how to use cot** for quick engineering or finance calculations without pulling in a separate math library.

---

## Step 4: Save workbook as XLSX – Persisting the File

All the fun of creating an array and inserting formulas is wasted if you never write the file to disk. Here’s the straightforward way to **save workbook as xlsx** using Aspose.Cells:

```csharp
        // Save the workbook to verify the formulas (optional)
        string outputPath = @"C:\Temp\output.xlsx";   // adjust to your folder
        workbook.Save(outputPath, SaveFormat.Xlsx);

        // Let the user know we’re done
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Why specify `SaveFormat.Xlsx`? It guarantees the modern OpenXML format, which is universally readable (Excel, LibreOffice, Google Sheets). If you need an older `.xls` file, just swap the enum.

---

## Full Working Example (All Steps Combined)

Below is the complete, ready‑to‑run program. Copy‑paste it into a console project, restore the Aspose.Cells NuGet package, and hit **F5**.

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Create a dynamic spill range (how to create array)
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";

        // Step 3: Calculate cotangent (how to use cot)
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";

        // Step 4: Persist the file (save workbook as xlsx)
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Expected outcome** after opening `output.xlsx`:

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 1 |   |   |   |
| 2 |   |   |   |   |
| 3 |   |   |   |   |

- Column A shows the numbers 1‑3 generated by `SEQUENCE`.  
- Column B contains the value **1** from the `COT` formula.  
- Columns C‑E are blank, illustrating the padding effect of `EXPAND`.

---

## Common Questions & Edge Cases

### What if I need more rows or columns?

Just tweak the arguments of `SEQUENCE` and `EXPAND`.  
- `SEQUENCE(10,2,5,2)` would give a 10‑row × 2‑column matrix starting at 5 and incrementing by 2.  
- `EXPAND(...,10,5)` would pad the result to 10 columns and 5 rows.

### Does this work with older Excel versions?

Dynamic array functions (`SEQUENCE`, `EXPAND`) require Excel 365 or 2019+. For legacy files, you can fall back to classic formulas or write values directly via `Cells[row, col].PutValue(value)`.

### Can I write the formula in R1C1 style?

Absolutely. Replace `A1` with `Cells[0, 0]` and use `FormulaR1C1` property:

```csharp
worksheet.Cells[0, 0].FormulaR1C1 = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

### What about culture‑specific decimal separators?

Aspose.Cells respects the workbook’s locale. If you need a specific culture, set `workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");` before writing formulas.

---

## Visual Summary

![how to create array in Excel using C#](/images/how-to-create-array-excel-csharp.png "how to create array in Excel using C#")

*The screenshot shows the final spill range and the cotangent result.*

---

## Conclusion

There you have it—**how to create array** in Excel with C# from scratch, generate sequence numbers, harness the `COT` function, and **save workbook as XLSX** in a single, tidy program. The key takeaways are:

1. Use `Workbook` and `Worksheet` objects to start your Excel automation.  
2. Leverage dynamic array functions (`SEQUENCE`, `EXPAND`) for flexible spill ranges.  
3. Plug in trigonometric functions like `COT` for quick math without extra libraries.  
4. Persist the result with `SaveFormat.Xlsx` to get a universally readable file.

Ready for the next step? Try swapping `COT(PI()/4)`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}