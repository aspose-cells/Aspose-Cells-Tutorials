---
title: Add Picture to Chart
linktitle: Add Picture to Chart
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to easily add pictures to Excel charts using Aspose.Cells for .NET. Enhance your charts and presentations in just a few simple steps.
weight: 11
url: /net/inserting-controls-in-charts/add-picture-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Add Picture to Chart

## Introduction

Are you tired of boring charts that lack a personal touch? Want to learn how to spice up your Excel visuals by adding pictures? Well, you're in luck! In this tutorial, we will dive into the world of Aspose.Cells for .NET and learn how to add pictures to charts in Excel. So, grab your favorite cup of coffee, and let’s get started!

## Prerequisites

Before we jump into the nitty-gritty of coding, there are a few prerequisites you need to have to follow along smoothly:

- Visual Studio: This is where you will write and run your .NET code. Make sure you have it installed.
- Aspose.Cells for .NET: You’ll need this library for working with Excel files. You can [download it here](https://releases.aspose.com/cells/net/).
- Basic Understanding of C#: While I’ll guide you through the code, having a handle on C# basics will make things clearer.

### Installation Steps

1. Install Aspose.Cells: You can add Aspose.Cells to your Visual Studio project via NuGet Package Manager. Do this by navigating to Tools > NuGet Package Manager > Manage NuGet Packages for Solution and searching for “Aspose.Cells.” Click Install.
2. Setting Up Your Project: Create a new C# console application project in Visual Studio.

## Import Packages

Once you’ve got everything set up, the next step is to import the necessary packages into your project. Here’s how to do it:

### Import the Required Namespaces

At the top of your C# code file, you’ll need to import the following namespaces:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
using System.IO;
```

This tells your program, “Hey! I’m going to use these cool features from Aspose.Cells.”

Now that we have our prerequisites in place, let’s break down the process into bite-sized steps. 

## Step 1: Define Your Directories

First things first, we need to set up the paths for our input and output files. This step is crucial because we need to know where to find our existing Excel file and where to save the modified file.

```csharp
//Source directory
string sourceDir = "Your Document Directory/";

//Output directory
string outputDir = "Your Output Directory/";
```

Replace `Your Document Directory` and `Your Output Directory` with actual paths on your computer. 

## Step 2: Load the Existing Workbook

Now, let’s load the existing Excel file where we want to add our picture to the chart.

```csharp
// Open the existing file.
Workbook workbook = new Workbook(sourceDir + "sampleAddingPictureInChart.xls");
```

This code opens up the workbook, making it ready for editing.

## Step 3: Prepare the Image Stream

Before adding the picture, we need to read the image we want to insert into the chart. 

```csharp
// Get an image file to the stream.
FileStream stream = new FileStream(sourceDir + "sampleAddingPictureInChart.png", FileMode.Open, FileAccess.Read);
```

Make sure you have the picture saved in the specified directory.

## Step 4: Target the Chart

Now, let’s specify which chart we're going to add our picture to. In this example, we’ll target the first chart on the first worksheet.

```csharp
// Get the designer chart in the second sheet.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

You can access any worksheet by changing the index accordingly.

## Step 5: Add the Picture to the Chart

With the chart selected, it’s time to add the picture! 

```csharp
// Add a new picture to the chart.
Aspose.Cells.Drawing.Picture pic0 = chart.Shapes.AddPictureInChart(50, 50, stream, 200, 200);
```

Here, `50` and `50` are the X and Y coordinates where the image will be placed, and `200` is the width and height of the image.

## Step 6: Customize the Picture's Line Format

Want to add some flair to your picture? You can customize its border! Here's how to do it:

```csharp
// Get the lineformat type of the picture.
Aspose.Cells.Drawing.LineFormat lineformat = pic0.Line; 

// Set the dash style.
lineformat.DashStyle = MsoLineDashStyle.Solid;

// Set the line weight.
lineformat.Weight = 4;    
```

This snippet allows you to choose how the border looks and how thick it is. Choose any style that resonates with your presentation!

## Step 7: Save the Modified Workbook

After all that hard work, let’s save your modifications by executing the following line of code:

```csharp
// Save the excel file.
workbook.Save(outputDir + "outputAddingPictureInChart.xls");
```

Now your picture is successfully integrated into the chart, and your output file is ready for viewing!

## Step 8: Indicate Success

Finally, you can add a simple message to confirm that your operation was successful:

```csharp
Console.WriteLine("AddingPictureInChart executed successfully.");
```

## Conclusion

In this tutorial, we’ve explored how to inject a little personality into your Excel charts by adding pictures using Aspose.Cells for .NET. With just a few simple steps, you can elevate your presentations from mundane to memorable. So, what are you waiting for? Give it a go and let your charts shine!

## FAQ's

### Can I add multiple pictures to a single chart?
Yes! You can call the `AddPictureInChart` method multiple times to add as many pictures as you desire.

### What image formats does Aspose.Cells support?
Aspose.Cells supports a variety of image formats, including PNG, JPEG, BMP, and GIF.

### Can I customize the position of the picture?
Certainly! The X and Y coordinates in the `AddPictureInChart` method allow precise positioning.

### Is Aspose.Cells free to use?
Aspose.Cells offers a free trial, but for full features, a license is required. You can find the pricing [here](https://purchase.aspose.com/buy).

### Where can I find more examples?
Check out the [Aspose.Cells documentation](https://reference.aspose.com/cells/net/) for more detailed examples and functionalities.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
