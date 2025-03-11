---
title: 在 .NET 中以编程方式指定 Excel 文件的兼容性
linktitle: 在 .NET 中以编程方式指定 Excel 文件的兼容性
second_title: Aspose.Cells .NET Excel 处理 API
description: 学习使用 Aspose.Cells for .NET 操作 Excel 数据透视表，包括数据更新、兼容性设置和单元格格式。
weight: 23
url: /zh/net/creating-and-configuring-pivot-tables/specifying-compatibility/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以编程方式指定 Excel 文件的兼容性

## 介绍

在当今数据驱动的世界中，以编程方式管理和操作 Excel 文件已成为许多开发人员的必需品。如果您在 .NET 中使用 Excel，Aspose.Cells 是一个功能强大的库，可让您轻松创建、读取、修改和保存 Excel 文件。此库的一个重要功能允许您以编程方式指定 Excel 文件的兼容性。在本教程中，我们将探讨如何操作 Excel 文件，特别是重点介绍如何使用 Aspose.Cells for .NET 管理兼容性。最后，您将了解如何在刷新和管理数据时设置 Excel 文件（尤其是数据透视表）的兼容性。

## 先决条件

在进入编码阶段之前，请确保您已具备以下条件：

1. C# 基础知识：由于我们将用 C# 编写代码，熟悉该语言将帮助您更好地理解本教程。
2.  Aspose.Cells for .NET 库：您可以从[Aspose Cells 发布页面](https://releases.aspose.com/cells/net/)。如果您还没有，请考虑先免费试用以了解其功能。
3. Visual Studio：一个可以有效地编写和测试 C# 代码的 IDE。
4. 示例 Excel 文件：确保您有一个示例 Excel 文件，最好是包含用于演示的数据透视表的文件。在我们的示例中，我们将使用`sample-pivot-table.xlsx`.

有了这些先决条件，我们就可以开始编码过程了。

## 导入包

在开始编写应用程序之前，您需要在代码中包含必要的命名空间，以便有效利用 Aspose.Cells 库。操作方法如下。

### 导入 Aspose.Cells 命名空间

```csharp
using System.IO;
using System;
using Aspose.Cells;
using Aspose.Cells.Pivot;
using System.Drawing;
```

这行代码确保您可以访问 Aspose.Cells 库中的所有类和方法。

现在，让我们详细分解该过程，以确保一切都清晰易懂。

## 步骤 1：设置目录

首先，设置 Excel 文件所在的目录。提供正确的文件路径很重要。

```csharp
//文档目录的路径。
string dataDir = "Your Document Directory";
```

在这里，替换`"Your Document Directory"`替换为 Excel 文件的实际路径。这是示例数据透视表文件应驻留的位置。

## 步骤 2：加载源 Excel 文件

接下来，我们需要加载包含示例数据透视表的 Excel 文件。 

```csharp
//加载包含示例数据透视表的源 Excel 文件
Workbook wb = new Workbook(dataDir + "sample-pivot-table.xlsx");
```

在此步骤中，我们创建`Workbook`类，加载指定的Excel文件。 

## 步骤 3：访问工作表

现在工作簿已加载，您必须访问包含数据透视表数据的工作表。

```csharp
//访问包含数据透视表数据的第一个工作表
Worksheet dataSheet = wb.Worksheets[0];
```

在这里，我们访问数据透视表所在的第一个工作表。您还可以根据 Excel 结构循环遍历或指定其他工作表。

## 步骤 4：处理单元格数据

接下来，您将修改工作表中的某些单元格值。 

### 步骤 4.1：修改单元格 A3

让我们首先访问单元格 A3 并设置其值。

```csharp
//访问单元格 A3 并设置其数据
Cells cells = dataSheet.Cells;
Cell cell = cells["A3"];
cell.PutValue("FooBar");
```

此代码片段使用值“FooBar”更新单元格 A3。

### 步骤 4.2：使用长字符串修改单元格 B3

现在，让我们在单元格 B3 中设置一个较长的字符串，它超出了 Excel 的标准字符限制。

```csharp
//访问单元格 B3，设置其数据
string longStr = "Very long text 1. very long text 2.... [continue your long string]";
cell = cells["B3"];
cell.PutValue(longStr);
```

此代码很重要，因为它设置了您对数据限制的期望，尤其是在使用 Excel 中的兼容性设置时。

## 步骤 5：检查单元格 B3 的长度

确认我们输入的字符串的长度也很重要。

```csharp
//打印单元格B3字符串的长度
Console.WriteLine("Length of original data string: " + cell.StringValue.Length);
```

这只是为了验证你的单元格中有多少个字符。

## 步骤 6：设置其他单元格值

现在我们将访问更多单元格并设置一些值。

```csharp
//访问单元格 C3 并设置其数据
cell = cells["C3"];
cell.PutValue("closed");

//访问单元格 D3 并设置其数据
cell = cells["D3"];
cell.PutValue("2016/07/21");
```

每个代码片段都会更新工作表中的几个附加单元格。

## 步骤 7：访问数据透视表

接下来，您将访问第二张工作表，其中包含数据透视表数据。

```csharp
//访问包含数据透视表的第二个工作表
Worksheet pivotSheet = wb.Worksheets[1];

//访问数据透视表
PivotTable pivotTable = pivotSheet.PivotTables[0];
```

此代码片段允许您操作数据透视表以进行兼容性设置。

## 步骤 8：设置 Excel 2003 兼容性

设置数据透视表是否与 Excel 2003 兼容至关重要。 

```csharp
// IsExcel2003Compatible 属性指示在刷新数据透视表时数据透视表是否与 Excel2003 兼容
pivotTable.IsExcel2003Compatible = true;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

这是真正的转变开始的地方。通过设置`IsExcel2003Compatible`到`true`，刷新时将字符长度限制为 255。

## 步骤 9：兼容性设置后检查长度

设置兼容性之后，我们来看看它对数据有何影响。

```csharp
//检查数据透视表的单元格 B5 的值。
Cell b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to True: " + b5.StringValue.Length);
```

如果初始数据超过 255 个字符，您可能会看到确认截断效果的输出。

## 步骤 10：更改兼容性设置

现在，让我们更改兼容性设置并再次检查。

```csharp
//现在将 IsExcel2003Compatible 属性设置为 false 并再次刷新
pivotTable.IsExcel2003Compatible = false;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

这使得您的数据能够反映其原始长度，而不受之前的限制。

## 步骤 11：再次验证长度 

让我们验证数据现在是否准确反映了其实际长度。

```csharp
//现在它将打印单元格数据的原始长度。数据现在尚未被截断。
b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to False: " + b5.StringValue.Length);
```

您应该看到输出确认删除了截断。

## 步骤 12：设置单元格格式

为了增强视觉体验，您可能需要设置单元格格式。 

```csharp
//设置单元格 B5 的行高和列宽，并设置其文本的换行
pivotSheet.Cells.SetRowHeight(b5.Row, 100);
pivotSheet.Cells.SetColumnWidth(b5.Column, 65);
Style st = b5.GetStyle();
st.IsTextWrapped = true;
b5.SetStyle(st);
```

这些代码行通过调整单元格尺寸和启用文本换行使数据更易于阅读。

## 步骤 13：保存工作簿

最后，保存包含您所做更改的工作簿。

```csharp
//以 xlsx 格式保存工作簿
wb.Save(dataDir + "SpecifyCompatibility_out.xlsx", SaveFormat.Xlsx);
```

保存 Excel 文件时，选择合适的文件格式至关重要。`Xlsx`格式应用广泛并且与多个 Excel 版本兼容。

## 结论

恭喜！您现在已经使用 Aspose.Cells for .NET 编写了 Excel 文件兼容性设置。本教程概述了每个步骤，从设置环境到更改数据透视表的兼容性设置。如果您曾经处理过需要特定限制或兼容性的数据，那么这是一项您不想忽视的技能。

## 常见问题解答

### 什么是 Aspose.Cells？  
Aspose.Cells 是一个.NET 库，旨在帮助开发人员无缝创建、操作和转换 Excel 文件。

### 为什么 Excel 兼容性很重要？  
Excel 兼容性对于确保文件可以在目标版本的 Excel 中打开和使用至关重要，特别是当文件包含早期版本不支持的功能或格式时。

### 我可以使用 Aspose.Cells 以编程方式创建数据透视表吗？  
是的，您可以使用 Aspose.Cells 以编程方式创建和操作数据透视表。该库提供了多种方法来添加与数据透视表相关的数据源、字段和功能。

### 如何检查 Excel 单元格中字符串的长度？  
您可以使用`StringValue`财产`Cell`对象来获取单元格的内容，然后调用`.Length`属性来找出字符串的长度。

### 除了行高和行宽之外，我还能自定义单元格格式吗？  
当然！Aspose.Cells 允许广泛的单元格格式。您可以通过`Style`班级。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
