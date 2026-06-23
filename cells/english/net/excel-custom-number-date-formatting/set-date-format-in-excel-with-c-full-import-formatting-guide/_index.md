---
category: general
date: 2026-06-17
description: Set date format in Excel using C# and also set cell background, apply
  foreground color, and color Excel column during import. Learn step‑by‑step.
draft: false
keywords:
- set date format
- set cell background
- apply foreground color
- color excel column
- excel import formatting
language: en
og_description: Set date format in Excel with C# while setting cell background, applying
  foreground color, and coloring Excel column during import. Full tutorial.
og_title: Set date format in Excel with C# – Complete Guide
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  headline: Set date format in Excel with C# – Full Import Formatting Guide
  type: TechArticle
- description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  name: Set date format in Excel with C# – Full Import Formatting Guide
  steps:
  - name: 2.1 Set Date Format for the First Column
    text: The first column (`OrderDate`) should display as “MM/dd/yyyy”. Aspose uses
      the built‑in number format index 14 for the short date, but you can also supply
      a custom format string if you prefer.
  - name: 2.2 Set Cell Background for the Second Column
    text: Let’s give the `CustomerName` column a light blue background. This is where
      **set cell background** comes into play.
  - name: 2.3 Apply Foreground (Text) Color – Optional Extra
    text: 'If you also want the text itself to be a contrasting color, you can tweak
      the same style:'
  - name: 3.1 Save the Workbook
    text: '```csharp // Save to a file – change path as needed wb.Save("FormattedReport.xlsx",
      SaveFormat.Xlsx); Console.WriteLine("Excel file created with date format and
      colors."); ```'
  - name: What if I have more than two columns?
    text: Just expand the `columnStyles` array and assign a `Style` to each index
      you care about. Unassigned indexes will fall back to the default style, which
      is perfectly fine.
  - name: How do I format a column as currency?
    text: '```csharp columnStyles[3] = wb.CreateStyle(); columnStyles[3].Number =
      164; // Built‑in currency format (e.g., $#,##0.00) ```'
  - name: Can I change the header row style separately?
    text: 'Yes. After the import, you can grab the first row and apply a distinct
      style:'
  - name: What if the DataTable contains null dates?
    text: 'Aspose will leave those cells blank. If you prefer a placeholder like “N/A”,
      you can preprocess the table:'
  type: HowTo
tags:
- excel
- csharp
- aspnet
- data-import
title: Set date format in Excel with C# – Full Import Formatting Guide
url: /net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Set date format in Excel with C# – Full Import Formatting Guide

Ever needed to **set date format** in an Excel sheet generated from C# code, but also wanted the column to have a custom background or text color? You're not the only one. In many reporting scenarios you pull a `DataTable` from a database, drop it into a worksheet, and then scramble to make the dates look right and the columns pop with the right colors.  

In this tutorial we’ll walk through a clean, end‑to‑end solution that **sets date format**, **sets cell background**, **applies foreground color**, and even **colors an Excel column** while importing data. By the end you’ll have a reusable pattern that handles **excel import formatting** without the usual trial‑and‑error.

> **What you’ll need**  
> * .NET 6+ (or .NET Framework 4.7+)  
> * Aspose.Cells for .NET (free trial works for testing)  
> * A `DataTable` source – any ADO.NET query will do  
> * Visual Studio or your favorite IDE  

Let’s get cracking.

---

## Overview of the Solution

We’ll break the problem into three logical chunks:

1. **Retrieve the source data** – a `DataTable` with rows you want to export.  
2. **Create column‑specific styles** – one style for the date column, another for a text column, plus any extra styling you’d like.  
3. **Import the table with styles** – use `Worksheet.Cells.ImportDataTable` so each column inherits the style you prepared.

Why this approach? Because Aspose.Cells lets you attach a `Style` array directly to the `ImportDataTable` call, meaning you don’t need a second pass to re‑apply formatting. It’s faster, less error‑prone, and keeps your code tidy.

---

## Step 1: Retrieve the Data to Export

First things first – you need a `DataTable`. In a real project you’d probably call a stored procedure or use Entity Framework to fill it, but for illustration we’ll mock a simple table with a date and a text column.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("OrderDate", typeof(DateTime));
    table.Columns.Add("CustomerName", typeof(string));

    // Sample rows – replace with your DB call
    table.Rows.Add(DateTime.Today.AddDays(-2), "Acme Corp");
    table.Rows.Add(DateTime.Today.AddDays(-1), "Globex Inc");
    table.Rows.Add(DateTime.Today, "Soylent Co");

    return table;
}
```

> **Pro tip:** If your source uses nullable dates, make sure the column type is `typeof(DateTime?)` – Aspose will still respect the format you assign later.

---

## Step 2: Prepare an Array of Styles – One per Column

Now we create a `Style[]` whose length matches the number of columns in the `DataTable`. Each entry will hold the formatting for its respective column.

```csharp
// Create a new workbook and get the first worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Pull the data
DataTable dataTable = GetData();

// Allocate the style array
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

### 2.1 Set Date Format for the First Column

The first column (`OrderDate`) should display as “MM/dd/yyyy”. Aspose uses the built‑in number format index 14 for the short date, but you can also supply a custom format string if you prefer.

```csharp
// Style for the date column (index 0)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Built‑in short date format
// Or a custom pattern:
// columnStyles[0].Custom = "mm/dd/yyyy";
```

**Why this matters:** Excel stores dates as serial numbers. By assigning a number format, you tell Excel to render those serials as human‑readable dates instead of raw numbers.

### 2.2 Set Cell Background for the Second Column

Let’s give the `CustomerName` column a light blue background. This is where **set cell background** comes into play.

```csharp
// Style for the text column (index 1)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightBlue;
columnStyles[1].Pattern = BackgroundType.Solid; // Needed to show the color
```

> **Note:** Without setting `Pattern` to `Solid`, the foreground color won’t appear because the default pattern is “None”.

### 2.3 Apply Foreground (Text) Color – Optional Extra

If you also want the text itself to be a contrasting color, you can tweak the same style:

```csharp
columnStyles[1].Font.Color = System.Drawing.Color.DarkBlue; // apply foreground color
```

That satisfies the **apply foreground color** requirement while keeping the column’s background intact.

---

## Step 3: Import the DataTable with the Defined Styles

With the styles ready, the final step is a single line that imports the data and applies the styles column‑by‑column.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// includeColumnNames = true to add a header row
ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**How it works:** Aspose reads the `columnStyles` array and maps each `Style` to the corresponding column index. The header row inherits the default style unless you supply a separate style for row 0.

### 3.1 Save the Workbook

```csharp
// Save to a file – change path as needed
wb.Save("FormattedReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Excel file created with date format and colors.");
```

Run the program, open *FormattedReport.xlsx*, and you should see:

- **OrderDate** column displayed as dates (e.g., `06/15/2026`).  
- **CustomerName** column with a light‑blue fill and dark‑blue text.  

That’s the whole **excel import formatting** workflow in under 30 lines of C#.

---

## Step‑by‑Step Recap (with Why)

| Step | What you do | Why it matters |
|------|-------------|----------------|
| **Retrieve data** | Call `GetData()` to fill a `DataTable`. | Provides a structured source that Aspose can ingest directly. |
| **Create style array** | Allocate `Style[]` matching column count. | Allows per‑column styling in a single import call. |
| **Set date format** | `columnStyles[0].Number = 14;` | Ensures dates render correctly in Excel. |
| **Set background color** | `ForegroundColor = LightBlue; Pattern = Solid;` | Highlights the column, satisfying **set cell background**. |
| **Apply foreground color** | `Font.Color = DarkBlue;` | Improves readability and meets **apply foreground color**. |
| **Import with styles** | `ImportDataTable(..., columnStyles);` | One‑pass import that respects all formatting. |
| **Save workbook** | `wb.Save(...);` | Persists the result for downstream users. |

---

## Handling Edge Cases & Common Questions

### What if I have more than two columns?

Just expand the `columnStyles` array and assign a `Style` to each index you care about. Unassigned indexes will fall back to the default style, which is perfectly fine.

```csharp
columnStyles[2] = wb.CreateStyle();
columnStyles[2].Number = 0; // General format for numeric columns
```

### How do I format a column as currency?

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 164; // Built‑in currency format (e.g., $#,##0.00)
```

### Can I change the header row style separately?

Yes. After the import, you can grab the first row and apply a distinct style:

```csharp
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = System.Drawing.Color.Gold;
headerStyle.Pattern = BackgroundType.Solid;

ws.Cells.Rows[0].ApplyStyle(headerStyle, new StyleFlag { All = true });
```

### What if the DataTable contains null dates?

Aspose will leave those cells blank. If you prefer a placeholder like “N/A”, you can preprocess the table:

```csharp
foreach (DataRow row in dataTable.Rows)
{
    if (row.IsNull("OrderDate"))
        row["OrderDate"] = DateTime.MinValue; // or any sentinel
}
```

Then adjust the style to display a custom format that shows “N/A” for the sentinel value.

---

## Full Working Example

Below is the complete, copy‑paste‑ready program. Run it as a console app, and you’ll get a nicely formatted Excel file.

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelExportDemo
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Create workbook & style array
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 2a️⃣ Date column – set date format
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // short date (MM/dd/yyyy)

        // 2b️⃣ Text column – set background & foreground colors
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].ForegroundColor = Color.LightBlue;
        columnStyles[1].Pattern = BackgroundType.Solid;
        columnStyles[1].Font.Color = Color.DarkBlue; // apply foreground color

        // 3️⃣ Import with formatting
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // Optional: style header row
        Style headerStyle = wb.CreateStyle();
        headerStyle.Font.IsBold = true;
        headerStyle.ForegroundColor = Color.Gold;
        headerStyle.Pattern = BackgroundType.Solid;
        ws.Cells


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Set Font Color in Excel Cells using Aspose.Cells for .NET](/cells/english/net/formatting/setting-font-color/)
- [Set Font Color in .NET Excel with Aspose.Cells](/cells/english/net/formatting/set-font-color-net-excel-aspose-cells/)
- [Set Excel Column Widths in Pixels Using Aspose.Cells for .NET | Step-by-Step Guide](/cells/english/net/formatting/set-excel-column-width-pixels-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}