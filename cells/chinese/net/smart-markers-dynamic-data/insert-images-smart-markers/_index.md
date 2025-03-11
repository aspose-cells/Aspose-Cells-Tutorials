---
title: 在 Aspose.Cells 中插入带有图像标记的图像
linktitle: 在 Aspose.Cells 中插入带有图像标记的图像
second_title: Aspose.Cells .NET Excel 处理 API
description: 通过我们的分步指南了解如何在 Aspose.Cells for .NET 中使用图像标记插入图像！使用视觉效果有效地增强您的 Excel 报告。
weight: 16
url: /zh/net/smart-markers-dynamic-data/insert-images-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Aspose.Cells 中插入带有图像标记的图像

## 介绍
您是否想用一些图片来丰富您的 Excel 电子表格？也许您想创建一个包含来自数据源的直接图像的动态报告？如果是这样，您来对地方了！在本指南中，我们将介绍使用 .NET 的 Aspose.Cells 库中的图像标记插入图像的过程。本教程非常适合希望增强其 Excel 报告并提高整体用户参与度的 .NET 开发人员。
## 先决条件
在深入研究编码细节之前，必须确保已设置好以下几项：
1. .NET 环境：拥有一个可用的 .NET 开发环境。您可以使用 Visual Studio 或您选择的任何其他 .NET IDE。
2.  Aspose.Cells for .NET 库：您必须下载并有权访问 Aspose.Cells 库。您可以获取最新版本[这里](https://releases.aspose.com/cells/net/).
3. 所需图像：确保您计划使用的图像存储在项目目录中。
4. 对 C# 的基本了解：对 C# 和使用 DataTables 的基本了解将帮助您顺利跟进。
现在我们已经做好了准备，让我们开始导入必要的包吧！
## 导入包
在执行任何功能之前，我们需要导入必要的命名空间。在您的 C# 文件中，请确保已包含以下内容：
```csharp
using System.IO;
using Aspose.Cells;
using System.Data;
```
这些命名空间将为您提供操作 Excel 文件和处理数据表的类和功能。
现在，让我们将使用 Aspose.Cells 插入图像的过程分解为简单的步骤。我们将完成设置数据表、加载图像和保存最终 Excel 文件所需的步骤。
## 步骤 1：指定文档目录
首先，您需要指定图像和模板文件所在的文档目录。此目录将作为所有文件操作的基本路径。
```csharp
//文档目录的路径。
string dataDir = "Your Document Directory"; //将其更改为您的实际目录
```
代替`"Your Document Directory"`存储图像和模板文件的路径。这可以是相对路径或绝对路径。
## 第 2 步：将图像加载到字节数组中
接下来，我们将读取要插入 Excel 文件的图像。您需要创建一个 DataTable 来保存图像数据。
```csharp
//获取图像数据。
byte[] imageData = File.ReadAllBytes(dataDir + "aspose-logo.jpg");
```
这`File.ReadAllBytes()`方法用于将图像文件读入字节数组。您可以对每个文件重复此过程，以对多幅图像执行此操作。
## 步骤 3：创建数据表来保存图像
现在我们将创建一个 DataTable。该表将允许我们以结构化的方式存储图像数据。
```csharp
//创建数据表。
DataTable t = new DataTable("Table1");
//添加用于保存图片的列。
DataColumn dc = t.Columns.Add("Picture");
//设置其数据类型。
dc.DataType = typeof(object);
```
在这里，我们创建一个名为“Table1”的新数据表，并添加一个名为“Picture”的列。此列的数据类型设置为`object`，这对于存储字节数组是必需的。
## 步骤 4：将图像记录添加到数据表
一旦设置了 DataTable，我们就可以开始向其中添加图像。
```csharp
//向其中添加新记录。
DataRow row = t.NewRow();
row[0] = imageData;
t.Rows.Add(row);
//向其中添加另一条记录（包含图片）。
imageData = File.ReadAllBytes(dataDir + "image2.jpg");
row = t.NewRow();
row[0] = imageData;
t.Rows.Add(row);
```
为每个图像创建一个新行，并将第一列值设置为图像数据。使用`t.Rows.Add(row)`将行附加到 DataTable。这就是动态构建图像集合的方法。
## 步骤 5：创建 WorkbookDesigner 对象
接下来，是时候创建一个`WorkbookDesigner`对象，它将用于处理 Excel 模板。
```csharp
//创建 WorkbookDesigner 对象。
WorkbookDesigner designer = new WorkbookDesigner();
```
这`WorkbookDesigner`该课程可帮助您使用模板设计复杂的报告，从而让您更灵活地处理 Excel 文件。
## 步骤6：打开模板Excel文件
您必须将 Excel 模板文件加载到`WorkbookDesigner`。它是处理图像标记的基础。
```csharp
//打开模板 Excel 文件。
designer.Workbook = new Workbook(dataDir + "TestSmartMarkers.xlsx");
```
代替`"TestSmartMarkers.xlsx"`使用实际模板的名称。此文件应包含称为智能标记的占位符，用于告诉 Aspose.Cells 将图像数据放置在何处。
## 步骤 7：设置 WorkbookDesigner 的数据源
打开工作簿后，下一步是将 DataTable 连接到 WorkbookDesigner。
```csharp
//设置数据源。
designer.SetDataSource(t);
```
这一行告诉设计器使用您创建的 DataTable 作为数据源。它在图像数据和模板之间建立了链接。
## 步骤 8：处理模板中的标记
现在是时候让魔法发生了！我们将处理模板中的标记，用实际的图像数据替换占位符。
```csharp
//处理标记。
designer.Process();
```
这`Process()`方法扫描模板中的智能标记并使用 DataTable 中的数据填充它们。
## 步骤 9：保存最终 Excel 文件
最后一步当然是保存新创建的包含图像的 Excel 文件。现在就这样做吧！
```csharp
//保存 Excel 文件。
designer.Workbook.Save(dataDir + "output.xls");
```
您可以选择保存文件的首选格式。在本例中，我们将其保存为“output.xls”。根据您的要求修改文件名。
## 结论
就是这样！这是使用 Aspose.Cells 在图像标记的帮助下将图像插入 Excel 电子表格的精简指南。此功能对于创建包含基于数据源的图像的动态报告非常方便。无论您是在处理业务分析还是教育材料，这些方法都可以显著增强您的文档演示效果。
## 常见问题解答
### 什么是 Aspose.Cells？
Aspose.Cells 是一个强大的.NET 库，允许用户以编程方式创建、操作和转换 Excel 文件。
### 我可以免费使用 Aspose.Cells 吗？
是的！您可以免费试用 Aspose.Cells[这里](https://releases.aspose.com/).
### 在哪里可以了解有关使用 Aspose.Cells 的更多信息？
您可以深入研究[Aspose.Cells 文档](https://reference.aspose.com/cells/net/)获得丰富的指南和资源。
### 我是否需要许可证才能将 Aspose.Cells 与我的应用程序一起部署？
是的，对于生产用途，您需要许可证。您可以获取临时许可证[这里](https://purchase.aspose.com/temporary-license/).
### 如何获得 Aspose.Cells 的技术支持？
如有技术问题，您可以访问[Aspose 支持论坛](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
