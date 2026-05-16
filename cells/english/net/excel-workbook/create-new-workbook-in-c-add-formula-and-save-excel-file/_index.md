---
category: general
date: 2026-02-23
description: Create new workbook programmatically in C# and add formula to a cell.
  Learn how to use EXPAND, then save Excel workbook effortlessly.
draft: false
keywords:
- create new workbook
- add formula to cell
- save excel workbook
- how to use expand
- create excel file programmatically
language: en
og_description: Create new workbook programmatically in C#. Add a formula to a cell,
  learn how to use EXPAND, and save the Excel workbook in seconds.
og_title: Create New Workbook in C# – Add Formula and Save Excel File
tags:
- C#
- Excel Automation
- Aspose.Cells
title: Create New Workbook in C# – Add Formula and Save Excel File
url: /net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create New Workbook in C# – Add Formula and Save Excel File

Ever wondered how to **create new workbook** objects from code without ever opening Excel? You're not the only one. Many developers hit a wall when they need to generate a spreadsheet on the fly—maybe for a report, an export, or a quick data dump.  

The good news? In this guide you’ll see exactly how to **create new workbook**, drop an **add formula to cell**, and then **save excel workbook** with just a few lines of C#. We'll also dive into **how to use expand** so you can generate dynamic arrays without manual copying. By the end, you’ll be able to **create excel file programmatically** and ship it to users or downstream services.

## Prerequisites

- .NET 6.0 or later (any recent .NET runtime works)
- Aspose.Cells for .NET (free trial or licensed version) – this library gives us the `Workbook` and `Worksheet` classes used below.
- A basic understanding of C# syntax—no deep Excel knowledge required.

If you already have those, great! If not, grab Aspose.Cells from NuGet (`Install-Package Aspose.Cells`) and you’ll be ready to roll.

---

## Step 1: Create New Workbook – The Foundation

To start, we need to instantiate a fresh workbook object. Think of it as opening a brand‑new Excel file that’s completely empty.

```csharp
using Aspose.Cells;

public class ExcelGenerator
{
    public void Generate()
    {
        // Step 1: Create a new workbook (this is the core of create new workbook)
        Workbook workbook = new Workbook();
```

> **Why this matters:** The `Workbook` class is the entry point for any Excel manipulation. By creating a new instance, we allocate memory for sheets, styles, and formulas—all without touching the file system.

---

## Step 2: Access the First Worksheet

Every new workbook comes with a default worksheet (named *Sheet1*). We’ll grab it so we can place data and formulas.

```csharp
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** If you need multiple sheets, simply call `workbook.Worksheets.Add("MySheet")` and work with the returned `Worksheet` object.

---

## Step 3: Add Formula to Cell – Using EXPAND

Now for the fun part: inserting a formula. The `EXPAND` function is perfect when you want to turn a static array into a larger, auto‑filled range.

```csharp
        // Step 3: Add formula to cell A1 using EXPAND
        // This creates a 5‑row array from the constant {1,2,3}
        worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";
```

### How the EXPAND Formula Works

| Argument | Meaning |
|----------|---------|
| `{1,2,3}` | The source array (a horizontal list of three numbers) |
| `5`       | Desired number of rows in the result |
| `1`       | Desired number of columns (keep it 1 to stay vertical) |

When Excel evaluates this, it produces a **vertical** list:

```
A1: 1
A2: 2
A3: 3
A4: 0   (filled with zeros)
A5: 0
```

> **Why use EXPAND?** It eliminates the need for manual copying or VBA loops. The function dynamically reshapes data, making your spreadsheets more robust and easier to maintain.

---

## Step 4: Save Excel Workbook – Persist the Result

With the formula in place, the final step is to write the workbook to disk. You can choose any folder you have write access to.

```csharp
        // Step 4: Save the workbook to view the result
        string outputPath = @"C:\Temp\ExpandFormula.xlsx";
        workbook.Save(outputPath);
    }
}
```

> **What you’ll see:** Open `ExpandFormula.xlsx` in Excel, and cell `A1` will display the expanded array. The formula itself stays in the cell, so if you edit the source array, the output updates automatically.

---

## Optional: Verify the Output Programmatically

If you prefer not to open Excel manually, you can read back the values to confirm they match expectations.

```csharp
        // Verify values without opening Excel
        for (int row = 0; row < 5; row++)
        {
            var value = worksheet.Cells[row, 0].Value; // column 0 = A
            Console.WriteLine($"Row {row + 1}: {value}");
        }
```

Running the above will print:

```
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

---

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| **Can I use EXPAND with a larger source array?** | Absolutely. Just change `{1,2,3}` to any constant or cell range, e.g., `EXPAND(A1:C1,10,1)`. |
| **What if I need a horizontal result?** | Swap the row/column arguments: `EXPAND({1,2,3},1,5)` will produce a 1‑row, 5‑column spread. |
| **Will this work on older Excel versions?** | `EXPAND` is available starting with Excel 365/2021. For older versions, you’d need to simulate the array with `INDEX`/`SEQUENCE`. |
| **Do I need to call `workbook.CalculateFormula()`?** | No. Aspose.Cells automatically evaluates formulas on save, so the values appear immediately. |
| **How to add more than one sheet before saving?** | Call `workbook.Worksheets.Add("SecondSheet")` and repeat the cell‑manipulation steps on the new worksheet. |

---

## Full Working Example

Below is the complete, ready‑to‑run program. Copy‑paste it into a console app, adjust the output path, and hit **F5**.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutomationDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create new workbook
            Workbook workbook = new Workbook();

            // Access first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // Add EXPAND formula to A1
            worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";

            // Optional: verify values in console
            workbook.CalculateFormula(); // ensures formulas are evaluated now
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine($"A{i + 1} = {worksheet.Cells[i, 0].Value}");
            }

            // Save the workbook
            string filePath = @"C:\Temp\ExpandFormula.xlsx";
            workbook.Save(filePath);
            Console.WriteLine($"Workbook saved to {filePath}");
        }
    }
}
```

**Expected output in the console:**

```
A1 = 1
A2 = 2
A3 = 3
A4 = 0
A5 = 0
Workbook saved to C:\Temp\ExpandFormula.xlsx
```

Open the generated file and you’ll see the same numbers populated in column **A**.

---

## Visual Summary

![Create new workbook example](create-new-workbook.png "Screenshot showing a new workbook created with create new workbook in C#")

*The image illustrates the freshly generated workbook with the EXPAND result.*

---

## Conclusion

You now know how to **create new workbook**, **add formula to cell**, and **save excel workbook** using C#. By mastering **how to use expand**, you can generate dynamic arrays without manual effort, and the whole process lets you **create excel file programmatically** for any automation scenario.

What's next? Try swapping the constant array for a range reference, experiment with different `EXPAND` dimensions, or chain multiple formulas across sheets. The same pattern works for charts, styling, and even pivot tables—so keep exploring.

If you ran into any hiccups, drop a comment below. Happy coding, and enjoy the power of programmatic Excel!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}