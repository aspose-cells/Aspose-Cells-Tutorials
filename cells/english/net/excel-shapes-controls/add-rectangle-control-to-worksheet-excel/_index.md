---
title: Add Rectangle Control to Worksheet in Excel
linktitle: Add Rectangle Control to Worksheet in Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to add a rectangle control to an Excel worksheet using Aspose.Cells for .NET with a detailed, step-by-step guide.
weight: 25
url: /net/excel-shapes-controls/add-rectangle-control-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Add Rectangle Control to Worksheet in Excel

## Introduction
When it comes to automating Excel tasks, Aspose.Cells for .NET is a powerful tool that can help you achieve a variety of objectives, one of which is adding shapes like rectangles to your worksheets. In this guide, we’ll explore how to add a rectangle control to an Excel worksheet using Aspose.Cells for .NET. By the end, you’ll be able to create, customize, and save a worksheet with a rectangle control embedded in it.
But before diving in, let’s talk about the prerequisites.
## Prerequisites
To follow along with this tutorial, ensure you have the following prerequisites in place:
1. Aspose.Cells for .NET library: If you haven’t already, [download the library](https://releases.aspose.com/cells/net/) or install it using NuGet in Visual Studio.
2. .NET Framework: You need to have the .NET development environment set up on your machine.
3. Basic knowledge of C#: Although we’ll guide you step-by-step, basic familiarity with C# and object-oriented programming is beneficial.
4. License: Using Aspose.Cells in evaluation mode works fine for basic tasks, but for full functionality, consider getting a [temporary license](https://purchase.aspose.com/temporary-license/) or purchasing one from [here](https://purchase.aspose.com/buy).
Now, let’s dive into the code!
## Import Packages
To get started with Aspose.Cells, make sure you have imported the necessary namespaces into your project. These imports will allow access to various classes and methods that you need to interact with Excel files.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
These lines ensure that your project can interact with file directories (`System.IO`), Excel workbooks (`Aspose.Cells`), and shape drawing (`Aspose.Cells.Drawing`).
Now, let’s break down the process into simple steps so you can easily follow along and replicate this in your own projects.
## Step 1: Setting Up the Directory Path
The first thing you need to do is define the directory where your Excel file will be saved. This step ensures that your project knows where to create and store the output file.
### Defining the Data Directory
```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```
Here, you specify the directory path where the Excel file will be stored. You can replace `"Your Document Directory"` with the actual path on your machine, or dynamically create a folder if it doesn’t exist.
### Checking and Creating the Directory
```csharp
// Create directory if it is not already present.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
This block checks if the directory exists. If not, it creates one. Think of it like having your file cabinet ready before you store any documents.
## Step 2: Instantiating a New Workbook
In this step, you create a new Excel workbook using the `Aspose.Cells.Workbook` class. This will serve as the container for your worksheet and shapes.
```csharp
// Instantiate a new Workbook.
Workbook excelbook = new Workbook();
```
By calling the `Workbook` constructor, you now have a blank Excel workbook ready for customization.
## Step 3: Adding a Rectangle Control
Here’s where the magic happens. You’ll add a rectangle shape to the first worksheet of your workbook.
```csharp
// Add a rectangle control.
Aspose.Cells.Drawing.RectangleShape rectangle = excelbook.Worksheets[0].Shapes.AddRectangle(3, 0, 2, 0, 70, 130);
```
Let’s break this down:
- `excelbook.Worksheets[0]`: This accesses the first worksheet in your workbook.
- `.Shapes.AddRectangle(3, 0, 2, 0, 70, 130)`: This adds a rectangle shape to the worksheet. The parameters here define the position (row and column), as well as the width and height of the rectangle.
## Step 4: Customizing the Rectangle
Just adding a rectangle isn’t enough—you’ll want to customize it. In this step, we’ll set the placement, line weight, and dash style of the rectangle.
### Setting the Placement
```csharp
// Set the placement of the rectangle.
rectangle.Placement = PlacementType.FreeFloating;
```
This specifies that the rectangle is free-floating, meaning it won’t be bound by cell dimensions.
### Setting the Line Weight
```csharp
// Set the line weight.
rectangle.Line.Weight = 4;
```
Here, we set the line thickness of the rectangle to 4 points. The higher the number, the thicker the line.
### Setting the Dash Style
```csharp
// Set the dash style of the rectangle.
rectangle.Line.DashStyle = MsoLineDashStyle.Solid;
```
This line sets the dash style of the rectangle’s border to solid. You can experiment with different styles like `Dash` or `Dot` depending on your requirements.
## Step 5: Saving the Workbook
Once the rectangle is added and customized, the final step is to save the workbook to the specified directory.
```csharp
// Save the excel file.
excelbook.Save(dataDir + "book1.out.xls");
```
This saves the workbook as an `.xls` file in the folder you defined earlier. You can modify the file format by changing the extension, such as `.xlsx` if you prefer the newer Excel format.
## Conclusion
And there you have it! Adding a rectangle control to an Excel worksheet using Aspose.Cells for .NET is a straightforward process once you break it down step by step. Whether you need to add shapes for visual appeal, highlight sections of your data, or customize your reports, Aspose.Cells gives you the flexibility to do so programmatically.
This guide should have equipped you with all the knowledge you need to start adding shapes like rectangles to your Excel sheets with Aspose.Cells. Now it’s time to experiment and see what else you can achieve with this powerful library!
## FAQ's
### Can I add other shapes like circles or lines using Aspose.Cells for .NET?  
Yes, Aspose.Cells allows you to add a variety of shapes, including circles, lines, arrows, and more.
### What other properties can I set for the rectangle control?  
You can customize the fill color, line color, transparency, and even add text within the rectangle.
### Is Aspose.Cells compatible with .NET Core?  
Yes, Aspose.Cells supports .NET Core, as well as .NET Framework and other .NET-based platforms.
### Can I position the rectangle relative to a specific cell?  
Yes, you can place the rectangle within specific rows and columns, or use the `PlacementType` to control how it is anchored.
### Is there a free trial available for Aspose.Cells?  
Yes, you can get a [free trial](https://releases.aspose.com/) from the website to test the library’s features before purchasing.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
