---
title: Get Connection Points of Shape in Excel
linktitle: Get Connection Points of Shape in Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to get shape connection points in Excel with Aspose.Cells for .NET. Follow our step-by-step guide to easily extract and display shape points programmatically.
weight: 11
url: /net/excel-shapes-controls/get-connection-points-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Get Connection Points of Shape in Excel

## Introduction
When working with Excel files programmatically, we often need to interact with shapes embedded in the sheets. One of the more advanced tasks you can perform is extracting connection points from a shape. Connection points are used to attach shapes with connectors and manage their layout more precisely. If you’re looking to get the connection points of a shape in Excel, Aspose.Cells for .NET is the tool you need. In this tutorial, we will take you through a step-by-step process to achieve this.
## Prerequisites
Before diving into the code, ensure you have the following prerequisites:
- Aspose.Cells for .NET: You will need to have Aspose.Cells installed in your development environment. If you don't have it yet, you can [download the latest version here](https://releases.aspose.com/cells/net/).
- Development Environment: Make sure you have a working installation of Visual Studio or any other .NET-compatible IDE.
- Basic Knowledge of C#: This tutorial assumes that you have a basic understanding of C# programming and object-oriented principles.
You can also sign up for a [free trial of Aspose.Cells](https://releases.aspose.com/) if you haven’t already. This will give you access to all the features required for this guide.

## Import Packages
To work with Aspose.Cells in your project, you need to include the necessary namespaces. The following import statements should be placed at the top of your code:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
These namespaces give you access to the core functionality of Aspose.Cells and allow you to manipulate worksheets and shapes.

## Step-by-Step Guide to Get Connection Points of a Shape
In this section, we will walk you through how to extract the connection points of a shape within an Excel worksheet. Follow each step carefully for a clear understanding.
## Step 1: Instantiate a New Workbook
First things first, we need to create an instance of the `Workbook` class. This represents an Excel file in Aspose.Cells. If you don’t have an existing file, no problem—you can start with a blank workbook.
```csharp
// Instantiate a new Workbook
Workbook workbook = new Workbook();
```
In this step, we’ve created an empty Excel workbook, but you can also load an existing one by passing the file path to the `Workbook` constructor.
## Step 2: Access the First Worksheet
Next, we need to access the worksheet where we want to work with shapes. In this case, we'll use the first worksheet of the workbook.
```csharp
// Get the first worksheet in the workbook
Worksheet worksheet = workbook.Worksheets[0];
```
This line accesses the first worksheet from the collection of worksheets in the workbook. If you're working with a specific sheet, you can replace the index `0` with the desired index.
## Step 3: Add a New Text Box (Shape)
Now, let’s add a new shape to the worksheet. We’ll create a text box, which is a type of shape. You can also add other types of shapes, but for simplicity, we’ll stick with a text box in this tutorial.
```csharp
// Add a new textbox to the collection
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
Here’s what we’ve done:
- Added a text box at row `2`, column `1`.
- Set the text box’s dimensions to `160` units in width and `200` units in height.
## Step 4: Access the Shape from the Shapes Collection
Once we’ve added the text box, it becomes part of the worksheet’s shapes collection. Now we’ll access that shape using the `Shapes` collection.
```csharp
// Access the shape (textbox) from the shapes collection
Shape shape = workbook.Worksheets[0].Shapes[0];
```
In this step, we retrieve the first shape (our text box) from the collection. If you have multiple shapes, you can specify the index or even find the shape by name.
## Step 5: Retrieve Connection Points
Now that we have our shape, let’s extract its connection points. These points are used for attaching connectors to the shape. The `ConnectionPoints` property of the shape returns all connection points available.
```csharp
// Get all the connection points in this shape
var connectionPoints = shape.ConnectionPoints;
```
This gives us a collection of all the connection points available for that shape.
## Step 6: Display Connection Points
Finally, we want to display the coordinates of each connection point. This is where we loop through the connection points and print them out to the console.
```csharp
// Display all the shape points
foreach (var pt in connectionPoints)
{
    System.Console.WriteLine(string.Format("X = {0}, Y = {1}", pt.X, pt.Y));
}
```
This loop iterates over each connection point and prints the `X` and `Y` coordinates. This can be useful for debugging or visually confirming the connection points of a shape.
## Step 7: Execute and Complete
Once you've set up all the steps above, you can run the code. Here’s the final line that ensures the process completes successfully:
```csharp
System.Console.WriteLine("GetShapeConnectionPoints executed successfully.");
```
This line simply logs a message to the console indicating that the process has been completed.

## Conclusion
In this tutorial, we covered how to retrieve connection points of a shape in Excel using Aspose.Cells for .NET. By breaking the task into small, digestible steps, we explored the process of creating a workbook, adding a shape, and extracting the connection points.
By understanding how to manipulate shapes programmatically, you unlock a world of possibilities for building dynamic and interactive Excel sheets. Whether you’re building reports, designing dashboards, or creating diagrams, this knowledge will come in handy.
## FAQ's
### What is a connection point in a shape?
A connection point is a specific point on a shape where you can attach connectors or link it to other shapes.
### Can I retrieve connection points for all shapes in a worksheet?
Yes, Aspose.Cells allows you to retrieve connection points for any shape that supports them. Simply loop through the shapes collection in the worksheet.
### Do I need a license to use Aspose.Cells?
Yes, while you can try it for free, a license is required for full features. You can [buy a license here](https://purchase.aspose.com/buy) or get a [temporary license](https://purchase.aspose.com/temporary-license/).
### How can I add different types of shapes in Aspose.Cells?
You can use the `Add` method for shapes like rectangles, ellipses, and more. Each shape has specific parameters you can customize.
### How do I load an existing Excel file instead of creating a new one?
To load an existing file, pass the file path to the `Workbook` constructor, like this:  
```csharp
Workbook workbook = new Workbook("path_to_file.xlsx");
```

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
