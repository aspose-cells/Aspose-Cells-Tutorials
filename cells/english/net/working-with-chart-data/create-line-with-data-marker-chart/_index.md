---
title: Create Line with Data Marker Chart
linktitle: Create Line with Data Marker Chart
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to create a Line with Data Markers chart in Excel using Aspose.Cells for .NET. Follow this step-by-step guide to easily generate and customize charts.
weight: 10
url: /net/working-with-chart-data/create-line-with-data-marker-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Line with Data Marker Chart

## Introduction

Have you ever wondered how to create stunning charts in Excel programmatically? Well, buckle up, because today we’re diving into creating a Line with Data Marker Chart using Aspose.Cells for .NET. This tutorial will guide you through each step, ensuring you have a firm grasp of chart generation, even if you’re just getting started with Aspose.Cells.

## Prerequisites

Before we begin, make sure you have everything in place to follow along seamlessly.

1. Aspose.Cells for .NET Library – You’ll need to install this. You can grab it [here](https://releases.aspose.com/cells/net/).
2. .NET Framework – Ensure your development environment is set up with the latest version of .NET.
3. IDE (Integrated Development Environment) – Visual Studio is recommended.
4. A valid Aspose.Cells license – If you don’t have one, you can request a [temporary license](https://purchase.aspose.com/temporary-license/) or check out their [free trial](https://releases.aspose.com/).

Ready to go? Let’s break it down!

## Importing Necessary Packages

To begin, make sure you import the following namespaces into your project. These will provide the necessary classes and methods to create your chart.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

Once you’ve got that down, we can start coding!

## Step 1: Set Up Your Workbook and Worksheet

First things first, you need to create a new workbook and access the first worksheet.

```csharp
//Output directory
static string outputDir = "Your Document Directory";
		
// Instantiate a workbook
Workbook workbook = new Workbook();

// Access first worksheet
Worksheet worksheet = workbook.Worksheets[0];
```

Think of the workbook as your Excel file and the worksheet as the specific sheet within it. In this case, we’re working with the first sheet.

## Step 2: Populate the Worksheet with Data

Now that we have our worksheet, let’s fill it with some data. We’re creating random data points for two series of values.

```csharp
// Set columns title
worksheet.Cells[0, 0].Value = "X";
worksheet.Cells[0, 1].Value = "Y";

// Random data for generating the chart
Random R = new Random();

// Create random data and save in the cells
for (int i = 1; i < 21; i++)
{
    worksheet.Cells[i, 0].Value = i;
    worksheet.Cells[i, 1].Value = 0.8;
}

for (int i = 21; i < 41; i++)
{
    worksheet.Cells[i, 0].Value = i - 20;
    worksheet.Cells[i, 1].Value = 0.9;
}
```

Here, we’re using random numbers to simulate data, but in real-life applications, you can populate it with actual values from your dataset.

## Step 3: Add the Chart to the Worksheet

Next up, we add the chart to the worksheet and choose the type – in this case, a Line with Data Markers Chart.

```csharp
// Add a chart to the worksheet
int idx = worksheet.Charts.Add(ChartType.LineWithDataMarkers, 1, 3, 20, 20);

// Access the newly created chart
Chart chart = worksheet.Charts[idx];
```

This snippet adds a line chart with data markers to the worksheet, placing it in a specific range (1,3 to 20,20). Pretty simple, right?

## Step 4: Customize the Chart’s Appearance

Once the chart is created, you can style it to your liking. Let’s change the background, title, and chart style.

```csharp
// Set chart style
chart.Style = 3;

// Set autoscaling value to true
chart.AutoScaling = true;

// Set foreground color to white
chart.PlotArea.Area.ForegroundColor = Color.White;

// Set chart title properties
chart.Title.Text = "Sample Chart";

// Set chart type
chart.Type = ChartType.LineWithDataMarkers;
```

Here, we’re giving the chart a clean look by setting a white background, autoscaling, and giving it a meaningful title.

## Step 5: Define Series and Plot Data Points

Now that our chart looks good, we need to define the data series that will be plotted.

```csharp
// Set Properties of category axis title
chart.CategoryAxis.Title.Text = "Units";

// Define two series for the chart
int s2_idx = chart.NSeries.Add("A2: A21", true);
int s3_idx = chart.NSeries.Add("A22: A41", true);
```

These series correspond to the ranges of data points that we populated earlier.

## Step 6: Add Colors and Customize Series Markers

Let’s make this chart even more appealing by adding custom colors to our data markers.

```csharp
// Customize first series
chart.NSeries[s2_idx].Marker.Area.ForegroundColor = Color.Yellow;
chart.NSeries[s2_idx].Marker.Border.IsVisible = false;

// Customize second series
chart.NSeries[s3_idx].Marker.Area.ForegroundColor = Color.Green;
chart.NSeries[s3_idx].Marker.Border.IsVisible = false;
```

By customizing the colors, you make the chart not only functional but visually engaging as well!

## Step 7: Set X and Y Values for Each Series

Finally, let’s assign the X and Y values for each of our series.

```csharp
// Set X and Y values of first series
chart.NSeries[s2_idx].XValues = "A2: A21";
chart.NSeries[s2_idx].Values = "B2: B21";

// Set X and Y values of second series
chart.NSeries[s3_idx].XValues = "A22: A41";
chart.NSeries[s3_idx].Values = "B22: B41";
```

The values are based on the data we populated in step 2.

## Step 8: Save the Workbook

Now that everything’s set, let’s save the workbook, so we can see the chart in action.

```csharp
// Save the workbook
workbook.Save(outputDir + @"LineWithDataMarkerChart.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```

And that’s it! You’ve just created a line chart with data markers using Aspose.Cells for .NET.

## Conclusion

Creating charts programmatically in Excel may seem daunting, but with Aspose.Cells for .NET, it’s as easy as following a step-by-step recipe. From setting up your workbook to customizing chart appearance, this powerful library handles it all. Whether you’re building reports, dashboards, or data visualizations, Aspose.Cells allows you to do it in a breeze.

## FAQ's

### Can I customize the chart further?  
Absolutely! Aspose.Cells offers a ton of customization options, from fonts to gridlines and more.

### Do I need a license to use Aspose.Cells?  
Yes, a license is required for full functionality. You can get a [temporary license](https://purchase.aspose.com/temporary-license/) or start with a [free trial](https://releases.aspose.com/).

### How can I add more data series?  
Just add additional series using the `NSeries.Add` method, specifying the cell ranges for the new data.

### Can I export the chart as an image?  
Yes, you can export charts directly as images using the `Chart.ToImage` method.

### Does Aspose.Cells support 3D charts?  
Yes, Aspose.Cells supports a wide range of chart types, including 3D charts.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
