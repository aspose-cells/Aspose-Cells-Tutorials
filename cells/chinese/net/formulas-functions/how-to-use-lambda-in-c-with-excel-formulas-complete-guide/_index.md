---
category: general
date: 2026-03-22
description: 如何在 C# 中使用 lambda 处理 Excel 公式。学习将公式写入单元格、将范围转换为数组、在控制台显示数组，以及在 Excel
  中计算余切。
draft: false
keywords:
- how to use lambda
- display array in console
- convert range to array
- write formula to cell
- calculate cotangent in excel
language: zh
og_description: 如何在 C# 中使用 lambda 操作 Excel 公式，将范围转换为数组，将公式写入单元格，在控制台显示数组，以及在 Excel
  中计算余切。
og_title: 如何在 C# 中使用 Lambda 与 Excel 公式 – 步骤指南
tags:
- C#
- Aspose.Cells
- Excel Automation
- Lambda Expressions
title: 在 C# 中使用 Lambda 与 Excel 公式的完整指南
url: /zh/net/formulas-functions/how-to-use-lambda-in-c-with-excel-formulas-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Lambda 与 Excel 公式 – 完整指南

是否曾经好奇 **如何使用 lambda** 在 C# 中自动化 Excel？你并不孤单。许多开发者在需要将 Excel 新的动态数组函数与 C# 的 `LAMBDA` 功能结合时会卡住。好消息是？只要看到各部分如何配合，这其实相当简单。

在本教程中，我们将演示 **向单元格写入公式**、**将范围转换为数组**、**在控制台显示该数组**，甚至 **在 Excel 中计算余切**——全部展示 **如何在 `REDUCE` 调用中使用 lambda**。完成后，你将拥有一段可直接放入任何引用 Aspose.Cells（或类似库）的 .NET 项目的可运行代码片段。

---

## 你将学到

- 如何使用 C# **向单元格写入公式**。
- 如何使用 `EXPAND` 函数 **将范围转换为数组**。
- 如何在计算后 **在控制台显示数组**。
- 如何使用 `COT` 与 `COTH` **在 Excel 中计算余切**。
- 从 C# 调用 Excel 的 `REDUCE` 函数时 **如何使用 lambda** 的完整语法。

> **先决条件：** 需要 .NET（Core 6+ 或 .NET Framework 4.7+）的最新版本，并通过 NuGet 安装 Aspose.Cells for .NET 库。

---

## 步骤 1：设置工作簿并向单元格写入公式

首先我们创建一个全新的工作簿并获取第一个工作表。随后 **向单元格写入公式** —— 在本例中，`A1` 将保存一次 `EXPAND` 调用的结果。

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write formula to A1 – we’ll expand B1:C2 into a 4‑by‑5 array later
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";
```

**为什么重要：** 直接从代码写入公式意味着可以在不打开 Excel 的情况下动态生成复杂的电子表格。这也为下一步 **将范围转换为数组** 做好准备。

---

## 步骤 2：使用 EXPAND 将范围转换为数组

`EXPAND` 是 Excel 用来将小范围扩展为更大矩阵的方式。把公式放在 `A1` 后，Excel 会在该单元格起始处溢出一个 4 × 5 的块。从 C# 端，我们无需手动复制数值——当调用 `Calculate` 时，库会完成繁重的工作。

```csharp
        // The EXPAND formula will spill into A1:E4 (4 rows × 5 columns)
        // No extra code needed – the workbook will handle the spill.
```

**如何使用 lambda：** 目前还没有，但请继续关注。先获取工作表中的数据，然后再用 lambda 进行归约。

---

## 步骤 3：在 REDUCE 中使用 LAMBDA —— “如何使用 Lambda”的核心

Excel 365 引入了 `REDUCE`，它接受 **初始值**、**范围** 和一个 **LAMBDA**，用于定义如何合并每个元素。从 C# 只需把公式字符串赋给单元格；lambda 本身位于 Excel 公式内部，而不是 C# 代码中。

```csharp
        // Reduce the spilled array by summing all its values.
        // This demonstrates how to use lambda inside REDUCE.
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";
```

**解释：**  
- `0` 是起始累加器（`acc`）。  
- `A1:D4` 是我们要处理的范围（溢出块的前四列）。  
- `LAMBDA(acc, x, acc + x)` 告诉 Excel 将每个单元格 (`x`) 加到累加器上。

这就是在电子表格环境中 **如何使用 lambda** 进行聚合的核心思路。

---

## 步骤 4：在 Excel 中计算余切 —— 从角度到双曲

如果需要三角函数结果，Excel 的 `COT` 与 `COTH` 函数非常便利。我们将在 `G1` 与 `G2` 中分别放置它们。

```csharp
        // Demonstrate trigonometric functions – cotangent and hyperbolic cotangent
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected result: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";      // Hyperbolic cotangent of 1
```

**为什么好用：** 掌握 **在 Excel 中计算余切** 能让你省去编写自定义数学代码的麻烦，尤其是当工作簿需要与非开发人员共享时。

---

## 步骤 5：强制计算并获取展开的数组

现在让工作簿评估所有公式，然后从 `A1` 中提取溢出的数组。这一步就是 **在控制台显示数组** 的时刻。

```csharp
        // Force calculation of all formulas
        workbook.Calculate();

        // Retrieve the spilled array from A1 as a 2‑D object
        var expanded = worksheet.Cells["A1"].Value;

        // Pretty‑print the 2‑D array to the console
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show the result of the REDUCE lambda
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**你将看到：**  
- 逐行打印的整齐 4 × 5 矩阵。  
- 由 `REDUCE` lambda 计算得到的总和。  
- 两个余切值。

至此，已完整演示了从 **向单元格写入公式** 到 **在控制台显示数组** 的整个流程。

---

## 完整可运行示例（复制粘贴即用）

下面是可以直接放入控制台应用的完整程序。记得先添加 `Aspose.Cells` NuGet 包（`dotnet add package Aspose.Cells`）。

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Write EXPAND formula (convert range to array)
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";

        // Step 3: Use REDUCE with LAMBDA (how to use lambda)
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";

        // Step 4: Calculate cotangent values (calculate cotangent in excel)
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";

        // Step 5: Force calculation
        workbook.Calculate();

        // Step 6: Retrieve and display the expanded array (display array in console)
        var expanded = worksheet.Cells["A1"].Value;
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show REDUCE result
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**预期的控制台输出（数值会根据 B1:C2 的默认内容而变化，默认均为 0）：**

```
Expanded array from A1 (4×5):
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0

Sum of A1:D4 (via REDUCE lambda): 0
Cotangent of π/4: 1
Hyperbolic cotangent of 1: 1.31303528549933
```

在运行前随意在 `B1:C2` 中填入自己的数字——矩阵会相应反映这些值。

---

## 专业技巧与常见坑点

- **技巧：** 如果需要让溢出范围从其他位置开始，只需更改目标单元格（`A1`）。`EXPAND` 会遵循新的锚点。
- **注意：** 源范围中的空单元格在溢出数组中会变成 `0`，这可能影响 `REDUCE` 的求和结果。
- **边缘情况：** 当工作簿包含依赖易变函数（如 `NOW()`）的公式时，设置完所有公式后调用 `workbook.Calculate()`，以确保数据是最新的。
- **性能提示：** 对于巨大的溢出范围，建议在 `EXPAND` 调用中限制大小；否则可能会分配过多内存。
- **兼容性：** The `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}