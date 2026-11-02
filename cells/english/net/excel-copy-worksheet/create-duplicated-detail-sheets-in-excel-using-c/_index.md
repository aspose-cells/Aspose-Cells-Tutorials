---
category: general
date: 2026-10-07
description: Create duplicated detail sheets in Excel using C#. Learn how to generate
  multiple worksheets and build a report from tables in a single run.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicated detail sheets
- how to generate multiple worksheets
- generate excel report from tables
language: en
lastmod: 2026-10-07
og_description: Create duplicated detail sheets in Excel with C#. This tutorial shows
  how to generate multiple worksheets and produce a full Excel report from tables.
og_image_alt: Screenshot of an Excel file that has create duplicated detail sheets
  output
og_title: Create duplicated detail sheets in Excel – step‑by‑step C# guide
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create duplicated detail sheets in Excel using C#. Learn how to generate
    multiple worksheets and build a report from tables in a single run.
  headline: Create duplicated detail sheets in Excel using C#
  type: TechArticle
- description: Create duplicated detail sheets in Excel using C#. Learn how to generate
    multiple worksheets and build a report from tables in a single run.
  name: Create duplicated detail sheets in Excel using C#
  steps:
  - name: '**Obtain the data source** that contains a master table and two detail
      tables.'
    text: '**Obtain the data source** that contains a master table and two detail
      tables.'
  - name: '**Configure the Smart‑marker processor** so each duplicated detail sheet
      receives a unique name.'
    text: '**Configure the Smart‑marker processor** so each duplicated detail sheet
      receives a unique name.'
  - name: '**Create a new workbook** and place a smart‑marker that references the
      master table.'
    text: '**Create a new workbook** and place a smart‑marker that references the
      master table.'
  - name: '**Run the processor** to generate the master sheet and all detail sheets.'
    text: '**Run the processor** to generate the master sheet and all detail sheets.'
  - name: '**Save the workbook** – each detail sheet now has a distinct name.'
    text: '**Save the workbook** – each detail sheet now has a distinct name.'
  type: HowTo
tags:
- C#
- Excel automation
- Aspose.Cells
title: Create duplicated detail sheets in Excel using C#
url: /net/excel-copy-worksheet/create-duplicated-detail-sheets-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create duplicated detail sheets in Excel using C#

If you need to **create duplicated detail sheets** in an Excel workbook, this guide walks you through the complete process. You’ll see how to **generate multiple worksheets** from a master‑detail data set and produce a polished Excel report directly from tables.

Generating an Excel report from tables is a common requirement for billing systems, inventory dashboards, or any scenario where a master record has several related detail rows. By the end of this tutorial you’ll have a runnable C# program that creates a workbook with a master sheet and a uniquely named sheet for each detail group.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 (or later) installed  
* Visual Studio 2022 or any C#‑compatible IDE  
* The **Aspose.Cells for .NET** NuGet package (provides `SmartMarkerProcessor`)  

You can add the package with the following command:

```bash
dotnet add package Aspose.Cells
```

## Overview of the solution

The solution follows these five steps:

1. **Obtain the data source** that contains a master table and two detail tables.  
2. **Configure the Smart‑marker processor** so each duplicated detail sheet receives a unique name.  
3. **Create a new workbook** and place a smart‑marker that references the master table.  
4. **Run the processor** to generate the master sheet and all detail sheets.  
5. **Save the workbook** – each detail sheet now has a distinct name.

Each step is explained in detail below, with full code and reasoning.

## Step 1: Obtain the data source that contains a master table and two detail tables

The first task is to build a `DataSet` that mimics the data you would normally retrieve from a database. The `DataSet` must contain a table named **Master** and one or more tables named **Detail**. The Smart‑marker engine uses these table names to populate the workbook.

```csharp
using System.Data;

/// <summary>
/// Returns a DataSet with a master table and two detail tables.
/// In a real application you would fill these tables from a database.
/// </summary>
static DataSet GetReportDataSet()
{
    var ds = new DataSet();

    // Master table – one row per invoice
    var master = new DataTable("Master");
    master.Columns.Add("InvoiceId", typeof(int));
    master.Columns.Add("CustomerName", typeof(string));
    master.Columns.Add("InvoiceDate", typeof(DateTime));
    master.Rows.Add(101, "Acme Corp", new DateTime(2024, 12, 01));
    master.Rows.Add(102, "Beta Ltd.", new DateTime(2024, 12, 03));
    ds.Tables.Add(master);

    // Detail table – multiple rows per invoice
    var detail = new DataTable("Detail");
    detail.Columns.Add("InvoiceId", typeof(int));
    detail.Columns.Add("Product", typeof(string));
    detail.Columns.Add("Quantity", typeof(int));
    detail.Columns.Add("Price", typeof(decimal));

    // Detail rows for Invoice 101
    detail.Rows.Add(101, "Widget A", 5, 9.99m);
    detail.Rows.Add(101, "Widget B", 2, 19.95m);

    // Detail rows for Invoice 102
    detail.Rows.Add(102, "Gadget X", 1, 99.00m);
    detail.Rows.Add(102, "Gadget Y", 3, 49.50m);
    ds.Tables.Add(detail);

    return ds;
}
```

**Why this matters:**  
*Smart‑marker* works with `DataSet` objects; each table name becomes a marker that the engine can replace. By structuring the data this way you enable the processor to automatically duplicate the detail sheet for every distinct `InvoiceId`.

## Step 2: Configure the Smart‑marker processor to give each duplicated detail sheet a unique name

When the processor encounters a detail marker, it creates a new worksheet for each group of rows. By default the new sheets share the same name, which leads to a naming conflict. Setting `DetailSheetNewName` tells the engine how to rename each copy.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

/// <summary>
/// Configures the SmartMarkerProcessor to rename duplicated detail sheets.
/// The placeholder {0} is replaced with a sequential number (1, 2, …).
/// </summary>
static SmartMarkerProcessor ConfigureProcessor()
{
    var processor = new SmartMarkerProcessor();

    // The pattern "Detail_{0}" becomes Detail_1, Detail_2, …
    processor.Options.DetailSheetNewName = "Detail_{0}";

    // Optional: keep the original sheet as a template (if you have one)
    processor.Options.KeepTemplateSheet = false;

    return processor;
}
```

**Why this matters:**  
Without a unique naming pattern the workbook would throw an exception when the processor tries to add a second details sheet. The placeholder `{0}` ensures each sheet receives a distinct, predictable name.

## Step 3: Create a new workbook and place a smart‑marker that references the master table

Now you create a fresh `Workbook`, add a marker that points to the **Master** table, and optionally format the header row.

```csharp
/// <summary>
/// Creates a workbook with a single cell that contains the master smart‑marker.
/// </summary>
static Workbook CreateTemplateWorkbook()
{
    var workbook = new Workbook();
    var sheet = workbook.Worksheets[0];

    // Put the master smart‑marker in cell A1.
    // The double braces {{ }} tell SmartMarker to replace the content with the Master table.
    sheet.Cells["A1"].PutValue("{{Master}}");

    // Optional: add a header row for visual clarity.
    sheet.Cells["A2"].PutValue("Invoice ID");
    sheet.Cells["B2"].PutValue("Customer");
    sheet.Cells["C2"].PutValue("Date");
    sheet.Cells["A2:C2"].Style.Font.IsBold = true;

    return workbook;
}
```

**Why this matters:**  
The marker `{{Master}}` instructs the processor to expand the master table starting at `A1`. The subsequent rows become the data rows for each master record. This is the entry point for **generate excel report from tables**.

## Step 4: Run the smart‑marker processor to generate the master sheet and the detail sheets

With the data source, processor, and template ready, you invoke `Process`. The engine expands the master marker, then creates a separate detail sheet for each distinct `InvoiceId`.

```csharp
static void GenerateReport()
{
    // 1️⃣ Obtain data
    DataSet reportData = GetReportDataSet();

    // 2️⃣ Configure processor
    SmartMarkerProcessor processor = ConfigureProcessor();

    // 3️⃣ Create template workbook
    Workbook workbook = CreateTemplateWorkbook();

    // 4️⃣ Process the smart‑markers – this creates the master sheet and duplicated detail sheets
    processor.Process(workbook, reportData);

    // 5️⃣ Save the file
    string outputPath = Path.Combine(
        Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
        "DuplicatedDetailSheets.xlsx");
    workbook.Save(outputPath);

    Console.WriteLine($"Report generated successfully: {outputPath}");
}
```

**Why this matters:**  
`processor.Process` performs the heavy lifting: it reads the master rows, creates a detail sheet for each unique key, and renames those sheets according to the pattern defined earlier. The result is a workbook that satisfies the **how to generate multiple worksheets** requirement.

## Step 5: Save the resulting workbook – each detail sheet now has a distinct name

The `Save` call writes the file to disk. When you open the workbook, you’ll see:

* **Sheet1** – the master sheet containing invoice headers.  
* **Detail_1**, **Detail_2**, … – each sheet contains the rows from the **Detail** table that belong to a particular invoice.

Below is a mock‑up of the expected workbook layout (the image is illustrative; you can replace it with a real screenshot if desired).

![Screenshot of an Excel file that has create duplicated detail sheets output](https://example.com/images/duplicated-detail-sheets.png)

### Expected output

| Sheet name | Content description |
|------------|----------------------|
| **Sheet1** | Master rows: InvoiceId, CustomerName, InvoiceDate |
| **Detail_1** | Detail rows where `InvoiceId = 101` |
| **Detail_2** | Detail rows where `InvoiceId = 102` |

Opening `DuplicatedDetailSheets.xlsx` should show exactly this structure.

## Full source code (ready to copy)

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace ExcelDetailSheetsDemo
{
    class Program
    {
        static void Main()
        {
            GenerateReport();
        }

        // ------------------------------------------------------------
        // Step 1 – data source
        // ------------------------------------------------------------
        static DataSet GetReportDataSet()
        {
            var ds = new DataSet();

            var master = new DataTable("Master");
            master.Columns.Add("InvoiceId", typeof(int));
            master.Columns.Add("CustomerName", typeof(string));
            master.Columns.Add("InvoiceDate", typeof(DateTime));
            master.Rows.Add(101, "Acme Corp", new DateTime(2024, 12, 01));
            master.Rows.Add(102, "Beta Ltd.", new DateTime(2024, 12, 03));
            ds.Tables.Add(master);

            var detail = new DataTable("Detail");
            detail.Columns.Add("InvoiceId", typeof(int));
            detail.Columns.Add("Product", typeof(string));
            detail.Columns.Add("Quantity", typeof(int));
            detail.Columns.Add("Price", typeof(decimal));
            detail.Rows.Add(101, "Widget A", 5, 9.99m);
            detail.Rows.Add(101, "Widget B", 2, 19.95m);
            detail.Rows.Add(102, "Gadget X", 1, 99.00m);
            detail.Rows.Add(102, "Gadget Y", 3, 49.50m);
            ds.Tables.Add(detail);

            return ds;
        }

        // ------------------------------------------------------------
        // Step 2 – processor configuration
        // ------------------------------------------------------------
        static SmartMarkerProcessor ConfigureProcessor()
        {
            var processor = new SmartMarkerProcessor();
            processor.Options.DetailSheetNewName = "Detail_{0}";
            processor.Options.KeepTemplate


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Name Sheets Automatically – Generate Multiple Sheets in C#](/cells/english/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/)
- [How to Create Worksheets – Step‑by‑Step Guide for Dynamic Excel Generation](/cells/english/net/worksheet-operations/how-to-create-worksheets-step-by-step-guide-for-dynamic-exce/)
- [How to Generate Excel Report in C# – Full Guide Using SmartMarker](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}