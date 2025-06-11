---
"description": "了解如何使用 Aspose.Cells for .NET 在 Excel 中创建带数据标记的折线图。按照本分步指南，轻松生成和自定义图表。"
"linktitle": "创建带数据标记的线条图"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "创建带数据标记的线条图"
"url": "/zh/net/working-with-chart-data/create-line-with-data-marker-chart/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 创建带数据标记的线条图

## 介绍

您是否想过如何以编程方式在 Excel 中创建精美的图表？那就系好安全带吧，因为今天我们将深入讲解如何使用 Aspose.Cells for .NET 创建带数据标记的折线图。本教程将指导您完成每个步骤，确保您即使刚刚开始使用 Aspose.Cells，也能熟练掌握图表生成技术。

## 先决条件

在我们开始之前，请确保一切准备就绪，以便顺利进行。

1. Aspose.Cells for .NET Library – 您需要安装它。您可以下载它 [这里](https://releases。aspose.com/cells/net/).
2. .NET Framework – 确保您的开发环境设置了最新版本的 .NET。
3. IDE（集成开发环境）——建议使用 Visual Studio。
4. 有效的 Aspose.Cells 许可证 – 如果您没有，您可以申请 [临时执照](https://purchase.aspose.com/temporary-license/) 或者查看他们的 [免费试用](https://releases。aspose.com/).

准备好了吗？我们来分解一下！

## 导入必要的包

首先，请确保将以下命名空间导入到项目中。这些命名空间将提供创建图表所需的类和方法。

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

一旦你搞定了这些，我们就可以开始编码了！

## 步骤 1：设置工作簿和工作表

首先，您需要创建一个新的工作簿并访问第一个工作表。

```csharp
//输出目录
static string outputDir = "Your Document Directory";
		
// 实例化工作簿
Workbook workbook = new Workbook();

// 访问第一个工作表
Worksheet worksheet = workbook.Worksheets[0];
```

可以将工作簿视为 Excel 文件，将工作表视为其中的特定工作表。在本例中，我们使用的是第一个工作表。

## 步骤 2：用数据填充工作表

现在我们有了工作表，让我们来填充一些数据。我们将为两个系列的值创建随机数据点。

```csharp
// 设置列标题
worksheet.Cells[0, 0].Value = "X";
worksheet.Cells[0, 1].Value = "Y";

// 用于生成图表的随机数据
Random R = new Random();

// 创建随机数据并保存在单元格中
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

在这里，我们使用随机数来模拟数据，但在实际应用中，您可以使用数据集中的实际值填充它。

## 步骤 3：将图表添加到工作表

接下来，我们将图表添加到工作表并选择类型 - 在本例中为带有数据标记的折线图。

```csharp
// 向工作表添加图表
int idx = worksheet.Charts.Add(ChartType.LineWithDataMarkers, 1, 3, 20, 20);

// 访问新创建的图表
Chart chart = worksheet.Charts[idx];
```

这段代码将一个带有数据标记的折线图添加到工作表中，并将其放置在特定范围内（1.3 到 20.20）。很简单，对吧？

## 步骤 4：自定义图表的外观

图表创建完成后，您可以根据自己的喜好设置其样式。让我们更改背景、标题和图表样式。

```csharp
// 设置图表样式
chart.Style = 3;

// 将自动缩放值设置为 true
chart.AutoScaling = true;

// 将前景色设置为白色
chart.PlotArea.Area.ForegroundColor = Color.White;

// 设置图表标题属性
chart.Title.Text = "Sample Chart";

// 设置图表类型
chart.Type = ChartType.LineWithDataMarkers;
```

在这里，我们通过设置白色背景、自动缩放并赋予其有意义的标题来使图表看起来整洁。

## 步骤 5：定义序列并绘制数据点

现在我们的图表看起来不错，我们需要定义将要绘制的数据系列。

```csharp
// 设置分类轴标题的属性
chart.CategoryAxis.Title.Text = "Units";

// 为图表定义两个系列
int s2_idx = chart.NSeries.Add("A2: A21", true);
int s3_idx = chart.NSeries.Add("A22: A41", true);
```

这些系列对应于我们之前填充的数据点范围。

## 步骤 6：添加颜色并自定义系列标记

让我们通过向数据标记添加自定义颜色来使该图表更具吸引力。

```csharp
// 定制第一个系列
chart.NSeries[s2_idx].Marker.Area.ForegroundColor = Color.Yellow;
chart.NSeries[s2_idx].Marker.Border.IsVisible = false;

// 定制第二系列
chart.NSeries[s3_idx].Marker.Area.ForegroundColor = Color.Green;
chart.NSeries[s3_idx].Marker.Border.IsVisible = false;
```

通过自定义颜色，您可以使图表不仅具有功能性，而且具有视觉吸引力！

## 步骤 7：设置每个系列的 X 和 Y 值

最后，让我们为每个系列分配 X 和 Y 值。

```csharp
// 设置第一个系列的 X 和 Y 值
chart.NSeries[s2_idx].XValues = "A2: A21";
chart.NSeries[s2_idx].Values = "B2: B21";

// 设置第二个系列的 X 和 Y 值
chart.NSeries[s3_idx].XValues = "A22: A41";
chart.NSeries[s3_idx].Values = "B22: B41";
```

这些值基于我们在步骤 2 中填充的数据。

## 步骤 8：保存工作簿

现在一切都已设置好，让我们保存工作簿，以便我们可以看到图表的运行情况。

```csharp
// 保存工作簿
workbook.Save(outputDir + @"LineWithDataMarkerChart.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```

就这样！您刚刚使用 Aspose.Cells for .NET 创建了带有数据标记的折线图。

## 结论

在 Excel 中以编程方式创建图表可能看似困难，但使用 Aspose.Cells for .NET，一切就变得轻而易举，只需按照步骤操作即可。从设置工作簿到自定义图表外观，这个强大的库都能轻松搞定。无论您是构建报表、仪表板还是数据可视化，Aspose.Cells 都能让您轻松搞定。

## 常见问题解答

### 我可以进一步自定义图表吗？  
当然！Aspose.Cells 提供了大量的自定义选项，从字体到网格线等等。

### 我需要许可证才能使用 Aspose.Cells 吗？  
是的，需要许可证才能使用全部功能。您可以获取 [临时执照](https://purchase.aspose.com/temporary-license/) 或者从 [免费试用](https://releases。aspose.com/).

### 我如何添加更多数据系列？  
只需使用 `NSeries.Add` 方法，指定新数据的单元格范围。

### 我可以将图表导出为图像吗？  
是的，您可以使用 `Chart.ToImage` 方法。

### Aspose.Cells 支持 3D 图表吗？  
是的，Aspose.Cells 支持多种图表类型，包括 3D 图表。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}