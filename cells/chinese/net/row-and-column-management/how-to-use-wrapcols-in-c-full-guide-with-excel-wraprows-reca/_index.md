---
category: general
date: 2026-06-27
description: 如何在 C# 中使用 wrapcols 和 wrap rows Excel。学习使用 C# 创建 Excel 工作簿，并通过一步步示例重新计算
  Excel 公式。
draft: false
keywords:
- how to use wrapcols
- wrap rows excel
- wrap columns excel
- recalculate excel formulas
- create excel workbook c#
language: zh
og_description: 如何使用 C# 在 Excel 中使用 wrapcols 和 wrap rows。本指南展示了如何使用 C# 创建 Excel 工作簿并在几分钟内重新计算
  Excel 公式。
og_title: 如何在 C# 中使用 wrapcols – 完整的 Excel 列换行教程
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: how to use wrapcols and wrap rows excel in C#. Learn to create excel
    workbook c# and recalculate excel formulas with a step‑by‑step example.
  headline: how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate
    Formulas
  type: TechArticle
- description: how to use wrapcols and wrap rows excel in C#. Learn to create excel
    workbook c# and recalculate excel formulas with a step‑by‑step example.
  name: how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas
  steps:
  - name: Expected Result
    text: '| A | B | C | |---|---|---| | 1 | A | 2 | | 2 | B | 3 | | 3 | C | 4 | |
      4 | D | 5 | | 5 | E | 6 | | 6 | F | 7 | | 7 | G | 8 | | 8 | H | 9 | | 9 | I
      | |'
  - name: What if the source range is empty?
    text: Both `WRAPCOLS` and `WRAPROWS` will simply return an empty array, resulting
      in a blank cell. It’s safe to call the functions even when you’re not sure about
      data presence.
  - name: Can I wrap more than one range at a time?
    text: Yes—just place additional formulas in other cells. Each formula works independently,
      so you could have `WRAPCOLS` in D1, `WRAPROWS` in E1, etc.
  - name: How does this differ from a simple copy‑paste transpose?
    text: '`WRAPCOLS`/`WRAPROWS` handle *pagination* automatically. If you have 20
      items and ask for 3 columns, the function creates the necessary number of rows
      (7 in this case) without you calculating the dimensions manually.'
  - name: Does the library support dynamic array formulas (Excel 365)?
    text: Aspose.Cells fully supports dynamic array functions, including `WRAPCOLS`
      and `WRAPROWS`. The calculation engine will spill the results just like native
      Excel.
  - name: What about performance on large datasets?
    text: For millions of rows, consider batching the calculation (`workbook.CalculateFormula(FormulaCalculationOptions)`)
      or disabling automatic calculation while you insert formulas, then re‑enable
      it before saving.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: 如何在 C# 中使用 wrapcols – 包含 Excel WRAPROWS 与重新计算公式的完整指南
url: /zh/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 wrapcols – 包含 Excel WRAPROWS 与重新计算公式的完整指南

有没有想过 **如何使用 wrapcols** 来把一长列数据重新排列成整齐的网格？也许你尝试过手动复制‑粘贴的技巧，但那既慢又容易出错，实在让人头疼。好消息是，Excel 的 `WRAPCOLS`（以及它的兄弟函数 `WRAPROWS`）可以帮你完成繁重的工作——*而且*你可以在 C# 代码中调用它们。

在本教程中，我们将一步步演示如何在 C# 中创建 Excel 工作簿、应用 `WRAPCOLS` 和 `WRAPROWS`，以及最后 **重新计算 Excel 公式** 使包装后的数据即时显示。完成后，你将拥有一段可直接运行的代码片段，能够在任何 .NET 项目中使用。

## 你将学到

- 如何使用 Aspose.Cells 库 **在 C# 中创建 Excel 工作簿**（无需 COM 互操作）。  
- `WRAPCOLS` 函数的精确语法以及它与 `WRAPROWS` 的区别。  
- 为什么在插入函数后必须 **重新计算 Excel 公式**，以及如何高效地完成此操作。  
- 一个完整、可运行的示例，复制‑粘贴后即可在 `.xlsx` 文件中看到结果。  

**前置条件** – 需要 .NET 6+（或 .NET Framework 4.7+）、Visual Studio 2022 或任意你喜欢的 IDE，以及 Aspose.Cells for .NET NuGet 包。如果你是 Aspose.Cells 新手，也无需担心，步骤简明且解释充分。

---

## 第一步：设置项目并安装 Aspose.Cells

首先，创建一个新的控制台项目：

```bash
dotnet new console -n WrapDemo
cd WrapDemo
dotnet add package Aspose.Cells
```

> **小技巧：** 如果使用 Visual Studio，只需右键点击项目 → *管理 NuGet 包* → 搜索 **Aspose.Cells** 并安装。

该库为我们提供了后续教程中需要的 `Workbook`、`Worksheet` 和 `Cell` 类。

## 第二步：创建 Excel 工作簿并填充示例数据

接下来我们将创建工作簿，获取第一个工作表，并在 **A**、**B** 列填入示例数字。这些数据稍后会被包装成列和行。

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 2‑1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2‑2: Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate A2:A10 with numbers 1‑9
        for (int i = 2; i <= 10; i++)
        {
            worksheet.Cells[$"A{i}"].PutValue(i - 1);
        }

        // Populate B2:B10 with letters A‑I (just for variety)
        char letter = 'A';
        for (int i = 2; i <= 10; i++, letter++)
        {
            worksheet.Cells[$"B{i}"].PutValue(letter.ToString());
        }

        // The rest of the steps follow…
```

> **为什么重要：** 使用确定性的示例数据可以帮助你验证 `WRAPCOLS` 与 `WRAPROWS` 的实际效果是否符合预期。

## 第三步：应用 `WRAPCOLS` 函数 – **how to use wrapcols**

`WRAPCOLS` 接受一维范围并将其按指定列数展开，必要时自动添加新行。下面是我们将在单元格 **A1** 中插入的公式：

```csharp
        // Step 3: Insert WRAPCOLS formula – wrap A2:A10 into 3 columns per row
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A2:A10, 3)";
```

> **解释：** 第二个参数 (`3`) 告诉 Excel 每行创建三列。因此前三个值 (1, 2, 3) 位于 A1:C1，接下来的三个值 (4, 5, 6) 位于 A2:C2，剩余的值继续填入后面的行。

## 第四步：应用 `WRAPROWS` 函数 – wrap rows excel

`WRAPROWS` 则相反：它接受垂直范围并按指定的每列行数排列。我们将在 **B1** 中放置此公式：

```csharp
        // Step 4: Insert WRAPROWS formula – wrap B2:B10 into 2 rows per column
        worksheet.Cells["B1"].Formula = "=WRAPROWS(B2:B10, 2)";
```

> **解释：** 使用 `2` 行每列时，值 “A, B” 填入 B1:B2， “C, D” 填入 C1:C2，依此类推。函数会自动向水平扩展工作表。

## 第五步：重新计算所有公式 – **recalculate excel formulas**

当你以编程方式设置公式时，Excel 不会在工作簿打开前或你显式要求库进行计算之前计算结果。这时就需要 **重新计算 Excel 公式**：

```csharp
        // Step 5: Force calculation so the wrapped data appears immediately
        workbook.CalculateFormula();
```

> **为什么需要：** 若不调用 `CalculateFormula()`，打开文件时单元格会显示原始的 `=WRAPCOLS(...)` 文本，这就失去了本教程的意义。

## 第六步：保存工作簿并验证输出

最后，将工作簿写入磁盘。你可以在 Excel 中打开生成的文件，查看包装后的布局。

```csharp
        // Step 6: Save the workbook (adjust the path as needed)
        string outputPath = "output.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see wrapcols and wraprows in action.");
    }
}
```

### 预期结果

| A | B | C |
|---|---|---|
| 1 | A | 2 |
| 2 | B | 3 |
| 3 | C | 4 |
| 4 | D | 5 |
| 5 | E | 6 |
| 6 | F | 7 |
| 7 | G | 8 |
| 8 | H | 9 |
| 9 | I |   |

- **A‑C 列** 由 `WRAPCOLS` 调用填充（每行三列）。  
- **B‑I 行** 由 `WRAPROWS` 调用填充（每列两行）。  

打开 `output.xlsx`，即可看到上表所示的布局。如果数字未对齐，请再次检查公式字符串并确保已调用 `CalculateFormula()`。

---

## 常见问题与边缘情况

### 如果源范围为空会怎样？
`WRAPCOLS` 与 `WRAPROWS` 都会返回空数组，导致单元格保持空白。即使不确定是否有数据，也可以安全调用这些函数。

### 能一次包装多个范围吗？
可以——只需在其他单元格中放置额外的公式。每个公式独立工作，例如可以在 D1 放 `WRAPCOLS`，在 E1 放 `WRAPROWS`，依此类推。

### 与简单的复制‑粘贴转置有什么区别？
`WRAPCOLS`/`WRAPROWS` 会自动处理 *分页*。例如有 20 条数据并要求 3 列时，函数会自动生成所需的行数（本例为 7 行），无需手动计算尺寸。

### 库是否支持动态数组公式（Excel 365）？
Aspose.Cells 完全支持动态数组函数，包括 `WRAPCOLS` 与 `WRAPROWS`。计算引擎会像原生 Excel 一样溢出结果。

### 大数据集的性能如何？
对于数百万行的数据，建议批量计算 (`workbook.CalculateFormula(FormulaCalculationOptions)`) 或在插入公式时暂时关闭自动计算，保存前再重新启用。

---

## 完整源代码（可直接运行）

下面是完整程序——复制到 `Program.cs` 并按 **F5** 运行。

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate column A (A2:A10) with numbers 1‑9
        for (int i = 2; i <= 10; i++)
        {
            worksheet.Cells[$"A{i}"].PutValue(i - 1);
        }

        // Populate column B (B2:B10) with letters A‑I
        char letter = 'A';
        for (int i = 2; i <= 10; i++, letter++)
        {
            worksheet.Cells[$"B{i}"].PutValue(letter.ToString());
        }

        // Apply WRAPCOLS – wrap A2:A10 into 3 columns per row
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A2:A10, 3)";

        // Apply WRAPROWS – wrap B2:B10 into 2 rows per column
        worksheet.Cells["B1"].Formula = "=WRAPROWS(B2:B10, 2)";

        // Recalculate all formulas so the wrapped data appears
        workbook.CalculateFormula();

        // Save the workbook (adjust the folder if needed)
        string outputPath = "output.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the wrapped results.");
    }
}
```

---

## 结论

现在你已经掌握了 **如何使用 wrapcols**（以及对应的 `WRAPROWS`）在 C# 中对 Excel 工作表进行数据重排，并了解了 **重新计算 Excel 公式** 为必不可少的步骤。这一模式——*创建 Excel 工作簿 C# → 插入 WRAP 函数 → 重新计算*——为任何需要动态列或行布局的报表或数据展示任务提供了坚实基础。

接下来可以尝试：

- 不同的列/行计数 (`WRAPCOLS(..., 5)` 或 `WRAPROWS(..., 4)`)。  
- 将 `WRAPCOLS` 与其他动态数组函数（如 `FILTER`、`SORT`）组合使用。  
- 使用 `workbook.Save("report.pdf", SaveFormat.Pdf)` 将工作簿导出为 PDF。

随意修改示例、添加样式，或将其集成到更大的自动化流水线中。如遇到任何问题，欢迎在下方留言——祝编码愉快！

![Diagram showing how wrapcols and wraprows transform a single column into a grid – how to use wrapcols example](wrapcols-wraprows-diagram.png "how to use wrapcols example")

## 接下来该学习什么？

以下教程与本指南所示技术密切相关，帮助你进一步掌握 API 功能并探索在项目中的替代实现方式，每篇均附完整可运行的代码示例和逐步说明。

- [如何使用 Aspose.Cells for .NET 在 Excel 中对行和列进行分组](/cells/english/net/data-analysis/excel-grouping-aspose-cells-net/)
- [如何使用 Aspose.Cells .NET 隐藏 Excel 中的行和列：全面指南](/cells/english/net/range-management/aspose-cells-net-hide-rows-columns-excel/)
- [如何使用 Aspose.Cells .NET 创建和配置 Excel 工作簿：分步指南](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}