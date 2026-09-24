---
category: general
date: 2026-03-21
description: 如何使用 Aspose.Cells 在 C# 中导出带列名的 Excel 数据，保留数字格式，并读取特定行。学习如何读取 Excel 工作表并高效导出特定行。
draft: false
keywords:
- how to export excel
- preserve number format
- export with column names
- read excel worksheet
- export specific rows
language: zh
og_description: 如何使用 Aspose.Cells 导出带列名的 Excel 数据，保留数字格式，并读取特定行。为 C# 开发者提供完整可运行的示例。
og_title: 如何在 C# 中导出 Excel 数据 – 完整编程指南
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: 如何在 C# 中导出 Excel 数据——一步步指南
url: /zh/net/excel-data-export-retrieval/how-to-export-excel-data-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中导出 Excel 数据 – 完整编程指南

是否曾经想过 **如何导出 excel** 数据而不丢失原始格式？也许你尝试过快速复制‑粘贴，结果日期显示成 “44728” 或者缺少列标题。那真让人沮丧，对吧？在本教程中，你将看到一种简洁、端到端的方式来读取 Excel 工作表、保留数字格式、导出带列名的数据，甚至只挑选你需要的行。

我们将使用 Aspose.Cells 库，因为它提供对导出选项的细粒度控制。阅读完本指南后，你将拥有一个可复用的代码片段，可直接放入任何 .NET 项目，并且了解每个选项为何重要。无需外部文档——所有内容都在这里。

---

## 你将学到的内容

- **Read Excel worksheet** 使用 Aspose.Cells 读取到内存中。
- **Export specific rows**（例如 rows 0‑49）并保留列名。
- **Preserve number format** 以保持货币、日期和百分比的原始显示。
- 如何 **export with column names** 并在需要时包含单元格注释。
- 一个完整、可直接运行的 C# 示例以及常见陷阱的提示。

### 前置条件

- .NET 6.0 或更高（代码同样适用于 .NET Framework 4.6+）。
- 通过 NuGet 安装 Aspose.Cells for .NET（`Install-Package Aspose.Cells`）。
- 将 Excel 文件（`input.xlsx`）放置在可引用的文件夹中。

> **Pro tip:** 如果你在 CI 流水线中，考虑从私有源获取 NuGet 包，以避免许可证意外。

## 第一步 – 安装 Aspose.Cells 并添加命名空间

首先，确保项目中已安装 Aspose.Cells 包。打开 Package Manager Console 并运行：

```powershell
Install-Package Aspose.Cells
```

然后在 C# 文件顶部添加所需的 `using` 指令：

```csharp
using Aspose.Cells;
using System.Data;
using System;
```

这些导入让你能够使用 `Workbook`、`Worksheet`、`ExportTableOptions` 和 `DataTable`——这是 **reading an Excel worksheet** 并导出数据的核心组件。

## 第二步 – 加载工作簿（读取 Excel 文件）

现在我们真正 **read the Excel worksheet**。`Workbook` 构造函数接受文件路径，Aspose.Cells 能处理 `.xlsx` 和旧的 `.xls` 格式。

```csharp
// Step 2: Load the workbook containing the data
string filePath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(filePath);
```

> **Why this matters:** 只加载一次工作簿并重复使用同一个 `Worksheet` 对象，比起反复打开文件要高效得多，尤其是处理大型电子表格时。

## 第三步 – 配置导出选项（保留数字格式和列名）

这里我们告诉 Aspose.Cells *如何* 导出。`ExportTableOptions` 类让我们可以细致地调节输出。我们将启用三个标志：

1. `ExportAsString = true` – 强制每个单元格转换为字符串，确保数字保持其可视化表示。
2. `IncludeCellComments = true` – 复制单元格上的任何注释（对文档编写很有帮助）。
3. `PreserveNumberFormat = true` – 保留原始数字格式（货币符号、日期模式等）。

```csharp
// Step 3: Configure export options to control how the table is exported
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export all values as strings
    IncludeCellComments = true,     // Preserve any cell comments
    PreserveNumberFormat = true     // Keep the original number formatting
};
```

> **Edge case:** 如果将 `ExportAsString` 设置为 `false`，但仍想保留数字格式，可能会得到原始数值（例如日期显示为 44728）。同时开启两个标志可以避免此类意外。

## 第四步 – 获取第一个工作表（读取 Excel 工作表）

大多数简单文件的数据位于第一个工作表，所以我们通过索引获取它。如果需要其他工作表，只需将 `0` 替换为相应的零基索引，或使用 `workbook.Worksheets["SheetName"]`。

```csharp
// Step 4: Get the first worksheet from the workbook
Worksheet firstWorksheet = workbook.Worksheets[0];
```

> **Why it’s useful:** 直接访问工作表对象可以完全控制其 `Cells` 集合，这对于后续的 **export specific rows** 至关重要。

## 第五步 – 导出单元格范围（导出特定行）

现在进入教程的核心：将第 0‑49 行和第 0‑4 列（即前 50 行和前五列）导出到 `DataTable`。我们还会让 Aspose.Cells 将列名作为 `DataTable` 的第一行。

```csharp
// Step 5: Export a range of cells (rows 0‑49, columns 0‑4) to a DataTable using the options
DataTable exportedTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 50,
    totalColumns: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

### 这段代码的作用

- **`startRow: 0`** – 从工作表的最顶部开始。
- **`totalRows: 50`** – 获取前 50 行（即 **export specific rows**）。
- **`totalColumns: 5`** – 将导出限制在前五列。
- **`includeColumnNames: true`** – 确保 `DataTable` 的列标题与 Excel 表头行匹配，满足 **export with column names** 的需求。
- **`exportOptions`** – 应用第 3 步的设置，使数值保持如 “$1,234.56” 而不是 “1234.56” 的显示。

## 第六步 – 验证导出（结果是什么样的）

让我们将前几行打印到控制台，以便查看格式是否保留。

```csharp
// Step 6: Display a few rows to verify the export
Console.WriteLine("=== Exported DataTable Preview ===");
foreach (DataRow row in exportedTable.Rows)
{
    // Join each column with a tab for readability
    Console.WriteLine(string.Join("\t", row.ItemArray));
}
```

**预期输出（示例）：**

```
=== Exported DataTable Preview ===
Date        Description    Amount   Tax   Total
01/02/2024  Widget A       $120.00  $12  $132.00
01/03/2024  Widget B       $200.00  $20  $220.00
...
```

请注意日期以 `MM/dd/yyyy` 格式显示，货币保留了 `$` 符号——这要归功于 **preserve number format**。

## 常见陷阱及规避方法

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| 日期变成大数字 | `ExportAsString` 为 `false` | 保持 `ExportAsString = true` 或手动转换单元格 |
| 缺少列标题 | `includeColumnNames` 设置为 `false` | 需要 **export with column names** 时设为 `true` |
| 注释消失 | `IncludeCellComments` 未启用 | 在 `ExportTableOptions` 中开启 `IncludeCellComments` |
| 导出错误的工作表 | 在多工作表文件中使用 `Worksheets[0]` | 指定工作表名称：`workbook.Worksheets["Data"]` |
| 超出范围异常 | `totalRows` 超出实际行数 | 使用 `Math.Min(totalRows, worksheet.Cells.MaxDataRow + 1)` |

## 进阶：导出整个工作表并保持格式

如果以后需要导出整张工作表，只需将 `totalRows` 和 `totalColumns` 替换为工作表的最大维度：

```csharp
int maxRows = firstWorksheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int maxCols = firstWorksheet.Cells.MaxDataColumn + 1;

DataTable fullTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: maxRows,
    totalColumns: maxCols,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

现在你拥有一个适用于任意大小的 **read excel worksheet** 例程，同时仍然 **preserving number format** 并 **exporting with column names**。

## 完整可运行示例（复制粘贴即用）

下面是完整的程序，可直接放入控制台应用。它包含所有步骤、导入以及一个简单的验证打印。

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);

            // 2️⃣ Set export options (preserve number format, include comments, export as strings)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                IncludeCellComments = true,
                PreserveNumberFormat = true
            };

            // 3️⃣ Grab the first worksheet (read excel worksheet)
            Worksheet sheet = workbook.Worksheets[0];

            // 4️⃣ Export rows 0‑49, columns 0‑4 (export specific rows) with column headers
            DataTable table = sheet.Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: 50,
                totalColumns: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // 5️⃣ Show a preview
            Console.WriteLine("=== Exported DataTable Preview ===");
            foreach (DataRow row in table.Rows)
            {
                Console.WriteLine(string.Join("\t", row.ItemArray));
            }

            // Keep console open
            Console.WriteLine("\nExport complete. Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

将其保存为 `Program.cs`，运行 `dotnet run`，你应该能在终端看到格式化的预览。

## 结论

我们已经完整演示了使用 Aspose.Cells **how to export excel** 数据的全过程，涵盖了从加载工作簿、保留数字格式、导出列名到限制特定行的导出。代码独立完整，可直接运行，并包含对常见边缘情况的实用防护。

准备好下一个挑战了吗？尝试直接导出为 CSV 并保持原始数字格式，或将 `DataTable` 推入 Entity Framework Core 上下文进行批量数据库插入。这两种场景都基于我们这里讲解的相同基础。

If you found this guide helpful

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}