---
category: general
date: 2026-03-30
description: 如何在 C# 中使用 Aspose.Cells 复制工作表 – 步骤指南，涵盖复制单元格范围、在工作表之间复制列、复制工作表透视表以及添加新工作表的代码。
draft: false
keywords:
- how to copy worksheet
- copy cell range
- copy columns between sheets
- copy worksheet pivot table
- add new worksheet code
language: zh
og_description: 学习如何使用 Aspose.Cells 在 C# 中复制工作表。本指南展示了复制单元格范围、保留数据透视表、在工作表之间复制列以及添加新工作表的代码。
og_title: 如何在 C# 中复制工作表 – 完整的 Aspose.Cells 教程
tags:
- Aspose.Cells
- C#
- Excel Automation
title: 如何在 C# 中使用 Aspose.Cells 复制工作表 – 完整指南
url: /zh/net/excel-copy-worksheet/how-to-copy-worksheet-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.Cells 复制工作表 – 完整指南

是否曾经想过 **如何复制工作表** 而不丢失任何数据透视表或公式？你并不孤单——很多开发者在需要复制工作表并保持所有内容完整时都会卡住。在本教程中，我们将一步步演示一个实用的端到端解决方案，不仅复制数据，还能保留 **复制工作表的数据透视表**，处理 **复制单元格范围**，并展示你需要的 **添加新工作表代码**。

我们将从加载源工作簿到保存目标文件的整个过程全部覆盖，这样你就可以在工作表之间复制列，保留对象，并保持代码整洁。没有模糊的引用，只有完整、可直接运行的示例，今天就可以放进你的项目中使用。

## 本教程涵盖内容

- 使用 Aspose.Cells 加载已有的 Excel 文件  
- 使用 **添加新工作表代码** 创建目标工作表  
- 定义包含数据透视表的 **复制单元格范围**  
- 设置 **CopyOptions** 以保持图表、公式和数据透视表完整  
- 执行 **在工作表之间复制列**，实现逐行精确复制  
- 保存结果并验证工作表是否正确复制  

阅读完本指南后，你将能够自信地回答 “如何复制工作表” 这一问题，无论是自动化报表还是构建基于电子表格的 UI。

---

## 如何复制工作表 – 概览

在深入代码之前，先梳理一下高层流程。把它想象成一道食谱：

1. **加载** 源工作簿 (`Source.xlsx`)。  
2. **添加** 一个全新的工作表来存放副本（**添加新工作表代码**）。  
3. **定义** 需要复制的区域（**复制单元格范围**）。  
4. **配置** 复制选项，使数据透视表能够保留下来（**复制工作表的数据透视表**）。  
5. **复制** 行和列（**在工作表之间复制列**）。  
6. **保存** 新工作簿 (`Destination.xlsx`)。  

就是这么简单——六个步骤，没有魔法。每一步下面都有代码片段和背后的原理说明。

---

## 第一步 – 加载源工作簿

首先，你需要一个指向要复制文件的 `Workbook` 实例。这一步至关重要，因为 Aspose.Cells 直接操作文件系统，而不是 Office UI。

```csharp
using Aspose.Cells;

// Path to the original file
string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";

// Load the workbook – this is the starting point for how to copy worksheet
Workbook workbook = new Workbook(sourcePath);
```

*为什么重要：* 加载文件会在内存中创建每个工作表、单元格和对象的表示。如果没有这一步，就没有可复制的内容，后续的 `添加新工作表代码` 也会因缺少源数据而失败。

---

## 第二步 – 添加新工作表（添加新工作表代码）

现在我们需要一个位置来粘贴复制的数据。这时 **添加新工作表代码** 派上用场。工作表名称可以随意，这里我们命名为 `"Copy"`。

```csharp
// Grab the first worksheet (the one we want to copy)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a fresh worksheet to receive the copy
Worksheet copySheet = workbook.Worksheets.Add("Copy");
```

*小技巧：* 如果需要复制多个工作表，可以在循环中调用 `Worksheets.Add` 并为每个工作表分配唯一名称。这样可以避免名称冲突，让工作簿保持整洁。

---

## 第三步 – 定义复制单元格范围

**复制单元格范围** 告诉 Aspose.Cells 要复制哪些行列。在很多实际场景中，这个范围会包含数据透视表，所以必须精准指定。

```csharp
// Define the area that contains the pivot table (A1:G20)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 19,       // Row 20
    EndColumn = 6      // Column G
};

// Destination range – we start at the same top‑left corner
CellArea destinationRange = new CellArea
{
    StartRow = 0,
    StartColumn = 0,
    EndRow = 19,
    EndColumn = 6
};
```

*为什么需要这一步：* 明确声明范围可以避免复制整张工作表（这会浪费资源），并确保数据透视表位于复制的区域内。这是实现 **如何复制工作表** 时，只复制部分内容的关键。

---

## 第四步 – 设置复制选项（保留复制工作表的数据透视表）

Aspose.Cells 提供了 `CopyOptions` 对象，用来控制粘贴的内容。为了保留数据透视表、图表和公式，我们将 `PasteType` 设置为 `All` 并启用 `PasteSpecial`。

```csharp
CopyOptions copyOptions = new CopyOptions
{
    PasteType = PasteType.All,   // Copy everything: values, formats, objects
    PasteSpecial = true          // Enable special paste to retain pivot tables
};
```

*说明：* `PasteType.All` 是最全面的选项，而 `PasteSpecial` 则指示引擎正确处理像数据透视表这样的复杂对象。跳过这一步是常见的陷阱，复制后的工作表会失去交互功能。

---

## 第五步 – 复制行和列（在工作表之间复制列）

下面进入核心：真正搬运数据。我们将使用 `CopyRows` 和 `CopyColumns` 来实现 **在工作表之间复制列**。两者一起使用可以保证合并单元格和列宽也被保留。

```csharp
// Copy rows from the source to the destination sheet
sourceSheet.Cells.CopyRows(
    sourceRange.StartRow,
    sourceRange.EndRow,
    copySheet.Cells,
    destinationRange.StartRow,
    copyOptions);

// Copy columns from the source to the destination sheet
sourceSheet.Cells.CopyColumns(
    sourceRange.StartColumn,
    sourceRange.EndColumn,
    copySheet.Cells,
    destinationRange.StartColumn,
    copyOptions);
```

*正在发生什么：* `CopyRows` 按行复制数据，`CopyColumns` 按列复制。两者同时执行可确保整个矩形块被完整复制，这在需要 **在工作表之间复制列** 且列宽或隐藏列不同的情况下尤为重要。

---

## 第六步 – 保存工作簿

最后，将更改写回磁盘。这一步完成了 **如何复制工作表** 的全部流程。

```csharp
// Save the workbook with the newly copied sheet
workbook.Save(destinationPath);
```

*验证小贴士：* 打开 `Destination.xlsx`，检查 `"Copy"` 工作表是否与原始工作表完全一致，数据透视表是否可用，列宽是否匹配。如有异常，请回顾 `CopyOptions` 设置。

---

## 边缘情况与常见变体

### 复制多个工作表

如果需要复制多张工作表，可将上述逻辑放入 `foreach` 循环：

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    Worksheet newWs = workbook.Worksheets.Add(ws.Name + "_Copy");
    // Re‑use sourceRange/destinationRange or calculate per sheet
    // Then call CopyRows/CopyColumns as shown earlier
}
```

### 在不同工作簿之间保留公式

当源工作簿和目标工作簿的命名范围不同，除了 `All` 之外，还可以将 `copyOptions` 设置为 `PasteType.Formulas`：

```csharp
copyOptions.PasteType = PasteType.All | PasteType.Formulas;
```

### 大范围数据与性能

对于极大数据集（数十万行），可以仅使用 `CopyRows`，如果列宽不重要则跳过 `CopyColumns`。这样可以节省几秒钟的执行时间。

---

## 完整可运行示例

下面是完整、可直接运行的程序示例，涵盖了本文所有要点。将其粘贴到控制台应用程序中，修改文件路径后按 **F5** 运行。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // ---------- Step 1: Load the source workbook ----------
        string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
        string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // ---------- Step 2: Add a new worksheet (add new worksheet code) ----------
        Worksheet sourceSheet = workbook.Worksheets[0];
        Worksheet copySheet = workbook.Worksheets.Add("Copy");

        // ---------- Step 3: Define the copy cell range ----------
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };
        CellArea destinationRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };

        // ---------- Step 4: Set copy options (preserve copy worksheet pivot table) ----------
        CopyOptions copyOptions = new CopyOptions
        {
            PasteType = PasteType.All,
            PasteSpecial = true
        };

        // ---------- Step 5: Copy rows and columns (copy columns between sheets) ----------
        sourceSheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            copySheet.Cells,
            destinationRange.StartRow,
            copyOptions);

        sourceSheet.Cells.CopyColumns(
            sourceRange.StartColumn,
            sourceRange.EndColumn,
            copySheet.Cells,
            destinationRange.StartColumn,
            copyOptions);

        // ---------- Step 6: Save the workbook ----------
        workbook.Save(destinationPath);
    }
}
```

**预期结果：** 打开 `Destination.xlsx`，会看到一个名为 **Copy** 的工作表，它完整复制了 `Source.xlsx` 的第一张工作表，包括所有数据透视表、格式和列宽。原始文件保持不变。

---

## 常见问答

**问：这段代码能处理 Excel 2019 创建的 .xlsx 文件吗？**  
答：完全可以。Aspose.Cells 支持所有现代 Excel 格式，代码同样适用于 `.xlsx`、`.xlsm`，甚至更旧的 `.xls` 文件。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}