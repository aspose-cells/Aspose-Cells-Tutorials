---
category: general
date: 2026-10-10
description: apply number format excel quickly by importing a DataTable, setting date
  and currency formats, and preserving header row excel in a single step.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- set date format excel
- format excel cells date
- set currency format excel
- preserve header row excel
language: en
lastmod: 2026-10-10
og_description: apply number format excel in C# using Aspose.Cells. Learn to set date
  format excel, set currency format excel, and preserve header row excel when importing
  a DataTable.
og_image_alt: Excel worksheet showing currency and date columns formatted after import
og_title: Apply number format excel in C# – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: apply number format excel quickly by importing a DataTable, setting
    date and currency formats, and preserving header row excel in a single step.
  headline: How to apply number format excel with Aspose.Cells
  type: TechArticle
tags:
- excel
- aspnet
- csharp
- excel-formatting
title: How to apply number format excel with Aspose.Cells
url: /net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to apply number format excel with Aspose.Cells

If you need to **apply number format excel** while loading data from a `DataTable`, this guide shows you exactly how. You’ll also learn how to **set date format excel**, **set currency format excel**, and **preserve header row excel** during the import, so the resulting worksheet looks professional without extra post‑processing.

We’ll cover everything from installing the library to writing a complete, runnable snippet. By the end you’ll be able to import any `DataTable` into an Excel workbook, automatically format numeric columns, and keep the header row intact—all in just a few lines of C#.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 or later (the code also works with .NET Framework 4.6+)
* Visual Studio 2022 (or any C# IDE you prefer)
* **Aspose.Cells for .NET** – install via NuGet:

```bash
dotnet add package Aspose.Cells
```

* A `DataTable` source – the example uses a helper method `GetTable()` that returns sample data.

> **Pro tip:** Aspose.Cells is a commercial library, but it offers a free evaluation mode that disables the watermark for up to 30 days.

## Step 1: Create a workbook and access the first worksheet

The workbook object is the entry point for all Excel operations. Creating a new workbook gives you a default worksheet at index 0.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook wb = new Workbook();

        // Obtain reference to the first worksheet
        Worksheet sheet = wb.Worksheets[0];
```

*Why this step?*  
`Workbook` manages file format, calculation engine, and style repository. Accessing `Worksheet` early lets us pass the target sheet to the import method later.

## Step 2: Retrieve the source data as a DataTable

In real projects the data often comes from a database query, a CSV parser, or an API response. For illustration we generate a simple `DataTable` with three columns: **Product**, **Price**, and **ReleaseDate**.

```csharp
        // Step 2: Retrieve the source data as a DataTable
        DataTable sourceTable = GetTable();
```

```csharp
        // Helper method that builds a sample DataTable
        static DataTable GetTable()
        {
            DataTable dt = new DataTable();
            dt.Columns.Add("Product", typeof(string));
            dt.Columns.Add("Price", typeof(decimal));
            dt.Columns.Add("ReleaseDate", typeof(DateTime));

            dt.Rows.Add("Widget A", 12.99m, new DateTime(2023, 5, 1));
            dt.Rows.Add("Widget B", 23.50m, new DateTime(2023, 6, 15));
            dt.Rows.Add("Widget C", 7.75m, new DateTime(2023, 7, 30));
            return dt;
        }
```

*Why this step?*  
A `DataTable` provides a tabular in‑memory representation that Aspose.Cells can import directly, preserving column order and data types.

## Step 3: Prepare a `Style` array – one style per column

Aspose.Cells lets you apply a distinct style to each column during import by passing an array of `Style` objects. The array length must match the number of columns in the source table.

```csharp
        // Step 3: Prepare an array of Style objects – one for each column
        Style[] columnStyles = new Style[sourceTable.Columns.Count];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            // Each entry must be instantiated before we can set properties
            columnStyles[i] = wb.CreateStyle();
        }
```

*Why this step?*  
If you skip the explicit creation (`CreateStyle()`), attempting to set `Number` will throw a `NullReferenceException`. Initialising each `Style` ensures the later assignments succeed.

## Step 4: Assign number formats – currency and date

Excel identifies built‑in number formats by ID.  
* **14** – Currency (e.g., `$1,234.00`)  
* **22** – Short Date (`mm/dd/yyyy`)

```csharp
        // Step 4: Assign number formats to the desired columns
        // Column 0 – Product name (no format needed)
        // Column 1 – Currency format (Number format ID 14)
        columnStyles[1].Number = 14;   // set currency format excel

        // Column 2 – Date format (Number format ID 22)
        columnStyles[2].Number = 22;   // set date format excel
```

> **Note:** If you need a custom format (e.g., `"¥#,##0.00"`), use `Style.Custom = "¥#,##0.00"` instead of a built‑in ID.

*Why this step?*  
Applying the correct **number format** at import time eliminates the need for a second pass that loops through cells to change formatting. It also guarantees that the **format excel cells date** and **set currency format excel** are consistent across all rows.

## Step 5: Import the DataTable while preserving the header row

The `ImportDataTable` method can copy data, keep the first row as a header, and apply the column styles we prepared.

```csharp
        // Step 5: Import the DataTable into the worksheet
        // Parameters:
        //   sourceTable – the DataTable to import
        //   true        – preserve the header row (preserve header row excel)
        //   "A1"        – start cell
        //   columnStyles – array of styles for each column
        sheet.Cells.ImportDataTable(sourceTable, true, "A1", columnStyles);
```

```csharp
        // Save the workbook to disk
        wb.Save("FormattedReport.xlsx");
        Console.WriteLine("Workbook created successfully.");
    }
}
```

**Expected output** – Open `FormattedReport.xlsx` and you’ll see:

| Product | Price (currency) | ReleaseDate (date) |
|---------|------------------|--------------------|
| Widget A| $12.99           | 05/01/2023         |
| Widget B| $23.50           | 06/15/2023         |
| Widget C| $7.75            | 07/30/2023         |

The header row is intact, the **Price** column displays the currency symbol, and the **ReleaseDate** column shows a short date format—all without any further styling code.

### Handling common edge cases

| Situation                               | Solution |
|----------------------------------------|----------|
| **More columns than styles**           | Ensure `columnStyles.Length` equals `sourceTable.Columns.Count`. Missing entries default to the workbook’s default style. |
| **Null values in numeric columns**     | Excel treats `null` as an empty cell; the number format still applies when a value is later entered. |
| **Custom locale‑specific currency**    | Use `columnStyles[i].Custom = "\"€\"#,##0.00"` and set `columnStyles[i].Number = -1` to disable the built‑in ID. |
| **Large tables ( > 100 000 rows )**    | Consider using `ImportDataTable` overload with `ImportTableOptions` to stream data and reduce memory pressure. |
| **Applying the same style to multiple columns** | Re‑use the same `Style` instance in the array (e.g., `columnStyles[1] = columnStyles[2] = dateStyle;`). |

## Bonus: Using a custom format string

If the built‑in IDs don’t meet your needs, you can define a custom number format:

```csharp
// Example: display Euro currency with no decimal places
Style euroStyle = wb.CreateStyle();
euroStyle.Custom = "\"€\"#,##0";
columnStyles[1] = euroStyle;   // replace the built‑in currency style
```

This approach gives you full control over **format excel cells date** and **set currency format excel** beyond the predefined IDs.

## Conclusion

You now know how to **apply number format excel** efficiently when importing a `DataTable` with Aspose.Cells. By creating a per‑column `Style` array, assigning built‑in or custom number IDs, and using the `ImportDataTable` overload that **preserve header row excel**, you can generate ready‑to‑publish worksheets in a single operation.

### What’s next?

* Explore **set date format excel** with custom patterns like `"dddd, mmmm dd, yyyy"`.
* Combine this technique with **conditional formatting** to highlight out‑of‑range values.
* Use **format excel cells date** in pivot tables or charts for dynamic reporting.

Feel free to experiment with different number IDs or custom strings to match your organization’s style guide. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [apply number format excel – Step‑by‑Step Guide to Formatting Columns](/cells/english/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/)
- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Set date format in Excel with C# – Full Import Formatting Guide](/cells/english/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}