---
title: Export HTML String Value of Cells to DataTable in Excel
linktitle: Export HTML String Value of Cells to DataTable in Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to export HTML string values from Excel cells to a DataTable using Aspose.Cells for .NET in a simple step-by-step tutorial.
weight: 11
url: /net/excel-data-sorting-exporting/export-html-string-value-of-cells-to-datatable-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Export HTML String Value of Cells to DataTable in Excel

## Introduction

When working with Excel files in a .NET environment, you might find yourself needing to extract information from cells, not just as plain text but rather as HTML strings. This can be quite handy when you're dealing with rich text data or when you want to maintain formatting. In this guide, I’ll walk you through exporting the HTML string value of cells to a DataTable using Aspose.Cells for .NET. 

## Prerequisites

Before diving into the code, let’s ensure you have everything you need in place. Here’s a quick checklist:

1. Basic Knowledge of C# and .NET: Before jumping into coding, make sure you're familiar with C# programming and the basics of the .NET framework.
2. Aspose.Cells for .NET: If you haven't already, you need to install Aspose.Cells for .NET. You can download a free trial from [here](https://releases.aspose.com/).
3. Visual Studio or IDE of Your Choice: Set up your environment to write C# code. Visual Studio is recommended for its wide range of features and ease of use.
4. Sample Excel File: You will need a sample Excel file (`sampleExportTableAsHtmlString.xlsx`) to work with. Ensure it's located in a directory that's accessible.
5. NuGet Package Manager: Make sure you have access to NuGet Package Manager in your project to easily add the Aspose.Cells library.

With these prerequisites in check, let’s get our hands dirty with some coding!

## Import Packages

Before we can start working with Aspose.Cells, we need to import the necessary packages. This usually involves adding the Aspose.Cells NuGet package to your project. Here’s how to do it:

### Open NuGet Package Manager

In Visual Studio, right-click on your project in the Solution Explorer, and select Manage NuGet Packages.

### Search for Aspose.Cells

In the NuGet Package Manager, type `Aspose.Cells` in the search bar.

### Install the Package

Once you find Aspose.Cells, click on the Install button. This will add the library to your project and allow you to import it in your code.

### Import the Namespace

Add the following using directive at the top of your code file:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Data;
```

Now that we’ve set everything up, let’s dive into the step-by-step process of exporting HTML string values from an Excel file to a DataTable. 

## Step 1: Define the Source Directory

You'll start by defining the directory where your sample Excel file is stored. This is crucial as it tells your application where to find the file. Here’s the code for that:

```csharp
string sourceDir = "Your Document Directory";
```

Make sure to replace `"Your Document Directory"` with the actual path to your Excel file.

## Step 2: Load the Sample Excel File

The next step is to load the Excel workbook. You will use the `Workbook` class from Aspose.Cells to do this. Here’s how you can load the file:

```csharp
Workbook wb = new Workbook(sourceDir + "sampleExportTableAsHtmlString.xlsx");
```

This simple line of code initializes the workbook and loads the specified Excel file.

## Step 3: Access the First Worksheet

Once the workbook is loaded, you’ll want to access the specific worksheet that contains the data you’re interested in. Generally, you'll start with the first worksheet:

```csharp
Worksheet ws = wb.Worksheets[0];
```

Here, we're working with the first worksheet (index 0). Make sure your data is on the correct sheet.

## Step 4: Specify Export Table Options

To control how the data is exported, you need to set up `ExportTableOptions`. In this case, you want to ensure that the column names are not exported, and you want the cell data exported as HTML strings:

```csharp
ExportTableOptions opts = new ExportTableOptions();
opts.ExportColumnName = false;
opts.ExportAsHtmlString = true;
```

This configuration allows you to maintain the rich formatting of your cell data when exporting.

## Step 5: Export Cells to DataTable

Now comes the crucial part where you actually export the data. Using the `ExportDataTable` method, you can pull the data from the worksheet into a `DataTable`. Here’s how to do that:

```csharp
DataTable dt = ws.Cells.ExportDataTable(0, 0, 3, 3, opts);
```

This code exports a specified range of cells (from row 0, column 0 to row 3, column 3) into a DataTable using the options specified earlier.

## Step 6: Print the HTML String Value

Finally, let’s print out the HTML string value from a specific cell in the DataTable to see what we've managed to export. For instance, if you want to print the value from the third row and second column, you would do the following:

```csharp
Console.WriteLine(dt.Rows[2][1].ToString());
```

This line prints the desired HTML string from the DataTable into the console. 

## Conclusion 

And there you have it! You've successfully exported HTML string values from cells in an Excel file to a DataTable using Aspose.Cells for .NET. This capability not only enriches your data manipulation skills but also broadens your options when dealing with formatted content straight from Excel files. 

## FAQ's

### Can I use Aspose.Cells for other file formats besides Excel?  
Yes, Aspose.Cells is primarily for Excel, but Aspose offers other libraries for different formats.

### Do I need a license for Aspose.Cells?  
Yes, a valid license is required for production use. You can get a temporary license [here](https://purchase.aspose.com/temporary-license/).

### What if my Excel file contains formulas? Will they export correctly?  
Yes, Aspose.Cells can handle formulas, and when exporting, they will be evaluated to their resulting values.

### Is it possible to change the export options?  
Absolutely! You can customize `ExportTableOptions` to fit your specific needs.

### Where can I find more detailed documentation for Aspose.Cells?  
You can find extensive documentation [here](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
