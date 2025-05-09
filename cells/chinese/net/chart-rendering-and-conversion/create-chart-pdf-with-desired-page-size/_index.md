---
"description": "使用 Aspose.Cells for .NET 创建包含 Excel 图表的 PDF。通过本分步指南学习如何操作。"
"linktitle": "创建具有所需页面大小的图表 PDF"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "创建具有所需页面大小的图表 PDF"
"url": "/zh/net/chart-rendering-and-conversion/create-chart-pdf-with-desired-page-size/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 创建具有所需页面大小的图表 PDF

## 介绍

创建视觉吸引力强且信息丰富的图表对于各个领域的数据呈现至关重要。无论您处理的是销售数据、绩效指标还是其他类型的信息，能够生成高质量的图表都能让您的研究结果更具深度和清晰度。如果您使用 .NET 应用程序，Aspose.Cells 是一个功能强大的库，可让您轻松处理 Excel 文档并生成图表。在本教程中，我们将指导您如何从 Excel 文件创建具有所需页面大小的图表 PDF。

## 先决条件

在深入研究代码之前，您必须满足一些先决条件以确保获得顺畅的体验：

### C# 和 .NET 基础知识

你需要对 C# 编程和 .NET 框架有基本的了解。这将帮助你掌握本指南中遇到的代码结构。

### Aspose.Cells for .NET

确保已安装 Aspose.Cells for .NET。您可以在 [Aspose.Cells 文档](https://reference。aspose.com/cells/net/). 

### 开发环境

设置您的开发环境。可以是 Visual Studio 或任何其他支持 C# 的 IDE。从以下位置下载并安装 Aspose.Cells 库： [下载页面](https://releases。aspose.com/cells/net/).

### 示例 Excel 文件

您需要一个包含至少一个图表的示例 Excel 文件。您可以创建一个示例文件，也可以下载一个，以供本教程使用。

## 导入包

要开始使用 Aspose.Cells，您需要在 C# 应用程序中导入必要的命名空间。操作方法如下：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Aspose.Cells.Charts;
```

这些命名空间使您可以访问操作 Excel 工作簿及其内容所需的类和方法。

现在我们已经整理好了所有先决条件，让我们将过程分解为详细的步骤。

## 步骤 1：设置输出和源目录

首先，您需要定义输出 PDF 的保存位置以及源 Excel 文档的位置。

```csharp
//输出目录
string outputDir = "Your Output Directory";

//源目录
string sourceDir = "Your Document Directory";
```

确保将“您的输出目录”和“您的文档目录”替换为您系统上的实际路径。这决定了 Aspose 将保存生成的 PDF 的位置以及 Excel 文件的位置。

## 步骤 2：加载示例 Excel 文件

接下来，您需要加载包含图表的 Excel 文件。操作方法如下：

```csharp
//加载包含图表的示例 Excel 文件。
Workbook wb = new Workbook(sourceDir + "sampleCreateChartPDFWithDesiredPageSize.xlsx");
```

这 `Workbook` 类是与 Excel 文档交互的核心。请确保路径正确指向您的 Excel 文件——此处的错误将导致其余代码无法执行。

## 步骤 3：访问第一个工作表

工作簿加载完成后，下一步是访问包含所需图表的工作表。

```csharp
//访问第一个工作表。
Worksheet ws = wb.Worksheets[0];
```

在 Aspose.Cells 中，工作表从零开始索引，因此 `Worksheets[0]` 指的是第一张表。

## 步骤 4：访问第一个图表

现在，让我们访问要导出为 PDF 的图表。此步骤假设您的工作表至少包含一个图表。

```csharp
//访问工作表内的第一个图表。
Chart ch = ws.Charts[0];
```

再次，这将访问工作表中的第一个图表；确保您的工作表结构适合这种方法。

## 步骤 5：创建具有所需页面大小的 PDF

最后，是时候根据指定的页面大小将图表创建为 PDF 了。以下是完成所有操作的神奇代码：

```csharp
//创建具有所需页面大小的图表 pdf。
ch.ToPdf(outputDir + "outputCreateChartPDFWithDesiredPageSize.pdf", 7, 7, PageLayoutAlignmentType.Center, PageLayoutAlignmentType.Center);
```

在此代码中：
- PDF 将保存到您之前指定的输出目录。
- 数字 `7, 7` 分别表示所需页面大小的宽度和高度。
- PageLayoutAlignmentType.Center 确保图表位于页面中央。

## 步骤6：确认消息

为了让您自己（和其他人）知道一切顺利，请在代码末尾添加一条确认消息：

```csharp
Console.WriteLine("CreateChartPDFWithDesiredPageSize executed successfully.");
```

该过程完成后，此消息将出现在控制台窗口中，表示您的 PDF 已顺利创建。

## 结论

恭喜！您刚刚学习了如何利用 Aspose.Cells for .NET 将 Excel 文件中的图表创建为 PDF。这个强大的库简化了操作 Excel 文档和生成数据可视化表示的流程，节省了您数小时的手动格式化时间。除了 PDF 生成之外，Aspose.Cells 还提供了许多其他功能——您永远不知道哪些功能会进一步提升您的项目！

## 常见问题解答

### Aspose.Cells for .NET 用于什么？  
Aspose.Cells for .NET 用于在 .NET 应用程序中以编程方式创建、编辑和转换 Excel 文档。

### 我可以免费使用 Aspose.Cells 吗？  
是的，Aspose.Cells 提供 [免费试用](https://releases.aspose.com/) 用于评估目的。

### 有没有办法将试用期延长至初始期限之后？  
您可以申请 [临时执照](https://purchase.aspose.com/temporary-license/) 进行扩展测试。

### 如果我遇到问题或有疑问怎么办？  
您可以在 Aspose 社区上寻求帮助 [支持论坛](https://forum。aspose.com/c/cells/9).

### 如何购买 Aspose.Cells？  
您可以从 [购买页面](https://purchase。aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}