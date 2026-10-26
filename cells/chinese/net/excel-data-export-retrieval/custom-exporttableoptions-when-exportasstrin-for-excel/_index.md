---
category: general
date: 2026-10-26
description: 在 ExportAsStrin 时，自定义 ExportTableOptions 可让您在 C# 中将 Excel 数据导出为字符串。请按照分步指南配置并运行导出。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Custom ExportTableOptions when ExportAsStrin
- how to export excel as string
- ExportTableOptions C#
- Excel to DataTable string conversion
- Aspose.Cells export as string
language: zh
lastmod: 2026-10-26
og_description: 当 ExportAsString 启用仅字符串的 Excel 导出时，自定义 ExportTableOptions。了解在 C# 中配置和运行导出的具体步骤。
og_image_alt: Code snippet showing ExportTableOptions configuration for string export
og_title: 在 ExportAsString 时自定义 ExportTableOptions – 在 C# 中将 Excel 导出为字符串
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Custom ExportTableOptions when ExportAsStrin lets you export Excel
    data as strings in C#. Follow the step‑by‑step guide to configure and run the
    export.
  headline: Custom ExportTableOptions when ExportAsStrin for Excel
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: 在 Excel 中使用 ExportAsString 时的自定义 ExportTableOptions
url: /zh/net/excel-data-export-retrieval/custom-exporttableoptions-when-exportasstrin-for-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Custom ExportTableOptions when ExportAsStrin – 在 C# 中将 Excel 导出为字符串

如果您需要 **Custom ExportTableOptions when ExportAsStrin** 来获取每个单元格的值为纯字符串，本指南将准确展示如何操作。无论您是在构建数据导入管道，还是需要干净的 CSV 准备导出，您都将了解为何以这种方式配置选项可以避免类型转换的意外。

在本教程中，您将学习使用 Aspose.Cells 库 **如何将 Excel 导出为字符串**，查看完整可运行的代码，并理解每个设置背后的原理。无需外部文档——所有内容就在这里。

## 前提条件

* .NET 6.0 SDK 或更高版本已安装  
* Visual Studio 2022（或任何支持 .NET 的 IDE）  
* Aspose.Cells for .NET 包（通过 NuGet 安装：`Install-Package Aspose.Cells`）  
* 将 Excel 工作簿（`sample.xlsx`）放置在项目根文件夹中  

这些项目是唯一的依赖项；代码可在 Windows、Linux 或 macOS 上运行，无需额外库。

## 步骤 1：加载要导出的工作簿

使用 **Custom ExportTableOptions when ExportAsStrin** 时，首先要从已加载的工作簿中获取一个 `Worksheet` 对象。该对象让您能够访问行、列以及导出 API。

```csharp
using Aspose.Cells;
using System.Data;

// Load the workbook from disk
Workbook workbook = new Workbook("sample.xlsx");

// Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*为什么这很重要:*  
`Workbook` 读取文件一次并将所有格式信息保存在内存中。通过选择特定的 `Worksheet`，您可以限制导出范围，避免对隐藏工作表进行不必要的处理。

## 步骤 2：使用 ExportAsString = true 配置 ExportTableOptions

**Custom ExportTableOptions when ExportAsStrin** 的核心是 `ExportTableOptions` 对象。将 `ExportAsString` 设置为 true 会强制导出器将每个单元格视为字符串，无论其原始数据类型（日期、数字、布尔等）如何。启用 `PreserveFormatting` 可在生成的字符串中保留视觉样式（例如货币符号）。

```csharp
// Create and configure the export options
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export every cell value as a string
    PreserveFormatting = true      // Keep the original cell formatting
};
```

*为什么这很重要:*  
当您随后调用 `ExportDataTable` 时，库通常会尝试推断每列的 .NET 类型。将 `ExportAsString = true` 后，这一步推断被跳过，防止出现意外的 `DateTime` 或 `double` 转换，从而导致下游 CSV 解析器出错。

## 步骤 3：使用自定义选项将范围导出为 DataTable

现在您可以从工作表中导出一个矩形范围（第 0‑9 行，第 0‑4 列）。该方法返回一个 `DataTable`，其中每个字段都是 `string`。

```csharp
// Export rows 0‑9 and columns 0‑4 (5 columns total) as a DataTable
DataTable dataTable = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 10,
    totalColumns: 5,
    options: exportOptions);
```

*为什么这很重要:*  
`ExportDataTable` 是将 Excel 数据转移到许多 .NET API 已经能够理解的关系结构（例如 Entity Framework、Dapper）最方便的方式。通过传递 **Custom ExportTableOptions when ExportAsStrin**，您可以确保每个 `DataColumn.DataType` 为 `typeof(string)`。

## 步骤 4：验证结果——所有值都是字符串

验证导出是否如预期工作是个好习惯。下面的循环会打印每个单元格及其运行时类型。

```csharp
Console.WriteLine("Exported DataTable (all values as strings):");
foreach (DataRow row in dataTable.Rows)
{
    for (int i = 0; i < dataTable.Columns.Count; i++)
    {
        object value = row[i];
        Console.Write($"{value} ({value.GetType().Name})\t");
    }
    Console.WriteLine();
}
```

**预期输出**

```
123 (String)    2023‑01‑15 (String)    $45.67 (String)    TRUE (String)    Sample text (String)
...
```

每个单元格都显示 `String` 作为其类型，确认 **Custom ExportTableOptions when ExportAsStrin** 正常工作。

## 步骤 5：可选 – 将 DataTable 写入 CSV

如果您的最终目标是纯文本文件，您可以轻松将 `DataTable` 序列化为 CSV：



## 接下来您应该学习什么？

以下教程涵盖与本指南演示的技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能，并在自己的项目中探索替代实现方案。

- [Export HTML Strings from Excel to DataTable using Aspose.Cells for .NET: A Step‑by‑Step Guide](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)
- [Export Custom Properties Excel Pdf Aspose Cells Net](/cells/hongkong/net/workbook-operations/export-custom-properties-excel-pdf-aspose-cells-net/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hongkong/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}