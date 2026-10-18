---
category: general
date: 2026-02-15
description: How to use WRAPCOLS to create a two column layout, add a formula and
  generate a sequence array in C# worksheets – step‑by‑step guide.
draft: false
keywords:
- how to use wrapcols
- create two column layout
- how to add formula
- how to create columns
- generate sequence array
language: en
og_description: How to use WRAPCOLS to build a two‑column layout, add formulas and
  generate a sequence array in a C# worksheet – complete guide.
og_title: 'How to Use WRAPCOLS: Two‑Column Layout in C#'
tags:
- CSharp
- ExcelAutomation
- WorksheetFormula
title: 'How to Use WRAPCOLS: Create a Two‑Column Layout in C#'
url: /net/row-and-column-management/how-to-use-wrapcols-create-a-two-column-layout-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use WRAPCOLS: Create a Two‑Column Layout in C#

Ever wondered **how to use WRAPCOLS** when you need a quick two‑column view inside an Excel‑style worksheet? You’re not alone. Many developers hit a wall when they try to split a generated list into neat columns without writing a loop for each cell. The good news? With the `WRAPCOLS` function you can drop a single formula into `A1` and let Excel (or a compatible engine) do the heavy lifting.

In this tutorial we’ll walk through **how to add formula** that creates a **create two column layout**, show you **how to create columns** dynamically, and even **generate sequence array** values on the fly. By the end you’ll have a fully runnable C# snippet that you can paste into your project, run, and see a tidy two‑column block appear instantly.

## What You’ll Learn

- The purpose of `WRAPCOLS` and why it’s a better alternative to manual looping.  
- How to **add a formula** to a worksheet cell using C#.  
- How to generate a sequence array with `SEQUENCE` and feed it into `WRAPCOLS`.  
- Tips for recalculating the sheet so the formula resolves immediately.  
- Edge‑case handling (e.g., empty worksheets, custom column counts).

No external libraries beyond a standard Excel‑processing package are required – we’ll use **ClosedXML** for its straightforward API, but the concepts translate to EPPlus, SpreadsheetGear, or even Google Sheets via its API.

---

## Prerequisites

- .NET 6.0 or later (the code compiles on .NET Core and .NET Framework).  
- A reference to **ClosedXML** (`dotnet add package ClosedXML`).  
- Basic C# knowledge – you should be comfortable with `using` statements and object initialization.  

If you already have a workbook open, you can skip the file‑creation part and jump straight to the formula section.

---

## Step 1: Set Up the Worksheet (How to Create Columns)

First we need a `Worksheet` object to work with. In ClosedXML you obtain it from a `XLWorkbook`. The snippet below creates a new workbook, adds a sheet called *Demo*, and grabs a reference named `worksheet` for clarity.

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // Create a fresh workbook and add a worksheet named "Demo"
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");

            // Rename for clarity – this is the worksheet we’ll manipulate
            var worksheet = ws;   // <-- same object, just a clearer name

            // --------------------------------------------------------------
            // Next step: write the WRAPCOLS formula
            // --------------------------------------------------------------
```

> **Why rename?**  
> Keeping the variable name short (`worksheet`) makes the later code easier to read, especially when you chain multiple operations. It also mirrors the naming style you’ll see in most documentation, reducing cognitive load.

---

## Step 2: Write the Formula (How to Add Formula + Generate Sequence Array)

Now comes the magic line. We’ll place a formula in cell **A1** that does two things:

1. **Generate a sequence array** of six numbers (`SEQUENCE(6)` → 1,2,3,4,5,6).  
2. **Wrap those numbers into two columns** (`WRAPCOLS(..., 2)`).

```csharp
            // Write the WRAPCOLS formula into A1
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // --------------------------------------------------------------
            // Finally, force the engine to evaluate the formula
            // --------------------------------------------------------------
```

> **What’s happening?**  
> `SEQUENCE(6)` creates a vertical array `{1;2;3;4;5;6}`. `WRAPCOLS` then takes that array and “wraps” it into the specified number of columns—in this case **2**. The result is a 3‑row × 2‑column block that looks like:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

If you change the second argument to **3**, you’d get a three‑column layout instead. That’s the core of **how to create columns** on the fly without manual loops.

---

## Step 3: Recalculate the Worksheet (Ensuring the Formula Evaluates)

ClosedXML won’t automatically evaluate formulas when you write them. You need to call `Calculate()` on the workbook (or on the specific worksheet) to force evaluation.

```csharp
            // Recalculate so the formula is evaluated immediately
            worksheet.Calculate();

            // Optional: save the workbook to inspect the result
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

> **Pro tip:** If you’re working with large workbooks, call `Calculate()` only on the sheets that actually changed. This saves memory and speeds up processing.

When you open `WrapColsDemo.xlsx` you’ll see the two‑column layout neatly populated in **A1:B3**. No additional code was required to loop through rows or columns – `WRAPCOLS` handled everything.

---

## Step 4: Verify the Output (What to Expect)

After running the program, open the generated file. You should see:

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

If the numbers appear vertically (i.e., all in column A), double‑check that you called `worksheet.Calculate()` **after** setting the formula. Some engines also need `workbook.Calculate()`; the snippet above works for ClosedXML’s built‑in evaluator.

---

## Common Variations & Edge Cases

### Changing the Number of Columns

To **create two column layout** with a different row count, simply adjust the `SEQUENCE` size or the second argument of `WRAPCOLS`:

```csharp
worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(12), 3)";
```

This produces a 4‑row × 3‑column block (12 numbers split across three columns).

### Using a Dynamic Column Count

If your column count comes from a variable, embed it with string interpolation:

```csharp
int colCount = 4;
worksheet.Cell("A1").FormulaA1 = $"=WRAPCOLS(SEQUENCE(8), {colCount})";
```

Now you’ve **how to add formula** that adapts at runtime.

### Empty Worksheets

If the worksheet is empty, `Calculate()` still works – the formula will populate cells starting at A1. However, if you later delete rows/columns that intersect the output range, you might see `#REF!` errors. To avoid that, clear the target range first:

```csharp
worksheet.Range("A1:Z100").Clear(); // wipes any leftovers
```

### Compatibility

`WRAPCOLS` and `SEQUENCE` are part of Excel’s **Dynamic Array** functions, introduced in Office 365. If you target older Excel versions, the functions won’t exist, and you’ll need a manual loop. ClosedXML’s evaluator mirrors the latest Excel behavior, so it’s safe for modern environments.

---

## Full Working Example (Copy‑Paste Ready)

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook & worksheet
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");
            var worksheet = ws;   // clearer name

            // 2️⃣ Write WRAPCOLS formula that generates a sequence array
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // 3️⃣ Force calculation so the formula resolves immediately
            worksheet.Calculate();

            // 4️⃣ Save the file (optional, but handy for verification)
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

**Expected result:** Opening *WrapColsDemo.xlsx* shows a tidy two‑column layout with numbers 1‑6 arranged as described earlier.

---

## Conclusion

We’ve covered **how to use WRAPCOLS** to **create a two column layout**, demonstrated **how to add formula** programmatically, and saw how `SEQUENCE` lets you **generate sequence array** values without a loop. By leveraging Excel’s dynamic array functions from C#, you can keep your code concise, readable, and maintainable.

Next, you might explore:

- **Creating dynamic row counts** with `ROWS` or `COUNTA`.  
- **Styling the output** (borders, number formats) using ClosedXML’s styling API.  
- **Exporting to CSV** after the layout is built, for downstream processing.

Give it a try, tweak the column count, and see how quickly you can prototype complex spreadsheets. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}