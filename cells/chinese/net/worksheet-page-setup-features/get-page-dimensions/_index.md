---
title: 获取工作表的页面尺寸
linktitle: 获取工作表的页面尺寸
second_title: Aspose.Cells .NET Excel 处理 API
description: 了解如何使用 Aspose.Cells for .NET 获取 Excel 工作表中的页面尺寸。自定义 A2、A3、A4 和 Letter 纸张尺寸的分步指南。
weight: 13
url: /zh/net/worksheet-page-setup-features/get-page-dimensions/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 获取工作表的页面尺寸

## 介绍
如果您使用 Aspose.Cells for .NET 以编程方式处理 Excel 文件，有时可能需要访问和设置工作表的页面尺寸。了解尺寸有助于布局、打印和自定义 Excel 工作表以用于特定目的。在本文中，我们将探讨如何使用 Aspose.Cells for .NET 在 Excel 中检索和显示各种页面尺寸。我们将逐步介绍教程，以确保您掌握所有细节，从而自信地开始使用。
## 先决条件
在深入研究之前，请确保您已准备好完成本教程所需的一切。
1.  Aspose.Cells for .NET：确保您已安装 Aspose.Cells for .NET。您可以[点击此处下载库](https://releases.aspose.com/cells/net/)或者通过 NuGet 在您的 .NET 项目中安装它。
2. .NET 环境：兼容的 .NET 开发环境（例如 Visual Studio）。
3. 许可证设置：要使用 Aspose.Cells 的全部功能，请申请许可证。您可以[申请免费临时执照](https://purchase.aspose.com/temporary-license/)用于评估目的。
如果您是第一次评估，请从 Aspose.Cells 的免费试用版开始。
## 导入包
在我们进入代码之前，您需要将 Aspose.Cells 命名空间导入到您的项目中以访问所有必要的类和方法。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
让我们将这个过程分解成几个简单的步骤。在这里，我们将访问不同的纸张尺寸，将它们应用到工作表，然后打印每个尺寸。
## 步骤 1：创建工作簿实例
第一步是创建`Workbook`类。此对象将充当我们的主要工作簿，其中包含我们可以操作的工作表。
```csharp
Workbook book = new Workbook();
```
想想`Workbook`作为 Excel 文件的主要容器。我们需要它来访问和控制单个工作表。
## 第 2 步：访问第一个工作表
接下来，让我们访问工作簿中的第一个工作表。默认情况下，新工作簿附带一个工作表，因此我们可以使用索引直接引用它`0`.
```csharp
Worksheet sheet = book.Worksheets[0];
```
这`Worksheets`收藏于`Workbook`允许我们通过索引访问每个工作表。在这里，我们抓取第一个工作表来开始设置页面尺寸。
## 步骤 3：将纸张尺寸设置为 A2 并显示尺寸
现在我们可以访问工作表了，让我们将其纸张大小设置为 A2。设置纸张大小对于在打印或导出之前格式化页面很有用。设置纸张大小后，我们将以英寸为单位打印页面尺寸。
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
在这里，我们改变`PaperSize`财产`PaperA2` 设定尺寸后，`PageSetup.PaperWidth`和`PageSetup.PaperHeight`检索纸张的宽度和高度（以英寸为单位）。这让我们可以快速概览页面尺寸。
## 步骤 4：将纸张尺寸设置为 A3 并显示尺寸
按照与上述相同的步骤，我们将页面尺寸调整为 A3 尺寸。此更改对于稍大一些的打印件或在一页上容纳更多内容很有用。
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
A3 尺寸是 A4 尺寸的两倍，非常适合用于大型表格或详细图表。更改纸张尺寸有助于相应地调整工作表布局。
## 步骤 5：将纸张尺寸设置为 A4 并显示尺寸
现在，让我们将纸张尺寸设置为 A4。这是打印文档最常用的页面尺寸。稍后我们将显示更新后的尺寸。
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
如果您的目标是标准文档格式，A4 通常是最合适的尺寸。了解尺寸有助于调整内容布局，避免打印问题。
## 步骤 6：将纸张尺寸设置为信纸和显示尺寸
最后，我们将纸张尺寸设置为北美常用的 Letter 格式。让我们最后一次打印尺寸。
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
北美的文件广泛使用 Letter 尺寸，因此设置此尺寸有助于与那里的团队或客户合作。
## 结论
在本教程中，我们介绍了如何使用 Aspose.Cells for .NET 设置和检索不同纸张尺寸的页面尺寸。通过配置 A2、A3、A4 和 Letter 等页面尺寸，您可以格式化 Excel 工作表以满足特定的打印和布局需求。这种对页面尺寸的控制对于专业报告和演示尤其有价值，因为它可以确保您的内容完美适合每种页面尺寸。
## 常见问题解答
### 如何在 Aspose.Cells 中更改页面的方向？  
您可以使用`PageSetup.Orientation`属性，将其设置为`PageOrientationType.Portrait`或者`PageOrientationType.Landscape`.
### 我可以在 Aspose.Cells 中设置自定义页面尺寸吗？  
是的，您可以通过调整页边距和缩放选项来设置自定义页面尺寸`PageSetup`以获得更多控制。
### Aspose.Cells 中的默认纸张尺寸是多少？  
默认纸张尺寸通常为 A4。但这可能取决于区域设置，可根据需要进行调整。
### 是否可以在 Aspose.Cells 中预览页面布局？  
虽然 Aspose.Cells 不提供图形预览，但您可以以编程方式设置布局并在 Excel 中使用打印预览。
### 如何安装 Aspose.Cells for .NET？  
您可以使用 Visual Studio 中的 NuGet 包管理器安装 Aspose.Cells，或者从[Aspose.Cells 下载页面](https://releases.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
