---
category: general
date: 2026-03-22
description: 如何导出带格式的 Excel 并保留数字格式。学习转换 Excel 区域、获取公式结果，以及使用 Aspose.Cells 导出带格式的
  Excel。
draft: false
keywords:
- how to export excel
- preserve number format
- convert excel range
- get formula result
- export excel with formatting
language: zh
og_description: 如何导出带格式的 Excel 并保留数字格式。一步步指南，转换 Excel 区域、获取公式结果，并在 C# 中导出带格式的 Excel。
og_title: 如何导出带格式的 Excel – 保留数字格式
tags:
- C#
- Aspose.Cells
- Excel automation
title: 如何导出带格式的Excel – 保留数字格式
url: /zh/net/number-and-display-formats-in-excel/how-to-export-excel-with-formatting-preserve-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何导出 Excel 并保留格式 – 保持数字格式

是否曾想过 **如何导出 Excel** 数据，同时保持每个单元格的外观与工作簿中看到的一模一样？也许您需要将报告发送给客户、填充网格控件，或仅仅将数值存入数据库。通常遇到的问题是数字格式丢失或公式变成原始字符串。  

在本教程中，我们将逐步演示一个完整、可直接运行的 C# 示例，**保留数字格式**、**将 Excel 区域转换为 `DataTable`**、**获取公式结果**，并最终使用 Aspose.Cells **导出带格式的 Excel**。结束时，您将拥有一个可以在任何项目中直接使用、接受工作表引用的单一方法。

> **快速预览：** 代码创建工作簿，写入一个数值和一个公式，指示 Aspose.Cells 将单元格导出为格式化字符串，并打印 `123.456 | 246.912` —— 正是您在 Excel 中期望看到的结果。

---

## 您需要的条件

- **Aspose.Cells for .NET**（免费试用版足以用于学习）
- .NET 6.0 或更高版本（在 .NET Framework 上 API 相同）
- 基本的 C# 开发环境（Visual Studio、VS Code、Rider…自行选择）

不需要除 Aspose.Cells 之外的额外 NuGet 包。如果您尚未安装，请运行：

```bash
dotnet add package Aspose.Cells
```

---

## Step 1 – 创建工作簿并写入数值（包括公式）

首先我们新建一个工作簿，并在 **A1** 中写入数值。随后在 **B1** 添加一个简单公式，将第一个单元格的值乘以二。这为后面演示 **获取公式结果** 做准备。

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a numeric value and a formula that uses it
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Continue with export options...
        ExportRangeAsDataTable(worksheet);
    }
}
```

**为何重要：**  
- `PutValue` 存储原始数字，而 `PutFormula` 存储计算公式。  
- Aspose.Cells 保持公式 **活跃**，因此当我们随后获取单元格的值时，实际得到的是 `246.912`，而不是字符串 `"=A1*2"`。

---

## Step 2 – 告诉 Aspose.Cells 将数值导出为格式化字符串

如果直接使用默认设置调用 `ExportDataTable`，数值单元格将以其底层 `double` 值返回。这会去除千位分隔符、货币符号或自定义小数位等格式。`ExportTableOptions` 类让我们 **保留数字格式** 并 **导出为字符串**。

```csharp
static void ExportRangeAsDataTable(Worksheet worksheet)
{
    // Step 2: Set export options to retrieve values as formatted strings
    ExportTableOptions exportOptions = new ExportTableOptions
    {
        ExportAsString = true,          // Return values as strings
        ExportNumberFormat = true      // Preserve the cell's number format
    };

    // Step 3: Export the range A1:B1 to a DataTable
    DataTable dataTable = worksheet.Cells.ExportDataTable(
        firstRow: 0,
        firstColumn: 0,
        totalRows: 1,
        totalColumns: 2,
        includeColumnNames: true,
        options: exportOptions);

    PrintDataTable(dataTable);
}
```

**关键点：** `ExportNumberFormat = true` 是实现 **保留数字格式** 的开关。若不设置此标志，您将看到 `"123.456"` 和 `"246.912"` 这类原始数字，在代码中看似正常，但粘贴到需要 Excel 相同格式的 UI 时就会出现问题。

---

## Step 3 – 打印导出的数据（验证）

现在我们拥有一个包含格式化字符串的 `DataTable`，把内容输出到控制台即可。这也演示了我们成功 **获取公式结果**，而无需自行计算公式。

```csharp
static void PrintDataTable(DataTable table)
{
    // Step 4: Print the exported values (already formatted)
    foreach (DataRow row in table.Rows)
    {
        // The output will look like: 123.456 | 246.912
        Console.WriteLine($"{row[0]} | {row[1]}");
    }
}
```

运行程序后输出：

```
123.456 | 246.912
```

请注意第二列显示的是 **公式结果**，而不是公式文本。这正是您在 **导出带格式的 Excel** 进行下游处理时所需要的。

---

## Step 4 – 转换更大范围的 Excel（可选）

上面的示例仅处理了 `A1:B1` 的小片段，但实际场景常常需要导出整张表。相同的方法适用于任何矩形区域——只需调整 `firstRow`、`firstColumn`、`totalRows` 和 `totalColumns` 参数即可。

```csharp
// Example: Export a 10‑row by 5‑column block starting at C3
DataTable bigTable = worksheet.Cells.ExportDataTable(
    firstRow: 2,          // Zero‑based index (C3 = row 2, column 2)
    firstColumn: 2,
    totalRows: 10,
    totalColumns: 5,
    includeColumnNames: true,
    options: exportOptions);
```

**小技巧：** 如果工作表已经有标题行，请将 `includeColumnNames` 设置为 `true`。Aspose.Cells 会把该范围的第一行作为列名，这在后续将 `DataTable` 绑定到 UI 网格时非常方便。

---

## Step 5 – 常见陷阱及规避方法

| 问题 | 产生原因 | 解决方案 |
|-------|----------------|-----|
| **数字失去逗号或货币符号** | `ExportAsString` 为 `false` 或未设置 `ExportNumberFormat` | 同时设置 `ExportAsString = true` **以及** `ExportNumberFormat = true`。 |
| **公式单元格返回公式文本** | 导出前未调用 `CalculateFormula`（仅在工作簿未开启自动计算时需要） | 启用自动计算 (`workbook.CalculateFormula()`) 或使用 `ExportAsString` 强制求值。 |
| **标题行被当作数据行** | `includeColumnNames` 为 `false`，但范围包含标题行 | 将 `includeColumnNames` 设置为 `true`，将首行视为列名。 |
| **大范围导致内存压力** | 一次性导出整张工作表会将所有数据加载到内存 | 分块导出（例如每次 500 行），必要时合并 `DataTable`。 |

---

## Step 6 – 完整可运行示例（复制粘贴即用）

下面是完整程序代码，从 `using` 语句到 `Main`。粘贴到控制台应用并按 **F5** 运行，即可立即看到格式化输出。

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate cells
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Export options: keep formatting and return strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            ExportNumberFormat = true
        };

        // Export A1:B1 as a DataTable
        DataTable dataTable = worksheet.Cells.ExportDataTable(
            firstRow: 0,
            firstColumn: 0,
            totalRows: 1,
            totalColumns: 2,
            includeColumnNames: true,
            options: exportOptions);

        // Print results
        foreach (DataRow row in dataTable.Rows)
        {
            Console.WriteLine($"{row[0]} | {row[1]}"); // Expected: "123.456 | 246.912"
        }

        // Keep console window open
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**预期输出**

```
123.456 | 246.912

Press any key to exit...
```

这就是完整的 **如何导出 Excel** 工作流，保持格式完整、公式已求值，并得到可供任何 .NET 消费者使用的干净 `DataTable`。

---

## 结论

我们已经覆盖了关于 **如何导出 Excel** 数据、**保留数字格式**、**将 Excel 区域转换为 `DataTable`**，以及 **获取公式结果** 而无需额外解析的全部要点。关键在于 `ExportTableOptions` 配置——只要将 `ExportAsString` 与 `ExportNumberFormat` 均设为 `true`，Aspose.Cells 就会为您完成繁重的工作。

接下来您可以：

- 将 `DataTable` 插入到 WPF `DataGrid` 或 ASP.NET MVC 视图中。
- 将表写入 CSV 文件，同时保持完全相同的视觉表现。
- 将此方法扩展到多工作表或动态范围。

欢迎尝试不同的格式（货币、百分比）以及更大的数据块。如果遇到任何异常，请回顾 **常见陷阱** 表格——它涵盖了在 **导出带格式的 Excel** 时最常见的问题。

祝编码愉快，愿您导出的电子表格始终如原始文件般精致！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}