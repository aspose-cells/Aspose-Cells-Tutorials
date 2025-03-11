---
title: 在 Excel 中向工作表添加矩形控件
linktitle: 在 Excel 中向工作表添加矩形控件
second_title: Aspose.Cells .NET Excel 处理 API
description: 通过详细的分步指南了解如何使用 Aspose.Cells for .NET 向 Excel 工作表添加矩形控件。
weight: 25
url: /zh/net/excel-shapes-controls/add-rectangle-control-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中向工作表添加矩形控件

## 介绍
在自动化 Excel 任务方面，Aspose.Cells for .NET 是一款功能强大的工具，可以帮助您实现各种目标，其中之一就是向工作表添加矩形等形状。在本指南中，我们将探讨如何使用 Aspose.Cells for .NET 向 Excel 工作表添加矩形控件。最后，您将能够创建、自定义和保存嵌入矩形控件的工作表。
但在深入探讨之前，让我们先讨论一下先决条件。
## 先决条件
要继续本教程，请确保您已满足以下先决条件：
1.  Aspose.Cells for .NET 库：如果你还没有，[下载库](https://releases.aspose.com/cells/net/)或者使用 Visual Studio 中的 NuGet 安装它。
2. .NET Framework：您需要在您的机器上设置.NET 开发环境。
3. C# 基础知识：虽然我们会逐步指导您，但熟悉 C# 和面向对象编程的基本知识还是有益的。
4. 许可证：在评估模式下使用 Aspose.Cells 可以很好地完成基本任务，但要获得完整功能，请考虑获取[临时执照](https://purchase.aspose.com/temporary-license/)或从以下网站购买[这里](https://purchase.aspose.com/buy).
现在，让我们深入研究代码！
## 导入包
要开始使用 Aspose.Cells，请确保您已将必要的命名空间导入到项目中。这些导入将允许访问与 Excel 文件交互所需的各种类和方法。
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
这些行确保您的项目可以与文件目录进行交互（`System.IO`)、Excel 工作簿（`Aspose.Cells`）和形状绘制（`Aspose.Cells.Drawing`）。
现在，让我们将这个过程分解为简单的步骤，以便您可以轻松地跟随并在自己的项目中复制它。
## 步骤 1：设置目录路径
您需要做的第一件事是定义保存 Excel 文件的目录。此步骤可确保您的项目知道在哪里创建和存储输出文件。
### 定义数据目录
```csharp
//文档目录的路径。
string dataDir = "Your Document Directory";
```
在这里，您可以指定存储 Excel 文件的目录路径。您可以替换`"Your Document Directory"`使用您机器上的实际路径，如果不存在则动态创建一个文件夹。
### 检查并创建目录
```csharp
//如果目录尚不存在，则创建目录。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
此块检查目录是否存在。如果不存在，则创建一个。可以将其想象为在存储任何文档之前准备好文件柜。
## 步骤 2：实例化新工作簿
在此步骤中，您将使用`Aspose.Cells.Workbook`类。这将作为您的工作表和形状的容器。
```csharp
//实例化一个新的工作簿。
Workbook excelbook = new Workbook();
```
通过调用`Workbook`构造函数后，您现在有了一个可供自定义的空白 Excel 工作簿。
## 步骤 3：添加矩形控件
奇迹就在这里发生。您将在工作簿的第一个工作表中添加一个矩形。
```csharp
//添加一个矩形控件。
Aspose.Cells.Drawing.RectangleShape rectangle = excelbook.Worksheets[0].Shapes.AddRectangle(3, 0, 2, 0, 70, 130);
```
让我们详细分析一下：
- `excelbook.Worksheets[0]`：这将访问工作簿中的第一个工作表。
- `.Shapes.AddRectangle(3, 0, 2, 0, 70, 130)`：这会将矩形形状添加到工作表。此处的参数定义矩形的位置（行和列）以及宽度和高度。
## 步骤 4：自定义矩形
仅添加矩形是不够的，您需要对其进行自定义。在此步骤中，我们将设置矩形的位置、线宽和虚线样式。
### 设置位置
```csharp
//设置矩形的位置。
rectangle.Placement = PlacementType.FreeFloating;
```
这指定矩形是自由浮动的，这意味着它不会受到单元格尺寸的限制。
### 设置线宽
```csharp
//设置线条粗细。
rectangle.Line.Weight = 4;
```
这里我们设置矩形的线条粗细为4点，数字越大，线条越粗。
### 设置虚线样式
```csharp
//设置矩形的虚线样式。
rectangle.Line.DashStyle = MsoLineDashStyle.Solid;
```
此行将矩形边框的虚线样式设置为实线。您可以尝试不同的样式，例如`Dash`或者`Dot`取决于您的要求。
## 步骤 5：保存工作簿
添加并自定义矩形后，最后一步是将工作簿保存到指定的目录。
```csharp
//保存 Excel 文件。
excelbook.Save(dataDir + "book1.out.xls");
```
这会将工作簿保存为`.xls`文件位于您之前定义的文件夹中。您可以通过更改扩展名来修改文件格式，例如`.xlsx`如果您更喜欢较新的 Excel 格式。
## 结论
就这样！使用 Aspose.Cells for .NET 向 Excel 工作表添加矩形控件是一个简单的过程，只要您逐步分解即可。无论您需要添加形状以增加视觉吸引力、突出显示数据部分还是自定义报告，Aspose.Cells 都可以让您灵活地以编程方式进行操作。
本指南应该为您提供了使用 Aspose.Cells 向 Excel 表格添加矩形等形状所需的所有知识。现在是时候进行实验并看看您还可以使用这个强大的库实现什么！
## 常见问题解答
### 我可以使用 Aspose.Cells for .NET 添加圆形或线条等其他形状吗？  
是的，Aspose.Cells 允许您添加各种形状，包括圆形、线条、箭头等。
### 我可以为矩形控件设置哪些其他属性？  
您可以自定义填充颜色、线条颜色、透明度，甚至可以在矩形内添加文本。
### Aspose.Cells 与 .NET Core 兼容吗？  
是的，Aspose.Cells 支持.NET Core，以及.NET Framework 和其他基于.NET 的平台。
### 我可以相对于特定单元格定位矩形吗？  
是的，您可以将矩形放置在特定的行和列内，或者使用`PlacementType`来控制它如何锚定。
### Aspose.Cells 有免费试用版吗？  
是的，你可以得到一个[免费试用](https://releases.aspose.com/)从网站上测试图书馆的功能，然后再购买。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
