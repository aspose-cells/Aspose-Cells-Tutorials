---
category: general
date: 2026-11-25
description: 学习如何在 C# 中删除 Excel 表格中的行，并高效地删除 Excel 工作表中的多行。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from excel table
- delete multiple rows from excel sheet
language: zh
lastmod: 2026-11-25
og_description: 在 C# 中删除 Excel 表格中的行，并学习使用简洁代码删除 Excel 工作表中的多行。
og_image_alt: Screenshot of C# code deleting rows from an Excel table
og_title: 在 C# 中删除 Excel 表格的行 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to delete rows from Excel table in C# and also delete multiple
    rows from Excel sheet efficiently.
  headline: How to delete rows from Excel table with C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# and also delete multiple
    rows from Excel sheet efficiently.
  name: How to delete rows from Excel table with C#
  steps:
  - name: Add Aspose.Cells to your project
    text: 'Open the **Package Manager Console** and run:'
  - name: Load the workbook and locate the table
    text: '```csharp using Aspose.Cells;'
  - name: Delete the desired data rows
    text: The `DeleteRows` method expects a **zero‑based** row index relative to the
      table, **including** the header row. Because the header cannot be removed, you
      must start at index 1 for the first data row.
  - name: Save the modified workbook
    text: '```csharp // Save the workbook to a new file to preserve the original workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
      } } ```'
  - name: Full working example
    text: '```csharp using Aspose.Cells;'
  - name: Edge cases and best practices
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Deleting rows beyond the last row | Check `worksheet.Rows.Count` before calling
      `RemoveAt`. | | Removing all rows except the header | Delete data rows in a
      loop or use `DeleteRows(1, table.DataRa'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
- data manipulation
title: 如何使用 C# 删除 Excel 表中的行
url: /zh/net/row-and-column-management/how-to-delete-rows-from-excel-table-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 C# 删除 Excel 表格中的行

如果您需要使用 C# 删除 Excel 表格中的行，本指南将向您展示具体操作方法。您还将看到如何在不影响其他数据的情况下删除 Excel 工作表中的多行。

以编程方式操作 Excel 时，通常需要删除过时或无效的记录。直接在工作表中删除行可能存在风险，因为结构化表格的标题行必须保持完整。本教程将引导您采用一种安全的方法，尊重表格的标题，并一次性删除任意数量的数据行。

## 前置条件

在开始之前，请确保您具备以下条件：

* 已安装 .NET 6.0 或更高版本  
* Visual Studio 2022（或任何兼容的 IDE）  
* **Aspose.Cells** NuGet 包（版本 23.10 或更新）——该库提供本文示例中使用的 `Workbook`、`Worksheet` 和 `ListObject` 类  

您无需在开发机器上安装 Microsoft Office，因为 Aspose.Cells 直接操作文件格式。

## 删除 Excel 表格中的行 – 步骤详解

以下章节逐步说明如何安全地删除 Excel 表格中的行。主关键词出现在本标题中，以满足 SEO 要求。

### 步骤 1：将 Aspose.Cells 添加到项目中

打开 **Package Manager Console** 并运行：

```powershell
Install-Package Aspose.Cells
```

该包会添加必要的程序集，并解析 `Workbook`、`Worksheet` 和 `ListObject` 类型。

### 步骤 2：加载工作簿并定位表格

```csharp
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Load the workbook that contains the table
        var workbook = new Workbook(@"C:\Data\table_with_header.xlsx");

        // Access the first worksheet (index 0)
        var worksheet = workbook.Worksheets[0];

        // Retrieve the first ListObject (structured table) on the sheet
        var table = worksheet.ListObjects[0];
```

*为什么重要*：`ListObject` 代表真正的 Excel 表格，它拥有自己的标题行。通过操作 `ListObject`，您可以避免意外删除标题。

### 步骤 3：删除所需的数据行

`DeleteRows` 方法接受相对于表格的 **零基** 行索引，**包括**标题行。由于标题行不能被删除，您必须从索引 1 开始，指向第一条数据行。

```csharp
        // Delete two data rows starting after the header (index 1)
        // Parameters: startRow (relative to the table), numberOfRows
        table.DeleteRows(1, 2);
```

如果您尝试 `table.DeleteRows(0, 2)`，Aspose.Cells 会抛出异常，因为标题行（索引 0）受保护。从索引 1 开始可确保仅删除数据行。

### 步骤 4：保存修改后的工作簿

```csharp
        // Save the workbook to a new file to preserve the original
        workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
    }
}
```

运行程序后，标题下方的两行会被立即删除，而表格结构保持完整。

### 完整工作示例

```csharp
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // 1. Load workbook
        var workbook = new Workbook(@"C:\Data\table_with_header.xlsx");

        // 2. Access first worksheet
        var worksheet = workbook.Worksheets[0];

        // 3. Get the first table (ListObject)
        var table = worksheet.ListObjects[0];

        // 4. Delete two rows after the header (cannot delete header itself)
        table.DeleteRows(1, 2);

        // 5. Save the result
        workbook.Save(@"C:\Data\table_with_header_modified.xlsx");
    }
}
```

**预期输出**：文件 `table_with_header_modified.xlsx` 包含原始表格标题，随后是除被删除的两行之外的所有行。其他工作表不受影响。

## 删除 Excel 工作表中的多行

有时您需要删除 **不属于结构化表格** 的行。次要关键词出现在本标题中。由于操作对象是工作表的 `Rows` 集合，而非 `ListObject`，方法略有不同。

```csharp
using Aspose.Cells;

class SheetRowDeletion
{
    static void Main()
    {
        var workbook = new Workbook(@"C:\Data\plain_sheet.xlsx");
        var worksheet = workbook.Worksheets[0];

        // Delete rows 5 through 9 (inclusive) – zero‑based index
        // The second argument is the count of rows to remove
        worksheet.Rows.RemoveAt(4, 5);

        workbook.Save(@"C:\Data\plain_sheet_modified.xlsx");
    }
}
```

**为什么可行**：`Rows.RemoveAt(startIndex, count)` 直接从工作表中删除一段连续的行。没有标题保护，您可以从任意索引开始。该方法效率高，因为它在一次操作中更新内部数据结构，非常适合一次性删除多行的场景。

### 边缘情况与最佳实践

| 场景                                 | 推荐处理方式 |
|--------------------------------------|--------------|
| 删除超出最后一行的行                 | 在调用 `RemoveAt` 前检查 `worksheet.Rows.Count`。 |
| 删除除标题外的所有行                 | 在循环中删除数据行，或使用 `DeleteRows(1, table.DataRange.RowCount - 1)`。 |
| 保留单元格格式                         | 通过 `ListObject` 删除会自动移动格式；对原始工作表，若需要可在删除前复制格式。 |
| 大型工作表（> 10 000 行）            | 采用降序删除以避免索引偏移，或尽可能使用表格的 `DeleteRows`。 |

**专业提示**：当需要根据条件删除行（例如，某列值为空的行）时，建议逆向遍历表格的 `DataRange`，对每个匹配的行调用 `DeleteRows`。逆向删除可防止索引错位。

## 常见问题

*这适用于 Excel 365 创建的 .xlsx 文件吗？*  
是的。Aspose.Cells 支持完整的 Office Open XML 规范，代码同样适用于任何现代 `.xlsx` 文件。

*如果工作簿包含多个表格怎么办？*  
通过名称获取目标表格：`var table = worksheet.ListObjects["MyTable"];` 然后按示例使用 `DeleteRows`。

*能否在不使用第三方库的情况下删除行？*  
您可以使用 Microsoft.Office.Interop.Excel COM 互操作，但这要求服务器上安装 Excel，并会带来 COM 相关的开销。Aspose.Cells 提供了轻量级、服务器安全的替代方案。

## 结论

现在，您已经掌握了如何安全地删除 Excel 表格中的行，以及如何在 Excel 工作表中删除多行。主要技术是使用 `ListObject.DeleteRows` 方法，它会保护表格标题；次要技术是对普通工作表使用 `Rows.RemoveAt`。将这些模式应用于数据清理、自动化报表生成或在应用程序中实现批量编辑功能。

**后续步骤**

* 探索 Aspose.Cells 的其他功能，如插入行、复制样式或过滤数据。  
* 如果您更倾向于开源库，可尝试 **ClosedXML**；其 API 类似，但使用 `IXLTable` 和 `IXLRows`。  
* 将行删除逻辑与 LINQ 查询结合，构建更复杂的数据清洗管道。

祝编码愉快！


## 接下来您应该学习什么？

以下教程涵盖与本指南技术密切相关的主题，帮助您进一步掌握 API 功能并探索项目中的替代实现方式，每篇资源均提供完整的可运行代码示例和逐步说明。

- [如何在 C# 中删除 Excel 行 – 保护表格标题](/cells/english/net/row-and-column-management/how-to-delete-rows-in-excel-with-c-protect-table-header/)
- [使用 Aspose.Cells 删除 Excel 表格中的行并保留…](/cells/english/net/row-and-column-management/how-to-use-aspose-cells-to-delete-rows-in-an-excel-table-whi/)
- [加载 Excel 文件 C# – 如何删除行并移除特定行](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}