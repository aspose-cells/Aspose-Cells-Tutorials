---
category: general
date: 2026-10-13
description: 学习如何使用 Aspose.Cells 将 Excel 保存为 TXT。本指南仅需几步即可实现 Excel 导出为 TXT、向单元格写入值以及设置有效数字。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as txt
- export excel to txt
- write value to cell
- set significant digits
- export spreadsheet as txt
language: zh
lastmod: 2026-10-13
og_description: 使用 Aspose.Cells 将 Excel 保存为 TXT。了解如何将 Excel 导出为 TXT、向单元格写入值，以及仅用几行
  C# 代码设置有效数字。
og_image_alt: Screenshot showing a workbook saved as a TXT file using save excel as
  txt
og_title: 将 Excel 保存为 TXT – .NET 开发者分步指南
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to save Excel as TXT with Aspose.Cells. This guide covers
    export Excel to TXT, write value to cell, and set significant digits in just a
    few steps.
  headline: How to save Excel as TXT using Aspose.Cells in C#
  type: TechArticle
- questions:
  - answer: It rounds to the nearest value based on the specified number of significant
      digits, ensuring the output is mathematically accurate to that precision.
    question: Does `SignificantDigits` round or truncate?
  - answer: 'Yes. Replace the file path with a `MemoryStream` instance: `workbook.Save(stream,
      txtOptions);`. This is handy for web APIs that need to return the TXT content
      without touching the file system.'
    question: Can I export directly to a memory stream?
  - answer: 'Use `txtOptions.ExportFormattedValues = true`. This forces Aspose.Cells
      to write the cell’s displayed text rather than the raw value. ## Conclusion
      You now know how to **save Excel as TXT** with full control over precision,
      formatting, and output location. By following the four steps—create a workbo'
    question: What if I need to keep the original formatting (e.g., dates)?
  type: FAQPage
tags:
- Excel
- TXT
- Aspose.Cells
- .NET
title: 如何使用 Aspose.Cells 在 C# 中将 Excel 保存为 TXT
url: /zh/net/converting-excel-files-to-other-formats/how-to-save-excel-as-txt-using-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.Cells 在 C# 中将 Excel 保存为 TXT

如果您需要快速 **save Excel as TXT**，本教程将在五分钟内展示完整过程。您将看到如何将 Excel 导出为 TXT、write value to cell，以及 set significant digits，以便文本文件恰好包含您期望的数据。

将电子表格导出为 TXT 在下游系统仅接受纯文本输入、需要生成日志或希望获得可读的计算转储时非常有用。下面的示例适用于 Aspose.Cells v25.10 或更高版本，并可在任何 .NET 6+ 运行时上运行。

## 前提条件

在开始之前，请确保您拥有：

* **Aspose.Cells for .NET** 的授权副本（免费试用版可用于测试）。
* 已安装 .NET 6 SDK 或更高版本。
* 如 Visual Studio 2022、VS Code 或 Rider 等 IDE。
* 基础 C# 知识——无需高级 Excel 自动化经验。

您可以使用以下方式安装 Aspose.Cells NuGet 包：

```bash
dotnet add package Aspose.Cells
```

## 第一步：创建工作簿并访问其第一个工作表 (save excel as txt)

当您想要 **save Excel as TXT** 时，首先需要创建一个 `Workbook` 对象。该对象在内存中表示整个 Excel 文件。

```csharp
using Aspose.Cells;

// Create a new workbook (an empty Excel file)
Workbook workbook = new Workbook();

// Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

> **为什么这很重要：** `Workbook` 类是所有电子表格操作的入口。使用全新的工作簿可以避免任何隐藏的格式影响纯文本输出。

## 第二步：向单元格写入高精度数字 (write value to cell)

现在需要 **write value to cell** A1。`PutValue` 方法会自动检测数据类型并将其存储为数值。

```csharp
// Write a high‑precision number into cell A1
worksheet.Cells["A1"].PutValue(12345.6789012345);
```

> **提示：** 如果以后需要写入字符串、日期或公式，同样使用 `PutValue` 方法——只需传入相应的 .NET 类型即可。

## 第三步：配置导出选项以保留所需的精度 (set significant digits)

导出为 TXT 文件时，通常希望限制数字位数，以保持文件体积小或符合下游规范。`TxtSaveOptions` 类提供了 `SignificantDigits` 属性来实现此目的。

```csharp
// Configure TXT save options to retain only 6 significant digits
TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
{
    SignificantDigits = 6   // New option in v25.10
};
```

> **为何要设置 significant digits：** 若不进行此设置，Aspose.Cells 会写入完整的双精度值，可能产生类似 `12345.6789012345` 的长字符串。将 `SignificantDigits = 6` 可将输出裁剪为 `12345.7`，满足大多数报告需求。

## 第四步：将工作簿导出为 TXT 文件 (export excel to txt)

最后，使用 `Workbook.Save` 并传入前面配置好的选项即可 **export Excel to TXT**。

```csharp
// Save the workbook as a TXT file using the configured options
string outputPath = @"C:\Temp\LimitedDigits.txt";
workbook.Save(outputPath, txtSaveOptions);
```

代码执行完毕后，`LimitedDigits.txt` 包含：

```
12345.7
```

> **结果验证：** 在任意文本编辑器（记事本、VS Code）中打开文件，确认仅保留了六位有效数字，且没有额外的逗号或制表符分隔符。

## 完整、可运行的示例

下面是一个完整的控制台应用程序示例，您可以直接复制、粘贴并运行。

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Write a high‑precision number to cell A1
            worksheet.Cells["A1"].PutValue(12345.6789012345);

            // 3️⃣ Set up TXT save options with 6 significant digits
            TxtSaveOptions txtOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                SignificantDigits = 6
            };

            // 4️⃣ Save as TXT
            string path = @"C:\Temp\LimitedDigits.txt";
            workbook.Save(path, txtOptions);

            Console.WriteLine($"Workbook exported to TXT at: {path}");
        }
    }
}
```

**各代码块说明**

| 块 | 用途 |
|---|------|
| `using Aspose.Cells;` | 引入 Aspose.Cells 命名空间，提供 `Workbook`、`Worksheet` 和 `TxtSaveOptions` 所需。 |
| `Workbook workbook = new Workbook();` | 在内存中实例化一个空的 Excel 工作簿。 |
| `worksheet.Cells["A1"].PutValue(...);` | **write value to cell** A1，写入双精度数值。 |
| `TxtSaveOptions` | 配置 **set significant digits** 行为，以控制 TXT 导出的精度。 |
| `workbook.Save(..., txtOptions);` | 执行 **export excel to txt** 操作，生成纯文本文件。 |

## 边缘情况与额外提示

| 场景 | 处理方式 |
|------|----------|
| **大型工作表**（行列众多） | 如需 Unicode 支持，使用 `txtOptions.Encoding = Encoding.UTF8`，并考虑使用 `Workbook.Save(Stream, txtOptions)` 进行流式写入，以降低内存占用。 |
| **自定义分隔符**（逗号分隔值） | `TxtSaveOptions` 还提供 `Separator` 属性——将其设为 `','` 可生成 CSV 风格的 TXT 输出。 |
| **保留公式** | 设置 `txtOptions.ExportFormulas = true`，将公式文本写入而非计算后的值。 |
| **地区特定的小数分隔符** | 将 `txtOptions.DecimalSeparator` 调整为 `','` 以适配欧洲地区。 |
| **多个工作表** | 遍历 `workbook.Worksheets`，对每个工作表调用 `Save`，并在文件名中追加工作表名称。 |

## 常见问题

**问：`SignificantDigits` 是四舍五入还是截断？**  
答：它会根据指定的有效数字位数进行四舍五入，确保输出在该精度范围内的数学准确性。

**问：我可以直接导出到内存流吗？**  
答：可以。将文件路径替换为 `MemoryStream` 实例：`workbook.Save(stream, txtOptions);`。这在需要通过 Web API 返回 TXT 内容而不触及文件系统时非常便利。

**问：如果需要保留原始格式（例如日期）怎么办？**  
答：使用 `txtOptions.ExportFormattedValues = true`。这会强制 Aspose.Cells 写入单元格的显示文本而非原始值。

## 结论

现在您已经掌握了如何 **save Excel as TXT**，并能够全面控制精度、格式以及输出位置。只需遵循四个步骤——创建工作簿、**write value to cell**、**set significant digits**、以及 **export Excel to TXT**——即可在任何 .NET 应用中集成纯文本导出功能。

接下来，您可以进一步了解 **export spreadsheet as TXT with custom delimiters**、**convert Excel to CSV** 或 **use Aspose.Cells to generate JSON reports** 等相关主题。所有这些都基于本指南展示的核心概念，为您提供跨平台数据交换的多功能工具箱。

祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，每篇资源都提供完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [将 Excel 保存为文本 – 完整的 C# 指南，导出 Excel 为 TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [创建新工作簿并使用精度导出 Excel 为 TXT](/cells/english/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/)
- [创建新工作簿 – 使用完整精度导出 Excel 为 TXT](/cells/english/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}