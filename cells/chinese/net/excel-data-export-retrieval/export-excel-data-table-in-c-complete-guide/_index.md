---
category: general
date: 2026-03-21
description: 使用 Aspose.Cells 将 Excel 数据表导出为带标题的 DataTable，限制小数位数，并导出前 100 行。
draft: false
keywords:
- export excel data table
- export excel to datatable
- limit decimal places excel
- export first 100 rows
- export excel with headers
language: zh
og_description: 学习如何将 Excel 数据表导出为 DataTable，保留标题，限制小数位数，并在 C# 中获取前 100 行。
og_title: 在 C# 中导出 Excel 数据表 – 步骤指南
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: 在 C# 中导出 Excel 数据表 – 完整指南
url: /zh/net/excel-data-export-retrieval/export-excel-data-table-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 导出 Excel 数据表 – 完整 C# 演练

需要将工作簿中的 **export excel data table** 导出为 .NET `DataTable` 吗？您来对地方了——本指南将准确演示如何实现此操作，保留列标题，限制小数位数，并仅提取前 100 行。  

如果您曾盯着电子表格并想，“如何在不丢失格式的情况下将其导入我的应用？” 那么您并不孤单。接下来几分钟，我们将把这种“假设”转化为一个具体的、可复制粘贴的解决方案，使用 Aspose.Cells——一个流行的 Excel 操作库。

## 您将学到

- 如何使用 `ExportDataTable` 方法 **export excel to datatable**。  
- 如何保留原始列名（`export excel with headers`）。  
- 如何通过配置 `ExportTableOptions` 来 **limit decimal places excel** 值。  
- 如何安全地仅检索前 100 行（`export first 100 rows`）。  

无需外部脚本，无需神奇字符串——只需普通的 C# 代码，您可以将其放入任何 .NET 项目中。

## 前置条件

| 要求 | 原因 |
|------|------|
| .NET 6 或更高（或 .NET Framework 4.7+） | Aspose.Cells 两者皆支持，但更新的运行时提供异步就绪的 API。 |
| Aspose.Cells for .NET NuGet 包 | 提供 `Workbook`、`ExportTableOptions` 和 `ExportDataTable` 辅助方法。 |
| 示例 Excel 文件（例如 `Numbers.xlsx`） | 您将导出数据的来源。 |
| 基本的 C# 知识 | 您将跟随代码片段学习，但不需要任何高级技巧。 |

如果上述内容有陌生之处，请使用 `dotnet add package Aspose.Cells` 获取 NuGet 包，并创建一个包含少量数字的简易 Excel 文件——作为测试数据。

![导出 excel 数据表示例](excel-data-table.png "将导出到 DataTable 的 Excel 表格截图")

## 步骤 1：加载工作簿（export excel data table）

您首先需要的是指向 Excel 文件的 `Workbook` 实例。可以把它想象成在阅读章节之前先打开一本书。

```csharp
using Aspose.Cells;

// 1️⃣ Load the workbook that contains the source data
Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");
```

> **为什么这很重要：** 加载工作簿后，您即可访问其工作表、单元格和样式。如果文件路径错误，Aspose 将抛出 `FileNotFoundException`，因此请再次确认文件位置。

## 步骤 2：配置导出选项 – limit decimal places excel

默认情况下，Aspose 会以完整精度导出所有数值。通常您只需要少量有效数字，尤其是在将数据提供给 UI 网格或需要四舍五入数字的 API 时。

```csharp
using Aspose.Cells;

// 2️⃣ Configure export options – keep only 4 significant digits
ExportTableOptions exportOptions = new ExportTableOptions
{
    // This property trims the number of significant digits.
    SignificantDigits = 4
};
```

> **专业提示：** 如果需要不同的舍入策略（例如，总是向上取整），可以在导出后对 `DataTable` 进行后处理。`SignificantDigits` 设置是 **limit decimal places excel** 的最快方法，无需编写额外循环。

## 步骤 3：导出所需范围（export first 100 rows）

现在我们告诉 Aspose 将哪块单元格导入到 `DataTable`。在本教程中，我们获取前 100 行和前 10 列，但您可以根据实际情况调整这些数字。

```csharp
using System.Data;
using Aspose.Cells;

// 3️⃣ Export a block of cells (first 100 rows × 10 columns) to a DataTable
DataTable dataTable = workbook.Worksheets[0].Cells.ExportDataTable(
    startRow: 0,          // zero‑based index, first row
    startColumn: 0,       // first column (A)
    totalRows: 100,       // export only the first 100 rows
    totalColumns: 10,     // and the first 10 columns
    exportColumnNames: true, // keep column headers (export excel with headers)
    options: exportOptions);
```

> **边缘情况：** 如果工作表少于 100 行，Aspose 将仅导出实际存在的内容，不会抛出错误。不过，您可能希望防范意外过小的范围：

```csharp
int rowsToExport = Math.Min(100, workbook.Worksheets[0].Cells.MaxDataRow + 1);
```

## 步骤 4：验证结果 – 快速控制台输出

在调试器中查看数据固然不错，但将几行数据打印到控制台可以确认 **export excel to datatable** 已成功执行，并且小数位已被截断。

```csharp
static void PrintDataTable(DataTable table)
{
    foreach (DataRow row in table.Rows)
    {
        foreach (var item in row.ItemArray)
            Console.Write($"{item}\t");
        Console.WriteLine();
    }
}

// Call the helper
PrintDataTable(dataTable);
```

### 预期输出

```
ID      Name    Score   Ratio   Date        ...
1       Alice   95.12   0.8234  2023-01-15  ...
2       Bob     88.5    0.7612  2023-01-16  ...
3       Carol   73.33   0.6721  2023-01-17  ...
...
```

请注意，数值列现在仅显示四位有效数字，符合我们之前设置的 `SignificantDigits = 4`。

## 步骤 5：完整封装 – 可运行的完整示例

下面是完整的程序，您可以复制粘贴到控制台应用中。它包含错误处理、可选的行数检查以及用于打印的辅助方法。

```csharp
using System;
using System.Data;
using Aspose.Cells;

class ExportExcelDemo
{
    static void Main()
    {
        try
        {
            // 👉 Load the workbook
            Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");

            // 👉 Set up export options (limit decimal places excel)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                SignificantDigits = 4
            };

            // 👉 Determine safe row count (export first 100 rows)
            int maxRows = workbook.Worksheets[0].Cells.MaxDataRow + 1;
            int rowsToExport = Math.Min(100, maxRows);

            // 👉 Export to DataTable (export excel to datatable, export excel with headers)
            DataTable dt = workbook.Worksheets[0].Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: rowsToExport,
                totalColumns: 10,
                exportColumnNames: true,
                options: exportOptions);

            // 👉 Show a glimpse of the data
            PrintDataTable(dt);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }

    static void PrintDataTable(DataTable table)
    {
        foreach (DataRow row in table.Rows)
        {
            foreach (var item in row.ItemArray)
                Console.Write($"{item}\t");
            Console.WriteLine();
        }
    }
}
```

运行程序后，您将看到工作表的前 100 行，已圆整且列名保持完整。

## 常见问题与注意事项

| 问题 | 答案 |
|------|------|
| **如果我的工作表有合并单元格怎么办？** | `ExportDataTable` 通过取左上角单元格的值来展平合并单元格。如果需要自定义处理，请先取消合并或读取原始 `Cell` 对象。 |
| **我可以导出到 `DataSet` 吗？** | 可以——使用 `ExportDataTable` |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}