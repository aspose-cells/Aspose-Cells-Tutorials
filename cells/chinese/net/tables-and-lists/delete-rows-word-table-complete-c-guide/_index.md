---
category: general
date: 2026-06-08
description: 使用 Aspose.Words 删除 Word 表格中的行。学习如何删除行、删除多个 Word 行，并在几分钟内掌握表格编辑。
draft: false
keywords:
- delete rows word table
- how to delete rows
- delete multiple rows word
language: zh
og_description: 使用 Aspose.Words 删除 Word 表格中的行。本教程展示了如何删除行、删除多个行，以及保持表格整洁。
og_title: 删除 Word 表格行 – 完整 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Delete rows word table using Aspose.Words. Learn how to delete rows,
    delete multiple rows word, and master table editing in minutes.
  headline: Delete rows word table – Complete C# Guide
  type: TechArticle
- description: Delete rows word table using Aspose.Words. Learn how to delete rows,
    delete multiple rows word, and master table editing in minutes.
  name: Delete rows word table – Complete C# Guide
  steps:
  - name: 3.1 How to delete rows (single row)
    text: 'To remove a single row, call `DeleteRows(startIndex, count)` where `startIndex`
      is zero‑based. Skipping the header row (index 0) is common:'
  - name: 3.2 Delete multiple rows word – batch removal
    text: 'When you need to drop a range—say rows 2‑6—you pass the start index and
      the number of rows to erase. This is the **delete multiple rows word** pattern:'
  - name: Expected output
    text: '- `output.docx` contains the original table **without** rows 2‑6. - All
      remaining rows shift up, preserving cell formatting and column widths. - The
      header row stays intact, keeping your column titles visible.'
  type: HowTo
- questions:
  - answer: Absolutely. Loop through `table.Rows`, inspect `row.Cells[i].GetText()`,
      and collect matching indices. Then call `DeleteRows` with the smallest index
      and total count, or delete rows in reverse order to avoid re‑indexing.
    question: Can I delete rows based on cell content instead of index?
  - answer: Yes. Aspose.Words supports both `.doc` and `.docx`. Just change the file
      extension in the `Document` constructor and `Save` call.
    question: Does this work with .doc files?
  - answer: 'Retrieve it via `doc.FirstSection.HeadersFooters` collection, then apply
      the same `DeleteRows` logic. ## Conclusion You now have a solid, end‑to‑end
      solution for **delete rows word table** using C#. The example shows *how to
      delete rows* individually and how to **delete multiple rows word** in a sin'
    question: What if the table is inside a header/footer?
  type: FAQPage
tags:
- C#
- Aspose.Words
- Word automation
title: 删除 Word 表格行 – 完整 C# 指南
url: /zh/net/tables-and-lists/delete-rows-word-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 删除 Word 表格行 – 完整 C# 指南

是否曾经需要**删除 Word 表格行**但不知从何入手？你并不孤单；许多开发者在清理生成的报告或裁剪数据驱动的表格时都会遇到这个难题。好消息是？只需几行 C# 代码和 Aspose.Words，你就可以轻松删除不需要的行，无论是一行还是一批。在本指南中，我们将逐步讲解*如何删除行*，甚至涵盖一次性**删除多个 Word 行**的更复杂情况。

我们将覆盖你需要了解的所有内容：完整代码、每一步为何重要、常见陷阱以及可直接运行的示例。结束时，你将能够在不破坏文档结构的前提下，从任何 Word 表格中删除行。没有废话，只有实用、经受考验的技巧。

## 前置条件

在开始之前，请确保你拥有：

- **Aspose.Words for .NET**（版本 23.12 或更新）。可通过 NuGet 获取：`Install-Package Aspose.Words`。
- .NET 开发环境（Visual Studio、Rider，或带有 C# 扩展的 VS Code）。
- 一个包含至少一行标题的表格的输入 Word 文件（`input.docx`）。

就这些——无需额外库、无需 COM 互操作，纯托管代码即可。

## 步骤 1：加载 Word 文档

首先要做的就是打开文档。Aspose.Words 将 Word 文件视为 `Document` 对象，提供对节、正文、表格等的完整访问。

```csharp
using Aspose.Words;

class TableCleaner
{
    static void Main()
    {
        // Load the source .docx file
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        // Continue with table manipulation…
```

*为什么这很重要：* 加载文档会在内存中创建表示，因此所有更改都非常快速，只有在显式保存时才会写入文件系统。

## 步骤 2：获取目标表格

在大多数场景下，你已经知道要编辑的表格——通常是第一个。Aspose.Words 通过 `FirstSection` 属性可以轻松获取它。

```csharp
        // Access the first table in the first section
        Table table = doc.FirstSection.Body.Tables[0];
```

如果文档中有多个表格，你可以遍历 `doc.GetChildNodes(NodeType.Table, true)`，根据索引或自定义标记挑选出正确的表格。

## 步骤 3：删除行 – 单行或多行

### 3.1 如何删除行（单行）

要删除单行，调用 `DeleteRows(startIndex, count)`，其中 `startIndex` 为零基索引。通常会跳过标题行（索引 0）：

```csharp
        // Delete just the second row (index 1)
        table.DeleteRows(1, 1);
```

### 3.2 删除多个 Word 行 – 批量删除

当需要一次性删除一段范围——例如第 2‑6 行——只需传入起始索引和要删除的行数。这就是 **删除多个 Word 行** 的模式：

```csharp
        // Delete rows 2‑6 (skip header at index 0)
        // startIndex = 1 (second row), count = 5 rows
        table.DeleteRows(1, 5);
```

*为什么使用一次调用？* 逐行删除会在每次移除后重新索引表格，容易出错且速度较慢。批量方法保持表格内部结构的一致性。

#### 边缘情况：删除超出表格大小的行

如果 `startIndex + count` 超过实际行数，Aspose.Words 会抛出 `ArgumentOutOfRangeException`。防御性检查如下：

```csharp
        int rowsToDelete = Math.Min(5, table.Rows.Count - 1); // never delete the header
        if (rowsToDelete > 0)
            table.DeleteRows(1, rowsToDelete);
```

该代码片段确保永远不会尝试删除超出实际存在的行数。

## 步骤 4：保存修改后的文档

行删除完毕后，只需一行代码即可持久化更改：

```csharp
        // Save the cleaned document
        doc.Save(@"YOUR_DIRECTORY\output.docx");
    }
}
```

`Save` 方法会根据文件扩展名自动选择格式，因此你可以输出为 PDF、HTML，甚至使用不同后缀的 ODT。

## 完整工作示例

将所有步骤组合在一起，下面是完整的、可直接运行的程序：

```csharp
using System;
using Aspose.Words;

class TableCleaner
{
    static void Main()
    {
        // 1️⃣ Load the Word document
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");

        // 2️⃣ Access the first table (adjust index if needed)
        Table table = doc.FirstSection.Body.Tables[0];

        // 3️⃣ Delete rows 2‑6 (skip header row at index 0)
        //    This demonstrates delete multiple rows word in one call.
        if (table.Rows.Count > 1) // ensure there is at least a header + one data row
        {
            int rowsToDelete = Math.Min(5, table.Rows.Count - 1);
            table.DeleteRows(1, rowsToDelete);
        }

        // 4️⃣ Save the modified document
        doc.Save(@"YOUR_DIRECTORY\output.docx");

        Console.WriteLine("Rows removed successfully. Output saved to output.docx");
    }
}
```

### 预期输出

- `output.docx` 包含原始表格，但 **第 2‑6 行已被删除**。
- 所有剩余行上移，保持单元格格式和列宽不变。
- 标题行保持完整，列标题仍然可见。

## 为什么这种方法优于其他方案

| 方法 | 优点 | 缺点 |
|------|------|------|
| **Aspose.Words `DeleteRows`** | 一行代码批量删除，保留样式，无 COM 依赖 | 需要商业库（提供免费试用） |
| Office Interop | 与本机 Word 配合使用 | 服务器需安装 Word，速度慢，COM 清理麻烦 |
| Open XML SDK | 免费、开源 | 手动操作 XML；安全删除行较为繁琐 |

如果你已经在使用 Aspose.Words 处理其他文档任务，继续使用 `DeleteRows` 能让代码库保持简洁一致。

## 专业技巧与常见陷阱

- **技巧：** 除非真的想删除标题，否则始终保留标题行（索引 0）。删除标题会导致下游处理期望列名时出错。
- **留意合并单元格。** 若某行包含垂直合并的单元格并跨入待删除的行，Aspose.Words 会自动调整合并范围，但请务必检查视觉效果是否符合预期。
- **性能提示：** 从包含数千行的大表格中删除大量行仍然很快，但若在循环中处理数百个文档，建议复用 `Document` 对象以降低分配开销。

## 常见问题

**问：能否根据单元格内容而非索引删除行？**  
答：完全可以。遍历 `table.Rows`，检查 `row.Cells[i].GetText()`，收集匹配的索引。随后使用最小索引和总计数调用 `DeleteRows`，或逆序删除行以避免重新索引。

**问：这对 .doc 文件也有效吗？**  
答：有效。Aspose.Words 同时支持 `.doc` 与 `.docx`。只需在 `Document` 构造函数和 `Save` 调用中更改文件扩展名即可。

**问：如果表格位于页眉/页脚中怎么办？**  
答：通过 `doc.FirstSection.HeadersFooters` 集合获取表格，然后使用相同的 `DeleteRows` 逻辑即可。

## 结论

现在，你已经掌握了使用 C# 和 Aspose.Words **删除 Word 表格行** 的完整端到端解决方案。示例展示了*如何单独删除行*以及如何在一次高效调用中**删除多个 Word 行**。借助 Aspose.Words，你拥有干净的 API、无需 COM 麻烦，并能完全控制 Word 文档。

准备好迎接下一个挑战了吗？尝试添加一行计算合计，或使用 `Table.ToTxt` 将裁剪后的表格导出为 CSV。掌握表格操作后，天地任你遨游。

祝编码愉快，愿你的 Word 表格保持整洁！

## 接下来你应该学习什么？

- [如何使用 Aspose.Cells for Java 删除 Excel 行 | 指南与教程](/cells/english/java/worksheet-management/delete-row-excel-aspose-cells-java/)
- [如何使用 Aspose.Cells .NET 删除 Excel 空白行以进行数据清理](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)
- [如何使用 Aspose.Cells for .NET 插入和删除 Excel 行：全面指南](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}