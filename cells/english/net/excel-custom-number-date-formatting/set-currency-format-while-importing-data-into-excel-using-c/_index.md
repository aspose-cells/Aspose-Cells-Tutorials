---
category: general
date: 2026-11-19
description: Set currency format in Excel with C# – learn how to set number format
  and style excel columns during an excel worksheet import.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set currency format
- how to set number format
- assign number format
- excel worksheet import
- style excel columns
language: en
lastmod: 2026-11-19
og_description: Set currency format in Excel with C# and discover how to set number
  format, assign number format, and style excel columns during an excel worksheet
  import.
og_image_alt: Screenshot showing Excel cells formatted as currency after import
og_title: Set currency format in Excel with C# – complete step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  headline: Set currency format while importing data into Excel using C#
  type: TechArticle
- description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  name: Set currency format while importing data into Excel using C#
  steps:
  - name: Expected result
    text: 'When you open **FinancialReport.xlsx**, you’ll see:'
  - name: Assign number format to date columns
    text: '```csharp // Suppose column 2 contains dates and you want "dd-MMM-yyyy"
      columnStyles[2].Number = 14; // 14 = built‑in short date ```'
  - name: Use custom number formats for percentages
    text: '```csharp columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00% ```'
  - name: Styling beyond number formats
    text: 'You can also set font, background color, or alignment on the same `Style`
      object:'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
- Formatting
title: Set currency format while importing data into Excel using C#
url: /net/excel-custom-number-date-formatting/set-currency-format-while-importing-data-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Set currency format while importing data into Excel using C#

If you need to **set currency format** in an Excel worksheet, this guide shows you how to **set number format** and style the columns while performing an **excel worksheet import**. You’ll see a complete, runnable example that assigns the correct number format to each column of a `DataTable` and imports the data with the desired styling.

Working with Excel from C# often requires more than just dumping raw values—you must also control how numbers appear. Whether you’re generating invoices, financial reports, or dashboards, correctly formatting currency, percentages, or dates makes the output instantly readable.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 (or later) installed.
* A reference to **Aspose.Cells for .NET** (or any library that exposes a `Style` class with a `Number` property).  
  *NuGet*: `Install-Package Aspose.Cells`.
* Basic familiarity with `DataTable` and C# collections.
* An IDE such as Visual Studio 2022 or VS Code.

## Step 1: Retrieve the data to be written to the worksheet

First obtain a `DataTable` that contains the raw data you want to export. In real projects this could come from a database query, an API call, or a CSV parser.

```csharp
using System.Data;

/// <summary>
/// Returns a sample DataTable with three columns:
/// Id (int), Amount (decimal), and Description (string).
/// </summary>
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Amount", typeof(decimal));
    table.Columns.Add("Description", typeof(string));

    // Sample rows
    table.Rows.Add(1, 1234.56m, "Office supplies");
    table.Rows.Add(2, 98765.43m, "Consulting fees");
    table.Rows.Add(3, 0.99m, "Miscellaneous");

    return table;
}

// Retrieve the data
DataTable dataTable = GetData();
```

> **Why this matters:** Importing a fully populated `DataTable` lets you keep the data‑retrieval logic separate from the Excel‑generation logic, which improves testability and maintainability.

## Step 2: Create a style array – one entry per column in the DataTable

Aspose.Cells expects a `Style[]` whose length matches the number of columns you plan to import. Each element can hold a specific number format.

```csharp
// Allocate a Style object for each column
Style[] columnStyles = new Style[dataTable.Columns.Count];

// Initialize each Style instance (required before assigning properties)
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = ws.Workbook.CreateStyle();
}
```

> **Pro tip:** Even if you only need formatting for a subset of columns, you still have to create a `Style` instance for every column; otherwise you’ll get a `NullReferenceException` during import.

## Step 3: Assign number format to the desired columns

The built‑in style numbers differ per library. In Aspose.Cells:

* `0` → General (integer)  
* `2` → Currency (e.g., `$#,##0.00`)  
* `3` → Date, etc.

Here we **assign number format** to two columns: the first column (Id) stays as an integer, while the second column (Amount) receives a currency format.

```csharp
// Column 0 → integer format (style number 0)
columnStyles[0].Number = 0;

// Column 1 → currency format (style number 2)
columnStyles[1].Number = 2;

// If you need a custom format, you can also use a format string:
// columnStyles[1].Custom = "$#,##0.00";
```

> **How to set number format**: Using the `Number` property is the quickest way to pick a built‑in format. For locale‑specific currencies, consider using a custom format string that includes the appropriate currency symbol.

## Step 4: Import the DataTable into the worksheet, applying the column styles

Now that the style array is ready, import the data. The `ImportDataTable` method respects the styles you passed.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];

// Import the DataTable, starting at cell A1 (row 0, column 0)
// The third argument (true) tells the method to write column headers.
ws.Cells.ImportDataTable(
    dataTable,
    /* includeColumnNames */ true,
    /* startRow */ 0,
    /* startColumn */ 0,
    columnStyles);

// Save the workbook
workbook.Save("FinancialReport.xlsx", SaveFormat.Xlsx);
```

### Expected result

When you open **FinancialReport.xlsx**, you’ll see:

| Id | Amount      | Description      |
|----|------------|------------------|
| 1  | $1,234.56  | Office supplies |
| 2  | $98,765.43 | Consulting fees |
| 3  | $0.99      | Miscellaneous    |

*The **Amount** column is displayed using the currency format you set, while **Id** remains an integer.*

## How to set number format for additional scenarios

### Assign number format to date columns

```csharp
// Suppose column 2 contains dates and you want "dd-MMM-yyyy"
columnStyles[2].Number = 14; // 14 = built‑in short date
```

### Use custom number formats for percentages

```csharp
columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00%
```

### Styling beyond number formats

You can also set font, background color, or alignment on the same `Style` object:

```csharp
columnStyles[1].Font.IsBold = true;
columnStyles[1].ForegroundColor = Color.LightYellow;
columnStyles[1].HorizontalAlignment = TextAlignmentType.Center;
```

> **Why this works:** The `Style` object aggregates all visual properties for a cell. When you pass the array to `ImportDataTable`, each cell inherits the defined style automatically.

## Common pitfalls and how to avoid them

| Pitfall | Symptom | Fix |
|---------|---------|-----|
| Forgetting to instantiate each `Style` | `NullReferenceException` on import | Loop through the array and call `CreateStyle()` before setting properties. |
| Using the wrong built‑in number index | Wrong format (e.g., dates appear as integers) | Consult the library’s documentation for the correct `Number` constants. |
| Not saving the workbook | No output file or empty file | Call `workbook.Save(...)` after the import completes. |
| Locale mismatch for currency symbol | `$` appears even in non‑US locales | Use a custom format string with the appropriate symbol (e.g., `"€#,##0.00"`). |

## Full, runnable example

```csharp
using System;
using System.Data;
using Aspose.Cells;
using System.Drawing; // For Color

class ExcelExport
{
    static void Main()
    {
        // ---------- Step 1 ----------
        DataTable dataTable = GetData();

        // ---------- Step 2 ----------
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];
        Style[] columnStyles = new Style[dataTable.Columns.Count];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            columnStyles[i] = ws.Workbook.CreateStyle();
        }

        // ---------- Step 3 ----------
        // Column 0 – integer (no special format)
        columnStyles[0].Number = 0;

        // Column 1 – currency format
        columnStyles[1].Number = 2; // built‑in currency
        // Optional: make the currency column bold with a light background
        columnStyles[1].Font.IsBold = true;
        columnStyles[1].ForegroundColor = Color.LightYellow;
        columnStyles[1].HorizontalAlignment = TextAlignmentType.Center;

        // If a third column existed with dates:
        // columnStyles[2].Number = 14; // short date

        // ---------- Step 4 ----------
        ws.Cells.ImportDataTable


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create excel file c# – style cells and set currency format](/cells/english/net/excel-formatting-and-styling/create-excel-file-c-style-cells-and-set-currency-format/)
- [How to Format Excel Columns in C# – Complete Guide](/cells/english/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/)
- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}