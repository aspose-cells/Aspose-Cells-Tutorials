---
category: general
date: 2026-03-01
description: Import data with formatting into Excel using C#. Learn how to import
  DataTable into Excel and add background color to cells in just a few steps.
draft: false
keywords:
- import data with formatting
- how to import datatable into excel
- add background color to excel cells
language: en
og_description: Import data with formatting into Excel using C#. Step‑by‑step guide
  that shows how to import a DataTable and add background color to cells.
og_title: Import Data with Formatting into Excel – C# Guide
tags:
- C#
- Excel
- DataTable
- Formatting
title: Import Data with Formatting into Excel using C#
url: /net/excel-data-import-export/import-data-with-formatting-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Import Data with Formatting into Excel using C#

Ever needed to **import data with formatting** into an Excel workbook but kept getting a plain, boring sheet? You're not alone. Most developers hit that wall when they discover the default import strips all the colors and styles they painstakingly set up in their source data.

In this tutorial we’ll walk through a complete, ready‑to‑run solution that **imports a DataTable into Excel** and **adds background color to Excel cells** at the same time. No extra post‑processing required—your spreadsheet will look exactly the way you want straight out of the box.

## What You’ll Learn

- How to retrieve data into a `DataTable`.
- How to define an array of `Style` objects that carry background colors.
- How to call `ImportDataTable` with those styles so the import preserves formatting.
- A full, runnable example that you can drop into a console app and see the result instantly.
- Tips, pitfalls, and variations for real‑world projects.

### Prerequisites

- .NET 6.0 or later (the code works with .NET Framework 4.6+ as well).
- The **GemBox.Spreadsheet** library (free version is enough for the demo).
- Basic familiarity with C# and Excel concepts.

If you’re wondering *why GemBox?* because it offers a single‑line `ImportDataTable` method that accepts style arrays—exactly what we need to **import data with formatting** without writing a loop.

---

## Step 1: Set Up the Project and Add GemBox.Spreadsheet

To get started, create a new console app:

```bash
dotnet new console -n ExcelImportDemo
cd ExcelImportDemo
dotnet add package GemBox.Spreadsheet
```

> **Pro tip:** The free version limits worksheets to 150 k cells, which is plenty for demos. If you hit the limit, upgrade or switch to EPPlus, but the API will look slightly different.

## Step 2: Retrieve the Source Data as a `DataTable`

The first thing we need is a `DataTable` that mimics the data you’d normally pull from a database. Here’s a tiny helper that creates one in memory:

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register the free license (remove for paid version).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve the source data as a DataTable.
        DataTable dataTable = GetSampleData();

        // Remaining steps will follow...
    }

    /// <summary>
    /// Generates a sample DataTable with three columns and five rows.
    /// In a real app you’d replace this with a DB call.
    /// </summary>
    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

**Why this matters:** By separating data retrieval into its own method, you can swap in any source—SQL, CSV, web service—without touching the import logic. This keeps the code clean and makes the tutorial **how to import datatable into excel** reusable.

## Step 3: Define the Styles You Want to Apply

Now comes the fun part: we’ll create an array of `Style` objects, each with a distinct `ForegroundColor`. GemBox lets you set `BackgroundPatternColor` (the cell fill) and `ForegroundColor` (the text color). For this demo we’ll color the first two columns differently.

```csharp
        // 2️⃣ Define the styles to apply to the imported cells.
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // Column 0 – Light blue fill
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Column 1 – Light green fill
            // No style for column 2 – it will keep the default look.
        };
```

**Explanation:**  
- `Style` objects are lightweight containers; you don’t need to create a new one for every cell.  
- By aligning the order of the array with the column order, GemBox automatically applies the matching style during import.  
- This is the key to **import data with formatting**—the formatting travels with the data, not after the fact.

## Step 4: Import the `DataTable` into the Worksheet with Styles

With the data and styles ready, we can now create a workbook, pick the first worksheet, and call `ImportDataTable`. The method signature looks like this:

```csharp
public void ImportDataTable(
    DataTable dataTable,
    bool includeColumnNames,
    int startRow,
    int startColumn,
    Style[] columnStyles = null);
```

Here’s how we use it:

```csharp
        // 3️⃣ Create a new workbook and import the DataTable.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        // Import, include column headers, start at A1 (0,0), apply our styles.
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the file to disk.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Excel file 'Report.xlsx' created with formatted data.");
```

**What’s happening under the hood?**  
- `true` tells GemBox to write the column names as the first row.  
- `0, 0` positions the import at cell A1.  
- `importStyles` ties each column to the colors we defined earlier.  

When you open *Report.xlsx*, you’ll see the **ID** column shaded light blue, the **Name** column shaded light green, and the **Score** column untouched. That’s **import data with formatting** in a single call.

## Step 5: Verify the Result (Expected Output)

Open the generated `Report.xlsx`. You should see something like this:

| ID (light blue) | Name (light green) | Score |
|-----------------|--------------------|-------|
| 1               | Alice              | 93.5 |
| 2               | Bob                | 78.0 |
| 3               | Charlie            | 85.2 |
| 4               | Diana              | 91.3 |
| 5               | Ethan              | 67.8 |

- The **ID** column cells have a light‑blue background.  
- The **Name** column cells have a light‑green background.  
- The **Score** column remains with the default white background.

That visual cue makes the report instantly scannable—a small touch that can dramatically improve user experience.

![Excel sheet showing import data with formatting – ID column light blue, Name column light green](excel-screenshot.png "import data with formatting example")

*Image alt text includes the primary keyword for SEO.*

---

## Common Questions & Edge Cases

### Can I apply more than just background colors?

Absolutely. `Style` lets you set fonts, borders, number formats, and even conditional formatting. For example, to make scores above 90 bold and red:

```csharp
Style highScoreStyle = new Style()
{
    FontColor = Color.Red,
    FontBold = true
};
worksheet.Cells["C2:C6"].ConditionalFormatting.Add(
    ConditionalFormattingCondition.GreaterThan, "90", highScoreStyle);
```

### What if my DataTable has more columns than styles?

GemBox will apply styles only to the columns that have a matching entry in the array. Extra columns fall back to the default style—no error thrown.

### Does this work with large datasets?

Yes, but keep an eye on the free version’s cell limit (150 k cells). For massive reports, consider the paid license or stream the data row‑by‑row with `worksheet.Cells[row, col].Value = …`—though you’ll lose the one‑liner convenience.

### How do I import data with formatting from an existing Excel template?

You can load a template workbook first:

```csharp
var template = ExcelFile.Load("Template.xlsx");
var targetSheet = template.Worksheets[0];
targetSheet.Cells.ImportDataTable(dataTable, true, 5, 2, importStyles);
template.Save("FilledReport.xlsx");
```

This lets you preserve header logos, footers, and any pre‑existing styles while still **import data with formatting** for the dynamic portion.

---

## Full Working Example (Copy‑Paste Ready)

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register free license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Get the source data.
        DataTable dataTable = GetSampleData();

        // 2️⃣ Define column styles (background colors).
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // ID column
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Name column
            // Score column gets default style.
        };

        // 3️⃣ Create workbook and import with styles.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the result.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Report.xlsx created – import data with formatting complete.");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

Run the program (`dotnet run`) and open the generated *Report.xlsx* to see the colors applied instantly.

---

## Conclusion

You now have a solid, end

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}