---
title: 在 .NET 中以编程方式创建新的数据透视表
linktitle: 在 .NET 中以编程方式创建新的数据透视表
second_title: Aspose.Cells .NET Excel 处理 API
description: 通过我们的分步指南，学习如何使用 Aspose.Cells 在 .NET 中以编程方式创建数据透视表。高效地分析您的数据。
weight: 13
url: /zh/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以编程方式创建新的数据透视表

## 介绍
创建数据透视表似乎是一项艰巨的任务，尤其是当您以编程方式执行时。但不要害怕！使用 Aspose.Cells for .NET，组合数据透视表不仅简单，而且对于数据分析也非常强大。在本教程中，我们将逐步指导您如何在 .NET 应用程序中创建新的数据透视表。无论您要添加销售、体育或任何其他业务指标的数据，本指南都将帮助您立即启动并运行数据透视表。

## 先决条件
在开始之前，让我们确保你已做好一切准备。以下是你需要做的事情：

1. 安装 .NET Framework：确保您的机器上安装了 .NET Framework。Aspose.Cells 支持各种版本，但最好使用最新版本。
2.  Aspose.Cells 库：您需要有 Aspose.Cells 库。您可以[点击下载](https://releases.aspose.com/cells/net/)或者得到[临时执照](https://purchase.aspose.com/temporary-license/)进行评估。
3. IDE 设置：准备好与 C# 兼容的 IDE，例如 Visual Studio，您可以在其中启动新项目。
4. C# 基础知识：熟悉 C# 编程将帮助您顺利完成课程而不会陷入困境。

一切就绪了吗？太棒了！让我们开始导入必要的包。

## 导入包
首先，您需要将所需的命名空间导入到您的 C# 项目中。打开您的 C# 文件并添加以下使用指令：

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

这些命名空间使您能够访问我们将在本教程中使用的工作簿、工作表和数据透视表功能。

## 步骤 1：创建工作簿对象
创建工作簿是您的旅程的开始。让我们从实例化一个新的工作簿并访问第一个工作表开始。

```csharp
//文档目录的路径。
string dataDir = "Your Document Directory";
//实例化 Workbook 对象
Workbook workbook = new Workbook();

//获取新添加工作表的引用
Worksheet sheet = workbook.Worksheets[0];
```

在此步骤中，我们创建一个`Workbook`代表我们的 Excel 文件的实例并获取第一个工作表，这将是我们的数据透视表的游乐场。

## 步骤 2：将数据插入单元格
接下来，让我们用一些示例数据填充工作表。我们将输入不同运动、季度和销售数据的行，以便我们的数据透视表可以汇总一些内容。

```csharp
Cells cells = sheet.Cells;

//将值设置为单元格
Cell cell = cells["A1"];
cell.PutValue("Sport");
cell = cells["B1"];
cell.PutValue("Quarter");
cell = cells["C1"];
cell.PutValue("Sales");

//填充数据单元 = 单元格["A2"];
cell.PutValue("Golf");
// ...更多数据条目
```

在这里，我们定义列标题并在每个标题下插入值。这些数据将作为数据透视表的来源，因此请确保其井然有序！按照此步骤操作，您将创建一个全面的数据集。

## 步骤 3：添加数据透视表
数据准备好后，就该创建数据透视表了。我们将使用工作表中的数据透视表集合来添加新的数据透视表。

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

//向工作表添加数据透视表
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

在此代码片段中，我们向工作表添加一个引用数据范围（在本例中为单元格 A1 至 C8）的数据透视表。我们将数据透视表放置在单元格 E3 的起始位置，并将其命名为“PivotTable2”。很简单，对吧？

## 步骤 4：自定义数据透视表
现在我们有了数据透视表，让我们对其进行自定义以显示有意义的摘要。我们可以控制数据透视表的行、列和数据区域中显示的内容。

```csharp
//访问新添加的数据透视表实例
Aspose.Cells.Pivot.PivotTable pivotTable = pivotTables[index];

//不显示各行总计。
pivotTable.RowGrand = false;

//将第一个字段拖拽至行区域。
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Row, 0);

//将第二个字段拖拽至列区域。
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Column, 1);

//将第三个字段拖拽至数据区域。
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Data, 2);
```

在此步骤中，我们告诉数据透视表隐藏行的总计，然后指定哪些字段进入行、列和数据区域。运动名称将填充行，季度将填充列，销售数字将提供摘要。

## 步骤 5：保存工作簿
最后，我们要保存新创建的工作簿来查看我们的劳动成果。

```csharp
//保存 Excel 文件
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

只需提供正确的路径，您就可以将数据透视表输出保存到可以打开和查看的 Excel 文件中。

## 结论
使用 Aspose.Cells for .NET 以编程方式创建数据透视表可以显著节省您的时间，尤其是在处理大型数据集时。您已经学习了如何设置项目、导入必要的包、填充数据以及从头开始创建可自定义的数据透视表。因此，下次您被数字淹没时，请记住本教程并让 Aspose.Cells 为您完成繁重的工作。

## 常见问题解答
### 什么是 Aspose.Cells？
Aspose.Cells 是一个功能强大的.NET 库，用于以编程方式创建和管理 Excel 电子表格。

### Aspose.Cells 有免费试用版吗？
是的，您可以免费试用[这里](https://releases.aspose.com/).

### 我可以自定义数据透视表的外观吗？
当然可以！您可以根据需要自定义数据透视表的格式、布局甚至样式。

### 在哪里可以找到有关 Aspose.Cells 的更多示例和文档？
您可以检查[文档](https://reference.aspose.com/cells/net/)以获得全面的指南和示例。

### 如何获得 Aspose.Cells 的支持？
您可以通过以下方式获得支持[Aspose 论坛](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
