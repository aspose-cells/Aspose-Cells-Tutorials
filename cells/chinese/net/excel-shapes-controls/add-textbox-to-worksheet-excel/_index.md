---
"description": "在本分步教程中了解如何使用 Aspose.Cells for .NET 向 Excel 添加可自定义的文本框。"
"linktitle": "在 Excel 中向工作表添加文本框"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "在 Excel 中向工作表添加文本框"
"url": "/zh/net/excel-shapes-controls/add-textbox-to-worksheet-excel/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中向工作表添加文本框

## 介绍
您是否渴望用独特的视觉效果增强您的 Excel 电子表格，从而吸引受众？添加文本框是实现这一目标的绝佳方法！使用 Aspose.Cells for .NET，您可以轻松地将文本框集成到您的 Excel 工作表中，使您的文档更具信息量和视觉吸引力。本分步指南将引导您完成使用 Aspose.Cells 添加文本框的简单过程，并展示如何使用文本、颜色、超链接等个性化设置文本框！
## 先决条件
在我们深入研究编码奇迹之前，以下是确保顺利航行体验的基本先决条件：
1. .NET 开发环境：您需要一个可运行的 .NET 框架以及像 Visual Studio 这样的 IDE。请确保它已更新到最新版本！
2. Aspose.Cells for .NET：请确保您已下载 Aspose.Cells 库。您可以从以下位置获取最新版本 [这里](https://releases。aspose.com/cells/net/).
3. 基本编程知识：熟悉 C# 和一些处理 Excel 文件的一般概念将使本教程更容易！
## 导入包
确保在 C# 文件的开头导入必要的包。具体操作如下：
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## 安装 Aspose.Cells
如果您还没有这样做，您可以通过 Visual Studio 中的 NuGet 包管理器添加 Aspose.Cells：
1. 打开 Visual Studio。
2. 前往 `Tools` -> `NuGet Package Manager` -> `Manage NuGet Packages for Solution`。
3. 搜索“Aspose.Cells”并将其安装到您的项目中。
现在我们已经打好了基础，让我们进入有趣的部分吧！
## 步骤 1：设置文档目录
首先，让我们设置存储所有 Excel 文档的目录。在开始创建工作簿之前，必须确保该目录存在。
```csharp
// 文档目录的路径。
string dataDir = "Your Document Directory"; 
// 如果目录尚不存在，则创建该目录。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists) 
    System.IO.Directory.CreateDirectory(dataDir);
```
此代码片段将创建一个名为 `Your Document Directory` （如果不存在，请用你的实际路径替换）。很简单，对吧？
## 步骤 2：实例化新工作簿
接下来，我们需要创建一个新的工作簿，用于添加文本框。只需几行代码即可轻松完成：
```csharp
// 实例化一个新的工作簿。
Workbook workbook = new Workbook();
```
这行代码创建了一个新的 Excel 工作簿。简单又直接！
## 步骤 3：访问第一个工作表
现在我们已经准备好工作簿，让我们获取第一个工作表，在其中添加文本框：
```csharp
// 获取书中的第一个工作表。
Worksheet worksheet = workbook.Worksheets[0];
```
就这样，您现在可以访问名为 `worksheet`。是时候让它闪耀光芒了！
## 步骤 4：添加文本框
好了，现在该添加我们的第一个文本框了！操作方法如下：
```csharp
// 向集合中添加一个新的文本框。
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
在这一行中，我们指定了文本框所在的行和列，以及它的宽度和高度（分别为 160 和 200）。您可以根据您的布局随意调整这些数字！
## 步骤5：获取TextBox对象
添加文本框后，我们需要获取对它的引用，以便我们可以自定义其内容：
```csharp
// 获取文本框对象。
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[textboxIndex];
```
现在， `textbox0` 是您修改此文本框的黄金门票！
## 步骤6：用内容填充文本框
接下来，让我们为文本框提供一些文本：
```csharp
// 填充文本。
textbox0.Text = "ASPOSE______The .NET & JAVA Component Publisher!";
```
将文本插入文本框就是这么简单！ 
## 步骤 7：自定义文本框外观
我们来美化一下怎么样？你可以调整字体颜色、样式等等！
```csharp
// 设置字体颜色。
textbox0.Font.Color = Color.Blue;
// 将字体设置为粗体。
textbox0.Font.IsBold = true;
// 设置字体大小。
textbox0.Font.Size = 14;
// 将字体属性设置为斜体。
textbox0.Font.IsItalic = true;
```
随意尝试不同的颜色和风格，看看哪种视觉效果最好！
## 步骤8：添加超链接
想要将文本框变成可点击的链接吗？让我们来做吧：
```csharp
// 向文本框添加超链接。
textbox0.AddHyperlink("http://www.aspose.com/”);
```
现在，任何人点击你的文本框都会被带到 Aspose 网站。简直太神奇了！
## 步骤9：设置文本框放置类型
您可以选择不同的方式设置文本框在工作表中的显示方式。以下是如何将其设置为自由浮动的示例：
```csharp
// 设置位置。
textbox0.Placement = PlacementType.FreeFloating;
```
或者，如果您希望它调整大小并随单元格移动，您可以像这样设置：
```csharp
// 设置放置类型，因为文本框将随单元格移动并调整大小。
textbox1.Placement = PlacementType.MoveAndSize;
```
## 步骤10：自定义线条和填充格式
您可以通过以下方式更改文本框边框和填充的外观：
```csharp
// 获取文本框的填充格式。
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;            
// 获取文本框的行格式类型。
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;           
// 设置线条粗细。
lineformat.Weight = 6;
// 将虚线样式设置为方点。
lineformat.DashStyle = MsoLineDashStyle.SquareDot;
```
通过它，您可以进一步自定义文本框，添加适合您风格的视觉效果。
## 步骤11：添加另一个文本框
没人说我们只能添加一个文本框！让我们添加另一个文本框，并添加一些不同的文本：
```csharp
// 添加另一个文本框。
textboxIndex = worksheet.TextBoxes.Add(15, 4, 85, 120);
// 获取第二个文本框。
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[textboxIndex];
// 输入一些文本。
textbox1.Text = "This is another simple text box";
```
现在，您确实可以使用多个文本框来使您的 Excel 工作表更加生动有趣！
## 步骤12：保存工作簿
最后，是时候保存我们的杰作了！这是今天的最后一行代码：
```csharp
// 保存 Excel 文件。
workbook.Save(dataDir + "book1.out.xls");
```
只需这一行代码，您就创建并修改了一个带有可自定义文本框的 Excel 文件！
## 结论
恭喜！您已成功使用 Aspose.Cells for .NET 探索 Excel 中的文本框世界。您不仅学习了如何添加文本框，还学会了如何自定义文本框，让您的电子表格更具吸引力。从更改颜色和样式到添加超链接，可能性几乎无穷无尽！ 
准备好开始改造你的 Excel 文档了吗？发挥你的创造力，尝试不同的布局！
## 常见问题解答
### 什么是 Aspose.Cells for .NET？
Aspose.Cells for .NET 是一个功能强大的库，允许开发人员轻松地创建、操作和转换 Excel 文件。
### 我可以在购买之前试用 Aspose.Cells 吗？
是的！您可以下载并使用免费试用版 [这里](https://releases。aspose.com/).
### 在哪里可以找到 Aspose.Cells 的文档？
您可以在以下位置访问综合文档 [Aspose.Cells文档](https://reference。aspose.com/cells/net/).
### 如果我遇到问题，可以获得支持吗？
当然！如果你需要帮助，可以前往 [Aspose 论坛](https://forum.aspose.com/c/cells/9) 寻求帮助。
### 我可以在没有许可证的情况下使用 Aspose.Cells 吗？
虽然您可以使用免费试用版，但要访问完整功能，则需要购买许可证。查看价格 [这里](https://purchase。aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}