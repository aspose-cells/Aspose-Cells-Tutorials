---
category: general
date: 2026-11-19
description: 使用 C# 在 Excel 中设置货币格式——学习在导入 Excel 工作表时如何设置数字格式并为列应用样式。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set currency format
- how to set number format
- assign number format
- excel worksheet import
- style excel columns
language: zh
lastmod: 2026-11-19
og_description: 使用 C# 在 Excel 中设置货币格式，并了解如何设置数字格式、分配数字格式以及在导入 Excel 工作表时对列进行样式设置。
og_image_alt: Screenshot showing Excel cells formatted as currency after import
og_title: 使用 C# 在 Excel 中设置货币格式 – 完整的分步指南
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  headline: Set currency format while importing data into Excel using C#
  type: TechArticle
- description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  name: Set currency format while importing data into Excel using C#
  steps:
  - name: Expected result
    text: 'When you open **FinancialReport.xlsx**, you’ll see:'
  - name: Assign number format to date columns
    text: '```csharp // Suppose column 2 contains dates and you want "dd-MMM-yyyy"
      columnStyles[2].Number = 14; // 14 = built‑in short date ```'
  - name: Use custom number formats for percentages
    text: '```csharp columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00% ```'
  - name: Styling beyond number formats
    text: 'You can also set font, background color, or alignment on the same `Style`
      object:'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
- Formatting
title: 使用 C# 将数据导入 Excel 时设置货币格式
url: /zh/net/excel-custom-number-date-formatting/set-currency-format-while-importing-data-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中导入数据到 Excel 时设置货币格式

如果您需要在 Excel 工作表中 **设置货币格式**，本指南将向您展示如何 **设置数字格式** 并在执行 **Excel 工作表导入** 时为列应用样式。您将看到一个完整、可运行的示例，该示例为 `DataTable` 的每一列分配正确的数字格式，并使用所需的样式导入数据。

在 C# 中操作 Excel 往往不仅仅是把原始值写入——您还必须控制数字的显示方式。无论是生成发票、财务报告还是仪表盘，正确地格式化货币、百分比或日期都能让输出瞬间易读。

## 前置条件

开始之前，请确保您具备：

* 已安装 .NET 6.0（或更高版本）。
* 引用了 **Aspose.Cells for .NET**（或任何提供带 `Number` 属性的 `Style` 类的库）。  
  *NuGet*: `Install-Package Aspose.Cells`。
* 对 `DataTable` 和 C# 集合有基本了解。
* 使用 Visual Studio 2022 或 VS Code 等 IDE。

## 第一步：获取要写入工作表的数据

首先获取包含原始数据的 `DataTable`。在实际项目中，这可能来自数据库查询、API 调用或 CSV 解析器。

```csharp
using System.Data;

/// <summary>
/// Returns a sample DataTable with three columns:
/// Id (int), Amount (decimal), and Description (string).
/// </summary>
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Amount", typeof(decimal));
    table.Columns.Add("Description", typeof(string));

    // Sample rows
    table.Rows.Add(1, 1234.56m, "Office supplies");
    table.Rows.Add(2, 98765.43m, "Consulting fees");
    table.Rows.Add(3, 0.99m, "Miscellaneous");

    return table;
}

// Retrieve the data
DataTable dataTable = GetData();
```

> **为什么重要：** 导入一个已填充的 `DataTable` 可以让数据获取逻辑与 Excel 生成逻辑分离，从而提升可测试性和可维护性。

## 第二步：创建样式数组 – 每列对应一个条目

Aspose.Cells 需要一个 `Style[]`，其长度必须与您计划导入的列数相匹配。每个元素可以保存特定的数字格式。

```csharp
// Allocate a Style object for each column
Style[] columnStyles = new Style[dataTable.Columns.Count];

// Initialize each Style instance (required before assigning properties)
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = ws.Workbook.CreateStyle();
}
```

> **专业提示：** 即使只需要为部分列设置格式，也必须为每一列创建一个 `Style` 实例；否则在导入时会出现 `NullReferenceException`。

## 第三步：为目标列分配数字格式

内置的样式编号因库而异。在 Aspose.Cells 中：

* `0` → 常规（整数）  
* `2` → 货币（例如 `$#,##0.00`）  
* `3` → 日期，等等。

这里我们 **为两列分配数字格式**：第一列（Id）保持整数，第二列（Amount）使用货币格式。

```csharp
// Column 0 → integer format (style number 0)
columnStyles[0].Number = 0;

// Column 1 → currency format (style number 2)
columnStyles[1].Number = 2;

// If you need a custom format, you can also use a format string:
// columnStyles[1].Custom = "$#,##0.00";
```

> **设置数字格式的方法：** 使用 `Number` 属性是选择内置格式的最快方式。若需本地化货币，请考虑使用包含相应货币符号的自定义格式字符串。

## 第四步：将 DataTable 导入工作表，并应用列样式

样式数组准备好后，执行导入。`ImportDataTable` 方法会遵循您传入的样式。

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];

// Import the DataTable, starting at cell A1 (row 0, column 0)
// The third argument (true) tells the method to write column headers.
ws.Cells.ImportDataTable(
    dataTable,
    /* includeColumnNames */ true,
    /* startRow */ 0,
    /* startColumn */ 0,
    columnStyles);

// Save the workbook
workbook.Save("FinancialReport.xlsx", SaveFormat.Xlsx);
```

### 预期结果

打开 **FinancialReport.xlsx** 时，您将看到：

| Id | Amount      | Description      |
|----|------------|------------------|
| 1  | $1,234.56  | Office supplies |
| 2  | $98,765.43 | Consulting fees |
| 3  | $0.99      | Miscellaneous    |

***Amount** 列使用您设置的货币格式显示，而 **Id** 列保持整数。*

## 为其他场景设置数字格式的方法

### 为日期列分配数字格式

```csharp
// Suppose column 2 contains dates and you want "dd-MMM-yyyy"
columnStyles[2].Number = 14; // 14 = built‑in short date
```

### 使用自定义数字格式显示百分比

```csharp
columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00%
```

### 超越数字格式的样式设置

您还可以在同一个 `Style` 对象上设置字体、背景色或对齐方式：

```csharp
columnStyles[1].Font.IsBold = true;
columnStyles[1].ForegroundColor = Color.LightYellow;
columnStyles[1].HorizontalAlignment = TextAlignmentType.Center;
```

> **为什么有效：** `Style` 对象聚合了单元格的所有视觉属性。当您将数组传递给 `ImportDataTable` 时，每个单元格会自动继承定义好的样式。

## 常见陷阱及规避方法

| 陷阱 | 症状 | 解决方案 |
|------|------|----------|
| 未为每个 `Style` 实例化对象 | 导入时出现 `NullReferenceException` | 在循环中调用 `CreateStyle()` 后再设置属性。 |
| 使用了错误的内置数字索引 | 格式错误（例如日期显示为整数） | 查阅库文档，获取正确的 `Number` 常量。 |
| 未保存工作簿 | 没有输出文件或文件为空 | 在导入完成后调用 `workbook.Save(...)`。 |
| 货币符号的地区不匹配 | 在非美国地区仍显示 `$` 符号 | 使用自定义格式字符串并加入相应符号（如 `"€#,##0.00"`）。 |

## 完整、可运行的示例



## 接下来应该学习什么？

以下教程涵盖与本指南紧密相关的主题，帮助您在实际项目中进一步掌握 API 功能并探索替代实现方式。

- [Create excel file c# – style cells and set currency format](/cells/english/net/excel-formatting-and-styling/create-excel-file-c-style-cells-and-set-currency-format/)
- [How to Format Excel Columns in C# – Complete Guide](/cells/english/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/)
- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}