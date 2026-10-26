---
category: general
date: 2026-10-26
description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
  WRAPROWS for rows, and save workbook as XLSX programmatically.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split range into rows
- excel wrapcols example
- save workbook as xlsx
- create excel workbook programmatically
language: en
lastmod: 2026-10-26
og_description: How to use WRAPCOLS in C# to split data into columns, use WRAPROWS
  for rows, and save workbook as XLSX. Follow the complete step‑by‑step guide.
og_image_alt: Screenshot illustrating how to use WRAPCOLS to split a range into columns
  in Excel
og_title: How to use WRAPCOLS in C# – split ranges and save as XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  headline: How to use WRAPCOLS in C# and save workbook as XLSX
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  name: How to use WRAPCOLS in C# and save workbook as XLSX
  steps:
  - name: What the saved file looks like
    text: 'When you open `wrapcols_wraprows_output.xlsx` in Excel you’ll see:'
  - name: Changing the number of columns or rows
    text: '* **More columns:** Increase the second argument of `WRAPCOLS`. Example:
      `=WRAPCOLS(A1:A10,5)` creates five columns, leaving empty cells where data runs
      out. * **Dynamic column count:** Use a cell reference instead of a hard‑coded
      number. `=WRAPCOLS(A1:A10, G1)` where `G1` holds the desired column c'
  - name: Handling empty or non‑numeric cells
    text: WRAPCOLS and WRAPROWS ignore empty cells by default, but they preserve the
      order of non‑empty values. If you need to preserve blanks, wrap the source range
      with `IFERROR` or `TEXT` functions before applying WRAPCOLS.
  - name: Saving to other formats
    text: 'While this tutorial focuses on **save workbook as xlsx**, Aspose.Cells
      supports many formats (`.xls`, `.csv`, `.pdf`, etc.):'
  - name: What’s next?
    text: '* Explore **conditional formatting** to highlight the spilled data. * Combine
      **WRAPCOLS** with **SORT** or **FILTER** for dynamic dashboards. * Use Aspose.Cells’
      **charting API** to visualize the rearranged data directly from code.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: How to use WRAPCOLS in C# and save workbook as XLSX
url: /net/row-and-column-management/how-to-use-wrapcols-in-c-and-save-workbook-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to use WRAPCOLS in C# and save workbook as XLSX

If you need to **how to use WRAPCOLS** to reorganize data in an Excel file, this guide shows you a complete, runnable solution. You’ll see an **excel wrapcols example**, learn how to **split range into rows** with WRAPROWS, and finish by **save workbook as XLSX**—all done **programmatically**.

Working with Excel from C# often means creating a workbook, applying formulas, and persisting the file. The code below uses the Aspose.Cells library, which lets you manipulate Excel files without needing Microsoft Office installed. By the end of this tutorial you’ll be able to **create excel workbook programmatically**, split data both horizontally and vertically, and produce a clean `.xlsx` file ready for downstream processing.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 or later (the code also works with .NET Framework 4.7+)
* A reference to the **Aspose.Cells** NuGet package  
  ```bash
  dotnet add package Aspose.Cells
  ```
* Basic familiarity with C# and Excel formulas

## Step 1: How to use WRAPCOLS to split a range into columns

The **WRAPCOLS** function takes a one‑dimensional range and spreads its values across the specified number of columns. In this example we start with values in `A1:A10` and ask WRAPCOLS to create three columns.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is the “create excel workbook programmatically” step
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Populate source data for demonstration
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 0].PutValue($"Item {i + 1}");
        }

        // Apply WRAPCOLS: split A1:A10 into 3 columns starting at C1
        // The formula is entered in cell C1 (row 0, column 2)
        ws.Cells[0, 2].Formula = "=WRAPCOLS(A1:A10,3)";

        // -------------------------------------------------
        // Why this works:
        // -------------------------------------------------
        // * WRAPCOLS reads the source range (A1:A10) vertically.
        // * The second argument (3) tells Excel to create three columns.
        // * The function returns a 2‑dimensional array that Excel spills into the
        //   surrounding cells automatically.
        // -------------------------------------------------
```

> **Result:** Cells `C1:E4` now contain the original ten items arranged in three columns (the last column holds the remaining items).

![Screenshot illustrating how to use WRAPCOLS to split a range into columns in Excel](image-url.png)

## Step 2: Split range into rows with WRAPROWS

While **WRAPCOLS** works horizontally, **WRAPROWS** performs the opposite: it spreads a range across a given number of rows. Here we take values from `B1:B10` and arrange them into two rows starting at `F1`.

```csharp
        // Populate a second source column for WRAPROWS
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 1].PutValue($"Value {i + 1}");
        }

        // Apply WRAPROWS: split B1:B10 into 2 rows starting at F1
        ws.Cells[0, 5].Formula = "=WRAPROWS(B1:B10,2)";

        // -------------------------------------------------
        // Why WRAPROWS is useful:
        // -------------------------------------------------
        // * It converts a vertical list into a matrix with the specified row count.
        // * Handy when you need to prepare data for pivot tables, charts, or
        //   reporting layouts that expect a horizontal orientation.
        // -------------------------------------------------
```

> **Result:** The formula fills cells `F1:K2` with the ten values distributed over two rows.

## Step 3: Save workbook as XLSX

After applying the formulas, the final step is to persist the file. The **save workbook as xlsx** operation writes the in‑memory workbook to disk in the modern OpenXML format.

```csharp
        // Save the workbook – this completes the “save workbook as xlsx” step
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "wrapcols_wraprows_output.xlsx");

        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### What the saved file looks like

When you open `wrapcols_wraprows_output.xlsx` in Excel you’ll see:

| C | D | E |
|---|---|---|
| Item 1 | Item 4 | Item 7 |
| Item 2 | Item 5 | Item 8 |
| Item 3 | Item 6 | Item 9 |
|        |        | Item 10 |

and

| F | G | H | I | J | K |
|---|---|---|---|---|---|
| Value 1 | Value 3 | Value 5 | Value 7 | Value 9 | |
| Value 2 | Value 4 | Value 6 | Value 8 | Value 10 | |

The formulas remain in the cells, so any later changes to the source ranges are reflected automatically.

## Step 4: Common variations and edge cases

### Changing the number of columns or rows

* **More columns:** Increase the second argument of `WRAPCOLS`.  
  Example: `=WRAPCOLS(A1:A10,5)` creates five columns, leaving empty cells where data runs out.
* **Dynamic column count:** Use a cell reference instead of a hard‑coded number.  
  `=WRAPCOLS(A1:A10, G1)` where `G1` holds the desired column count.

### Handling empty or non‑numeric cells

WRAPCOLS and WRAPROWS ignore empty cells by default, but they preserve the order of non‑empty values. If you need to preserve blanks, wrap the source range with `IFERROR` or `TEXT` functions before applying WRAPCOLS.

### Saving to other formats

While this tutorial focuses on **save workbook as xlsx**, Aspose.Cells supports many formats (`.xls`, `.csv`, `.pdf`, etc.):

```csharp
workbook.Save("output.pdf", SaveFormat.Pdf);   // Export to PDF
workbook.Save("output.csv", SaveFormat.Csv);   // Export to CSV
```

## Pro tips and pitfalls

* **Pro tip:** Set `Workbook.Settings.CalcEngineEnabled = true` if you plan to evaluate formulas immediately after saving.
* **Watch out for:** Large source ranges can produce very large spill areas, which may impact performance. Limit the range size or split the operation into multiple worksheets.
* **Thread safety:** Aspose.Cells objects are **not** thread‑safe. Create a separate `Workbook` instance per thread if you’re processing files in parallel.

## Conclusion

You now know **how to use WRAPCOLS** to split a vertical range into multiple columns, how to **split range into rows** with WRAPROWS, and how to **save workbook as XLSX** after performing these transformations. By following the steps above you can **create excel workbook programmatically**, apply powerful spill formulas, and generate ready‑to‑share Excel files without manual intervention.

### What’s next?

* Explore **conditional formatting** to highlight the spilled data.
* Combine **WRAPCOLS** with **SORT** or **FILTER** for dynamic dashboards.
* Use Aspose.Cells’ **charting API** to visualize the rearranged data directly from code.

Happy coding, and enjoy automating your Excel workflows!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)
- [How to Use WRAPCOLS – Complete Guide for C# Excel Automation](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}