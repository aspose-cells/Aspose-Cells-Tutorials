---
"description": "通过我们简单易懂的指南，了解如何使用 Aspose.Cells for .NET 控制 Excel 到 PDF 转换中的外部资源。"
"linktitle": "在 Aspose.Cells 中控制 Excel 中的外部资源转换为 PDF"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "在 Aspose.Cells 中控制 Excel 中的外部资源转换为 PDF"
"url": "/zh/net/rendering-and-export/control-loading-of-external-resources/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Aspose.Cells 中控制 Excel 中的外部资源转换为 PDF

## 介绍
在当今的数字时代，将 Excel 电子表格转换为 PDF 文档是一项常见的任务。无论是准备报告、财务数据还是演示文稿，您都希望确保 PDF 的外观完全符合您的预期。Aspose.Cells for .NET 是一个强大的库，它允许您控制转换过程的每个细节，尤其是在处理 Excel 文件附带的图像等外部资源时。在本指南中，我们将深入探讨如何使用 Aspose.Cells 在 Excel 到 PDF 的转换过程中控制外部资源。所以，准备好您最喜欢的饮料，让我们开始吧！
## 先决条件
在深入探讨细节之前，我们先来确认一下你已准备好一切，以便开始行动。以下是一份快速检查清单：
1. Visual Studio 或任何与 .NET 兼容的 IDE：您需要一个环境来编写和测试您的代码。
2. Aspose.Cells for .NET：如果您尚未安装，请前往 [Aspose 下载](https://releases.aspose.com/cells/net/) 页面并获取最新版本。
3. C# 基础知识：熟悉 C# 编程语言将大有裨益。如果您对任何概念感到困惑，请随时查阅相关知识。
4. 示例 Excel 文件：准备一个 Excel 文件，其中包含您想要转换的任何外部资源。您可以使用提供的示例文件“samplePdfSaveOptions_StreamProvider.xlsx”。
5. 用于测试的图像文件：这将在转换过程中用作外部资源。图像文件“newPdfSaveOptions_StreamProvider.png”是一个很好的占位符。
## 导入包
首先，您需要从 Aspose.Cells 库导入必要的命名空间。这对于访问其功能至关重要。请确保在文件顶部添加以下 using 指令：
```csharp
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Rendering;
using System;
```
这些包将提供执行任务所需的所有基本类和方法。
## 步骤 1：创建流提供程序类
第一项工作是创建一个流提供程序类，实现 `IStreamProvider` 接口。此类将允许您控制如何加载外部资源。
```csharp
class MyStreamProvider : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        Debug.WriteLine("-----Close Stream-----");
    }
    public void InitStream(StreamProviderOptions options)
    {
        string sourceDir = "Your Document Directory";
        Debug.WriteLine("-----Init Stream-----");
        // 在内存流中读取新图像并将其分配给 Stream 属性
        byte[] bts = File.ReadAllBytes(sourceDir + "newPdfSaveOptions_StreamProvider.png");
        MemoryStream ms = new MemoryStream(bts);
        options.Stream = ms;
    }
}
```
在本课程中：
- CloseStream：当流关闭时，此方法将被调用。目前，我们只是编写一条调试消息进行跟踪。
- InitStream：魔法从这里开始。在这里，你将读取外部图像作为字节数组，将其转换为内存流，并将其分配给 `options.Stream` 财产。
## 步骤 2：设置源和输出目录
现在您的流提供商已经准备就绪，是时候确定您的 Excel 文件的位置以及您想要保存 PDF 的位置了。
```csharp
// 源目录
string sourceDir = "Your Document Directory";
// 输出目录
string outputDir = "Your Document Directory";
```
只需更换 `"Your Document Directory"` 与您计算机上文件所在的实际路径一致。保持文件井然有序是关键！
## 步骤3：加载Excel文件
接下来，您将加载要从中创建 PDF 的 Excel 文件。
```csharp
// 加载包含外部图像的源 Excel 文件
Workbook wb = new Workbook(sourceDir + "samplePdfSaveOptions_StreamProvider.xlsx");
```
我们正在使用 `Workbook` Aspose.Cells 中的类，代表您的 Excel 文件。该文件可以包含各种外部资源，例如您想要在转换过程中控制的图像。
## 步骤 4：设置 PDF 保存选项
在将工作簿保存为 PDF 之前，请先指定保存方式。您可以根据需要调整这些选项。
```csharp
// 指定 PDF 保存选项 - Stream Provider
PdfSaveOptions opts = new PdfSaveOptions();
opts.OnePagePerSheet = true; // 将每张表保存在新页面上
```
在这里，我们创建一个新的实例 `PdfSaveOptions`，它允许您自定义 PDF 的格式。 `OnePagePerSheet` 该选项可方便确保每个 Excel 表在最终的 PDF 中都有自己的页面。
## 步骤 5：指定您的流媒体提供商
设置 PDF 选项后，您需要告诉 Aspose 使用自定义流提供程序来获取外部资源。
```csharp
wb.Settings.StreamProvider = new MyStreamProvider();
```
这条线连接你的 `Workbook` 实例 `MyStreamProvider` 您之前创建的类。这意味着，无论何时在转换过程中遇到外部资源，您的提供程序都会按照指定的方式处理它们。
## 步骤 6：将工作簿保存为 PDF
一切设置完成后，终于可以将 Excel 工作簿保存为 PDF 了。
```csharp
// 将工作簿保存为 PDF
wb.Save(outputDir + "outputPdfSaveOptions_StreamProvider.pdf", opts);
```
通过调用 `Save` 方法在工作簿对象上并传入输出目录以及 PDF 选项，您就可以将 Excel 文件转换为格式精美的 PDF。
## 步骤7：确认执行成功
总而言之，确认您的流程已成功总是令人高兴的！
```csharp
Console.WriteLine("ControlLoadingOfExternalResourcesInExcelToPDF executed successfully.\r\n");
```
将成功消息打印到控制台有助于您随时了解操作状态。在代码中包含这些简单的确认信息是一个好习惯。
## 结论
就是这样！只需遵循这些简单的步骤，您就可以使用 Aspose.Cells 熟练地控制 Excel 到 PDF 转换过程中外部资源的处理方式。这意味着您的文档现在可以准确地包含图像和其他外部元素，确保每次都能获得完美的最终产品。
## 常见问题解答
### 什么是 Aspose.Cells？  
Aspose.Cells 是一个面向 .NET 开发人员的强大库，允许您创建、操作、转换和呈现各种格式的 Excel 文件。
### 如何下载 Aspose.Cells？  
您可以从 [下载链接](https://releases。aspose.com/cells/net/).
### 我可以免费试用 Aspose.Cells 吗？  
是的！您可以访问以下链接获取免费试用 [免费试用页面](https://releases。aspose.com/).
### 在哪里可以找到对 Aspose.Cells 的支持？  
对于任何与支持相关的疑问，您可以访问 [Aspose 支持论坛](https://forum。aspose.com/c/cells/9).
### 如何获得 Aspose.Cells 的临时许可证？  
您可以申请临时驾照 [这里](https://purchase。aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}