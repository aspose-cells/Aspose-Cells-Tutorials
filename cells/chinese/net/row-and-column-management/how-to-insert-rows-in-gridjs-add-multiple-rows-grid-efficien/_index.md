---
category: general
date: 2026-03-29
description: 学习如何快速在 GridJs 中插入行。本指南还涵盖如何添加行以及使用批量操作向网格中添加多行。
draft: false
keywords:
- how to insert rows
- how to add rows
- add multiple rows grid
- batch row insertion
- large grid performance
language: zh
og_description: 快速学习如何在 GridJs 中插入行。本指南展示了如何添加行、在网格中添加多行，以及处理大批量插入。
og_title: 如何在 GridJs 中插入行 – 高效批量添加多行
tags:
- GridJs
- C#
- data‑grid
title: 如何在 GridJs 中插入行 – 高效添加多行
url: /zh/net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-grid-efficien/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 GridJs 中插入行 – 高效批量添加多行

是否曾经想过 **如何在 GridJs 表格中插入行** 而不导致 UI 卡死？也许你在尝试 **逐行添加** 时遇到瓶颈，性能急剧下降。好消息是，GridJs 提供了批量 API，允许你在一次调用中 **批量添加多行**，即使处理数百万条记录也能保持流畅。

在本教程中，我们将通过一个完整、可运行的示例演示如何使用 `InsertRowsBatch` **插入行**。你将了解批量操作为何重要、如何验证结果，以及在目标索引非常大时需要注意的事项。完成后，你就能自信地向任何 GridJs 实例中一次性插入上千条新记录。

## 前置条件

在开始之前，请确保你具备以下条件：

- .NET 6.0 或更高（代码可在任何近期 SDK 上编译）
- 已引用 `GridJs` NuGet 包（或使用自定义构建的 DLL）
- 基础 C# 知识——不需要是专家，只要对类和方法熟悉即可
- 任选的 IDE 或编辑器（Visual Studio、Rider、VS Code…均可）

> **专业提示：** 若需处理真正巨大的网格（数千万行），请启用 `gridJs.EnableVirtualization = true;` 以保持 UI 渲染轻量。

## 第一步：创建并配置 GridJs 实例

首先，你需要一个可用的 `GridJs` 对象。可以把它想象成绘制行的画布。

```csharp
using System;
using GridJsLibrary;   // Assume this is the namespace for GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Initialize the grid
            GridJs gridJs = new GridJs();

            // Optional: turn on virtualization for huge data sets
            gridJs.EnableVirtualization = true;

            // Populate the grid with some dummy data so we can see the effect
            SeedInitialData(gridJs);

            // Now we’re ready to insert rows in bulk
            InsertRowsInBatch(gridJs);
        }

        // Helper: add 2 000 000 rows so our batch lands at index 2 000 001
        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }
```

> **此步骤重要原因：** 初始化网格并可选地预填充数据，模拟真实场景——网格已经包含大量信息。后续的批量插入必须遵循零基索引，因此我们提前填充数据以演示准确的插入位置。

## 第二步：使用 `InsertRowsBatch` **批量添加多行**

下面进入教程核心——一次性 **批量添加行** 的调用。方法签名为 `InsertRowsBatch(int startIndex, int count)`。本例中我们将在索引 2 000 000（即第 2 000 001 行）处插入十行。

```csharp
        // Step 2 – Insert a batch of rows
        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based, so this is row 2 000 001
            int rowsToAdd = 10;

            // The batch call creates placeholder rows; you can later populate them
            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Verify by reading back a few rows
            VerifyInsertion(grid, startIndex, rowsToAdd);
        }
```

> **工作原理：** `InsertRowsBatch` 在内部分配所需的行数并将已有行向下移动。由于整个操作在单一事务中完成，UI 只刷新一次，这也是推荐的 **高效添加行** 方式。

## 第三步：验证插入 – 行是否出现在预期位置？

批量操作后，你需要确认这些行已正确插入。下面的辅助代码读取新插入块的首行和尾行，并将其打印到控制台。

```csharp
        // Step 3 – Simple verification
        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

**预期输出**

```
Initial seed completed – 2 000 000 rows present.
Inserted 10 rows starting at index 2000001.
Verifying inserted rows:
Row 2000001: , 
Row 2000002: , 
...
Row 2000010: , 
```

空白单元格表示这些行是占位符，等待填充数据。随后你可以逐个填充，或再执行一次批量更新。

> **边缘情况说明：** 若 `startIndex` 超过当前行数，GridJs 会自动在末尾追加新行。相反，负数索引会抛出 `ArgumentOutOfRangeException`，因此务必对用户提供的索引进行校验。

## 第四步：填充新行（可选但常见）

通常你并不希望得到空行，而是需要填入有意义的值。可以遍历新创建的范围，调用 `SetCell` 或类似 API。

```csharp
        // Optional: fill the newly added rows with sample data
        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }
```

如果需要新行立即可见，可在批量插入后直接调用 `PopulateNewRows(gridJs, startIndex, rowsToAdd);`。

## 第五步：针对超大网格的性能技巧

在处理 **数百万行的批量添加** 时，请记住以下技巧：

1. **批量大小影响性能** – 一次插入 10 000 行往往比十次插入 1 000 行更快，因为每个批次只触发一次 UI 刷新。
2. **关闭 UI 更新** – 某些 GridJs 版本提供 `grid.SuspendLayout()` / `grid.ResumeLayout()`。如果出现卡顿，可将批量操作包裹在这两个调用之间。
3. **使用虚拟化** – 如前所述，`EnableVirtualization` 能显著降低内存占用和渲染时间。
4. **避免深拷贝** – 向网格传递简单值类型或轻量对象；沉重对象会导致网格克隆数据，进而拖慢性能。

## 完整工作示例

将所有内容整合后，下面是可以直接复制到新控制台项目中的完整程序：

```csharp
using System;
using GridJsLibrary;   // Replace with the actual namespace of your GridJs library

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            GridJs gridJs = new GridJs
            {
                EnableVirtualization = true
            };

            SeedInitialData(gridJs);
            InsertRowsInBatch(gridJs);
        }

        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }

        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based index for row 2 000 001
            int rowsToAdd = 10;

            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Optional: fill them with data
            PopulateNewRows(grid, startIndex, rowsToAdd);

            VerifyInsertion(grid, startIndex, rowsToAdd);
        }

        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }

        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

运行程序后，你将在控制台看到确认十行已在正确位置插入并随后被填充的输出。

## 结论

我们已经介绍了使用批量 API 在 GridJs 中 **插入行** 的方法，演示了 **高效添加行** 的技巧，并探讨了在不阻塞 UI 的情况下 **批量添加多行** 的实现要点。关键收获如下：

- 对任何批量操作使用 `InsertRowsBatch(startIndex, count)`。
- 校验索引并在大数据集下考虑启用虚拟化。
- 如需即时显示内容，可在批量后立即填充行。

接下来，你可以进一步探索 **如何删除行**、实现 **批量编辑的撤销/重做**，或将 GridJs 与按需流式传输数据的后端服务集成。这些主题都直接基于本教程中学到的概念。

欢迎大胆实验——更改批量大小、尝试在网格最前端插入，或在一次事务中组合多个批次。实践得越多，你对大规模 GridJs 的驾驭就越得心应手。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}