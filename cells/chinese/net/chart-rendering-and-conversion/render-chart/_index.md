---
title: 渲染图表
linktitle: 渲染图表
second_title: Aspose.Cells .NET Excel 处理 API
description: 了解如何使用 Aspose.Cells 在 .NET 中呈现图表。按照我们的分步教程轻松创建令人惊叹的视觉效果。
weight: 10
url: /zh/net/chart-rendering-and-conversion/render-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 渲染图表

## 介绍

图表是数据呈现和分析中必不可少的元素，可使复杂的信息变得易于理解。如果您使用 .NET 并需要以编程方式生成图表，Aspose.Cells 是一个功能强大的库，它提供直观和高级的功能来处理 Excel 文件和图表。在本指南中，我们将介绍使用 Aspose.Cells for .NET 呈现图表的过程。准备好深入研究这个详细的教程，它旨在引人入胜且易于理解！

## 先决条件

在我们开始编写代码之前，让我们确保你已经准备好了一切。以下是你需要的东西：

1. .NET 环境：确保您已设置 .NET 开发环境。您可以使用 Visual Studio 或任何其他支持 .NET 的 IDE。
2.  Aspose.Cells for .NET：您需要安装 Aspose.Cells 库。您可以从以下网址下载[Aspose 的发布页面](https://releases.aspose.com/cells/net/).
3. 基本 C# 知识：熟悉 C# 编程将帮助您更好地理解示例，但如果您是新手，请不要担心 - 本指南将逐步解释一切！

## 导入包

编码之旅的第一步是导入必要的软件包。在 IDE 中打开项目并添加以下命名空间：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
```

这些命名空间将为您提供对 Aspose.Cells 库所提供的功能的访问，从而使您可以无缝地创建和操作图表。


现在我们已经介绍了先决条件和导入，让我们深入了解渲染图表的细节！我们将把它分解为清晰、易于管理的步骤。

## 步骤 1：设置输出目录

在创建工作簿和图表之前，我们需要确定输出的保存位置。这样，当我们的图表生成时，您就会知道在哪里可以找到它。

```csharp
string outputDir = "Your Output Directory"; //在此处指定输出目录。
```

确保将“您的输出目录”替换为您想要保存图表图像的路径。

## 步骤 2：创建工作簿

接下来，我们将创建一个新的工作簿。这就是所有神奇的事情发生的地方！

```csharp
Workbook workbook = new Workbook();
```

此行创建了`Workbook`类，它允许我们使用工作表和图表。

## 步骤 3：添加新工作表

现在我们有了工作簿，是时候添加新的工作表了。将工作表视为笔记本中的不同页面，您可以在其中整理数据。

```csharp
int sheetIndex = workbook.Worksheets.Add();
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```

在这里，我们添加一个新的工作表并获取对它的引用。您将使用此工作表输入数据和图表。

## 步骤 4：输入样本值

创建工作表后，让我们向单元格添加一些示例数据。这些数据是您的图表的基础，因此请选择适合您的图表类型的值！

```csharp
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```

在此代码片段中，我们用一些数值填充单元格“A1”至“A3”，用另一组值填充单元格“B1”至“B3”。您可以随意自定义这些数字以满足您的需求！

## 步骤 5：创建图表

现在，是时候创建图表了。我们将添加柱状图类型，它非常适合比较值。

```csharp
int chartIndex = worksheet.Charts.Add(ChartType.Column, 5, 0, 15, 5);
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

在这里，我们通过定义其布局在指定位置添加图表：第一组数字代表图表在网格上的位置。

## 步骤6：向图表添加数据系列

创建图表后，我们现在需要将其绑定到前面步骤中输入的数据。

```csharp
chart.NSeries.Add("A1:B3", true);
```

此线将图表的数据系列与单元格“A1”至“B3”中的值连接起来。这意味着您的图表将按预期直观地呈现数据。

## 步骤 7：将图表保存为图像

现在让我们将图表转换为图像格式，以便轻松共享和查看。

```csharp
chart.ToImage(outputDir + "outputChartRendering.emf", System.Drawing.Imaging.ImageFormat.Emf);
```

在此步骤中，我们将图表作为 EMF（增强型图元文件）图像保存在指定的输出目录中。您还可以将其保存为不同的格式，例如 BMP 或 PNG。

## 步骤 8：将图表转换为位图

如果您更喜欢使用位图，请按照以下方法将图表转换为位图格式。

```csharp
System.Drawing.Bitmap bitmap = chart.ToImage();
bitmap.Save(outputDir + "outputChartRendering.bmp", System.Drawing.Imaging.ImageFormat.Bmp);
```

这会将您的图表保存为 BMP 图像。请记住，BMP 文件通常较大，但质量极高！

## 步骤 9：使用高级选项渲染

我们还可以使用一些高级图像选项来渲染图表，以获得更好的质量和分辨率。让我们设置一些选项：

```csharp
ImageOrPrintOptions options = new ImageOrPrintOptions()
{
    VerticalResolution = 300,
    HorizontalResolution = 300,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.AntiAlias
};
```

这些选项有助于提高您生成的图像的视觉质量，对于演示或出版物特别有用。

## 步骤 10：使用高级选项将图表转换为图像

现在让我们使用刚刚设置的高级选项实际转换图表。

```csharp
chart.ToImage(outputDir + "outputChartRendering.png", options);
```

这会将您的图表保存为具有增强质量设置的 PNG 文件。

## 步骤 11：将图表导出为 PDF

最后，如果您想要一份精美且易于共享的文档，您可以将图表直接导出为 PDF 格式。

```csharp
chart.ToPdf(outputDir + "outputChartRendering.pdf");
```

此步骤将创建包含图表的 PDF，使其非常适合用于数字报告或与同事共享。

## 结论 

恭喜！您已成功使用 Aspose.Cells for .NET 渲染图表。这个功能强大的库简化了 Excel 文件和图表的创建和操作，使您的数据更易于访问且更具视觉吸引力。无论您是在准备报告、分析还是演示文稿，图表都会产生重大影响，使用 Aspose，您可以轻松地以编程方式创建它们。

## 常见问题解答

### 我可以使用 Aspose.Cells for .NET 创建哪些类型的图表？
您可以创建各种图表，包括柱形图、折线图、饼图和条形图等。

### 我可以自定义图表的外观吗？
是的，Aspose.Cells 允许进行广泛的定制，包括颜色、样式和图表元素。

### 有免费试用吗？
当然！你可以从[这里](https://releases.aspose.com/).

### 我可以在哪里获得 Aspose.Cells 的支持？
您可以在以下位置找到社区支持和资源[Aspose 支持论坛](https://forum.aspose.com/c/cells/9).

### 我需要许可证才能使用 Aspose.Cells 吗？
是的，试用期结束后继续使用需要许可证，但你可以申请临时许可证[这里](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
