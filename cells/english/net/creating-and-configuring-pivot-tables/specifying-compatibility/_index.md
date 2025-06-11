---
title: Specify Compatibility of Excel File Programmatically in .NET
linktitle: Specify Compatibility of Excel File Programmatically in .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Learn to manipulate Excel pivot tables with Aspose.Cells for .NET, including data updates, compatibility settings, and cell formatting.
weight: 23
url: /net/creating-and-configuring-pivot-tables/specifying-compatibility/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Specify Compatibility of Excel File Programmatically in .NET

## Introduction

In today’s data-driven world, managing and manipulating Excel files programmatically has become essential for many developers. If you're working with Excel in .NET, Aspose.Cells is a powerful library that makes it easy to create, read, modify, and save Excel files. One important feature of this library allows you to specify the compatibility of Excel files programmatically. In this tutorial, we will explore how to manipulate Excel files, particularly focusing on managing compatibility using Aspose.Cells for .NET. By the end, you’ll understand how to set compatibility for Excel files, especially for pivot tables, while refreshing and managing data.

## Prerequisites

Before diving into the coding phase, ensure you have the following:

1. Basic knowledge of C#: Since we’ll be writing code in C#, familiarity with the language will help you understand the tutorial better.
2. Aspose.Cells for .NET library: You can download it from the [Aspose Cells releases page](https://releases.aspose.com/cells/net/). If you haven't already, consider getting a free trial to explore its features first.
3. Visual Studio: An IDE where you can write and test your C# code effectively.
4. Sample Excel File: Make sure you have a sample Excel file, preferably one that contains a pivot table for the demo. For our example, we will use `sample-pivot-table.xlsx`.

With these prerequisites in place, let’s get started with the coding process.

## Import Packages

Before you start writing your application, you need to include the necessary namespaces in your code to utilize the Aspose.Cells library effectively. Here’s how to do it.

### Import Aspose.Cells Namespace

```csharp
using System.IO;
using System;
using Aspose.Cells;
using Aspose.Cells.Pivot;
using System.Drawing;
```

This line of code ensures that you can access all classes and methods within the Aspose.Cells library.

Now, let's break down the process in detail to ensure everything is clear and understandable.

## Step 1: Set Up Your Directory

First things first, set up the directory where your Excel files are located. It’s important to provide the right file path.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

Here, replace `"Your Document Directory"` with the actual path to your Excel files. This is where your sample pivot table file should reside.

## Step 2: Load the Source Excel File

Next, we need to load the Excel file that contains the sample pivot table. 

```csharp
// Load source excel file containing sample pivot table
Workbook wb = new Workbook(dataDir + "sample-pivot-table.xlsx");
```

In this step, we create an instance of the `Workbook` class, which loads the specified Excel file. 

## Step 3: Access the Worksheets

Now that the workbook is loaded, you have to access the worksheet that contains the pivot table data.

```csharp
// Access first worksheet that contains pivot table data
Worksheet dataSheet = wb.Worksheets[0];
```

Here, we access the first worksheet where the pivot table is located. You can also loop through or specify other worksheets based on your Excel structure.

## Step 4: Manipulate Cell Data

Next up, you’ll modify some cell values in the worksheet. 

### Step 4.1: Modify Cell A3

Let’s start by accessing cell A3 and setting its value.

```csharp
// Access cell A3 and sets its data
Cells cells = dataSheet.Cells;
Cell cell = cells["A3"];
cell.PutValue("FooBar");
```

This code snippet updates cell A3 with the value “FooBar”.

### Step 4.2: Modify Cell B3 with Long String

Now, let’s set a lengthy string into cell B3, which exceeds Excel's standard character limits.

```csharp
// Access cell B3, sets its data
string longStr = "Very long text 1. very long text 2.... [continue your long string]";
cell = cells["B3"];
cell.PutValue(longStr);
```

This code is important because it sets your expectations regarding data limits, especially when working with compatibility settings in Excel.

## Step 5: Check the Length of Cell B3

It’s also essential to confirm the length of the string we entered.

```csharp
// Print the length of cell B3 string
Console.WriteLine("Length of original data string: " + cell.StringValue.Length);
```

This is just for verification to show how many characters your cell is holding.

## Step 6: Set Other Cell Values

Now we'll access more cells and set some values.

```csharp
// Access cell C3 and sets its data
cell = cells["C3"];
cell.PutValue("closed");

// Access cell D3 and sets its data
cell = cells["D3"];
cell.PutValue("2016/07/21");
```

Each of these snippets updates several additional cells within the worksheet.

## Step 7: Access the Pivot Table

Next, you’ll access the second worksheet, which consists of the pivot table data.

```csharp
// Access the second worksheet that contains pivot table
Worksheet pivotSheet = wb.Worksheets[1];

// Access the pivot table
PivotTable pivotTable = pivotSheet.PivotTables[0];
```

This snippet allows you to manipulate the pivot table for compatibility settings.

## Step 8: Set Compatibility for Excel 2003

It's crucial to set whether your pivot table is compatible with Excel 2003 or not. 

```csharp
// IsExcel2003Compatible property tells if PivotTable is compatible for Excel2003 while refreshing PivotTable
pivotTable.IsExcel2003Compatible = true;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

This is where the real transformation starts. By setting `IsExcel2003Compatible` to `true`, you limit character lengths to 255 when refreshing.

## Step 9: Check Length After Compatibility Setting

After setting the compatibility, let’s see how it affects the data.

```csharp
// Check the value of cell B5 of pivot sheet.
Cell b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to True: " + b5.StringValue.Length);
```

You’ll likely see an output that confirms the truncation effect if the initial data exceeds 255 characters.

## Step 10: Change Compatibility Setting

Now, let’s change the compatibility setting and check again.

```csharp
// Now set IsExcel2003Compatible property to false and again refresh
pivotTable.IsExcel2003Compatible = false;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

This allows your data to reflect its original length without the previous restrictions.

## Step 11: Verify Length Again 

Let’s verify that the data is now accurately reflecting its real length.

```csharp
// Now it will print the original length of cell data. The data has not been truncated now.
b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to False: " + b5.StringValue.Length);
```

You should see that the output confirms the removal of the truncation.

## Step 12: Format the Cells

To enhance the visual experience, you might want to format the cells. 

```csharp
// Set the row height and column width of cell B5 and also wrap its text
pivotSheet.Cells.SetRowHeight(b5.Row, 100);
pivotSheet.Cells.SetColumnWidth(b5.Column, 65);
Style st = b5.GetStyle();
st.IsTextWrapped = true;
b5.SetStyle(st);
```

These lines of code make the data easier to read by adjusting the cell dimensions and enabling text wrapping.

## Step 13: Save the Workbook

Finally, save your workbook with the changes you've made.

```csharp
// Save workbook in xlsx format
wb.Save(dataDir + "SpecifyCompatibility_out.xlsx", SaveFormat.Xlsx);
```

Choosing an appropriate file format is crucial when saving Excel files. The `Xlsx` format is widely used and compatible with many Excel versions.

## Conclusion

Congratulations! You’ve now programmed Excel file compatibility settings using Aspose.Cells for .NET. This tutorial outlined each step, from setting up your environment to altering compatibility settings for pivot tables. If you've ever worked with data that required specific limitations or compatibility, this is a skill you won't want to overlook.

## FAQ's

### What is Aspose.Cells?  
Aspose.Cells is a .NET library designed to help developers create, manipulate, and convert Excel files seamlessly.

### Why is Excel compatibility important?  
Excel compatibility is crucial for ensuring that files can be opened and used in the intended versions of Excel, particularly if they contain features or formats not supported in earlier versions.

### Can I programmatically create Pivot Tables with Aspose.Cells?  
Yes, you can create and manipulate Pivot Tables programmatically using Aspose.Cells. The library provides various methods to add data sources, fields, and features associated with Pivot Tables.

### How do I check the length of a string in an Excel cell?  
You can use the `StringValue` property of a `Cell` object to get the content of the cell and then call the `.Length` property to find out the length of the string.

### Can I customize cell formatting beyond row height and width?  
Absolutely! Aspose.Cells allows for extensive cell formatting. You can change font styles, colors, borders, number formats, and much more through the `Style` class.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
