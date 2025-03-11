---
title: 在输出 HTML 中单独导出工作表 CSS
linktitle: 在输出 HTML 中单独导出工作表 CSS
second_title: Aspose.Cells .NET Excel 处理 API
description: 在本全面的分步教程中学习如何使用 Aspose.Cells for .NET 将 Excel 工作表有效地导出为带有单独 CSS 的 HTML。
weight: 14
url: /zh/net/exporting-excel-to-html-with-advanced-options/exporting-worksheet-css-separately/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在输出 HTML 中单独导出工作表 CSS

## 介绍
在本指南中，您将学习如何将 Excel 工作表导出为 HTML，并特别关注单独导出 CSS。这不仅可以提高样式的可维护性，还可以提高工作流程效率。现在，让我们深入了解先决条件并开始动手吧！
## 先决条件
在我们开始编写代码之前，您需要完成以下工作以使本教程顺利进行：
1. Aspose.Cells for .NET 许可证：您需要许可证才能充分利用 Aspose.Cells 的功能。您可以[下载最新版本](https://releases.aspose.com/cells/net/)或者得到[临时执照](https://purchase.aspose.com/temporary-license/)如果你只是在试水。
2. 开发环境：理想情况下，您应该安装 Visual Studio 以便无缝运行您的 .NET 项目。
3. C# 基础知识：对 C# 编程有一点了解将有助于您更好地理解代码片段。
4. 参考文档：熟悉[Aspose.Cells 文档](https://reference.aspose.com/cells/net/)获得更多特性和能力。
一旦您满足了这些先决条件，我们就可以开始激动人心的部分了！
## 导入包
首先，您需要从 Aspose.Cells 导入相关的命名空间。设置方法如下：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Drawing;
```
此设置将为您提供创建工作簿、操作工作表和管理样式所需的所有工具。

让我们将其分解为易于管理的部分，每个步骤都使您更接近将生动的 Excel 工作表直接导出到 HTML 文件中的目标，并将所有 CSS 汁液分开！
## 步骤 1：设置输出目录
您需要做的第一件事就是决定要将导出的 HTML 文件保存在哪里。这至关重要，因为如果您做错了，您可能最终会到处寻找您的文档！
```csharp
string outputDir = "Your Document Directory";
```
只需更换`"Your Document Directory"`替换为要保存文件的路径。例如：`string outputDir = @"C:\MyExports\";`.
## 步骤 2：创建工作簿对象
接下来，我们需要创建一个新的工作簿对象。将工作簿视为空白画布，所有神奇的事情都在这里发生！
```csharp
Workbook wb = new Workbook();
```
通过这样做，我们初始化了 Workbook 类的一个新实例。此变量`wb`现在将保存我们的整个 Excel 工作表。
## 步骤 3：访问第一个工作表
现在是时候深入画布并获取第一个工作表了。这部分很简单，因为本教程只需要第一个工作表。
```csharp
Worksheet ws = wb.Worksheets[0];
```
此行获取工作簿中的第一个工作表，以供操作。
## 步骤 4：操作单元格的值
现在到了有趣的部分——让我们将一些数据放入单元格中！您可以选择任何单元格，但在本例中，我们将使用单元格“B5”。
```csharp
Cell cell = ws.Cells["B5"];
cell.PutValue("This is some text.");
```
通过此行，我们将文本“This is some text。”插入到单元格 B5 中。很简单，对吧？ 
## 步骤 5：设置单元格样式
让我们添加一点特色！我们将通过将字体颜色更改为红色来设置文本样式。 
```csharp
Style st = cell.GetStyle();
st.Font.Color = Color.Red;
cell.SetStyle(st);
```
此步骤将检索单元格 B5 的现有样式，将字体颜色更改为红色，然后重新应用新样式。现在您的单元格不再只是另一个纯文本框！
## 步骤 6：指定 HTML 保存选项
在此阶段，我们将准备 HTML 保存选项。这对于确保您的 CSS 单独导出至关重要。
```csharp
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.ExportWorksheetCSSSeparately = true;
```
随着`ExportWorksheetCSSSeparately`选项设置为 true，则告诉库以不同的方式处理 CSS 样式，而不是将它们直接嵌入到 HTML 文件中。
## 步骤 7：将工作簿保存为 HTML
最后，是时候保存所有辛苦的工作成果了！此行将您的工作簿作为 HTML 文件保存在指定的输出目录中。
```csharp
wb.Save(outputDir + "outputExportWorksheetCSSSeparately.html", opts);
```
在这里，我们命名我们的输出文件`outputExportWorksheetCSSSeparately.html`。瞧 — 您成功了！
## 步骤8：确认执行
为了确保一切顺利，输出确认消息总是很好的做法。
```csharp
Console.WriteLine("ExportWorksheetCSSSeparatelyInOutputHTML executed successfully.");
```
现在您可以运行代码，如果您看到确认消息，那么恭喜您 - 您已成功使用单独的 CSS 导出 Excel 工作表！
## 结论
以上就是 Aspose.Cells for .NET 提供的将 Excel 工作表导出为 HTML 并保持 CSS 独立的指南。这不仅可以让您的样式井然有序，还可以在将来需要进行更改时为您提供更大的灵活性。 
## 常见问题解答
### 什么是 Aspose.Cells？
Aspose.Cells 是一个功能强大的.NET 库，它允许您创建、修改和转换 Excel 电子表格，而无需 Microsoft Excel。
### 如何获得 Aspose.Cells 的免费试用版？
您可以从[Aspose.Cells 发布页面](https://releases.aspose.com/).
### 我可以进一步自定义 HTML 输出吗？
是的，Aspose.Cells 提供了各种选项来根据您的需要定制 HTML 输出。
### 是否可以使用 Aspose.Cells 操作其他工作表元素？
当然！Aspose.Cells 允许您操作电子表格中的图表、图像和许多其他元素。
### 在哪里可以找到其他资源？
查看[Aspose.Cells 文档](https://reference.aspose.com/cells/net/)以获取详细指南和 API 参考。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
