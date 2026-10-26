---
category: general
date: 2026-10-26
description: 学习如何在 C# 中使用 WRAPCOLS 将范围拆分为列，使用 WRAPROWS 处理行，并以编程方式将工作簿保存为 XLSX。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split range into rows
- excel wrapcols example
- save workbook as xlsx
- create excel workbook programmatically
language: zh
lastmod: 2026-10-26
og_description: 如何在 C# 中使用 WRAPCOLS 将数据拆分为列，使用 WRAPROWS 拆分为行，并将工作簿保存为 XLSX。请按照完整的分步指南操作。
og_image_alt: Screenshot illustrating how to use WRAPCOLS to split a range into columns
  in Excel
og_title: 如何在 C# 中使用 WRAPCOLS – 拆分范围并保存为 XLSX
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  headline: How to use WRAPCOLS in C# and save workbook as XLSX
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  name: How to use WRAPCOLS in C# and save workbook as XLSX
  steps:
  - name: What the saved file looks like
    text: 'When you open `wrapcols_wraprows_output.xlsx` in Excel you’ll see:'
  - name: Changing the number of columns or rows
    text: '* **More columns:** Increase the second argument of `WRAPCOLS`. Example:
      `=WRAPCOLS(A1:A10,5)` creates five columns, leaving empty cells where data runs
      out. * **Dynamic column count:** Use a cell reference instead of a hard‑coded
      number. `=WRAPCOLS(A1:A10, G1)` where `G1` holds the desired column c'
  - name: Handling empty or non‑numeric cells
    text: WRAPCOLS and WRAPROWS ignore empty cells by default, but they preserve the
      order of non‑empty values. If you need to preserve blanks, wrap the source range
      with `IFERROR` or `TEXT` functions before applying WRAPCOLS.
  - name: Saving to other formats
    text: 'While this tutorial focuses on **save workbook as xlsx**, Aspose.Cells
      supports many formats (`.xls`, `.csv`, `.pdf`, etc.):'
  - name: What’s next?
    text: '* Explore **conditional formatting** to highlight the spilled data. * Combine
      **WRAPCOLS** with **SORT** or **FILTER** for dynamic dashboards. * Use Aspose.Cells’
      **charting API** to visualize the rearranged data directly from code.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: 如何在 C# 中使用 WRAPCOLS 并将工作簿保存为 XLSX
url: /zh/net/row-and-column-management/how-to-use-wrapcols-in-c-and-save-workbook-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 WRAPCOLS 并将工作簿保存为 XLSX

如果您需要 **如何使用 WRAPCOLS** 来重新组织 Excel 文件中的数据，本指南将为您展示一个完整、可运行的解决方案。您将看到 **excel wrapcols 示例**，学习如何使用 **WRAPROWS 将范围拆分为行**，并通过 **以 XLSX 格式保存工作簿** 完成整个 **编程** 流程。

在 C# 中操作 Excel 通常意味着创建工作簿、应用公式并持久化文件。下面的代码使用 Aspose.Cells 库，它允许您在无需安装 Microsoft Office 的情况下操作 Excel 文件。完成本教程后，您将能够 **以编程方式创建 excel 工作簿**，水平和垂直拆分数据，并生成一个干净的 `.xlsx` 文件，供后续处理使用。

## 前置条件

在开始之前，请确保您具备：

* .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.7+）
* 对 **Aspose.Cells** NuGet 包的引用  
  ```bash
  dotnet add package Aspose.Cells
  ```
* 对 C# 和 Excel 公式的基本了解

## 步骤 1：如何使用 WRAPCOLS 将范围拆分为列

**WRAPCOLS** 函数接受一维范围，并将其值按指定的列数展开。在本例中，我们从 `A1:A10` 开始，并让 WRAPCOLS 创建三列。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is the “create excel workbook programmatically” step
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Populate source data for demonstration
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 0].PutValue($"Item {i + 1}");
        }

        // Apply WRAPCOLS: split A1:A10 into 3 columns starting at C1
        // The formula is entered in cell C1 (row 0, column 2)
        ws.Cells[0, 2].Formula = "=WRAPCOLS(A1:A10,3)";

        // -------------------------------------------------
        // Why this works:
        // -------------------------------------------------
        // * WRAPCOLS reads the source range (A1:A10) vertically.
        // * The second argument (3) tells Excel to create three columns.
        // * The function returns a 2‑dimensional array that Excel spills into the
        //   surrounding cells automatically.
        // -------------------------------------------------
```

> **结果：** 单元格 `C1:E4` 现在包含原始的十个项目，按三列排列（最后一列放置剩余的项目）。

![演示如何使用 WRAPCOLS 将范围拆分为 Excel 中的列的截图](image-url.png)

## 步骤 2：使用 WRAPROWS 将范围拆分为行

**WRAPCOLS** 横向展开，而 **WRAPROWS** 则执行相反操作：它在指定的行数上展开范围。这里我们取 `B1:B10` 的值，并在 `F1` 开始的区域中排列成两行。

```csharp
        // Populate a second source column for WRAPROWS
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 1].PutValue($"Value {i + 1}");
        }

        // Apply WRAPROWS: split B1:B10 into 2 rows starting at F1
        ws.Cells[0, 5].Formula = "=WRAPROWS(B1:B10,2)";

        // -------------------------------------------------
        // Why WRAPROWS is useful:
        // -------------------------------------------------
        // * It converts a vertical list into a matrix with the specified row count.
        // * Handy when you need to prepare data for pivot tables, charts, or
        //   reporting layouts that expect a horizontal orientation.
        // -------------------------------------------------
```

> **结果：** 公式将十个值填充到 `F1:K2` 单元格中，分布在两行内。

## 步骤 3：以 XLSX 格式保存工作簿

在应用公式后，最后一步是将文件持久化。**以 xlsx 格式保存工作簿** 操作会将内存中的工作簿写入磁盘，采用现代的 OpenXML 格式。

```csharp
        // Save the workbook – this completes the “save workbook as xlsx” step
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "wrapcols_wraprows_output.xlsx");

        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### 保存后的文件效果

当您在 Excel 中打开 `wrapcols_wraprows_output.xlsx` 时，会看到：

| C | D | E |
|---|---|---|
| 项目 1 | 项目 4 | 项目 7 |
| 项目 2 | 项目 5 | 项目 8 |
| 项目 3 | 项目 6 | 项目 9 |
|        |        | 项目 10 |

以及

| F | G | H | I | J | K |
|---|---|---|---|---|---|
| 值 1 | 值 3 | 值 5 | 值 7 | 值 9 | |
| 值 2 | 值 4 | 值 6 | 值 8 | 值 10 | |

公式仍保留在单元格中，后续对源范围的更改会自动反映。

## 步骤 4：常见变体和边缘情况

### 更改列数或行数

* **更多列：** 增加 `WRAPCOLS` 的第二个参数。  
  示例：`=WRAPCOLS(A1:A10,5)` 会创建五列，数据不足的单元格保持为空。
* **动态列数：** 使用单元格引用代替硬编码数字。  
  `=WRAPCOLS(A1:A10, G1)`，其中 `G1` 保存所需的列数。

### 处理空单元格或非数值单元格

WRAPCOLS 和 WRAPROWS 默认会忽略空单元格，但会保留非空值的顺序。如果需要保留空白，请在应用 WRAPCOLS 前使用 `IFERROR` 或 `TEXT` 函数包装源范围。

### 保存为其他格式

虽然本教程侧重于 **以 xlsx 格式保存工作簿**，但 Aspose.Cells 支持多种格式（`.xls`、`.csv`、`.pdf` 等）：

```csharp
workbook.Save("output.pdf", SaveFormat.Pdf);   // Export to PDF
workbook.Save("output.csv", SaveFormat.Csv);   // Export to CSV
```

## 专业技巧与常见陷阱

* **技巧：** 如果计划在保存后立即评估公式，请设置 `Workbook.Settings.CalcEngineEnabled = true`。
* **注意：** 大范围源数据可能产生非常大的溢出区域，影响性能。请限制范围大小或将操作拆分到多个工作表中。
* **线程安全：** Aspose.Cells 对象 **不是** 线程安全的。如果在并行处理中多个文件，请为每个线程创建单独的 `Workbook` 实例。

## 结论

现在，您已经掌握了 **如何使用 WRAPCOLS** 将垂直范围拆分为多列，了解了 **如何使用 WRAPROWS 将范围拆分为行**，以及在完成这些转换后 **如何以 XLSX 格式保存工作簿**。按照上述步骤，您可以 **以编程方式创建 excel 工作簿**，应用强大的溢出公式，并生成可直接共享的 Excel 文件，无需手动操作。

### 接下来可以做什么？

* 探索 **条件格式**，为溢出数据添加高亮。
* 将 **WRAPCOLS** 与 **SORT** 或 **FILTER** 结合，实现动态仪表盘。
* 使用 Aspose.Cells 的 **图表 API**，直接在代码中可视化重新排列的数据。

祝编码愉快，尽情享受 Excel 工作流的自动化吧！


## 接下来应该学习什么？

以下教程涵盖了与本指南技术密切相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式。每个资源都提供完整的可运行代码示例和逐步解释。

- [如何在 C# 中使用 wrapcols – 完整指南，包含 Excel WRAPROWS 与重新计算公式](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [如何在 C# 中使用 WRAPCOLS – 将数组重塑为 Excel 中的矩阵](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)
- [如何使用 WRAPCOLS – C# Excel 自动化完整指南](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}