---
category: general
date: 2026-03-22
description: 自定义数字格式 Excel 教程，展示如何将数据表导入 Excel，设置列背景颜色，将列格式化为货币并将工作簿保存为 xlsx。
draft: false
keywords:
- custom number format excel
- import datatable to excel
- set column background color
- format column as currency
- save workbook as xlsx
language: zh
og_description: 自定义数字格式 Excel 教程，逐步演示导入 DataTable、设置列背景颜色、将列格式化为货币以及将工作簿保存为 xlsx。
og_title: C# 中的 Excel 自定义数字格式 – 步骤指南
tags:
- C#
- Excel automation
- Aspose.Cells
- Data export
title: C# 中的 Excel 自定义数字格式 – 完整指南
url: /zh/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 自定义数字格式 Excel – 全栈 C# 教程

有没有想过如何直接在 C# 中应用 **custom number format excel** 样式？也许你已经尝试将 `DataTable` 导出到电子表格，却只能看到普通数字，没有颜色，也没有货币格式。这是一个常见的痛点——尤其在需要为利益相关者提供精美报告时。

在本指南中我们将一起解决这个问题：你将学习如何 **import datatable to excel**、**set column background color**、**format column as currency**，以及最终 **save workbook as xlsx**，并使用自定义数字格式让你的数据更醒目。没有模糊的引用，只有完整、可直接复制粘贴到项目中的可运行解决方案。

---

## 你将构建的内容

完成本教程后，你将拥有一个独立的 C# 控制台应用程序，它能够：

1. 获取一个 `DataTable`（你可以将示例代码替换为自己的查询）。  
2. 使用 Aspose.Cells（或任何兼容库）创建一个新的 Excel 工作簿。  
3. 为第一列设置蓝色加粗字体，为第二列设置浅黄色背景，为第三列设置货币格式（`$#,##0.00`）。  
4. 将文件保存为 `DataTableWithStyleArray.xlsx`，保存位置由你自行选择。

你将看到每一行代码是如何影响最终 Excel 文件的，并且我们会讨论这些选择在可维护性和性能方面的意义。

---

## 前置条件

- .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.7+）。  
- Aspose.Cells for .NET（免费试用版或授权版）。通过 NuGet 安装：

```bash
dotnet add package Aspose.Cells
```

- 对 `DataTable` 和 C# 控制台应用有基本了解。

---

## 步骤 1：将源数据检索为 DataTable

首先，我们需要一些数据来导出。在真实场景中，你可能会调用仓库或执行 SQL 查询。这里为了演示，我们将在内存中创建一个简单的表。

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetSampleData()
{
    var table = new DataTable("Sales");
    table.Columns.Add("Product", typeof(string));
    table.Columns.Add("Quantity", typeof(int));
    table.Columns.Add("Revenue", typeof(decimal));

    table.Rows.Add("Widget A", 120, 3450.75m);
    table.Rows.Add("Widget B", 85, 2190.00m);
    table.Rows.Add("Widget C", 60, 1580.40m);

    return table;
}
```

> **为什么这很重要：** 使用 `DataTable` 能提供带模式的表格数据，能够干净地映射到 Excel 的行列上。它还让你能够在不重写代码的情况下复用相同的导出逻辑处理任何数据集。

---

## 步骤 2：创建新工作簿并获取第一个工作表

现在我们创建一个 Excel 工作簿。`Workbook` 类代表整个文件；其 `Worksheets[0]` 是默认工作表，我们将在这里放置数据。

```csharp
// Initialize a fresh workbook
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet
Worksheet worksheet = workbook.Worksheets[0];
```

> **小技巧：** 如果需要多个工作表，只需调用 `workbook.Worksheets.Add("SheetName")`，然后对每个工作表重复样式设置步骤。

---

## 步骤 3：定义列样式 – 字体、背景和数字格式

在 Aspose.Cells 中，样式通过 `Style` 对象实现。我们将构建一个数组，每个元素对应 `DataTable` 中的一列。

```csharp
// Prepare an array to hold three distinct styles
Style[] columnStyles = new Style[3];

// 1️⃣ First column – blue, bold font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = System.Drawing.Color.Blue;
columnStyles[0].Font.IsBold = true;

// 2️⃣ Second column – light‑yellow background
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
columnStyles[1].Pattern = BackgroundType.Solid;

// 3️⃣ Third column – custom currency format (custom number format excel)
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Custom = "$#,##0.00";
```

> **为什么使用样式数组？** 将数组传递给 `ImportDataTable` 可以在一次调用中为每列应用不同的样式，既简洁又高效。它还能保证格式与数据顺序保持同步。

---

## 步骤 4：在导入时应用样式导入 DataTable

下面是核心操作：我们将 `DataTable` 导入工作表，告诉 Aspose 包含标题行，并传入我们的 `columnStyles` 数组。

```csharp
// Import data starting at cell A1 (row 0, column 0)
worksheet.Cells.ImportDataTable(
    GetSampleData(),   // source DataTable
    true,              // include column names as header
    0, 0,              // start row, start column
    columnStyles);     // apply the style array
```

> **内部发生了什么？** Aspose 会遍历每一列，先写入标题，然后写入每行的值。与此同时，它会从数组中取出对应的 `Style` 并应用，因此你会得到“Product”列的蓝色标题、“Quantity”列的浅黄底色，以及格式化好的“Revenue”列。

---

## 步骤 5：将工作簿保存为 XLSX 文件

最后，我们将工作簿持久化到磁盘。`Save` 方法会根据文件扩展名自动选择 XLSX 格式。

```csharp
// Choose a folder that exists on your machine
string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";

// Ensure the directory exists (optional safety check)
System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);

// Save the workbook
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

> **提示：** 如果需要以流的方式输出文件（例如用于 Web API），请使用 `workbook.Save(stream, SaveFormat.Xlsx)` 而不是文件路径。

---

## 完整可运行示例

下面是完整的程序代码，你可以直接粘贴到新的控制台项目中。它可以直接编译运行，生成带样式的 Excel 文件。

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Get data
            DataTable dataTable = GetSampleData();

            // Step 2 – Create workbook & worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 3 – Prepare column styles
            Style[] columnStyles = new Style[3];

            // Font style for first column (blue, bold)
            columnStyles[0] = workbook.CreateStyle();
            columnStyles[0].Font.Color = System.Drawing.Color.Blue;
            columnStyles[0].Font.IsBold = true;

            // Background style for second column (light yellow)
            columnStyles[1] = workbook.CreateStyle();
            columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
            columnStyles[1].Pattern = BackgroundType.Solid;

            // Currency format for third column (custom number format excel)
            columnStyles[2] = workbook.CreateStyle();
            columnStyles[2].Custom = "$#,##0.00";

            // Step 4 – Import data with styles
            worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

            // Step 5 – Save as XLSX
            string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";
            System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }

        // Helper method to build a demo DataTable
        static DataTable GetSampleData()
        {
            var table = new DataTable("Sales");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Revenue", typeof(decimal));

            table.Rows.Add("Widget A", 120, 3450.75m);
            table.Rows.Add("Widget B", 85, 2190.00m);
            table.Rows.Add("Widget C", 60, 1580.40m);

            return table;
        }
    }
}
```

### 预期结果

打开 `DataTableWithStyleArray.xlsx` 后，你会看到：

| **产品**（蓝色，加粗） | **数量**（浅黄） | **收入**（货币） |
|------------------------|------------------|-----------------|
| Widget A               | 120              | $3,450.75       |
| Widget B               | 85               | $2,190.00       |
| Widget C               | 60               | $1,580.40       |

你指定的 **custom number format excel**（`$#,##0.00`）确保每个收入单元格都显示美元符号、千位分隔符以及两位小数——正是财务团队所期望的格式。

---

## 常见问题与边缘情况

### 我可以使用其他 Excel 库吗？

当然可以。创建每列样式并在导入时应用的思路同样适用于 EPPlus、ClosedXML 或 NPOI。API 调用会有所不同，但整体模式保持不变。

### 如果我的 DataTable 列数多于样式数组怎么办？

Aspose 会对没有匹配样式的列使用默认样式。为避免意外，建议将数组大小设为 `dataTable.Columns.Count`，或在循环中动态生成样式。

### 如何为日期设置自定义数字格式？

只需将 `style.Custom = "dd‑mm‑yyyy"`（或任意有效的 Excel 格式字符串）即可。相同的数组方式同样适用于日期、百分比或科学计数法。

### 导入后如何自动调整列宽？

调用 `worksheet.AutoFitColumns();` 即可在导入后自动计算并设置列宽。

### 大数据集（10 万行以上）怎么办？

`ImportDataTable` 已针对批量操作做了优化，但仍可能遇到内存限制。此时可以考虑手动逐行写入 `Cells[i, j].PutValue(...)`，并复用单个 `Style` 对象以降低开销。

---

## 实用技巧与常见陷阱

- **避免在生产代码中硬编码路径**；使用 `Environment.GetFolderPath` 或配置项获取路径。  
- **在长时间运行的服务中释放工作簿**——使用 `using` 块包装，以释放本机资源。  
- **留意文化特定的分隔符**。自定义格式 `$#,##0.00` 强制使用点号作为小数分隔符，无论操作系统区域设置为何，这通常是财务报表的期望。  
- **记得引用 System.Drawing**（在 .NET Core 上使用 `System.Drawing.Common`）以获取样式中使用的颜色结构体。  
- **在不同 Excel 版本上测试输出**；旧版本可能对某些自定义格式的解释略有差异。

---

## 结论

我们已经覆盖了从 C# **custom number format excel** 文件所需的全部内容：从 `DataTable` 中提取数据、**import datatable to excel**、**set column background color**、**format column as currency**，以及最终 **save workbook as x

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}