---
category: general
date: 2026-07-03
description: Create Excel workbook in C# and set cell formula, calculate pi formula,
  then export Excel with formulas. Follow this quick, practical tutorial.
draft: false
keywords:
- create excel workbook
- set cell formula
- calculate pi formula
- how to set formula
- export excel with formulas
language: en
og_description: Create Excel workbook in C# and set cell formula, calculate pi formula,
  then export Excel with formulas. Learn the full process in minutes.
og_title: Create Excel Workbook with Formulas – Complete Guide
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Create Excel workbook in C# and set cell formula, calculate pi formula,
    then export Excel with formulas. Follow this quick, practical tutorial.
  headline: Create Excel Workbook with Formulas – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create Excel workbook in C# and set cell formula, calculate pi formula,
    then export Excel with formulas. Follow this quick, practical tutorial.
  name: Create Excel Workbook with Formulas – Full Step‑by‑Step Guide
  steps:
  - name: Does the workbook keep the formulas after saving?
    text: Yes. Aspose.Cells writes both the formula string (`Formula`) and the evaluated
      value (`Value`). When you open the file, Excel will re‑evaluate the formulas
      on load, but the saved formula remains intact—perfect for later edits.
  - name: What if I need to set a formula that references another sheet?
    text: Just use the typical Excel notation, e.g., `=Sheet2!C3*2`. Aspose.Cells
      parses it correctly as long as the target sheet exists.
  - name: How to handle large data sets without blowing memory?
    text: Use `WorkbookDesigner` or stream the workbook directly to a `MemoryStream`
      and then to a response object. This avoids loading the entire file into RAM
      when you only need to push it to a client.
  - name: Can I protect the sheet while still allowing formula evaluation?
    text: 'Absolutely. After setting formulas, call:'
  type: HowTo
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Create Excel Workbook with Formulas – Full Step‑by‑Step Guide
url: /net/excel-formulas-and-calculation-options/create-excel-workbook-with-formulas-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel Workbook with Formulas – Complete Guide

Ever wondered how to **create excel workbook** programmatically and have the formulas stay alive when you open the file? You're not the only one. Whether you're building a reporting engine, an invoice generator, or just automating a daily dump, being able to set cell formula, calculate pi formula, and then **export excel with formulas** saves you hours of manual tweaking.

In this tutorial we’ll walk through a hands‑on example using the Aspose.Cells for .NET library. We'll start by creating the workbook, then show you **how to set formula** for dynamic arrays, compute a trigonometric value with π, recalculate the sheet, and finally save the file so Excel shows the results instantly.

## What You’ll Need

- .NET 6 (or any recent .NET runtime) – the code compiles with .NET Core as well.  
- Aspose.Cells for .NET – a powerful, license‑free NuGet package for our demo (`Install-Package Aspose.Cells`).  
- An IDE you like (Visual Studio, Rider, VS Code – pick whatever feels comfy).  

No other dependencies. If you’ve never touched Aspose.Cells before, don’t worry; the API is straightforward and the snippets below are ready to copy‑paste.

## Create Excel Workbook – Initial Setup

First things first. We need a fresh workbook object that will host our worksheets. Think of it as an empty Excel file waiting for content.

```csharp
using Aspose.Cells;

 // Step 1: Create a workbook and obtain the first worksheet
Workbook workbook = new Workbook();               // <-- creates a new .xlsx in memory
Worksheet ws = workbook.Worksheets[0];           // the default first sheet
```

*Why this matters:* The `Workbook` class is the entry point for every operation—without it you can’t add sheets, set formulas, or export anything. By grabbing `Worksheets[0]` we get a reference to the default tab named “Sheet1”.

> **Pro tip:** If you need multiple sheets, just call `workbook.Worksheets.Add()` and keep the returned `Worksheet` reference.

## Set Cell Formula – Dynamic Array Expansion

Now let’s **set cell formula** that expands a range dynamically. The `EXPAND` function is a new Excel 365 feature that spills the source array into a specified size.

```csharp
// Step 2: Apply a dynamic array formula that expands A2:A5 to 4 rows, 1 column
ws.Cells["A1"].Formula = "=EXPAND(A2:A5,4,1)";
```

What happens under the hood?  

- `A2:A5` is the source range (four cells).  
- The second argument (`4`) tells Excel to create **4 rows**.  
- The third argument (`1`) forces **1 column**.  

When you open the saved file, cells A1:A4 will automatically contain the values from A2:A5. If you later change any of those source cells, the spill updates instantly—no macro required.

> **Edge case:** `EXPAND` works only in Excel versions that support dynamic arrays (Office 365, Excel 2021+). Older versions will display a `#NAME?` error.

## Calculate Pi Formula – Trigonometric Example

Next we’ll demonstrate **calculate pi formula** by using the built‑in `PI()` function together with `COT`. This showcases how any Excel‑compatible expression can be injected from code.

```csharp
// Step 3: Apply a trigonometric formula to compute the cotangent of π/4
ws.Cells["B1"].Formula = "=COT(PI()/4)";
```

Why `COT(PI()/4)`? The cotangent of 45° (π/4 radians) equals 1, so the cell should show **1** after calculation. It’s a neat sanity check—if you see anything else, the recalculation step probably didn’t run.

## Recalculate the Worksheet – Ensuring Formulas Resolve

Aspose.Cells doesn’t automatically evaluate formulas when you set them. You must explicitly trigger a calculation pass.

```csharp
// Step 4: Recalculate the worksheet so the formulas are evaluated
ws.CalculateFormula();
```

Calling `CalculateFormula()` walks through every cell that contains a formula, computes the result, and stores it in the cell’s `Value` property. This step guarantees that the workbook you save already contains the computed numbers, which is handy when you later open the file in a head‑less environment (e.g., a reporting service).

## Export Excel with Formulas – Saving the File

Finally, we **export excel with formulas** to a physical file. The format is standard `.xlsx`, fully compatible with any modern spreadsheet program.

```csharp
// Step 5: Save the workbook to view the results
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);
```

Open `output.xlsx` in Excel and you’ll see:

| A | B |
|---|---|
| (value from A2) | 1 |
| (value from A3) |   |
| (value from A4) |   |
| (value from A5) |   |

Cell **B1** shows **1**, confirming our `COT(PI()/4)` calculation. Cells **A1:A4** display the spilled values from **A2:A5** thanks to the `EXPAND` formula.

> **Quick verification:** Change the value in `A2` to `99`, re‑run the program, and open the file again. The spill in column A should now reflect `99` at the top of the range.

## Common Questions & Gotchas

### Does the workbook keep the formulas after saving?

Yes. Aspose.Cells writes both the formula string (`Formula`) and the evaluated value (`Value`). When you open the file, Excel will re‑evaluate the formulas on load, but the saved formula remains intact—perfect for later edits.

### What if I need to set a formula that references another sheet?

Just use the typical Excel notation, e.g., `=Sheet2!C3*2`. Aspose.Cells parses it correctly as long as the target sheet exists.

### How to handle large data sets without blowing memory?

Use `WorkbookDesigner` or stream the workbook directly to a `MemoryStream` and then to a response object. This avoids loading the entire file into RAM when you only need to push it to a client.

### Can I protect the sheet while still allowing formula evaluation?

Absolutely. After setting formulas, call:

```csharp
ws.Protect(ProtectionType.All);
```

The protection flag doesn’t stop calculation; it just restricts user edits.

## Full Working Example

Below is the complete, ready‑to‑run program. Paste it into a new console project, add the Aspose.Cells NuGet package, and hit **F5**.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelFormulaDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook and grab the first worksheet
            Workbook workbook = new Workbook();
            Worksheet ws = workbook.Worksheets[0];

            // Populate source cells A2:A5 so the EXPAND formula has something to spill
            ws.Cells["A2"].PutValue(10);
            ws.Cells["A3"].PutValue(20);
            ws.Cells["A4"].PutValue(30);
            ws.Cells["A5"].PutValue(40);

            // 2️⃣ Set a dynamic array formula in A1
            ws.Cells["A1"].Formula = "=EXPAND(A2:A5,4,1)";

            // 3️⃣ Compute cotangent of π/4 in B1
            ws.Cells["B1"].Formula = "=COT(PI()/4)";

            // 4️⃣ Force calculation so values are stored
            ws.CalculateFormula();

            // 5️⃣ Save the workbook – this exports the Excel with formulas intact
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to: {outputPath}");
        }
    }
}
```

**Expected output** (when you open `output.xlsx`):

- **A1:A4** contain `10, 20, 30, 40` respectively (the spill from A2:A5).  
- **B1** displays `1` (the result of `COT(PI()/4)`).  

Everything else stays blank, just as we programmed it.

## Wrap‑Up

We’ve just **created excel workbook**, **set cell formula** for a dynamic array, **calculated pi formula** with a trigonometric function, forced a recalculation, and finally **export excel with formulas** to disk. The whole flow fits into a handful of lines, yet it demonstrates the core capabilities you’ll need for real‑world automation.

What’s next? Try swapping `EXPAND` for `FILTER`, embed images via `Picture` objects, or generate charts on the fly. The Aspose.Cells API covers everything from simple cell writes to complex pivot tables, so the sky’s the limit.

Feel free to experiment, break things, and then come back with your own tweaks. If you hit a snag, drop a comment below—happy coding! 

![Create Excel workbook example screenshot](excel-workbook-example.png "Create Excel workbook example showing formulas in A1 and B1")


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Excel Automation with Aspose.Cells .NET&#58; Mastering Workbook & Formula Calculations](/cells/english/net/formulas-functions/excel-automation-aspose-cells-net-workbook-formulas/)
- [Excel Automation with Aspose.Cells .NET&#58; Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}