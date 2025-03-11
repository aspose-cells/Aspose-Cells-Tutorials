---
title: 在 Excel 中向工作表添加文本框
linktitle: 在 Excel 中向工作表添加文本框
second_title: Aspose.Cells .NET Excel 处理 API
description: 在本分步教程中了解如何使用 Aspose.Cells for .NET 向 Excel 添加可自定义的文本框。
weight: 14
url: /zh/net/excel-shapes-controls/add-textbox-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中向工作表添加文本框

## 介绍
您是否渴望通过独特的视觉效果增强您的 Excel 电子表格，以吸引您的受众？添加文本框是实现此目标的好方法！使用 Aspose.Cells for .NET，您可以轻松地将文本框集成到您的 Excel 工作表中，使您的文档更具信息性和视觉吸引力。本分步指南将引导您完成使用 Aspose.Cells 添加文本框的简单过程，展示如何使用文本、颜色、超链接等对其进行个性化设置！
## 先决条件
在我们深入研究编码奇迹之前，以下是确保顺利完成体验的基本先决条件：
1. .NET 开发环境：您需要一个可运行的 .NET 框架以及 Visual Studio 之类的 IDE。确保它已更新到最新版本！
2.  Aspose.Cells for .NET：确保已下载 Aspose.Cells 库。你可以从以下网址获取最新版本[这里](https://releases.aspose.com/cells/net/).
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
2. 转至`Tools` ->`NuGet Package Manager` ->`Manage NuGet Packages for Solution`.
3. 搜索“Aspose.Cells”并将其安装到您的项目中。
现在我们已经打好了基础，让我们进入有趣的部分吧！
## 步骤 1：设置文档目录
首先，让我们设置存储所有 Excel 文档的目录。在开始创建工作簿之前，必须确保此目录存在。
```csharp
//文档目录的路径。
string dataDir = "Your Document Directory"; 
//如果目录尚不存在，则创建目录。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists) 
    System.IO.Directory.CreateDirectory(dataDir);
```
此代码片段将创建一个名为`Your Document Directory`（如果不存在，请用您的实际路径替换它）。很简单，对吧？
## 步骤 2：实例化新工作簿
接下来，我们需要创建一个新的工作簿，在其中添加文本框。只需几行代码即可轻松完成：
```csharp
//实例化一个新的工作簿。
Workbook workbook = new Workbook();
```
这行代码创建一个新的 Excel 工作簿。简单明了！
## 步骤 3：访问第一个工作表
现在我们已经准备好工作簿，让我们获取第一个工作表，在其中添加文本框：
```csharp
//获取书中的第一个工作表。
Worksheet worksheet = workbook.Worksheets[0];
```
就这样，你现在可以访问名为`worksheet`。是时候让它闪耀光芒了！
## 步骤 4：添加文本框
好了，现在该添加我们的第一个文本框了！操作方法如下：
```csharp
//向集合中添加新的文本框。
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
在这一行中，我们指定文本框所在的行和列，并设置其宽度和高度（分别为 160 和 200）。您可以根据您的布局随意调整这些数字！
## 步骤5：获取 TextBox 对象
添加文本框后，我们需要获取对它的引用，以便我们可以自定义其内容：
```csharp
//获取文本框对象。
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[textboxIndex];
```
现在，`textbox0`是您修改此文本框的黄金门票！
## 步骤6：用内容填充文本框
接下来，让我们为文本框提供一些文本：
```csharp
//填充文本。
textbox0.Text = "ASPOSE______The .NET & JAVA Component Publisher!";
```
在文本框中插入文本就是这么简单！ 
## 步骤 7：自定义文本框外观
我们来美化一下怎么样？您可以调整字体颜色、样式等等！
```csharp
//设置字体颜色。
textbox0.Font.Color = Color.Blue;
//将字体设置为粗体。
textbox0.Font.IsBold = true;
//设置字体大小。
textbox0.Font.Size = 14;
//将字体属性设置为斜体。
textbox0.Font.IsItalic = true;
```
随意尝试不同的颜色和风格，看看哪种视觉效果最好！
## 步骤 8：添加超链接
想要将文本框变成可点击的链接吗？让我们来做吧：
```csharp
//向文本框添加超链接。
textbox0.AddHyperlink("http://www.aspose.com/”);
```
现在，任何人点击您的文本框都会被带到 Aspose 网站。这就像魔术一样！
## 步骤 9：设置文本框放置类型
您可以根据工作表的不同选择文本框的行为方式。以下是如何将其设置为自由浮动的示例：
```csharp
//设置位置。
textbox0.Placement = PlacementType.FreeFloating;
```
或者，如果您希望它调整大小并随单元格移动，您可以像这样设置：
```csharp
//设置放置类型，因为文本框将随单元格移动并调整大小。
textbox1.Placement = PlacementType.MoveAndSize;
```
## 步骤 10：自定义线条和填充格式
您可以通过以下方法更改文本框边框和填充的外观：
```csharp
//获取文本框的填充格式。
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;            
//获取文本框的行格式类型。
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;           
//设置线条粗细。
lineformat.Weight = 6;
//将虚线样式设置为方点。
lineformat.DashStyle = MsoLineDashStyle.SquareDot;
```
通过它，您可以进一步自定义文本框，添加适合您风格的视觉效果。
## 步骤11：添加另一个文本框
没人说我们只能添加一个文本框！让我们再添加一个，并添加一些不同的文本：
```csharp
//添加另一个文本框。
textboxIndex = worksheet.TextBoxes.Add(15, 4, 85, 120);
//获取第二个文本框。
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[textboxIndex];
//输入一些文本。
textbox1.Text = "This is another simple text box";
```
现在您真的可以使用多个文本框来使您的 Excel 工作表变得更加有趣了！
## 步骤 12：保存工作簿
最后，是时候保存我们的杰作了！这是今天的最后一行代码：
```csharp
//保存 Excel 文件。
workbook.Save(dataDir + "book1.out.xls");
```
仅用这一行代码，您就创建并修改了一个带有可自定义文本框的 Excel 文件！
## 结论
恭喜！您已成功使用 Aspose.Cells for .NET 浏览 Excel 中的文本框世界。您不仅学会了如何添加文本框，还学会了如何自定义文本框以使您的电子表格更具吸引力。从更改颜色和样式到添加超链接，可能性几乎无穷无尽！ 
您准备好开始转换 Excel 文档了吗？发挥您的创造力，尝试不同的布局！
## 常见问题解答
### 什么是 Aspose.Cells for .NET？
Aspose.Cells for .NET 是一个功能强大的库，允许开发人员毫不费力地创建、操作和转换 Excel 文件。
### 我可以在购买之前试用 Aspose.Cells 吗？
是的！您可以下载并使用免费试用版[这里](https://releases.aspose.com/).
### 在哪里可以找到 Aspose.Cells 的文档？
您可以访问以下网址获取全面的文档[Aspose.Cells 文档](https://reference.aspose.com/cells/net/).
### 如果我遇到问题，可以获得支持吗？
当然！如果您需要帮助，请前往[Aspose 论坛](https://forum.aspose.com/c/cells/9)寻求帮助。
### 我可以在没有许可证的情况下使用 Aspose.Cells 吗？
虽然您可以使用免费试用版，但要访问完整功能，您需要购买许可证。查看定价[这里](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
