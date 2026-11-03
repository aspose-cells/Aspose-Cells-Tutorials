---
category: general
date: 2026-10-01
description: 学习使用 C# 删除 Excel 表格中的行并更改 Excel 表格名称。一步一步的指南，提供完整代码和最佳实践。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows excel table
- change excel table name
- load excel workbook c#
- remove rows from excel table
- update excel table name
language: zh
lastmod: 2026-10-01
og_description: 在 C# 中删除 Excel 表格中的行并更改表格名称。请按照本完整教程加载工作簿、修改表格并保存结果。
og_image_alt: Screenshot showing C# code that deletes rows from an Excel table and
  updates the table name
og_title: 在 C# 中删除 Excel 表格的行并更改其名称 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn to delete rows from an Excel table and change the Excel table
    name using C#. Step‑by‑step guide with full code and best practices.
  headline: How to delete rows from an Excel table and change its name in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: 如何在 C# 中删除 Excel 表格的行并更改其名称
url: /zh/net/tables-and-lists/how-to-delete-rows-from-an-excel-table-and-change-its-name-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中删除 Excel 表格的行并更改其名称

如果您需要在使用 C# 时 **删除 Excel 表格的行**，本指南将展示所需的完整步骤。您将看到如何 **在 C# 中加载 Excel 工作簿**、从表格中删除特定行，然后 **更新 Excel 表格名称**，以保持文件的一致性。

本教程涵盖您需要了解的全部内容：必需的 NuGet 包、可直接运行的完整代码，以及诸如表结构违规等常见陷阱。阅读完本文后，您即可在无需手动操作的情况下以编程方式修改任何 Excel 表格。

## 前置条件

在开始之前，请确保您具备以下条件：

* 已安装 .NET 6.0 SDK 或更高版本。
* 已配置 .NET 开发环境的 Visual Studio 2022（或任意 C# IDE）。
* 通过 NuGet 添加了 **Aspose.Cells for .NET** 库（`Install-Package Aspose.Cells`）。
* 已存在的 Excel 工作簿（`Table.xlsx`），其中至少包含一个工作表和一个表格。

这些项目为 **load Excel workbook c#** 代码的执行提供了必要的环境。

## 步骤 1：加载包含表格的工作簿

第一步是打开工作簿文件。Aspose.Cells 会将整个工作簿读取到内存中，让您能够完全控制工作表、表格和单元格数据。

```csharp
using Aspose.Cells;

string inputPath = @"C:\Data\Table.xlsx";

// Load the workbook from disk
Workbook workbook = new Workbook(inputPath);
```

*为何重要*：加载工作簿是后续所有表格操作的基础。`Workbook` 对象公开了 `Worksheets` 集合，您将使用它来定位目标表格。

## 步骤 2：访问第一个工作表及其第一个表格

大多数 Excel 文件将表格存放在第一个工作表中，必要时您可以调整索引。下面的代码检索第一个 `Table` 对象。

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Retrieve the first table on that worksheet
Table table = sheet.Tables[0];
```

如果工作表中不包含表格，`sheet.Tables.Count` 将为零，您需要相应处理。尝试在不存在表格时访问 `sheet.Tables[0]` 会抛出异常，这也是在生产代码中建议使用防护语句的原因。

## 步骤 3：删除 Excel 表格中的行

要 **从 Excel 表格中删除行**，请调用 `DeleteRows(startRow, totalRows)`。`startRow` 参数是相对于表格第一数据行（标题行之后）的零基索引。

```csharp
// Delete two rows starting from the second data row (index 1)
int startRow = 1;   // second row within the table
int rowsToDelete = 2;

table.DeleteRows(startRow, rowsToDelete);
```

### 为什么使用 `DeleteRows` 而不是直接删除工作表行？

`DeleteRows` 会更新表格的内部范围，保留属于表格的公式、样式和已定义名称。直接删除工作表行可能会破坏表格结构并导致异常。

**边界情况**：如果删除操作会导致表格没有数据行，Aspose.Cells 会抛出 `ArgumentException`。在删除前检查 `table.RowCount` 以防止此类情况。

```csharp
if (table.RowCount - rowsToDelete < 1)
{
    throw new InvalidOperationException("Cannot delete all data rows from the table.");
}
```

## 步骤 4：更改 Excel 表格名称

删除行后，您可能希望为表格指定一个更具描述性的标识符。`Name` 属性用于设置表格的已定义名称，该名称在公式和 VBA 中都会被使用。

```csharp
// Assign a new name to the table
string newTableName = "SalesData2026";

if (workbook.Worksheets.GetDefinedNames().Any(d => d.Text == newTableName))
{
    throw new InvalidOperationException($"The name '{newTableName}' already exists as a defined name.");
}

table.Name = newTableName;
```

*为何要重命名？* 清晰的表格名称有助于在公式中提升可读性（例如 `=SUM(SalesData2026[Amount])`），并避免在多个表格用途相似时出现名称冲突。

## 步骤 5：保存修改后的工作簿（可选）

通过保存到新文件或覆盖原文件来持久化更改。开发阶段将文件保存到新位置更为安全。

```csharp
string outputPath = @"C:\Data\ModifiedTable.xlsx";
workbook.Save(outputPath);
```

`Save` 方法会将更新后的工作簿（包括已更改的表格范围和新表格名称）写入磁盘。

## 完整可运行示例

将所有步骤组合在一起，即可得到一个可直接运行的自包含程序。

```csharp
using System;
using System.Linq;
using Aspose.Cells;

class ExcelTableModifier
{
    static void Main()
    {
        // ----- Step 1: Load workbook -----
        string inputPath = @"C:\Data\Table.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // ----- Step 2: Access worksheet and table -----
        Worksheet sheet = workbook.Worksheets[0];
        if (sheet.Tables.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        Table table = sheet.Tables[0];

        // ----- Step 3: Delete rows -----
        int startRow = 1;      // second data row (zero‑based)
        int rowsToDelete = 2;

        if (table.RowCount - rowsToDelete < 1)
        {
            Console.WriteLine("Deletion would remove all data rows; operation aborted.");
            return;
        }

        table.DeleteRows(startRow, rowsToDelete);
        Console.WriteLine($"{rowsToDelete} rows removed starting at index {startRow}.");

        // ----- Step 4: Change table name -----
        string newTableName = "SalesData2026";

        bool nameExists = workbook.Worksheets.GetDefinedNames()
                               .Any(d => d.Text.Equals(newTableName, StringComparison.OrdinalIgnoreCase));

        if (nameExists)
        {
            Console.WriteLine($"The name '{newTableName}' already exists. Choose a different name.");
            return;
        }

        table.Name = newTableName;
        Console.WriteLine($"Table renamed to '{newTableName}'.");

        // ----- Step 5: Save workbook -----
        string outputPath = @"C:\Data\ModifiedTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Modified workbook saved to '{outputPath}'.");
    }
}
```

**预期输出**（假设文件和表格均存在）：

```
2 rows removed starting at index 1.
Table renamed to 'SalesData2026'.
Modified workbook saved to 'C:\Data\ModifiedTable.xlsx'.
```

运行程序后，Excel 文件将按照描述进行更新：行被删除，表格名称被更改，且结果已保存，无需手动编辑。

## 常见问题与故障排除

| 问题 | 答案 |
|----------|--------|
| *如果表格跨越合并单元格会怎样？* | `DeleteRows` 会尊重合并范围。如果合并单元格跨越删除边界，Aspose.Cells 会自动调整合并。若依赖复杂合并，请目视检查结果。 |
| *能否删除属于数据透视缓存的表格行？* | 从作为数据透视表源的表格中删除行 **不会** 自动刷新数据透视缓存。修改源表后请调用 `pivotTable.RefreshData()`。 |
| *是否可以基于条件（例如值 < 0）删除行？* | 可以。遍历 `table.ListObjects` 或 `table.Rows` 找到匹配的行，收集其索引后对相应范围调用 `DeleteRows`。 |
| *是否需要释放 `Workbook` 对象？* | `Workbook` 实现了 `IDisposable`。建议使用 `using` 块以确定性释放资源，尤其在处理大文件时。 |
| *这与使用 EPPlus 有何不同？* | EPPlus 也支持表格操作，但使用不同的 API（`ExcelTable`）。加载工作簿、删除行、重命名表格的概念类似。请选择符合您许可需求的库。 |

## 在 C# 中修改 Excel 表格的最佳实践

* **验证索引** – 表格行索引为零基；越界错误会导致意外删除。
* **检查名称冲突** – Excel 不允许重复的已定义名称；在分配新名称前务必确保唯一性。
* **备份原始文件** – 自动化脚本可能会损坏数据，请保留工作簿的副本。
* **使用 `using` 语句** – 能及时释放文件句柄：

```csharp
using (Workbook wb = new Workbook(inputPath))
{
    // modify workbook
}
```

* **使用边界案例进行测试** – 包含单行数据的表格、跨越整个工作表的表格以及与图表关联的表格，都应在修改后进行验证。

## 结论

现在，您已经掌握了如何使用 C# **删除 Excel 表格的行** 并 **更改 Excel 表格名称**。完整的解决方案包括加载工作簿、定位目标表格、删除所需行、重命名表格以及保存结果。将这些技术应用于报告生成、数据清洗或任何需要以编程方式管理 Excel 表格的工作流。

接下来，您可以进一步探索 **在 Excel 表格中更新单元格值**、**以编程方式添加新行**以及**将表格数据导出为 CSV**等相关主题。熟练掌握这些操作后，您将能够在 C# 应用程序中全面控制 Excel 文件。

## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您在已有技巧的基础上进一步提升。每篇资源都提供完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并探索项目中的替代实现方案。

- [How to Rename Table in Excel with C# – Step‑by‑Step Guide](/cells/english/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/)
- [Create Excel Table in C# – Step‑by‑Step Guide](/cells/english/net/tables-and-lists/create-excel-table-in-c-step-by-step-guide/)
- [Get First Table from Excel Workbook in C# – Complete Guide](/cells/english/net/excel-autofilter-validation/get-first-table-from-excel-workbook-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}