---
category: general
date: 2026-11-19
description: 学习如何在 C# 中通过向单元格添加公式、使用 EXPAND 函数，并使用 Aspose.Cells 评估所有公式来计算余切。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to calculate cotangent
- how to use expand
- add formula to cell
- evaluate all formulas
- use expand function
language: zh
lastmod: 2026-11-19
og_description: 如何在 C# 中计算余切？本教程向您展示如何向单元格添加公式、使用 EXPAND 函数以及使用 Aspose.Cells 评估所有公式。
og_image_alt: C# code snippet adding Excel formulas with Aspose.Cells
og_title: 如何在 C# 中使用 EXPAND 计算余切 – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to calculate cotangent in C# by adding formulas to cells,
    using the EXPAND function, and evaluating all formulas with Aspose.Cells.
  headline: How to calculate cotangent in C# using the EXPAND function
  type: TechArticle
- description: Learn how to calculate cotangent in C# by adding formulas to cells,
    using the EXPAND function, and evaluating all formulas with Aspose.Cells.
  name: How to calculate cotangent in C# using the EXPAND function
  steps:
  - name: Creates a workbook and accesses the first worksheet.
    text: Creates a workbook and accesses the first worksheet.
  - name: Writes an `EXPAND` formula that turns a single value into a 5‑row array.
    text: Writes an `EXPAND` formula that turns a single value into a 5‑row array.
  - name: Writes a `COT` formula that **how to calculate cotangent** of π/4.
    text: Writes a `COT` formula that **how to calculate cotangent** of π/4.
  - name: Forces the engine to **evaluate all formulas** so the values are stored
      in the file.
    text: Forces the engine to **evaluate all formulas** so the values are stored
      in the file.
  - name: '**Validate source data** – check that cells referenced by `EXPAND` or `COT`
      contain numbers to avoid `#VALUE!` errors.'
    text: '**Validate source data** – check that cells referenced by `EXPAND` or `COT`
      contain numbers to avoid `#VALUE!` errors.'
  - name: '**Reuse the workbook object** – creating a single `Workbook` instance and
      reusing it for multiple operations reduces memory overhead.'
    text: '**Reuse the workbook object** – creating a single `Workbook` instance and
      reusing it for multiple operations reduces memory overhead.'
  - name: '**Save in the appropriate format** – `.xlsx` retains dynamic‑array formulas;
      `.xls` will downgrade them to static values.'
    text: '**Save in the appropriate format** – `.xlsx` retains dynamic‑array formulas;
      `.xls` will downgrade them to static values.'
  - name: '**Wrap calculations in try/catch** – formula parsing can throw `CellsException`
      if the syntax is invalid.'
    text: '**Wrap calculations in try/catch** – formula parsing can throw `CellsException`
      if the syntax is invalid.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- formulas
title: 如何使用 EXPAND 函数在 C# 中计算余切
url: /zh/net/formulas-functions/how-to-calculate-cotangent-in-c-using-the-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 EXPAND 函数计算余切

如果你需要在 C# 中 **计算余切** 并将结果写入 .xlsx 文件，本指南提供了完整、可直接运行的解决方案。你将看到如何 **向单元格添加公式**，利用 **EXPAND** 函数生成动态数组，最后 **评估所有公式**，使工作簿中保存计算后的结果。

以编程方式操作 Excel 往往需要处理单元格引用、数组公式和自定义函数。完成本教程后，你将拥有一个完整的 C# 程序，能够：

1. 创建工作簿并访问第一个工作表。  
2. 写入一个 `EXPAND` 公式，将单个数值转换为 5 行数组。  
3. 写入一个 `COT` 公式，**计算 π/4 的余切**。  
4. 强制引擎 **评估所有公式**，使数值存储在文件中。  

该方法适用于最新的 Aspose.Cells for .NET（撰写时为 v23.12），仅需 NuGet 包 `Aspose.Cells`，无需外部 Excel 安装。

## 前置条件

- .NET 6.0 SDK 或更高版本（代码同样可以在 .NET Framework 4.7.2 上编译）。  
- Visual Studio 2022 或任何支持 C# 的 IDE。  
- NuGet 包 **Aspose.Cells**（`Install-Package Aspose.Cells`）。  

> **专业提示：** 如果你使用 CI/CD 流水线，请在项目文件中添加包引用，而不是全局安装。这可以保证构建的可复现性。

## 第一步：创建工作簿并访问第一个工作表

工作簿对象是所有电子表格操作的入口。将其创建在内存中可以避免任何文件系统副作用，直到你显式保存为止。

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1 – instantiate a new workbook and get the first worksheet
        Workbook wb = new Workbook();               // empty workbook with one sheet
        Worksheet ws = wb.Worksheets[0];            // reference to Sheet1
```

**为什么重要：**  
Aspose.Cells 会自动创建默认工作表（`Sheet1`）。通过 `Worksheets[0]` 访问它，可确保你写入的是已知位置，从而避免后续出现 “找不到工作表” 的错误。

## 第二步：添加一个 EXPAND 将读取的简单数值

`EXPAND` 函数需要一个源单元格。这里我们在 **B1** 中放置一个数值，随后将其展开为垂直数组。

```csharp
        // Step 2 – write a source value in B1
        ws.Cells["B1"].PutValue(42);   // any numeric value works
```

**边缘情况：** 如果 `B1` 为空，`EXPAND` 会返回 `#VALUE!` 错误。请始终确保源单元格包含有效数字或能够解析为数字的公式。

## 第三步：使用 EXPAND 函数生成 5 行数组

现在我们向 **A1** 写入公式，将 **B1** 的值展开为 5 行 1 列的范围。这演示了 **如何使用 expand**，并涉及 **使用 expand 函数** 的基本用法。

```csharp
        // Step 3 – write the EXPAND formula in A1
        // =EXPAND(B1,5,1) creates a vertical array of 5 rows based on B1
        ws.Cells["A1"].Formula = "=EXPAND(B1,5,1)";
```

**为什么使用 EXPAND？**  
`EXPAND` 是 Excel 365 中引入的动态数组函数。它消除了传统 `Ctrl+Shift+Enter` 数组公式的需求，并自动将结果溢出到相邻单元格。在本例中，结果将占据 **A1:A5**，每个单元格显示数值 `42`。

## 第四步：写入 **计算余切** 的公式

角度 θ 的余切为 `1 / tan(θ)`。Excel 提供内置的 `COT` 函数，我们可以直接计算 `cot(π/4)`，结果应为 `1`。

```csharp
        // Step 4 – calculate cotangent of π/4 in A2
        ws.Cells["A2"].Formula = "=COT(PI()/4)";
```

**解释：**  
- `PI()` 返回数学常数 π。  
- `PI()/4` 计算得到 π/4（45 度）。  
- `COT` 返回该角度的余切，即 `1`。  

如果你需要计算存放在单元格中的可变角度（例如 `B2`），只需将字面量替换为引用：`=COT(B2)`。

## 第五步：强制工作簿 **评估所有公式**

默认情况下，Aspose.Cells 会将公式写入文件但不计算其结果。若要存储计算后的数值，请调用 `CalculateFormula()`。

```csharp
        // Step 5 – evaluate every formula in the workbook
        wb.CalculateFormula();
```

**内部发生了什么？**  
Aspose.Cells 会解析每个公式，构建执行树，并使用自身的计算引擎求值。这与 Excel 的行为相同，确保保存的文件包含结果而非仅仅是公式。

## 第六步：保存工作簿并验证输出

最后，将工作簿持久化到磁盘，并可选择将计算结果打印到控制台，以便快速验证。

```csharp
        // Step 6 – save the workbook
        string outPath = "CotangentAndExpandDemo.xlsx";
        wb.Save(outPath);

        // Optional: display calculated values in the console
        Console.WriteLine("A1–A5 (EXPAND result):");
        for (int row = 0; row < 5; row++)
        {
            Console.WriteLine($"A{row + 1} = {ws.Cells[row, 0].StringValue}");
        }
        Console.WriteLine($"A2 (COT result) = {ws.Cells["A2"].StringValue}");
        Console.WriteLine($"Workbook saved to {outPath}");
    }
}
```

### 预期输出

运行程序后，控制台会显示：

```
A1–A5 (EXPAND result):
A1 = 42
A2 = 42
A3 = 42
A4 = 42
A5 = 42
A2 (COT result) = 1
Workbook saved to CotangentAndExpandDemo.xlsx
```

在 Excel 中打开 *CotangentAndExpandDemo.xlsx* 可确认：

- **A1:A5** 单元格包含 `42`（展开的数组）。  
- **A2** 单元格显示 `1`（π/4 的余切）。  

所有公式均已被 `wb.CalculateFormula()` 替换为其计算值。

## 常见问题与故障排除

| Question | Answer |
|----------|--------|
| **需要水平数组怎么办？** | 使用 `=EXPAND(B1,1,5)` —— 第二个参数（`rows`）设为 1，第三个参数（`columns`）设为 5，结果会溢出到 **A1:E1**。 |
| **可以展开一个范围而不是单个单元格吗？** | 可以。`=EXPAND(B1:B3,5,1)` 会将三行源数据重复填充至 5 行结果，必要时会截断或填充。 |
| **为什么 `COT` 对某些角度返回 `#DIV/0!`？** | `COT(θ) = 1 / tan(θ)`。如果 `tan(θ)` 为零（例如 θ = 0、π、2π），结果未定义，导致除零错误。 |
| **需要启用任何计算选项吗？** | 不需要。调用 `CalculateFormula()` 时，Aspose.Cells 会自动启用完整计算模式。 |
| **旧版 Excel 是否支持 EXPAND 函数？** | `EXPAND` 需要 Excel 365 或更高版本。若需兼容旧版，可使用传统数组公式或通过代码手动填充单元格。 |

## 使用 Aspose.Cells 处理公式的最佳实践

1. **验证源数据** —— 检查 `EXPAND` 或 `COT` 引用的单元格是否包含数字，以避免 `#VALUE!` 错误。  
2. **复用 Workbook 对象** —— 创建单个 `Workbook` 实例并在多次操作中复用，可降低内存开销。  
3. **选择合适的保存格式** —— `.xlsx` 能保留动态数组公式；`.xls` 会将其降级为静态值。  
4. **在 try/catch 中包装计算** —— 公式解析若语法无效会抛出 `CellsException`，请做好异常处理。  

## 结论

现在，你已经掌握了在 C# 中 **计算余切** 的完整流程：**向单元格添加公式**、使用 **EXPAND** 生成动态数组、并通过 Aspose.Cells **评估所有公式**。完整示例展示了从工作簿创建到结果验证的清晰工作流，可直接集成到更大的报表或数据处理管道中。

接下来可以进一步探索：

- **使用 expand** 处理多列数组，实现矩阵式数据。  
- 根据用户输入或配置文件 **动态向单元格添加公式**。  
- 在多工作表工作簿中 **评估所有公式**，并使用自定义计算设置（例如迭代计算）。  

欢迎尝试其他数学函数（`SIN`、`COS`、`TAN`、`COT`），并将它们与 `EXPAND` 结合，构建强大的基于电子表格的计算器。祝编码愉快！


## 接下来该学习什么？

以下教程与本指南紧密相关，帮助你进一步掌握相关技术。每篇资源都包含完整的可运行代码示例和逐步说明，帮助你在项目中灵活运用更多 API 功能或探索替代实现方案。

- [How to Calculate Cotangent in Excel with C# – Step‑by‑Step Guide](/cells/english/net/excel-formulas-and-calculation-options/how-to-calculate-cotangent-in-excel-with-c-step-by-step-guid/)
- [How to Evaluate Formulas in C# – Complete Aspose.Cells Guide](/cells/english/net/calculation-engine/how-to-evaluate-formulas-in-c-complete-aspose-cells-guide/)
- [How to Expand Array in C# with Aspose.Cells – Step‑by‑Step Guide](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}