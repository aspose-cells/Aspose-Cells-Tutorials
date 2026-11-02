---
category: general
date: 2026-10-04
description: 学习如何使用 C# 将数据透视表从一个工作簿复制到另一个工作簿。本指南还涵盖如何复制行、复制数据透视表以及高效复制 Excel 区域。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- how to copy rows
- duplicate pivot table
language: zh
lastmod: 2026-10-04
og_description: 使用 C# 复制 Excel 中的数据透视表。通过本完整教程学习如何复制数据透视表、复制行以及使用 Aspose.Cells 复制
  Excel 区域。
og_image_alt: Screenshot showing a duplicated pivot table in an Excel worksheet after
  using C# code
og_title: 使用 C# 复制 Excel 数据透视表 – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to copy pivot table from one workbook to another using C#.
    This guide also covers how to copy rows, duplicate pivot table, and copy Excel
    range efficiently.
  headline: How to copy pivot table in Excel with C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: 如何使用 C# 和 Aspose.Cells 复制 Excel 透视表
url: /zh/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 C# 和 Aspose.Cells 复制 Excel 透视表

如果您需要 **复制透视表** 从一个工作簿到另一个工作簿，本教程将展示一个完整、可运行的解决方案。您将看到如何加载源文件、定义包含透视表的范围、复制行（包括透视表定义），以及保存结果。无论是自动化报表流程还是构建迁移工具，下面的步骤只需几行 C# 代码即可实现透视表的复制。

复制透视表不仅仅是复制单元格的值；底层缓存和字段设置必须一起迁移。示例使用 **Aspose.Cells** 库，因为它会自动处理透视表的元数据，您无需手动重建缓存。阅读完本指南后，您将能够 **如何复制透视表**、**复制 Excel 区域**，以及 **如何复制行**，并确保安全可靠。

## 前置条件

在开始之前，请确保您具备以下条件：

- 已安装 .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.7+）。
- 有效的 Aspose.Cells for .NET 许可证或临时评估许可证。
- 两个 Excel 文件：`Source.xlsx`（包含您要复制的透视表）以及一个用于写入 `CopyWithPivot.xlsx` 的空文件夹。
- Visual Studio 2022（或任何支持 C# 的 IDE）。

## 第 1 步：创建项目并添加 Aspose.Cells

创建一个新的控制台项目并添加 Aspose.Cells NuGet 包：

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
dotnet add package Aspose.Cells
```

该包提供了本文代码中使用的 `Workbook`、`Worksheet` 和 `CellArea` 类。

## 第 2 步：加载包含透视表的源工作簿

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the source workbook that holds the pivot you want to duplicate
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");
```

> **为什么重要：** 加载工作簿会在内存中创建所有工作表的表示，包括任何隐藏的透视缓存。未加载文件时，您无法引用透视表的范围。

## 第 3 步：定义覆盖透视表的单元格区域

您必须告诉 Aspose.Cells 哪些行列属于透视表。`CellArea` 结构体用于指定一个矩形块。

```csharp
        // Define the rectangle that encloses the pivot table (adjust as needed)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,      // first row (zero‑based)
            StartColumn = 0,   // first column
            EndRow = 30,       // last row of the pivot
            EndColumn = 10     // last column of the pivot
        };
```

> **提示：** 如果不确定确切大小，可在 Excel 中打开源文件，选中透视表，并在名称框中查看范围（例如 `A1:K31`）。将 Excel 坐标转换为从零开始的索引用于代码。

## 第 4 步：创建目标工作簿并获取其第一个工作表

```csharp
        // Create an empty workbook that will receive the copied pivot
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

> **为什么需要此步骤：** 在复制行之前必须先存在目标工作簿。Aspose.Cells 会自动创建默认工作表，我们将其用作目标。

## 第 5 步：将行（包括透视表）从源复制到目标

`CopyRows` 方法会复制单元格值以及底层的透视缓存。

```csharp
        // Copy rows from source to destination, preserving the pivot definition
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,      // source cells
            sourceRange.StartRow,                 // first row to copy
            sourceRange.EndRow - sourceRange.StartRow + 1, // number of rows
            destWorksheet.Cells,                  // target cells
            sourceRange.StartRow);                // target start row
```

> **工作原理：**  
> - `CopyRows` 接收源工作表、起始行以及要复制的行数。  
> - 同时接收目标工作表以及复制应开始的行号。  
> - 因为源范围包含透视表，该方法会完整转移透视的缓存、字段列表和布局。这正是 **如何复制透视表** 而不丢失功能的核心。

### 边缘情况：复制跨多个工作表的透视表

如果透视表的源数据位于与透视表本身不同的工作表，缓存仍会随复制一起迁移，因为 Aspose.Cells 将缓存存储在工作簿级别，而非工作表级别。不过，您必须确保目标工作簿中也包含相同的源数据范围；否则透视表会显示 `#REF!` 错误。在这种情况下，请先复制源数据范围，再复制透视表行。

## 第 6 步：保存已包含复制透视表的工作簿

```csharp
        // Persist the destination workbook to disk
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

运行程序后会生成 `CopyWithPivot.xlsx`，其中的透视表与原始透视表完全相同，包含所有切片器、筛选器和计算字段。

### 预期输出

打开 `CopyWithPivot.xlsx` 时：

- 透视表出现在与 `Source.xlsx` 相同的位置（例如 A1:K31）。
- 所有行列标签、合计以及格式均被保留。
- 刷新透视表后显示的数据与源文件相同，说明缓存已正确复制。

## 如何在没有透视表的情况下复制行（复制 Excel 区域）

如果只需要 **复制 Excel 区域** 而不涉及透视表数据，可以使用相同的 `CopyRows` 方法，只需指向不包含透视表的范围。例如：

```csharp
// Copy a simple data table from rows 5‑15, columns A‑D
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    4,            // start at row 5 (zero‑based)
    11,           // copy 11 rows (5‑15 inclusive)
    destWorksheet.Cells,
    0);           // paste at the top of the destination sheet
```

这演示了 **如何复制行** 用于普通数据，进一步体现同一 API 的多功能性。

## 在同一工作簿中复制透视表（替代方案）

有时您希望在同一工作簿内 **复制透视表**，而不是创建新文件。可以通过将行复制到不同位置实现：

```csharp
// Duplicate pivot table to start at row 40 in the same worksheet
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    sourceRange.StartRow,
    sourceRange.EndRow - sourceRange.StartRow + 1,
    destWorksheet.Cells,
    40); // destination start row (zero‑based)
```

保存后，工作簿将包含两个相同的透视表——适用于并排比较或创建备份。

## 常见陷阱及规避方法

| 陷阱 | 产生原因 | 解决方案 |
|---------|----------------|-----|
| 复制后透视表显示 `#REF!` | 目标工作簿中缺少源数据范围 | 先复制源数据范围，或在复制透视表前先对源数据工作表使用 `CopyRows` |
| 格式丢失 | 仅复制了数值（例如使用 `Copy` 而非 `CopyRows`） | 始终使用 `CopyRows`，它会保留样式、格式以及透视元数据 |
| 行偏移异常 | 目标起始行与源起始行不匹配 | 确认 `destWorksheet.Cells` 的起始行与预期位置一致 |
| 大型工作簿导致内存压力 | `CopyRows` 会将整个工作表加载到内存 | 将复制过程分块处理，或在处理超过 100,000 行时使用流式 API |

## 完整可运行示例

下面是完整的程序代码，您可以直接粘贴到 `Program.cs` 并立即运行（将 `YOUR_DIRECTORY` 替换为您机器上的实际路径）。

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook containing the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");

        // 2️⃣ Define the area that encloses the pivot (adjust to your sheet)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 30,
            EndColumn = 10
        };

        // 3️⃣ Create the destination workbook (empty) and get its first sheet
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // 4️⃣ Copy rows—including the pivot cache—into the destination
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,
            sourceRange.StartRow,
            sourceRange.EndRow - sourceRange.StartRow + 1,
            destWorksheet.Cells,
            sourceRange.StartRow);

        // 5️⃣ Save the result
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

使用 `dotnet run` 运行程序。执行完毕后，打开 `CopyWithPivot.xlsx` 验证透视表是否与源文件完全一致。

## 结论

现在，您已经掌握了使用 C# 和 Aspose.Cells **复制透视表** 的完整流程。本文涵盖了从加载源文件、定义透视表单元格区域、复制行到保存目标工作簿的全部步骤。您还学会了 **如何复制行**、**复制 Excel 区域**，以及在同一文件中 **复制透视表** 的方法，并了解了常见陷阱和最佳实践。

准备好下一步了吗？尝试添加代码以编程方式刷新复制后的透视表，或使用 Aspose.Cells 将透视表导出为 PDF。尝试不同的源范围，您将快速掌握 .NET 中的 Excel 自动化。

---


## 接下来应该学习什么？

以下教程涵盖了与本指南技术密切相关的主题，帮助您进一步深化对 API 的使用并探索替代实现方式。

- [Copy Pivot Table in C# – Complete Step‑by‑Step Guide](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [copy rows excel – Preserve Pivot Table While Duplicating Rows](/cells/english/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}