---
title: 在 Excel 中旋转带形状的文本
linktitle: 在 Excel 中旋转带形状的文本
second_title: Aspose.Cells .NET Excel 处理 API
description: 了解如何使用 Aspose.Cells for .NET 在 Excel 中旋转带有形状的文本。按照此分步指南进行操作，即可获得完美的 Excel 演示。
weight: 12
url: /zh/net/excel-shape-text-modifications/rotate-text-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中旋转带形状的文本

## 介绍
在 Excel 世界中，视觉呈现与数据本身同样重要。无论您是制作报告还是设计动态仪表板，信息的布局方式都会极大地影响其可读性和整体外观。那么，您是否曾经想旋转文本以使其与形状时尚地对齐？你很幸运！在本教程中，我们将深入研究如何使用 Aspose.Cells for .NET 旋转带有形状的文本，确保您的电子表格不仅提供信息，而且令人印象深刻。
## 先决条件
在开始之前，让我们确保您已获得所需的一切：
1. Visual Studio：确保您的机器上安装了 Visual Studio，因为我们将在那里编写代码。
2.  Aspose.Cells for .NET：您需要 Aspose.Cells 库。您可以[点击这里下载最新版本](https://releases.aspose.com/cells/net/)或者免费试用[免费试用](https://releases.aspose.com/).
3. C# 基础知识：熟悉 C# 和 .NET 环境将会很有帮助，但我们会指导您完成每一步。
4.  Excel 文件：示例 Excel 文件，我们称之为`sampleRotateTextWithShapeInsideWorksheet.xlsx`，是测试我们的代码所必需的。您应该将此文件放在您可以轻松访问的目录中。
一切都准备好了吗？太棒了！让我们进入最有趣的部分。
## 导入包
首先，我们需要将必要的包导入到我们的项目中。操作方法如下：
### 创建新项目
1. 打开 Visual Studio。
2. 选择“创建新项目”。
3. 选择“控制台应用程序”并选择 C# 作为您的首选编程语言。
### 安装 Aspose.Cells
现在，让我们将 Aspose.Cells 添加到您的项目中。您可以使用 NuGet 包管理器执行此操作：
1. 在顶部菜单中打开“工具”。
2. 选择“NuGet 包管理器”，然后选择“管理解决方案的 NuGet 包”。
3. 搜索“Aspose.Cells”。
4. 单击“安装”将其添加到您的项目中。
### 添加使用指令
在主 C# 文件的顶部，需要添加以下指令：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
现在我们就可以开始编码了！
让我们将这个过程分解成容易理解的步骤。以下是如何在 Excel 文件中旋转带有形状的文本：
## 步骤 1：设置目录路径
首先，您需要设置存储 Excel 文件的源目录和输出目录。操作方法如下：
```csharp
//源目录
string sourceDir = "Your Document Directory"; //设置文档目录
//输出目录
string outputDir = "Your Document Directory"; //设置输出目录
```
代替`"Your Document Directory"`实际路径`sampleRotateTextWithShapeInsideWorksheet.xlsx`文件位于。
## 步骤 2：加载示例 Excel 文件
现在，让我们加载示例 Excel 文件。这很关键，因为我们要操作现有数据。
```csharp
//加载示例 Excel 文件。
Workbook wb = new Workbook(sourceDir + "sampleRotateTextWithShapeInsideWorksheet.xlsx");
```
## 步骤 3：访问工作表
文件加载完成后，我们需要访问要修改的特定工作表。在我们的例子中，它是第一个工作表。
```csharp
//访问第一个工作表。
Worksheet ws = wb.Worksheets[0];
```
## 步骤 4：修改单元格
接下来，我们将修改特定单元格以显示消息。在我们的示例中，我们将使用单元格 B4。
```csharp
//访问单元格 B4 并在其中添加一条消息。
Cell b4 = ws.Cells["B4"];
b4.PutValue("Text is not rotating with shape because RotateTextWithShape is false.");
```
这一步主要是沟通——确保无论谁打开这张表都能明白我们正在调整什么。
## 步骤 5：访问第一个形状
要旋转文本，我们需要一个形状。在这里，我们将访问工作表中的第一个形状。
```csharp
//访问第一个形状。
Shape sh = ws.Shapes[0];
```
## 步骤 6：调整形状文本对齐方式
奇迹就在这里发生。我们将调整形状的文本对齐属性。
```csharp
//访问形状文本对齐方式。
Aspose.Cells.Drawing.Texts.ShapeTextAlignment shapeTextAlignment = sh.TextBody.TextAlignment;
//通过将 RotateTextWithShape 设置为 false，不要旋转具有形状的文本。
shapeTextAlignment.RotateTextWithShape = false;
```
通过设置`RotateTextWithShape`为 false，我们确保文本保持直立并且不会随形状旋转，从而使一切保持整洁有序。
## 步骤 7：保存输出 Excel 文件
最后，让我们将更改保存到新的 Excel 文件中。这可确保我们不会丢失编辑内容并获得整洁的输出。
```csharp
//保存输出 Excel 文件。
wb.Save(outputDir + "outputRotateTextWithShapeInsideWorksheet.xlsx");
```
就这样！您的输出文件现已保存，包括单元格 B4 中的文本和对形状所做的调整。
## 步骤 8：执行代码
在你的`Main`方法，包装上述所有代码片段，然后运行您的项目。查看输出文件中反映的更改！
```csharp
Console.WriteLine("RotateTextWithShapeInsideWorksheet executed successfully.");
```
## 结论
使用 Aspose.Cells for .NET 在 Excel 中旋转带有形状的文本乍一看似乎是一个复杂的过程，但一旦分解它就会变得非常简单。通过遵循这些简单的步骤，您可以自定义电子表格，使其看起来更专业、更具视觉吸引力。现在，无论您是为客户还是个人项目执行此操作，每个人都会对您的工作质量赞不绝口！
## 常见问题解答
### 我可以免费使用 Aspose.Cells 吗？
是的！您可以使用[免费试用](https://releases.aspose.com/)尝试一下这个图书馆。
### Aspose.Cells 支持哪些版本的 Excel？
Aspose.Cells 支持多种 Excel 格式，包括 XLS、XLSX、CSV 等。
### 在旧版本的 Excel 中可以旋转带有形状的文本吗？
是的，该功能可以应用于 Aspose.Cells 支持的旧格式。
### 在哪里可以找到有关 Aspose.Cells 的更多文档？
您可以探索全面的[文档](https://reference.aspose.com/cells/net/)以获得更多见解。
### 如何获得 Aspose.Cells 的支持？
您可以通过访问以下地址寻求支持[Aspose 论坛](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
