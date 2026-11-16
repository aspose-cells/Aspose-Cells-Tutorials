---
category: general
date: 2026-11-16
description: 学习如何使用 Aspose.Cells、动态数组函数和 lambda 归约器在 Excel 中展开数组，然后使用 C# 写入 Excel
  文件。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- create excel workbook
- how to use lambda
- dynamic array functions
- write excel file
language: zh
lastmod: 2026-11-16
og_description: 如何使用 Aspose.Cells、动态数组函数和 lambda 归约器在 Excel 中展开数组。请参阅完整的 C# 示例以写入
  Excel 文件。
og_image_alt: Diagram illustrating how to expand array in an Excel worksheet
og_title: 使用 Aspose.Cells 在 Excel 中展开数组 – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to expand array in Excel using Aspose.Cells, dynamic array
    functions, and a lambda reducer, then write the Excel file from C#.
  headline: How to expand array in Excel with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. `EXPAND` pads missing columns with blank cells. The same works for
      rows.
    question: Can I expand to more columns than the source provides?
  - answer: '`EXPAND` will treat the source as a single row; you can still specify
      rows and columns to reshape it.'
    question: What if the source array is horizontal (`{1,2,3,4,5}`)?
  - answer: The lambda must return a value compatible with the accumulator type. For
      text concatenation you could use `LAMBDA(acc, val, acc & val)`.
    question: Does `REDUCE` work with non‑numeric data?
  - answer: Only when you need the computed values before saving. Excel will recalculate
      on open if you skip it.
    question: Do I need to call `CalculateFormula` for every change?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: 如何使用 Aspose.Cells 在 Excel 中展开数组
url: /zh/net/calculation-engine/how-to-expand-array-in-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Excel 中使用 Aspose.Cells 扩展数组

如果您需要在 C# 中 **扩展数组** 到 Excel 工作表，本教程将展示完整步骤。您将创建一个 Excel 工作簿，使用 `EXPAND`、`REDUCE` 等动态数组函数，应用 **lambda** 累加器，最后 **写入 Excel 文件** 到磁盘。该方法适用于 Aspose.Cells 23.10 及以上版本，无需手动安装 Excel。

阅读完本指南后，您将拥有一个完整可用的 `ExpandReduceDemo.xlsx`，展示在编程环境中使用动态数组公式的强大功能。

## 您需要的环境

- .NET 6.0（或任何 Aspose.Cells 支持的 .NET 版本）
- Aspose.Cells for .NET 包（`dotnet add package Aspose.Cells`）
- 代码编辑器或 IDE（Visual Studio、VS Code、Rider 等）

无需额外的 COM 互操作或 Office 安装，因为 Aspose.Cells 在内部处理文件格式。

## 步骤 1：创建 Excel 工作簿

首要任务是 **创建 Excel 工作簿** 于内存中。Aspose.Cells 提供 `Workbook` 类，代表整个 XLSX 文件。

```csharp
using System;
using Aspose.Cells;

class ExpandReduceDemo
{
    static void Main()
    {
        // Step 1: instantiate a new workbook and get the default worksheet
        Workbook workbook = new Workbook();              // creates an empty .xlsx structure
        Worksheet sheet = workbook.Worksheets[0];        // the first (and only) sheet by default
```

> **为什么重要：** 实例化 `Workbook` 为您提供一块干净的画布。默认工作表已经准备好，除非您需要多个工作表，否则无需手动添加。

## 步骤 2：插入垂直数组常量

Excel 的动态数组引擎可以使用字面量数组常量。我们将在单元格 **A1** 中放入垂直数组 `{1;2;3;4;5}`。

```csharp
        // Step 2: put a vertical array constant into A1
        sheet.Cells["A1"].PutValue("{1;2;3;4;5}");
```

> **提示：** 分号（`;`）用于分隔常量中的行，而逗号（`,`）则用于分隔列。这与 Excel 本身的语法相同。

## 步骤 3：使用 EXPAND 将数组展开为矩阵

现在我们回答核心问题——**如何扩展数组**——使用 `EXPAND` 函数。该公式将单列数组展开为 5 行 × 2 列的矩阵，起始位置为 **B1**。

```csharp
        // Step 3: use EXPAND to create a 5‑row by 2‑column matrix
        sheet.Cells["B1"].Formula = "EXPAND(A1,5,2)";
```

> **为什么使用 EXPAND？** `EXPAND(source, rows, cols)` 强制源范围占据指定的大小，必要时用空白填充。它是从单个数组生成更大矩阵的最直观方式。

## 步骤 4：使用 lambda 累加器对矩阵进行 Reduce

`REDUCE` 函数遍历范围并使用 **lambda** 表达式聚合值。这里我们将每列的值求和到单列，并将结果放在 **D1**。

```csharp
        // Step 4: REDUCE the expanded matrix using a lambda accumulator
        sheet.Cells["D1"].Formula = "REDUCE(A1, B1:E5, LAMBDA(acc, val, acc+val))";
```

> **如何使用 lambda：** `LAMBDA(acc, val, acc+val)` 接收当前累加器 (`acc`) 和下一个单元格值 (`val`) ，返回新的累加器，实现运行总计。这演示了 **在 Excel 公式中使用 lambda** 的方法。

## 步骤 5：计算公式以显示结果

设置公式后，Aspose.Cells 不会自动求值。调用 `CalculateFormula` 可强制引擎计算工作簿中的所有公式。

```csharp
        // Step 5: recalculate all formulas so the results are materialized
        workbook.CalculateFormula();
```

> **注意：** 如果在 Excel 中打开生成的文件，数值已经可见，因为它们已被预先计算。

## 步骤 6：将 Excel 文件写入磁盘

最后，使用 `Save` 方法 **写入 Excel 文件**。请选择您拥有写入权限的文件夹。

```csharp
        // Step 6: save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\ExpandReduceDemo.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### 预期结果

| A | B | C | D |
|---|---|---|---|
| {1;2;3;4;5} | 1 |  | 15 |
|            | 2 |  |    |
|            | 3 |  |    |
|            | 4 |  |    |
|            | 5 |  |    |

- **列 B** 和 **列 C** 包含 `EXPAND` 生成的 5 × 2 矩阵。
- **单元格 D1** 显示 `15`，即所有数字的和，由 `REDUCE` + **lambda** 公式计算得到。

## 常见问题与边缘情况

- **可以将列数扩展到源数组未提供的数量吗？**  
  可以。`EXPAND` 会用空单元格填充缺失的列。行同理。

- **如果源数组是水平的 (`{1,2,3,4,5}`) 会怎样？**  
  `EXPAND` 会将其视为单行；您仍然可以指定行数和列数来重新塑形。

- **`REDUCE` 能处理非数值数据吗？**  
  lambda 必须返回与累加器类型兼容的值。对文本拼接可以使用 `LAMBDA(acc, val, acc & val)`。

- **是否需要对每次更改都调用 `CalculateFormula`？**  
  仅在需要在保存前获取计算结果时调用。若省略，Excel 打开时会重新计算。

## 专业技巧

- **性能优化：** 对于大型工作簿，建议在所有公式设置完毕后一次性调用 `workbook.CalculateFormula`，而不是在每个单元格后调用。
- **版本兼容性：** `EXPAND` 与 `REDUCE` 在 Excel 365 及更高版本可用。Aspose.Cells 无论目标 Excel 版本如何，都实现了这些函数，因为计算引擎是内置的。
- **调试公式：** 使用 `sheet.Cells["B1"].Formula` 读取您设置的完整公式字符串，有助于动态构建公式时的排错。

## 结论

现在您已经掌握了 **如何在 Excel 中使用 Aspose.Cells 扩展数组**，了解了 **动态数组函数** 的使用，能够通过 `REDUCE` 应用 **lambda**，并且能够 **从 C# 写入 Excel 文件**。此端到端示例可进一步扩展为更复杂的数据转换，如矩阵转置、累计总计或自定义聚合。

---

*后续步骤：*  
- 探索其他动态函数，如 `FILTER`、`SORT` 和 `UNIQUE`。  
- 将多个 `LAMBDA` 表达式组合，构建可复用的用户自定义函数。  
- 将工作簿生成集成到 ASP.NET Core API 中，实现即时报告创建。

## 接下来您应该学习什么？

以下教程与本指南紧密相关，进一步深化您所学的技术。每篇资源都提供完整的可运行代码示例和逐步解释，帮助您掌握更多 API 功能并探索在项目中的替代实现方案。

- [How to create Excel workbook C# with a dynamic array formula](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/)
- [How to expand array in Excel and populate a template](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)
- [How to Expand Array in C# with Aspose.Cells – Step‑by‑Step Guide](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}