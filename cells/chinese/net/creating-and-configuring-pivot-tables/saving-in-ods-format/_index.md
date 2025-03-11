---
title: 在 .NET 中以编程方式将数据透视表保存为 ODS 格式
linktitle: 在 .NET 中以编程方式将数据透视表保存为 ODS 格式
second_title: Aspose.Cells .NET Excel 处理 API
description: 通过本分步指南了解如何使用 Aspose.Cells for .NET 以 ODS 格式保存数据透视表。
weight: 25
url: /zh/net/creating-and-configuring-pivot-tables/saving-in-ods-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以编程方式将数据透视表保存为 ODS 格式

## 介绍
在管理电子表格中的数据时，没有什么能比得上数据透视表的强大功能。它们是汇总、分析和呈现复杂数据集的首选工具。今天，我们将深入研究如何使用 Aspose.Cells for .NET 以 ODS 格式保存数据透视表。无论您是经验丰富的开发人员还是刚刚接触 .NET，您都会发现本指南非常简单易懂。 
让我们开始吧！
## 先决条件
在我们进入代码之前，您需要满足一些基本要求：
### 1. .NET 基础知识
对.NET 及其编程概念有基本的了解将有助于您轻松地跟上进度。
### 2.适用于 .NET 的 Aspose.Cells
您需要安装 Aspose.Cells for .NET。您可以从[Aspose 发布页面](https://releases.aspose.com/cells/net/) 还提供试用版[这里](https://releases.aspose.com/).
### 3. 开发环境
确保您有一个像 Visual Studio 这样的 IDE，您可以在其中编写和测试您的 .NET 代码。
### 4. 一点耐心
和任何编码工作一样，耐心是关键。如果第一次没有完美运行，请不要担心；调试是过程的一部分。
## 导入包
要使用 Aspose.Cells，您需要导入必要的命名空间。在代码文件的开头添加以下 using 指令：
```csharp
using System;
using Aspose.Cells.Pivot;
```
此行允许您访问 Aspose.Cells 库中的所有功能，使您的编码过程变得轻而易举。
现在，让我们将这个过程分解为易于管理的步骤。
## 步骤 1：设置输出目录
首先，您需要定义要保存 ODS 文件的位置。这是一个简单的目录路径分配。
```csharp
string outputDir = "Your Document Directory";
```
在这一行中，替换`"Your Document Directory"`使用您想要保存文件的路径。
## 步骤 2：创建新工作簿
接下来，您将实例化一个新的 Workbook 对象，它将保存您的所有数据和结构，包括数据透视表。
```csharp
Workbook workbook = new Workbook();
```
在这里，您基本上是从头开始 - 将其视为一块空白画布，您可以在其中创作自己的杰作。
## 步骤 3：访问工作表
现在我们有了工作簿，我们需要开始处理工作表。Aspose.Cells 允许您轻松访问第一个可用的工作表。
```csharp
Worksheet sheet = workbook.Worksheets[0];
```
这行代码将带我们进入第一张表，准备输入数据。
## 步骤 4：用数据填充单元格
现在该用一些数据填充我们的工作表了。我们将使用一个简单的体育销售数据示例。 
您可以在不同的单元格中设置值，方法如下：
```csharp
Cells cells = sheet.Cells;
cells["A1"].PutValue("Sport");
cells["B1"].PutValue("Quarter");
cells["C1"].PutValue("Sales");
cells["A2"].PutValue("Golf");
cells["A3"].PutValue("Golf");
cells["A4"].PutValue("Tennis");
cells["A5"].PutValue("Tennis");
cells["A6"].PutValue("Tennis");
cells["A7"].PutValue("Tennis");
cells["A8"].PutValue("Golf");
cells["B2"].PutValue("Qtr3");
cells["B3"].PutValue("Qtr4");
cells["B4"].PutValue("Qtr3");
cells["B5"].PutValue("Qtr4");
cells["B6"].PutValue("Qtr3");
cells["B7"].PutValue("Qtr4");
cells["B8"].PutValue("Qtr3");
cells["C2"].PutValue(1500);
cells["C3"].PutValue(2000);
cells["C4"].PutValue(600);
cells["C5"].PutValue(1500);
cells["C6"].PutValue(4070);
cells["C7"].PutValue(5000);
cells["C8"].PutValue(6430);
```
在这些行中，我们定义标题并填充销售数据。可以将此步骤想象为在做饭前储备食品；食材（数据）越好，饭菜（分析）就越好。
## 步骤 5：创建数据透视表
现在到了最有趣的部分 — 创建数据透视表！以下是如何将其添加到工作表的方法：
```csharp
PivotTableCollection pivotTables = sheet.PivotTables;
//向工作表添加数据透视表
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```
在此代码片段中，我们指定了数据透视表的数据范围以及将其放置在工作表上的位置。数据范围`=A1:C8`覆盖我们的数据所在的区域。
## 步骤 6：自定义数据透视表
接下来，您需要自定义数据透视表以满足您的需求。这涉及控制显示的内容、分类方式以及如何计算数据。
```csharp
PivotTable pivotTable = pivotTables[index];
//不显示各行总计。
pivotTable.RowGrand = false;
//将第一个字段拖拽至行区域。
pivotTable.AddFieldToArea(PivotFieldType.Row, 0);
//将第二个字段拖拽至列区域。
pivotTable.AddFieldToArea(PivotFieldType.Column, 1);
//将第三个字段拖拽至数据区域。
pivotTable.AddFieldToArea(PivotFieldType.Data, 2);
pivotTable.CalculateData();
```
在这里，您要决定要汇总哪些数据字段以及如何表示它们。这就像为晚宴布置餐桌一样；您要决定什么最合适以及如何呈现它。
## 步骤 7：保存工作簿
最后，您可以将工作保存为所需的 ODS 格式。操作方法如下：
```csharp
workbook.Save(outputDir + "PivotTableSaveInODS_out.ods");
```
通过这一步，您就完成了您的项目并将其保存在您选择的目录中 - 令人满意的结局！
## 步骤 8：验证输出
最后，检查该过程是否成功完成总是一个好主意。您可以添加一个简单的控制台消息：
```csharp
Console.WriteLine("PivotTableSaveInODS executed successfully.");
```
此消息将出现在您的控制台中，以确认一切顺利进行。就像厨师在上菜前检查所有东西是否煮熟了一样！
## 结论 
就这样！您不仅使用 Aspose.Cells 创建了数据透视表，还将其保存为 ODS 格式。本指南将指导您完成每个步骤，确保您具备足够的知识和信心来应对未来的类似任务。
## 常见问题解答
### 什么是 Aspose.Cells？
Aspose.Cells 是一个复杂的库，可让您在.NET 应用程序中创建和操作 Excel 文件。
### 我可以免费使用 Aspose.Cells 吗？
是的，你可以从[Aspose 网站](https://releases.aspose.com/).
### Aspose.Cells 支持哪些格式?
它支持多种格式，包括 XLSX、XLS、ODS、PDF 等。
### 如何获得 Aspose.Cells 的支持？
您可以在[Aspose 支持论坛](https://forum.aspose.com/c/cells/9).
### 有临时执照吗？
是的，您可以通过 Aspose 网站申请临时许可证[这里](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
