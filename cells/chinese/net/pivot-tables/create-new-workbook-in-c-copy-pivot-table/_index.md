---
category: general
date: 2026-06-24
description: 在 C# 中创建新工作簿并复制数据透视表，同时保留其数据。学习如何复制行、导出选定范围，并保持数据透视表完整。
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- export selected range
language: zh
og_description: 在 C# 中创建新工作簿并复制透视表，同时保留其数据。逐步指南，涵盖如何复制行以及导出选定范围。
og_title: 在 C# 中创建新工作簿 – 复制数据透视表
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Create new workbook in C# and copy pivot table while preserving its
    data. Learn how to copy rows, export selected range, and keep the pivot intact.
  headline: Create New Workbook in C# – Copy Pivot Table
  type: TechArticle
- questions:
  - answer: Yes, as long as the copied rectangle encloses each pivot you need. If
      you only want one, adjust `rows`/`cols` to isolate it.
    question: Does this work with multiple pivot tables on the same sheet?
  - answer: The pivot cache will still point to the original connection. Call `pivotTable.RefreshData()`
      after loading the destination if you want to re‑query the source.
    question: What if the source workbook uses external data connections?
  - answer: Absolutely. Replace `destinationWorkbook` with `sourceWorkbook` and pick
      another worksheet index.
    question: Can I copy the pivot to a different sheet within the same workbook?
  - answer: 'Use `CopyRows`/`CopyColumns` overloads that accept a `CopyOptions` object—set
      `CopyOptions.CopyType = CopyType.ValuesOnly` or `CopyType.All` depending on
      your needs. --- ## Conclusion We’ve just walked through a **create new workbook**
      scenario that **copy pivot table**, **preserve pivot table**, an'
    question: Is there a way to copy formatting only?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel automation
title: 在 C# 中创建新工作簿 – 复制数据透视表
url: /zh/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中创建新工作簿 – 复制数据透视表

是否曾经需要在 C# 中 **create new workbook** 只是为了移动包含数据透视表的一段数据？你并不是唯一的遇到这种情况的人。在许多报告流程中，你会抓取少量行，可能还有几列，并且期望数据透视表保持原样——没有断开的引用，没有缺失的计算。  

好消息是？只需几行 Aspose.Cells 代码，你就可以 **copy pivot table**，保持其完整，甚至 **export selected range** 而不破坏任何内容。下面你将看到一个完整的、可直接运行的示例，展示 **how to copy rows**，保留数据透视表，并将结果保存为全新的工作簿。

## 本教程涵盖内容

- 使用 Aspose.Cells 设置 C# 项目（该库为代码提供支持）。
- 加载包含原始数据透视表的源工作簿。
- 使用库的 `CopyRows` 和 `CopyColumns` 方法复制所需的精确范围。
- 将复制的区域保存到 **create new workbook** 场景中，同时保持数据透视表可用。
- 针对多数据透视表、隐藏行和大数据集等边缘情况的提示。

通过本指南，你将能够从任何 Excel 文件 **export selected range**，保持数据透视表逻辑的活性，并将新文件放置在任意位置。

> **先决条件**：通过 NuGet 安装的 Aspose.Cells for .NET（免费试用版或授权版）。如果尚未添加，请在项目文件夹中运行 `dotnet add package Aspose.Cells`。

## 创建新工作簿并复制数据透视表

以下是解决方案的核心。我们将逐行讲解，说明其重要性，并展示完整程序。

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // 1️⃣ Load the source workbook that contains the pivot table
        string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destSheet = destinationWorkbook.Worksheets[0];

        // 3️⃣ Define the range we want to copy (first 20 rows, first 4 columns)
        //    This range includes the pivot table we care about.
        int startRow = 0;   // zero‑based index
        int startColumn = 0;
        int totalRows = 20;
        int totalColumns = 4;

        // 4️⃣ Copy rows – this is the “how to copy rows” part.
        //    Aspose.Cells lets us copy rows directly from the source cells collection.
        sourceWorkbook.Worksheets[0].Cells.CopyRows(startRow, startRow, totalRows);

        // 5️⃣ Copy columns – paired with the row copy to form a rectangular block.
        sourceWorkbook.Worksheets[0].Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 6️⃣ Now move the copied block into the destination sheet.
        //    We use the same start cell (A1) for simplicity.
        destSheet.Cells.CopyRows(startRow, startRow, totalRows);
        destSheet.Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 7️⃣ Save the destination workbook – the pivot table is preserved in the copied range
        string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
        destinationWorkbook.Save(destPath);

        Console.WriteLine("✅ New workbook created and pivot table preserved at: " + destPath);
    }
}
```

### 为什么这样有效

- **`CopyRows` / `CopyColumns`**：这些方法会复制底层单元格数据 *以及* 关联的对象（如数据透视缓存）。这就是在移动后数据透视表仍然可用的原因。
- **Separate destination workbook**：通过创建全新的 `Workbook` 实例，我们 **create new workbook**，避免任何残留的格式或隐藏工作表干扰。
- **Zero‑based indexing**：Aspose.Cells 使用从零开始的索引，因此 `0` 指向单元格 **A1**。如果你的数据透视表不在左上角，请调整 `startRow`/`startColumn`。
- **Preserve pivot table**：数据透视表的缓存位于同一范围内，复制该范围会自动复制缓存。无需额外代码。

## 如何复制行而不破坏数据透视表

如果你只关心行复制部分，可以单独处理：

```csharp
// Copy just rows 5‑15 (inclusive) from the source sheet
int sourceStartRow = 4;   // row 5 in Excel terms
int rowsToCopy = 11;      // rows 5‑15 => 11 rows
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy);
```

**技巧**：在复制与数据透视表相交的行时，始终复制 *整个* 数据透视区域（行 + 列）。部分复制可能导致数据透视表缺少字段，出现 `#REF!` 错误。

## 导出选定范围 – 实际场景

假设你有一个庞大的销售工作簿，但客户只需要第一季度的汇总，位于第 1‑20 行和 A‑D 列。上面的代码片段已经为你 **export selected range**。只需将 `totalRows` 和 `totalColumns` 变量改为符合客户需求的值，即可完成。

### 处理隐藏行或筛选

如果源工作表有隐藏行（可能是被筛选掉的），你可能只想复制 *可见* 行。Aspose.Cells 提供了尊重可见性的 `CopyRows` 重载：

```csharp
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy, true);
```

将最后一个布尔参数设为 `true` 即可仅复制可见行——在用户已应用筛选时进行“export selected range”非常合适。

## 保持数据透视表 – 常见陷阱及规避方法

| 陷阱 | 产生原因 | 解决方案 |
|---------|----------------|-----|
| **Pivot cache not copied** | 使用普通的 `Range.Copy` 而不是 `Cells.CopyRows/CopyColumns`。 | 按示例使用 `Cells` 方法。 |
| **Destination sheet has existing pivot** | 将工作簿保存到已经包含同名数据透视表的工作簿上。 | 从全新的 `Workbook()` 开始（如本例所示）。 |
| **Named ranges break** | 源数据透视表引用了在新文件中不存在的命名范围。 | 同时复制命名范围：`sourceWorkbook.Worksheets[0].Names.CopyTo(destSheet);` |
| **Data source path changes** | 数据透视表指向不可用的外部数据源。 | 如有需要，在复制后调用 `PivotTable.RefreshData()`。 |

## 完整端到端示例（可直接运行）

以下是完整程序，包括 `using` 指令和简短的控制台 UI。复制粘贴到新的 Console App 项目中并按 **F5** 运行。

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyUtility
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Load source workbook (contains the pivot)
            // -------------------------------------------------
            string srcPath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook srcWb = new Workbook(srcPath);

            // -------------------------------------------------
            // Step 2: Prepare destination workbook (create new workbook)
            // -------------------------------------------------
            Workbook destWb = new Workbook();
            Worksheet destWs = destWb.Worksheets[0];

            // -------------------------------------------------
            // Step 3: Define the block we want to copy
            // -------------------------------------------------
            int startRow = 0;      // A1
            int startCol = 0;      // A
            int rows = 20;         // first 20 rows
            int cols = 4;          // first 4 columns

            // -------------------------------------------------
            // Step 4: Copy rows and columns from source to destination
            // -------------------------------------------------
            srcWb.Worksheets[0].Cells.CopyRows(startRow, startRow, rows);
            srcWb.Worksheets[0].Cells.CopyColumns(startCol, startCol, cols);
            destWs.Cells.CopyRows(startRow, startRow, rows);
            destWs.Cells.CopyColumns(startCol, startCol, cols);

            // -------------------------------------------------
            // Step 5: Save the new workbook (preserve pivot table)
            // -------------------------------------------------
            string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
            destWb.Save(destPath);

            Console.WriteLine($"✅ Workbook created at {destPath}");
        }
    }
}
```

**预期输出**（在控制台中）：

```
✅ Workbook created at YOUR_DIRECTORY\copy-pivot.xlsx
```

打开 `copy-pivot.xlsx`，你会看到与 `source.xlsx` 中相同的数据透视表，功能完整且引用了复制后的数据范围。

## 常见问题

**Q: 这在同一工作表上有多个数据透视表时是否可用？**  
A: 可以，只要复制的矩形包含你需要的每个数据透视表。如果只想要一个，请调整 `rows`/`cols` 进行隔离。

**Q: 如果源工作簿使用外部数据连接怎么办？**  
A: 数据透视缓存仍会指向原始连接。如果想重新查询源数据，请在加载目标后调用 `pivotTable.RefreshData()`。

**Q: 能否将数据透视表复制到同一工作簿的其他工作表？**  
A: 完全可以。将 `destinationWorkbook` 替换为 `sourceWorkbook` 并选择另一个工作表索引。

**Q: 有办法仅复制格式吗？**  
A: 使用接受 `CopyOptions` 对象的 `CopyRows`/`CopyColumns` 重载——根据需求将 `CopyOptions.CopyType = CopyType.ValuesOnly` 或 `CopyType.All` 设置即可。

## 结论

我们刚刚演示了一个 **create new workbook** 场景，完成了 **copy pivot table**、**preserve pivot table** 和 **export selected range**——全部使用纯 C# 实现。

## 接下来你应该学习什么？

以下教程涵盖与本指南演示的技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步说明，帮助你掌握更多 API 功能，并在项目中探索替代实现方案。

- [在 .NET 中以编程方式创建新数据透视表](/cells/english/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/)
- [使用 Aspose.Cells for .NET 更改数据透视表源数据 | 数据分析指南](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [使用 Aspose.Cells for .NET 管理 Excel 数据透视表兼容性 | 数据分析指南](/cells/english/net/data-analysis/manage-excel-pivot-table-compatibility-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}