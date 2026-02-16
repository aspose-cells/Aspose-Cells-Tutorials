---
category: general
date: 2026-02-15
description: 创建新的 Excel 工作簿，学习如何使用 EXPAND、展开序列以及计算余切。同时了解如何将工作簿保存为文件。
draft: false
keywords:
- create new excel workbook
- save workbook to file
- how to use expand
- how to expand sequence
- how to calculate cotangent
language: zh
og_description: 使用 C# 创建新的 Excel 工作簿。学习如何使用 EXPAND、展开序列、计算余切，并将工作簿保存到文件。
og_title: 在 C# 中创建新的 Excel 工作簿 – 完整编程指南
tags:
- C#
- Aspose.Cells
- Excel automation
title: 在 C# 中创建新的 Excel 工作簿 – 步骤指南
url: /zh/net/excel-workbook/create-new-excel-workbook-in-c-step-by-step-guide/
---

Now produce final content with all translations.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中创建新的 Excel 工作簿 – 完整编程指南

是否曾经需要从代码 **create new Excel workbook**，但不知从何入手？你并不孤单；许多开发者在自动化报告或构建数据管道时都会遇到这个难题。在本教程中，我们将准确演示如何 create new Excel workbook，编写几个酷炫的公式，然后 **save workbook to file** 以便后续检查。  

我们还将深入探讨 `EXPAND` 函数的细节，演示 **how to use expand** 如何将一个小序列扩展为大块，解释 **how to expand sequence** 的实际用法，最后揭示 **how to calculate cotangent** 在 Excel 中的直接计算方法。完成后，你将拥有一个可运行的 C# 程序，可直接放入任何 .NET 项目中。

## 你需要的条件

- **Aspose.Cells for .NET**（免费试用或授权版本）– 该库让我们在未安装 Office 的情况下操作 Excel。  
- **.NET 6+**（或 .NET Framework 4.6+）。  
- 一个普通的 IDE，例如 Visual Studio 2022、VS Code 或 Rider。  

除了 `Aspose.Cells` 外无需其他 NuGet 包。如果尚未安装，请运行：

```bash
dotnet add package Aspose.Cells
```

就这样——无需其他设置。

## 步骤 1：创建新的 Excel 工作簿

我们首先要实例化一个 `Workbook` 对象。可以把它看作所有工作表、单元格和公式所在的空白画布。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];    // default sheet is named "Sheet1"
```

> **为什么重要：** 在内存中创建工作簿意味着在我们明确决定 **save workbook to file** 之前，根本不会触及磁盘。这使操作更快，并且可以在不产生 I/O 开销的情况下链式进行后续修改。

## 步骤 2：如何使用 EXPAND 扩展序列

`EXPAND` 是一个较新的 Excel 函数，用于将较小的数组拉伸到指定大小。在本例中，我们从一个三行的垂直序列开始，将其转换为 5 × 5 的块。

```csharp
        // Step 2: Write a formula that expands a 3‑row sequence into a 5×5 block
        // The formula lives in A1 and will spill over to E5
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3),5,5)";
```

> **解释：** `SEQUENCE(3)` 生成 `{1;2;3}`（垂直数组）。`EXPAND(...,5,5)` 告诉 Excel 将该数组重复，直至填满从 A1 开始的 5 行 5 列矩形。结果是一个矩阵，每列重复原始的三个数字，最后两行为空，因为源数组只有三行。

### 预期输出

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 1 | 1 | 1 | 1 |
| 2 | 2 | 2 | 2 | 2 |
| 3 | 3 | 3 | 3 | 3 |
|   |   |   |   |   |
|   |   |   |   |   |

在 Excel 中打开工作簿后，你会看到相同的模式填满整个范围。

## 步骤 3：如何在 Excel 中计算余切

大多数人熟悉 `SIN`、`COS` 和 `TAN`，但 `COT` 是求正切倒数的便捷函数。下面演示如何使用弧度计算 45°（等于 1）的余切。

```csharp
        // Step 3: Write a formula that returns the cotangent of 45° (π/4 radians)
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

> **为什么使用 COT？** 直接调用 `COT` 可以避免使用 `1/TAN(...)` 所需的额外除法，使公式更清晰，并在大型工作表中略微提升速度。

## 步骤 4：评估所有公式

除非显式指示，Aspose.Cells 不会自动计算公式。`CalculateFormula` 方法强制进行完整评估，使得计算结果存入单元格。

```csharp
        // Step 4: Evaluate all formulas so the results are stored in the cells
        workbook.CalculateFormula();
```

> **提示：** 如果有大量耗时的公式，可以传入 `CalculationOptions` 对象来微调性能（例如，启用多线程）。

## 步骤 5：保存工作簿到文件

现在所有内容都已准备就绪，我们终于 **save workbook to file**。选择一个你有写入权限的文件夹，并为文件起一个有意义的名称。

```csharp
        // Step 5: Save the workbook to a file for inspection
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath);
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

> **磁盘上会发生什么？** `Save` 调用会写入一个完整的 `.xlsx` 包，其中包含来自 `EXPAND` 的展开数组以及计算得到的余切值。用 Excel 打开文件，你会看到从 A1 开始的 5 × 5 块以及 B1 中的数字 `1`。

![创建新的 Excel 工作簿示例输出](excel-output.png "创建新的 Excel 工作簿示例输出")

*图片替代文字：创建新的 Excel 工作簿示例输出*

### 快速验证

1. 打开 `output.xlsx`。  
2. 检查单元格 **A1:E5** 是否包含重复的 1‑2‑3 模式。  
3. 查看 **B1** —— 应显示 `1`。  

如果一切匹配，恭喜你——已成功实现 Excel 自动化！

## 如何在其他场景中 expand sequence

虽然上面的示例使用了静态的 `SEQUENCE(3)`，但你可以轻松将其替换为动态范围或其他公式：

```csharp
// Expand a dynamic range from D1:D10 to a 4×4 block
worksheet.Cells["F1"].Formula = "=EXPAND(D1:D10,4,4)";
```

**何时使用？**  
- 为模板生成占位表格。  
- 快速在多列之间复制标题行。  
- 构建热图网格，无需手动复制粘贴。

## 常见陷阱及避免方法

| 陷阱 | 产生原因 | 解决方案 |
|------|----------|--------|
| `#VALUE!` after `EXPAND` | 源数组不是有效范围（例如包含错误） | 清理源数据或使用 `IFERROR` 包裹。 |
| Cotangent returns `#DIV/0!` for 0° | `COT(0)` 在数学上是无穷大 | 使用 `IF(PI()/4=0,0,COT(...))` 进行防护。 |
| Workbook not saved | 路径无效或缺少写入权限 | 使用 `Path.GetFullPath` 并验证文件夹是否存在。 |
| Formulas not calculated | 未调用 `CalculateFormula` | 在 `Save` 之前始终调用它。 |

## 额外内容：添加样式（可选）

如果希望输出更美观，可以在计算后应用一个简单的样式：

```csharp
        // Apply a light gray background to the expanded block
        Style style = workbook.CreateStyle();
        style.Pattern = BackgroundType.Solid;
        style.ForegroundColor = System.Drawing.Color.LightGray;
        StyleFlag flag = new StyleFlag { CellShading = true };
        worksheet.Cells.CreateRange("A1:E5").ApplyStyle(style, flag);
```

此代码片段为可选，但它展示了如何在一次操作中将 **create new Excel workbook** 逻辑与格式化相结合。

## 回顾

我们已经完整演示了整个过程：

1. **Create new Excel workbook** 使用 Aspose.Cells。  
2. 使用 **how to use expand** 将小型 `SEQUENCE` 转换为 5 × 5 矩阵。  
3. 展示 **how to calculate cotangent** 在单元格中的直接计算。  
4. 使用 `CalculateFormula` 强制计算。  
5. **Save workbook to file** 并验证结果。  

所有这些都是独立的，可在任何近期的 .NET 运行时上运行，并且仅需一个 NuGet 包。

## 接下来做什么？

- **Dynamic data sources:** 从数据库提取数据并将其输入 `EXPAND`。  
- **Multiple worksheets:** 遍历工作表集合以生成完整的报告簿。  
- **Advanced formulas:** 探索 `LET`、`LAMBDA` 或基于数组的条件逻辑，以实现更智能的电子表格。  

随意尝试——更换 `SEQUENCE` 参数，尝试不同角度的 `COT`，或加入图表生成。当你能够以编程方式 **create new Excel workbook** 时，想象空间无限。

---

*祝编码愉快！如果遇到任何问题，请在下方留言或在 Twitter 上 @YourHandle 私信我。我很乐意提供帮助。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}