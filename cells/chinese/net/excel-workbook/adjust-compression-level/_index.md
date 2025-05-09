---
"description": "了解如何使用 Aspose.Cells for .NET 调整 Excel 文件的压缩级别。遵循本分步指南，高效优化文件大小。"
"linktitle": "调整压缩级别"
"second_title": "Aspose.Cells for .NET API参考"
"title": "调整压缩级别"
"url": "/zh/net/excel-workbook/adjust-compression-level/"
"weight": 50
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 调整压缩级别

## 介绍

在处理大型 Excel 文件时，高效的存储至关重要。无论您是希望优化文件大小的开发人员，还是希望加快文件传输速度的数据分析师，了解如何在 Aspose.Cells for .NET 中调整压缩级别都将带来显著的改变。在本指南中，我们将引导您完成保存 Excel 文件时调整压缩级别的步骤，确保您在不牺牲质量的情况下保持性能。

## 先决条件

在深入研究压缩级别之前，让我们确保您已准备好开始所需的一切：

1. C# 基础知识：掌握 C# 编程的基础知识至关重要。如果您熟悉变量、循环和基本文件操作，那么就可以轻松上手！
2. Aspose.Cells for .NET 库：确保您已安装 Aspose.Cells 库。您可以从 [网站](https://releases.aspose.com/cells/net/)。如果您刚刚开始，请考虑免费试用 [这里](https://releases。aspose.com/).
3. 开发环境：设置您的开发环境，最好是 Visual Studio，以编写和执行您的 C# 代码。 
4. 示例 Excel 文件：准备一个较大的 Excel 文件进行测试。您可以创建一个，也可以使用任何现有文件，但请确保其大小足够大，以便查看压缩效果。

有了这些先决条件，我们就开始吧！

## 导入包

在操作Excel文件之前，我们需要导入必要的命名空间。这是至关重要的一步，它使我们能够访问Aspose.Cells提供的类和方法。

### 导入 Aspose.Cells 命名空间

```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```

此代码片段导入 `Aspose.Cells` 命名空间，其中包含处理 Excel 文件所需的所有类。 `Aspose.Cells.Xlsb` 命名空间专门用于处理 XLSB 文件格式。

现在一切设置完毕，让我们将调整压缩级别的过程分解成几个易于管理的步骤。我们将保存一个具有不同压缩级别的工作簿，并测量每个操作所需的时间。 

## 步骤 1：设置目录

首先，我们需要定义文件的存储位置。这包括指定输入文件的源目录和压缩文件的输出目录。

```csharp
// 源目录
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```

## 第 2 步：加载工作簿

接下来，我们将加载要压缩的 Excel 工作簿。在这里，您需要指向大型 Excel 文件。

```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```

这行初始化一个新的 `Workbook` 将对象与指定的文件关联。请确保文件路径正确，否则会出错。

## 步骤 3：为 XLSB 创建保存选项

现在，我们将创建一个 `XlsbSaveOptions`，它允许我们指定如何保存工作簿，包括压缩级别。

```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```

此行准备了我们将用于以 XLSB 格式保存工作簿的选项。

## 步骤 4：设置并测量压缩级别

现在到了最有趣的部分！我们将使用不同的压缩级别保存工作簿，并测量每个操作所需的时间。 

### 1级压缩

让我们从最低压缩级别开始：

```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = System.Diagnostics.Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```

在此代码片段中，我们将压缩类型设置为 1 级，保存工作簿，并记录所花费的时间。 

### 6级压缩

接下来，我们将尝试中等压缩级别：

```csharp
options.CompressionType = OoxmlCompressionType.Level6;
watch = System.Diagnostics.Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```

这次，我们将压缩类型设置为6级，并重复保存操作。

### 9级压缩

最后，让我们使用最高压缩级别进行保存：

```csharp
options.CompressionType = OoxmlCompressionType.Level9;
watch = System.Diagnostics.Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_9_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 9 Elapsed Time: " + elapsedMs);
```

在此步骤中，我们将压缩类型设置为 9 级，这应该会产生最小的文件大小，但可能需要更长时间才能保存。

## 步骤5：最终输出

执行完上述所有步骤后，您将看到打印到控制台的每个压缩级别的经过时间。 

```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```

此行确认整个过程已顺利完成。

## 结论

使用 Aspose.Cells for .NET 保存 Excel 文件时调整压缩级别是一项简单而强大的技巧。按照本指南中概述的步骤，您可以轻松调整文件大小，使其更易于存储和传输。无论您是需要快速访问数据还是希望优化应用程序性能，掌握这些技巧无疑将提升您作为开发人员的技能。

## 常见问题解答

### 什么是 Aspose.Cells？
Aspose.Cells 是一个 .NET 库，允许开发人员以编程方式创建、操作和转换 Excel 文件。

### 如何下载 Aspose.Cells？
您可以从 [网站](https://releases。aspose.com/cells/net/).

### 我可以免费使用 Aspose.Cells 吗？
是的，Aspose 提供免费试用版，您可以访问 [这里](https://releases。aspose.com/).

### 有哪些不同的压缩级别可用？
Aspose.Cells 支持多种压缩级别，从 1 级（最低压缩）到 9 级（最高压缩）。

### 在哪里可以找到对 Aspose.Cells 的支持？
您可以获得支持并提出问题 [Aspose 论坛](https://forum。aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}