---
"description": "通过本分步指南，学习如何使用 Aspose.Cells for .NET 在 Excel 中创建饼图。轻松实现数据可视化。"
"linktitle": "创建饼图"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "创建饼图"
"url": "/zh/net/manipulating-chart-types/create-pie-chart/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 创建饼图

## 介绍

创建图表对于直观地呈现数据至关重要，而饼图是展示各个部分如何构成整体的最常用方法之一。使用 Aspose.Cells for .NET，您可以轻松地在 Excel 文件中自动生成饼图。在本教程中，我们将深入讲解如何使用 Aspose.Cells for .NET 从零开始创建饼图，并提供分步指南，使整个过程更加流畅、直观。无论您是新手还是希望提升 Excel 自动化技能，本指南都能满足您的需求！

## 先决条件

在深入研究代码之前，请确保已进行以下设置：

1. Aspose.Cells for .NET Library：确保您的项目中已安装 Aspose.Cells。如果您尚未安装，可以从以下位置下载： [这里](https://releases。aspose.com/cells/net/).
2. .NET 开发环境：确保您的项目设置为使用 .NET Framework 或 .NET Core。
3. C# 基础知识：您应该熟悉 C# 编程，尤其是面向对象编程 (OOP)。

对于高级用户，可以申请临时许可证来解锁 Aspose.Cells 的所有功能。您可以通过以下方式申请： [这里](https://purchase。aspose.com/temporary-license/).

## 导入包

首先，导入本教程所需的命名空间和包。其中包括基本 I/O 操作和 Aspose.Cells 包。

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## 步骤 1：创建新工作簿

首先，我们需要创建一个 `Workbook` 类，代表 Excel 文件。一个工作簿包含多个工作表，在本例中，我们将使用两个工作表：一个用于数据，一个用于饼图。

```csharp
Workbook workbook = new Workbook();
```

这将初始化一个新的 Excel 工作簿。但是数据会存储到哪里呢？让我们在下一步中解决这个问题。

## 步骤 2：向工作表添加数据

创建工作簿后，我们需要访问第一个工作表并为其命名。我们将在这里输入饼图所需的数据。

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

现在，我们可以输入一些代表不同地区的虚拟销售数据：

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

这里我们添加两列：一列用于显示地区数据，另一列用于显示销售额数据。这些数据将以饼图的形式呈现。

## 步骤 3：添加图表表

接下来，让我们添加一个单独的工作表来保存饼图。

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

此新工作表将用于存放饼图。将其命名为“Chart”（图表），可确保用户在打开文件时了解其内容。

## 步骤 4：创建饼图

现在是时候创建实际的图表了。我们将指定饼图，并定义它在工作表上的位置。

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

方法 `Add()` 接受图表类型的参数（在本例中， `ChartType.Pie`) 及其在工作表上的位置。数字代表行和列的位置。

## 步骤 5：自定义图表外观

如果没有一些自定义，饼图就不完整！让我们通过调整颜色、标签和标题，让图表更具视觉吸引力。

### 设置图表标题
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### 自定义绘图区域
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

我们为绘图区域设置渐变填充，并隐藏边框以获得更整洁的外观。

## 步骤 6：定义图表数据

现在是时候将图表链接到我们的数据了。 `NSeries` 图表的属性将销售数字和地区绑定到饼图。

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

第一行指定我们使用单元格中的销售数据 `B2:B8`。我们还告诉图表使用来自 `A2:A8` 作为类别标签。

## 步骤 7：添加数据标签

直接在图表片段上添加标签可以使其更易于理解。让我们在饼图切片中包含区域名称和销售额。

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## 步骤 8：自定义图表区域和图例

最后，让我们对图表区域和图例进行一些最后的修饰。这将增强图表的整体呈现效果。

### 图表区
```csharp
ChartArea chartArea = chart.ChartArea;
chartArea.Area.Formatting = FormattingType.Custom;
chartArea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
```

### 传奇
```csharp
Legend legend = chart.Legend;
legend.Position = LegendPositionType.Left;
legend.Font.IsBold = true;
legend.Border.Color = Color.Blue;
legend.Area.FillFormat.Texture = TextureType.Bouquet;
```

## 步骤 9：保存工作簿

最后，我们将工作簿保存为 Excel 文件。您可以根据需要指定输出目录和文件名。

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## 结论

使用 Aspose.Cells for .NET 创建饼图的过程简单易懂，且可自定义。按照本指南，您只需几个步骤即可生成具有专业外观的图表，传达有价值的见解。无论是用于商业报告还是教育用途，掌握图表创建技能都能提升您的 Excel 自动化技能。请记住，Aspose.Cells 为您提供所需的灵活性，让您轻松创建令人惊叹的数据驱动型 Excel 文件。

## 常见问题解答

### 我可以使用 Aspose.Cells for .NET 创建其他类型的图表吗？
是的！Aspose.Cells 支持各种图表类型，包括条形图、折线图和散点图。

### 我需要付费许可证才能使用 Aspose.Cells for .NET 吗？
您可以使用免费版本，但有一些限制。要使用完整功能，您需要购买许可证。 [这里](https://purchase。aspose.com/buy).

### 我可以将图表导出为 PDF 或图像等格式吗？
当然！Aspose.Cells 允许您将图表导出为各种格式，包括 PDF 和 PNG。

### 是否可以为每个饼图切片设置不同的颜色？
是的，您可以通过设置为每个切片应用不同的颜色 `IsColorVaried` 财产 `true`，如教程所示。

### 我可以在单个工作簿中自动生成多个图表吗？
是的，您可以在单个 Excel 文件中创建和自定义所需数量的图表。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}