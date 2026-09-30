---
category: general
date: 2026-03-18
description: 如何在 C# 中将 Excel 数据导出到 DataTable，使用处理特定单元格的代码，将 Excel 转换为 DataTable 并格式化数字。了解导出特定单元格及更多内容。
draft: false
keywords:
- how to export excel
- convert excel to datatable
- export specific cells
- excel to datatable c#
- excel range to datatable
language: zh
og_description: 如何在 C# 中将 Excel 数据导出到 DataTable。本教程展示了如何导出特定单元格、将 Excel 转换为 DataTable，以及轻松格式化数字。
og_title: 如何在 C# 中将 Excel 导出为 DataTable – 完整指南
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: 如何在 C# 中将 Excel 导出为 DataTable – 步骤指南
url: /zh/net/excel-data-import-export/how-to-export-excel-to-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中将 Excel 导出为 DataTable – 步骤指南

是否曾经想过 **如何导出 Excel** 数据到 `DataTable` 而不丢失格式？你并不是唯一有此需求的人——开发者经常需要将电子表格的一部分加载到内存中，以便进行报表、校验或批量插入操作。好消息是，只需几行 C# 代码就可以导出精确的范围（例如 *A1:F11*），强制每个单元格都作为字符串处理，甚至还能应用自定义数字格式。

在本教程中，我们将覆盖你需要了解的所有内容：从加载工作簿、配置 **导出特定单元格**、将范围转换为 `DataTable`，到处理空行或地区依赖数字等边缘情况。完成后，你将拥有一个可复用的方法，能够在生产代码中应对 **excel to datatable c#** 场景。

> **先决条件** – 你需要 Aspose.Cells for .NET 库（或任何提供 `ExportDataTable` 的类似 API）。示例假设使用 .NET 6+，但概念同样适用于更早的版本。

---

## 你将学到的内容

- 如何使用 Aspose.Cells **将 Excel 转换为 DataTable**。
- 在导出时将所有值视为字符串的自定义范围导出（`excel range to datatable`）。
- 在导出过程中应用两位小数的数字格式（`#,#00.00`）。
- 常见陷阱（空行、隐藏列）以及如何规避。
- 一个可直接复制、完整可运行的代码示例。

---

## 先决条件和环境搭建

在编写代码之前，请确保你已经：

1. 通过 NuGet 安装 **Aspose.Cells for .NET**：

   ```bash
   dotnet add package Aspose.Cells
   ```

2. 将 Excel 文件（`input.xlsx`）放置在可引用的文件夹中，例如 `YOUR_DIRECTORY/input.xlsx`。
3. 项目目标为 .NET 6 或更高版本（下面的 `using` 语句可直接使用）。

> **专业提示**：如果你使用的是其他库（例如 EPPlus 或 ClosedXML），思路保持不变——加载工作簿、选择范围，然后调用返回 `DataTable` 的方法。

---

## 步骤 1：加载工作簿并获取第一个工作表

首先需要一个代表 Excel 文件的 `Workbook` 对象。获取后，你可以通过索引或名称访问任意工作表。

```csharp
using Aspose.Cells;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];

            // Continue with export options...
        }
    }
}
```

**为什么重要**：提前加载工作簿可以让你检查其结构（隐藏工作表、保护等），再决定导出哪些单元格。如果文件很大，考虑使用 `LoadOptions` 只流式读取所需部分。

---

## 步骤 2：配置导出选项 – 将所有值视为字符串

在将数据导出用于下游处理（例如批量插入 SQL）时，通常希望拥有 **一致的字符串表示**，以避免后续的类型不匹配错误。

```csharp
// Configure export behavior
ExportTableOptions exportOptions = new ExportTableOptions
{
    // Force every cell to be returned as a string, regardless of its original type
    ExportAsString = true,

    // Apply a two‑decimal‑place format to numeric cells
    NumberFormat = "#,##0.00"
};
```

**说明**：  
- `ExportAsString = true` 告诉 Aspose.Cells 忽略原始单元格类型，返回格式化后的文本。  
- `NumberFormat = "#,##0.00"` 确保像 `1234.5` 这样的数字会变为 `"1,234.50"`——对财务报表非常有用。

如果需要保留原始数据类型，只需将 `ExportAsString` 设置为 `false`，自行处理转换。

---

## 步骤 3：导出特定范围 (A1:F11) 到 DataTable

下面进入 **导出特定单元格** 的核心。`ExportDataTable` 方法接受起始/结束行列索引（从 0 开始）以及是否包含表头的标志。

```csharp
// Export cells A1:F11 (rows 0‑10, columns 0‑5) including the header row
DataTable table = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    endRow: 10,
    endColumn: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

**得到的结果**：一个包含 11 行（含表头）和 6 列（`A`‑`F`）的 `DataTable`。所有值均按 `exportOptions` 中的设置进行字符串格式化。

---

## 步骤 4：验证结果 – 打印到控制台

在将表格交给其他组件之前，最好先进行一次完整性检查。

```csharp
// Simple console dump
foreach (DataRow row in table.Rows)
{
    foreach (var item in row.ItemArray)
    {
        Console.Write($"{item}\t");
    }
    Console.WriteLine();
}
```

你应该会看到类似下面的输出：

```
Id      Name        Qty     Price   Total   Date
1       Widget A    10      2.50    25.00   2026-01-01
2       Widget B    5       3.75    18.75   2026-01-02
...
```

注意数值列显示了两位小数，正是我们指定的格式。

---

## 完整可运行示例（复制粘贴即用）

下面是把所有步骤串联起来的完整程序。将其放入新的控制台项目，修改文件路径后运行——无需额外配置。

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load workbook and select worksheet
            // -------------------------------------------------
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -------------------------------------------------
            // 2️⃣ Set export options – strings + number format
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                NumberFormat = "#,##0.00"
            };

            // -------------------------------------------------
            // 3️⃣ Export range A1:F11 (rows 0‑10, cols 0‑5)
            // -------------------------------------------------
            DataTable table = worksheet.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                endRow: 10,
                endColumn: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // -------------------------------------------------
            // 4️⃣ Output to console for verification
            // -------------------------------------------------
            Console.WriteLine("=== Exported DataTable ===");
            foreach (DataRow row in table.Rows)
            {
                foreach (var cell in row.ItemArray)
                {
                    Console.Write($"{cell}\t");
                }
                Console.WriteLine();
            }

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**代码要点**：

- `ExportTableOptions` 对象可复用；如果需要导出多个范围，可多次传入同一实例。
- 索引从 **0** 开始，因此 `A1` 对应 `(0,0)`。
- 将 `includeColumnNames` 设置为 `true` 会自动使用第一行作为列标题——这对后续的 `DataTable` 操作非常便利。

---

## 处理边缘情况与常见问题

### 如果工作表中有隐藏的行或列怎么办？

Aspose.Cells 默认会尊重可见性。如果需要导出隐藏的数据，可设置 `exportOptions.ExportHiddenRows = true` 和 `ExportHiddenColumns = true`。

### 我的 Excel 文件包含公式——会得到计算后的值吗？

会。默认情况下 `ExportDataTable` 返回 **显示的值**（公式的计算结果）。如果想要获取公式本身的文本，设置 `exportOptions.ExportFormulas = true` 即可。

### 如何跳过完全空白的行？

导出后，你可以对 `DataTable` 进行修剪：

```csharp
foreach (DataRow row in table.Rows.Cast<DataRow>()
                                   .Where(r => r.ItemArray.All(c => c == DBNull.Value || string.IsNullOrWhiteSpace(c.ToString()))).ToList())
{
    table.Rows.Remove(row);
}
```

### 能否导出非连续的范围（例如 A1:B5 和 D1:E5）？

Aspose.Cells 不支持在一次调用中导出不相连的范围。可以分别导出每个块，然后手动合并得到的 `DataTable`。

---

## 性能优化建议

- **复用 `ExportTableOptions`** 进行多次导出；每次新建实例虽然开销不大，但会让代码显得冗余。
- 使用 `LoadOptions` **流式读取大文件**，避免一次性将整个工作簿加载到内存。
- 如果仅需快速导出 CSV，**避免使用 `DataTable`**——`ExportDataTable` 虽然方便，但在处理超大表格时并非最省内存的方案。

---

## 结论

我们已经完整演示了 **如何将 Excel 导出为 DataTable**，包括格式控制、特定单元格范围的处理，以及确保所有值以字符串形式返回。完整示例展示了一种简洁、可投入生产的实现方式，能够轻松适配 **convert excel to datatable**、**export specific cells** 或任何 **excel range to datatable** 场景。

欢迎自行实验：更改导出范围、切换 `ExportAsString`，或直接将 `DataTable` 通过 Entity Framework 批量插入。只要掌握了这套基础，后续的可能性几乎无限。

---

### 后续步骤与相关主题

- **将 DataTable 导入回 Excel** – 了解使用 `ImportDataTable` 的逆向操作。  
- **将 DataTable 批量插入 SQL Server** – 使用 `SqlBulkCopy` 实现闪电般的加载速度。  
- **使用 EPPlus 或 ClosedXML** – 看看使用其他库时同样任务的实现方式。  
- **导出时的单元格格式化** – 深入探索 `ExportTableOptions`，包括日期格式、自定义文化设置等。

有疑问或其他使用场景？欢迎留言讨论，让我们一起持续交流。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}