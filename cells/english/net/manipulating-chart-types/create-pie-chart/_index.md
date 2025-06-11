---
title: Create Pie Chart
linktitle: Create Pie Chart
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to create a pie chart in Excel using Aspose.Cells for .NET with this step-by-step guide. Visualize your data effortlessly.
weight: 12
url: /net/manipulating-chart-types/create-pie-chart/
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Create Pie Chart

## Introduction

Creating charts is essential for visually representing data, and pie charts are one of the most popular ways to illustrate how parts make up a whole. With Aspose.Cells for .NET, you can easily automate the generation of pie charts in Excel files. In this tutorial, we'll dive into how to create a pie chart from scratch using Aspose.Cells for .NET, with a step-by-step guide to make the process smooth and straightforward. Whether you're new to the tool or looking to enhance your Excel automation skills, this guide has you covered!

## Prerequisites

Before diving into the code, make sure you have the following set up:

1. Aspose.Cells for .NET Library: Ensure that you have Aspose.Cells installed in your project. If you haven't installed it yet, you can download it from [here](https://releases.aspose.com/cells/net/).
2. .NET Development Environment: Make sure your project is set up to use .NET Framework or .NET Core.
3. Basic Knowledge of C#: You should be comfortable with C# programming, particularly object-oriented programming (OOP).

For advanced users, a temporary license can be applied to unlock all the features of Aspose.Cells. You can request one from [here](https://purchase.aspose.com/temporary-license/).

## Import Packages

To start, import the necessary namespaces and packages required for this tutorial. These include basic I/O operations and the Aspose.Cells package.

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## Step 1: Create a New Workbook

First, we need to create an instance of the `Workbook` class, which represents the Excel file. A workbook contains multiple sheets, and for our example, we will be working with two sheets—one for data and one for the pie chart.

```csharp
Workbook workbook = new Workbook();
```

This initializes a new Excel workbook. But where does the data go? Let’s take care of that in the next step.

## Step 2: Add Data to the Worksheet

Once the workbook is created, we need to access the first worksheet and give it a name. This is where we’ll input the data required for the pie chart.

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

Now, we can input some dummy sales data representing different regions:

```csharp
cells["A1"].PutValue("Region");
cells["A2"].PutValue("France");
cells["A3"].PutValue("Germany");
cells["A4"].PutValue("England");
cells["A5"].PutValue("Sweden");
cells["A6"].PutValue("Italy");
cells["A7"].PutValue("Spain");
cells["A8"].PutValue("Portugal");

cells["B1"].PutValue("Sales");
cells["B2"].PutValue(70000);
cells["B3"].PutValue(55000);
cells["B4"].PutValue(30000);
cells["B5"].PutValue(40000);
cells["B6"].PutValue(35000);
cells["B7"].PutValue(32000);
cells["B8"].PutValue(10000);
```

Here, we’re adding two columns: one for regions and another for sales figures. This data will be represented in the pie chart.

## Step 3: Add a Chart Sheet

Next, let's add a separate worksheet to hold the pie chart.

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

This new sheet will host the pie chart. Giving it a name such as "Chart" ensures that users know what to expect when they open the file.

## Step 4: Create the Pie Chart

Now it's time to create the actual chart. We’ll specify that we want a pie chart, and we'll define its position on the sheet.

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

The method `Add()` accepts parameters for the chart type (in this case, `ChartType.Pie`), and its location on the worksheet. The numbers represent row and column positions.

## Step 5: Customize the Chart Appearance

A pie chart wouldn’t be complete without some customization! Let’s make our chart visually appealing by tweaking the colors, labels, and title.

### Set Chart Title
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### Customize Plot Area
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

We set the gradient fill for the plot area and hide the border for a cleaner look.

## Step 6: Define Chart Data

It's time to link the chart to our data. The `NSeries` property of the chart binds the sales figures and regions to the pie chart.

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

The first line specifies that we’re using the sales data from cells `B2:B8`. We also tell the chart to use the region names from `A2:A8` as category labels.

## Step 7: Add Data Labels

Adding labels directly to the chart segments can make it easier to understand. Let’s include the region names and sales values within the pie chart slices.

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## Step 8: Customize Chart Area and Legend

Lastly, let’s give the chart area and legend some final touches. This enhances the overall presentation of the chart.

### Chart Area
```csharp
ChartArea chartArea = chart.ChartArea;
chartArea.Area.Formatting = FormattingType.Custom;
chartArea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
```

### Legend
```csharp
Legend legend = chart.Legend;
legend.Position = LegendPositionType.Left;
legend.Font.IsBold = true;
legend.Border.Color = Color.Blue;
legend.Area.FillFormat.Texture = TextureType.Bouquet;
```

## Step 9: Save the Workbook

Finally, we save the workbook to an Excel file. You can specify the output directory and filename as needed.

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## Conclusion

Creating a pie chart with Aspose.Cells for .NET is a straightforward and customizable process. By following this guide, you can generate a professional-looking chart that conveys valuable insights in just a few steps. Whether for business reporting or educational purposes, mastering chart creation will elevate your Excel automation skills. Remember, Aspose.Cells provides the flexibility you need to create stunning, data-driven Excel files effortlessly.

## FAQ's

### Can I create other types of charts using Aspose.Cells for .NET?
Yes! Aspose.Cells supports various chart types, including bar charts, line charts, and scatter plots.

### Do I need a paid license to use Aspose.Cells for .NET?
You can use the free version with some limitations. For full features, you’ll need a license, which you can buy [here](https://purchase.aspose.com/buy).

### Can I export the chart to formats like PDF or images?
Absolutely! Aspose.Cells allows you to export charts to various formats, including PDF and PNG.

### Is it possible to style each pie slice with different colors?
Yes, you can apply different colors to each slice by setting the `IsColorVaried` property to `true`, as shown in the tutorial.

### Can I automate the generation of multiple charts in a single workbook?
Yes, you can create and customize as many charts as needed within a single Excel file.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
