---
category: general
date: 2026-07-29
description: 将行从一个工作表复制到另一个工作表，并在一步步的教程中学习如何使用 Aspose.Cells 以编程方式加载 Excel 工作簿。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy rows from one worksheet to another
- load excel workbook programmatically
- Aspose.Cells copy rows
- C# Excel automation
- worksheet data transfer
language: zh
lastmod: 2026-07-29
og_description: 使用 Aspose.Cells 将行从一个工作表复制到另一个工作表。学习如何以编程方式加载 Excel 工作簿，并在几行 C# 代码中保留数据透视表。
og_image_alt: Screenshot showing C# code that copies rows from one worksheet to another
  while preserving pivot tables
og_title: 将行从一个工作表复制到另一个工作表 – C# Excel 自动化指南
schemas:
- author: Aspose
  dateModified: '2026-07-29'
  description: Copy rows from one worksheet to another and learn how to load Excel
    workbook programmatically using Aspose.Cells in a step‑by‑step tutorial.
  headline: Copy rows from one worksheet to another – Complete C# Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Replace `destinationWorkbook.Worksheets[0]` with `destinationWorkbook.Worksheets["TargetSheet"]`
      (create the sheet first if it doesn’t exist).
    question: Can I copy to a specific worksheet instead of the first one?
  - answer: Use `CopyRows` with the overload that accepts a `CopyRowsOptions` object
      and set `PasteType` to `PasteType.Values`.
    question: What if I need to copy only values, not formulas?
  - answer: Aspose.Cells supports **streaming** via `LoadOptions` with `MemorySetting.MemoryPreference`.
      Load the source workbook with a lower memory footprint and the copy operation
      will still be efficient.
    question: How do I handle large files without exhausting memory?
  - answer: When you set the `true` flag, the pivot cache is duplicated, so the new
      workbook’s pivots reference the copied data, not the original file.
    question: Do pivot tables stay linked to the original data source?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: 将行从一个工作表复制到另一个工作表 – 完整 C# 指南
url: /zh/net/row-and-column-management/copy-rows-from-one-worksheet-to-another-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将行从一个工作表复制到另一个工作表 – 完整 C# 指南

是否曾经需要 **将行从一个工作表复制到另一个工作表**，但不确定如何保持公式和数据透视表完整？你并不孤单。在许多报告流水线中，我们必须从主工作表中提取一部分数据并放入全新的工作簿，以便后续处理。好消息是？使用 Aspose.Cells，你可以通过编程实现，而且整个操作只需几行代码。

在本教程中，我们将演示如何以编程方式加载 Excel 工作簿、选择一个范围，然后将这些行复制到全新的工作簿，同时保留任何嵌入的数据透视表。完成后，你将拥有一个可复用的代码片段，能够直接放入任何 C# 项目——无需手动复制粘贴。

## 您将实现的目标

- **以编程方式加载 Excel 工作簿**，使用 Aspose.Cells 的 `Workbook` 类。  
- 定义包含要移动行的 **单元格区域**。  
- 使用单一方法调用 **将行从一个工作表复制到另一个工作表**，并保持数据透视表有效。  
- 将结果保存为新文件，以便分发或进一步处理。

### 前置条件

- .NET 6.0 或更高版本（代码在 .NET Core 和 .NET Framework 上均可运行）。  
- 有效的 Aspose.Cells 许可证（或临时评估密钥）。  
- 磁盘上两个文件夹：一个用于源工作簿（`Source.xlsx`），一个用于目标工作簿（`Destination.xlsx`）。  

如果你已经准备好这些，下面开始吧。

## 步骤 1：以编程方式加载 Excel 工作簿

首先，在能够复制之前，需要将源文件加载到内存中。Aspose.Cells 让这一步变得轻而易举：

```csharp
using Aspose.Cells;

// Load the source workbook from disk
Workbook sourceWorkbook = new Workbook(@"C:\Data\Source.xlsx");
```

> **为什么这很重要：** 以编程方式加载工作簿让你能够完全控制文件内容，而无需在服务器上打开 Excel。它还能避免 COM 互操作的麻烦，并且可以在 CI 流水线等无头环境中运行。

## 步骤 2：定义包含行的源范围

接下来，准确定位你想要转移的行。`CellArea` 对象允许使用左上角和右下角单元格地址来指定一个矩形块：

```csharp
// Define the area A1:H20 – adjust as needed
CellArea sourceRange = CellArea.CreateCellArea("A1", "H20");
```

> **小技巧：** 如果你的数据量会动态变化，可以使用 `sourceWorksheet.Cells.MaxDataRow` 来计算 `EndRow`，从而始终捕获完整表格。

## 步骤 3：为目标创建一个全新的工作簿

现在创建一个空工作簿，用来接收复制的行。默认情况下，这个工作簿只包含一个工作表：

```csharp
// Create a new, empty workbook
Workbook destinationWorkbook = new Workbook();
```

> **为什么要新建工作簿？** 从空白开始可以确保不会意外覆盖已有数据，并为测试提供可预测的环境。

## 步骤 4：将行从一个工作表复制到另一个工作表（保留数据透视表）

下面是本教程的核心。`CopyRows` 方法复制选定的行，并且当你将最后一个参数设为 `true` 时，还会复制范围内的所有数据透视表：

```csharp
// Perform the copy operation
destinationWorkbook.Worksheets[0].Cells.CopyRows(
    sourceWorkbook.Worksheets[0],      // source worksheet
    sourceRange.StartRow,              // first row to copy (0‑based)
    sourceRange.EndRow,                // last row to copy (inclusive)
    destinationWorkbook.Worksheets[0].Cells, // target worksheet
    0,                                 // target start row (top of sheet)
    true);                             // preserve pivot tables
```

### 这背后发生了什么？

- **源工作表**：`sourceWorkbook.Worksheets[0]` 指向源文件中的第一个工作表。  
- **行索引**：Aspose.Cells 使用零基索引，因此 `StartRow` 和 `EndRow` 对应于你在 `sourceRange` 中定义的行。  
- **目标起始行**：我们在新工作表的第 0 行开始，等同于将复制的块放在最顶部。  
- **`true` 标志**：这就是魔法开关，告诉 Aspose.Cells 克隆复制行内的任何数据透视表，保留其缓存和连接。

> **边缘情况警告：** 如果源范围包含跨出定义区域的合并单元格，这些合并将被截断。若需保持完整，请将范围扩展至覆盖整个合并区域。

## 步骤 5：保存目标工作簿

最后，将新文件写入磁盘。你可以选择任意文件夹，只需确保进程拥有写入权限：

```csharp
// Save the result
destinationWorkbook.Save(@"C:\Data\Destination.xlsx");
```

打开 `Destination.xlsx` 后，你会看到 A1‑H20 行已被复制，且原本嵌入的所有数据透视表也随之复制。工作簿的其余部分保持为空，方便你后续添加更多工作表或数据。

## 完整可运行示例

将上述步骤整合起来，下面是完整的可运行程序：

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook programmatically
        Workbook sourceWorkbook = new Workbook(@"C:\Data\Source.xlsx");

        // 2️⃣ Define the source range (adjust as needed)
        CellArea sourceRange = CellArea.CreateCellArea("A1", "H20");

        // 3️⃣ Create a new destination workbook
        Workbook destinationWorkbook = new Workbook();

        // 4️⃣ Copy rows from one worksheet to another, preserving pivot tables
        destinationWorkbook.Worksheets[0].Cells.CopyRows(
            sourceWorkbook.Worksheets[0],
            sourceRange.StartRow,
            sourceRange.EndRow,
            destinationWorkbook.Worksheets[0].Cells,
            0,
            true);

        // 5️⃣ Save the result
        destinationWorkbook.Save(@"C:\Data\Destination.xlsx");

        Console.WriteLine("Rows successfully copied! Check C:\\Data\\Destination.xlsx");
    }
}
```

**预期输出**（控制台）：

```
Rows successfully copied! Check C:\Data\Destination.xlsx
```

打开目标文件，验证数据、格式以及数据透视表是否与源文件完全一致。如果发现缺失，请再次检查 `sourceRange` 是否完整覆盖了相关行。

## 常见问题与技巧

- **可以将复制的内容放到特定工作表而不是第一个吗？**  
  完全可以。将 `destinationWorkbook.Worksheets[0]` 替换为 `destinationWorkbook.Worksheets["TargetSheet"]`（如果工作表不存在，请先创建）。

- **如果只想复制数值而不是公式怎么办？**  
  使用接受 `CopyRowsOptions` 对象的 `CopyRows` 重载，并将 `PasteType` 设置为 `PasteType.Values`。

- **如何在处理大文件时避免内存耗尽？**  
  Aspose.Cells 支持通过 `LoadOptions` 的 `MemorySetting.MemoryPreference` 进行 **流式加载**。以较低的内存占用加载源工作簿，复制操作仍然高效。

- **数据透视表会保持链接到原始数据源吗？**  
  当你设置 `true` 标志时，透视缓存会被复制，新工作簿的透视表引用的是复制后的数据，而不是原始文件。

## 总结

现在，你已经掌握了 **在保持数据透视表完整的前提下，将行从一个工作表复制到另一个工作表** 的方法，并了解了如何 **以编程方式加载 Excel 工作簿**，这为构建自动化报告流水线、数据迁移脚本或任何需要即时拼接 Excel 数据的场景提供了坚实基础。

接下来可以尝试扩展代码片段：

- 循环遍历多个源范围并汇总到单个目标文件。  
- 在复制后应用条件格式，以突出关键指标。  
- 将最终工作簿导出为 PDF 或 CSV，以供下游使用。

尽情实验吧，如有问题，欢迎在下方留言。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助你进一步掌握 API 功能并探索在项目中的替代实现方式，每篇资源均提供完整的可运行代码示例和逐步解释。

- [如何使用 Aspose.Cells for .NET 复制 Excel 行：C# 指南](/cells/english/net/worksheet-management/copy-rows-excel-aspose-cells-net-guide/)
- [使用 Aspose.Cells 将工作表从一个工作簿复制到另一个工作簿](/cells/english/net/worksheet-value-operations/copy-worksheet-between-workbooks/)
- [如何使用 Aspose.Cells for .NET 导出可见的 Excel 行：分步指南](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}