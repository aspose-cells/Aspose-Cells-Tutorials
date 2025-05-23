---
"description": "了解如何使用 Aspose.Cells for .NET 在 Excel 中创建令人惊叹的 3D 图表。请遵循我们简单的分步指南。"
"linktitle": "将 3D 格式应用于图表"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "将 3D 格式应用于图表"
"url": "/zh/net/advanced-chart-operations/apply-3d-format-to-chart/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 将 3D 格式应用于图表

## 介绍

在数据可视化至关重要的时代，我们呈现数据的方式已超越了基本的图形和图表。借助 Aspose.Cells for .NET 等工具，您可以使用精美的 3D 图表提升数据演示效果，这些图表不仅能吸引眼球，还能有效地传达信息。本指南将指导您如何使用 Aspose.Cells 将 3D 格式应用于图表，将原始数据转换为引人入胜的显示效果。

## 先决条件

在我们深入研究将 3D 格式应用于图表的细节之前，让我们确保您已准备好所需的一切。

### 软件要求

- Visual Studio：确保您已安装 Visual Studio 以便使用 .NET 应用程序。
- Aspose.Cells for .NET：如果您还没有，请从以下网址下载并安装 Aspose.Cells [这里](https://releases。aspose.com/cells/net/).

### 编码环境设置

1. 创建一个新的 .NET 项目：打开 Visual Studio，选择“创建一个新项目”，然后选择一个控制台应用程序。
2. 添加 Aspose.Cells 参考：通过 NuGet 包管理器，通过搜索或通过包管理器控制台添加 Aspose.Cells：

```bash
Install-Package Aspose.Cells
```

3. 设置输出目录：指定保存生成的文件的输出目录 - 这可以像在桌面上创建文件夹一样简单。

现在您已完成所有设置，是时候进入代码并创建一些令人眼花缭乱的 3D 图表了！

## 导入包

首先，您需要导入必要的命名空间。这将帮助您访问 Aspose.Cells 提供的类和方法。操作方法如下：

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

本节将把流程分解为易于管理的步骤，让您清楚地了解每个阶段。

## 步骤 1：初始化工作簿

首先，您需要创建一个 `Workbook` 类。此对象将作为您的 Excel 文档的基础。

```csharp
//输出目录
string outputDir = "Your Document Directory";
Workbook book = new Workbook();
```
想想这个 `Workbook` 就像一块空白的画布——您可以用丰富多彩的数据和有影响力的可视化效果来填充它。

## 步骤 2：重命名第一个工作表

接下来，让我们重命名第一个工作表。这可以更清楚地显示我们正在处理的数据。

```csharp
book.Worksheets[0].Name = "DataSheet";
```

名称应该直观易懂。在本例中，我们将其命名为“DataSheet”，以便我们了解数据所在的位置。

## 步骤 3：为图表创建数据

现在，我们将向“数据表”添加一些数据。让我们用图表将使用的值来填充它。

```csharp
Worksheet dataSheet = book.Worksheets["DataSheet"];
dataSheet.Cells["B1"].PutValue(1);
dataSheet.Cells["B2"].PutValue(2);
dataSheet.Cells["B3"].PutValue(3);
dataSheet.Cells["A1"].PutValue("A");
dataSheet.Cells["A2"].PutValue("B");
dataSheet.Cells["A3"].PutValue("C");
```

就像食谱取决于配料一样，图表的有效性取决于输入数据的质量和组织。

## 步骤 4：设置新的图表工作表

是时候为图表本身创建一个新的工作表了。这有助于保持数据可视化的条理性。

```csharp
Worksheet sheet = book.Worksheets.Add("MyChart");
```

将此工作表视为您的舞台——您的数据性能在此展现。

## 步骤 5：添加图表

在这里，我们将向新创建的工作表添加一个柱形图。  

```csharp
ChartCollection charts = sheet.Charts;
int chartSheetIdx = charts.Add(ChartType.Column, 5, 0, 25, 15);
```

我们正在为图表定义一个空间，并指定它的类型。就把它想象成为你的艺术作品选择框架的类型。

## 步骤 6：自定义图表外观

现在，让我们通过设置背景颜色来自定义图表的外观。 

```csharp
Aspose.Cells.Charts.Chart chart = book.Worksheets["MyChart"].Charts[0];
chart.PlotArea.Area.BackgroundColor = Color.White;
chart.ChartArea.Area.BackgroundColor = Color.White;
chart.PlotArea.Area.ForegroundColor = Color.White;
chart.ChartArea.Area.ForegroundColor = Color.White;
chart.ShowLegend = false;
```

干净的白色背景通常会使数据的颜色脱颖而出，从而增强可见性。

## 步骤 7：向图表添加数据系列

现在该为图表提供数据了。我们将从“数据表”中添加一个数据系列，以确保图表能够反映所需的数据。

```csharp
chart.NSeries.Add("DataSheet!B1:B3", true);
chart.NSeries.CategoryData = "DataSheet!A1:A3";
```

这就像厨师用特定的食材烹制菜肴一样。每个数据点都很重要！

## 步骤 8：访问并设置数据系列的格式

现在我们已经链接了数据，让我们抓住数据系列并开始应用一些 3D 效果。

```csharp
Aspose.Cells.Charts.Series ser = chart.NSeries[0];
ShapePropertyCollection spPr = ser.ShapeProperties;
Format3D fmt3d = spPr.Format3D;
```

我们正准备为我们的菜肴添加一些风味——可以将其视为增强整体风味的调味品。

## 步骤9：应用3D斜角效果

接下来，我们将添加斜面效果来为图表提供一些维度。

```csharp
Bevel bevel = fmt3d.TopBevel;
bevel.Type = BevelPresetType.Circle;
bevel.Height = 2;
bevel.Width = 5;
```

就像雕塑家塑造石头一样，我们正在创造深度，让我们的图表变得生动！

## 步骤10：自定义表面材质和照明

让我们的图表更加闪耀夺目！我们将调整表面材质和光照设置。

```csharp
fmt3d.SurfaceMaterialType = PresetMaterialType.WarmMatte;
fmt3d.SurfaceLightingType = LightRigType.ThreePoint;
fmt3d.LightingAngle = 20;
```

合适的灯光和材质，能将平面物体转化为引人入胜的视觉效果。想象一下，在电影布景中，专业的灯光能提升每个场景的视觉效果。

## 步骤11：系列外观的最后润色

现在通过调整颜色来完成数据系列的外观。

```csharp
ser.Area.BackgroundColor = Color.Maroon;
ser.Area.ForegroundColor = Color.Maroon;
ser.Border.Color = Color.Maroon;
```

合适的颜色可以唤起特定的感觉和反应——栗色增添了一丝优雅和精致。

## 步骤 12：保存工作簿

最后，是时候保存你的杰作了！别忘了指定保存位置。

```csharp
book.Save(outputDir + "outputApplying3DFormat.xlsx");
Console.WriteLine("Applying3DFormat executed successfully.");
```

保存您的作品就像将您的艺术品放在画廊中一样；这是一个值得珍惜和分享的时刻。

## 结论

恭喜！您已成功使用 Aspose.Cells for .NET 创建了美观的 3D 图表。按照以下步骤操作，您将拥有一个强大的工具来增强数据演示效果，使其不仅信息丰富，更具有视觉吸引力。在优化图表时，请记住，每个可视化都是一个故事——务必使其引人入胜、清晰明了、富有影响力！

## 常见问题解答

### 什么是 Aspose.Cells for .NET？
Aspose.Cells for .NET 是一个功能强大的库，允许开发人员以编程方式操作 Excel 文档，包括创建图表和示意图。

### 我可以在 Aspose.Cells 中自定义图表类型吗？
是的！Aspose.Cells 支持各种图表类型，例如柱形图、折线图、饼图等等，并且可以轻松自定义。

### Aspose.Cells 有免费试用版吗？
当然！你可以从 [这里](https://releases。aspose.com/).

### 除了 3D 格式之外，我还可以对图表应用其他效果吗？
是的，您可以应用各种效果，例如阴影、渐变和不同样式，以增强您的图表超越 3D 的效果。

### 在哪里可以找到对 Aspose.Cells 的支持？
如需支持，您可以访问 [Aspose 论坛](https://forum.aspose.com/c/cells/9) 寻求社区援助和帮助。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}