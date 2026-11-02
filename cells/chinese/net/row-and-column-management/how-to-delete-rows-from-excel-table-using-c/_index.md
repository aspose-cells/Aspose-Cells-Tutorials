---
category: general
date: 2026-09-27
description: 学习如何在 C# 中删除 Excel 表格的行，配有一步步的指南，并展示如何快速加载 Excel 工作簿（C#）。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from Excel table
- load Excel workbook C#
language: zh
lastmod: 2026-09-27
og_description: 在 C# 中删除 Excel 表格的行，并提供清晰示例。本教程还涵盖如何在 C# 中加载 Excel 工作簿以及处理常见的边缘情况。
og_image_alt: Screenshot illustrating delete rows from Excel table using C# code
og_title: 在 C# 中从 Excel 表格删除行 – 完整代码指南
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  headline: How to delete rows from Excel table using C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  name: How to delete rows from Excel table using C#
  steps:
  - name: What if the table has a different name or position?
    text: '* **Named table:** Use `ws.ListObjects["MyTableName"]` instead of the index.
      * **Multiple tables:** Loop through `ws.ListObjects` and pick the one that matches
      a condition (e.g., column header names). * **Dynamic row count:** You can compute
      `rowCount` at runtime by inspecting `ws.ListObjects[0].Dat'
  - name: Edge‑case handling
    text: '| Situation | Recommended code change | |----------------------------------------|--------------------------------------------------------------|
      | Table is empty or has fewer rows | Check `ws.ListObjects[0].DataRange.RowCount`
      before deleting. | | Rows to delete exceed table size | Clamp `rowCount`'
  - name: How do I delete rows from **all** tables in a workbook?
    text: '```csharp foreach (Worksheet sheet in workbook.Worksheets) { foreach (ListObject
      tbl in sheet.ListObjects) { // Example: delete the first data row of each table
      if (tbl.DataRange.RowCount > 1) tbl.DeleteRows(1, 1); } } ```'
  - name: Can I delete rows based on a **cell value**?
    text: 'Yes. Scan the `DataRange` for matching cells, collect their zero‑based
      indices, then delete in descending order:'
  - name: What if I need to **preserve formatting**?
    text: '`DeleteRows` removes the entire row from the table but retains the table’s
      style for remaining rows. If you need to keep specific formatting on a row you’re
      deleting, copy the style to another row before deletion.'
  - name: Does this work with **.xls** (Excel 97‑2003) files?
    text: Yes. Aspose.Cells automatically detects the file format, so the same code
      works with `.xls`. Just change the file extension in the `Workbook` constructor.
  - name: Next steps
    text: '* Explore **ClosedXML** or **EPPlus** if you prefer a fully open‑source
      stack. * Combine row deletion with **data validation** to clean spreadsheets
      before importing into a database. * Automate the process for a folder of workbooks
      using `Directory.GetFiles` and a loop.'
  type: HowTo
tags:
- Excel
- C#
- .NET
title: 如何使用 C# 删除 Excel 表格中的行
url: /zh/net/row-and-column-management/how-to-delete-rows-from-excel-table-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中删除 Excel 表格行 – 完整编程指南

如果您需要在 .xlsx 文件中**删除 Excel 表格行**，本教程将向您展示如何使用 C# 完成此操作。您将看到一个简洁、可运行的示例，加载 Excel 工作簿，删除第一个表格中的特定行，并保存结果。该方法适用于流行的 Aspose.Cells 库，也可以适配其他 .NET Excel API。

在清理导入数据、裁剪报告章节或自动化电子表格更新时，删除表格行是常见任务。阅读完本指南后，您将能够**加载 Excel 工作簿 C#**，定位表格（ListObject），删除任意行，并将修改后的文件写回磁盘。

## 前提条件

* 已安装 .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.7+）。
* 引用 **Aspose.Cells** NuGet 包（或任何提供 `Workbook`、`Worksheet` 和 `ListObject` 类型的兼容库）。
* 将名为 `input.xlsx` 的输入文件放置在项目可引用的文件夹中。
* 对 C# 语法和 Visual Studio（或您偏好的 IDE）有基本了解。

> **专业提示：** 如果您更倾向于开源方案，可以使用 **ClosedXML** 实现相同逻辑——只需将 Aspose 专用类替换为 `XLWorkbook`、`IXLWorksheet` 和 `IXLTable`。

## 步骤 1：在 C# 中加载 Excel 工作簿

第一步是将源文件读取到内存中。对于常规的电子表格大小，加载工作簿开销很小，并且可以完整访问工作表、表格和单元格值。

```csharp
using Aspose.Cells;

// Step 1: Load the workbook
// Replace YOUR_DIRECTORY with the actual folder path, e.g. @"C:\Data"
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

*为什么这很重要：* `Workbook` 解析 .xlsx 文件的 Open XML 结构，公开 `Worksheet` 对象集合。如果文件未找到，Aspose 会抛出 `FileNotFoundException`，因此请确保路径正确。

## 步骤 2：访问目标工作表

大多数电子表格包含多个工作表；您需要选择包含要修改的表格的那一页。这里我们使用第一张工作表（`Worksheets[0]`），这是简单文件的安全默认选择。

```csharp
// Step 2: Access the first worksheet
Worksheet ws = workbook.Worksheets[0];
```

*为什么这很重要：* `Worksheet` 是表格（`ListObjects`）的容器。访问正确的工作表可防止意外修改无关数据。

## 步骤 3：从 Excel 表格中删除行

Excel 表格由 `ListObject` 对象表示。工作表上的第一张表格是 `ListObjects[0]`。`DeleteRows(startIndex, rowCount)` 方法删除的是**相对于表格数据区域**的行，而不是工作表的绝对行号。  

在本例中，我们删除表格的第二行和第三行（标题行是第 0 行，因此从索引 1 开始）。

```csharp
// Step 3: Delete rows 1 and 2 from the first table (ListObject)
// The first row (index 0) is the header, so we start at index 1
ws.ListObjects[0].DeleteRows(1, 2);
```

### 如果表格有不同的名称或位置怎么办？

* **已命名表格：** 使用 `ws.ListObjects["MyTableName"]` 替代索引。
* **多个表格：** 遍历 `ws.ListObjects`，挑选符合条件的表格（例如列标题名称）。
* **动态行数：** 可以在运行时检查 `ws.ListObjects[0].DataRange.RowCount` 来计算 `rowCount`。

### 边缘情况处理

| 情况                              | 推荐的代码更改                                      |
|-----------------------------------|----------------------------------------------------|
| 表格为空或行数不足                | 在删除前检查 `ws.ListObjects[0].DataRange.RowCount`。 |
| 待删除的行数超过表格大小          | 将 `rowCount` 限制为 `DataRange.RowCount - startIndex`。 |
| 需要根据条件删除行（例如列 C 的值）| 遍历 `DataRange.Rows` 并收集匹配的索引，然后逆序删除以保持索引稳定。 |

## 步骤 4：保存修改后的工作簿

删除完成后，将工作簿写回新文件（或如果您愿意则覆盖原文件）。保存会生成一个反映更新后表格的全新 .xlsx。

```csharp
// Step 4: Save the modified workbook
workbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

*为什么这很重要：* `Save` 将内存中的表示序列化到磁盘。如果需要保留原始文件，请始终写入不同的路径。

## 完整、可运行的示例

将所有步骤组合在一起，即可得到一个可自行复制、粘贴并运行的完整程序。

```csharp
using System;
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Adjust the folder path as needed
        const string folder = @"YOUR_DIRECTORY";

        // Load the workbook (load Excel workbook C#)
        Workbook workbook = new Workbook($"{folder}\\input.xlsx");

        // Access the first worksheet
        Worksheet ws = workbook.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (ws.ListObjects.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Delete rows 1 and 2 from the first table (skip header)
        ListObject table = ws.ListObjects[0];
        int rowsToDelete = Math.Min(2, table.DataRange.RowCount - 1); // guard against short tables
        if (rowsToDelete > 0)
        {
            table.DeleteRows(1, rowsToDelete);
            Console.WriteLine($"Deleted {rowsToDelete} row(s) from table \"{table.Name}\".");
        }
        else
        {
            Console.WriteLine("Table does not have enough rows to delete.");
        }

        // Save the result
        workbook.Save($"{folder}\\output.xlsx");
        Console.WriteLine("Workbook saved as output.xlsx");
    }
}
```

**预期输出**（控制台）：

```
Deleted 2 row(s) from table "Table1".
Workbook saved as output.xlsx
```

打开 `output.xlsx` —— 第一个表格现在已没有您删除的行，而标题行仍然完整。

## 常见问题与变体

### 如何从工作簿中的**所有**表格删除行？

```csharp
foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (ListObject tbl in sheet.ListObjects)
    {
        // Example: delete the first data row of each table
        if (tbl.DataRange.RowCount > 1)
            tbl.DeleteRows(1, 1);
    }
}
```

### 能否根据**单元格值**删除行？

可以。扫描 `DataRange` 中匹配的单元格，收集其零基索引，然后按降序删除：

```csharp
var rowsToRemove = new List<int>();
for (int i = 0; i < table.DataRange.RowCount; i++)
{
    var cell = table.DataRange[i, 2]; // column C (zero‑based)
    if (cell.StringValue == "Obsolete")
        rowsToRemove.Add(i);
}

// Delete rows from bottom to top to keep indices valid
rowsToRemove.Sort((a, b) => b.CompareTo(a));
foreach (int rowIdx in rowsToRemove)
    table.DeleteRows(rowIdx, 1);
```

### 如果需要**保留格式**怎么办？

`DeleteRows` 会从表格中删除整行，但会保留其余行的表格样式。如果您需要保留被删除行的特定格式，请在删除前将样式复制到其他行。

### 这是否适用于 **.xls**（Excel 97‑2003）文件？

是的。Aspose.Cells 会自动检测文件格式，因此相同代码同样适用于 `.xls`。只需在 `Workbook` 构造函数中更改文件扩展名即可。

## 性能提示

* **批量删除：** 一行一行删除大量行会较慢。尽可能使用单次 `DeleteRows(start, count)` 调用。
* **避免阻塞 UI 线程：** 如果将此功能集成到桌面应用中，请在后台线程上运行工作簿操作，以保持 UI 响应。
* **正确释放资源：** 虽然 Aspose.Cells 使用托管内存，但在处理大文件时，建议将 `Workbook` 包裹在 `using` 块中，以及时释放资源。

## 结论

现在您拥有一个完整、可用于生产环境的示例，使用 C# **删除 Excel 表格行**。本指南介绍了如何**加载 Excel 工作簿 C#**，定位目标 `ListObject`，安全地删除行并保存更新后的文件。结合边缘情况处理和性能建议，您可以将此模式扩展到更复杂的场景，如条件删除、多个表格或其他 .NET Excel 库。

### 下一步

* 如果您偏好完全开源的技术栈，可探索 **ClosedXML** 或 **EPPlus**。
* 将行删除与 **数据验证** 结合，在导入数据库前清理电子表格。
* 使用 `Directory.GetFiles` 和循环，为文件夹中的工作簿自动化此过程。

随意尝试不同的行范围、表格名称和条件逻辑。祝编码愉快！

## 接下来应该学习什么？

以下教程涵盖与本指南技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能，并在项目中探索替代实现方案。

- [加载 Excel 文件 C# – 如何删除行并移除特定行](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)
- [使用 Aspose.Cells for .NET 在 Excel 中插入和删除行：全面指南](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [使用 Aspose.Cells .NET 删除 Excel 空白行进行数据清理](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}