---
"description": "学习如何使用 Aspose.Cells 在 .NET 中以编程方式对数据透视表进行排序。本指南将逐步讲解设置、配置、排序以及如何将结果保存为 Excel 和 PDF 文件。"
"linktitle": "在 .NET 中以编程方式对数据透视表进行自定义排序"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "在 .NET 中以编程方式对数据透视表进行自定义排序"
"url": "/zh/net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/"
"weight": 29
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以编程方式对数据透视表进行自定义排序

## 介绍
在 .NET 环境中使用 Excel 时，有一个库脱颖而出：Aspose.Cells。现在，如果有一个工具允许您以编程方式操作电子表格，难道您不会爱上它吗？这正是 Aspose.Cells 的功能！在今天的教程中，我们将深入探讨数据透视表的世界，并向您展示如何使用这个多功能库以编程方式实现自定义排序。
## 先决条件
在我们卷起袖子开始编写代码之前，请确保您已准备好以下几件事：
1. Visual Studio：你需要一个可以运行的 Visual Studio 版本。它是所有魔法发生的地方。
2. .NET Framework：熟悉 .NET 编程至关重要。无论您是 .NET Core 还是 .NET Framework 爱好者，都可以顺利上手。
3. Aspose.Cells 库：您需要安装 Aspose.Cells 库。您可以从 [下载链接](https://releases.aspose.com/cells/net/) 并将其添加到您的项目中。
4. 对数据透视表的基本了解：虽然您不需要成为专家，但在学习本教程时，了解一些有关数据透视表工作原理的知识将会很有帮助。
5. 示例 Excel 文件：有一个名为的示例 Excel 文件 `SamplePivotSort.xlsx` 已准备好在您的工作目录中进行测试。
## 导入包
整理好所有先决条件后，第一步就是导入必要的软件包。为此，请在代码顶部添加以下几行：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
该软件包提供了使用 Aspose.Cells 操作 Excel 文件所需的所有功能。

好了，让我们进入精彩的部分！我们将把创建数据透视表和应用自定义排序的过程分解成易于管理的步骤。
## 步骤 1：设置工作簿
首先，我们需要设置工作簿。操作方法如下：
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
在此步骤中，我们初始化一个新的 `Workbook` 实例，其中包含指向 Excel 文件的路径。这将充当数据透视表的画布。
## 第 2 步：访问工作表
接下来，我们需要访问将添加数据透视表的工作表。
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
在这里，我们抓取工作簿中的第一个工作表并调用 `PivotTableCollection`。此集合允许我们管理此工作表上的所有数据透视表。
## 步骤3：创建您的第一个数据透视表
现在是时候创建我们的数据透视表了。
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
我们在工作表中添加一个新的数据透视表，并指定数据范围及其位置。“E3”表示我们希望数据透视表的起始位置。然后，我们使用其索引来引用这个新的数据透视表。
## 步骤 4：配置数据透视表设置
让我们配置数据透视表！这意味着控制总计和字段排列等方面。
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
我们确保不显示行和列的总计，这样可以使数据更清晰。然后，我们将第一个字段添加到行区域，以启用自动排序和升序排序。
## 步骤 5：添加列和数据字段
设置好行之后，我们来添加列和数据字段。
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
我们将第二个字段添加为列，并将其格式化为日期。同样，我们启用自动排序和升序排列，以保持数据井然有序。最后，我们需要将第三个字段添加到数据区域：
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## 步骤 6：刷新并计算数据透视表
添加所有必要的字段后，确保我们的数据透视表是最新的并且已准备就绪。
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
这些方法刷新数据并重新计算，确保所有内容都是最新的并正确显示在数据透视表中。
## 步骤 7：根据行字段值进行自定义排序
让我们通过根据特定值（例如“海鲜”）对数据透视表进行排序来添加一些特色。
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
我们重复这个过程，创建另一个数据透视表，并按照第一个数据透视表类似的方式进行设置。现在我们可以进一步自定义它：
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## 步骤 8：额外的排序自定义让我们尝试另一种基于特定日期的排序方法：
```csharp
// 添加另一个数据透视表以按日期排序
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
// 重复与前面步骤类似的行和列设置
```
您只需重复相同的过程，创建第三个数据透视表，并根据您的需要定制其排序标准。
## 步骤 9：保存工作簿时间来保存我们投入的所有辛勤工作！
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
在这里，您可以将工作簿保存为 Excel 文件和 PDF。 `PdfSaveOptions` 允许更好的格式化，确保转换时每张表都出现在单独的页面上。
## 步骤 10：完成，让用户知道一切都很酷。
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## 结论
到目前为止，您已经学习了如何利用 Aspose.Cells 的强大功能在 .NET 应用程序中创建和自定义数据透视表。从初始设置到自定义排序，每个步骤都无缝衔接，带来流畅的体验。无论您需要展示年度销售数据还是跟踪库存统计数据，这些技能都能为您提供帮助！
## 常见问题解答
### 什么是数据透视表？
数据透视表是 Excel 中的一种数据处理工具，可让您汇总和分析数据，从而提供一种灵活的方式来轻松提取见解。
### 如何安装 Aspose.Cells？
您可以通过 Visual Studio 中的 NuGet 安装它，或者直接从 [下载链接](https://releases。aspose.com/cells/net/).
### Aspose.Cells 有试用版吗？
是的！您可以访问以下链接免费试用 [免费试用链接](https://releases。aspose.com/).
### 我可以对数据透视表中的多个字段进行排序吗？
当然！您可以根据需要添加和排序多个字段。
### 在哪里可以找到对 Aspose.Cells 的支持？
社区非常活跃，您可以在他们的论坛上提问 [这里](https://forum。aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}