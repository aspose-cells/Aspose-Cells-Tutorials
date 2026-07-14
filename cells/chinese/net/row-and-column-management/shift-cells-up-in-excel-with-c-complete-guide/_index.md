---
category: general
date: 2026-07-13
description: 使用 C# 在 Excel 中向上移动单元格。了解如何删除首行、删除多行以及一次安全操作中从表格中移除行。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- shift cells up
- remove first rows
- remove rows from table
- delete multiple rows
- how to delete rows
language: zh
lastmod: 2026-07-13
og_description: 使用 C# 在 Excel 工作表中向上移动单元格。本教程展示了如何删除首行、删除多行以及安全地从表格中删除行。
og_image_alt: Screenshot of C# code that shifts cells up after deleting rows in an
  Excel worksheet
og_title: 使用 C# 在 Excel 中向上移动单元格 – 完整编程演练
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Shift cells up in Excel using C#. Learn how to remove first rows, delete
    multiple rows, and remove rows from table in a single, safe operation.
  headline: Shift Cells Up in Excel with C# – Complete Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Loop through `sheet.Cells.Rows` and call `DeleteRows(rowIndex,
      1, true)` whenever the condition matches. Just remember to iterate backwards
      to avoid index shifting.
    question: Can I delete rows based on a condition instead of a fixed index?
  - answer: Yes. Aspose.Cells supports both `.xlsx` and legacy `.xls` formats. The
      same API applies.
    question: Does this work with `.xls` files?
  - answer: 'Target the specific table by name: `Table myTable = sheet.Tables["MyTable"];`
      then use `myTable.Range.StartRow` to calculate the rows to delete. --- ## Full
      Working Example Below is the complete, ready‑to‑run program that incorporates
      everything we discussed. Copy‑paste it into a console app, adjust'
    question: What if my workbook contains multiple tables and I only want to affect
      one?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: 使用 C# 在 Excel 中向上移动单元格 – 完整指南
url: /zh/net/row-and-column-management/shift-cells-up-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中使用 C# 将单元格上移 – 完整指南

是否曾想过在 Excel 文件中删除行后如何 **上移单元格**？你并非唯一有此困惑的人。无论是清理导入的数据还是裁剪庞大的报告，能够在不破坏表格的情况下删除首行是每个 C# 开发者必备的技能。

在本教程中，我们将一步步演示一个实用的端到端解决方案，展示 **如何删除行**，保持标题完整，并自动上移剩余单元格。完成后，你将能够仅用几行代码就 **从表格中删除行**、**删除多行**，以及 **删除首行**。

---

## 所需条件

- .NET 6+（或 .NET Framework 4.7.2 及更高）  
- **Aspose.Cells for .NET** 库（免费试用或授权版）  
- 对 C# 和 Visual Studio（或你喜欢的任何 IDE）的基本了解  

无需其他依赖——只需 NuGet 包和一个用于操作的 Excel 文件。

---

## 步骤 1：安装 Aspose.Cells

首先，将 Aspose.Cells 包添加到你的项目中：

```bash
dotnet add package Aspose.Cells
```

这行代码会把处理工作簿、工作表和表格所需的所有内容都引入。如果你使用 Visual Studio，也可以右键项目 → **Manage NuGet Packages** → 搜索 *Aspose.Cells* 并点击 **Install**。

*小技巧：* 使用最新的稳定版本；截至 2026 年 7 月，它是 **23.9.0**，支持最新的 Excel 文件格式。

---

## 步骤 2：加载包含表格的工作簿

现在我们打开包含需要清理数据的 Excel 文件。将 `YOUR_DIRECTORY` 替换为你机器上的实际路径。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains the table
        Workbook workbook = new Workbook(@"C:\Data\table.xlsx");
        
        // Grab the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];
        
        // Optional: get a reference to the first table for context
        Table table = sheet.Tables[0];
```

此时我们已经拥有一个可供操作的 `Worksheet` 对象。请注意我们尚未触及表格——在后续 **上移单元格** 时保持标题完整至关重要。

---

## 步骤 3：删除前两行并上移单元格

这就是关键所在：删除行 *并且* 让下面的单元格自动上移。Aspose.Cells 提供了 `DeleteRows` 方法，当为 `shiftCellsUp` 标志传入 `true` 时即可实现此功能。

```csharp
        // Delete the first two rows (row index starts at 0)
        // The third argument ‑‑> true tells Aspose.Cells to shift cells up.
        sheet.Cells.DeleteRows(0, 2, true);
```

### 为什么 `true` 标志很重要

如果省略 `true` 标志，行会被删除，但它们占用的空间仍然为空，导致数据出现空隙。将其设为 **true** 会让库收缩范围，实际 **上移单元格**，使第 3 行成为新的第 1 行。这是 **删除首行** 而不破坏公式或表格结构的最简洁方式。

> **重要提示：** 删除包含表格标题的行会抛出异常。请保持标题行（通常是第 0 行）完整，或在重新创建表格标题后单独删除它。

---

## 步骤 4：验证表格仍然正常

删除后，最好再次确认表格引用仍指向正确的范围。你可以打印表格的地址或刷新它：

```csharp
        // Refresh the table range to reflect the new data area
        table.Refresh();

        // Output the new range for debugging
        Console.WriteLine($"Table now spans: {table.Ref}");
```

运行程序后应显示类似 `Table1!A1:D8` 而不是原来的 `A1:D10`，以确认行已被删除且单元格已上移。

---

## 步骤 5：保存修改后的工作簿

最后，将更改写回磁盘。你可以覆盖原文件，也可以创建新副本——由你决定。

```csharp
        // Save the workbook with the changes
        workbook.Save(@"C:\Data\modified_table.xlsx");
    }
}
```

在 Excel 中打开 `modified_table.xlsx`，你会看到前两行已消失，剩余行上移，表格仍保持完整。此操作已有效 **删除多行**，同时保持数据完整性。

---

## 边缘情况与常见陷阱

| 情况 | 会发生什么 | 处理方法 |
|-----------|--------------|------------------|
| **标题行是删除范围的一部分** | Aspose.Cells 抛出 `InvalidOperationException`，因为表格不能失去标题。 | 仅删除数据行，或在删除后使用 `sheet.Cells["A1"].PutValue("Header")` 重新创建标题。 |
| **表格跨多个工作表** | 在一个工作表上删除行不会影响其他工作表。 | 如果需要全局清理，请遍历每个工作表的表格。 |
| **大文件（>100 MB）** | 内存使用激增。 | 使用 `LoadOptions` 并将 `MemoryPreference` 设置为 `MemoryPreference.MemoryOnly` 以降低内存占用。 |
| **需要保留引用已删除行的公式** | 公式可能变为 `#REF!`。 | 使用 `sheet.Cells.DeleteRows(startRow, count, true, true)` —— 第四个参数告诉 Aspose.Cells 更新公式。 |

---

## 常见问题

**问：我可以根据条件而不是固定索引删除行吗？**  
答：当然可以。遍历 `sheet.Cells.Rows`，在条件满足时调用 `DeleteRows(rowIndex, 1, true)`。请记得逆向遍历以避免索引错位。

**问：这对 `.xls` 文件也适用吗？**  
答：是的。Aspose.Cells 同时支持 `.xlsx` 和旧版 `.xls` 格式，使用相同的 API。

**问：如果工作簿包含多个表格，我只想影响其中一个怎么办？**  
答：通过名称定位特定表格：`Table myTable = sheet.Tables["MyTable"];` 然后使用 `myTable.Range.StartRow` 来计算要删除的行。

---

## 完整示例代码

下面是完整的、可直接运行的程序，包含了我们讨论的所有内容。复制粘贴到控制台应用程序中，调整文件路径，然后按 **F5**。

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"C:\Data\table.xlsx");
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ (Optional) Reference the first table for context
        Table table = sheet.Tables[0];

        // 3️⃣ Delete the first two rows and shift cells up
        //    Row index starts at 0, delete 2 rows, shift up = true
        sheet.Cells.DeleteRows(0, 2, true);

        // 4️⃣ Refresh the table range so it reflects the new data area
        table.Refresh();

        // 5️⃣ Show the new table reference (useful for debugging)
        Console.WriteLine($"Table now spans: {table.Ref}");

        // 6️⃣ Save the modified workbook
        workbook.Save(@"C:\Data\modified_table.xlsx");

        Console.WriteLine("Rows removed and cells shifted up successfully!");
    }
}
```

**预期结果：**  
- 第 1‑2 行从工作表中消失。  
- 第 3 行成为新的第 1 行，第 4 行成为第 2 行，依此类推。  
- 表格范围自动更新，确认 **上移单元格** 已按预期工作。

---

## 结论

我们刚刚介绍了如何使用 C# 在 Excel 工作表中 **上移单元格**。通过使用 Aspose.Cells 的 `DeleteRows` 方法并传入 `true` 标志，你可以安全地 **删除首行**、**删除多行**，以及 **从表格中删除行**，而不会破坏数据模型。此方法快速、可靠，适用于所有现代 Excel 格式。

准备好下一步了吗？尝试将此技术与条件过滤相结合，以清除包含空白或重复条目的行。或者探索 Aspose.Cells 的样式 API，在上移后重新应用格式。掌握 Excel 行操作后，可能性无限。

有任何问题或想分享的酷用例吗？在下方留言吧，祝编码愉快！

## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你进一步学习。每个资源都提供完整的可运行代码示例和逐步说明，帮助你掌握更多 API 功能并在项目中探索替代实现方式。

- [使用 Aspose.Cells .NET 在 Excel 中删除多行&#58; 数据处理综合指南](/cells/english/net/data-manipulation/delete-rows-excel-aspose-cells-net/)
- [使用 Aspose.Cells for .NET 在 Excel 中插入和删除行&#58; 综合指南](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [使用 Aspose.Cells .NET 在 Excel 中删除空白行&#58; 数据清理指南](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}