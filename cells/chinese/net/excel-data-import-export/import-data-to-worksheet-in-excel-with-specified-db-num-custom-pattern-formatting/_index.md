---
title: 使用自定义数据库数字模式格式将数据导入 Excel
linktitle: 使用自定义数据库数字模式格式将数据导入 Excel
second_title: Aspose.Cells .NET Excel 处理 API
description: 在本简单易懂的教程中学习如何使用 Aspose.Cells for .NET 将具有自定义 DB Num 格式的数据导入 Excel。
weight: 10
url: /zh/net/excel-data-import-export/import-data-to-worksheet-in-excel-with-specified-db-num-custom-pattern-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用自定义数据库数字模式格式将数据导入 Excel

## 介绍

当涉及到电子表格操作时，将数据导入 Excel 并正确格式化可能感觉是一项艰巨的任务，尤其是当您想要使用特定的基于文化的格式（例如 DB Num 模式）时。如果您曾经被 Excel 格式化的技术细节所困扰，那么您来对地方了！在本指南中，我们将使用 Aspose.Cells for .NET 将事情分解为简单的步骤，使您的数据导入不仅简单而且美观。所以，请稍等，因为我们将直接进入 .NET 编程、格式化和轻松导出 Excel 文件的世界！

## 先决条件

在深入讨论细节之前，让我们先确保您已准备好一切所需。以下是一份快速的先决条件清单，可帮助您取得成功：

1. .NET Framework：确保您的机器上安装了 .NET Framework。Aspose.Cells 可与各种 .NET 版本无缝协作。
2.  Aspose.Cells for .NET：您需要下载并安装 Aspose.Cells 库。您可以从[下载链接](https://releases.aspose.com/cells/net/).
3. 集成开发环境 (IDE)：使用 Visual Studio 之类的 IDE，您可以在其中编写和执行 C# 代码。
4. C# 基础知识：对 C# 有基本的了解将帮助您遵循我们在本指南中使用的编码实践。

一切都搞定了？太棒了！让我们继续导入必要的包。

## 导入包

为了有效地使用 Aspose.Cells，您需要在 C# 文件的开头导入所需的命名空间。让我们一步一步来。

### 创建 C# 文件

打开 IDE（建议使用 Visual Studio）并创建一个新的 C# 项目。将其命名为相关名称，例如`ExcelDataImport`.

### 参考 Aspose.Cells

您必须在项目中包含 Aspose.Cells 库。在解决方案资源管理器中右键单击您的项目并选择“添加引用”。浏览到您安装 Aspose.Cells 的位置并选择它。

### 导入必要的命名空间

在 C# 文件的顶部，导入以下命名空间：

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

这条简单的线路是您通向 Aspose.Cells 提供的所有功能的门户。 

现在我们已经满足了所有先决条件并导入了必要的软件包，让我们深入了解将数据导入 Excel 并应用自定义 DB Num 模式格式的分步过程。我们将有条不紊地进行这一过程，以确保清晰易懂。

## 步骤 1：设置数据目录

首先，您需要指定保存输出的文档目录的路径。根据您的文件结构进行调整。

```csharp
string dataDir = "Your Document Directory";
```

在此示例中，替换`Your Document Directory`与您的实际路径，如`C:\\Users\\YourName\\Documents\\`.

## 步骤 2：创建工作簿

接下来，您将创建一个新的工作簿，它本质上是您的 Excel 文件。

```csharp
Workbook wb = new Workbook();
```

在这里，我们实例化一个新的`Workbook`对象。这是你的空白画布！

## 步骤 3：访问第一个工作表

每个工作簿包含多个工作表。您需要访问第一个工作表才能开始输入数据。

```csharp
Worksheet ws = wb.Worksheets[0];
```

就像翻开一本书的第一页一样，您正在访问第一个工作表来添加数据。

## 步骤 4：将数据输入单元格

现在，让我们用一些数据填充单元格。在本例中，我们将输入值`123`进入单元格 A1。

```csharp
Cell cell = ws.Cells["A1"];
cell.PutValue(123);
```

您在这里直接与 Excel 对话 - 将数据直接输入单元格 A1！ 

## 步骤 5：访问单元格样式

每个单元格都有一种样式，您可以自定义其外观。要应用自定义格式，首先，您需要访问单元格的样式。

```csharp
Style st = cell.GetStyle();
```

通过抓住单元格的风格，您正准备添加自己独特的风格！

## 步骤 6：指定 DBNum 自定义模式格式

这就是奇迹发生的地方。您可以使用 DBNum 格式样式指定自定义格式模式。

```csharp
st.Custom = "[DBNum2][$-804]General";
```

这一行告诉 Excel 格式化数字`123`根据与中文对应的 DBNum 模式。很简洁，对吧？

## 步骤 7：设置更新的单元格样式

现在您已经定义了自定义样式，是时候将其应用到单元格了。

```csharp
cell.SetStyle(st);
```

这就像给你的手机穿上一件时髦的新衣服！

## 步骤 8：调整列宽

让我们确保一切看起来都漂亮又整洁。您可以调整第一列的宽度以更好地适应您的数据。

```csharp
ws.Cells.SetColumnWidth(0, 30);
```

在这里，我们扩大了列宽，这样您的数据就不会显得拥挤。想象一下给您的数据留出呼吸的空间！

## 步骤 9：保存工作簿

最后，让我们将这份杰作保存为 PDF 格式。这才是压轴大戏！

```csharp
wb.Save(dataDir + "outputDBNumCustomFormatting.pdf", SaveFormat.Pdf);
```

恭喜！您刚刚创建了一个 PDF 文件，其中展示了使用 DB Num 样式格式化的数字。

## 结论

就这样！您已成功将数据导入 Excel，应用自定义 DB Num 格式，并将其保存为 PDF 格式。使用 Aspose.Cells for .NET，此过程不仅变得更加简单，而且更加灵活和强大。不再需要费力处理 Excel 的内置格式选项 - 现在您可以通过代码直接控制！

无论您要准备数据报告还是创建财务报表，利用 Aspose.Cells 的强大功能都会将您的电子表格游戏提升到一个全新的水平。那么，您还在等什么？满怀信心地投入您的项目，让您的数据大放异彩！

## 常见问题解答

### 什么是 Aspose.Cells？  
Aspose.Cells 是一个强大的.NET 库，允许开发人员以编程方式创建、操作和转换 Excel 文件。

### 我可以格式化其他类型的单元格吗？  
是的！您可以将不同的样式、格式甚至公式应用于工作表中的任何单元格。

### 有免费试用吗？  
当然可以！您可以免费试用[这里](https://releases.aspose.com/).

### 我可以将 Excel 文件保存为哪些格式？  
Aspose.Cells 支持多种格式，包括 XLSX、XLS、CSV、PDF 等。

### 在哪里可以找到更多支持？  
如果您需要帮助，请访问他们的[支持论坛](https://forum.aspose.com/c/cells/9)寻求社区和专家的帮助。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
