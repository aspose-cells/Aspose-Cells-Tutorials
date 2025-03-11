---
title: Rotate Text with Shape in Excel
linktitle: Rotate Text with Shape in Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to rotate text with shapes in Excel using Aspose.Cells for .NET. Follow this step-by-step guide for perfect Excel presentation.
weight: 12
url: /net/excel-shape-text-modifications/rotate-text-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rotate Text with Shape in Excel

## Introduction
In the world of Excel, visual representation is just as important as the data itself. Whether you're crafting a report or designing a dynamic dashboard, the way information is laid out can dramatically impact its readability and overall appearance. So, have you ever wanted to rotate text to align it stylishly with shapes? You’re in luck! In this tutorial, we'll dive into how to rotate text with shapes using Aspose.Cells for .NET, ensuring your spreadsheets not only inform but also impress.
## Prerequisites
Before we get started, let’s make sure you’ve got everything you need:
1. Visual Studio: Ensure you have Visual Studio installed on your machine, as that’s where we’ll be writing our code.
2. Aspose.Cells for .NET: You’ll need the Aspose.Cells library. You can [download the latest version here](https://releases.aspose.com/cells/net/) or try it out for free with a [free trial](https://releases.aspose.com/).
3. Basic Knowledge of C#: Familiarity with C# and .NET environment will be helpful, although we’ll guide you every step of the way.
4. Excel File: A sample Excel file, let's call it `sampleRotateTextWithShapeInsideWorksheet.xlsx`, is needed to test our code. You should place this file in a directory that you can easily access.
Got everything ready? Fantastic! Let’s jump into the fun part.
## Import Packages
To get kicked off, we need to import the necessary packages into our project. Here’s how you do that:
### Create a New Project
1. Open Visual Studio.
2. Select "Create a new project."
3. Choose "Console App" and select C# as your preferred programming language.
### Install Aspose.Cells
Now, let’s add Aspose.Cells to your project. You can do this using NuGet Package Manager:
1. Open "Tools" in the top menu.
2. Select "NuGet Package Manager" and then "Manage NuGet Packages for Solution."
3. Search for "Aspose.Cells."
4. Click "Install" to add it to your project.
### Add Using Directive
At the top of your main C# file, you need to add the following directive:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Now we’re all set to start coding!
Let’s break down the process into easily digestible steps. Here’s how to rotate text with shapes in an Excel file:
## Step 1: Set Up Your Directory Paths
First, you need to set up your source and output directories where your Excel files will be stored. Here’s how:
```csharp
//Source directory
string sourceDir = "Your Document Directory"; // Set your document directory
//Output directory
string outputDir = "Your Document Directory"; // Set your output directory
```
Replace `"Your Document Directory"` with the actual path where your `sampleRotateTextWithShapeInsideWorksheet.xlsx` file is located.
## Step 2: Load the Sample Excel File
Now, let’s load the sample Excel file. This is crucial, as we want to manipulate the existing data.
```csharp
//Load sample Excel file.
Workbook wb = new Workbook(sourceDir + "sampleRotateTextWithShapeInsideWorksheet.xlsx");
```
## Step 3: Access the Worksheet
Once the file is loaded, we need to access the specific worksheet we want to modify. In our case, it’s the first worksheet.
```csharp
//Access first worksheet.
Worksheet ws = wb.Worksheets[0];
```
## Step 4: Modify a Cell
Next, we’ll modify a specific cell to display a message. In our example, we’ll use cell B4.
```csharp
//Access cell B4 and add a message inside it.
Cell b4 = ws.Cells["B4"];
b4.PutValue("Text is not rotating with shape because RotateTextWithShape is false.");
```
This step is all about communication—ensuring whoever opens this sheet understands what we’re tweaking.
## Step 5: Access the First Shape
To rotate text, we need a shape to work with. Here, we’ll access the first shape in the worksheet.
```csharp
//Access first shape.
Shape sh = ws.Shapes[0];
```
## Step 6: Adjust Shape Text Alignment
Here's where the magic happens. We will adjust the text alignment properties of the shape.
```csharp
//Access shape text alignment.
Aspose.Cells.Drawing.Texts.ShapeTextAlignment shapeTextAlignment = sh.TextBody.TextAlignment;
//Do not rotate text with shape by setting RotateTextWithShape as false.
shapeTextAlignment.RotateTextWithShape = false;
```
By setting `RotateTextWithShape` to false, we ensure that the text remains upright and does not rotate with the shape, thus keeping everything neat and organized.
## Step 7: Save the Output Excel File
Finally, let’s save our changes to a new Excel file. This makes sure we don't lose our edits and have a tidy output.
```csharp
//Save the output Excel file.
wb.Save(outputDir + "outputRotateTextWithShapeInsideWorksheet.xlsx");
```
And that’s it! Your output file is now saved, including the text in cell B4 and the adjustments made to the shape.
## Step 8: Execute the Code
In your `Main` method, wrap all of the above code snippets, and run your project. See the changes reflect in your output file!
```csharp
Console.WriteLine("RotateTextWithShapeInsideWorksheet executed successfully.");
```
## Conclusion
Rotating text with shapes in Excel using Aspose.Cells for .NET might seem like an elaborate process at first, but it’s quite straightforward once you break it down. By following these simple steps, you can customize your spreadsheets to look more professional and visually appealing. Now, whether you’re doing this for a client or your personal projects, everyone will be raving about the quality of your work!
## FAQ's
### Can I use Aspose.Cells for free?
Yes! You can use the [free trial](https://releases.aspose.com/) to try out the library.
### What versions of Excel does Aspose.Cells support?
Aspose.Cells supports a variety of Excel formats, including XLS, XLSX, CSV, and more.
### Is it possible to rotate text with shapes in older Excel versions?
Yes, the functionality can be applied to older formats supported by Aspose.Cells.
### Where can I find more documentation about Aspose.Cells?
You can explore the comprehensive [documentation](https://reference.aspose.com/cells/net/) for more insights.
### How do I get support for Aspose.Cells?
You can ask for support by visiting the [Aspose forum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
