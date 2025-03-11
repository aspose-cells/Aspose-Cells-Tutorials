---
title: 从 Excel 单元格中检索数据
linktitle: 从 Excel 单元格中检索数据
second_title: Aspose.Cells .NET Excel 处理 API
description: 本分步教程将帮助您学习如何使用 Aspose.Cells for .NET 从 Excel 单元格中检索数据，非常适合初学者和经验丰富的开发人员。
weight: 10
url: /zh/net/excel-data-export-retrieval/retrieve-data-from-cells-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 Excel 单元格中检索数据

## 介绍

在 Excel 中管理数据时，从单元格读取和检索信息的能力至关重要。Aspose.Cells for .NET 是一个功能强大的库，允许开发人员无缝操作 Excel 文件。在本教程中，我们将深入介绍如何使用 Aspose.Cells 从 Excel 工作簿中的单元格检索数据。无论您是经验丰富的开发人员还是刚刚入门，本指南都将逐步指导您完成该过程。

## 先决条件

在我们进入代码之前，您需要满足一些先决条件：

1. Visual Studio：确保您的机器上安装了 Visual Studio。这是我们用来编写和执行代码的 IDE。
2.  Aspose.Cells for .NET：您需要有 Aspose.Cells 库。您可以从[Aspose 网站](https://releases.aspose.com/cells/net/).
3. C# 基础知识：熟悉 C# 编程将帮助您更好地理解示例。
4. Excel 文件：准备好 Excel 文件（例如，`book1.xls`) 您将在本教程中使用它。

一旦满足了这些先决条件，我们就可以开始探索如何从 Excel 单元格中检索数据。

## 导入包

首先，您需要在 C# 项目中导入必要的命名空间。这将允许您使用 Aspose.Cells 提供的类和方法。

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

导入这些命名空间后，您就可以开始编码了。让我们将这个过程分解为易于管理的步骤。

## 步骤 1：设置文档目录

第一步是定义 Excel 文件所在的文档目录的路径。这很重要，因为它告诉应用程序在哪里找到您要处理的文件。


```csharp
//文档目录的路径。
string dataDir = "Your Document Directory";
```

代替`"Your Document Directory"`实际路径`book1.xls`文件存储的位置。当您尝试打开文件时，Aspose.Cells 将在此路径中查找该文件。

## 步骤 2：打开现有工作簿

现在您已经设置了文档目录，下一步是打开您要使用的工作簿（Excel 文件）。


```csharp
//打开现有工作簿
Workbook workbook = new Workbook(dataDir + "book1.xls");
```

在这里，我们创建一个`Workbook`通过传递 Excel 文件的完整路径来获取工作簿。此步骤将初始化工作簿并使其准备好进行数据检索。

## 步骤 3：访问第一个工作表

打开工作簿后，您需要访问要从中检索数据的特定工作表。在本例中，我们将访问第一个工作表。


```csharp
//访问第一个工作表
Worksheet worksheet = workbook.Worksheets[0];
```

这`Worksheets`集合允许您访问工作簿中的不同工作表。索引`[0]`指的是第一个工作表。如果要访问后续工作表，可以相应地更改索引。

## 步骤 4：循环遍历单元格

现在您有了工作表，是时候循环遍历每个单元格来检索数据了。这就是奇迹发生的地方！


```csharp
foreach (Cell cell1 in worksheet.Cells)
{
    //用于存储不同数据类型值的变量
    string stringValue;
    double doubleValue;
    bool boolValue;
    DateTime dateTimeValue;

    //传递单元格中包含的数据类型以供评估
    switch (cell1.Type)
    {
        //评估单元格数据的字符串值数据类型
        case CellValueType.IsString:
            stringValue = cell1.StringValue;
            Console.WriteLine("String Value: " + stringValue);
            break;

        //评估单元格数据的双精度数据类型
        case CellValueType.IsNumeric:
            doubleValue = cell1.DoubleValue;
            Console.WriteLine("Double Value: " + doubleValue);
            break;

        //评估单元格数据的布尔值类型
        case CellValueType.IsBool:
            boolValue = cell1.BoolValue;
            Console.WriteLine("Bool Value: " + boolValue);
            break;

        //评估单元格数据的日期/时间值的数据类型
        case CellValueType.IsDateTime:
            dateTimeValue = cell1.DateTimeValue;
            Console.WriteLine("DateTime Value: " + dateTimeValue);
            break;

        //评估单元格数据的未知数据类型
        case CellValueType.IsUnknown:
            stringValue = cell1.StringValue;
            Console.WriteLine("Unknown Value: " + stringValue);
            break;

        //终止单元格数据类型为空的类型检查
        case CellValueType.IsNull:
            break;
    }
}
```

在此步骤中，我们循环遍历工作表中的每个单元格。对于每个单元格，我们使用`switch`语句。根据类型，我们检索值并将其打印到控制台。以下是案例的细分：

-  IsString：如果单元格包含字符串，我们使用以下方法检索它`StringValue`.
- IsNumeric：对于数值，我们使用`DoubleValue`.
- IsBool：如果单元格包含布尔值，则我们使用以下方法访问它`BoolValue`.
- IsDateTime：对于日期和时间值，我们使用`DateTimeValue`.
- IsUnknown：如果数据类型未知，我们仍然检索字符串表示形式。
- IsNull：如果单元格为空，我们就跳过它。

## 结论

使用 Aspose.Cells for .NET 从 Excel 单元格检索数据是一个简单的过程。通过遵循这些步骤，您可以高效地从 Excel 文件中提取各种数据类型。无论您是构建报告工具、自动化数据输入，还是只需要分析数据，Aspose.Cells 都能提供完成工作所需的灵活性和功能。

## 常见问题解答

### 什么是 Aspose.Cells？  
Aspose.Cells 是一个.NET 库，允许开发人员创建、操作和转换 Excel 文件，而无需安装 Microsoft Excel。

### 我可以免费使用 Aspose.Cells 吗？  
是的，Aspose.Cells 提供免费试用版，您可以用来测试其功能。您可以下载[这里](https://releases.aspose.com/).

### 我可以从 Excel 单元格中检索哪些类型的数据？  
您可以检索各种数据类型，包括字符串、数字、布尔值和日期/时间值。

### 如何获得 Aspose.Cells 的支持？  
您可以通过访问获得支持[Aspose 论坛](https://forum.aspose.com/c/cells/9)您可以在这里提出问题并获得社区的帮助。

### 有临时执照吗？  
是的，Aspose 提供临时许可证以供评估。您可以找到更多信息[这里](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
