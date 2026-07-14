---
category: general
date: 2026-07-13
description: 如何使用 C# 和 ExportTableOptions 将单元格范围导出为表格。学习逐步的工作簿设置、格式化和表格导出。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export cell range as table
- ExportTableOptions usage
- Workbook and Worksheet handling
- cell value formatting C#
- scientific notation export
language: zh
lastmod: 2026-07-13
og_description: 如何使用 ExportTableOptions 在 C# 中将单元格范围导出为表格。请按照本指南格式化单元格、创建工作簿，并轻松导出表格。
og_image_alt: Diagram illustrating a C# code snippet that exports a single cell range
  as a formatted table
og_title: 如何将单元格范围导出为表格 – 完整的 C# 教程
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to export cell range as table using C# and ExportTableOptions.
    Learn step‑by‑step workbook setup, formatting, and table export.
  headline: How to Export Cell Range as Table – Complete C# Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
- data export
title: 如何将单元格范围导出为表格 – 完整 C# 指南
url: /zh/net/excel-data-export-retrieval/how-to-export-cell-range-as-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何导出单元格范围为表格 – 完整 C# 指南

是否曾经想过 **如何导出单元格范围为表格**，却因为格式问题抓狂？你并不是唯一的遇到这种情况的人。无论是将数据输送到报告管道，还是仅仅需要快速的 CSV‑style 导出，掌握导出过程都能为你节省大量手动复制粘贴的时间。

在本教程中，我们将逐步演示如何对数值单元格应用科学计数法，并使用 **ExportTableOptions** 将其导出为表格。完成后，你将拥有可运行的代码片段，了解每一次调用背后的 *原因*，并知道如何为更大的范围或不同的格式调整代码。

## 前置条件

- .NET 6 或更高版本（API 在 .NET Framework 4.7+ 上表现相同）
- 已安装 Aspose.Cells for .NET（`Install-Package Aspose.Cells`）
- 对 C# 语法有基本了解；不需要深入了解 Excel 内部实现

准备好了吗？太好了——让我们开始吧。

## 第一步：设置导出选项 – 如何导出单元格范围为表格

首先需要创建一个 **ExportTableOptions** 实例，告诉库如何处理单元格内容。没有它，导出默认使用原始数值，这会导致下游消费者期望文本时出现问题。

```csharp
// Step 1: Define export options – export the cell value as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Return the cell content as text
    CustomFormat = "0.00E+00"       // Apply scientific notation format
};
```

**为什么这很重要：**  
- `ExportAsString = true` 强制库写入单元格显示的文本，而不是其底层的 double。  
- `CustomFormat` 让你实现 **科学计数法导出**，在处理非常大或非常小的数字时非常有用。

> **小技巧：** 如果需要日期或货币格式，分别将 `"0.00E+00"` 替换为 `"yyyy‑MM‑dd"` 或 `"$#,##0.00"`。

## 第二步：创建工作簿并获取第一个工作表 – 工作簿和工作表处理

**Workbook** 代表整个 Excel 文件，而 **Worksheet** 是单个标签页。对于简单的导出，我们只使用索引为 0 的第一个工作表，它始终存在。

```csharp
// Step 2: Create a new workbook and access the first worksheet
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

**为什么这很重要：**  
创建一个全新的 `Workbook` 可确保干净的起始状态——没有隐藏样式或残留数据会干扰你。访问 `Worksheets[0]` 是获取活动工作表的最快方式，无需担心工作表名称。

## 第三步：填充目标单元格 – C# 中的单元格值格式化

现在我们在单元格 **A1**（第 0 行，第 0 列）中插入一个数值。我们选择的值特意使用了长小数，以便你能看到科学计数法的效果。

```csharp
// Step 3: Insert a numeric value into cell A1 (row 0, column 0)
sheet.Cells[0, 0].PutValue(12345.6789);
```

**为什么这很重要：**  
调用 `PutValue` 会自动推断单元格的数据类型。因为我们随后以字符串形式导出，原始的 double 将使用前面设置的格式进行转换，得到整洁的 `"1.23E+04"` 输出。

## 第四步：将定义的单元格范围导出为表格 – 将单元格范围导出为表格

在选项和数据准备就绪后，最后一步是让 Aspose.Cells 将范围写出。`ExportTable` 方法需要起始行/列、范围大小以及我们构建的 options 对象。

```csharp
// Step 4: Export the defined cell range as a table using the options above
// Parameters: startRow, startColumn, totalRows, totalColumns, options
sheet.ExportTable(0, 0, 1, 1, exportOptions);
```

**为什么这很重要：**  
- `totalRows = 1` 与 `totalColumns = 1` 将导出限制在单个单元格，但你可以将这些数字扩大以覆盖更大的块（例如 `5, 3` 表示 5 行 × 3 列的范围）。  
- 该方法将数据写入内部表结构，可保存为 CSV、HTML，甚至直接流式传输给客户端。

### 保存结果（可选）

如果你想将导出的表格持久化到磁盘，可以将其写入 CSV 文件：

```csharp
// Optional: Save the exported table as CSV for verification
using (var stream = new MemoryStream())
{
    sheet.ExportTableToCSV(stream, exportOptions);
    File.WriteAllBytes("ExportedTable.csv", stream.ToArray());
}
```

运行上述代码将生成包含以下内容的文件：

```
1.23E+04
```

## 边缘情况与常见变体

| 场景 | 需要更改的内容 | 原因 |
|-----------|----------------|--------|
| **导出多行** | 调整 `totalRows` 并在需要时遍历行 | 允许批量导出而无需重复调用 `ExportTable` |
| **保留公式** | 将 `ExportAsString = false` | 保持原始公式而不是显示的数值 |
| **不同分隔符** | 使用 `ExportTableToCSV(..., ',', ...)` 重载 | 将逗号分隔切换为制表符或管道符分隔 |
| **大型工作表** | 流式导出以避免 `OutOfMemoryException` | 适用于超过 10 000 行的情况 |

## 完整工作示例

下面是完整的、可直接复制粘贴的程序。它可以在任何引用 Aspose.Cells 的 .NET 控制台项目中编译运行。

```csharp
using System;
using System.IO;
using Aspose.Cells;

class ExportCellRangeDemo
{
    static void Main()
    {
        // 1️⃣ Define export options – how to export cell range as table
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            CustomFormat = "0.00E+00"
        };

        // 2️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Put a numeric value into A1
        sheet.Cells[0, 0].PutValue(12345.6789);

        // 4️⃣ Export the single‑cell range as a table
        sheet.ExportTable(0, 0, 1, 1, exportOptions);

        // Optional: write to CSV to see the result
        using (var ms = new MemoryStream())
        {
            sheet.ExportTableToCSV(ms, exportOptions);
            File.WriteAllBytes("ExportedTable.csv", ms.ToArray());
        }

        Console.WriteLine("Export complete! Check ExportedTable.csv");
    }
}
```

**预期输出：**  
一个名为 `ExportedTable.csv` 的文件，包含单行内容：

```
1.23E+04
```

如果在文本编辑器中打开该 CSV，你会看到科学计数法正如定义那样被应用。

## 结论

我们已经从头到尾覆盖了 **如何导出单元格范围为表格**：设置 `ExportTableOptions`、创建 `Workbook`、插入数据，最后调用 `ExportTable`。通过理解每个环节，你现在可以将此方法扩展到更大的范围、不同的格式，甚至集成到 Web API 中，实现 Excel 派生数据的即时服务。

展望未来，你可能想探索：

- **ExportTableToHTML** 用于网页预览  
- **ExportTableToDataTable** 直接供 ADO.NET 管道使用  
- 高级 **自定义格式** 用于日期、货币或百分比  

试一试这些功能，你就能把简单的单元格导出转变为强大的数据交付引擎。有什么问题或奇特的使用场景？在下方留言——祝编码愉快！

## 接下来你应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你在自己的项目中进一步掌握 API 功能并探索替代实现方式。每篇资源都包含完整的可运行代码示例和逐步解释。

- [How to Export Visible Excel Rows Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [How to Export Excel Files in .NET Using Aspose.Cells&#58; A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [How to Access an Excel Cell by Name Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/cell-operations/access-cell-by-name-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}