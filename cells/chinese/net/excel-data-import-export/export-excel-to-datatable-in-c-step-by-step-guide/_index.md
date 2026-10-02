---
category: general
date: 2026-03-25
description: 快速学习如何在 C# 中将 Excel 导出为 DataTable。本教程涵盖带列名的 Excel 导出以及将 Excel 数据导出为字符串，以实现可靠的数据处理。
draft: false
keywords:
- export excel to datatable
- how to export excel to datatable
- export excel with column names
- export excel data as string
language: zh
og_description: 在 C# 中将 Excel 导出为 DataTable，保留列名并进行字符串转换。请遵循本简明教程，获取可直接运行的解决方案。
og_title: 在 C# 中将 Excel 导出为 DataTable – 完整指南
tags:
- C#
- Aspose.Cells
- DataTable
- Excel
title: 在 C# 中将 Excel 导出为 DataTable – 步骤指南
url: /zh/net/excel-data-import-export/export-excel-to-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将 Excel 导出到 DataTable（C#）——逐步指南

是否曾经需要 **export Excel to DataTable**，却不确定该打开哪些标志？你并不孤单——很多开发者在首次尝试将电子表格数据拉入 `DataTable` 时都会遇到同样的难题。  

好消息是，只需几行代码，你就可以 **export Excel with column names**，甚至 **export Excel data as string**，从而避免类型不匹配的烦恼。下面提供了完整、可运行的示例以及每个设置背后的“原因”，帮助你在任何项目中轻松适配，无需猜测。

## 本教程涵盖内容

* 如何在内存中创建工作簿（无需物理文件）。  
* 填充几行示例数据，以便立即看到结果。  
* 配置 `ExportTableOptions`，使每个单元格都被视为字符串。  
* 将矩形范围导出到 `DataTable`，并保留首行为列标题。  
* 验证输出并将首行打印到控制台。  

无需外部文档链接——所有内容都在这里。如果你已经有一个磁盘上的 Excel 文件，只需将工作簿创建行替换为 `new Workbook("path/to/file.xlsx")` 即可使用。

---

## 第 1 步：设置项目并添加 Aspose.Cells NuGet 包

在编写任何代码之前，确保你的项目引用了 **Aspose.Cells for .NET**（提供 `Workbook` 类的库）。可以通过 NuGet 包管理器添加：

```bash
dotnet add package Aspose.Cells
```

> **专业提示：** 使用最新的稳定版本（截至 2026 年 3 月，版本为 22.12），以获取最新的错误修复和性能改进。

---

## 第 2 步：创建工作簿并填充示例数据

我们将从一个全新的 `Workbook` 开始，并写入几行数据，以便你看到导出效果。此步骤还演示了 **how to export excel to datatable**，当源数据仅存在于内存中时的做法。

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();                 // in‑memory workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Populate a few cells – this mimics a real Excel file
        worksheet.Cells["A1"].PutValue("Name");   // column header
        worksheet.Cells["B1"].PutValue("Age");    // column header
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);
```

*为什么重要：* 先插入标题行（`A1` & `B1`），随后即可让导出器将首行视为列名——这正是 **export excel with column names** 所指的含义。

---

## 第 3 步：告诉 Aspose.Cells 将每个单元格视为字符串

在导出数值或日期单元格时，Aspose 会尝试推断 .NET 类型。如果下游代码期望字符串，这可能导致细微的错误。`ExportTableOptions.ExportAsString` 标志会强制统一的字符串转换。

```csharp
        // 3️⃣ Configure export options – all values will be strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true       // <-- ensures Export Excel Data As String
        };
```

*为何使用它？* 想象一下某列有时是数字有时是文本（例如 “00123” 与 “ABC”）。将所有内容导出为字符串可以避免丢失前导零或触发类型转换异常。

---

## 第 4 步：将所需范围导出到 DataTable

现在我们真正 **export excel to datatable**。`ExportDataTable` 方法接受起始行/列、行数/列数、列名提取标志以及我们刚构建的选项。

```csharp
        // 4️⃣ Export rows 0‑9 and columns 0‑4 (adjust as needed)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,   // <-- uses the first row as headers
            exportOptions: exportOptions);
```

*内部发生了什么？*  
- `startRow: 0` 指向 Excel 的第一行（标题行）。  
- `exportColumnNames: true` 告诉 Aspose 将 “Name” 与 “Age” 提取为 `DataTable` 的列集合。  
- `totalRows`/`totalColumns` 可以大于实际数据；多余的单元格会因 `ExportAsString` 而变为空字符串。

---

## 第 5 步：验证结果 – 打印首行

快速的控制台转储可以证明转换成功且列名完整。

```csharp
        // 5️⃣ Show the first data row (if any)
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

**预期输出**

```
First row: Alice, 30
```

如果你更改了示例数据，控制台会自动反映这些变化——无需额外代码。

---

## 常见问题与边缘情况

| Question | Answer |
|----------|--------|
| **我可以导出已经存在于磁盘上的工作表吗？** | 可以——将 `new Workbook()` 替换为 `new Workbook("myFile.xlsx")`。其余步骤保持不变。 |
| **如果我的 Excel 文件包含合并单元格怎么办？** | 合并单元格会被展开；左上角单元格的值会用于整个合并范围。 |
| **我需要担心特定文化的数字格式吗？** | 当 `ExportAsString = true` 时不需要；所有内容都会以 Excel 中显示的原始字符串形式出现。 |
| **一次可以导出多少行？** | Aspose.Cells 能处理数百万行，但 `DataTable` 的大小会随内存消耗增长。如果达到限制，请考虑分页。 |
| **隐藏列会被导出吗？** | 除非在 `ExportTableOptions` 中将 `ExportHiddenColumns = false`，否则隐藏列会被导出。 |

---

## 进阶：导出为 CSV 而非 DataTable

有时你可能更倾向于平面文件。相同的 `ExportTableOptions` 可与 `ExportDataTableToCSV` 结合使用：

```csharp
        string csvPath = "output.csv";
        worksheet.Cells.ExportDataTableToCSV(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            csvPath,
            exportColumnNames: true,
            exportOptions);
        Console.WriteLine($"CSV written to {csvPath}");
```

这行代码即可生成可直接导入的 CSV，同时仍然 **export excel data as string**。

---

## 完整可运行示例（复制粘贴即用）

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate sample data (header + two rows)
        worksheet.Cells["A1"].PutValue("Name");
        worksheet.Cells["B1"].PutValue("Age");
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);

        // Export everything as strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true
        };

        // Export range to DataTable (first row = column names)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,
            exportOptions: exportOptions);

        // Display first row
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

运行程序（`dotnet run`），你将看到 **export excel to datatable** 结果打印在控制台。替换示例数据、修改 `totalRows`/`totalColumns`，或将工作簿指向真实文件——一切都能平滑扩展。

---

## 结论

你现在拥有一个 **complete, self‑contained solution for exporting Excel to DataTable**（完整、独立的 Excel 导出到 DataTable 解决方案）在 C# 中。通过配置 `ExportTableOptions.ExportAsString`，你可以保证 **export excel data as string**，并通过设置 `exportColumnNames: true` 获得在 **export excel with column names** 时期望的列标题。  

接下来你可以：

* 将 `DataTable` 传入 Entity Framework 或 Dapper 进行批量插入。  
* 将其交给像 **FastReport** 或 **RDLC** 这样的报表引擎。  
* 将其转换为 JSON 供 API 响应使用（`JsonConvert.SerializeObject(table)`）。

尽情实验吧——可以尝试导出更大的工作表，或结合 **how to export excel to datatable** 从网络共享导出。模式保持不变，代码已准备好投入生产。

![Excel → DataTable 转换流程图 – export excel to datatable](https://example.com/placeholder.png "export excel to datatable diagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}