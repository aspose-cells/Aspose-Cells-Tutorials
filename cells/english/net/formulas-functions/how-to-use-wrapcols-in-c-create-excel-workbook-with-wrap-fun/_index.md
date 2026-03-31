---
category: general
date: 2026-03-30
description: Learn how to use WRAPCOLS in C# to create an Excel workbook, add data
  to Excel, and force formula calculation while also using WRAPROWS.
draft: false
keywords:
- how to use wrapcols
- create excel workbook c#
- add data to excel
- force formula calculation
- how to use wraprows
language: en
og_description: Discover how to use WRAPCOLS in C# to build an Excel workbook, add
  data, force formula calculation and leverage WRAPROWS for array formulas.
og_title: How to Use WRAPCOLS in C# – Complete Guide
tags:
- Aspose.Cells
- C#
- Excel Automation
title: How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions
url: /net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions

Ever wondered **how to use WRAPCOLS** when you’re automating Excel with C#? You’re not alone—many developers hit a wall when they need to turn a horizontal range into a vertical array without writing a ton of code. The good news is that Aspose.Cells makes it a piece of cake.

In this tutorial we’ll walk through a complete, runnable example that shows **how to use WRAPCOLS**, how to **create Excel workbook C#**‑style, how to **add data to Excel**, and even how to **force formula calculation** so the results appear instantly. We’ll also sprinkle in **how to use WRAPROWS** for the opposite transformation. By the end you’ll have a ready‑to‑run program and a clear understanding of why each step matters.

---

![How to use WRAPCOLS in C# example](alt="Screenshot showing Excel workbook after using WRAPCOLS in C#")

## What This Guide Covers

* Setting up a fresh workbook with Aspose.Cells.
* Populating cells programmatically (**add data to Excel**).
* Applying the `WRAPCOLS` function to turn a row into a column.
* Using `WRAPROWS` to flip a column back into a row (**how to use wraprows**).
* Forcing the engine to evaluate formulas right away (**force formula calculation**).
* Saving the file and checking the output.

No external documentation required—everything you need lives right here.

---

## How to Use WRAPCOLS in C# – Step‑by‑Step Implementation

Below is the full source file. Feel free to copy‑paste it into a new console project, add the Aspose.Cells NuGet package, and hit **F5**.

```csharp
// ------------------------------------------------------------
// How to Use WRAPCOLS in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.Cells;

namespace WrapFunctionsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a fresh workbook (this is how we **create excel workbook c#** style)
            Workbook workbook = new Workbook();

            // 2️⃣ Grab the first worksheet – it's created by default
            Worksheet sheet = workbook.Worksheets[0];

            // 3️⃣ **Add data to Excel**: place two numbers side‑by‑side
            sheet.Cells["A1"].PutValue(1);   // first value
            sheet.Cells["B1"].PutValue(2);   // second value

            // 4️⃣ **How to use WRAPCOLS** – turn the horizontal range A1:B1 into a vertical array
            //    The second argument (1) tells WRAPCOLS to create 1 column per element.
            sheet["C1"].Formula = "WRAPCOLS(A1:B1, 1)";

            // 5️⃣ **How to use WRAPROWS** – the opposite; turn the same range into a horizontal array
            //    Here we ask for 2 rows per element, which produces a single row with both values.
            sheet["C2"].Formula = "WRAPROWS(A1:B1, 2)";

            // 6️⃣ **Force formula calculation** so the workbook reflects the results immediately
            workbook.CalculateFormula();

            // 7️⃣ Save the workbook to disk – change the path to a folder you own
            string outputPath = @"WrapFunctions.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
            Console.WriteLine("Check cells C1 and C2 for the WRAPCOLS / WRAPROWS results.");
        }
    }
}
```

### Why Each Line Matters

| Step | Explanation |
|------|-------------|
| **1️⃣ Create a fresh workbook** | This is the foundation. Aspose.Cells treats a `Workbook` object as the entire Excel file, so you’re effectively **creating an Excel workbook C#** style. |
| **2️⃣ Grab the first worksheet** | A new workbook always contains at least one worksheet (`Worksheets[0]`). Accessing it early avoids null‑reference surprises. |
| **3️⃣ Add data to Excel** | By using `PutValue` we **add data to Excel** without worrying about cell formatting. The numbers `1` and `2` are our test data for the wrap functions. |
| **4️⃣ How to use WRAPCOLS** | `WRAPCOLS(A1:B1, 1)` tells Excel to take the range `A1:B1` and spill its values vertically, one per row. The result lands in `C1` and spills downwards (`C1`, `C2`, …). |
| **5️⃣ How to use WRAPROWS** | `WRAPROWS(A1:B1, 2)` does the opposite: it creates a horizontal spill, fitting the two values into a single row starting at `C2`. |
| **6️⃣ Force formula calculation** | By default, Aspose.Cells may defer calculation until the file is opened in Excel. Calling `CalculateFormula()` **forces formula calculation** so you can read the results immediately after saving. |
| **7️⃣ Save the workbook** | The final step writes everything to disk. Open the resulting `WrapFunctions.xlsx` to see the outcome. |

---

## Create Excel Workbook C# – Setting Up the Environment

Before you run the code, make sure you have the right tools:

1. **.NET 6.0+** – The latest LTS version works best.
2. **Visual Studio 2022** (or VS Code with the C# extension).
3. **Aspose.Cells for .NET** – Install via NuGet:  
   ```bash
   dotnet add package Aspose.Cells
   ```
4. A writeable folder for the output file.

These prerequisites are minimal; no COM interop or Office installation is required, which is why Aspose.Cells is a popular choice for server‑side Excel generation.

---

## Add Data to Excel – Best Practices

When you **add data to Excel** programmatically, consider these tips:

* **Use `PutValue`** for raw numbers or strings; it automatically detects the data type.
* **Avoid hard‑coding cell addresses** in large projects—use loops or named ranges for scalability.
* **Set cell styles sparingly**; each style change incurs overhead. If you need formatting, create a single style object and apply it to multiple cells.

In our tiny example we only insert two numbers, but the same pattern scales to thousands of rows.

---

## How to Use WRAPROWS – Horizontal Array Example

If you need the opposite of `WRAPCOLS`, `WRAPROWS` is your go‑to. The syntax is:

```
WRAPROWS(source_range, [rows_per_item])
```

* `source_range` – the range you want to transform.
* `rows_per_item` – optional; tells Excel how many rows each element occupies. In our demo we used `2` to force both values onto a single row.

You can experiment by changing the second argument:

```csharp
// Example: split each value into its own column, three rows per item
sheet["D1"].Formula = "WRAPROWS(A1:B1, 3)";
```

Open the workbook and you’ll see the values spill across three columns, each column containing the original numbers repeated as needed.

---

## Force Formula Calculation – When and Why

You might wonder, “Do I really need to call `CalculateFormula()`?” The answer is **yes**, if:

* You plan to read calculated values **programmatically** after saving.
* You want to guarantee the file opens in Excel with the correct results already displayed.
* You’re running in a **headless environment** (e.g., a web API) where no user will manually trigger a recalculation.

Skipping this step won’t break the workbook, but the cells will show the formula text (`=WRAPCOLS(...)`) instead of the computed values until Excel recalculates.

---

## Expected Output – What to Look For

After running the program and opening `WrapFunctions.xlsx`:

| Cell | Formula | Displayed Value |
|------|---------|-----------------|
| **C1** | `=WRAPCOLS(A1:B1, 1)` | `1` (in C1) and `2` (in C2) – a vertical list |
| **C2** | `=WRAPROWS(A1:B1, 2)` | `1` in C2 and `2` in D2 – a horizontal list |

So you’ll see a column of values starting at **C1** and a row of values starting at **C2**. This confirms both wrap functions behaved as expected.

---

## Edge Cases & Variations

| Scenario | What changes? | Suggested tweak |
|----------|---------------|-----------------|
| **Large range (A1:Z1)** | More values to spill vertically | Increase the second argument of `WRAPCOLS` if you want multiple columns per group. |
| **Non‑numeric data** | Strings are handled the same way | No code change; `PutValue` accepts any object. |
| **Dynamic range** | You don’t know the size at compile time | Use `sheet.Cells.MaxDataColumn` and `MaxDataRow` to build the address string. |
| **Multiple worksheets** | Need to apply wrap functions on different sheets | Reference the correct worksheet (`workbook.Worksheets["Sheet2"]`). |

By anticipating these variations, you can adapt the core pattern to almost any automation scenario.

---

## Pro Tips from the Trenches

* **Pro tip:** Wrap the workbook creation in a `using` block if you’re targeting .NET Core 3.1+ to ensure all resources are released promptly.
* **Watch out for:** Setting the same formula in a large range without calling `CalculateFormula()` can cause performance bottlenecks. Batch‑process formulas when possible.
* **Tip:** If you need to read back the calculated values in code, call `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}