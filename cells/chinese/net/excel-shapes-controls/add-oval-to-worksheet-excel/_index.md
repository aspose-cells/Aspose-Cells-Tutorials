---
"description": "学习如何使用 Aspose.Cells for .NET 在 Excel 工作表中添加椭圆形。分步指南，包含详细的代码解释。"
"linktitle": "在 Excel 中将椭圆形添加到工作表"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "在 Excel 中将椭圆形添加到工作表"
"url": "/zh/net/excel-shapes-controls/add-oval-to-worksheet-excel/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中将椭圆形添加到工作表

## 介绍
创建精美且交互式的 Excel 文件不仅仅涉及数字和公式。像椭圆这样的形状可以提升视觉吸引力，或为您的工作表提供实用元素。在本教程中，我们将探索如何使用 Aspose.Cells for .NET 以编程方式将椭圆添加到 Excel 工作表中。无论您是想添加一些功能还是增添一些新意，我们都会提供分步指南，帮助您轻松完成所有操作。
## 先决条件
在深入研究代码之前，您需要做好以下几点：
1. Aspose.Cells for .NET Library：您可以从 [这里](https://releases.aspose.com/cells/net/) 或者使用 Visual Studio 中的 NuGet 安装它。
2. 开发环境：类似 Visual Studio 的 C# IDE。
3. 对 C# 的基本了解：您应该熟悉 C# 中的基本编码概念。
另外，请务必安装 Aspose.Cells for .NET 库来设置您的项目。如果您还没有许可证，可以申请 [临时执照](https://purchase.aspose.com/temporary-license/) 或使用 [免费试用](https://releases.aspose.com/) 版本。
## 导入包
在编写任何代码之前，请确保已包含所需的命名空间。以下是 C# 代码片段，可确保您使用的是正确的库：
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## 步骤 1：设置目录
在 Excel 工作表中添加椭圆的第一步是指定 Excel 文件的保存位置。让我们先定义目录路径，并确保该目录在保存之前存在。

我们将创建一个目录路径并验证它是否存在。如果该文件夹不存在，则创建它。
```csharp
// 文档目录的路径。
string dataDir = "Your Document Directory";
// 如果目录尚不存在，则创建该目录。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
此步骤至关重要，因为它可以确保您的文件保存在正确的位置，并且您以后不会遇到文件路径问题。
## 步骤 2：初始化新工作簿
接下来，我们需要创建一个新的工作簿，在其中添加椭圆形。该工作簿代表一个 Excel 文件，我们可以在其中添加内容或形状。

在此步骤中，我们实例化一个新的 `Workbook` 该对象将作为我们的 Excel 文件容器。
```csharp
// 实例化一个新的工作簿。
Workbook excelbook = new Workbook();
```
## 步骤 3：添加第一个椭圆形
现在到了最有趣的部分——在工作表中添加一个椭圆形。这个椭圆形可以表示一个视觉元素，例如按钮或高亮显示。我们首先将第一个椭圆形添加到工作簿的第一个工作表中。

在这里，我们使用 `Shapes.AddOval()` 方法在工作表上的特定行和列创建椭圆。
```csharp
// 添加椭圆形。
Aspose.Cells.Drawing.Oval oval1 = excelbook.Worksheets[0].Shapes.AddOval(2, 0, 2, 0, 130, 160);
```
里面的参数 `AddOval()` 如下：
- 前两个数字代表椭圆左上角的行和列。
- 接下来的两个数字代表椭圆的高度和宽度。
## 步骤 4：设置椭圆的位置和样式
创建椭圆后，我们可以设置其位置、线宽和虚线样式。 `Placement` 属性决定了在工作表中调整大小或移动单元格时椭圆的行为方式。

我们使椭圆自由浮动并调整其外观。
```csharp
// 设置椭圆的位置。
oval1.Placement = PlacementType.FreeFloating;
// 设置线条粗细。
oval1.Line.Weight = 1;
// 设置椭圆的虚线样式。
oval1.Line.DashStyle = MsoLineDashStyle.Solid;
```
这使得椭圆可以在工作表内自由移动，并且其线条粗细和样式设置以实现视觉一致性。
## 步骤5：添加另一个椭圆（圆形）形状
为什么要止步于一个呢？在这一步中，我们将添加另一个椭圆形，这次通过使高度和宽度相同来创建一个完美的圆形。

我们创建另一个椭圆，将其放置在不同的位置，并通过设置相等的高度和宽度确保它具有圆形。
```csharp
// 添加另一个椭圆形（圆形）。
Aspose.Cells.Drawing.Oval oval2 = excelbook.Worksheets[0].Shapes.AddOval(9, 0, 2, 15, 130, 130);
```
## 步骤 6：设计第二个椭圆
就像以前一样，我们将调整第二个椭圆（或圆形）的位置、粗细和虚线样式。

我们将类似的属性应用于第二个椭圆，以匹配第一个椭圆的风格。
```csharp
// 设置椭圆的位置。
oval2.Placement = PlacementType.FreeFloating;
// 设置线条粗细。
oval2.Line.Weight = 1;
// 设置椭圆的虚线样式。
oval2.Line.DashStyle = MsoLineDashStyle.Solid;
```
## 步骤 7：保存工作簿
最后，我们需要保存包含刚刚添加的椭圆的工作簿。保存文件可以确保所有更改都已保存。

我们将工作簿保存到我们之前定义的目录路径。
```csharp
// 保存 Excel 文件。
excelbook.Save(dataDir + "book1.out.xls");
```
就这样！您已成功将椭圆添加到 Excel 工作表并保存了文件。
## 结论
使用 Aspose.Cells for .NET 在 Excel 工作表中添加椭圆等形状不仅简单易用，还能通过额外的视觉元素增强您的电子表格的趣味性。无论是出于设计目的还是添加可点击元素，形状都会对 Excel 文件的外观和功能产生重大影响。因此，下次您开展需要交互式或视觉吸引力强的 Excel 工作表的项目时，您就能知道如何添加这些完美的椭圆了！
## 常见问题解答
### 我可以使用 Aspose.Cells for .NET 添加其他形状，例如矩形或线条吗？
是的，你可以使用 `Shapes` Aspose.Cells 中的集合。
### 添加椭圆后可以调整其大小吗？
当然！添加椭圆后，您可以修改其高度和宽度属性。
### 除了 XLS 之外，我还可以将工作簿保存为哪些文件格式？
Aspose.Cells 支持多种格式，例如 XLSX、CSV 和 PDF 等。
### 我可以修改椭圆轮廓的颜色吗？
是的，你可以使用 `Line.Color` 财产。
### Aspose.Cells 需要许可证吗？
虽然您可以免费试用 Aspose.Cells，但您需要 [执照](https://purchase.aspose.com/buy) 适合长期使用或访问高级功能。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}