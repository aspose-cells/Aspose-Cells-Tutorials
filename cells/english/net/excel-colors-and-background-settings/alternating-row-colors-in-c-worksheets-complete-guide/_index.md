---
category: general
date: 2026-05-30
description: Learn how to add alternating row colors in C# worksheets, set cell background
  with a solid fill pattern, and customize worksheet cell style effortlessly.
draft: false
keywords:
- alternating row colors
- set cell background
- solid fill pattern
- add background color
- worksheet cell style
language: en
og_description: Alternating row colors in C# worksheets made easy. Learn to set cell
  background, use a solid fill pattern, and master worksheet cell style.
og_title: Alternating Row Colors in C# Worksheets – Complete Guide
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  headline: Alternating Row Colors in C# Worksheets – Complete Guide
  type: TechArticle
- description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  name: Alternating Row Colors in C# Worksheets – Complete Guide
  steps:
  - name: Why Use a **Solid Fill Pattern**?
    text: The `Pattern` property tells the engine how to render the color. A `Solid`
      fill guarantees that the entire cell background is painted, eliminating any
      faint gridlines that might otherwise show through. This is the most common way
      to **set cell background** when you want a clean look.
  - name: Change the Colors
    text: 'If your brand uses different hues, just replace `Color.LightYellow` and
      `Color.LightCyan` with any `System.Drawing.Color` you prefer. For example:'
  - name: Use a Different **Background Type**
    text: While `BackgroundType.Solid` is the most common, you can experiment with
      `BackgroundType.Gray125`, `BackgroundType.Horizontal`, or any pattern that the
      library supports. This changes the visual texture while still **adding background
      color**.
  - name: Apply a **Worksheet Cell Style** to Specific Columns
    text: 'Sometimes you only want the alternating effect on data columns, leaving
      the first column (e.g., IDs) untouched. Create a separate style for that column
      and assign it after the import:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Alternating Row Colors in C# Worksheets – Complete Guide
url: /net/excel-colors-and-background-settings/alternating-row-colors-in-c-worksheets-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Alternating Row Colors in C# Worksheets – Complete Guide

Ever wondered how to make your Excel export look polished by using **alternating row colors**? You’re not alone—developers constantly ask how to *add background color* to rows without writing a million lines of code.  

In this tutorial we’ll walk through a straightforward way to **set cell background** on each row, apply a **solid fill pattern**, and control the **worksheet cell style** so the result is both readable and visually appealing.

## What You’ll Learn

- Retrieve data into a `DataTable` (or any tabular source).  
- Build an array of `Style` objects that alternate between two colors.  
- Import the `DataTable` into a worksheet while applying those styles.  
- Verify the output and tweak the colors or patterns if needed.  

No external tools beyond a .NET environment and a spreadsheet library (we’ll use **Aspose.Cells** in the examples) are required. By the end you’ll have a reusable method that you can drop into any reporting pipeline.

---

## Step 1: Retrieve the Source Data as a `DataTable`

First things first—without data there’s nothing to style. Below is a tiny helper that builds a `DataTable` with sample rows. In a real project you’d replace this with a database call or CSV parser.

```csharp
using System;
using System.Data;

static DataTable GetData()
{
    // Create a simple table with three columns
    DataTable table = new DataTable("Report");
    table.Columns.Add("ID", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with dummy rows
    for (int i = 1; i <= 10; i++)
    {
        table.Rows.Add(i, $"Item {i}", Math.Round(new Random().NextDouble() * 100, 2));
    }

    return table;
}
```

> **Why this matters:** Having the data in a `DataTable` lets the worksheet engine *import* it in one call, preserving column names and data types automatically.

## Step 2: Create **Alternating Row Colors** Styles

Now we’ll generate an array of `Style` objects—one per row—so that even rows get a light yellow shade while odd rows receive a gentle cyan. This is the core of the **alternating row colors** technique.

```csharp
using Aspose.Cells;
using System.Drawing;

// Assume workbook and worksheet are already instantiated
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Retrieve data
DataTable dataTable = GetData();

// Prepare an array of styles – one for each row in the table
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style for the current row
    rowStyles[i] = workbook.CreateStyle();

    // **Add background color**: LightYellow for even rows, LightCyan for odd rows
    rowStyles[i].ForegroundColor = (i % 2 == 0)
        ? Color.LightYellow
        : Color.LightCyan;

    // **Set cell background** using a **solid fill pattern**
    rowStyles[i].Pattern = BackgroundType.Solid;

    // Optional: you could also set font color, borders, etc., here
}
```

### Why Use a **Solid Fill Pattern**?

The `Pattern` property tells the engine how to render the color. A `Solid` fill guarantees that the entire cell background is painted, eliminating any faint gridlines that might otherwise show through. This is the most common way to **set cell background** when you want a clean look.

## Step 3: Import the `DataTable` with the Prepared Styles

With the style array ready, the import call becomes a one‑liner. Aspose.Cells will apply the corresponding style to each row automatically.

```csharp
// Import the DataTable into the worksheet, applying the prepared styles
worksheet.Cells.ImportDataTable(
    dataTable,                     // source
    true,                          // include column names
    0,                             // start row (0‑based)
    0,                             // start column (0‑based)
    rowStyles);                    // array of styles
```

> **What happens under the hood?**  
> The library iterates over each row, copies the values into cells, and then applies the matching `Style` from `rowStyles`. Because we already defined a **solid fill pattern**, every cell in a row inherits the same background color, giving you perfect **alternating row colors**.

## Step 4: Save the Workbook and Verify the Result

A quick save lets you open the file in Excel (or any compatible viewer) and see the effect.

```csharp
// Save to disk – you can change the format to .xlsx, .xls, .csv, etc.
workbook.Save("AlternatingRowsReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved. Open 'AlternatingRowsReport.xlsx' to see the result.");
```

When you open the file, rows 1, 3, 5… will be light yellow, while rows 2, 4, 6… will be light cyan. The column headers stay white, making the data stand out.

![Worksheet showing alternating row colors](/images/alternating-row-colors.png "Screenshot of worksheet with alternating row colors")

*Image alt text:* **alternating row colors** screenshot of a worksheet where each row’s background alternates between light yellow and light cyan.

## Step 5: Customizing Further (Optional)

### Change the Colors

If your brand uses different hues, just replace `Color.LightYellow` and `Color.LightCyan` with any `System.Drawing.Color` you prefer. For example:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.FromArgb(255, 235, 205) // Peach
                                            : Color.FromArgb(205, 235, 255); // Soft blue
```

### Use a Different **Background Type**

While `BackgroundType.Solid` is the most common, you can experiment with `BackgroundType.Gray125`, `BackgroundType.Horizontal`, or any pattern that the library supports. This changes the visual texture while still **adding background color**.

### Apply a **Worksheet Cell Style** to Specific Columns

Sometimes you only want the alternating effect on data columns, leaving the first column (e.g., IDs) untouched. Create a separate style for that column and assign it after the import:

```csharp
Style idStyle = workbook.CreateStyle();
idStyle.ForegroundColor = Color.White;
idStyle.Pattern = BackgroundType.Solid;

// Apply to the first column (A)
for (int row = 0; row < dataTable.Rows.Count + 1; row++) // +1 for header
{
    worksheet.Cells[row, 0].SetStyle(idStyle);
}
```

---

## Conclusion

You now have a complete, reusable solution for **alternating row colors** in C# worksheets. By building an array of `Style` objects, **setting cell background** with a **solid fill pattern**, and importing a `DataTable` in one call, you can produce professional‑looking reports with minimal code.  

From here you might:

- **Add background color** to header rows for extra emphasis.  
- Combine the technique with conditional formatting for dynamic visual cues.  
- Explore other **worksheet cell style** properties like fonts, borders, or number formats.

Give it a try in your next export routine—your users will thank you for the cleaner, more readable spreadsheets. Happy coding!


## What Should You Learn Next?

- [Set Row Height in Worksheet with Aspose.Cells for .NET](/cells/english/net/size-and-spacing-customization/setting-height-of-all-rows-in-worksheet/)
- [Convert Excel Cell Names to Row and Column Indices Using Aspose.Cells for .NET](/cells/english/net/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-dotnet/)
- [Set Worksheet Tab Colors in Excel Using Aspose.Cells .NET - A Comprehensive Guide](/cells/english/net/worksheet-management/set-worksheet-tab-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}