---
category: general
date: 2026-11-19
description: 学习如何使用 C# 将工作簿保存为 CSV。本指南涵盖将 Excel 转换为 CSV、将电子表格导出为 CSV 以及精度选项。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save workbook as csv
- convert excel to csv
- export excel to csv
- export spreadsheet to csv
- how to convert xlsx to csv
language: zh
lastmod: 2026-11-19
og_description: 在 C# 中将工作簿保存为 CSV，附完整代码示例。将 Excel 转换为 CSV，导出电子表格为 CSV 并控制数值精度。
og_image_alt: Screenshot of C# code that saves a workbook as CSV
og_title: 在 C# 中将工作簿保存为 CSV – 完整编程指南
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to save workbook as CSV using C#. This guide covers convert
    Excel to CSV, export spreadsheet to CSV and precision options.
  headline: How to save workbook as CSV in C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- CSV export
title: 如何在 C# 中将工作簿保存为 CSV – 步骤指南
url: /zh/net/csv-file-handling/how-to-save-workbook-as-csv-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中将工作簿保存为 CSV – 步骤指南

如果您需要快速 **将工作簿保存为 CSV**，本教程将向您展示具体操作。您将看到一个完整、可运行的示例，将 Excel 文件转换为 CSV 文件，同时限制数字精度。

本指南还涵盖了相关任务，如 **convert Excel to CSV**、**export Excel to CSV** 和 **export spreadsheet to CSV**，让您可以选择最适合项目的方式。

## 您需要的环境

* .NET 6.0 或更高版本（代码兼容 .NET Core 和 .NET Framework）
* 对 **Aspose.Cells for .NET** NuGet 包的引用（示例中使用的 API）
* 一个名为 `input.xlsx` 的输入文件，放置在代码可引用的文件夹中
* 开发环境，例如 Visual Studio 2022 或 VS Code

> **技巧提示：** 如果您更倾向于使用免费替代方案，同样的逻辑适用于 `ClosedXML` 库；只需将 `Workbook` 和 `CsvSaveOptions` 类型替换为对应的 ClosedXML 类型。

![C# 程序将工作簿保存为 CSV 的示意图](image-placeholder.png "保存工作簿为 CSV 的示意图")

## 步骤 1：安装 Aspose.Cells

在项目文件夹中打开终端并运行：

```bash
dotnet add package Aspose.Cells
```

该包会添加 `Aspose.Cells` 命名空间，提供后续使用的 `Workbook` 类和 `CsvSaveOptions` 对象。

## 步骤 2：导入所需的命名空间

创建一个新的 C# 控制台项目（`dotnet new console`），并在 `Program.cs` 顶部添加以下 `using` 语句：

```csharp
using System;
using Aspose.Cells;
```

这些语句使得 `Workbook` 和 `CsvSaveOptions` 类型无需每次都写完整命名空间即可使用。

## 步骤 3：加载 Excel 工作簿

第一步是打开源 `.xlsx` 文件。`Workbook` 构造函数接受文件路径，因此您可以指向磁盘上的任意位置。

```csharp
// Step 1: Load the Excel workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*为什么重要*：加载工作簿会在内存中创建所有工作表、公式和单元格格式的表示。如果找不到文件，`Workbook` 会抛出 `FileNotFoundException`，您可以捕获它以提供更友好的错误信息。

## 步骤 4：配置 CSV 导出选项

当您 **export Excel to CSV** 时，通常需要控制数字的写入方式。`CsvSaveOptions` 类允许您指定有效数字位数、分隔符以及是否包含 UTF‑8 BOM。

```csharp
// Step 2: Configure CSV save options to limit precision
CsvSaveOptions csvOptions = new CsvSaveOptions
{
    // Keep only 5 significant digits to avoid overly long floating‑point strings
    SignificantDigits = 5,

    // Optional: change the delimiter from a comma to a semicolon for European locales
    // Separator = ';',

    // Optional: include a UTF‑8 BOM so Excel opens the file with the correct encoding
    // Encoding = Encoding.UTF8
};
```

*为什么重要*：默认情况下，Aspose.Cells 会写入单元格中存储的所有数字，这可能产生如 `0.123456789` 之类难以阅读的字符串。将 `SignificantDigits` 设置为 `5` 可将输出截断为更易读的格式（`0.12346`）。如果目标系统需要不同的分隔符，您也可以调整 `Separator`。

## 步骤 5：将工作簿保存为 CSV 文件

最后，调用 `Save` 方法，传入输出路径和已配置的选项。

```csharp
// Step 3: Save the workbook as a CSV file using the configured options
workbook.Save("YOUR_DIRECTORY/output.csv", csvOptions);
```

调用完成后，`output.csv` 包含 `input.xlsx` 的第一个工作表，以纯文本形式呈现。如果工作簿包含多个工作表且您只想导出特定的一个，请在调用 `Save` 前将 `csvOptions.ExportActiveWorksheetOnly = true` 设置好。

## 完整可运行示例

将所有内容整合在一起，下面是一个可直接复制、粘贴并运行的独立程序：

```csharp
using System;
using Aspose.Cells;

namespace ExcelToCsvDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Define file locations (adjust to your environment)
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            string outputPath = @"YOUR_DIRECTORY\output.csv";

            // Load the Excel workbook
            Workbook workbook = new Workbook(inputPath);

            // Configure CSV export options
            CsvSaveOptions csvOptions = new CsvSaveOptions
            {
                SignificantDigits = 5,               // limit numeric precision
                ExportActiveWorksheetOnly = true,    // export only the first sheet
                Separator = ',',                     // standard comma delimiter
                Encoding = System.Text.Encoding.UTF8 // ensure UTF‑8 output
            };

            // Save as CSV
            workbook.Save(outputPath, csvOptions);

            Console.WriteLine($"Workbook saved as CSV at: {outputPath}");
        }
    }
}
```

### 预期输出

运行程序会打印确认信息：

```
Workbook saved as CSV at: YOUR_DIRECTORY\output.csv
```

在文本编辑器或 Excel 中打开 `output.csv`——您会看到来自第一个工作表的数据，数字已四舍五入为五位有效数字。

## 如何使用自定义分隔符将 xlsx 转换为 csv

如果下游系统需要制表符分隔的文件，只需更改 `Separator` 属性：

```csharp
csvOptions.Separator = '\t';   // use a tab character
```

此小改动即可让您 **convert Excel to CSV** 为任意分隔符，而无需修改其他代码。

## 导出电子表格为 CSV 并将公式保留为数值

Aspose.Cells 在保存过程中会自动计算公式，因此 CSV 中包含 **计算后的数值**，而不是原始公式。如果您需要原始公式文本，请将 `csvOptions.ExportFormulaValues = false` 设置为 false：

```csharp
csvOptions.ExportFormulaValues = false; // writes the formula string itself
```

大多数报表场景需要计算后的结果，这也是默认行为符合典型 **export spreadsheet to CSV** 用例的原因。

## 常见陷阱及避免方法

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| 数字以科学计数法显示 | 大数或极小数值会自动使用科学计数法格式化 | 将 `csvOptions.UseScientificNotation = false` 或调整 `SignificantDigits`。 |
| 非 ASCII 字符出现乱码 | CSV 使用默认的 ANSI 代码页保存 | 在 `CsvSaveOptions` 中指定 `Encoding = Encoding.UTF8`。 |
| 多个工作表合并为一个 CSV | 默认情况下所有工作表会被串联 | 将 `csvOptions.ExportActiveWorksheetOnly = true` 并通过 `workbook.Worksheets[0].Activate()` 激活所需工作表。 |
| 文件末尾出现额外空行 | 某些库在最后一条记录后会添加换行符 | 保存后修剪文件或将 `csvOptions.AddTrailingNewLine = false` 设置为 false。 |

## 在 Web API 中导出 Excel 为 CSV（可选）

如果您需要将转换功能作为 REST 端点提供，可以将 CSV 直接流式传输到 HTTP 响应，而不是写入磁盘：

```csharp
[HttpGet("api/convert")]
public IActionResult ConvertToCsv()
{
    var workbook = new Workbook("input.xlsx");
    var options = new CsvSaveOptions { SignificantDigits = 5 };
    using var stream = new MemoryStream();
    workbook.Save(stream, options);
    stream.Position = 0;
    return File(stream, "text/csv", "output.csv");
}
```

此模式使您能够按需 **export Excel to CSV**，而无需在服务器上创建临时文件。

## 结论

现在您已经了解如何使用 C# **save workbook as CSV**。本教程涵盖了加载 Excel 文件、为精度和分隔符配置 `CsvSaveOptions`，以及将结果写入磁盘或响应流的过程。通过这些步骤，您同样可以 **convert Excel to CSV**、**export Excel to CSV** 和 **export spreadsheet to CSV**，以满足任何下游处理管道的需求。

接下来，您可以考虑探索：

* **如何使用多个工作表将 xlsx 转换为 CSV**（遍历 `workbook.Worksheets`）。
* 在导出前添加自定义标题或页脚。
* 如果受许可限制，可使用其他库，如 **ClosedXML** 或 **EPPlus**。

欢迎尝试本文展示的选项，并根据项目的具体需求调整代码。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于本教程展示的技术。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [将工作簿保存为 CSV – 完整的 C# 中 Export Excel to CSV 指南](/cells/english/net/csv-file-handling/save-workbook-as-csv-complete-guide-to-export-excel-to-csv-i/)
- [如何使用 Aspose.Cells 在 C# 中将 Excel 工作簿导出为 CSV](/cells/english/net/csv-file-handling/how-to-export-excel-workbook-to-csv-with-aspose-cells-in-c/)
- [如何使用 Aspose.Cells 以精确格式将工作簿保存为 CSV](/cells/english/net/csv-file-handling/how-to-save-workbook-as-csv-with-precise-formatting-using-as/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}