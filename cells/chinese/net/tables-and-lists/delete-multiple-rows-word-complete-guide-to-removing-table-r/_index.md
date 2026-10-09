---
category: general
date: 2026-06-27
description: 使用 C# 删除 Word 中的多行。学习如何删除表格行、移除表格行以及高效编辑 Word 文档表格。
draft: false
keywords:
- delete multiple rows word
- how to delete table rows
- how to remove table rows
- delete rows from word table
- word document table editing
language: zh
og_description: 即时删除多个 Word 行。本教程展示如何删除表格行、从 Word 表格中移除行以及掌握 Word 文档的表格编辑。
og_title: 在 Word 中删除多行 – 步骤式表格编辑
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Delete multiple rows word using C#. Learn how to delete table rows,
    remove table rows and edit Word document tables efficiently.
  headline: Delete Multiple Rows Word – Complete Guide to Removing Table Rows
  type: TechArticle
tags:
- Aspose.Words
- C#
- Word Automation
title: Word 删除多行 – 完整的表格行删除指南
url: /zh/net/tables-and-lists/delete-multiple-rows-word-complete-guide-to-removing-table-r/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 删除多个行 Word – 完整的表格行删除指南

是否曾需要在 **Word 文档中删除多个行**，却不确定该使用哪个 API 调用？你并不孤单——大多数开发者在尝试在保留表头的同时裁剪表格时都会遇到同样的难题。

在本教程中，我们将一步步演示一个简洁的端到端解决方案，展示 *如何以编程方式删除表格行*、*如何安全地移除表格行*，以及为何该方法适用于所有 **从 Word 表格中删除行** 的场景。

阅读完本教程后，你将拥有一个可在任何 C# 项目中直接使用的可复用代码片段，以及一些用于更广泛 **Word 文档表格编辑** 任务的技巧。

## 前置条件

- .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.6+）
- 已安装 Aspose.Words for .NET（`dotnet add package Aspose.Words`）
- 对 C# 语法有基本了解
- 一个包含至少一行表头的 `.docx` 输入文件

> **专业提示：** 如果你还没有许可证，Aspose.Words 提供免费评估模式，非常适合测试。

## 第一步：创建项目并加载 Word 文档

首先——创建一个控制台应用（或集成到现有服务），并添加必要的 `using` 指令。随后加载源文档。

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Tables;

class Program
{
    static void Main()
    {
        // Load the Word document (replace YOUR_DIRECTORY with your actual path)
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        Console.WriteLine("Document loaded successfully.");
```

**为什么重要：**  
`Document` 是所有 Aspose.Words 操作的入口。一次性加载文件可以降低内存占用，并为后续的表格编辑调用提供句柄。

## 第二步：定位第一张表（或你需要的任意表）

如果文档中包含多张表，你可以通过索引或关键字搜索来选取目标表。为简便起见，这里我们获取第一张表，通常它包含我们想要裁剪的数据。

```csharp
        // Retrieve the first table in the document
        Table firstTable = doc.GetChild(NodeType.Table, 0, true) as Table;
        if (firstTable == null)
        {
            Console.WriteLine("No table found in the document.");
            return;
        }
        Console.WriteLine($"Table with {firstTable.Rows.Count} rows found.");
```

**解释：**  
`GetChild(NodeType.Table, 0, true)` 以深度优先方式遍历文档树，并返回遇到的第一个 `Table` 节点。`as Table` 强制转换安全地将节点转为 `Table`，以便后续操作 `Rows`。

## 第三步：在保留表头的前提下删除多行

现在进入核心：**删除 Word 文档中的多行**。假设表头位于第 0 行，你想删除接下来的两行（索引 1 和 2）。`DeleteRows` 方法正是为此设计的。

```csharp
        // Delete two rows starting from the second row (index 1)
        // This keeps the header row untouched while removing the following rows
        firstTable?.DeleteRows(1, 2);
        Console.WriteLine("Specified rows deleted.");
```

### 删除表格行的不同写法

- **删除单行：** `firstTable?.DeleteRows(rowIndex, 1);`
- **删除除表头外的所有行：** `firstTable?.DeleteRows(1, firstTable.Rows.Count - 1);`
- **根据条件删除行：** 遍历 `firstTable.Rows`，在单元格满足条件时调用 `DeleteRows`。

这些代码片段以灵活的方式回答了常见的 **如何移除表格行** 问题。

## 第四步：保存修改后的文档

行删除完毕后，只需将文档写回磁盘。你可以覆盖原文件，也可以生成新副本。

```csharp
        // Save the modified document
        doc.Save(@"YOUR_DIRECTORY\output.docx");
        Console.WriteLine("Document saved as output.docx");
    }
}
```

**你将看到的结果：**  
如果原表格有五行（表头 + 四行数据），保存后的 `output.docx` 将只剩三行（表头 + 剩余两行数据）。在 Word 中打开文件即可验证，未需要的行已消失且其他内容未受影响。

![delete multiple rows word example](delete-multiple-rows-word.png)

*图片替代文字：删除多个行 Word – Word 表格的前后对比截图。*

## 完整、可直接运行的示例

将上述步骤整合在一起，下面是完整的程序代码，可直接复制粘贴使用：

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Tables;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the Word document
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        Console.WriteLine("Document loaded.");

        // 2️⃣ Retrieve the first table
        Table firstTable = doc.GetChild(NodeType.Table, 0, true) as Table;
        if (firstTable == null)
        {
            Console.WriteLine("No table found.");
            return;
        }
        Console.WriteLine($"Found table with {firstTable.Rows.Count} rows.");

        // 3️⃣ Delete rows – this is the core of delete rows from word table
        //    Starting at index 1 (second row), delete the next two rows.
        firstTable?.DeleteRows(1, 2);
        Console.WriteLine("Rows deleted.");

        // 4️⃣ Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
        Console.WriteLine("Saved output.docx");
    }
}
```

运行程序，打开 `output.docx`，你会看到表头仍在，而选中的行已消失。这就是 **删除多个行 Word** 的实际效果。

## 常见陷阱及规避方法

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| **NullReferenceException** 当 `firstTable` 为 `null` 时 | 文档中没有表格或索引错误 | 在调用 `DeleteRows` 前始终检查 `firstTable != null`。 |
| **行未被删除** | 使用了错误的起始索引（Word 表格索引从 0 开始） | 记住表头是第 0 行，若要保留表头应从 1 开始。 |
| **覆盖只读文件时保存失败** | 文件权限阻止覆盖 | 保存到其他路径或修改文件属性。 |
| **布局意外变化** | 删除包含合并单元格的行会破坏表格结构 | 先处理合并单元格——先取消合并或谨慎删除整行。 |

## 扩展方案 – 更多 Word 文档表格编辑

如果你想进一步探索 **Word 文档表格编辑**，可以尝试以下操作：

- **插入新行：** `firstTable?.Rows.Add(new Row(doc));`
- **更新单元格文本：** `firstTable.Rows[rowIndex].Cells[colIndex].Paragraphs[0].AppendText("New value");`
- **应用样式：** 使用 `CellFormat` 或 `RowFormat` 设置底纹、边框或字体属性。
- **导出为 PDF：** `doc.Save("output.pdf", SaveFormat.Pdf);`

所有这些操作都基于我们用于删除行的相同对象模型，使代码库保持一致。

## 结论

我们已经演示了如何使用几行 C# 代码 **删除多个行 Word** 文档。该方法涵盖了 *如何删除表格行*、*如何移除表格行*，以及更广泛的 **Word 文档表格编辑** 主题。

现在你拥有一套可靠、可复用的模式：加载文档 → 定位表格 → 使用正确的索引调用 `DeleteRows` → 保存。接下来，你可以调整行范围、遍历多张表，或结合其他编辑功能，以满足任何自动化任务。

准备好进一步探索了吗？尝试自动生成发票、清理报告模板，或构建一次性处理数十个 Word 文件的批量更新工具。天空才是极限，API 让一切变得轻而易举。

如果遇到任何问题，欢迎在下方留言——祝编码愉快！

## 接下来你应该学习什么？

以下教程与本指南紧密相关，基于相同技术构建，提供完整可运行的代码示例和逐步解释，帮助你掌握更多 API 功能并在项目中探索替代实现方案。

- [如何使用 Aspose.Cells for .NET 在 Excel 中插入和删除行：完整指南](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [使用 Aspose.Cells .NET 删除 Excel 中的多行：数据操作完整指南](/cells/english/net/data-manipulation/delete-rows-excel-aspose-cells-net/)
- [在 Aspose.Cells .NET 中删除多行](/cells/english/net/row-and-column-management/delete-multiple-rows-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}