---
title: Extract Text from Gear Type Smart Art in Excel
linktitle: Extract Text from Gear Type Smart Art in Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to extract text from gear-type SmartArt in Excel using Aspose.Cells for .NET. Step-by-step guide and code example included.
weight: 10
url: /net/excel-shape-text-modifications/extract-text-gear-smart-art-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extract Text from Gear Type Smart Art in Excel

## Introduction
When working with Excel, you may encounter SmartArt graphics that help convey your messages in a visually appealing way. Among these graphics, gear-type SmartArt is a favorite for its hierarchical and directional flows, often used in project management or systems modeling. But what if you need to extract text from these shapes programmatically? This is where Aspose.Cells for .NET comes in handy! In this blog post, we will walk you through a step-by-step guide on how to extract text from gear-type SmartArt shapes in Excel using Aspose.Cells for .NET.
## Prerequisites
Before we dive in, there are some essential prerequisites you need to have in place. Don’t worry; it’s simple, and I’ll guide you through it.
### .NET Environment
Make sure you have a .NET development environment set up on your computer. This could be Visual Studio or any IDE of your choice that supports .NET development.
### Aspose.Cells for .NET
Next, you will need to install the Aspose.Cells library. This is the powerhouse that will enable you to manipulate Excel files seamlessly. You can download it from the [Aspose Releases page](https://releases.aspose.com/cells/net/). If you want to explore it first, take advantage of the [free trial](https://releases.aspose.com/).
### Basic Knowledge of C#
A basic understanding of C# programming is just what you need to follow along with this tutorial. If you're new to it, no worries—I'll design the steps to be as beginner-friendly as possible.
### Sample Excel File
For this tutorial, you will also need a sample Excel file that contains gear-type SmartArt shapes. You can easily create one or find a template online. Just ensure the SmartArt includes at least one gear-type shape.
## Import Packages
To start coding, you’ll need to import the necessary packages. Here’s how to do it:
### Create a New Project
1. Open your .NET IDE.
2. Create a new project. For example, select 'Console Application' under the .NET options.
3. Give your project a name and set the desired framework. 
### Add References
To use Aspose.Cells, you’ll need to add the library references to your project:
1. Right-click on your project name in the Solution Explorer.
2. Choose “Manage NuGet Packages”.
3. Search for "Aspose.Cells" and install it.
Once installed, you are all set for coding!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Now, let’s break down the code you’ll use to extract the text. We will do this step by step.
## Step 1: Set Up the Source Directory
Begin by defining the directory where your Excel file is located:
```csharp
// Source directory
string sourceDir = "Your Document Directory";
```
Make sure to replace `"Your Document Directory"` with the actual path to your Excel file.
## Step 2: Load the Excel Workbook
Next, we will load the Excel workbook. This is how we can access its contents:
```csharp
// Load sample Excel file containing gear type smart art shape.
Workbook wb = new Workbook(sourceDir + "sampleExtractTextFromGearTypeSmartArtShape.xlsx");
```
This piece will load your sample Excel workbook.
## Step 3: Access the First Worksheet
Now that we have loaded the workbook, let’s access the first worksheet where our SmartArt exists:
```csharp
// Access first worksheet.
Worksheet ws = wb.Worksheets[0];
```
This retrieves the first worksheet for further manipulation.
## Step 4: Access the First Shape
Next, we need to access the first shape within our worksheet. By doing this, we can navigate through our SmartArt graphics:
```csharp
// Access first shape.
Aspose.Cells.Drawing.Shape sh = ws.Shapes[0];
```
Here, we are focusing on the first shape, which we assume is the SmartArt we need.
## Step 5: Get the Group Shape
Once we have our shape, it’s time to get the result of our SmartArt representation:
```csharp
// Get the result of gear type smart art shape in the form of group shape.
Aspose.Cells.Drawing.GroupShape gs = sh.GetResultOfSmartArt();
```
This retrieves our gear-type SmartArt as a grouped shape.
## Step 6: Extract Individual Shapes
Now, let's extract the individual shapes that make up our SmartArt:
```csharp
// Get the list of individual shapes consisting of group shape.
Aspose.Cells.Drawing.Shape[] shps = gs.GetGroupedShapes();
```
This array will hold all the individual shapes that we need to loop through.
## Step 7: Extract and Print Text
Finally, we can loop through our shapes array and extract the text from any gear-type shape:
```csharp
// Extract the text of gear type shapes and print them on console.
for (int i = 0; i < shps.Length; i++)
{
    Aspose.Cells.Drawing.Shape s = shps[i];
    if (s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear9 || s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear6)
    {
        Console.WriteLine("Gear Type Shape Text: " + s.Text);
    }
}
```
In this loop, we check the type of shape and print the text if it's a gear-type shape.
## Step 8: Execution Confirmation
Lastly, you may want to add a confirmation message once the process is completed successfully:
```csharp
Console.WriteLine("ExtractTextFromGearTypeSmartArtShape executed successfully.");
```
With this, your extraction is complete, and you should see your text output in the console!
## Conclusion
Congratulations! You’ve just learned how to extract text from gear-type SmartArt shapes in Excel using Aspose.Cells for .NET. This handy technique opens doors to automating reports or documentation that relies on visual data representation. Whether you're a seasoned developer or just starting, controlling and extracting information from SmartArt can streamline your workflow and make you more efficient. Don’t forget to explore the detailed [Aspose.Cells Documentation](https://reference.aspose.com/cells/net/) for further capabilities.
## FAQ's
### What is Aspose.Cells?
Aspose.Cells is a .NET library that allows developers to create and manipulate Excel files easily.
### Can I use Aspose.Cells with other languages?
Yes! Aspose.Cells is available in multiple programming languages, including Java and Python.
### Do I need to purchase Aspose.Cells for .NET?
Aspose.Cells offers a free trial, but for extended use, a purchase is required. You can find purchasing options [here](https://purchase.aspose.com/buy).
### Is there support available for Aspose.Cells users?
Absolutely! You can find community support at the [Aspose.Cells forum](https://forum.aspose.com/c/cells/9).
### Can I extract other SmartArt types using this method?
Yes, with slight modifications, you can extract text from various SmartArt shapes by changing the conditions in your code.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
