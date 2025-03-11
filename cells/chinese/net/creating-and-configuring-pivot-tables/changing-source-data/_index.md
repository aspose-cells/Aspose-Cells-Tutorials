---
title: 在 .NET 中以编程方式更改数据透视表的源数据
linktitle: 在 .NET 中以编程方式更改数据透视表的源数据
second_title: Aspose.Cells .NET Excel 处理 API
description: 通过我们全面的分步教程学习如何使用 Aspose.Cells for .NET 以编程方式更改数据透视表源数据。
weight: 10
url: /zh/net/creating-and-configuring-pivot-tables/changing-source-data/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以编程方式更改数据透视表的源数据

## 介绍
在数据分析领域，很少有工具能像 Microsoft Excel 一样耀眼。每天，无数用户都依赖 Excel 来管理和分析数据，但在幕后，它比单击和拖动要复杂得多。如果您曾经想以编程方式操作 Excel 文件（特别是更改数据透视表的源数据），那么您来对地方了！在本指南中，我们将探讨如何使用 Aspose.Cells for .NET 实现此目的。无论您是经验丰富的开发人员还是刚刚涉足编程领域，您都会发现本教程包含大量易于理解的宝贵信息。
## 先决条件
在我们开始更改数据透视表的源数据之前，让我们确保您已完成所有设置并准备就绪：
1. Visual Studio：确保您已安装 Microsoft Visual Studio 的副本，因为我们将在这里编写代码。
2. Aspose.Cells 库：您需要下载 Aspose.Cells 库并在项目中引用。您可以下载它[这里](https://releases.aspose.com/cells/net/).
3. C# 基础知识：虽然本教程比较简化，但掌握 C# 将有助于您更好地理解代码。
4. Excel 文件：您应该有一个示例 Excel 文件（如“Book1.xlsx”），其中包含我们可以操作的数据透视表。
好了，检查完这些先决条件后，我们可以继续导入必要的包并开始编码！
## 导入包
首先，让我们导入所需的包。在 Visual Studio 中打开您的 C# 项目，并在代码文件顶部添加以下使用指令：
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
这些命名空间将使您能够访问处理 Excel 文件和使用 Aspose.Cells 操作其内容所需的基本类。

现在，让我们将流程分解为易于管理的步骤。我们将逐步介绍如何打开 Excel 文件、修改工作表、更改数据透视表的数据源以及保存结果。
## 步骤 1：定义文档目录
首先，您需要指定 Excel 文件的位置。修改`dataDir`变量指向包含“Book1.xlsx”的文件夹。
```csharp
//文档目录的路径。
string dataDir = "Your Document Directory";
```
此行设置了存储 Excel 文件的目录，以便以后更容易访问。
## 步骤 2：指定输入路径
接下来，让我们创建一个字符串来指定输入 Excel 文件的完整路径：
```csharp
string InputPath = dataDir + "Book1.xlsx";
```
这有助于简化您的文件访问；您不必在整个代码中多次输入相同的路径。
## 步骤 3：创建文件流
现在是时候打开 Excel 文件了。我们将创建一个`FileStream`它可以让您读取 Excel 文件的内容：
```csharp
//创建包含要打开的 Excel 文件的文件流
FileStream fstream = new FileStream(InputPath, FileMode.Open);
```
此行以读取模式打开文件，允许我们访问其数据。
## 步骤 4：加载工作簿
有了文件流后，下一步就是加载工作簿：
```csharp
//通过文件流打开Excel文件
Workbook workbook = new Workbook(fstream);
```
此命令获取您的 Excel 文件并将其加载到`Workbook`对象。加载后，您可以根据需要操作该文件。
## 步骤 5：访问工作表
是时候深入了解细节了。我们将访问工作簿中的第一个工作表：
```csharp
//访问 Excel 文件中的第一个工作表
Worksheet worksheet = workbook.Worksheets[0];
```
这使您可以直接访问第一个工作表中的数据，从而轻松进行修改。
## 步骤 6：填充新数据
接下来，我们要将新数据插入单元格。在此示例中，我们将添加一些示例数据：
```csharp
//将新数据填充到工作表单元格
worksheet.Cells["A9"].PutValue("Golf");
worksheet.Cells["B9"].PutValue("Qtr4");
worksheet.Cells["C9"].PutValue(7000);
```
在这里，我们输入值“Golf”、“Qtr4”和`7000`到特定单元格中。您可以根据需要更改这些值。
## 步骤 7：更改命名范围
现在，我们将更改数据透视表引用的命名范围。这涉及创建或更新范围：
```csharp
//更改命名范围“DataSource”
Range range = worksheet.Cells.CreateRange(0,0,9,3);
range.Name = "DataSource";
```
通过定义新的范围，我们确保数据透视表在刷新时使用这些新数据。
## 步骤 8：保存修改后的 Excel 文件
完成所有更改后，保存您的工作至关重要！让我们保存修改后的工作簿：
```csharp
//保存修改后的 Excel 文件
workbook.Save(dataDir + "output.xls");
```
此命令将工作簿保存到新文件，因此除非您愿意，否则不会覆盖原始文件！
## 步骤 9：关闭文件流
最后，必须关闭文件流以释放您正在使用的任何资源：
```csharp
//关闭文件流以释放所有资源
fstream.Close();
```
此步骤可确保您的应用程序不会泄漏内存并保持高效。
## 结论
恭喜！您刚刚使用 Aspose.Cells 在 .NET 中以编程方式成功更改了数据透视表的源数据。此功能为自动化 Excel 任务和改进工作流程开辟了许多可能性。无论您是更新财务报告、跟踪销售数据，还是只是处理数据集，能够以编程方式执行此操作都可以为您节省大量时间并降低出错风险。

## 常见问题解答
### 什么是 Aspose.Cells？
Aspose.Cells 是一个功能强大的.NET 库，用于处理 Excel 文件，允许用户以编程方式创建、修改和操作 Excel 文档。
### 我可以使用此方法更改现有数据透视表的源数据吗？
当然可以！此方法允许您更新 Excel 工作簿中现有数据透视表的数据源。
### 我需要安装 Office 才能使用 Aspose.Cells 吗？
不！Aspose.Cells 是一个独立库，这意味着您不需要安装 Microsoft Office 即可处理 Excel 文件。
### Aspose.Cells 可以免费使用吗？
Aspose.Cells 提供免费试用版，但要获得完整功能，您必须购买许可证。您可以找到详细信息[这里](https://purchase.aspose.com/buy).
### 在哪里可以找到更多示例和支持？
如需更多示例和支持，请查看[Aspose.Cells 文档](https://reference.aspose.com/cells/net/)以及他们的社区论坛[这里](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
