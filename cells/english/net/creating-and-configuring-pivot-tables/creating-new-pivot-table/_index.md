---
title: Create a New Pivot Table Programmatically in .NET
linktitle: Create a New Pivot Table Programmatically in .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Learn to create a pivot table programmatically in .NET using Aspose.Cells with our step-by-step guide. Efficiently analyze your data.
weight: 13
url: /net/creating-and-configuring-pivot-tables/creating-new-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Create a New Pivot Table Programmatically in .NET

## Introduction
Creating a pivot table can seem like an intimidating task, especially when you're doing it programmatically. But fear not! With Aspose.Cells for .NET, putting together a pivot table is not only straightforward but also quite powerful for data analysis. In this tutorial, we will guide you step-by-step on how to create a new pivot table in a .NET application. Whether you’re adding data for sales, sports, or any other business metric, this guide will help you get your pivot tables up and running in no time.

## Prerequisites
Before diving in, let’s ensure you have everything ready to go. Here’s what you need to do:

1. Install .NET Framework: Make sure you have the .NET framework installed on your machine. Aspose.Cells supports various versions, but it’s best to stick to the latest.
2. Aspose.Cells Library: You need to have the Aspose.Cells library. You can [download it here](https://releases.aspose.com/cells/net/) or get a [temporary license](https://purchase.aspose.com/temporary-license/) for evaluation.
3. IDE Setup: Have a C# compatible IDE ready, like Visual Studio, where you can start a new project.
4. Basic Knowledge of C#: Familiarity with C# programming will help you follow along without getting too bogged down.

Are you all set? Great! Let’s jump into importing the necessary packages.

## Import Packages
First thing first, you need to import the required namespaces into your C# project. Open your C# file and add the following using directives:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

These namespaces provide you access to the workbook, worksheet, and pivot table functionalities we’ll be using throughout this tutorial.

## Step 1: Create a Workbook Object
Creating a workbook is the beginning of your journey. Let’s start by instantiating a new workbook and accessing the first worksheet.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
// Instantiating a Workbook object
Workbook workbook = new Workbook();

// Obtaining the reference of the newly added worksheet
Worksheet sheet = workbook.Worksheets[0];
```

In this step, we create a `Workbook` instance which represents our Excel file and grab the very first worksheet, which will be our playground for the pivot table.

## Step 2: Insert Data into Cells
Next, let’s populate our worksheet with some sample data. We’re going to input rows for different sports, quarters, and sales figures to give our pivot table something to summarize.

```csharp
Cells cells = sheet.Cells;

// Setting the value to the cells
Cell cell = cells["A1"];
cell.PutValue("Sport");
cell = cells["B1"];
cell.PutValue("Quarter");
cell = cells["C1"];
cell.PutValue("Sales");

// Filling datacell = cells["A2"];
cell.PutValue("Golf");
// ... More data entries
```

Here, we’re defining our column headers and inserting values under each header. This data will act as the source for our pivot table, so make sure it's organized! Follow through this block, and you'll create a comprehensive dataset.

## Step 3: Adding a Pivot Table
With our data ready, it’s time to create the pivot table. We will use the pivot table collection from the worksheet to add our new pivot table.

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

// Adding a PivotTable to the worksheet
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

In this snippet, we add a pivot table to the worksheet that references our data range (in this case, cells A1 to C8). We place the pivot table starting at cell E3, and name it "PivotTable2". Pretty simple, right?

## Step 4: Customize the Pivot Table
Now that we have our pivot table, let’s customize it to show meaningful summaries. We can control what appears in the rows, columns, and data areas of the pivot table.

```csharp
// Accessing the instance of the newly added PivotTable
Aspose.Cells.Pivot.PivotTable pivotTable = pivotTables[index];

// Unshowing grand totals for rows.
pivotTable.RowGrand = false;

// Draging the first field to the row area.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Row, 0);

// Draging the second field to the column area.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Column, 1);

// Draging the third field to the data area.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Data, 2);
```

In this step, we tell the pivot table to hide grand totals for rows and then specify which fields go into the row, column, and data areas. The sport names will fill the rows, the quarters will fill the columns, and the sales figures will provide the summaries.

## Step 5: Save the Workbook
Finally, we want to save our newly created workbook to see the fruits of our labor.

```csharp
// Saving the Excel file
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

Just provide a proper path, and you'll have your pivot table output saved into an Excel file you can open and review.

## Conclusion
Creating pivot tables programmatically using Aspose.Cells for .NET can significantly save you time, especially when dealing with large datasets. You've learned how to set up your project, import necessary packages, populate data, and create a customizable pivot table from scratch. So, the next time you're drowning in numbers, remember this tutorial and let Aspose.Cells do the heavy lifting for you.

## FAQ's
### What is Aspose.Cells?
Aspose.Cells is a powerful .NET library for creating and managing Excel spreadsheets programmatically.

### Is there a free trial for Aspose.Cells?
Yes, you can get a free trial [here](https://releases.aspose.com/).

### Can I customize the appearance of the pivot table?
Absolutely! You can customize formatting, layout, and even styles of the pivot table as per your needs.

### Where can I find more examples and documentation on Aspose.Cells?
You can check the [documentation](https://reference.aspose.com/cells/net/) for comprehensive guides and examples.

### How do I get support for Aspose.Cells?
You can get support through the [Aspose forum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
