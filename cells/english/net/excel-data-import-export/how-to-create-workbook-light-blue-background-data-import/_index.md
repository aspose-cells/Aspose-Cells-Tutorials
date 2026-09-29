---
category: general
date: 2026-02-09
description: How to create workbook in C# with a light blue background and import
  data with headers. Learn to add light blue background, use default style excel and
  import datatable.
draft: false
keywords:
- how to create workbook
- add light blue background
- import data with headers
- excel import datatable c#
- use default style excel
language: en
og_description: How to create workbook in C# with a light blue background, import
  data with headers, and apply default style excel—all in one concise guide.
og_title: How to Create Workbook – Light Blue Background, Data Import
tags:
- C#
- Excel
- Aspose.Cells
title: How to Create Workbook – Light Blue Background, Data Import
url: /net/excel-data-import-export/how-to-create-workbook-light-blue-background-data-import/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Create Workbook – Light Blue Background, Data Import

Ever wondered **how to create workbook** in C# that looks a little prettier straight out of the box? Maybe you’ve pulled a `DataTable` from a database and you’re tired of the bland, default‑white cells. In this tutorial we’ll walk through creating a new workbook, adding a light‑blue background to a column, and importing data with headers—all while using the default style Excel provides.

We’ll also sprinkle in a few “what‑if” scenarios, like handling null values or customizing more than one column. By the end, you’ll have a fully‑styled Excel file you can ship to stakeholders without any post‑processing.

## Prerequisites

Before we dive in, make sure you have:

* **.NET 6+** (the code works on .NET Framework 4.6+ as well)  
* **Aspose.Cells for .NET** – the library that powers the `Workbook`, `Style`, and `ImportDataTable` calls. Install it via NuGet:  

  ```bash
  dotnet add package Aspose.Cells
  ```

* A `DataTable` source – we’ll fake one in the example, but you can replace it with any ADO.NET query.

Got those? Great, let’s get started.

## Step 1: Initialize a New Workbook (Primary Keyword)

The first thing you need to do is **how to create workbook** – literally. The `Workbook` class represents the entire Excel file, and its constructor gives you a clean slate.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

namespace ExcelStylingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or obtain an existing one)
            Workbook workbook = new Workbook();   // <-- this is how to create workbook
```

> **Why this matters:** Starting with a fresh `Workbook` ensures you control every style from the get‑go. If you opened an existing file, you’d inherit whatever styles the original author left behind, which can lead to inconsistent formatting.

## Step 2: Prepare the DataTable You’ll Import

For the sake of illustration, let’s spin up a simple `DataTable`. In real‑world scenarios you’d probably call a stored procedure or an ORM method.

```csharp
            // Step 2: Retrieve the data you want to import (e.g., from a database)
            DataTable dataTable = GetSampleData(); // replace with your own GetData()
```

```csharp
        // Helper method that returns a dummy DataTable
        static DataTable GetSampleData()
        {
            DataTable table = new DataTable("Employees");
            table.Columns.Add("ID", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("HireDate", typeof(DateTime));
            table.Columns.Add("Salary", typeof(decimal));

            table.Rows.Add(1, "Alice Johnson", new DateTime(2020, 5, 12), 72000);
            table.Rows.Add(2, "Bob Smith", new DateTime(2019, 3, 4), 68000);
            table.Rows.Add(3, "Carol White", DBNull.Value, 75000); // demonstrates a null value
            return table;
        }
```

> **Tip:** If you need to preserve column order exactly as it appears in the database, set the `ImportDataTable` `importColumnNames` parameter to `true`. This tells Aspose.Cells to write the column headers for you.

## Step 3: Define Column Styles – Default + Light‑Blue Background

Now we answer the **add light blue background** part of the puzzle. Aspose.Cells lets you pass an array of `Style` objects that correspond to each column you import. The first entry is the style for column 0, the second for column 1, and so on. If you have fewer styles than columns, the remaining columns fall back to the default style.

```csharp
            // Step 3: Define column styles – the default style and a custom style with a light‑blue foreground
            Style defaultStyle = workbook.DefaultStyle; // this is the use default style excel
            Style lightBlueStyle = workbook.CreateStyle();
            lightBlueStyle.ForegroundColor = Color.LightBlue;
            lightBlueStyle.Pattern = BackgroundType.Solid; // make sure the color shows

            // Apply default style to the first column, light blue to the second column
            Style[] columnStyles = { defaultStyle, lightBlueStyle };
```

> **Why only two styles?** In our sample we have four columns, but we only want the second column (Name) to stand out. The array length doesn’t need to match the column count; any missing entries automatically inherit the workbook’s default style.

## Step 4: Import the DataTable with Headers and Styles

Here’s where we bring together **excel import datatable c#** and **import data with headers**. The `ImportDataTable` method does the heavy lifting: it writes the column names, rows, and applies the style array we just built.

```csharp
            // Step 4: Import the DataTable into the first worksheet starting at cell A1, applying the styles
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells.ImportDataTable(dataTable, // the source DataTable
                                        true,       // import column names as headers
                                        0,          // start row (0‑based)
                                        0,          // start column (0‑based)
                                        columnStyles);
```

### Expected Result

After running the program, `workbook` will contain a single worksheet that looks like this:

| **ID** | **Name** (light‑blue) | **HireDate** | **Salary** |
|-------|------------------------|--------------|------------|
| 1     | Alice Johnson          | 5/12/2020    | 72000      |
| 2     | Bob Smith              | 3/4/2019     | 68000      |
| 3     | Carol White            | *(blank)*    | 75000      |

* The **Name** column sports a light‑blue background, proving that the style array works.
* Column headers are automatically generated because we passed `true` for `importColumnNames`.
* Null values appear as empty cells, which is the default behaviour of Aspose.Cells.

## Step 5: Save the Workbook (Optional but Useful)

You’ll probably want to write the file to disk or stream it back to a web client. Saving is straightforward:

```csharp
            // Step 5: Save the workbook to a file
            string outputPath = "StyledEmployees.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

> **Pro tip:** If you’re targeting older Excel versions, change `SaveFormat.Xlsx` to `SaveFormat.Xls`. The API handles the conversion for you.

## Edge Cases & Variations

### Multiple Styled Columns

If you need more than one styled column, simply expand the `columnStyles` array:

```csharp
Style[] columnStyles = { defaultStyle, lightBlueStyle, defaultStyle, lightBlueStyle };
```

Now both **Name** and **Salary** will be light‑blue.

### Conditional Formatting Instead of Fixed Styles

Sometimes you want a column to turn red when a value exceeds a threshold. That’s where **use default style excel** meets conditional formatting:

```csharp
int salaryColIdx = 3; // zero‑based index for Salary column
FormatCondition condition = sheet.ConditionalFormattings[0]
    .AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");
condition.Style.ForegroundColor = Color.LightCoral;
condition.Style.Pattern = BackgroundType.Solid;
```

### Importing Without Headers

If your downstream system already supplies its own headers, just pass `false` for the `importColumnNames` argument. The data will start at `A1` and you can write custom headers afterwards.

```csharp
sheet.Cells.ImportDataTable(dataTable, false, 1, 0); // start at row 2 (index 1)
```

## Full Working Example (All

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}