---
category: general
date: 2026-02-21
description: Learn how to style columns when you import a DataTable to Excel using
  C#. Includes tips to color second column Excel and import datatable excel c#.
draft: false
keywords:
- how to style columns
- import datatable to excel
- how to import datatable
- color second column excel
- import datatable excel c#
language: en
og_description: How to style columns when importing a DataTable to Excel using C#.
  Step‑by‑step code, color second column Excel, and best practices.
og_title: How to Style Columns in Excel with C# – Complete Guide
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: How to Style Columns in Excel with C# – Import DataTable
url: /net/excel-formatting-and-styling/how-to-style-columns-in-excel-with-c-import-datatable/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Style Columns in Excel with C# – Import DataTable

Ever wondered **how to style columns** in an Excel worksheet while pulling data straight from a `DataTable`? You're not the only one. Many developers hit a wall when they need a quick splash of color—maybe red for the first column, blue for the second—without manually fiddling with each cell after the import.  

The good news? The answer is a handful of lines of C# code, and you’ll have a fully‑styled sheet the moment the data lands. In this tutorial we’ll also cover **import datatable to excel**, show you **color second column excel**, and explain why the approach works for both .NET Framework and .NET 6+ projects.

---

## What You’ll Learn

- Retrieve a populated `DataTable` (or create one on the fly).  
- Define per‑column `Style` objects to set foreground colors.  
- Create a workbook, grab the first worksheet, and import the table with styles applied.  
- Handle edge cases like empty tables, custom start rows, and dynamic column counts.  

By the end, you’ll be able to drop a styled Excel file into any reporting pipeline—no post‑processing required.

> **Prerequisite:** Basic familiarity with C# and a reference to a spreadsheet library that supports `ImportDataTable` (e.g., Aspose.Cells, GemBox.Spreadsheet, or EPPlus with a helper). The code below uses **Aspose.Cells** because its `ImportDataTable` overload directly accepts a `Style[]`.

---

## Step 1: Set Up the Project and Add the Excel Library

Before we can style anything, we need a project that references an Excel manipulation library.

```csharp
// Install-Package Aspose.Cells -Version 24.7
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;   // For Color
```

*Pro tip:* If you’re on .NET 6, add the package via `dotnet add package Aspose.Cells`. The library works on Windows, Linux, and macOS, so you’re future‑proof.

---

## Step 2: Retrieve or Build the Source DataTable

The tutorial’s core focuses on styling, but you still need a `DataTable`. Below is a quick helper that creates sample data; replace it with your own `GetTable()` call in production.

```csharp
/// <summary>
/// Returns a DataTable with three columns and five rows of demo data.
/// </summary>
static DataTable GetTable()
{
    var dt = new DataTable("Demo");
    dt.Columns.Add("ID", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Score", typeof(double));

    dt.Rows.Add(1, "Alice", 92.5);
    dt.Rows.Add(2, "Bob", 85.3);
    dt.Rows.Add(3, "Charlie", 78.9);
    dt.Rows.Add(4, "Diana", 88.1);
    dt.Rows.Add(5, "Ethan", 91.4);

    return dt;
}
```

> **Why this matters:** Using a `DataTable` keeps your data source agnostic—whether it comes from SQL, CSV, or an in‑memory collection, the import logic stays the same. This is the cornerstone of **how to import datatable** efficiently.

---

## Step 3: Define Column Styles (The Heart of “How to Style Columns”)

Now we tell the worksheet how each column should look. The `Style` class lets you set fonts, colors, borders, and more. For this example we only change the foreground color.

```csharp
// Step 3: Define column styles – red for first, blue for second, default for others
Style[] columnStyles = new Style[3]; // Assuming three columns; adjust as needed

// Style for column 0 (first column) – red text
columnStyles[0] = new Style();
columnStyles[0].ForegroundColor = Color.Red;

// Style for column 1 (second column) – blue text
columnStyles[1] = new Style();
columnStyles[1].ForegroundColor = Color.Blue;

// Column 2 (third column) – keep default styling
columnStyles[2] = new Style(); // No changes, but array entry required
```

*What if you have more columns?* Just increase the array size and fill in the styles you care about. Unstyled columns automatically inherit the worksheet’s default style.

---

## Step 4: Create the Workbook and Import the DataTable with Styles

With data and styles ready, it’s time to bring everything together.

```csharp
static void Main()
{
    // Retrieve the data
    DataTable dataTable = GetTable();

    // Initialize a new workbook (in‑memory)
    Workbook workbook = new Workbook();

    // Grab the first worksheet (index 0)
    Worksheet worksheet = workbook.Worksheets[0];

    // Import the DataTable starting at cell A1 (row 0, column 0)
    // The 'true' flag tells Aspose.Cells to include column headers
    worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

    // Optional: Auto‑fit columns for a cleaner look
    worksheet.AutoFitColumns();

    // Save the result to disk
    string outputPath = "StyledDataTable.xlsx";
    workbook.Save(outputPath);

    Console.WriteLine($"Excel file saved to {outputPath}");
}
```

**What just happened?**  
- `ImportDataTable` copies rows, columns, and *optionally* the header row.  
- By passing `columnStyles`, each column receives the `Style` we defined earlier.  
- The call is a single line, which means **import datatable excel c#** is as simple as that.

---

## Step 5: Verify the Result – Expected Output

Open `StyledDataTable.xlsx` in Excel (or LibreOffice). You should see:

| **ID** (red) | **Name** (blue) | **Score** (default) |
|--------------|-----------------|----------------------|
| 1            | Alice           | 92.5                 |
| 2            | Bob             | 85.3                 |
| …            | …               | …                    |

- The first column’s text appears in **red**, satisfying the “how to style columns” requirement.  
- The second column’s text is **blue**, which also covers the **color second column excel** query.  

If the file opens without errors, you’ve successfully mastered **how to import datatable** while styling columns.

---

## Common Questions & Edge Cases

### What if the DataTable is empty?
`ImportDataTable` will still create the header row (if you passed `true`). No data rows are added, but the styles still apply to the header cells.

### Need to start the import at a different cell?
Change the `rowIndex` and `columnIndex` parameters in `ImportDataTable`. For example, to start at `B2` use `1, 1` instead of `0, 0`.

### Want to style rows instead of columns?
You can loop through `worksheet.Cells.Rows` after import and assign a `Style` per row. However, column‑level styling is far more performant because the library applies the style once per column.

### Using EPPlus or ClosedXML?
Those libraries don’t expose a direct `ImportDataTable` overload with a style array. The workaround is to import the table first, then iterate over the column range and set `Style.Font.Color.SetColor(...)`. The logic remains the same, just a few extra lines.

---

## Pro Tips for Production‑Ready Code

- **Reuse Styles:** Creating a new `Style` for every column can be wasteful. Store reusable styles in a dictionary keyed by color or font weight.  
- **Avoid Hard‑Coded Column Counts:** Detect `dataTable.Columns.Count` and build the `columnStyles` array dynamically.  
- **Thread Safety:** If you generate many workbooks in parallel, instantiate a separate `Workbook` per thread; Aspose.Cells objects aren’t thread‑safe.  
- **Performance:** For tables larger than 10 k rows, consider disabling `AutoFitColumns` (it scans every cell) and set column widths manually.

---

## Full Working Example (Copy‑Paste Ready)

```csharp
// ------------------------------------------------------------
// Full example: How to style columns while importing a DataTable
// ------------------------------------------------------------
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetTable();

        // 2️⃣ Define per‑column styles
        int colCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[colCount];

        // Red for first column
        columnStyles[0] = new Style { ForegroundColor = Color.Red };

        // Blue for second column (if it exists)
        if (colCount > 1)
            columnStyles[1] = new Style { ForegroundColor = Color.Blue };

        // Default style for remaining columns
        for (int i = 2; i < colCount; i++)
            columnStyles[i] = new Style(); // no special formatting

        // 3️⃣ Create workbook and import with styles
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
        sheet.AutoFitColumns();

        // 4️⃣ Save to file
        string path = "StyledDataTable.xlsx";
        workbook.Save(path);
        Console.WriteLine($"File saved: {path}");
    }

    // Helper: sample DataTable
    static DataTable GetTable()
    {
        var dt = new DataTable("Demo");
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        dt.Rows.Add(1, "Alice", 92.5);
        dt.Rows.Add(2, "Bob", 85.3);
        dt.Rows.Add(3, "Charlie", 78.9);
        dt.Rows.Add(4, "Diana", 88.1);
        dt.Rows.Add(5, "Ethan", 91.4);
        return dt;
    }
}
```

Run the program, open the generated `StyledDataTable.xlsx`, and you’ll see the colored columns instantly. That’s the entire **import datatable excel c#** workflow in a nutshell.

---

## Conclusion

We’ve just covered **how to style columns** when you **import datatable to excel** using C#. By defining a `Style[]` array and passing it to `ImportDataTable`, you can color the first column red, the second column blue, and leave the rest untouched—all in a single line of code.  

The approach scales: add more `Style` objects for additional columns, adjust start rows, or swap out Aspose.Cells for another library with a similar API. Now you can generate polished Excel reports without ever touching the file manually.

**Next steps** you might explore:

- Use **conditional formatting** to highlight values dynamically (ties into “color second column excel”).  
- Export multiple worksheets from a single `DataTable` set (great for monthly dashboards).  
- Combine this with **CSV → DataTable** conversion to build an end‑to‑

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}