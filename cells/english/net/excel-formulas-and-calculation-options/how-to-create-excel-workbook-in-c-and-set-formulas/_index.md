---
category: general
date: 2026-10-01
description: Create Excel workbook in C# quickly, learn how to set a formula, calculate
  cotangent, and use the PI function in Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- how to calculate cot
- set formula in cell
- write formula to cell
- how to use pi function
language: en
lastmod: 2026-10-01
og_description: Create Excel workbook in C# with Aspose.Cells. Learn how to set a
  formula, use the PI function, and calculate cotangent in just a few steps.
og_image_alt: Diagram showing an Excel workbook created in C# with a formula in cell
  A1
og_title: Create Excel workbook in C# – set formulas and calculate cot
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create Excel workbook in C# quickly, learn how to set a formula, calculate
    cotangent, and use the PI function in Aspose.Cells.
  headline: How to create Excel workbook in C# and set formulas
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: How to create Excel workbook in C# and set formulas
url: /net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-in-c-and-set-formulas/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create Excel workbook in C# and set formulas

If you need to **create Excel workbook C#** code that writes a formula into a cell, this guide shows you exactly how. You’ll see how to set a formula in a worksheet, use the built‑in PI function, and calculate the cotangent of an angle—all with Aspose.Cells.

The tutorial covers everything from initializing the workbook to retrieving the calculated result, so you can copy the complete example into your own project without any missing pieces.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 or later installed  
* A valid Aspose.Cells license (or a temporary evaluation key)  
* Visual Studio 2022 or any C# IDE you prefer  

No additional NuGet packages are required beyond `Aspose.Cells`.

## Create Excel workbook in C#

The first step is to instantiate a new `Workbook` object. This object represents the entire Excel file in memory and gives you access to its worksheets.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                 // creates an empty .xlsx file
        var worksheet = workbook.Worksheets[0];        // the default first sheet

        // Continue with the rest of the steps...
```

Creating the workbook this way ensures the file is ready for any further manipulation, such as adding data, styling cells, or writing formulas.

## Set formula in cell using the PI function

Now you’ll **write formula to cell** A1. The formula uses the `PI()` function to supply the constant π and the `COT` function to compute its cotangent.

```csharp
        // Step 2: Set a formula in cell A1 (row 0, column 0)
        // The formula calculates the cotangent of π/4, which equals 1
        worksheet.Cells[0, 0].Formula = "=COT(PI()/4)";

        // Continue with calculation...
```

*Why this matters*: `PI()` is a built‑in Excel function that returns the value of π. By dividing it by 4 you get 45°, and `COT` returns the cotangent of that angle. This demonstrates **how to use pi function** inside an Excel formula from C#.

## How to calculate cot with Aspose.Cells

If you’re wondering **how to calculate cot** without manually converting angles, the `COT` function does the heavy lifting. It accepts an angle in radians, so you can combine it with `PI()` for common angles.

```csharp
        // Step 3: Recalculate the workbook so the formula is evaluated
        workbook.Calculate();

        // Step 4: Retrieve and display the calculated result
        double result = worksheet.Cells[0, 0].DoubleValue;
        Console.WriteLine($"Cotangent of PI/4 = {result}");
    }
}
```

Running the program prints:

```
Cotangent of PI/4 = 1
```

Because `COT(π/4)` equals 1, the output confirms that the formula was correctly **set formula in cell** and evaluated.

## Write formula to cell – additional tips

* **Multiple formulas**: You can assign a formula to any cell using the same `Formula` property, e.g., `worksheet.Cells["B2"].Formula = "=SIN(PI()/2)";`.
* **International settings**: Aspose.Cells respects the workbook’s locale, so function names stay in English (`PI`, `COT`) regardless of the user’s regional settings.
* **Performance**: If you need to set thousands of formulas, batch them and call `workbook.Calculate()` once at the end to avoid repeated recalculations.

## Complete runnable example

Below is the full program you can copy‑paste into a console project. It includes all required `using` statements and demonstrates the complete workflow from workbook creation to result output.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook and obtain the first worksheet
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // Write a formula that uses the PI function and calculates cotangent
        worksheet.Cells[0, 0].Formula = "=COT(PI()/4)";

        // Force calculation so the formula value is materialized
        workbook.Calculate();

        // Read the calculated value and display it
        double cotValue = worksheet.Cells[0, 0].DoubleValue;
        Console.WriteLine($"Cotangent of PI/4 = {cotValue}");

        // Optional: save the workbook to verify the formula visually
        workbook.Save("CotExample.xlsx");
    }
}
```

**Expected output** when you run the program:

```
Cotangent of PI/4 = 1
```

The generated `CotExample.xlsx` file contains the formula in cell A1, allowing you to open it in Excel and see the same result.

## Conclusion

You now know how to **create Excel workbook C#** code that writes a formula, uses the `PI` function, and **calculates cot** with Aspose.Cells. The example covers the entire lifecycle: workbook creation, **set formula in cell**, recalculation, and result retrieval.

Next steps you might explore:

* Apply **write formula to cell** for more complex calculations like financial models.  
* Use **set formula in cell** together with conditional formatting to highlight results.  
* Combine the **how to use pi function** with trigonometric charts for scientific reporting.

Feel free to experiment with different angles, functions, and worksheet layouts. Mastering formula handling in C# opens the door to fully automated Excel reporting pipelines. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Calculate Cotangent in Excel with C# – Create Workbook, Use EXPAND](/cells/english/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/)
- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}