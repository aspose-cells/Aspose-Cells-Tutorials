---
category: general
date: 2026-03-25
description: 在 C# 中创建新工作簿，学习如何使用 EXPAND，计算余切，并使用逐步代码将工作簿保存到文件。
draft: false
keywords:
- create new workbook
- save workbook to file
- how to use expand
- how to calculate cotangent
- how to save excel
language: zh
og_description: 在 C# 中创建新工作簿，立即了解如何使用 EXPAND、计算余切并将工作簿保存到文件。
og_title: 在 C# 中创建新工作簿 – 完整编程指南
tags:
- Aspose.Cells
- C#
- Excel Automation
title: 在 C# 中创建新工作簿 – 完整编程指南
url: /zh/net/workbook-operations/create-new-workbook-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中创建新工作簿 – 完整编程指南

是否曾经需要在 C# 中**创建新工作簿**却不知从何入手？你并非唯一。无论是自动化报告流水线，还是仅在代码中玩转 Excel 公式，能够创建工作簿、插入诸如 `EXPAND` 或 `COT` 的公式，然后**将工作簿保存到文件**，都是任何 .NET 开发者的核心技能。

在本教程中，我们将演示一个真实案例：实例化一个全新的工作簿，使用 `EXPAND` 函数将静态数组转为动态列，使用 `COT` 函数计算余切，最后**将工作簿保存到文件**为 `.xlsx`。完成后，你将拥有可直接运行的代码片段，理解每一次调用的意义，并看到一些针对边缘情况的实用变体。

> **Pro tip:** 以下所有代码均适用于截至 2026 年 3 月的最新 Aspose.Cells for .NET 版本。如果你使用的是旧版，API 大体保持一致，但请再次确认命名空间引用。

## 您需要的环境

- .NET 6.0 或更高（示例针对 .NET 6，.NET 5 也可运行）  
- 通过 NuGet 安装 Aspose.Cells for .NET (`Install-Package Aspose.Cells`)  
- 具备一定的 C# 基础（你已经掌握）  

就这些——无需额外 DLL、无需 COM 互操作，机器上也不必安装 Excel。准备好了吗？让我们开始吧。

![Screenshot showing how to create new workbook in C#](assets/create-new-workbook.png){alt="展示如何在 C# 中创建新工作簿的截图"}

## 步骤 1：创建新工作簿

首先需要实例化 `Workbook` 类。可以把它想象成在内存中打开一个空的 Excel 文件。该对象包含工作表、样式以及后续可能需要的所有内容。

```csharp
using Aspose.Cells;

class ExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();               // <-- creates an empty .xlsx structure
        Worksheet ws = workbook.Worksheets[0];            // default sheet is named "Sheet1"
```

为什么要立即获取第一个工作表？大多数快速入门示例只使用单个工作表，而 `Worksheets[0]` 访问器是获取引用的最快方式，无需遍历。如果以后需要多个工作表，可以使用 `workbook.Worksheets.Add()` 添加。

## 步骤 2：如何使用 EXPAND 生成动态范围

`EXPAND` 是 Excel 中较新的函数，用于将数组填充到指定大小。在本例中，我们将文字数组 `{1,2,3}` 扩展为从单元格 `A1` 开始的**5 行列**。字符串内部的语法与在 Excel 中直接输入完全相同，后续可以直接复制粘贴到单元格中使用。

```csharp
        // Step 2: Apply EXPAND to turn {1,2,3} into a 5‑row vertical range
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"; // rows=5, cols=1
```

### 背后发生了什么？

- `{1,2,3}` 是水平数组文字。  
- 第二个参数 (`5`) 告诉 Excel 将数组扩展为 **5 行**。  
- 第三个参数 (`1`) 强制输出为 **单列**。  

如果省略第三个参数，Excel 会尝试保留原始形状，可能得到一个 5×3 的块而不是单列。这是初次使用 `EXPAND` 时常见的陷阱。

#### 您可能需要的变体

| 所需形状 | 公式示例 |
|---------------|-----------------|
| 3 行 2 列块 | `=EXPAND({1,2,3},3,2)` |
| 仅向下填充（同一列） | `=EXPAND({10,20},10,1)` |
| 扩展到更大的列数 | `=EXPAND({5},5,4)` |

随意替换文字或维度，以匹配你的数据生成逻辑。

## 步骤 3：如何使用 COT 函数计算余切

`COT` 函数返回以弧度表示的角度的余切。在本例中，我们计算 45°（π/4 弧度）的余切。结果 `1` 位于单元格 `B1`。

```csharp
        // Step 3: Use COT to calculate cotangent of 45 degrees (π/4 radians)
        ws.Cells["B1"].Formula = "=COT(PI()/4)"; // PI() returns π, divided by 4 = 45°
```

### 为什么使用 COT 而不是手动计算？

Excel 已内置三角函数转换，使用 `COT` 可避免手动计算 `1 / TAN(angle)` 时可能出现的浮点舍入误差。此外，公式对后续查看电子表格的人员更易读。

#### 边界情况：角度超出 0‑360°

如果提供的角度大于 `2*PI()`（或为负数），Excel 会自动进行取模，但结果可能出乎意料。为保险起见，建议先对角度进行归一化处理：

```csharp
        // Normalize angle to 0‑2π range before applying COT
        ws.Cells["C1"].Formula = "=COT(MOD(PI()*3, 2*PI()))";
```

该代码片段演示了如何将 `MOD` 与 `COT` 结合，实现更稳健的计算。

## 步骤 4：如何将工作簿保存为文件（Excel）

现在公式已经就位，最后一步是**将工作簿保存到文件**。可以自行选择任意路径——只需确保目录已存在且拥有写入权限。

```csharp
        // Step 4 (optional): Save the workbook so you can inspect the results
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "output.xlsx");

        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### 实际保存了什么？

打开 `output.xlsx` 时，你会看到：

| A | B |
|---|---|
| 1 | 1 |
| 2 |   |
| 3 |   |
|   |   |
|   |   |

- 列 **A** 包含展开后的数组 `{1,2,3}`，随后两个空单元格（因为我们要求 5 行）。  
- 单元格 **B1** 显示 `1`，即 45° 的余切。  

如果刷新工作簿（按 `F9` 或启用自动计算），Excel 将计算公式并显示结果。Aspose.Cells 还提供 `CalculateFormula` 方法，可在不打开 Excel 的情况下获取数值：

```csharp
        workbook.CalculateFormula();
        double cotResult = ws.Cells["B1"].DoubleValue; // should be 1.0
```

## 常见问题与注意事项

| 问题 | 答案 |
|----------|--------|
| **我需要手动启用计算吗？** | 不需要。默认情况下 Aspose.Cells 会原样保存公式；Excel 在打开时会计算它们。如需预先计算，请使用 `workbook.CalculateFormula()`。 |
| **我可以一次向多个单元格写入公式吗？** | 当然。使用 `ws.Cells["D1:D5"].Formula = "=RAND()"` 可以为一个范围填充随机数。 |
| **如果目标文件夹不存在怎么办？** | 首先创建它：`Directory.CreateDirectory(Path.GetDirectoryName(outputPath));` |
| **`EXPAND` 在旧版 Excel 中受支持吗？** | `EXPAND` 随 Excel 365/2019 引入。如果需要兼容旧文件，考虑使用 `INDEX`/`SEQUENCE` 组合。 |
| **如何隐藏公式视图？** | 设置 `ws.Cells["A1"].FormulaHidden = true;` 并保护工作表，以防用户看到底层公式。 |

## 总结

现在你已经掌握了在 C# 中**创建新工作簿**对象、利用 `EXPAND` 生成动态数组、使用 `COT` 计算余切，并将工作簿**保存为文件**为整洁的 Excel 文档。完整、可运行的示例已在上面的代码片段中提供——复制到控制台应用，按 `F5` 运行，然后打开生成的 `output.xlsx`，即可看到效果。

### 接下来做什么？

- **探索其他动态数组函数**，如 `SEQUENCE`、`FILTER`、`SORT`。  
- **使用 Aspose.Cells 丰富的图表 API**实现图表自动化。  
- **集成数据源**（SQL、CSV），并以编程方式将这些值写入公式。  
- **学习将 Excel 保存为 PDF**或其他格式——非常适合报告流水线。

随意实验：更改数组值、调整角度，或将结果写入不同的工作表。将 C# 与 Excel 现代公式引擎结合，天地无限。

祝编码愉快，愿你的电子表格始终正确计算！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}