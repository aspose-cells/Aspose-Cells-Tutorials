---
title: Pivot Table Custom Sort Programmatically in .NET
linktitle: Pivot Table Custom Sort Programmatically in .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to programmatically sort Pivot Tables in .NET using Aspose.Cells. A step-by-step guide covering setup, configuration, sorting, and saving results as Excel and PDF files.
weight: 29
url: /net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pivot Table Custom Sort Programmatically in .NET

## Introduction
When it comes to working with Excel in a .NET environment, one library stands out among the rest: Aspose.Cells. Now, don’t you just love it when a tool allows you to manipulate spreadsheets programmatically? That’s precisely what Aspose.Cells does! In today’s tutorial, we’re diving deep into the world of Pivot Tables and showing you how to implement custom sorting programmatically using this versatile library.
## Prerequisites
Before we roll up our sleeves and jump into the code, make sure you've got a few things in place:
1. Visual Studio: You’ll need a working version of Visual Studio. It’s the playground where all the magic happens.
2. .NET Framework: Familiarity with .NET programming is essential. Whether you’re a .NET Core or .NET Framework enthusiast, you're good to go.
3. Aspose.Cells Library: You need to install the Aspose.Cells library. You can get it from the [Download link](https://releases.aspose.com/cells/net/) and add it to your project.
4. Basic Understanding of Pivot Tables: While you don’t need to be an expert, a little knowledge about how Pivot Tables work will be beneficial as we go through this tutorial.
5. Sample Excel File: Have a sample Excel file named `SamplePivotSort.xlsx` ready in your working directory for testing.
## Import Packages
Once you have all your prerequisites sorted, the first step is to import the necessary packages. To do this, include the following lines at the top of your code:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
This package provides all the functionality you need for manipulating Excel files using Aspose.Cells.

Alright, let’s get into the fun part! We're going to break down the process of creating a Pivot Table and applying custom sorting into manageable steps.
## Step 1: Set Up the Workbook
To kick things off, we need to set up our workbook. Here's how you do it:
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
In this step, we initialize a new `Workbook` instance with the path to our Excel file. This acts as the canvas where our Pivot Table will come to life.
## Step 2: Access the Worksheet
Next, we need to access the worksheet where we will add our Pivot Table.
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
Here, we grab the first worksheet in our workbook and call upon the `PivotTableCollection`. This collection allows us to manage all the Pivot Tables on this worksheet.
## Step 3: Create Your First Pivot Table
Now it’s time to create our Pivot Table.
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
We add a new Pivot Table to our worksheet, specifying the data range and its location. "E3" indicates where we want our Pivot Table to begin. We then reference this new Pivot Table using its index.
## Step 4: Configure Pivot Table Settings
Let’s configure our Pivot Table! This means controlling aspects like grand totals and field arrangements.
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
We ensure that grand totals for rows and columns are not displayed, which can make the data cleaner. Then we’re adding the first field to the row area, enabling auto-sorting and an ascending sort.
## Step 5: Add Column and Data Fields
Once the rows are set, let’s add the column and data fields.
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
We add the second field as a column and format it as a date. Again, we enable auto-sorting and ascending order to keep things organized. Finally, we need to add the third field to our data area:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## Step 6: Refresh and Calculate the Pivot Table
After adding all the necessary fields, let’s ensure our Pivot Table is fresh and ready.
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
These methods refresh the data and recalculate it, ensuring everything is up-to-date and displayed correctly in our Pivot Table.
## Step 7: Custom Sort Based on Row Field Values
Let’s add a bit of flair by sorting the Pivot Table based on specific values, like "SeaFood".
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
We’re repeating the process by creating another Pivot Table and setting it up similarly to the first one. We can now customize it further:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## Step 8: Additional Sort CustomizationLet’s try another sorting method based on a specific date:
```csharp
// Adding another Pivot Table for sorting by a date
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
// Repeat row and column settings similar to previous steps
```
You just iterate through the same process, creating a third Pivot Table with its sorting criteria tailored to your needs.
## Step 9: Save the WorkbookTime to save all the hard work we’ve put in!
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
Here, you save the workbook as an Excel file and a PDF. The `PdfSaveOptions` allows for better formatting, ensuring each sheet appears on a separate page when converted.
## Step 10: Finish UpWrap it all up by letting the user know everything's cool.
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## Conclusion
By now, you’ve learned how to harness the power of Aspose.Cells to create and customize Pivot Tables in your .NET applications. From initial setup to custom sorting, each step combines to deliver a seamless experience. Whether you need to present yearly sales data or track inventory stats, these skills will serve you well!
## FAQ's
### What is a Pivot Table?
A Pivot Table is a data processing tool in Excel that allows you to summarize and analyze data, providing a flexible way to extract insights easily.
### How do I install Aspose.Cells?
You can install it via NuGet in Visual Studio or download it directly from the [Download link](https://releases.aspose.com/cells/net/).
### Is there a trial version of Aspose.Cells?
Yes! You can try it for free by visiting the [Free trial link](https://releases.aspose.com/).
### Can I sort multiple fields in a Pivot Table?
Absolutely! You can add and sort multiple fields based on your requirements.
### Where can I find support for Aspose.Cells?
The community is quite active, and you can ask questions on their forum [here](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
