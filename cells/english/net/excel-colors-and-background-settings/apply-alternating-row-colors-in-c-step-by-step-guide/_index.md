---
category: general
date: 2026-03-18
description: Learn how to apply alternating row colors in a worksheet using C#. Includes
  set row background color, add light yellow background, and color rows alternately.
draft: false
keywords:
- apply alternating row colors
- set row background color
- add light yellow background
- set alternating row shading
- color rows alternately
language: en
og_description: Apply alternating row colors in C# to improve readability. This guide
  shows how to set row background color, add light yellow background, and color rows
  alternately.
og_title: Apply Alternating Row Colors in C# – Complete Tutorial
tags:
- C#
- DataTable
- Spreadsheet styling
- UI design
title: Apply Alternating Row Colors in C# – Step‑by‑Step Guide
url: /net/excel-colors-and-background-settings/apply-alternating-row-colors-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Apply Alternating Row Colors in C# – Complete Tutorial

Ever needed to **apply alternating row colors** to a data‑driven worksheet but weren’t sure where to start? You’re not the only one — most developers hit that snag when they first try to make tables look a bit friendlier. The good news? In just a few lines of C# you can **set row background color**, sprinkle in an **add light yellow background**, and end up with a polished grid that instantly improves readability.

In this tutorial we’ll walk through the whole process, from pulling a `DataTable` into memory to styling each row with a subtle yellow‑white stripe. By the end you’ll be able to **color rows alternately** with confidence, and you’ll also see a few handy variations for when you need different shades or dynamic theming.

## What You’ll Need

Before we dive in, make sure you have the following on hand:

- A .NET project targeting .NET 6 or later (the code works on .NET Framework 4.7+ as well).  
- A spreadsheet library that supports style objects – the example uses a generic `Workbook`/`Worksheet` API that mirrors libraries like **Aspose.Cells**, **GemBox.Spreadsheet**, or **ClosedXML**.  
- A `DataTable` source – could be from a database query, CSV import, or any in‑memory collection.  

No extra NuGet packages beyond the spreadsheet library itself. If you’re using Aspose.Cells, the namespace is `Aspose.Cells`; for ClosedXML it’s `ClosedXML.Excel`. Swap the `CreateStyle` and `ImportDataTable` calls accordingly.

## Step 1: Retrieve the Source Data as a DataTable

First thing’s first—grab the data you want to display. In real‑world apps this usually means hitting a database, but for clarity we’ll stub a helper method called `GetData()` that returns a populated `DataTable`.

```csharp
// Step 1: Retrieve the source data as a DataTable
DataTable dataTable = GetData();   // Replace with your actual data retrieval logic
```

> **Why this matters:** The `DataTable` defines the rows and columns that later receive the alternating shading. If the table is empty, there’s nothing to style, so always verify that `Rows.Count` > 0 before proceeding.

### Pro tip
If you’re pulling data from Entity Framework, you can use `DataTable.Load(reader)` after executing a `SqlCommand`. That keeps the code tidy and avoids manual column definitions.

## Step 2: Allocate an Array to Hold a Style for Each Row

Next, we need a container that matches the number of rows. Most spreadsheet APIs let you pass a style array to the import method, so we’ll create a `Style[]` sized exactly to the row count.

```csharp
// Step 2: Allocate an array to hold a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];
```

> **Explanation:** By pre‑allocating the array, we avoid reallocating a new style object on every iteration, which can be a performance win when dealing with thousands of rows.

## Step 3: Apply Alternating Row Colors (Light Yellow / White)

Now comes the heart of the matter: **apply alternating row colors**. We’ll loop through each row, create a fresh style instance from the workbook, and set its background based on the row index. Even rows get a light yellow fill, odd rows stay white.

```csharp
// Step 3: Create alternating background colors (light yellow / white) for the rows
for (int rowIndex = 0; rowIndex < dataTable.Rows.Count; rowIndex++)
{
    // Create a new style instance from the workbook
    rowStyles[rowIndex] = wb.CreateStyle();

    // Apply a light yellow background to even rows, white to odd rows
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow   // add light yellow background
        : Color.White;        // set row background color to white

    rowStyles[rowIndex].Pattern = BackgroundType.Solid; // set alternating row shading
}
```

### Why this works
- **`rowIndex % 2 == 0`** checks whether the row is even.  
- **`Color.LightYellow`** gives a gentle, non‑intrusive hue that’s perfect for data tables.  
- **`BackgroundType.Solid`** ensures the fill covers the whole cell, achieving the **set row background color** effect.  

You can swap `Color.LightYellow` with any other shade (e.g., `Color.LightCyan`) if you prefer a different look. The same logic also lets you **color rows alternately** based on other criteria, such as status flags.

## Step 4: Import the DataTable into the Worksheet with the Prepared Styles

Finally, we push everything into the worksheet. Most libraries expose an `ImportDataTable` overload that accepts a style array. The `true` flag tells the API to write column headers, and the `0, 0` coordinates start at the top‑left cell.

```csharp
// Step 4: Import the DataTable into the worksheet, applying the prepared row styles
ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

> **Result:** The worksheet now displays your data with a clean **alternating row shading** pattern—light yellow on even rows, white on odd rows. Users can scan the grid without their eyes hopping back and forth.

### Expected Output
If you opened the resulting spreadsheet, you’d see something like this:

| ID | Name      | Quantity |
|----|-----------|----------|
| **1** | Apple      | 50       |
| **2** | Banana     | 30       |
| **3** | Cherry     | 20       |
| **4** | Date       | 15       |

Rows 1, 3, 5… have a **light yellow background**, while rows 2, 4, 6… remain **white**. The header row (row 0) inherits the default style unless you customize it separately.

## Optional Variations & Edge Cases

### 1. Using a Different Color Palette
If light yellow clashes with your branding, simply replace `Color.LightYellow` with another `System.Drawing.Color`. For a blue‑gray theme you might use:

```csharp
rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
    ? Color.FromArgb(220, 235, 247) // soft blue
    : Color.White;
```

### 2. Dynamic Shading Based on Data
Sometimes you want to highlight rows that meet a condition (e.g., low inventory). Combine the modulo check with a custom test:

```csharp
int quantity = Convert.ToInt32(dataTable.Rows[rowIndex]["Quantity"]);
if (quantity < 20)
{
    rowStyles[rowIndex].ForegroundColor = Color.Salmon; // urgent low‑stock color
}
else
{
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow
        : Color.White;
}
```

### 3. Applying Styles to Specific Columns Only
If you only need the **set row background color** on certain columns, create a separate style for each column and assign it after the import using the worksheet’s cell range API.

```csharp
// Example for column B only
var colBStyle = wb.CreateStyle();
colBStyle.ForegroundColor = Color.LightYellow;
colBStyle.Pattern = BackgroundType.Solid;

// Apply after import
ws.Cells[$"B2:B{dataTable.Rows.Count + 1}"].SetStyle(colBStyle);
```

### 4. Performance Tip for Large Tables
When dealing with > 10,000 rows, consider reusing a single style object for each color instead of creating a new one per row. The array then holds references to the two shared styles, dramatically cutting memory usage.

```csharp
Style yellowStyle = wb.CreateStyle();
yellowStyle.ForegroundColor = Color.LightYellow;
yellowStyle.Pattern = BackgroundType.Solid;

Style whiteStyle = wb.CreateStyle();
whiteStyle.ForegroundColor = Color.White;
whiteStyle.Pattern = BackgroundType.Solid;

for (int i = 0; i < dataTable.Rows.Count; i++)
    rowStyles[i] = (i % 2 == 0) ? yellowStyle : whiteStyle;
```

## Full Working Example

Below is a self‑contained program you can paste into a console app. It uses a fictitious `Workbook`/`Worksheet` API; replace the types with those from your chosen library.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using YourSpreadsheetLib;     // Replace with actual namespace

class Program
{
    static void Main()
    {
        // Initialize workbook & worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Step 1: Retrieve data
        DataTable dataTable = GetData();

        // Step 2: Allocate style array
        Style[] rowStyles = new Style[dataTable.Rows.Count];

        // Step 3: Apply alternating row colors
        for (int i = 0; i < dataTable.Rows.Count; i++)
        {
            rowStyles[i] = wb.CreateStyle();
            rowStyles[i].ForegroundColor = (i % 2 == 0)
                ? Color.LightYellow   // add light yellow background
                : Color.White;        // set row background color
            rowStyles[i].Pattern = BackgroundType.Solid; // set alternating row shading
        }

        // Step 4: Import with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // Save to file
        wb.Save("AlternatingRows.xlsx");
        Console.WriteLine("Workbook saved with alternating row colors.");
    }

    // Sample data generator
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(1, "Apple", 50);
        dt.Rows.Add(2, "Banana", 30);
        dt.Rows.Add(3, "Cherry", 20);
        dt.Rows.Add(4, "Date", 15);
        dt.Rows.Add(5, "Elderberry", 5);
        return dt;
    }
}
```

**Output:** A file named `AlternatingRows.xlsx` where each row alternates between a light yellow fill and white, making the table easier on the eyes.

## Frequently Asked Questions

**Q: Does this approach work with Excel‑style conditional formatting?**  
A: Yes. If your library supports conditional rules, you can translate the same logic into a rule that checks `MOD(ROW(),2)=0`. The code‑based method shown here is more portable across libraries that lack built‑in conditional formatting.

**Q: What if I need to **color rows alternately** in a PDF table instead of an Excel sheet?**  
A: Most PDF table generators (e.g., iTextSharp, PdfSharp) let you set a `BackgroundColor` per row. The same modulo calculation applies—

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}