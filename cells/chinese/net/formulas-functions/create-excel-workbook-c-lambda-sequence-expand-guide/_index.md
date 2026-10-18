---
category: general
date: 2026-03-30
description: 使用 Aspose.Cells 在 C# 中创建 Excel 工作簿。学习在 Excel 中使用 lambda 函数、sequence 函数、expand
  array 函数，并将工作簿保存为 xlsx。
draft: false
keywords:
- create excel workbook c#
- lambda function excel
- save workbook as xlsx
- sequence function excel
- expand array excel
language: zh
og_description: 快速使用 C# 创建 Excel 工作簿。本指南展示如何使用 Excel 的 lambda 函数、sequence 函数、expand
  array 函数，并将工作簿保存为 xlsx。
og_title: 使用 C# 创建 Excel 工作簿 – Lambda、SEQUENCE 与 EXPAND 指南
tags:
- Aspose.Cells
- C#
- Excel automation
title: 使用 C# 创建 Excel 工作簿 – Lambda、SEQUENCE 与 EXPAND 指南
url: /zh/net/formulas-functions/create-excel-workbook-c-lambda-sequence-expand-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建 Excel 工作簿 C# – Lambda、SEQUENCE 与 EXPAND 指南

是否曾经需要 **创建 Excel 工作簿 C#** 来生成自动化报告，却不确定该使用哪些 API 调用？你并不孤单——许多开发者在首次接触编程生成 Excel 时都会遇到同样的难题。在本指南中，你将看到一个完整、可运行的示例，涵盖从全新的 **SEQUENCE 函数 Excel** 到强大的 **LAMBDA 函数 Excel**，甚至还有如何 **展开数组 Excel** 结果的全部内容。

我们还会演示 **将工作簿保存为 xlsx** 的精确步骤，这样你就可以把文件交给任何使用 Excel 的人。阅读完本教程后，你将拥有一段坚固、可直接投入生产的代码片段，能够在任何 .NET 项目中使用。没有模糊的 “参考文档” 链接——只有今天就能运行的代码。

## 你需要准备的内容

- **.NET 6.0 或更高** – 示例针对 .NET 6，但任何近期版本均可。  
- **Aspose.Cells for .NET** – 通过 NuGet 安装 (`Install-Package Aspose.Cells`)。  
- 对 C# 语法有基本了解（变量、对象和 lambda 表达式）。  
- 你熟悉的 IDE（Visual Studio、Rider 或 VS Code）。  

就这些。无需额外的 COM 互操作，也不需要在服务器上安装 Office——Aspose.Cells 在内存中处理一切。

## 创建 Excel 工作簿 C# – 步骤实现

下面我们将过程拆分为若干小步骤。每一步都有明确的标题、简短的代码摘录以及 **为什么** 要这么做的解释。你可以直接复制最后的完整代码块并作为控制台应用运行。

### 步骤 1 – 初始化新工作簿

首先：我们需要一个空的工作簿对象，它代表内存中的 Excel 文件。

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // empty workbook
Worksheet sheet = workbook.Worksheets[0];         // default first sheet
```

*为什么重要：* `Workbook` 是所有 Aspose.Cells 操作的入口。通过获取第一个 `Worksheet`，我们得到一个可以写入公式、数值或格式的画布。  

> **小技巧：** 如果需要多个工作表，只需调用 `workbook.Worksheets.Add()` 并保持对每个工作表的引用。

### 步骤 2 – 使用 SEQUENCE 函数 Excel 生成数据

**sequence function excel** 可以在不使用 VBA 的情况下创建动态数字数组。我们将在单元格 `A1` 中放置它，并让 Excel 自动展开。

```csharp
// Step 2: Generate a 5‑row, 1‑column array from a SEQUENCE
sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)"; // 1..3 padded with blanks
```

*为什么重要：* `SEQUENCE(3)` 会产生 `[1,2,3]`。将其与 `EXPAND` 包裹后，会强制结果扩展为 5 行范围，额外的行会填充为空白。这一次性演示了 **sequence function excel** 和 **expand array excel**。

### 步骤 3 – 使用 LAMBDA 函数 Excel 聚合数字

现在展示 **lambda function excel** 的能力。我们将使用全新的 `REDUCE` 函数对 1‑5 的数字求和，`REDUCE` 在内部依赖 lambda 表达式。

```csharp
// Step 3: Aggregate a sequence (sum 1..5) using REDUCE/LAMBDA
sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))"; // result = 15
```

*为什么重要：* `REDUCE` 会遍历 `SEQUENCE(5)` 产生的数组，将每个元素 (`b`) 与累加器 (`a`) 传入 lambda，lambda `a+b` 将它们相加，最终在 `B1` 中得到 `15`。这是一种纯公式、无需在 C# 中循环的简洁归约方式。

### 步骤 4 – 在单元格中直接使用三角函数

Excel 内置的数学函数非常适合快速计算。我们将在相邻的单元格中放置余切和双曲余切。

```csharp
// Step 4: Trigonometric functions directly in Excel cells
sheet["C1"].Formula = "COT(PI()/4)";   // evaluates to 1
sheet["D1"].Formula = "COTH(1)";      // hyperbolic cotangent of 1
```

*为什么重要：* 演示了可以将经典数学函数与新式动态数组公式混合使用。除非有特定的性能需求，否则无需在 C# 中预先计算这些值。

### 步骤 5 – 计算所有公式

当你设置公式后，Aspose.Cells 并不会自动求值。必须显式调用计算。

```csharp
// Step 5: Force calculation so that cells store the results
workbook.CalculateFormula();
```

*为什么重要：* 调用此方法后，每个单元格的 `Value` 属性将包含已求值的结果，准备好保存或再次读取。

### 步骤 6 – 将工作簿保存为 Xlsx

最后，使用 **save workbook as xlsx** 的模式将工作簿持久化到磁盘。

```csharp
// Step 6: Save the workbook to an Excel file (XLSX format)
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "NewFunctions.xlsx");

workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

*为什么重要：* `Save` 方法会自动识别文件扩展名。使用 “.xlsx” 可确保文件兼容现代 Excel 版本。路径指向桌面，便于在测试期间快速访问。

### 完整可运行示例

下面是可以粘贴到新控制台项目中的完整程序。它包含上述所有步骤，并附带一个小的验证块，将计算结果打印到控制台。

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Initialize workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // SEQUENCE + EXPAND
        sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)";

        // REDUCE with LAMBDA
        sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))";

        // Trig functions
        sheet["C1"].Formula = "COT(PI()/4)";
        sheet["D1"].Formula = "COTH(1)";

        // Calculate formulas
        workbook.CalculateFormula();

        // Verify results (optional)
        Console.WriteLine("A1‑A5 (expanded SEQUENCE):");
        for (int i = 0; i < 5; i++)
        {
            Console.WriteLine($"  Row {i + 1}: {sheet.Cells[i, 0].Value ?? "blank"}");
        }
        Console.WriteLine($"B1 (sum 1‑5): {sheet["B1"].Value}");
        Console.WriteLine($"C1 (cot(π/4)): {sheet["C1"].Value}");
        Console.WriteLine($"D1 (coth(1)): {sheet["D1"].Value}");

        // Save workbook
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "NewFunctions.xlsx");
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

**控制台预期输出**

```
A1‑A5 (expanded SEQUENCE):
  Row 1: 1
  Row 2: 2
  Row 3: 3
  Row 4: blank
  Row 5: blank
B1 (sum 1‑5): 15
C1 (cot(π/4)): 1
D1 (coth(1)): 1.31303528549933
Workbook saved to: C:\Users\YourName\Desktop\NewFunctions.xlsx
```

打开 *NewFunctions.xlsx* 时，你会看到相同的数字排列在前四列。

![创建 Excel 工作簿 c# 的结果电子表格截图](/images/create-excel-workbook-csharp.png)

## 边缘情况、技巧与常见问题

- **如果需要多个工作表怎么办？**  
  只需调用 `workbook.Worksheets.Add()`，并在每个新 `Worksheet` 对象上重复公式赋值。  

- **能兼容旧版 Excel 吗？**  
  动态数组函数（`SEQUENCE`、`EXPAND`、`REDUCE`）需要 Excel 365 或 Excel 2021 及以上版本。如果目标是旧版，请使用传统公式或在 C# 中先计算好数值再写入。  

- **性能方面的顾虑？**  
  对于成千上万行的数据，在一个范围内设置公式后再调用 `CalculateFormula`，通常比逐个循环赋值更快。  

- **想将文件保存到流而不是磁盘？**  
  `work

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}