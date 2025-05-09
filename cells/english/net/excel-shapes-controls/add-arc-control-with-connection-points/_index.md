---
title: Add Arc Control with Connection Points
linktitle: Add Arc Control with Connection Points
second_title: Aspose.Cells .NET Excel Processing API
description: Discover how to add arc controls with connection points using Aspose.Cells for .NET in this detailed guide.
weight: 27
url: /net/excel-shapes-controls/add-arc-control-with-connection-points/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Add Arc Control with Connection Points

## Introduction
When it comes to creating visually engaging Excel reports, illustrations play a vital role. Whether you're crafting a financial report or a project breakdown, using shapes like arcs can add depth and clarity to your data presentation. Today, we're diving deep into how to utilize Aspose.Cells for .NET to add arc controls with connection points in your Excel worksheets. So, if you've ever wondered how to spice up your spreadsheets or make your data sing, read on!
## Prerequisites
Before we jump into the excitement of coding, let’s make sure you’re all set up. Here’s what you need:
1. .NET Framework: Make sure you have a compatible version installed. Aspose.Cells works with multiple versions, including .NET Core.
2. Aspose.Cells for .NET: You’ll need to download and install the Aspose.Cells library. You can easily grab it from the [download link](https://releases.aspose.com/cells/net/).
3. A Good IDE: Visual Studio, that faithful companion of any .NET developer, will help streamline your coding experience.
4. Basic Knowledge of C#: If you know your way around C#, you’ll find this tutorial smooth sailing.
5. Access to Your Document Directory: Know where you'll save your Excel files. It's essential for organizing your output efficiently.
## Import Packages
The next step is to ensure you have the right packages imported into your project. Aspose.Cells for .NET has various functionalities, so we’ll keep it simple. Here’s what you’ll need to include:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
These namespaces will give you access to all the drawing features and cell management functionalities you’ll use throughout this guide.
## Step 1: Set Up Your Document Directory
First things first—let’s put in place a directory where you’ll save those shiny new Excel files. Here’s how we do it:
```csharp
string dataDir = "Your Document Directory";
// Create directory if it is not already present.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
This bit of code checks if your specified folder exists. If not, it creates one. Simple, right? It’s always good to have a specific place for your files to avoid clutter.
## Step 2: Instantiate a Workbook
Now that we have our directory ready, let’s create a new Excel workbook.
```csharp
Workbook excelbook = new Workbook();
```
By calling the `Workbook` constructor, you’re essentially saying, “Hey, let’s start a new Excel file!” This will be the canvas for all your shapes and data.
## Step 3: Adding the First Arc Shape
This is where the fun begins! Let's add our first arc shape.
```csharp
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
This line of code adds an arc shape to the first worksheet. The parameters specify the arc's coordinates and the angles that define its curvature. 
## Step 4: Customize the Arc’s Appearance
A blank arc shape is like a canvas without paint—it needs a bit of flair!
### Set Arc Fill Color
```csharp
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
```
This makes the arc solid blue. You can change the color to any hue you like by swapping out `Color.Blue` for another color.
### Set Arc Placement
```csharp
arc1.Placement = PlacementType.FreeFloating;
```
Setting the placement to "FreeFloating" allows the arc to move independently of cell boundaries, giving you flexibility in positioning.
### Adjust Line Weight and Style
```csharp
arc1.Line.Weight = 1;      
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Here, you define the line's weight and style, making it more prominent and visually appealing.
## Step 5: Adding Another Arc Shape
Why stop at one? Let’s add another arc shape to enrich our Excel visual.
```csharp
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
Like the first arc, this one is added at a different position—this is where the magic of design takes place!
## Step 6: Customize the Second Arc
Let’s give our second arc some personality too!
### Change Arc Line Color
```csharp
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
```
We’re keeping it consistent with a blue color, but you can always mix and match to see what fits best in your design!
### Set Properties Similar to the First Arc
Make sure to replicate those aesthetic choices:
```csharp
arc2.Placement = PlacementType.FreeFloating;
arc2.Line.Weight = 1;           
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
Here, you’re simply ensuring that the second arc matches the first, creating a cohesive look throughout your worksheet.
## Step 7: Save Your Workbook
No masterpiece is complete without being saved, right? Time to write your arcs into an Excel file.
```csharp
excelbook.Save(dataDir + "book1.out.xls");
```
This line saves your newly created arcs into an Excel file named "book1.out.xls" in your designated directory.
## Conclusion
Congratulations! You've just mastered the basics of adding arc controls with connection points in your Excel sheets using Aspose.Cells for .NET. This functionality not only beautifies your spreadsheets but can also make complex data easier to digest. Whether you're a seasoned developer or just starting, these visual elements can transform your reports from bland to grand.
## FAQ's
### What is Aspose.Cells?
Aspose.Cells is a powerful .NET library that allows developers to create and manipulate Excel files programmatically.
### Can I use Aspose.Cells for free?
Yes! You can try a free trial. Visit [this link](https://releases.aspose.com/) to start.
### How do I add other shapes besides arcs?
You can use different classes available in the Aspose.Cells.Drawing namespace to add various shapes like rectangles, circles, and more.
### What type of files can I create with Aspose.Cells?
You can create and manipulate various Excel formats including XLS, XLSX, CSV, and more.
### Is technical support available for Aspose.Cells?
Absolutely! You can access the [Aspose support forum](https://forum.aspose.com/c/cells/9) for assistance.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
