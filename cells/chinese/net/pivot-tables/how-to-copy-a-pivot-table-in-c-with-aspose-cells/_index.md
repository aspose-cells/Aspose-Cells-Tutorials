---
category: general
date: 2026-09-27
description: 学习如何使用 Aspose.Cells 在 C# 中复制数据透视表。包括复制带格式的行、将数据透视表复制到另一个工作表以及将数据透视表导出到新工作簿。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy rows with formatting
- copy pivot table to another sheet
- how to copy excel rows
- export pivot table to new workbook
language: zh
lastmod: 2026-09-27
og_description: 如何使用 Aspose.Cells 在 C# 中复制数据透视表。请按照分步指南复制带格式的行，将数据透视表移动到另一个工作表，并将其导出到新工作簿。
og_image_alt: Excel sheet showing a copied pivot table after using Aspose.Cells
og_title: 如何在 C# 中复制数据透视表 – 完整 Aspose.Cells 指南
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to copy a pivot table in C# using Aspose.Cells. Includes
    copy rows with formatting, copy pivot table to another sheet, and export pivot
    table to a new workbook.
  headline: How to copy a pivot table in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot table
title: 如何在 C# 中使用 Aspose.Cells 复制数据透视表
url: /zh/net/pivot-tables/how-to-copy-a-pivot-table-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.Cells 复制数据透视表

如果您需要 **复制数据透视表** 从一个工作表到另一个工作表，学习 **如何在 C# 中复制数据透视表** 使用 Aspose.Cells 可以为您节省大量手动操作的时间。该方法还能 **复制带格式的行**、保持数据透视缓存完整，甚至在需要独立文件时 **将数据透视表导出到新工作簿**。

本教程将带您完成完整工作流：

* 创建工作簿，  
* 复制数据透视表范围并保留格式，  
* 将复制的数据放置到新工作表上，  
* 将结果保存为单独的文件。

您将了解内置的 `CopyRows` 方法为何是 **将数据透视表复制到另一张工作表** 最可靠的方式，并获得处理隐藏行或外部数据源等边缘情况的技巧。

## 前置条件

在开始之前，请确保您具备以下条件：

| 要求 | 为什么重要 |
|------|------------|
| .NET 6.0 或更高版本 | Aspose.Cells 支持 .NET 6+，并提供最佳性能。 |
| Visual Studio 2022（或任意 C# IDE） | 您需要能够恢复 NuGet 包的编辑器。 |
| Aspose.Cells for .NET（NuGet 包 `Aspose.Cells`） | 本库提供本文示例中使用的 `CopyRows` API。 |
| 包含数据透视表的源 Excel 文件（`source.xlsx`），范围为 `A1:G20` | 代码会复制此特定范围；如果您的数据透视表更大，请相应调整范围。 |

使用 NuGet CLI 或包管理器控制台安装库：

```bash
dotnet add package Aspose.Cells
```

## 步骤 1：加载包含数据透视表的工作簿

第一行创建一个表示整个 Excel 文件的 `Workbook` 对象。一次性加载文件即可对每个工作表进行读写访问。

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **此步骤重要原因** – 未加载工作簿，后续的 `CopyRows` 调用将无法引用源数据或数据透视缓存。

## 步骤 2：准备源工作表和目标工作表

您需要一个目标工作表来存放复制后的数据透视表。下面的代码获取原始数据透视表所在的第一个工作表，并添加一个名为 **Copy** 的新工作表。

```csharp
// Get the source worksheet (index 0 = first sheet)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a new worksheet that will receive the copied rows
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
```

> **专业提示**：如果目标工作表已存在，请先调用 `Worksheets.RemoveAt(index)` 删除，以避免名称重复。

## 步骤 3：定义包含数据透视表的单元格区域

`CellArea` 对象描述了要移动的范围的左上角和右下角单元格。在本例中，数据透视表占据 `A1:G20`。如表格更大，请相应调整坐标。

```csharp
// Define the range that includes the pivot table (A1:G20)
CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");
```

## 步骤 4：复制带格式的行并保留数据透视缓存

`CopyRows` 方法将 **行** 从源工作表复制到目标工作表。通过传入 `CopyOptions.CopyAll`，您可以确保值、格式、图表以及嵌入对象——这些都是数据透视表的一部分——全部被转移。

```csharp
// Copy the rows from the source area to the destination sheet
sourceSheet.CopyRows(
    sourceArea.StartRow,          // start row in the source sheet
    destinationSheet,            // target worksheet
    0,                            // start row in the destination sheet
    sourceArea.RowCount,          // number of rows to copy
    CopyOptions.CopyAll);        // copy everything (values, formats, objects, etc.)
```

### 为什么 `CopyRows` 比 `Copy` 更适合数据透视表

* `CopyRows` 会尊重内部的数据透视缓存，复制后的数据透视表仍然可用。  
* 它完整保留 **复制带格式的行**，与原始工作表完全一致。  
* 与单纯的范围 `Copy` 不同，它还能复制隐藏行以及关联的切片器。

## 步骤 5：保存包含复制后数据透视表的工作簿

最后，将修改后的工作簿写入磁盘。新文件包含原始工作表以及一个名为 **Copy** 的工作表，后者保存了功能完整的原始数据透视表副本。

```csharp
// Save the workbook to a new file
workbook.Save(@"YOUR_DIRECTORY\pivot_copied.xlsx");
```

### 预期结果

打开 `pivot_copied.xlsx` 时：

* **Sheet1** 仍然包含原始数据和数据透视表。  
* **Copy** 工作表显示一个与原始完全相同的数据透视表，布局、筛选和格式保持一致。  
* 所有公式和数据连接保持完整，因为数据透视缓存已随行一起复制。

## 如何在同一工作簿的另一张工作表中复制数据透视表

如果只需要将数据透视表放到已有的其他工作表（例如 “Report”），请将目标工作表创建步骤替换为对目标工作表的引用：

```csharp
Worksheet destinationSheet = workbook.Worksheets["Report"]; // existing sheet
sourceSheet.CopyRows(sourceArea.StartRow, destinationSheet, 0,
                     sourceArea.RowCount, CopyOptions.CopyAll);
```

此代码片段演示了 **将数据透视表复制到另一张工作表**，而无需创建新工作表。

## 将数据透视表导出到新工作簿

有时您希望将数据透视表放在完全独立的文件中。复制操作完成后，您可以删除除包含复制后数据透视表的工作表之外的所有工作表，然后保存：

```csharp
// Keep only the copied sheet
for (int i = workbook.Worksheets.Count - 1; i >= 0; i--)
{
    if (workbook.Worksheets[i].Name != "Copy")
        workbook.Worksheets.RemoveAt(i);
}

// Save as a new workbook containing only the pivot table
workbook.Save(@"YOUR_DIRECTORY\pivot_only.xlsx");
```

现在 `pivot_only.xlsx` 只包含一个带有复制后数据透视表的工作表，满足 **将数据透视表导出到新工作簿** 的需求。

## 如何复制 Excel 行而不丢失格式

相同的 `CopyRows` 调用适用于任何范围，而不仅限于数据透视表。如果需要 **复制 Excel 行**，且这些行包含条件格式、数据验证或合并单元格，请使用同样的方法：

```csharp
// Example: copy rows 30‑40 from Sheet1 to Sheet2
sourceSheet.CopyRows(29, // zero‑based index for row 30
                     workbook.Worksheets["Sheet2"],
                     0,
                     11, // rows 30‑40 = 11 rows
                     CopyOptions.CopyAll);
```

因为 `CopyOptions.CopyAll` 会转移所有内容，目标行看起来与源行完全一致。

## 常见陷阱及规避方法

| 陷阱 | 症状 | 解决方案 |
|------|------|----------|
| 源范围未覆盖整个数据透视表 | 复制后数据透视表被截断。 | 确认 `CellArea` 包含数据透视表的所有行列。 |
| 目标工作表已存在数据 | 被覆盖的行导致数据丢失。 | 使用全新工作表或在更高的行索引处开始复制。 |
| 数据透视表使用外部数据源 | 复制后失去连接。 | 复制后调用 `pivotTable.RefreshData()` 重新建立链接。 |
| 隐藏行被省略 | 某些行在复制后消失。 | `CopyRows` 会自动复制隐藏行；确保未使用 `CopyOptions.CopyValuesOnly`。 |

## 完整可运行示例

下面是一个可直接粘贴到新控制台项目中的完整程序，演示本文讨论的每一步。

```csharp
using System;
using Aspose.Cells;

namespace PivotTableCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains the pivot table
            string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2️⃣ Get source and destination worksheets
            Worksheet sourceSheet = workbook.Worksheets[0]; // first sheet
            Worksheet destinationSheet = workbook.Worksheets.Add("Copy");

            // 3️⃣ Define the cell area that holds the pivot table (A1:G20)
            CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");

            // 4️⃣ Copy rows with formatting and keep the pivot cache
            sourceSheet.CopyRows(
                sourceArea.StartRow,      // start row index (0‑based)
                destinationSheet,        // target sheet
                0,                        // start row in destination
                sourceArea.RowCount,      // number of rows to copy
                CopyOptions.CopyAll);    // copy everything

            // 5️⃣ Save the workbook with the copied pivot table
            string destPath = @"YOUR_DIRECTORY\pivot_copied.xlsx";
            workbook.Save(destPath);

            Console.WriteLine("Pivot table copied successfully to " + destPath);
        }
    }
}
```

**运行该程序** 将生成 `pivot_copied.xlsx`，其中新建的 **Copy** 工作表上拥有原始数据透视表的完整副本。

## 结论

您现在已经掌握了在 C# 中使用  

## 接下来应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助您进一步深入 API 功能并探索在项目中的替代实现方式。每篇资源都提供了完整的可运行代码示例和逐步解释。

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy Pivot Table in C# – Complete Step‑by‑Step Guide](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [How to copy range with pivot tables in C# – Complete Guide](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}