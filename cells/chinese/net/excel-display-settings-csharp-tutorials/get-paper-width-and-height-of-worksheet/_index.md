---
title: 获取工作表的纸张宽度和高度
linktitle: 获取工作表的纸张宽度和高度
second_title: Aspose.Cells for .NET API 参考
description: 通过简单的分步指南了解如何在 Aspose.Cells for .NET 中获取工作表的纸张宽度和高度。
weight: 80
url: /zh/net/excel-display-settings-csharp-tutorials/get-paper-width-and-height-of-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 获取工作表的纸张宽度和高度

## 介绍

是否曾经尝试打印 Excel 表格并处理各种纸张尺寸的混乱尺寸？如果您和我一样，您就会知道没有什么比布局不正确更能毁掉您的一天了！无论您是打印报告、发票还是只是一个简单的列表，了解如何以编程方式调整纸张尺寸都可以为您省去很多麻烦。今天，我们将深入研究 Aspose.Cells for .NET 的世界，研究如何直接在您的应用程序中检索和设置纸张尺寸。让我们撸起袖子，深入了解管理这些纸张尺寸的细节！

## 先决条件 

在我们进入编码魔法之前，让我们先收集一下开始所需的信息：

1. 对 C# 有基本了解：您应该对 C# 有初步了解。如果您是编程新手，不用担心！我们会尽量讲得简单易懂。
2.  Aspose.Cells 库：确保您的机器上安装了 .NET 的 Aspose.Cells 库。您可以从以下网址下载[此链接](https://releases.aspose.com/cells/net/).
3. .NET 开发环境：设置 Visual Studio 或您选择的任何 IDE 来编写和执行您的 C# 代码。如果您不确定从哪里开始，Visual Studio 社区版是一个不错的选择。
4. 参考文献和文档：熟悉 Aspose.Cells 文档以获得更深入的见解。您可以找到它[这里](https://reference.aspose.com/cells/net/).
5. 基本 Excel 文件知识：了解 Excel 文件的结构（工作表、行和列）将大有帮助。

太棒了！现在我们已经完成了基本工作，让我们直接开始导入必要的包。

## 导入包

为了让我们的生活更轻松，充分利用 Aspose.Cells 的全部功能，我们需要导入几个包。这就像添加一个`using`代码文件顶部的语句。以下是您需要导入的内容：

```csharp
using System;
using System.IO;
```

此行允许我们访问 Aspose.Cells 库中的所有类和方法，从而更轻松地操作 Excel 文件。现在，让我们逐步了解如何检索各种纸张尺寸的纸张宽度和高度。

## 步骤 1：创建新工作簿

使用 Aspose.Cells 的第一步是创建一个新的工作簿。将工作簿视为一个空白画布，您可以在其中添加工作表、单元格，以及在我们的例子中定义纸张大小。

```csharp
//创建工作簿
Workbook wb = new Workbook();
```

这行代码实例化了一个新的工作簿对象，可供我们操作。您现在还看不到任何东西，但我们的画布已经设置好了！

## 第 2 步：访问第一个工作表

现在我们有了工作簿，我们需要访问其中的特定工作表。工作表就像工作簿中的一页，所有操作都发生在这里。

```csharp
//访问第一个工作表
Worksheet ws = wb.Worksheets[0];
```

这里，我们从工作簿中抓取第一个工作表（索引 0）。您可以将其想象为翻到书的第一页。 

## 步骤 3：设置纸张尺寸并获取尺寸

现在到了激动人心的部分！我们将设置不同的纸张尺寸并逐一检索它们的尺寸。这一步至关重要，因为它让我们看到不同的尺寸如何影响布局。

```csharp
//将纸张尺寸设置为 A2 并以英寸为单位打印纸张宽度和高度
ws.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```

在此块中，我们将纸张尺寸设置为 A2，然后检索其宽度和高度。`PaperWidth`和`PaperHeight`属性提供以英寸为单位的尺寸。这就像在将图片放入相框之前先检查相框的尺寸一样。

## 步骤 4：对其他纸张尺寸重复上述步骤

让我们对其他常见纸张尺寸重复此过程。我们将检查 A3、A4 和 Letter 尺寸。此重复对于理解 Aspose.Cells 框架中每个尺寸的定义方式非常重要。

```csharp
//将纸张尺寸设置为 A3 并以英寸为单位打印纸张的宽度和高度
ws.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
//将纸张尺寸设置为 A4 并以英寸为单位打印纸张的宽度和高度
ws.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
//将纸张大小设置为 Letter，并以英寸为单位打印纸张的宽度和高度
ws.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```

这些块中的每一个都模仿了上一步，但调整了`PaperSize`属性。只需更改尺寸指示器，即可轻松获得不同的纸张尺寸。这就像根据存储需要更改盒子的尺寸一样！

## 结论

就这样！按照这些步骤，您可以轻松地在 Aspose.Cells for .NET 中设置和检索各种纸张尺寸的尺寸。此功能不仅可以节省您的时间，还可以防止由于页面设置配置错误而导致的打印事故。因此，下次您需要打印 Excel 工作表或创建报告时，您可以放心地进行操作，因为您知道尺寸就在您手中。 

## 常见问题解答

### 什么是 Aspose.Cells？
Aspose.Cells 是一个.NET 库，专为处理 Excel 文件而设计，无需安装 Excel。

### 我可以免费使用 Aspose.Cells 吗？
是的！您可以先免费试用，网址为[此链接](https://releases.aspose.com/).

### 如何设置自定义纸张尺寸？
 Aspose.Cells 提供了使用以下选项设置自定义纸张尺寸`PageSetup`班级。

### 使用 Aspose.Cells 是否需要编码知识？
基本的编码知识会有所帮助，但您可以按照教程更轻松地理解！

### 在哪里可以找到更多示例？
这[Aspose.Cells 文档](https://reference.aspose.com/cells/net/)提供丰富的实例和教程。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
