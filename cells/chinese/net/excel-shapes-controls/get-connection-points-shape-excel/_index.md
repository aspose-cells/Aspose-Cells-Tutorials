---
"description": "了解如何使用 Aspose.Cells for .NET 在 Excel 中获取形状连接点。按照我们的分步指南，轻松以编程方式提取和显示形状点。"
"linktitle": "在 Excel 中获取形状的连接点"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "在 Excel 中获取形状的连接点"
"url": "/zh/net/excel-shapes-controls/get-connection-points-shape-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中获取形状的连接点

## 介绍
在以编程方式处理 Excel 文件时，我们经常需要与工作表中嵌入的形状进行交互。您可以执行的一项更高级的任务是从形状中提取连接点。连接点用于将形状与连接器连接起来，并更精确地管理其布局。如果您想在 Excel 中获取形状的连接点，Aspose.Cells for .NET 就是您所需要的工具。在本教程中，我们将逐步指导您实现此目的。
## 先决条件
在深入研究代码之前，请确保您满足以下先决条件：
- Aspose.Cells for .NET：您需要在开发环境中安装 Aspose.Cells。如果您尚未安装，您可以 [点击此处下载最新版本](https://releases。aspose.com/cells/net/).
- 开发环境：确保您已安装 Visual Studio 或任何其他与 .NET 兼容的 IDE。
- C# 基础知识：本教程假设您对 C# 编程和面向对象原理有基本的了解。
您还可以注册 [Aspose.Cells 免费试用](https://releases.aspose.com/) 如果您还没有安装。这将使您能够访问本指南所需的所有功能。

## 导入包
为了在您的项目中使用 Aspose.Cells，您需要包含必要的命名空间。以下 import 语句应放在代码顶部：
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
这些命名空间让您可以访问 Aspose.Cells 的核心功能，并允许您操作工作表和形状。

## 获取形状连接点的分步指南
在本节中，我们将引导您了解如何在 Excel 工作表中提取形状的连接点。请仔细遵循每个步骤，以便清晰理解。
## 步骤 1：实例化新工作簿
首先，我们需要创建一个 `Workbook` 类。这代表 Aspose.Cells 中的一个 Excel 文件。如果您没有现有文件，没问题——您可以从一个空白工作簿开始。
```csharp
// 实例化新的工作簿
Workbook workbook = new Workbook();
```
在此步骤中，我们创建了一个空的 Excel 工作簿，但您也可以通过将文件路径传递给 `Workbook` 构造函数。
## 第 2 步：访问第一个工作表
接下来，我们需要访问要处理形状的工作表。在本例中，我们将使用工作簿的第一个工作表。
```csharp
// 获取工作簿中的第一个工作表
Worksheet worksheet = workbook.Worksheets[0];
```
此行代码用于访问工作簿中工作表集合中的第一个工作表。如果您正在使用特定工作表，则可以将索引替换为 `0` 使用所需的索引。
## 步骤 3：添加新文本框（形状）
现在，让我们在工作表中添加一个新形状。我们将创建一个文本框，它是一种形状。您也可以添加其他类型的形状，但为了简单起见，本教程中我们将使用文本框。
```csharp
// 向集合中添加新的文本框
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
以下是我们所做的工作：
- 在行中添加了文本框 `2`， 柱子 `1`。
- 将文本框的尺寸设置为 `160` 宽度单位和 `200` 高度单位。
## 步骤 4：从 Shapes 集合访问 Shape
添加文本框后，它将成为工作表形状集合的一部分。现在，我们将使用 `Shapes` 收藏。
```csharp
// 从形状集合访问形状（文本框）
Shape shape = workbook.Worksheets[0].Shapes[0];
```
在此步骤中，我们从集合中检索第一个形状（我们的文本框）。如果有多个形状，您可以指定索引，甚至可以通过名称查找形状。
## 步骤 5：检索连接点
现在我们有了形状，让我们提取它的连接点。这些点用于将连接器连接到形状。 `ConnectionPoints` 形状的属性返回所有可用的连接点。
```csharp
// 获取此形状中的所有连接点
var connectionPoints = shape.ConnectionPoints;
```
这为我们提供了该形状可用的所有连接点的集合。
## 步骤6：显示连接点
最后，我们要显示每个连接点的坐标。这里我们循环遍历连接点并将它们打印到控制台。
```csharp
// 显示所有形状点
foreach (var pt in connectionPoints)
{
    System.Console.WriteLine(string.Format("X = {0}, Y = {1}", pt.X, pt.Y));
}
```
此循环遍历每个连接点并打印 `X` 和 `Y` 坐标。这对于调试或直观地确认形状的连接点很有用。
## 步骤 7：执行并完成
完成上述所有步骤后，即可运行代码。以下是确保该过程成功完成的最后一行：
```csharp
System.Console.WriteLine("GetShapeConnectionPoints executed successfully.");
```
此行只是向控制台记录一条消息，表明该过程已完成。

## 结论
在本教程中，我们介绍了如何使用 Aspose.Cells for .NET 在 Excel 中检索形状的连接点。通过将任务分解为易于理解的小步骤，我们探索了创建工作簿、添加形状和提取连接点的过程。
通过了解如何以编程方式操作形状，您将开启构建动态交互式 Excel 工作表的无限可能。无论您是构建报表、设计仪表板还是创建图表，这些知识都将派上用场。
## 常见问题解答
### 形状中的连接点是什么？
连接点是形状上的特定点，您可以在此连接或将其链接到其他形状。
### 我可以检索工作表中所有形状的连接点吗？
是的，Aspose.Cells 允许您检索任何支持连接点的形状的连接点。只需循环遍历工作表中的形状集合即可。
### 我需要许可证才能使用 Aspose.Cells 吗？
是的，虽然您可以免费试用，但要使用完整功能则需要许可证。您可以 [在这里购买许可证](https://purchase.aspose.com/buy) 或者得到 [临时执照](https://purchase。aspose.com/temporary-license/).
### 如何在 Aspose.Cells 中添加不同类型的形状？
您可以使用 `Add` 适用于矩形、椭圆形等形状的方法。每个形状都有您可以自定义的特定参数。
### 如何加载现有的 Excel 文件而不是创建新文件？
要加载现有文件，请将文件路径传递给 `Workbook` 构造函数，如下所示：  
```csharp
Workbook workbook = new Workbook("path_to_file.xlsx");
```

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}