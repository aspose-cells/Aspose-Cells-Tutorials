---
title: 将数据导入 Excel 工作表时指定公式字段
linktitle: 将数据导入 Excel 工作表时指定公式字段
second_title: Aspose.Cells .NET Excel 处理 API
description: 在本详细教程中了解如何使用 Aspose.Cells for .NET 将数据导入具有指定公式字段的 Excel 表。
weight: 11
url: /zh/net/excel-custom-number-date-formatting/specify-formula-fields-while-importing-data-to-worksheet-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将数据导入 Excel 工作表时指定公式字段

## 介绍

在以编程方式处理 Excel 文件时，Aspose.Cells for .NET 是一款非常有价值的工具。它提供了强大的功能，可轻松创建、修改和操作 Excel 电子表格。它提供的有趣功能之一是能够在将数据导入 Excel 工作表时指定公式字段。想象一下，您正在处理财务报告，需要根据用户输入自动计算总数。本教程将指导您逐步以简洁明了的方式实现这一目标。

## 先决条件

在深入研究代码之前，让我们确保您拥有所需的一切。 

1. Visual Studio 或任何 .NET 集成开发环境 (IDE)：确保您有一个合适的 IDE 来编写和运行您的 C# 代码。
2.  Aspose.Cells for .NET：您需要下载并在项目中引用 Aspose.Cells 库。您可以从[Aspose 发布](https://releases.aspose.com/cells/net/).
3. 基本 C# 知识：熟悉 C# 和面向对象编程概念将帮助您更好地理解示例。
4. .NET Framework：本教程假设您使用 .NET Framework 4.5 或更高版本。

一旦您整理好了先决条件，让我们继续使用指定的公式字段将一些数据导入到 Excel 表中。

## 导入包

在开始编写代码之前，您需要导入必要的 Aspose.Cells 命名空间。这通常在 C# 文件的顶部完成：

```csharp
using Aspose.Cells;
using System;
using System.Collections.Generic;
```

这使您可以使用 Aspose.Cells 库提供的类和方法，而无需每次都在其前面加上命名空间。

让我们将整个过程分解为可管理的步骤：

## 步骤 1：定义输出目录

首先，您需要确定要保存 Excel 文件的位置。操作方法如下：

```csharp
static string outputDir = "Your Document Directory"; //在此指定您的文档目录
```

代替`"Your Document Directory"`替换为您的实际文件路径。生成的 Excel 文件将保存在此处。

## 步骤 2：为数据项创建用户定义类

接下来，我们将定义一个类来构造我们计划导入的数据。

```csharp
class DataItems
{
    public int Number1 { get; set; }
    public int Number2 { get; set; }
    public string Formula1 { get; set; }
    public string Formula2 { get; set; }
}
```

这`DataItems`该类将保存原始整数和我们将写入 Excel 表的公式。 

## 步骤 3：初始化列表以保存数据项

我们将使用一个列表来保存我们的多个实例`DataItems`班级。

```csharp
List<DataItems> dis = new List<DataItems>();
```

## 步骤 4：将数据项添加到列表

现在，让我们向列表中添加一些条目。每个条目将包含两个数字和两个公式。

```csharp
//定义并添加每个数据项
DataItems di = new DataItems();
di.Number1 = 2002;
di.Number2 = 3502;
di.Formula1 = "=SUM(A2,B2)";
di.Formula2 = "=HYPERLINK(\"https://www.aspose.com\",\"Aspose 网站\")”;
dis.Add(di);

//对其他数据项重复上述操作
```

确保定制每一个`DataItems`具有唯一值和公式的实例。

## 步骤 5：创建工作簿和 Access 工作表

接下来，创建工作簿并访问我们最终将导入数据的第一个工作表。

```csharp
Workbook wb = new Workbook(); //创建新工作簿
Worksheet ws = wb.Worksheets[0]; //访问第一个工作表
```

## 步骤 6：指定导入表选项

这就是奇迹发生的地方。您需要指定数据中的哪些字段与公式相对应。 

```csharp
ImportTableOptions opts = new ImportTableOptions();
opts.IsFormulas = new bool[] { false, false, true, true };
```

在此示例中，最后两个字段包含公式，由`true`，而前两个字段设置为`false`.

## 步骤 7：导入自定义对象

现在一切都已设置好，让我们将数据项列表导入工作表。

```csharp
ws.Cells.ImportCustomObjects(dis, 0, 0, opts);
```

此行有效地导入从单元格 A1 开始的数据。

## 步骤 8：计算公式

由于我们已经导入了一些公式，因此计算它们至关重要。

```csharp
wb.CalculateFormula();
```

此方法可确保您的公式根据其依赖关系进行评估。

## 步骤 9：自动调整列

为了确保您的数据易于显示，您可以根据内容自动调整列。

```csharp
ws.AutoFitColumns();
```

此步骤优化了 Excel 文件的布局。 

## 步骤 10：保存 Excel 文件

最后，是时候保存您新创建的 Excel 文件了。 

```csharp
wb.Save(outputDir + "outputSpecifyFormulaFieldsWhileImportingDataToWorksheet.xlsx");
```

确保您的输出文件名相关且具有描述性！

## 步骤 11：检查执行

作为确认一切运行正确的简单方法，您可能需要打印一条消息。

```csharp
Console.WriteLine("SpecifyFormulaFieldsWhileImportingDataToWorksheet executed successfully.");
```

这会立即给您反馈，表明代码运行正常，没有任何问题。

## 结论

就这样！您已成功使用 Aspose.Cells for .NET 和指定公式字段将数据导入 Excel 工作表。通过遵循这些步骤，您可以应用类似的技术来自动执行适合您需求的数据处理任务。无论您是处理报告的数字还是只是维护数据，掌握使用 Aspose 进行 Excel 操作的技巧都是一项值得拥有的技能。

## 常见问题解答

### 什么是 Aspose.Cells？
Aspose.Cells 是一个.NET 库，旨在以编程方式创建、操作和转换 Excel 文件。

### 如何安装 Aspose.Cells for .NET？
您可以从[Aspose 发布](https://releases.aspose.com/cells/net/)并在您的项目中引用它。

### 我可以免费使用 Aspose.Cells 吗？
是的，Aspose 提供免费试用，网址为[此链接](https://releases.aspose.com/).

### 在哪里可以找到更多示例？
更多示例和文档可在以下位置找到：[Aspose 文档页面](https://reference.aspose.com/cells/net/).

### 如果我在使用 Aspose 时遇到问题该怎么办？
您可以从 Aspose 支持论坛寻求帮助[这里](https://forum.aspose.com/c/cells/9).
 
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
