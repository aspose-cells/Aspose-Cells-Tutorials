---
category: general
date: 2026-08-11
description: Create excel sheet from a DataTable in C# and export datatable to excel
  with automatic sheet naming. Learn how to add rows to datatable and save workbook
  as xlsx.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel sheet
- export datatable to excel
- add rows to datatable
- create multiple excel sheets
- save workbook as xlsx
language: en
lastmod: 2026-08-11
og_description: Create excel sheet from a DataTable in C#. This tutorial shows how
  to export datatable to excel, add rows to datatable, generate multiple excel sheets
  and save workbook as xlsx.
og_image_alt: Screenshot of an Excel workbook created from a DataTable with automatically
  renamed sheets
og_title: Create excel sheet from a DataTable in C# – full programming guide
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create excel sheet from a DataTable in C# and export datatable to excel
    with automatic sheet naming. Learn how to add rows to datatable and save workbook
    as xlsx.
  headline: Create excel sheet from a DataTable in C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: Create excel sheet from a DataTable in C# – step‑by‑step guide
url: /net/excel-data-export-retrieval/create-excel-sheet-from-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create excel sheet from a DataTable in C# – step‑by‑step guide

If you need to **create excel sheet** from a `DataTable` in C#, this guide shows you exactly how to do it. You’ll see how to **export datatable to excel**, add rows, handle duplicate sheet names, and finally **save workbook as xlsx**.

The example uses Aspose.Cells, a widely‑used .NET library for Excel automation. The same concepts apply to other libraries that support SmartMarker‑style processing, but the code below works out‑of‑the‑box with Aspose.Cells 22.12 or later.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 SDK or later installed  
* A reference to the **Aspose.Cells** NuGet package (`Install-Package Aspose.Cells`)  
* Basic familiarity with `DataTable` and C# console applications  

These requirements keep the tutorial self‑contained and avoid external tooling.

## Step 1: Create a DataTable that will be exported to Excel

The first step is to build a `DataTable` that mirrors the data you want in the worksheet. Here we create a table named **Sheet1**, add an `Id` column, and insert two rows.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a DataTable named "Sheet1"
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // 2️⃣ Add rows to the DataTable
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);

        // Subsequent steps are called from here
        ProcessAndSaveWorkbook(dataTable);
    }
```

**Why this matters:**  
`DataTable` is a convenient in‑memory representation of tabular data. Naming the table `"Sheet1"` tells Aspose.Cells which sheet to target when processing SmartMarkers.

## Step 2: Add rows to the DataTable (optional expansion)

If your source data is dynamic, you’ll often need to add rows in a loop. The following snippet demonstrates a typical pattern:

```csharp
        // Example: add rows from a collection
        int[] ids = { 3, 4, 5 };
        foreach (int id in ids)
        {
            dataTable.Rows.Add(id);
        }
```

**Tip:** When adding many rows, consider disabling constraints (`dataTable.Constraints.Clear()`) to improve performance.

## Step 3: Configure SmartMarker options to create multiple excel sheets automatically

SmartMarker options let you control how duplicate sheet names are handled. Setting `DetailSheetNewName` to `"Sheet1_{0}"` tells Aspose.Cells to rename subsequent sheets as `Sheet1_1`, `Sheet1_2`, and so on.

```csharp
    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // 3️⃣ Set SmartMarker options for automatic sheet renaming
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // New sheets will be named Sheet1_1, Sheet1_2, etc.
            DetailSheetNewName = "Sheet1_{0}"
        };
```

**Why this matters:**  
When you process several `DataTable` objects that share the same name, Excel would normally throw an error because sheet names must be unique. The `DetailSheetNewName` pattern eliminates that conflict automatically.

## Step 4: Process the SmartMarkers and export datatable to excel

Now we create a fresh `Workbook`, run `ProcessSmartMarkers`, and let Aspose.Cells populate the worksheet(s) based on the `DataTable`.

```csharp
        // 4️⃣ Create a workbook and process SmartMarkers
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);
```

**Explanation:**  
`ProcessSmartMarkers` scans the workbook for markers like `&=Sheet1!A1` (not shown here) and replaces them with the data from `dataTable`. Because we started with an empty workbook, Aspose.Cells creates a new sheet matching the table name and fills it with the rows we added.

## Step 5: Save workbook as xlsx

Finally, write the workbook to disk with the modern OpenXML format (`.xlsx`). You can change the path to suit your environment.

```csharp
        // 5️⃣ Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Result:**  
Running the program produces an Excel file that contains:

| Sheet name | Rows |
|------------|------|
| Sheet1     | 1, 2, 3, 4, 5 |
| Sheet1_1   | (if another DataTable with the same name were processed) |

The sheet‑renaming logic ensures **create multiple excel sheets** without manual name management.

## Common variations and edge cases

| Situation | How to handle it |
|-----------|------------------|
| **Very large tables** (≥ 100 000 rows) | Use `WorkbookSettings.MemorySetting = MemorySetting.MemoryOptimized` before processing to keep memory usage low. |
| **Custom column order** | Reorder `DataColumn` objects in the `DataTable` before calling `ProcessSmartMarkers`. |
| **Multiple DataTables with different names** | Call `ProcessSmartMarkers` for each table; Aspose.Cells will create a separate sheet for each name automatically. |
| **Need a header row with styling** | After processing, access `Worksheet.Cells["A1"]` and apply `Style` properties (font, background). |
| **Saving to a stream instead of a file** | Replace `workbook.Save(outputPath, SaveFormat.Xlsx)` with `workbook.Save(stream, SaveFormat.Xlsx)`. |

**Pro tip:** Always wrap file‑system operations in `try…catch` blocks to surface permission issues early.

## Full source code (ready to copy)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create the DataTable that will be exported
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // Add rows – you can replace this with your own data source
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);
        int[] extraIds = { 3, 4, 5 };
        foreach (int id in extraIds)
        {
            dataTable.Rows.Add(id);
        }

        // Process SmartMarkers and save the workbook
        ProcessAndSaveWorkbook(dataTable);
    }

    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // Configure SmartMarkerOptions to rename duplicate sheets automatically
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Sheet1_{0}"
        };

        // Create a new workbook and populate it from the DataTable
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);

        // Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Expected output

Running the program prints:

```
Workbook saved to YOUR_DIRECTORY\DuplicateSheets.xlsx
```

Opening `DuplicateSheets.xlsx` shows a sheet named **Sheet1** with the `Id` column containing the values `1, 2, 3, 4, 5`. If you later process another `DataTable` named `"Sheet1"` in the same workbook, Aspose.Cells will create **Sheet1_1**, **Sheet1_2**, etc., automatically.

## Conclusion

You now know how to **create excel sheet** from a `DataTable` in C#, **export datatable to excel**, **add rows to datatable**, generate **create multiple excel sheets** with automatic naming, and **save workbook as xlsx**. The complete, runnable example demonstrates the end‑to‑end workflow and provides practical tips for large data sets and custom styling.

### What’s next?

* Explore **cell formatting** (fonts, colors, borders) by accessing `Worksheet.Cells` after `ProcessSmartMarkers`.  
* Use **SmartMarker loops** to generate master‑detail reports in a single workbook.  
* Switch to **CSV export** by changing `SaveFormat.Csv` if you need a plain‑text representation.  

Feel free to adapt the code to your own data sources—whether it’s a database query, an API response, or an in‑memory collection. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}