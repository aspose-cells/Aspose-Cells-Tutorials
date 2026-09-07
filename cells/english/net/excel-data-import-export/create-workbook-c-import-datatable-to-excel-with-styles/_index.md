---
category: general
date: 2026-02-28
description: Create Workbook C# guide demonstrates how to import DataTable to Excel,
  add custom styles, and export with formatting in just a few clear steps.
draft: false
keywords:
- create workbook c#
- import datatable to excel
- add custom styles excel
- how to import datatable
- export datatable with formatting
language: en
og_description: Create Workbook C# tutorial shows how to import DataTable to Excel,
  apply custom styles, and export with formatting—all in a concise guide.
og_title: Create Workbook C# – Import DataTable to Excel with Styles
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: Create Workbook C# – Import DataTable to Excel with Styles
url: /net/excel-data-import-export/create-workbook-c-import-datatable-to-excel-with-styles/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Workbook C# – Import DataTable to Excel with Styles

Ever needed to **create workbook c#** and wondered how to get your `DataTable` into Excel with proper formatting? In this guide, we’ll walk through **import datatable to excel**, add custom styles, and export the result with full formatting—all using plain C# code you can drop into any project.

We’ll cover everything from pulling data out of a database to styling each column with alternating font colors. By the end, you’ll have a reusable snippet that not only **import datatable to excel**, but also shows **how to import datatable** with custom styling, and finally **export datatable with formatting** ready for distribution.

> **Prerequisites**  
> - .NET 6 or later (the example compiles on .NET Framework 4.7+ as well)  
> - A reference to a spreadsheet library that provides `Workbook`, `Worksheet`, and `Style` classes (e.g., Aspose.Cells, GemBox.Spreadsheet, or ClosedXML).  
> - Basic familiarity with `DataTable` objects.

---

![Create Workbook C# example showing styled Excel export](https://example.com/images/create-workbook-csharp.png)

## Step 1: Create Workbook C# – Initialize the Spreadsheet Object

First things first. We need a fresh workbook instance that will become the container for our Excel file.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using Aspose.Cells;           // Replace with your library if different

// Initialize a new workbook
Workbook workbook = new Workbook();               // assume a new workbook for this example
Worksheet worksheet = workbook.Worksheets[0];    // Grab the first (default) worksheet
```

**Why this matters:**  
Creating the workbook is the equivalent of opening a blank Excel file. The `Worksheet` object gives us a grid where we’ll later drop the `DataTable`. If you skip this step, there’s nowhere to import the data, and the library will throw a null‑reference exception.

> **Pro tip:** If you already have a template file (maybe with a logo or pre‑defined columns), load it with `new Workbook("Template.xlsx")` instead of a brand‑new instance.

## Step 2: Prepare the Source Data – Retrieve a DataTable

Next, we need the data we’re about to export. In real‑world apps this often comes from a database, but for illustration we’ll build a simple table in‑memory.

```csharp
// Step 2: Retrieve the source data as a DataTable
DataTable GetData()
{
    DataTable table = new DataTable("Employees");

    // Define columns
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Department", typeof(string));
    table.Columns.Add("HireDate", typeof(DateTime));

    // Populate rows
    table.Rows.Add(1, "Alice Johnson", "Finance", new DateTime(2018, 4, 12));
    table.Rows.Add(2, "Bob Smith", "Engineering", new DateTime(2020, 7, 23));
    table.Rows.Add(3, "Carol White", "HR", new DateTime(2019, 11, 5));
    table.Rows.Add(4, "David Brown", "Marketing", new DateTime(2021, 1, 30));

    return table;
}

DataTable dataTable = GetData();   // Call the method to obtain the DataTable
```

**Why this matters:**  
A `DataTable` is a versatile, in‑memory representation of tabular data. It mirrors the rows and columns you’d eventually see in Excel, making the **how to import datatable** step straightforward.

## Step 3: Define Column‑Level Styles – Add Custom Styles Excel

Now we get to the fun part: styling. We’ll create an array of `Style` objects—one for each column—so that every column can have its own visual treatment. In this example we’ll alternate font colors between blue and green.

```csharp
// Step 3: Prepare a style for each column in the DataTable
Style[] columnStyles = new Style[dataTable.Columns.Count];

for (int columnIndex = 0; columnIndex < columnStyles.Length; columnIndex++)
{
    // Create a new style instance for the current column
    columnStyles[columnIndex] = workbook.CreateStyle();

    // Step 4: Assign alternating font colors for visual distinction
    columnStyles[columnIndex].Font.Color = (columnIndex % 2 == 0) ? Color.Blue : Color.Green;
}
```

**Why this matters:**  
Applying styles column‑wise gives you fine‑grained control over the final look. Instead of a single blanket style, each column can convey meaning—think “blue for IDs, green for names.” This is the core of **add custom styles excel**.

> **Watch out:** Some libraries require you to also set `StyleFlag` properties (e.g., `styleFlag.FontColor = true`) before the style takes effect. Check your library’s docs if colors don’t appear.

## Step 4: Import the DataTable – How to Import DataTable into the Worksheet

With data and styles ready, we finally import the table. The `ImportDataTable` method copies rows, columns, and optionally the column headers.

```csharp
// Step 5: Import the DataTable into the worksheet, applying the column styles
bool includeColumnNames = true;   // true to write column headers
int startRow = 0;                 // zero‑based index; 0 = first row
int startColumn = 0;              // zero‑based index; 0 = first column

worksheet.Cells.ImportDataTable(dataTable, includeColumnNames, startRow, startColumn, columnStyles);
```

**Why this matters:**  
This single call does the heavy lifting of **import datatable to excel**. It respects the `columnStyles` array, so each column’s font color is applied as soon as the data lands in the sheet. If you ever need to skip headers, just flip `includeColumnNames` to `false`.

## Step 5: Save the Workbook – Export DataTable with Formatting

The final piece is persisting the workbook to a file (or a memory stream). This is where **export datatable with formatting** becomes visible to the end user.

```csharp
// Step 6: Save the workbook to an .xlsx file
string outputPath = Path.Combine(Environment.CurrentDirectory, "Employees.xlsx");
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved successfully to {outputPath}");
```

**Why this matters:**  
Saving as `Xlsx` preserves all style information. If you choose CSV, all formatting would be lost. The resulting file can be opened in Excel, Google Sheets, or any modern spreadsheet app, showing the alternating blue/green fonts we defined earlier.

### Expected Output

When you open `Employees.xlsx`, you’ll see:

| Id | Name          | Department | HireDate   |
|----|---------------|------------|------------|
| 1  | Alice Johnson | Finance    | 4/12/2018 |
| 2  | Bob Smith     | Engineering| 7/23/2020 |
| 3  | Carol White   | HR         | 11/5/2019 |
| 4  | David Brown   | Marketing  | 1/30/2021 |

- **Id** and **HireDate** columns appear in **blue** font.  
- **Name** and **Department** columns appear in **green** font.  
- Column headers are bold (default style from the library) and included because we set `includeColumnNames` to `true`.

---

## Common Variations & Edge Cases

### 1. Using a Template File

If you have a pre‑styled template (company logo, frozen panes, etc.), load it instead of creating a blank workbook:

```csharp
Workbook workbook = new Workbook("Template.xlsx");
Worksheet worksheet = workbook.Worksheets[0];
```

The `ImportDataTable` call works the same way, and the styles you define will blend with the template’s existing formatting.

### 2. Styling Rows Instead of Columns

Sometimes you want alternating row colors rather than column colors. Swap the loop logic:

```csharp
for (int rowIndex = 0; rowIndex < dataTable.Rows.Count; rowIndex++)
{
    Style rowStyle = workbook.CreateStyle();
    rowStyle.Font.Color = (rowIndex % 2 == 0

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}