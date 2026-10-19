---
category: general
date: 2026-08-11
description: 在 C# 中导出 Excel 为 txt，提供分步指南。学习如何使用 Aspose.Cells 将 xlsx 转换为纯文本。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- convert xlsx to plain text
- how to export excel worksheet as text
- export worksheet as text file
language: zh
lastmod: 2026-08-11
og_description: 在 C# 中快速将 Excel 导出为 txt。本教程展示如何将 xlsx 转换为纯文本，配置格式，并处理大型工作表。
og_image_alt: Code snippet that exports an Excel worksheet to a plain text file using
  C#
og_title: 使用 C# 将 Excel 导出为 txt – 开发者分步指南
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  headline: Export excel to txt in C# – complete programming guide
  type: TechArticle
- description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  name: Export excel to txt in C# – complete programming guide
  steps:
  - name: – load the workbook
    text: '```csharp using Aspose.Cells;'
  - name: – get the first worksheet
    text: '```csharp Worksheet sheet = workbook.Worksheets[0]; ```'
  - name: – define export options for text conversion
    text: '```csharp ExportTableOptions exportOptions = new ExportTableOptions { ExportAsString
      = true, // Export all values as text DateTimeFormat = "yyyy-MM-dd", // Desired
      date format NumberFormat = "#,##0.00" // Desired numeric format }; ```'
  - name: – export worksheet as text file
    text: '```csharp // Apply the options to the worksheet sheet.ExportTableOptions
      = exportOptions;'
  type: HowTo
tags:
- excel
- csharp
- text export
- aspose.cells
title: 在 C# 中将 Excel 导出为 TXT – 完整编程指南
url: /zh/net/converting-excel-files-to-other-formats/export-excel-to-txt-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中将 Excel 导出为 txt – 完整编程指南

如果您需要 **将 Excel 导出为 txt**，只需几行 C# 代码即可实现。本指南展示了如何将 `.xlsx` 工作簿转换为纯文本文件，并保持您定义的数据格式。

将工作表导出为文本文件是常见需求，尤其是下游系统仅接受分隔数据，或您需要审计原始单元格值时。在以下章节中，您将学习如何配置日期和数字格式、处理大表格以及避免常见陷阱。

## 将 xlsx 转换为纯文本的前置条件

在开始之前，请确保您拥有：

* 已安装 .NET 6.0（或更高版本）——代码目标为 .NET Standard 2.0，亦可在 .NET Framework 4.6+ 上运行。
* **Aspose.Cells** 的许可证（免费评估版可用于测试）。
* 如 Visual Studio 2022 或 Visual Studio Code 等 IDE。
* 一个名为 `input.xlsx` 的 Excel 文件，放置在项目可引用的文件夹中。

这些即为唯一的外部需求；本教程不依赖其他 NuGet 包。

## 使用 Aspose.Cells 将 excel 导出为 txt 的方法

Aspose.Cells 提供了 `ExportTableOptions` 类，可让您控制单元格值如何渲染为字符串。将 `ExportAsString` 设置为 `true` 可强制每个单元格以文本形式写入，这对于需要确定性纯文本输出的场景至关重要。

### 步骤 1 – 加载工作簿

```csharp
using Aspose.Cells;

string inputPath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(inputPath);
```

*`Workbook` 构造函数会将 Excel 文件读取到内存中。如果文件不存在，会抛出异常，生产代码中建议使用 try‑catch 包裹此调用。*

### 步骤 2 – 获取第一个工作表

```csharp
Worksheet sheet = workbook.Worksheets[0];
```

*工作表采用零基索引，索引 0 对应第一张标签页。需要定位特定标签页时，可使用工作表名称（`workbook.Worksheets["Sheet1"]`）代替索引。*

### 步骤 3 – 为文本转换定义导出选项

```csharp
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,               // Export all values as text
    DateTimeFormat = "yyyy-MM-dd",       // Desired date format
    NumberFormat   = "#,##0.00"          // Desired numeric format
};
```

*`ExportAsString` 确保每个单元格，无论原始类型如何，都会在输出文件中成为字符串。`DateTimeFormat` 和 `NumberFormat` 属性让您控制日期和数字的显示方式，这在 **将 xlsx 转换为纯文本** 时尤为关键，因为系统可能期望特定的格式。*

### 步骤 4 – 将工作表导出为文本文件

```csharp
// Apply the options to the worksheet
sheet.ExportTableOptions = exportOptions;

// Export the data to a tab‑delimited text file
string outputPath = @"YOUR_DIRECTORY\Exported.txt";
sheet.ExportDataTable(outputPath);
```

*`ExportDataTable` 使用您提供的选项将工作表内容写入纯文本文件。默认分隔符为制表符（`\t`）。如果需要其他分隔符，可使用接受 `ExportTableOptions` 实例的重载，并指定 `ExportTableOptions.Separator`。生成的文件可在任意文本编辑器中打开，或导入数据库。*

#### 预期输出

假设 `input.xlsx` 包含：

| A            | B       | C          |
|--------------|---------|------------|
| 2023‑05‑01   | 1234.5  | Sample text|

使用上述选项后，`Exported.txt` 文件将包含：

```
2023-05-01	1,234.50	Sample text
```

每列之间以制表符分隔，日期采用 `yyyy‑MM‑dd` 格式，数字使用千位分隔符（逗号）并保留两位小数。

## 导出工作表为文本文件时的常见陷阱

| 问题 | 产生原因 | 如何避免 |
|------|----------|----------|
| 区域设置导致的数字格式差异 | 默认格式遵循操作系统语言环境，可能出现逗号或句点不一致的情况。 | 在 `ExportTableOptions` 中显式设置 `NumberFormat`。 |
| 隐藏的行或列出现在输出中 | Aspose.Cells 会导出整个已使用范围，包括隐藏的行。 | 将 `ExportTableOptions.ExportHiddenRows = false` 和 `ExportHiddenColumns = false` 设置为 false，以跳过它们。 |
| 大工作表导致内存压力 | 导出前会将整个工作簿加载到内存。 | 使用 `Workbook.LoadOptions` 并将 `LoadDataOnly = true`，或分块处理文件以降低内存占用。 |
| 源文件中日期单元格已存为文本 | 若单元格已经是格式化的字符串，导出器会把它当作文本并忽略 `DateTimeFormat`。 | 确保源工作簿中的日期以 Excel 正式的日期类型存储。 |

解决这些问题后，**如何将 Excel 工作表导出为文本**的过程在不同环境下都能可靠运行。

## 扩展方案 – 自定义分隔符与流式导出

如果需要逗号分隔值（CSV）文件而非制表符分隔文件，可修改选项：

```csharp
exportOptions.Separator = ',';
exportOptions.ExportHiddenRows = false;   // optional
exportOptions.ExportHiddenColumns = false; // optional
sheet.ExportTableOptions = exportOptions;
sheet.ExportDataTable(@"YOUR_DIRECTORY\Exported.csv");
```

对于大于 500 MB 的文件，采用流式写入可防止应用耗尽内存：

```csharp
using (FileStream stream = new FileStream(@"YOUR_DIRECTORY\LargeExport.txt",
                                          FileMode.Create,
                                          FileAccess.Write,
                                          FileShare.None,
                                          bufferSize: 81920,
                                          useAsync: true))
{
    sheet.ExportDataTable(stream, exportOptions);
}
```

接受 `Stream` 的重载会逐行写入，非常适合批处理作业或直接向客户端返回文本文件的 Web 服务。

## 以编程方式验证结果

导出完成后，您可以读取第一行回到内存，以确认格式是否正确：

```csharp
string firstLine = File.ReadLines(outputPath).First();
Console.WriteLine($"First line: {firstLine}");
```

运行此代码片段应打印出 *预期输出* 部分显示的同一行，从而确认转换成功。

## 完整代码回顾

将所有片段组合在一起，即可得到一个可直接复制到控制台应用程序的自包含程序：

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputPath  = @"YOUR_DIRECTORY\input.xlsx";
        string outputPath = @"YOUR_DIRECTORY\Exported.txt";

        // Load workbook
        Workbook workbook = new Workbook(inputPath);
        Worksheet sheet = workbook.Worksheets[0];

        // Configure export options
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            DateTimeFormat = "yyyy-MM-dd",
            NumberFormat   = "#,##0.00",
            Separator      = '\t' // tab delimiter
        };

        // Apply options and export
        sheet.ExportTableOptions = exportOptions;
        sheet.ExportDataTable(outputPath);

        // Simple verification
        string firstLine = File.ReadLines(outputPath).First();
        Console.WriteLine($"Export completed. First line: {firstLine}");
    }
}
```

编译并运行程序；`Exported.txt` 文件会出现在与源工作簿相同的目录下。

## 后续步骤与相关主题

* **将工作表导出为文本文件** – 试验不同的分隔符、编码（UTF‑8 与 ASCII）以及换行风格，以实现跨平台兼容。
* **批量转换** – 循环遍历 `workbook.Worksheets` 为每个标签页生成单独的文本文件。
* **与数据库集成** – 将生成的文本直接管道到 SQL Server 或 PostgreSQL 的批量插入操作。
* **

## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并探索替代实现方式：

- [How to Export Excel Files in .NET Using Aspose.Cells&#58; A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [How to Export Visible Excel Rows Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}