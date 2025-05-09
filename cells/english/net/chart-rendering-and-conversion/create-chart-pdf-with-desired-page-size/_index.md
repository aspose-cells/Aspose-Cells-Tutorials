---
title: Create Chart PDF with Desired Page Size
linktitle: Create Chart PDF with Desired Page Size
second_title: Aspose.Cells .NET Excel Processing API
description: Create a PDF with your Excel chart using Aspose.Cells for .NET. Learn how with this step-by-step guide.
weight: 12
url: /net/chart-rendering-and-conversion/create-chart-pdf-with-desired-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Create Chart PDF with Desired Page Size

## Introduction

Creating visually appealing and informative charts is essential for data representation in various fields. Whether you're dealing with sales data, performance metrics, or any other type of information, having the ability to produce high-quality charts gives your findings depth and clarity. If you're working with .NET applications, Aspose.Cells is a powerful library that makes handling Excel documents and generating charts a breeze. In this tutorial, we’ll guide you through the process of creating a PDF of a chart from an Excel file with a desired page size.

## Prerequisites

Before diving into the code, there are a few prerequisites you must fulfill to ensure a smooth experience:

### Basic Knowledge of C# and .NET

You'll need a fundamental understanding of C# programming and the .NET framework. This will help you grasp the structure of the code that you will encounter in this guide.

### Aspose.Cells for .NET

Make sure you have Aspose.Cells for .NET installed. You can find all the details on the [Aspose.Cells documentation](https://reference.aspose.com/cells/net/). 

### Development Environment

Set up your development environment. This can be Visual Studio or any other IDE that supports C#. Download and install the Aspose.Cells library from the [download page](https://releases.aspose.com/cells/net/).

### Sample Excel File

You will need a sample Excel file that contains at least one chart. You can create a sample file or download one to use throughout this tutorial.

## Import Packages

To start working with Aspose.Cells, you need to import the necessary namespaces in your C# application. Here's how you do that:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Aspose.Cells.Charts;
```

These namespaces give you access to the classes and methods needed to manipulate Excel workbooks and their contents.

Now that we have all the prerequisites sorted out, let’s break down the process into detailed steps.

## Step 1: Setup Output and Source Directories

To begin, you need to define where the output PDF will be saved and where your source Excel document is located.

```csharp
//Output directory
string outputDir = "Your Output Directory";

//Source directory
string sourceDir = "Your Document Directory";
```

Make sure to replace "Your Output Directory" and "Your Document Directory" with the actual paths on your system. This dictates where Aspose will save the generated PDF and where it will find the Excel file.

## Step 2: Load the Sample Excel File

Next, you need to load the Excel file that contains the chart. Here’s how:

```csharp
//Load sample Excel file containing the chart.
Workbook wb = new Workbook(sourceDir + "sampleCreateChartPDFWithDesiredPageSize.xlsx");
```

The `Workbook` class is central to interacting with your Excel document. Ensure the path points correctly to your Excel file—an error here will prevent the rest of the code from executing.

## Step 3: Access the First Worksheet

Once the workbook is loaded, the next step is to access the worksheet containing the desired chart.

```csharp
//Access first worksheet.
Worksheet ws = wb.Worksheets[0];
```

In Aspose.Cells, worksheets are indexed starting from zero, so `Worksheets[0]` refers to the first sheet.

## Step 4: Access the First Chart

Now, let’s access the chart you want to export to a PDF. This step assumes that your worksheet contains at least one chart.

```csharp
//Access first chart inside the worksheet.
Chart ch = ws.Charts[0];
```

Again, this accesses the first chart in the worksheet; make sure your worksheet structure suits this approach.

## Step 5: Create PDF with Desired Page Size

Finally, it’s time to create the PDF from the chart with a specified page size. Here’s the magic line of code that does it all:

```csharp
//Create chart pdf with desired page size.
ch.ToPdf(outputDir + "outputCreateChartPDFWithDesiredPageSize.pdf", 7, 7, PageLayoutAlignmentType.Center, PageLayoutAlignmentType.Center);
```

In this code:
- The PDF will be saved to the output directory you specified before.
- The numbers `7, 7` represent the width and height of the desired page size, respectively.
- PageLayoutAlignmentType.Center ensures the chart is centered on the page.

## Step 6: Confirmation Message

To let yourself (and others) know that everything went smoothly, include a confirmation message at the end of your code:

```csharp
Console.WriteLine("CreateChartPDFWithDesiredPageSize executed successfully.");
```

This message will appear in the console window once the process completes, signaling that your PDF has been created without a hitch.

## Conclusion

Congratulations! You’ve just learned how to leverage Aspose.Cells for .NET to create a PDF from a chart contained in an Excel file. This powerful library streamlines the process of manipulating Excel documents and generating visual representations of data, saving you hours of manual formatting. Be sure to explore the plethora of other features Aspose.Cells offers beyond just PDF generation—you never know what may enhance your projects further!

## FAQ's

### What is Aspose.Cells for .NET used for?  
Aspose.Cells for .NET is used for creating, editing, and converting Excel documents programmatically in .NET applications.

### Can I use Aspose.Cells for free?  
Yes, Aspose.Cells offers a [free trial](https://releases.aspose.com/) for evaluation purposes.

### Is there a way to extend my trial beyond the initial period?  
You can apply for a [temporary license](https://purchase.aspose.com/temporary-license/) for extended testing.

### What if I encounter issues or have questions?  
You can seek help from the Aspose community on their [support forum](https://forum.aspose.com/c/cells/9).

### How can I purchase Aspose.Cells?  
You can buy Aspose.Cells from the [purchase page](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
