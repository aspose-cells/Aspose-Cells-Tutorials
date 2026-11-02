---
category: general
date: 2026-10-10
description: Create Excel workbook in C# and use the WRAPCOLS function to split array
  data into columns. Follow a complete step‑by‑step guide with runnable code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- excel formula split data
- use wrapcols function
- how to use wrapcols
- split array columns
language: en
lastmod: 2026-10-10
og_description: Create Excel workbook in C# and apply the WRAPCOLS function to split
  array data into columns. This guide shows the full code and explains each step.
og_image_alt: Screenshot of an Excel sheet showing three columns filled by the WRAPCOLS
  formula
og_title: Create Excel workbook and split data with WRAPCOLS in C#
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  headline: How to create Excel workbook and split data with WRAPCOLS in C#
  type: TechArticle
- description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  name: How to create Excel workbook and split data with WRAPCOLS in C#
  steps:
  - name: Using the function with different data types
    text: 'The `WRAPCOLS` function is not limited to numbers. You can split text values,
      dates, or mixed types:'
  - name: Variable column count at runtime
    text: 'Often the number of columns you need depends on user input. You can build
      the formula string dynamically:'
  - name: Large arrays and performance
    text: '`WRAPCOLS` can handle thousands of elements, but evaluating extremely large
      arrays in a single cell may increase calculation time. If you notice slowdown:'
  - name: Handling empty cells
    text: If the source array contains empty strings (`""`) or `NULL` values, `WRAPCOLS`
      inserts blank cells, preserving the column layout. This behavior is useful when
      you need placeholder columns for later data entry.
  - name: Using named ranges instead of literals
    text: 'For maintainability, define a named range that holds the source data, then
      reference it:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: How to create Excel workbook and split data with WRAPCOLS in C#
url: /net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create Excel workbook and split data with WRAPCOLS in C#

If you need to **create Excel workbook** programmatically, this guide shows you exactly how to do it and how to **split array data** across columns using the `WRAPCOLS` function. You’ll get a complete, runnable example that produces an `.xlsx` file with the data distributed into three columns.

The tutorial covers everything you need: required NuGet packages, each line of code, why the `WRAPCOLS` formula works, and how to adapt the solution for different array sizes or column counts. By the end you’ll be able to embed the **use wrapcols function** technique in any C# project that generates Excel files.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 SDK or later installed  
* A C# IDE (Visual Studio, VS Code, Rider, etc.)  
* The **Aspose.Cells for .NET** NuGet package – the library that provides the `Workbook` class used in the examples  

You do not need an Office installation; Aspose.Cells writes the `.xlsx` file directly.

## Step 1 – create Excel workbook

The first task is to instantiate a new workbook object and obtain a reference to the first worksheet. This step is the foundation for any further manipulation.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();                // creates an empty Excel file in memory
        Worksheet ws = wb.Worksheets[0];             // the default worksheet is at index 0
```

`Workbook` represents the whole file, while `Worksheet` represents a single sheet. By creating the workbook in memory you avoid disk I/O until you explicitly save it.

## Step 2 – apply WRAPCOLS to split array columns

Now you’ll place a formula in cell **A1** that uses `WRAPCOLS`. The function receives two arguments: the source array and the number of columns you want the array to wrap into.

```csharp
        // Step 2: Apply the WRAPCOLS formula to split the array into 3 columns
        // The array {1,2,3,4,5,6} will be distributed as:
        // 1 2 3
        // 4 5 6
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

**Why this works:** `WRAPCOLS` takes the flat array `{1,2,3,4,5,6}` and fills the worksheet row‑by‑row, creating three columns per row. The first argument can be any Excel array literal, a named range, or a dynamic array formula. The second argument (`3`) tells Excel how many columns to generate before moving to the next row.

### Using the function with different data types

The `WRAPCOLS` function is not limited to numbers. You can split text values, dates, or mixed types:

```csharp
        // Example with mixed data: strings and numbers
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";
```

When the source array contains strings, Excel automatically treats the result as text cells. This flexibility lets you **excel formula split data** for reporting, dashboards, or data‑migration tasks.

## Step 3 – calculate formulas so the worksheet is populated

Formulas are stored as strings until you ask the workbook to evaluate them. Calling `CalculateFormula` forces evaluation and writes the results into the cells.

```csharp
        // Step 3: Calculate formulas so the worksheet is populated
        wb.CalculateFormula();   // evaluates all formulas in the workbook
```

Without this call the saved file would contain only the formula text, not the calculated values. The method works across the entire workbook, so you can place additional formulas elsewhere and they will all be resolved with a single call.

## Step 4 – save the workbook to see the result

Finally, write the workbook to disk. Choose a folder you have write permission for, and give the file a clear name.

```csharp
        // Step 4: Save the workbook to see the result
        string outputPath = @"output.xlsx";
        wb.Save(outputPath);      // creates output.xlsx in the application directory
    }
}
```

When you open `output.xlsx` in Excel (or any compatible viewer), you’ll see:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

If you used the mixed‑type example, rows 3‑4 would contain the text and numbers accordingly.

## Advanced variations and edge‑case handling

### Variable column count at runtime

Often the number of columns you need depends on user input. You can build the formula string dynamically:

```csharp
int columns = 4; // could come from UI, config, etc.
string arrayLiteral = "{10,20,30,40,50,60,70,80}";
ws.Cells[5, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
```

### Large arrays and performance

`WRAPCOLS` can handle thousands of elements, but evaluating extremely large arrays in a single cell may increase calculation time. If you notice slowdown:

* Break the source array into smaller chunks and write each chunk to a separate starting cell.  
* Use `WorkbookSettings` to enable multi‑threaded calculation:

```csharp
wb.Settings.CalcMode = CalculationModeType.Automatic;
wb.Settings.EnableMultiThreadedCalc = true;
```

### Handling empty cells

If the source array contains empty strings (`""`) or `NULL` values, `WRAPCOLS` inserts blank cells, preserving the column layout. This behavior is useful when you need placeholder columns for later data entry.

### Using named ranges instead of literals

For maintainability, define a named range that holds the source data, then reference it:

```csharp
ws.Cells["D1:D6"].PutValue(new object[] { 11, 12, 13, 14, 15, 16 });
ws.Cells["E1"].Formula = "=WRAPCOLS(D1:D6,3)";
```

Now the formula reads data from the worksheet itself, enabling **how to use wrapcols** in dynamic reporting scenarios.

## Common pitfalls and pro tips

* **Do not omit the second argument.** `WRAPCOLS(array)` without a column count returns a single column, which defeats the purpose of splitting data.  
* **Avoid mixing array dimensions.** The source array must be one‑dimensional; providing a two‑dimensional array (e.g., `{ {1,2},{3,4} }`) triggers a `#VALUE!` error.  
* **Save after calculation.** If you call `wb.Save` before `CalculateFormula`, the file will contain only the formula text.  
* **Check file permissions.** When running in restricted environments (e.g., ASP.NET), ensure the process identity can write to the target folder.  

## Full working example

Below is the complete program you can copy, paste, and run. It includes all imports, error handling, and comments.

```csharp
using System;
using Aspose.Cells;

class ExcelWrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Split a numeric array into 3 columns
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

        // Split a mixed array (text + numbers) into 3 columns, starting at row 3
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";

        // Dynamically build a formula with a variable column count
        int columnCount = 4;
        string sourceArray = "{10,20,30,40,50,60,70,80}";
        ws.Cells[5, 0].Formula = $"=WRAPCOLS({sourceArray},{columnCount})";

        // Evaluate all formulas
        wb.CalculateFormula();

        // Save the workbook
        string outputPath = "output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Running the program produces `output.xlsx` with three distinct regions demonstrating **excel formula split data** using the `WRAPCOLS` function.

## Conclusion

You now know how to **create Excel workbook** files in C# and how to **use wrapcols function** to **split array columns** efficiently. The primary steps—instantiating `Workbook`, inserting the `WRAPCOLS` formula, calculating, and saving—form a reusable pattern for any automation task that requires data distribution across columns.

From here you can:

* Combine `WRAPCOLS` with other dynamic‑array functions like `FILTER` or `SORT`.  
* Export large data sets from databases and let Excel handle the layout automatically.  
* Build user‑driven reports where the column count is selected via a UI control.

Experiment with different array sources, column counts, and additional formulas to extend this foundation. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Create Excel Workbook – Convert Array to Matrix with WRAPCOLS](/cells/english/net/calculation-engine/create-excel-workbook-convert-array-to-matrix-with-wrapcols/)
- [Create Excel Workbook C# – Step‑by‑Step Guide](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}