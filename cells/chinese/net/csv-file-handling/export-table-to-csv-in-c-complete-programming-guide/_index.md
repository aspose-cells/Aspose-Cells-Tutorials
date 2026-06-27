---
category: general
date: 2026-06-27
description: 在 C# 中使用自定义 CSV 导出选项将表导出为 CSV。了解 TableExportOptions 和单元格导出处理程序如何让您为任何工作簿定制
  CSV 输出。
draft: false
keywords:
- export table to csv
- custom CSV export
- TableExportOptions
- cell export handler
- C# workbook to CSV
language: zh
og_description: 使用 C# 将表格导出为 CSV，并自定义 CSV 导出选项。本指南将带您了解 TableExportOptions、单元格导出处理程序以及完整代码示例。
og_title: 在 C# 中将表导出为 CSV – 完整编程指南
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Export table to CSV with custom CSV export options in C#. Learn how
    TableExportOptions and a cell export handler let you tailor CSV output for any
    workbook.
  headline: Export table to CSV in C# – Complete Programming Guide
  type: TechArticle
- description: Export table to CSV with custom CSV export options in C#. Learn how
    TableExportOptions and a cell export handler let you tailor CSV output for any
    workbook.
  name: Export table to CSV in C# – Complete Programming Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code works on .NET Framework 4.6+ as well). -
      A reference to the **GemBox.Spreadsheet** NuGet package (or any library exposing
      `TableExportOptions`). - Basic familiarity with C# and CSV concepts.'
  - name: Why `ExportAsString = true`?
    text: When you set `ExportAsString` to `true`, the library treats every cell as
      text before handing it to your handler. This guarantees that numeric cells don’t
      get auto‑formatted (e.g., scientific notation) before you have a chance to prepend
      the `$`. If you leave this flag `false`, the handler might rec
  - name: Understanding the **cell export handler**
    text: The lambda receives a `cell` object that carries metadata such as `Column`,
      `Row`, and `Value`. By checking `cell.Column == 1` we target the *Price* column
      only. The `double.TryParse` guard ensures we only format legitimate numbers—avoiding
      exceptions on empty or text cells.
  - name: Null or Empty Cells
    text: If your source data contains blanks, the handler will receive `null`. The
      guard clause `if (cell == null) return string.Empty;` prevents a `NullReferenceException`.
      You can also return a placeholder like `"N/A"` if that fits your business rules.
  - name: Large Workbooks
    text: 'When dealing with thousands of rows, consider streaming the CSV to avoid
      high memory consumption:'
  - name: Different Delimiters
    text: 'If you need a semicolon (`;`) instead of a comma, adjust the `SaveOptions`:'
  type: HowTo
tags:
- CSV
- C#
- Spreadsheet
title: 在 C# 中将表导出为 CSV – 完整编程指南
url: /zh/net/csv-file-handling/export-table-to-csv-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中将表导出为 CSV – 完整编程指南

是否曾经需要 **导出表为 CSV**，但默认的输出并不能满足需求？也许你想在前面添加货币符号、修改分隔符，或跳过某些列。在本教程中，我们将展示如何使用强大的 `TableExportOptions` 类和自定义 *单元格导出处理器* 来 **导出表为 CSV**——无需外部脚本。

我们将通过一个真实场景演示：对一个类似电子表格的工作簿进行处理，将第二列的每个值都显示为美元金额，然后将结果保存为 CSV 文件。完成后，你将拥有一个可复用的模式，适用于 C# 项目中任何 **自定义 CSV 导出** 的需求。

## 你将学到

- 如何使用 GemBox.Spreadsheet 库（或任何兼容的 API）设置 **C# 工作簿到 CSV** 的转换。  
- 为什么在需要基于字符串的输出时 `TableExportOptions.ExportAsString` 很重要。  
- 如何编写 **单元格导出处理器**，在导出时即时修改单元格值。  
- 处理空单元格、不同数据类型以及大数据集等边缘情况的技巧。  

### 前置条件

- .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.6+）。  
- 已引用 **GemBox.Spreadsheet** NuGet 包（或任何提供 `TableExportOptions` 的库）。  
- 对 C# 和 CSV 概念有基本了解。  

如果你满足以上条件，下面开始吧。

---

## 步骤 1：安装并引用 Spreadsheet 库

首先，将 GemBox.Spreadsheet 包添加到项目中。在解决方案文件夹的终端运行：

```bash
dotnet add package GemBox.Spreadsheet --version 131.0
```

> **小技巧：** GemBox 提供免费模式，支持最多 150 行——非常适合在购买许可证前进行实验。

包恢复完成后，在 `.cs` 文件顶部加入命名空间：

```csharp
using GemBox.Spreadsheet;
```

> **为什么重要：** `TableExportOptions` 类型位于该命名空间中，若缺少引用编译器会报错。

---

## 步骤 2：创建带数据的示例工作簿

我们构建一个小型工作簿，模拟典型的销售报告。这将为导出提供具体的示例数据。

```csharp
// Initialize the library (free mode)
SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

// Create a new workbook and a worksheet
var wb = new ExcelFile();
var ws = wb.Worksheets.Add("Sales");

// Populate header row
ws.Cells[0, 0].Value = "Product";
ws.Cells[0, 1].Value = "Price";

// Add a few data rows
ws.Cells[1, 0].Value = "Laptop";
ws.Cells[1, 1].Value = 999.99;

ws.Cells[2, 0].Value = "Mouse";
ws.Cells[2, 1].Value = 25.5;

ws.Cells[3, 0].Value = "Keyboard";
ws.Cells[3, 1].Value = 45.0;
```

单独运行此代码会生成一个普通的 Excel 文件。我们的目标是 **导出表为 CSV**，并在价格列前加上 `$` 前缀。

---

## 步骤 3：为自定义 CSV 导出配置 `TableExportOptions`

下面就是关键所在。`TableExportOptions` 让你控制每个单元格的渲染方式，决定数字是保持数值还是转为字符串，甚至可以自定义分隔符。

```csharp
// Step 3.1: Create export options for the table
var tableExportOptions = new TableExportOptions();

// Step 3.2: Export each cell's value as a string – essential for custom formatting
tableExportOptions.ExportAsString = true;

// Step 3.3: Define a custom handler to modify cell output
//         We prepend a dollar sign only for the second column (index 1)
tableExportOptions.CellExportHandler = (cell) =>
{
    // Guard against null cells – they become empty strings
    if (cell == null) return string.Empty;

    // If we are in the Price column, format as currency
    if (cell.Column == 1 && double.TryParse(cell.Value?.ToString(), out var price))
        return "$" + price.ToString("0.00");

    // Default: return the cell's string representation
    return cell.StringValue;
};
```

### 为什么要设置 `ExportAsString = true`？

将 `ExportAsString` 设为 `true` 后，库会在交给处理器之前把每个单元格当作文本处理。这样可以确保数值单元格不会在你添加 `$` 前被自动格式化（例如科学计数法）。如果保持 `false`，处理器可能收到数值类型，难以直接转换为带格式的字符串。

### 了解 **单元格导出处理器**

该 lambda 接收一个 `cell` 对象，包含 `Column`、`Row`、`Value` 等元数据。通过判断 `cell.Column == 1` 我们只针对 *Price* 列进行处理。`double.TryParse` 的判断确保只对合法数字进行格式化，避免在空单元格或文本单元格上抛异常。

---

## 步骤 4：使用自定义选项将工作簿保存为 CSV

现在我们终于可以 **导出表为 CSV**，并把自定义逻辑内置其中。

```csharp
// Define the output path – change this to your desired folder
string outputPath = Path.Combine(Environment.CurrentDirectory, "customSalesReport.csv");

// Save the worksheet as CSV using the options we configured
ws.Save(outputPath, SaveOptions.CsvDefault, tableExportOptions);

// Inform the user
Console.WriteLine($"CSV file created at: {outputPath}");
```

> **预期输出（`customSalesReport.csv`）：**  
> ```
> Product,Price  
> Laptop,$999.99  
> Mouse,$25.50  
> Keyboard,$45.00  
> ```

可以看到每个价格前都已加上 `$`——正是我们的 **单元格导出处理器** 所指示的效果。

---

## 步骤 5：处理边缘情况和常见陷阱

### 空或 Null 单元格

如果源数据中存在空白，处理器会收到 `null`。通过 `if (cell == null) return string.Empty;` 可以防止 `NullReferenceException`。如果业务需要，也可以返回 `"N/A"` 等占位符。

### 大型工作簿

处理成千上万行数据时，建议使用流式写入 CSV，以降低内存占用：

```csharp
using (var stream = new FileStream(outputPath, FileMode.Create, FileAccess.Write))
{
    ws.Save(stream, SaveOptions.CsvDefault, tableExportOptions);
}
```

### 不同分隔符

如果需要使用分号（`;`）而不是逗号，只需调整 `SaveOptions`：

```csharp
var csvOptions = SaveOptions.CsvDefault;
csvOptions.Separator = ';';
ws.Save(outputPath, csvOptions, tableExportOptions);
```

这就是 **自定义 CSV 导出** 的灵活示例。

---

## 步骤 6：完整可运行示例（复制粘贴即可）

下面是完整的程序代码。复制到新的控制台项目中运行——无需额外文件。

```csharp
using System;
using System.IO;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize GemBox (free mode)
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 2️⃣ Build a sample workbook
        var wb = new ExcelFile();
        var ws = wb.Worksheets.Add("Sales");

        ws.Cells[0, 0].Value = "Product";
        ws.Cells[0, 1].Value = "Price";

        ws.Cells[1, 0].Value = "Laptop";
        ws.Cells[1, 1].Value = 999.99;

        ws.Cells[2, 0].Value = "Mouse";
        ws.Cells[2, 1].Value = 25.5;

        ws.Cells[3, 0].Value = "Keyboard";
        ws.Cells[3, 1].Value = 45.0;

        // 3️⃣ Configure export options (custom CSV export)
        var tableExportOptions = new TableExportOptions
        {
            ExportAsString = true,
            CellExportHandler = (cell) =>
            {
                if (cell == null) return string.Empty;
                if (cell.Column == 1 && double.TryParse(cell.Value?.ToString(), out var price))
                    return "$" + price.ToString("0.00");
                return cell.StringValue;
            }
        };

        // 4️⃣ Save as CSV
        string outputPath = Path.Combine(Environment.CurrentDirectory, "customSalesReport.csv");
        ws.Save(outputPath, SaveOptions.CsvDefault, tableExportOptions);

        Console.WriteLine($"✅ CSV created at: {outputPath}");
    }
}
```

运行程序后，用任意文本编辑器打开 `customSalesReport.csv`，即可看到格式化后的输出。

---

## 结论

现在你已经掌握了在 C# 中 **导出表为 CSV** 的可靠、可复用模式。通过 `TableExportOptions` 与 **单元格导出处理器**，可以注入任意自定义逻辑——货币符号、日期格式、条件遮蔽，随你所需。该方法适用于小型报表，也能在配合流式写入时处理海量数据导出。

接下来可以尝试将 `$` 替换为其他前缀、将日期输出为 ISO 格式，或从同一工作簿的不同工作表生成多个 CSV 文件。相同的 **自定义 CSV 导出** 原则同样适用。

对多语言数据或特殊字符等边缘情况有疑问？欢迎在下方留言，祝编码愉快！

## 接下来你可以学习什么？

以下教程与本指南紧密相关，帮助你进一步掌握 API 功能并探索替代实现方式。

- [Load CSV & Export to JSON Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/import-export/load-csv-export-json-aspose-cells-dotnet/)
- [Export Excel Csv Blank Rows Aspose Cells Net](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)
- [Export Excel Csv Blank Rows Aspose Cells Net](/cells/spanish/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}