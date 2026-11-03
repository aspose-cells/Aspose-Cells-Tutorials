---
category: general
date: 2026-10-01
description: alternating column colors excel using C# – learn to create an Excel file
  from a DataTable, set cell background color c#, and import datatable to excel with
  styled columns.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- alternating column colors excel
- set cell background color c#
- create excel file from datatable c#
- import datatable to excel
language: en
lastmod: 2026-10-01
og_description: alternating column colors excel made easy. Follow this guide to create
  an Excel file from a DataTable, set cell background color c#, and import datatable
  to excel with styled columns.
og_image_alt: Screenshot of an Excel sheet showing alternating column colors applied
  by C# code
og_title: Add alternating column colors in Excel with C# – step‑by‑step guide
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: alternating column colors excel using C# – learn to create an Excel
    file from a DataTable, set cell background color c#, and import datatable to excel
    with styled columns.
  headline: How to add alternating column colors in Excel using C#
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: How to add alternating column colors in Excel using C#
url: /net/excel-colors-and-background-settings/how-to-add-alternating-column-colors-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to add alternating column colors in Excel using C#

If you need **alternating column colors excel** in a report generated from your application, this guide shows you a complete solution. You’ll see how to create an Excel file from a `DataTable`, set cell background color C# style, and import datatable to excel while applying a distinct style to each column.

The tutorial covers everything you need: required NuGet packages, a full, runnable code sample, and explanations of why each step matters. By the end you’ll have a styled workbook that can be opened directly in Microsoft Excel.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 (or later) SDK installed  
* Visual Studio 2022 (or any C#‑compatible IDE)  
* The **Aspose.Cells for .NET** library – install it with  

```bash
dotnet add package Aspose.Cells
```

Aspose.Cells provides the `Workbook`, `Worksheet`, `Style`, and `BackgroundType` classes used in the example.

## Step 1: Retrieve the source data as a `DataTable`

The first task is to obtain the data you want to export. In real projects you might fill the `DataTable` from a database query, an API call, or any in‑memory collection.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetData()
{
    // Create a sample DataTable with three columns and five rows
    DataTable table = new DataTable("Sample");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    for (int i = 1; i <= 5; i++)
    {
        table.Rows.Add(i, $"Student {i}", 60 + i * 5);
    }
    return table;
}
```

**Why this matters:**  
A `DataTable` is a universal container that maps cleanly to an Excel worksheet. Using a `DataTable` lets you **create excel file from datatable c#** without writing custom loops for each column.

## Step 2: Create a new workbook and get its first worksheet

```csharp
// Initialize a new workbook – this represents the Excel file
Workbook workbook = new Workbook();

// The first worksheet is created by default
Worksheet worksheet = workbook.Worksheets[0];
```

**Explanation:**  
`Workbook` is the root object; `Worksheets[0]` gives you the default sheet where the data will be placed.

## Step 3: Prepare a distinct style for each column (alternating background colors)

To achieve **alternating column colors excel**, we generate a `Style` for every column and assign a light background color that flips between two shades.

```csharp
// Determine how many columns we have
int columnCount = dataTable.Columns.Count;
Style[] columnStyles = new Style[columnCount];

// Create a style for each column
for (int i = 0; i < columnCount; i++)
{
    // Create a fresh style instance
    Style style = workbook.CreateStyle();

    // Alternate between LightYellow and LightCyan
    style.ForegroundColor = (i % 2 == 0)
        ? System.Drawing.Color.LightYellow
        : System.Drawing.Color.LightCyan;

    // Use a solid fill pattern
    style.Pattern = BackgroundType.Solid;

    columnStyles[i] = style;
}
```

**Why we use a loop:**  
The loop guarantees that **set cell background color c#** is applied consistently, even if the number of columns changes at runtime. This makes the solution robust for dynamic reports.

## Step 4: Import the `DataTable` into the worksheet, applying the column styles

Aspose.Cells can import a `DataTable` directly, and we can pass the array of styles to color each column.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// The second argument (true) tells the API to add column headers
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**What happens under the hood:**  
`ImportDataTable` writes the header row, then each data row. Because we supplied `columnStyles`, every cell in a given column receives the corresponding style, giving us the desired alternating colors.

## Step 5: Save the styled workbook to a file

```csharp
// Choose an output path – adjust as needed for your environment
string outputPath = @"C:\Temp\StyledTable.xlsx";
workbook.Save(outputPath);

Console.WriteLine($"Workbook saved to {outputPath}");
```

When you open *StyledTable.xlsx* in Excel you’ll see each column shaded alternately, making the table easier to read.

## Full, runnable example

Putting all the pieces together, here is a self‑contained program you can copy, paste, and run.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Get the source data
        DataTable dataTable = GetData();

        // Step 2: Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Build alternating column styles
        int columnCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++)
        {
            Style style = workbook.CreateStyle();
            style.ForegroundColor = (i % 2 == 0)
                ? System.Drawing.Color.LightYellow
                : System.Drawing.Color.LightCyan;
            style.Pattern = BackgroundType.Solid;
            columnStyles[i] = style;
        }

        // Step 4: Import DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // Step 5: Save the file
        string outputPath = @"C:\Temp\StyledTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetData()
    {
        DataTable table = new DataTable("Students");
        table.Columns.Add("Id", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        for (int i = 1; i <= 5; i++)
        {
            table.Rows.Add(i, $"Student {i}", 60 + i * 5);
        }
        return table;
    }
}
```

### Expected output

* A file named **StyledTable.xlsx** located at `C:\Temp\`.
* The worksheet shows three columns (`Id`, `Name`, `Score`) with alternating background colors: columns 1 and 3 in *LightYellow*, column 2 in *LightCyan*.
* All rows from the `DataTable` appear beneath the header row.

## Common questions and edge cases

| Question | Answer |
|----------|--------|
| *Can I use other colors?* | Yes. Replace `System.Drawing.Color.LightYellow` and `LightCyan` with any `System.Drawing.Color` value. |
| *What if the DataTable has many columns?* | The loop automatically creates a style for each column, so the pattern scales without code changes. |
| *Do I need to dispose of the workbook?* | Aspose.Cells implements `IDisposable`. If you wrap the `Workbook` in a `using` block, resources are released promptly. |
| *How to apply the same alternating colors to rows instead of columns?* | Create a `Style[]` for rows and call `worksheet.Cells.ImportDataTable(..., rowStyles)` – Aspose.Cells overloads support both. |
| *Can I write the file directly to a stream (e.g., for a web API)?* | Yes. Use `workbook.Save(stream, SaveFormat.Xlsx);` instead of a file path. |

## Tips from the field

* **Pro tip:** Cache the style objects if you generate many worksheets in a single run – creating a style is relatively cheap, but reusing them reduces memory churn.  
* **Watch out for:** When using `System.Drawing.Color` on non‑Windows platforms, add the `System.Drawing.Common` NuGet package and ensure the runtime supports GDI+.

## Conclusion

You now know how to **alternating column colors excel** by creating an Excel file from a `DataTable` in C#, setting cell background colors with Aspose.Cells, and **import datatable to excel** with a styled column array. This approach is fast, maintainable, and works with any size of data set.

### Next steps

* Explore **set cell background color c#** for conditional formatting (e.g., highlight low scores).  
* Combine this technique with **create excel file from datatable c#** to generate multi‑sheet reports.  
* Look into Aspose.Cells’ charting API to add visual summaries to the same workbook.

Feel free to adapt the colors, file format, or data source to match your project’s needs. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Set Column Background in Excel with C# – Complete Guide](/cells/english/net/excel-colors-and-background-settings/set-column-background-in-excel-with-c-complete-guide/)
- [Add background color excel – Alternating Row Styles in C#](/cells/english/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/)
- [Create Workbook C# – Import DataTable to Excel with Styles](/cells/english/net/excel-data-import-export/create-workbook-c-import-datatable-to-excel-with-styles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}