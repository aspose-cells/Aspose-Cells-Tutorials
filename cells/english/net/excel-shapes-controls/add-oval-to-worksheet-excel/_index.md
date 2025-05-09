---
title: Add Oval to Worksheet in Excel
linktitle: Add Oval to Worksheet in Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to add an oval to an Excel worksheet using Aspose.Cells for .NET. Step-by-step guide with detailed code explanations.
weight: 17
url: /net/excel-shapes-controls/add-oval-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Add Oval to Worksheet in Excel

## Introduction
Creating stunning and interactive Excel files can involve more than just numbers and formulas. Shapes like ovals can add a visual appeal or provide functional elements in your worksheets. In this tutorial, we'll explore how to use Aspose.Cells for .NET to add ovals to an Excel worksheet programmatically. Whether you're looking to add some flair or functionality, we’ve got you covered with a step-by-step guide that breaks everything down.
## Prerequisites
Before diving into the code, there are a few things you need to have in place:
1. Aspose.Cells for .NET Library: You can download it from [here](https://releases.aspose.com/cells/net/) or install it using NuGet in Visual Studio.
2. Development Environment: A C# IDE like Visual Studio.
3. Basic Understanding of C#: You should be familiar with basic coding concepts in C#.
Also, remember to set up your project by installing the Aspose.Cells for .NET library. If you don't have a license yet, you can apply for a [temporary license](https://purchase.aspose.com/temporary-license/) or use the [free trial](https://releases.aspose.com/) version.
## Import Packages
Before writing any code, make sure you've included the required namespaces. Here's the C# code snippet to ensure you’re using the right libraries:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## Step 1: Set Up Your Directory
The first step in adding an oval to an Excel sheet is to specify where your Excel file will be saved. Let's define the directory path and ensure the directory exists before saving our work.

We’ll create a directory path and verify if it exists. If the folder doesn’t exist, it will be created.
```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
// Create directory if it is not already present.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
This step is crucial as it ensures that your file is saved in a proper location, and you don't run into file path issues later on.
## Step 2: Initialize a New Workbook
Next, we need to create a new workbook in which we will add our oval shapes. The workbook represents an Excel file, and we can add content or shapes into it.

In this step, we instantiate a new `Workbook` object that will serve as our Excel file container.
```csharp
// Instantiate a new Workbook.
Workbook excelbook = new Workbook();
```
## Step 3: Add the First Oval Shape
Now comes the fun part—adding an oval shape to the worksheet. This oval could represent a visual element like a button or a highlight. We'll start by adding the first oval shape to the first worksheet of our workbook.

Here, we use the `Shapes.AddOval()` method to create an oval on the worksheet at a specific row and column.
```csharp
// Add an oval shape.
Aspose.Cells.Drawing.Oval oval1 = excelbook.Worksheets[0].Shapes.AddOval(2, 0, 2, 0, 130, 160);
```
The parameters inside `AddOval()` are as follows:
- The first two numbers represent the row and column for the top-left corner of the oval.
- The next two numbers represent the height and width of the oval.
## Step 4: Set the Oval's Placement and Style
Once the oval is created, we can set its position, line weight, and dash style. The `Placement` property determines how the oval behaves when you resize or move cells in the worksheet.

We make the oval free-floating and adjust its appearance.
```csharp
// Set the placement of the oval.
oval1.Placement = PlacementType.FreeFloating;
// Set the line weight.
oval1.Line.Weight = 1;
// Set the dash style of the oval.
oval1.Line.DashStyle = MsoLineDashStyle.Solid;
```
This allows the oval to move freely within the worksheet, and its line weight and style are set for visual consistency.
## Step 5: Add Another Oval (Circle) Shape
Why stop at one? In this step, we'll add another oval shape, this time creating a perfect circle by making the height and width the same.

We create another oval, place it in a different location, and ensure it has a circular shape by setting equal height and width.
```csharp
// Add another oval (circle) shape.
Aspose.Cells.Drawing.Oval oval2 = excelbook.Worksheets[0].Shapes.AddOval(9, 0, 2, 15, 130, 130);
```
## Step 6: Style the Second Oval
Just like before, we’ll adjust the placement, weight, and dash style of this second oval (or circle).

We apply similar properties to the second oval to match the style of the first.
```csharp
// Set the placement of the oval.
oval2.Placement = PlacementType.FreeFloating;
// Set the line weight.
oval2.Line.Weight = 1;
// Set the dash style of the oval.
oval2.Line.DashStyle = MsoLineDashStyle.Solid;
```
## Step 7: Save the Workbook
Finally, we need to save the workbook with the ovals we’ve just added. Saving the file ensures that all our changes are stored.

We save the workbook to the directory path we defined earlier.
```csharp
// Save the excel file.
excelbook.Save(dataDir + "book1.out.xls");
```
And that's it! You've successfully added ovals to your Excel worksheet and saved the file.
## Conclusion
Adding shapes like ovals to an Excel sheet using Aspose.Cells for .NET is not only straightforward but also a fun way to enhance your spreadsheets with additional visual elements. Whether for design purposes or adding clickable elements, shapes can play a significant role in how your Excel files look and function. So, the next time you're working on a project that requires interactive or visually appealing Excel sheets, you know exactly how to add those perfect ovals!
## FAQ's
### Can I add other shapes like rectangles or lines using Aspose.Cells for .NET?
Yes, you can add various shapes like rectangles, lines, and arrows using the `Shapes` collection in Aspose.Cells.
### Is it possible to resize the ovals after adding them?
Absolutely! You can modify the height and width properties of the ovals after adding them.
### What file formats can I save the workbook in besides XLS?
Aspose.Cells supports multiple formats like XLSX, CSV, and PDF, among others.
### Can I modify the color of the oval's outline?
Yes, you can change the oval's line color using the `Line.Color` property.
### Is it necessary to have a license for Aspose.Cells?
While you can try Aspose.Cells with a free trial, you'll need a [license](https://purchase.aspose.com/buy) for long-term use or for accessing advanced features.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
