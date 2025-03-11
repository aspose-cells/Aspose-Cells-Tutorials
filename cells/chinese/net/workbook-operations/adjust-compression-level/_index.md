---
title: 调整工作簿中的压缩级别
linktitle: 调整工作簿中的压缩级别
second_title: Aspose.Cells .NET Excel 处理 API
description: 通过本分步指南了解如何使用 Aspose.Cells for .NET 调整 Excel 工作簿的压缩级别。优化您的文件管理。
weight: 14
url: /zh/net/workbook-operations/adjust-compression-level/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 调整工作簿中的压缩级别

## 介绍
在管理大型 Excel 文件时，压缩可以改变游戏规则。它不仅可以节省存储空间，还可以使文件传输更快、更高效。如果您使用 Aspose.Cells for .NET，则可以轻松调整工作簿的压缩级别。在本指南中，我们将逐步引导您完成该过程，确保您了解代码的每个部分及其工作原理。
## 先决条件
在深入研究代码之前，您需要满足一些先决条件：
1. C# 基础知识：熟悉 C# 编程将帮助您更好地理解代码片段。
2.  Aspose.Cells 库：您需要安装 Aspose.Cells 库。您可以从以下网址下载[这里](https://releases.aspose.com/cells/net/).
3. Visual Studio：运行代码需要像 Visual Studio 这样的开发环境。
4. .NET Framework：确保您的项目设置了兼容版本的 .NET Framework。
## 导入包
首先，您需要在 C# 项目中导入必要的包。具体操作如下：
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```
这些包对于使用 Aspose.Cells 库处理 Excel 文件至关重要。`Aspose.Cells`命名空间包含操作 Excel 文件所需的所有类，而`Aspose.Cells.Xlsb`提供以 XLSB 格式保存文件的选项。
现在，让我们将调整工作簿中的压缩级别的过程分解为易于管理的步骤。
## 步骤 1：定义源和输出目录
首先，你需要指定源文件的位置以及要保存输出文件的位置。这对于确保你的程序知道在哪里找到需要处理的文件至关重要。
```csharp
//源目录
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```
代替`"Your Document Directory"`替换为目录的实际路径。这将帮助程序找到您要压缩的文件。
## 步骤 2：加载工作簿
接下来，您将加载要压缩的工作簿。这就是魔法开始的地方！
```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```
在这一行中，我们创建了`Workbook`类并加载现有的 Excel 文件。确保文件名与源目录中的文件名匹配。
## 步骤 3：设置保存选项
现在该配置保存选项了。我们将设置输出文件的压缩类型。 
```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```
这`XlsbSaveOptions`该类允许您在以 XLSB 格式保存工作簿时指定各种选项，包括压缩级别。
## 步骤 4：测量 1 级压缩时间
让我们从第一个压缩级别开始。我们将测量使用此压缩级别保存工作簿需要多长时间。
```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```
在这里，我们将压缩类型设置为 1 级，保存工作簿，然后测量所用时间。这让我们了解该过程需要多长时间。
## 步骤 5：测量第 6 级的压缩时间
接下来我们看看 6 级压缩的表现如何。
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level6;
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```
这一步与上一步类似，但我们将压缩级别更改为 6 级。您会注意到，所花费的时间可能会根据工作簿的复杂程度而有所不同。
## 步骤 6：测量第 9 级的压缩时间
最后，我们来检查一下最高压缩级别的性能。
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level9;
workbook.Save(outDir + "LargeSampleFile_level_9_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 9 Elapsed Time: " + elapsedMs);
```
在此步骤中，我们将压缩级别设置为 9 级。此时您通常会看到文件大小最显著的减少，但处理时间可能会更长。
## 步骤7：最终输出
运行完所有压缩级别后，可以输出一条消息，表明该过程已成功完成。
```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```
这行简单的代码确认您的程序已顺利完成执行。
## 结论
使用 Aspose.Cells for .NET 调整工作簿的压缩级别是一个简单的过程，可以显著减少文件大小和性能。按照本指南中概述的步骤，您可以轻松地在应用程序中实现压缩并提高 Excel 文件管理的效率。
## 常见问题解答
### 什么是 Aspose.Cells？  
Aspose.Cells 是一个强大的.NET 库，允许开发人员创建、操作和转换 Excel 文件，而无需 Microsoft Excel。
### 如何安装 Aspose.Cells？  
您可以从[Aspose 网站](https://releases.aspose.com/cells/net/).
### 有哪些压缩级别？  
Aspose.Cells 支持多种压缩级别，从 1 级（最低压缩）到 9 级（最高压缩）。
### 我可以免费测试 Aspose.Cells 吗？  
是的！您可以免费试用 Aspose.Cells[这里](https://releases.aspose.com/).
### 在哪里可以找到对 Aspose.Cells 的支持？  
如有任何疑问或需要支持，您可以访问 Aspose 支持论坛[这里](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
