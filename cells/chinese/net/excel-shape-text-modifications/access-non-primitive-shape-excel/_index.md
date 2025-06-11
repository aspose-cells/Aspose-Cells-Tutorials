---
"description": "学习如何使用 Aspose.Cells for .NET 在 Excel 中访问非原始形状。在本指南中探索循序渐进的方法。"
"linktitle": "在 Excel 中访问非原始形状"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "在 Excel 中访问非原始形状"
"url": "/zh/net/excel-shape-text-modifications/access-non-primitive-shape-excel/"
"weight": 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中访问非原始形状

## 介绍
您是否曾在 Excel 文件中偶然发现非原始形状，并想知道如何访问其中的复杂细节？如果您是一位使用 .NET 的开发人员，并且希望操作 Excel 工作表，那么您来对地方了！在本文中，我们将探讨如何使用 Aspose.Cells 库高效地访问和操作 Excel 中的非原始形状。我们将提供全面的分步指南，逐步讲解整个操作过程，即使您是该平台的新手也能轻松上手。所以，请安心学习，让我们一起探索 Aspose.Cells 的精彩世界！
## 先决条件
在我们进入代码之前，您需要满足一些先决条件：
1. C# 基础知识：熟悉 C# 编程语言对于顺利完成学习至关重要。
2. Visual Studio：你的机器上应该已经安装了 Visual Studio。我们将在这里编写代码。
3. Aspose.Cells 库：您需要安装 Aspose.Cells 库。您可以下载最新版本 [这里](https://releases。aspose.com/cells/net/).
4. Excel 文件：创建或获取包含非原始形状的 Excel 文件，用于测试。在本教程中，我们将使用 `"NonPrimitiveShape。xlsx"`.
一旦满足了这些先决条件，我们就可以进入有趣的部分了！
## 导入包
启动并运行一切的第一步是将必要的包导入到你的 C# 项目中。你需要执行以下操作：
### 创建新项目
- 打开 Visual Studio 并创建一个新的 C# 控制台应用程序项目。
- 为您的项目选择一个合适的名称，例如 `AsposeShapeAccess`。
### 安装 Aspose.Cells NuGet 包
- 在解决方案资源管理器中右键单击该项目。
- 选择“管理 NuGet 包”。
- 搜索 `Aspose.Cells` 并点击“安装”。
### 导入命名空间
在你的顶部 `Program.cs` 文件中，通过添加以下行导入 Aspose.Cells 命名空间：
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Collections;
using System;
```
现在，让我们深入研究实际的代码，我们将访问 Excel 文件中的非原始形状。
## 步骤 1：设置文档路径
在访问形状之前，我们需要指定 Excel 文件所在的目录。操作方法如下：
```csharp
string dataDir = "Your Document Directory";
```
代替 `"Your Document Directory"` 实际路径 `NonPrimitiveShape.xlsx` 文件已存储。 
## 第 2 步：加载工作簿
现在我们已经设置好了文档路径，接下来就可以加载工作簿了。操作方法如下：
```csharp
Workbook workbook = new Workbook(dataDir + "NonPrimitiveShape.xlsx");
```
这行创建了一个新的 `Workbook` 对象，它读取您之前指定的 Excel 文件。
## 步骤 3：访问工作表
接下来，我们将访问工作簿中的第一个工作表。让我们这样做：
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
此行访问工作簿中的第一个工作表 - 当我们将注意力限制在一次一张工作表上时，Excel 的效果最佳。
## 步骤 4：访问用户定义形状
现在到了激动人心的部分！我们将在工作表中访问用户定义的形状（可能是非原始的）。
```csharp
Shape shape = worksheet.Shapes[0];
```
这里，我们访问的是工作表中的第一个形状。如果有多个形状，您可以更改索引。
## 步骤 5：检查形状是否为非原始形状
在继续访问其详细信息之前，确认形状是否为非原始形状至关重要：
```csharp
if (shape.AutoShapeType == AutoShapeType.NotPrimitive)
{
```
这个块确保我们只处理具有更复杂细节的形状。
## 步骤 6：访问形状的数据
现在我们已经确认它是一个非原始形状，我们就可以访问它的数据。
```csharp
ShapePathCollection shapePathCollection = shape.Paths;
```
这行代码获取了定义形状的路径集合。你可以把它想象成获取形状设计的蓝图！
## 步骤 7：循环遍历每条路径
为了更深入地了解形状的结构，我们将循环遍历与形状相关的每条路径：
```csharp
foreach (ShapePath shapePath in shapePathCollection)
{
```
这个循环将使我们能够深入研究每条路径并探索其细节。
## 步骤 8：访问路径段
每个形状路径可以包含多个段。让我们来访问它们！
```csharp
ShapeSegmentPathCollection pathSegments = shapePath.PathSegementList;
```
该集合包含组成形状路径的段。
## 步骤 9：循环遍历每个路径段
在这里，我们将循环遍历路径段集合中的每个段：
```csharp
foreach (ShapeSegmentPath pathSegment in pathSegments)
{
```
有趣的部分从这里开始，因为我们将深入探讨每个部分的细节！
## 步骤10：访问路径段点
现在，让我们了解每个路径段中的各个点：
```csharp
ShapePathPointCollection segmentPoints = pathSegment.Points;
```
可以将其视为收集定义形状的曲线和角的所有坐标。
## 步骤11：打印点详细信息
最后，让我们将路径段中每个点的详细信息打印到控制台：
```csharp
foreach (ShapePathPoint pathPoint in segmentPoints)
{
    Console.WriteLine("X: " + pathPoint.X + ", Y: " + pathPoint.Y);
}
```
通过这种方式，我们可以有效地输出定义非原始形状的每个点的坐标——这是一种可视化底层发生的事情的奇妙方法！
## 结论
就这样！您已经成功使用 Aspose.Cells for .NET 访问并探索了 Excel 中非原始形状的细节。这个强大的库为操作 Excel 文件开辟了无限可能，无论您是生成报告、创建动态电子表格还是处理复杂形状。如果您有任何疑问或需要进一步的帮助，请随时联系我们！
## 常见问题解答
### Excel 中的非原始形状是什么？
非原始形状是由多个线段和曲线组成的复杂形状，而不是简单的几何形状。
### 如何安装 Aspose.Cells for .NET？
您可以通过 Visual Studio 中的 NuGet 包管理器安装它，或者从他们的网站下载它 [地点](https://releases。aspose.com/cells/net/).
### 我可以免费使用 Aspose.Cells 吗？
是的，您可以从他们的网站获取免费试用版来探索其功能 [这里](https://releases。aspose.com/).
### 使用 Aspose.Cells 有什么好处？
Aspose.Cells 提供了强大的功能，可以通过编程方式操作 Excel 电子表格，而无需在您的机器上安装 Excel。
### 在哪里可以找到对 Aspose.Cells 的支持？
您可以从 Aspose 社区论坛获得帮助和支持 [这里](https://forum。aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}