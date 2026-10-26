---
category: general
date: 2026-10-26
description: Custom ExportTableOptions when ExportAsStrin lets you export Excel data
  as strings in C#. Follow the step‑by‑step guide to configure and run the export.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Custom ExportTableOptions when ExportAsStrin
- how to export excel as string
- ExportTableOptions C#
- Excel to DataTable string conversion
- Aspose.Cells export as string
language: en
lastmod: 2026-10-26
og_description: Custom ExportTableOptions when ExportAsStrin enables string‑only Excel
  export. Learn the exact steps to configure and run the export in C#.
og_image_alt: Code snippet showing ExportTableOptions configuration for string export
og_title: Custom ExportTableOptions when ExportAsStrin – export Excel as string in
  C#
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Custom ExportTableOptions when ExportAsStrin lets you export Excel
    data as strings in C#. Follow the step‑by‑step guide to configure and run the
    export.
  headline: Custom ExportTableOptions when ExportAsStrin for Excel
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Custom ExportTableOptions when ExportAsStrin for Excel
url: /net/excel-data-export-retrieval/custom-exporttableoptions-when-exportasstrin-for-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Custom ExportTableOptions when ExportAsStrin – export Excel as string in C#

If you need **Custom ExportTableOptions when ExportAsStrin** to get every cell value as a plain string, this guide shows you exactly how to do it. Whether you are building a data‑import pipeline or need a clean CSV‑ready dump, you’ll see why configuring the options this way avoids type‑conversion surprises.

In this tutorial you will learn **how to export excel as string** using the Aspose.Cells library, see the complete, runnable code, and understand the reasoning behind each setting. No external documentation is required – everything you need is right here.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 SDK or later installed  
* Visual Studio 2022 (or any IDE that supports .NET)  
* Aspose.Cells for .NET package (install via NuGet: `Install-Package Aspose.Cells`)  
* An Excel workbook (`sample.xlsx`) placed in the project’s root folder  

These items are the only dependencies; the code runs on Windows, Linux, or macOS without additional libraries.

## Step 1: Load the workbook you want to export

The first thing you do when using **Custom ExportTableOptions when ExportAsStrin** is to obtain a `Worksheet` object from a loaded workbook. This object gives you access to rows, columns, and the export API.

```csharp
using Aspose.Cells;
using System.Data;

// Load the workbook from disk
Workbook workbook = new Workbook("sample.xlsx");

// Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*Why this matters:*  
`Workbook` reads the file once and keeps all formatting information in memory. By selecting a specific `Worksheet`, you limit the export scope and avoid unnecessary processing of hidden sheets.

## Step 2: Configure ExportTableOptions with ExportAsString = true

The core of **Custom ExportTableOptions when ExportAsStrin** is the `ExportTableOptions` object. Setting `ExportAsString` forces the exporter to treat every cell as a string, regardless of its original data type (date, number, boolean, etc.). Enabling `PreserveFormatting` keeps the visual style (e.g., currency symbols) in the resulting string.

```csharp
// Create and configure the export options
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export every cell value as a string
    PreserveFormatting = true      // Keep the original cell formatting
};
```

*Why this matters:*  
When you later call `ExportDataTable`, the library normally tries to infer the .NET type of each column. With `ExportAsString = true`, that inference step is skipped, preventing unexpected `DateTime` or `double` conversions that can break downstream CSV parsers.

## Step 3: Export a range to a DataTable using the custom options

Now you can export a rectangular range (rows 0‑9, columns 0‑4) from the worksheet. The method returns a `DataTable` where every field is a `string`.

```csharp
// Export rows 0‑9 and columns 0‑4 (5 columns total) as a DataTable
DataTable dataTable = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 10,
    totalColumns: 5,
    options: exportOptions);
```

*Why this matters:*  
`ExportDataTable` is the most convenient way to move Excel data into a relational structure that many .NET APIs already understand (e.g., Entity Framework, Dapper). By passing the **Custom ExportTableOptions when ExportAsStrin**, you guarantee that each `DataColumn.DataType` will be `typeof(string)`.

## Step 4: Verify the result – all values are strings

It’s good practice to confirm that the export behaved as expected. The following loop prints each cell and its runtime type.

```csharp
Console.WriteLine("Exported DataTable (all values as strings):");
foreach (DataRow row in dataTable.Rows)
{
    for (int i = 0; i < dataTable.Columns.Count; i++)
    {
        object value = row[i];
        Console.Write($"{value} ({value.GetType().Name})\t");
    }
    Console.WriteLine();
}
```

**Expected output**

```
123 (String)    2023‑01‑15 (String)    $45.67 (String)    TRUE (String)    Sample text (String)
...
```

Every cell shows `String` as its type, confirming that **Custom ExportTableOptions when ExportAsStrin** worked correctly.

## Step 5: Optional – write the DataTable to CSV

If your ultimate goal is a plain‑text file, you can easily serialize the `DataTable` to CSV:

```csharp
using System.IO;
using System.Text;

// Choose a destination file
string csvPath = "exported.csv";

using (StreamWriter writer = new StreamWriter(csvPath, false,


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Export HTML Strings from Excel to DataTable using Aspose.Cells for .NET: A Step‑by‑Step Guide](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)
- [Export Custom Properties Excel Pdf Aspose Cells Net](/cells/hongkong/net/workbook-operations/export-custom-properties-excel-pdf-aspose-cells-net/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hongkong/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}