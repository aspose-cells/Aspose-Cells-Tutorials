---
title: 在 Excel 中插入数据表行时将第一行向下移动
linktitle: 在 Excel 中插入数据表行时将第一行向下移动
second_title: Aspose.Cells .NET Excel 处理 API
description: 学习使用 Aspose.Cells for .NET 在 Excel 中插入 DataTable 行，而无需将第一行向下移动。分步指南，轻松实现自动化。
weight: 11
url: /zh/net/excel-data-import-export/shift-first-row-down-when-inserting-cells-datatable-rows-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中插入数据表行时将第一行向下移动

## 介绍

在将新数据插入 Excel 电子表格时，您是否厌倦了手动移动行？好吧，您很幸运！在本文中，我们将深入研究如何使用 Aspose.Cells for .NET 自动执行此过程。在本教程结束时，您不仅将学习如何使用 Excel 中的数据表，还将学习如何自定义导入选项以更好地满足您的需求。相信我；这可以为您节省大量时间和麻烦！所以，喝杯咖啡，让我们开始吧！

## 先决条件

在开始编码之前，请确保已完成所有设置：

1. Visual Studio：确保您已安装 Visual Studio（2017 或更高版本应该可以正常工作）。
2.  Aspose.Cells for .NET：您需要有 Aspose.Cells 库。如果您还没有这样做，您可以下载它[这里](https://releases.aspose.com/cells/net/).
3. 对 C# 和 Excel 的基本了解：对 C# 编程和 Excel 的工作原理的基本掌握肯定有助于您更有效地跟进。

您还需要准备一个示例 Excel 文件。在本指南中，我们将使用一个名为`sampleImportTableOptionsShiftFirstRowDown.xlsx`。您可以创建此文件或找到适合您需要的模板。

## 导入包

在开始编码之前，我们需要确保导入必要的包。在您的 C# 项目中，包括以下命名空间：

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

这些包对于处理工作簿、工作表和表格至关重要。

## 步骤 1：设置你的项目

### 创建新的 C# 项目

首先在 Visual Studio 中创建一个新的 C# 控制台应用程序。为项目起一个合适的名字，例如“ExcelDataImport”。

### 添加 Aspose.Cells NuGet 包

要添加 Aspose.Cells 包，请在解决方案资源管理器中右键单击您的项目，选择管理 NuGet 包，然后搜索“Aspose.Cells”。安装该包以确保您可以访问我们需要的所有功能。

## 第 2 步：定义数据表

接下来，我们将实现`ICellsDataTable`接口创建一个提供要导入的数据的类。以下是您可以如何构造`CellsDataTable`班级：

```csharp
class CellsDataTable : ICellsDataTable
{
    int m_index = -1;
    static String[] colsNames = new String[] { "Pet", "Fruit", "Country", "Color" };
    static String[] col0data = new String[] { "Dog", "Cat", "Duck" };
    static String[] col1data = new String[] { "Apple", "Pear", "Banana" };
    static String[] col2data = new String[] { "UK", "USA", "China" };
    static String[] col3data = new String[] { "Red", "Green", "Blue" };
    static String[][] colsData = new String[][] { col0data, col1data, col2data, col3data };
    
    // ... 实现其他成员...
}
```

在这里，我们定义列名和每列的数据，这将有助于我们导入表的结构。

## 步骤 3：实现 ICellsDataTable 接口成员

在`CellsDataTable`类，你需要实现`ICellsDataTable`接口。以下是所需的实现：

```csharp
public object this[string columnName]
{
    get
    {
        throw new NotImplementedException();
    }
}

object ICellsDataTable.this[int columnIndex]
{
    get
    {
        return colsData[columnIndex][m_index];
    }
}

string[] ICellsDataTable.Columns
{
    get { return colsNames; }
}

int ICellsDataTable.Count
{
    get { return col0data.Length; }
}

void ICellsDataTable.BeforeFirst()
{
    m_index = -1;
}

bool ICellsDataTable.Next()
{
    m_index++;
    return (m_index < Count);
}
```

该类的这一部分处理数据检索，定义有多少行和多少列，以及管理当前索引状态。

## 步骤 4：编写主函数

现在，让我们创建`Run`方法来协调整个表导入过程：

```csharp
public static void Run()
{
    string sourceDir = "Your Document Directory\\";
    string outputDir = "Your Document Directory\\";
    
    CellsDataTable cellsDataTable = new CellsDataTable();
    Workbook wb = new Workbook(sourceDir + "sampleImportTableOptionsShiftFirstRowDown.xlsx");
    Worksheet ws = wb.Worksheets[0];
```

## 步骤 5：设置导入选项

为了控制导入行为，您应该创建一个实例`ImportTableOptions`并相应地设置属性。具体来说，我们要设置`ShiftFirstRowDown`到`false`.

```csharp
    ImportTableOptions opts = new ImportTableOptions();
    opts.ShiftFirstRowDown = false; //我们不想将第一行向下移动
```

## 步骤 6：导入数据表

现在我们可以从我们的`CellsDataTable`到工作表中。

```csharp
    ws.Cells.ImportData(cellsDataTable, 2, 2, opts);
}
```

此命令将直接从指定的行和列开始插入数据表。

## 步骤 7：保存工作簿

最后，我们将修改后的工作簿保存回文件：

```csharp
    wb.Save(outputDir + "outputImportTableOptionsShiftFirstRowDown-False.xlsx");
}
```

## 结论

就这样！您已经学会了如何使用 Aspose.Cells for .NET 将 DataTable 行插入 Excel 工作表而不移动第一行。此过程不仅简化了 Excel 中的数据操作，而且还通过自动执行通常繁琐的任务来提高应用程序的性能。有了这些知识，您就可以更好地处理 Excel 自动化任务，从而节省您的时间和精力。

## 常见问题解答

### 什么是 Aspose.Cells for .NET？
Aspose.Cells for .NET 是一个编程库，允许开发人员在.NET 应用程序中创建、操作和转换 Excel 文件。

### 我需要许可证才能使用 Aspose.Cells 吗？
是的，您需要有效的许可证才能使用全部功能。不过，您可以免费试用以进行初步测试。

### 我可以在Web应用程序中使用Aspose.Cells吗？
当然！Aspose.Cells 非常适合使用 .NET 开发的桌面、Web 和基于云的应用程序。

### 我可以使用 Aspose.Cells 创建哪些类型的 Excel 文件？
您可以创建各种 Excel 文件格式，包括 XLSX、XLS、CSV 等。

### 我可以在哪里获得 Aspose.Cells 的支持？
您可以在[Aspose 论坛](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
