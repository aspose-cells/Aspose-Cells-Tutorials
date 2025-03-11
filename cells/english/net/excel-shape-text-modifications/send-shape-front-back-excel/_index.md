---
title: Send Shape Front or Back in Excel
linktitle: Send Shape Front or Back in Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Discover how to send shapes to the front or back in Excel using Aspose.Cells for .NET. This guide provides a step-by-step tutorial with tips.
weight: 16
url: /net/excel-shape-text-modifications/send-shape-front-back-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Send Shape Front or Back in Excel

## Introduction
When working with Excel files, you may find yourself needing more control over the visual elements in your spreadsheet. Shapes, like images and graphics, can enhance your data’s presentation. But what happens when these shapes overlap or need to be reordered? This is where Aspose.Cells for .NET shines. In this tutorial, we'll walk you through the steps to manipulate shapes in an Excel worksheet, specifically sending shapes to the front or back of other shapes. If you're ready to amp up your Excel game, let’s dive right in!
## Prerequisites
Before we get started, you’ll need to have a few things in place:
1. Installation of Aspose.Cells Library: Ensure you have the Aspose.Cells library installed for .NET. You can find it [here](https://releases.aspose.com/cells/net/).
2. Development Environment: Make sure you have a development environment set up with .NET support, such as Visual Studio.
3. Basic Knowledge of C#: Familiarity with C# programming will help you understand the code snippets better.
Alright, you've ticked all the boxes on the prerequisites list? Great! Let’s move on to the fun part – writing some code!
## Import Packages
Before we dive into the actual coding, let’s import the necessary packages. Just add the following using directive at the top of your C# file:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
These namespaces are crucial since they contain the classes and methods we'll use to manipulate Excel files and shapes.
## Step 1: Define Your File Paths
In this first step, we need to establish the source and output directories. This is where your Excel file is located and where you want to save the modified file.
```csharp
//Source directory
string sourceDir = "Your Document Directory";
//Output directory
string outputDir = "Your Document Directory";
```
Replace `"Your Document Directory"` with the actual path where your Excel files are stored.
## Step 2: Load the Workbook
Now that we have our directories set, let’s load the workbook (the Excel file) that contains the shapes we want to manipulate.
```csharp
//Load source Excel file
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
This line of code initializes a new `Workbook` object, loading the specified Excel file into memory so that we can work with it.
## Step 3: Access the Worksheet 
Next, we need to access the specific worksheet where our shapes reside. For this example, we'll use the first worksheet.
```csharp
//Access first worksheet
Worksheet ws = wb.Worksheets[0];
```
By referencing `Worksheets[0]`, we’re targeting the first sheet of our workbook. If your shapes are on a different sheet, adjust the index accordingly.
## Step 4: Access the Shapes
With access to the worksheet ready, let’s grab the shapes we're interested in. For this example, we’ll access the first and fourth shapes.
```csharp
//Access first and fourth shape
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
These lines get the specific shapes from the worksheet based on their index.
## Step 5: Print the Z-Order Position of Shapes
Before we move any shapes, let's print out their current Z-Order position. This helps us track their positioning before we make changes.
```csharp
//Print the Z-Order position of the shape
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
By calling `ZOrderPosition`, we can see where each shape sits in the drawing order.
## Step 6: Send the First Shape to Front
Now it's time for action! Let's send the first shape to the front of the Z-Order.
```csharp
//Send this shape to front
sh1.ToFrontOrBack(2);
```
By passing `2` to `ToFrontOrBack`, we’re instructing Aspose.Cells to bring this shape to the front. 
## Step 7: Print the Z-Order Position of the Second Shape
Before we send the second shape to the back, let’s check where it is positioned.
```csharp
//Print the Z-Order position of the shape
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
This gives us insight into the position of the fourth shape before we make any changes.
## Step 8: Send the Fourth Shape to Back
Finally, we’re going to send the fourth shape to the back of the Z-Order stack.
```csharp
//Send this shape to back
sh4.ToFrontOrBack(-2);
```
Using `-2` as the parameter sends the shape towards the back of the stack, ensuring it won’t obstruct other shapes or text.
## Step 9: Save the Workbook 
The last step is to save your workbook with the newly positioned shapes.
```csharp
//Save the output Excel file
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
This command saves the modified workbook to the specified output directory.
## Step 10: Confirmation Message
Finally, let’s provide a simple confirmation to let us know that our task completed successfully.
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
And that wraps up the code for our tutorial!
## Conclusion
Manipulating shapes in Excel using Aspose.Cells for .NET is not only straightforward but also powerful. By following this guide, you should now be able to send shapes to the front or back with ease, allowing for better control over your Excel presentations. With these tools at your disposal, you're ready to enhance the visual appeal of your spreadsheets.
## FAQ's
### What programming language do I need for Aspose.Cells?  
You need to use C# or any .NET-supported language to work with Aspose.Cells.
### Can I try Aspose.Cells for free?  
Yes, you can start with a free trial of Aspose.Cells [here](https://releases.aspose.com/).
### What kind of shapes can I manipulate in Excel?  
You can manipulate various shapes such as rectangles, circles, lines, and images.
### How can I get support for Aspose.Cells?  
You can visit their community forum for any support or queries [here](https://forum.aspose.com/c/cells/9).
### Is there a temporary license available for Aspose.Cells?  
Yes, you can request a temporary license [here](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
