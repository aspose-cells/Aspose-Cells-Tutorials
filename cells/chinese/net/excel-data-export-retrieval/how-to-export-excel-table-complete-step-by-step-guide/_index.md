---
category: general
date: 2026-07-03
description: 学习如何使用 C# 将 Excel 表导出为 .txt 文件并保存 Excel 表为 .txt 文件。提供完整代码示例，将 Excel 数据导出为纯文本。
draft: false
keywords:
- how to export excel table
- save excel table to .txt file
- export excel data as plain text
- Aspose.Cells export table
- C# Excel to text
language: zh
og_description: 如何将 Excel 表格导出为纯文本。本指南向您展示如何将 Excel 数据导出为纯文本，并使用 Aspose.Cells 将 Excel
  表格保存为 .txt 文件。
og_title: 如何导出Excel表格 – 完整的C#教程
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to export Excel table to a .txt file and save Excel table
    to .txt file using C#. Export Excel data as plain text with full code example.
  headline: How to Export Excel Table – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- File I/O
title: 如何导出 Excel 表格——完整的逐步指南
url: /zh/net/excel-data-export-retrieval/how-to-export-excel-table-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何导出 Excel 表格 – 完整分步指南

是否曾经想过 **如何导出 Excel 表格** 而不把整个工作簿全部加载到内存中？你并不是唯一有此需求的人。在许多自动化任务中，下游系统只接受一个简单的 `.txt` 文件，所以你需要 **将 Excel 表格保存为 .txt 文件**，既快速又可靠。

在本教程中，我们将通过一个简洁的 C# 示例，使用 Aspose.Cells **将 Excel 数据导出为纯文本**。完成后，你将拥有一个可直接运行的程序，了解每行代码的意义，并学会如何根据自己的特殊情况调整导出方式。

## 你需要准备的内容

- **Aspose.Cells for .NET**（任意近期版本，例如 23.12）。  
- .NET 6 SDK 或更高版本——代码同样可以在 .NET Core 上编译。  
- 一个包含至少一个 Excel 表格的示例 `input.xlsx`。  
- 文本编辑器或 IDE（Visual Studio、VS Code、Rider……随你喜欢）。

除了 Aspose.Cells 之外不需要额外的 NuGet 包，整个过程可在 Windows、Linux 或 macOS 上运行。

## 第一步：创建项目并导入命名空间

首先，新建一个控制台应用并引入必要的命名空间。

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTableExport
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the export logic here.
        }
    }
}
```

> **小技巧：** 如果使用 .NET CLI，运行 `dotnet new console -n ExcelTableExport`，随后执行 `dotnet add package Aspose.Cells`，再粘贴上述代码。

## 第二步：加载工作簿并获取第一张工作表

`Workbook` 对象代表整个 Excel 文件。只加载一次即可保持低内存占用。

```csharp
// Step 2: Load the workbook and get the first worksheet
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = wb.Worksheets[0];
```

为什么选择第一张工作表？在许多自动生成的报表中，数据都位于首张工作表，但你也可以更改索引，或使用 `wb.Worksheets["SheetName"]` 按名称获取。

## 第三步：获取工作表上定义的第一个表格

Excel 表格（ListObjects）提供结构化数据，使导出过程更可预测。

```csharp
// Step 3: Retrieve the first table defined on the worksheet
Table tbl = ws.Tables[0];
```

如果工作簿中包含多个表格，只需遍历 `ws.Tables` 或通过 `tbl.Name` 进行选择。

## 第四步：配置导出选项 – 将每个单元格导出为字符串

Aspose.Cells 允许在导出时控制每个单元格的格式。将 `ExportAsString` 设置为 `true`，即可让数字、日期和公式都以纯文本形式输出。

```csharp
// Step 4: Set up export options – export every cell as a string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true
};
```

### 添加自定义导出操作以去除空白字符

源数据中常常会出现前后空格。去除空格可以让最终的 `.txt` 文件更整洁。

```csharp
// Define a custom export action to trim cell values before writing
exportOptions.CustomExport = (cell, writer) =>
{
    writer.Write(cell.StringValue.Trim());
};
```

该 lambda 接收 `Cell` 对象和 `TextWriter`。你也可以在这里加入条件逻辑——例如将逗号替换为分号，以实现 CSV‑style 输出。

## 第五步：从单元格 A1 开始导出表格到文本文件

现在我们真正把表格写入磁盘。`ExportTable` 方法会逐行遍历表格，并应用前面定义的选项。

```csharp
// Step 5: Export the table starting at cell A1 to a text file
using (StreamWriter writer = new StreamWriter("YOUR_DIRECTORY/Table.txt"))
{
    ws.Cells.ExportTable(tbl, "A1", exportOptions, writer);
}
```

**运行结果示例：** Excel 表格的每一行都会成为 `Table.txt` 中的一行。默认情况下列之间使用制表符（`\t`）分隔——非常适合下游解析。

### 预期输出示例

假设 `input.xlsx` 包含一个拥有三列（`ID`、`Name`、`Score`）和两行数据的表格，`Table.txt` 将呈现如下：

```
1    Alice    85
2    Bob      92
```

可以看到空格已被去除，所有内容都是纯文本——正是 **export excel data as plain text** 所要求的效果。

## 常见边缘情况处理

| 情况 | 处理方法 | 原因 |
|-----------|------------|-----|
| **表格中存在空单元格** | Lambda 使用 `cell.StringValue.Trim()`，对空白返回空字符串。 | 保持列对齐且不产生多余字符。 |
| **需要自定义分隔符** | 将 `writer.Write(cell.StringValue.Trim());` 替换为 `writer.Write($"{cell.StringValue.Trim()},");`，并在每行末尾去除多余的分隔符。 | 某些系统更偏好使用逗号或管道符而非制表符。 |
| **大型工作表（> 100 k 行）** | 使用 `ExportTableOptions` 并将 `ExportAsString = true`，如示例中那样流式写入文件；Aspose.Cells 会以流式方式处理行，避免 OOM。 | 确保可扩展性。 |
| **同一工作表中有多个表格** | 遍历 `ws.Tables`，对每个表格调用 `ExportTable`，可在导出之间插入分隔行。 | 让你 **save Excel table to .txt file** 针对每个表格都能导出。 |

## 完整工作示例

下面是可以直接复制到 `Program.cs` 的完整程序。将 `YOUR_DIRECTORY` 替换为你机器上实际存在的绝对或相对路径。

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTableExport
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
            Worksheet ws = wb.Worksheets[0];

            // Get first table
            if (ws.Tables.Count == 0)
            {
                Console.WriteLine("No tables found on the first worksheet.");
                return;
            }
            Table tbl = ws.Tables[0];

            // Configure export options
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                CustomExport = (cell, writer) =>
                {
                    // Trim whitespace and write value
                    writer.Write(cell.StringValue.Trim());
                }
            };

            // Export to text file
            string outputPath = "YOUR_DIRECTORY/Table.txt";
            using (StreamWriter writer = new StreamWriter(outputPath))
            {
                ws.Cells.ExportTable(tbl, "A1", exportOptions, writer);
            }

            Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

使用 `dotnet run` 运行程序。如果一切配置正确，你将看到确认信息，并在同目录下生成包含 **export excel data as plain text** 的 `Table.txt`。

## 附加：可视化确认（可选）

如果想快速查看生成文件的截图，可以在任意文本编辑器中打开它。下面是一张占位图，展示了预期的布局。

![how to export excel table screenshot](https://example.com/images/export-excel-table.png "how to export excel table")

*替代文字：* **how to export excel table** – 显示导出 Excel 表格后的纯文本输出。

## 小结与后续步骤

我们已经完整演示了使用 Aspose.Cells **如何导出 Excel 表格**，从加载工作簿、去除单元格空格，到最终写入干净的 `.txt` 文件。

- 现在你已经掌握了 **save Excel table to .txt file** 的自定义逻辑。  
- 可以根据需要修改 lambda，以处理日期、数字或自定义分隔符。  
- 对于更大的项目，建议将此逻辑封装为可复用的方法或类。

**接下来做什么？** 试着导出多个表格，或将分隔符改为逗号，以生成 CSV 文件。你也可以探索将 **export excel data as plain text** 直接写入网络流，实现实时集成。

有问题或遇到卡点？欢迎留言，祝编码愉快！


## 接下来该学习什么？

以下教程与本指南紧密相关，帮助你进一步掌握 API 功能并在项目中尝试不同实现方式，每篇均提供完整可运行的代码示例和逐步解释。

- [How to Export Excel Files in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [How to Export Visible Excel Rows Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [How to Combine Excel Sheets into a Single Text File Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/combine-excel-sheets-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}