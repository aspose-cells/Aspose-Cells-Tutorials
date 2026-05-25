---
category: general
date: 2026-03-27
description: How to create pivot in C# using Aspose.Cells – learn to add data, enable
  refresh, and save workbook as xlsx in a single tutorial.
draft: false
keywords:
- how to create pivot
- save workbook as xlsx
- how to enable refresh
- how to add data
- generate excel file c#
language: en
og_description: How to create pivot in C# with Aspose.Cells. This guide shows you
  how to add data, enable refresh, and save workbook as xlsx.
og_title: How to Create Pivot in C# – Complete Aspose.Cells Tutorial
tags:
- Aspose.Cells
- C#
- Excel automation
title: How to Create Pivot in C# – Full Guide with Aspose.Cells
url: /net/creating-and-configuring-pivot-tables/how-to-create-pivot-in-c-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Create Pivot in C# – Complete Aspose.Cells Tutorial

Ever wondered **how to create pivot** in C# without wrestling with COM interop? You're not the only one. In many data‑driven apps we need a quick way to turn raw sales figures into a tidy summary, and Aspose.Cells makes that a piece of cake.  

In this tutorial we’ll walk through every step: adding data, building the pivot table, turning on automatic refresh, and finally **save workbook as xlsx** so your users can open it in Excel instantly. By the end you’ll have a ready‑to‑use `PivotRefresh.xlsx` file and a solid understanding of why each line matters.

## Prerequisites

- .NET 6+ (or .NET Framework 4.7.2 and later) – any recent runtime works.
- Aspose.Cells for .NET – you can pull it from NuGet (`Install-Package Aspose.Cells`).
- A basic familiarity with C# syntax – no deep Excel knowledge required.

> **Pro tip:** If you’re on a corporate machine, make sure the Aspose license is applied; otherwise you’ll get a watermark on the generated file.

## Step 1 – How to Add Data to a New Workbook

Before a pivot can exist, there must be a source table. We’ll create a fresh workbook, name the first worksheet *SalesData*, and drop a handful of rows that mimic a real‑world sales dump.

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and grab the default sheet
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        // 2️⃣ Write column headers
        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // 3️⃣ Insert a sample row – add more rows as your scenario demands
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);
```

**Why this matters:**  
- Using `PutValue` automatically sets the cell type, so you don’t have to worry about string vs numeric mismatches later.  
- Defining headers in row 1 gives the pivot engine something to reference when you map fields.

## Step 2 – Create a Worksheet that Will Host the Pivot Table

A pivot table lives on its own sheet, keeping the source data clean and the report tidy.

```csharp
        // 4️⃣ Add a dedicated sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");
```

> **What if you already have a sheet?** Just reference it by index (`workbook.Worksheets["MySheet"]`) instead of adding a new one.

## Step 3 – Define the Source Range (How to Add Data → Define Range)

Aspose.Cells needs a `CellArea` or a range string that encloses both headers and data. Here we assume a maximum of 100 rows; adjust as needed.

```csharp
        // 5️⃣ Build the source range (A1:D100 covers headers + up to 99 data rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");
```

**Edge case:** If your data set is dynamic, you can calculate the last used row with `salesDataSheet.Cells.MaxDataRow` and build the range accordingly.

## Step 4 – How to Create Pivot – Insert the Pivot Table

Now the fun part: we tell Aspose.Cells to create a pivot linked to the range we just set up.

```csharp
        // 6️⃣ Insert the pivot table at cell A3 of the pivot sheet
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];
```

Notice the formula‑style reference (`=SalesData!A1:D100`). That’s the same syntax you’d type into Excel, which makes the API intuitive.

## Step 5 – Configure Row, Column, and Data Fields (How to Add Data → Fields)

We’ll place *Region* on rows, *Product* on columns, and sum both *Units* and *Revenue*.

```csharp
        // 7️⃣ Set up row, column, and data fields
        pivotTable.RowFields.Add(0); // 0 = first column => Region
        pivotTable.ColumnFields.Add(1); // 1 = second column => Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);
```

**Why these indices?**  
Aspose.Cells indexes columns starting at 0, so `0` points to *Region*. The `DataFields.Add` method lets you rename the field (e.g., “Sum of Units”) and pick an aggregation type – `Sum` is the most common for numeric data.

## Step 6 – How to Enable Refresh – Make the Pivot Auto‑Update on Open

If the source data changes later, you probably want the pivot to reflect those changes automatically. That’s where `RefreshDataOnOpen` shines.

```csharp
        // 8️⃣ Turn on automatic refresh when the file is opened
        pivotTable.RefreshDataOnOpen = true;
```

> **Note:** This flag only works when the workbook is opened in Excel; it won’t re‑calculate inside Aspose.Cells unless you call `pivotTable.RefreshData()` manually.

## Step 7 – Save Workbook as XLSX (How to Save Workbook as XLSX)

Finally, we persist the file to disk. The `.xlsx` format is the modern, zip‑based Excel file type that works everywhere.

```csharp
        // 9️⃣ Save the workbook – this also satisfies the “save workbook as xlsx” requirement
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

Running the program produces a file named **PivotRefresh.xlsx** in the execution folder. Open it in Excel and you’ll see a neatly laid‑out pivot with *Region* rows, *Product* columns, and summed *Units* and *Revenue* values. Because we enabled refresh, any edits you make to the *SalesData* sheet will automatically update the pivot the next time you open the workbook.

### Expected Output

| Region | Widget | Gadget | … |
|--------|--------|--------|---|
| East   | 120    | 0      |   |
| West   | 0      | 85     |   |
| **Grand Total** | **120** | **85** |   |

*(Numbers will vary based on the rows you add.)*

---

## Common Questions & Variations

### What if I need multiple pivot tables?

You can repeat **Step 4** with a different name and location. Each call to `PivotTables.Add` returns a new index you can use to retrieve the table object.

### How do I change the aggregation to *Average* instead of *Sum*?

Replace `PivotTableDataAggregationType.Sum` with `PivotTableDataAggregationType.Average` in the `DataFields.Add` calls.

### Can I style the pivot (fonts, colors)?

Yes. After creating the pivot, you can access its `Style` property or apply cell formatting to the range that contains the pivot. For example:

```csharp
pivotTable.Style = workbook.Styles[workbook.Styles.Add()];
pivotTable.Style.Font.Color = System.Drawing.Color.DarkBlue;
```

### Is it possible to add more rows after the workbook is saved?

Absolutely. Load the file with `new Workbook("PivotRefresh.xlsx")`, append rows to the *SalesData* sheet, and call `pivotTable.RefreshData()` before saving again.

---

## Full Working Example (Copy‑Paste Ready)

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // Step 1: Create workbook & add sample data
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // Sample rows – extend as needed
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);

        salesDataSheet.Cells["A3"].PutValue("West");
        salesDataSheet.Cells["B3"].PutValue("Gadget");
        salesDataSheet.Cells["C3"].PutValue(85);
        salesDataSheet.Cells["D3"].PutValue(4250);

        // Step 2: Add sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");

        // Step 3: Define source range (covers up to 100 rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");

        // Step 4: Insert pivot table
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];

        // Step 5: Configure fields
        pivotTable.RowFields.Add(0); // Region
        pivotTable.ColumnFields.Add(1); // Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);

        // Step 6: Enable automatic refresh
        pivotTable.RefreshDataOnOpen = true;

        // Step 7: Save as .xlsx
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

Save the file, run it, and open the generated **PivotRefresh.xlsx** – you’ve just mastered **how to create pivot** in C#.

---

## Wrapping Up

We’ve covered **how to create pivot** tables programmatically, how to **add data**, how to **enable refresh**, and finally how to **save workbook as xlsx** using Aspose.Cells. The code

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}