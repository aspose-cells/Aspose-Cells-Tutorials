---
title: 添加带连接点的弧形控制
linktitle: 添加带连接点的弧形控制
second_title: Aspose.Cells .NET Excel 处理 API
description: 在此详细指南中了解如何使用 Aspose.Cells for .NET 添加带有连接点的弧形控件。
weight: 27
url: /zh/net/excel-shapes-controls/add-arc-control-with-connection-points/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 添加带连接点的弧形控制

## 介绍
在创建具有视觉吸引力的 Excel 报告时，插图起着至关重要的作用。无论您是在制作财务报告还是项目细分，使用弧线等形状都可以为您的数据呈现增加深度和清晰度。今天，我们将深入探讨如何利用 Aspose.Cells for .NET 在 Excel 工作表中添加带有连接点的弧线控件。因此，如果您想知道如何为电子表格增添趣味或让数据更生动，请继续阅读！
## 先决条件
在我们开始激动人心的编码之前，让我们确保您已做好一切准备。以下是您需要的内容：
1. .NET Framework：确保您已安装兼容版本。Aspose.Cells 适用于多个版本，包括 .NET Core。
2.  Aspose.Cells for .NET：您需要下载并安装 Aspose.Cells 库。您可以从[下载链接](https://releases.aspose.com/cells/net/).
3. 一个好的 IDE：Visual Studio，任何 .NET 开发人员的忠实伴侣，将有助于简化您的编码体验。
4. C# 基础知识：如果您熟悉 C#，您会发现本教程很顺利。
5. 访问您的文档目录：了解您将在哪里保存您的 Excel 文件。这对于有效地组织您的输出至关重要。
## 导入包
下一步是确保将正确的包导入到项目中。Aspose.Cells for .NET 具有多种功能，因此我们将尽量简化。以下是您需要包含的内容：
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
这些命名空间将使您能够访问本指南中使用的所有绘图功能和单元格管理功能。
## 步骤 1：设置文档目录
首先，让我们建立一个目录来保存这些崭新的 Excel 文件。操作方法如下：
```csharp
string dataDir = "Your Document Directory";
//如果目录尚不存在，则创建目录。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
这段代码检查您指定的文件夹是否存在。如果不存在，则创建一个。很简单，对吧？将文件放在特定位置以避免混乱总是好的。
## 步骤 2：实例化工作簿
现在我们已经准备好目录，让我们创建一个新的 Excel 工作簿。
```csharp
Workbook excelbook = new Workbook();
```
通过调用`Workbook`构造函数，你实际上是在说，“嘿，让我们开始一个新的 Excel 文件！”这将成为你所有形状和数据的画布。
## 步骤 3：添加第一个圆弧形状
乐趣就从这里开始！让我们添加第一个圆弧形状。
```csharp
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
这行代码将圆弧形状添加到第一个工作表。参数指定圆弧的坐标和定义其曲率的角度。 
## 步骤 4：自定义弧线的外观
空白的弧形就像没有油漆的画布——它需要一点天赋！
### 设置弧形填充颜色
```csharp
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
```
这使得弧线呈纯蓝色。你可以将颜色更改为你喜欢的任何色调，只需换出`Color.Blue`另一种颜色。
### 设置圆弧位置
```csharp
arc1.Placement = PlacementType.FreeFloating;
```
将位置设置为“FreeFloating”可使弧线独立于单元格边界移动，让您可以灵活地定位。
### 调整线条粗细和样式
```csharp
arc1.Line.Weight = 1;      
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
在这里，您可以定义线条的粗细和样式，使其更加突出和更具视觉吸引力。
## 步骤 5：添加另一个圆弧形状
为什么要止步于此？让我们添加另一个弧形来丰富我们的 Excel 视觉效果。
```csharp
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
与第一个圆弧一样，这个圆弧也添加在不同的位置——这就是设计的魔力所在！
## 步骤 6：自定义第二条弧线
让我们的第二篇章也具有一些个性吧！
### 改变弧线颜色
```csharp
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
```
我们将其与蓝色保持一致，但您可以随时混合搭配，以找到最适合您的设计的颜色！
### 设置与第一个圆弧相似的属性
确保复制这些美学选择：
```csharp
arc2.Placement = PlacementType.FreeFloating;
arc2.Line.Weight = 1;           
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
在这里，您只需确保第二个圆弧与第一个圆弧相匹配，从而在整个工作表中创建一个有凝聚力的外观。
## 步骤 7：保存工作簿
杰作若不保存，就不算完整，对吧？是时候将您的弧线写入 Excel 文件了。
```csharp
excelbook.Save(dataDir + "book1.out.xls");
```
此行将您新创建的弧保存到指定目录中名为“book1.out.xls”的 Excel 文件中。
## 结论
恭喜！您刚刚掌握了使用 Aspose.Cells for .NET 在 Excel 表中添加带有连接点的弧形控件的基础知识。此功能不仅可以美化您的电子表格，还可以使复杂的数据更易于理解。无论您是经验丰富的开发人员还是刚刚起步，这些视觉元素都可以将您的报告从平淡无奇变为宏伟壮观。
## 常见问题解答
### 什么是 Aspose.Cells？
Aspose.Cells 是一个功能强大的.NET 库，允许开发人员以编程方式创建和操作 Excel 文件。
### 我可以免费使用 Aspose.Cells 吗？
是的！您可以免费试用。访问[此链接](https://releases.aspose.com/)开始。
### 除了弧线以外，如何添加其他形状？
您可以使用 Aspose.Cells.Drawing 命名空间中提供的不同类来添加各种形状，如矩形、圆形等。
### 我可以使用 Aspose.Cells 创建什么类型的文件？
您可以创建和操作各种 Excel 格式，包括 XLS、XLSX、CSV 等。
### Aspose.Cells 提供技术支持吗？
当然！您可以访问[Aspose 支持论坛](https://forum.aspose.com/c/cells/9)寻求帮助。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
