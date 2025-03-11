---
title: Add Arc to Worksheet in Excel
linktitle: Add Arc to Worksheet in Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Learn to add arcs to Excel worksheets using Aspose.Cells for .NET. Follow our step-by-step guide to enhance your spreadsheet designs.
weight: 16
url: /net/excel-shapes-controls/add-arc-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Arc to Worksheet in Excel

## Introduction
Creating visually appealing Excel spreadsheets is crucial for data presentation, and the Aspose.Cells library provides developers with robust tools to accomplish this task. One interesting feature you might want to incorporate into your Excel documents is the ability to add shapes, such as arcs. In this tutorial, we’ll walk through step-by-step how to add arcs to an Excel worksheet using Aspose.Cells for .NET. By the end of this article, you'll not only learn how to add arcs but also gain insight into managing shapes in general.
## Prerequisites
Before we dive into the intricacies of adding arcs to your worksheet, it’s essential to ensure you have a few things in place. Here are the prerequisites you'll need to get started:
1. Visual Studio: You’ll need to have Visual Studio installed on your computer as we will be using C# as our programming language.
2. .NET Framework: Ensure you have the .NET Framework or .NET Core installed. Aspose.Cells supports both.
3. Aspose.Cells for .NET: You must have the Aspose.Cells library. You can download it from the [Aspose.Cells Downloads](https://releases.aspose.com/cells/net/) page.
4. Basic Understanding of C#: Familiarity with C# will help you follow along with the code snippets without much hassle.
## Import Packages
To start working with Aspose.Cells in your project, you need to import the necessary packages. Here’s how to do it:
### Create a New Project
- Open Visual Studio.
- Choose "Create a new project."
- Select a template that works with .NET (like Console Application).
  
### Add Aspose.Cells References
- Right-click on your project in the Solution Explorer.
- Select "Manage NuGet Packages."
- Search for “Aspose.Cells” and install it.
Now you're ready to start coding the arc addition.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Here’s a step-by-step breakdown of the code that demonstrates how to add arcs to a worksheet in Excel.
## Step 1: Setting Up the Directory
The first step is to set up a directory where you'll save your Excel file. This helps in managing your output files easily.
```csharp
string dataDir = "Your Document Directory";
// Create directory if it is not already present.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
In this code snippet, we specify the path to the document directory. We also check if the directory exists; if not, we create it. This sets the groundwork for our output.
## Step 2: Instantiate a Workbook
Next, let’s create a new workbook instance.
```csharp
// Instantiate a new Workbook.
Workbook excelbook = new Workbook();
```
This line creates a new Excel workbook. Think of this as a blank canvas where we can add shapes, data, and more.
## Step 3: Add the First Arc Shape
Now, let’s add our first arc shape to the worksheet.
```csharp
// Add an arc shape.
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
Here, we are adding an arc to the first worksheet. The parameters define the position and size of the arc: `(left, top, width, height, startAngle, endAngle)`. It’s like plotting a segment of a circle!
## Step 4: Customize the First Arc
After adding the arc, you might want to customize its appearance.
```csharp
// Set the fill shape color
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
// Set the placement of the arc.
arc1.Placement = PlacementType.FreeFloating;           
// Set the line weight.
arc1.Line.Weight = 1;      
// Set the dash style of the arc.
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
In this section, we're customizing the arc. We set its fill type to solid color (blue in this case), define how it’s placed, establish the line weight, and choose a dash style. Basically, we're dressing up our arc to make it visually appealing!
## Step 5: Add a Second Arc Shape
Let’s add another arc shape to provide more context.
```csharp
// Add another arc shape.
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Similar to the first arc, we’re adding a second arc on the same worksheet. The coordinates here are a bit shifted to position it differently.
## Step 6: Customize the Second Arc
Just like we did with the first arc, we'll customize the second one too.
```csharp
// Set the line color
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
// Set the placement of the arc.
arc2.Placement = PlacementType.FreeFloating;          
// Set the line weight.
arc2.Line.Weight = 1;           
// Set the dash style of the arc.
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Here, we’re giving the second arc the same styling as the first. You could change the color or styling as desired for uniqueness or thematic purposes.
## Step 7: Save the Workbook
Finally, it's time to save your newly created workbook with the arcs.
```csharp
// Save the excel file.
excelbook.Save(dataDir + "book1.out.xls");
```
This line works like hitting the save button. We're saving our work to the specified location with a designated filename. Make sure to check your directory to see your masterpiece in Excel format!
## Conclusion
In this tutorial, we've explored the process of adding arc shapes to an Excel worksheet using Aspose.Cells for .NET. Through a simple step-by-step guide, you've learned how to create a new workbook, add arcs, customize their appearance, and save your document. This capability not only enhances the visual appeal of your spreadsheets but also makes your data presentations more informative. Whether you’re creating charts, reports, or just experimenting, using shapes like arcs can add a creative twist to your projects.
## FAQ's
### What is Aspose.Cells?
Aspose.Cells is a powerful library that allows developers to create, manipulate, and convert Excel files programmatically without the need for Microsoft Excel.
### Do I need to install Microsoft Excel to use Aspose.Cells?
No, Aspose.Cells is completely independent and does not require Microsoft Excel to be installed.
### Can I try Aspose.Cells for free?
Yes, you can try out Aspose.Cells using their [Free Trial](https://releases.aspose.com/).
### What programming languages does Aspose.Cells support?
Aspose.Cells supports multiple languages, including C#, VB.NET, and more.
### Where can I get support for Aspose.Cells?
You can get support through the [Aspose Forum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
