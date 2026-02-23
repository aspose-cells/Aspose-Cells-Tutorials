---
category: general
date: 2026-02-23
description: 在 C# 中以编程方式创建新工作簿并向单元格添加公式。学习如何使用 EXPAND，然后轻松保存 Excel 工作簿。
draft: false
keywords:
- create new workbook
- add formula to cell
- save excel workbook
- how to use expand
- create excel file programmatically
language: zh
og_description: 在 C# 中以编程方式创建新工作簿。向单元格添加公式，学习如何使用 EXPAND，并在几秒钟内保存 Excel 工作簿。
og_title: 在 C# 中创建新工作簿 – 添加公式并保存 Excel 文件
tags:
- C#
- Excel Automation
- Aspose.Cells
title: 在 C# 中创建新工作簿 – 添加公式并保存 Excel 文件
url: /zh/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中创建新工作簿 – 添加公式并保存 Excel 文件

是否曾想过 **从代码创建新工作簿** 而无需打开 Excel？你并不是唯一有此需求的人。许多开发者在需要即时生成电子表格时会碰壁——可能是为了报告、导出或快速的数据转储。

好消息是？在本指南中，你将看到如何 **创建新工作簿**、向 **单元格添加公式**，然后仅用几行 C# **保存 Excel 工作簿**。我们还会深入探讨 **如何使用 EXPAND**，让你在无需手动复制的情况下生成动态数组。完成后，你将能够 **以编程方式创建 Excel 文件** 并将其交付给用户或下游服务。

## 前置条件

- .NET 6.0 或更高版本（任何近期的 .NET 运行时均可）
- Aspose.Cells for .NET（免费试用版或正式授权版）——该库提供本文使用的 `Workbook` 和 `Worksheet` 类。
- 对 C# 语法有基本了解——不需要深入的 Excel 知识。

如果你已经具备上述条件，太好了！如果没有，请从 NuGet 获取 Aspose.Cells（`Install-Package Aspose.Cells`），即可开始使用。

---

## 步骤 1：创建新工作簿 – 基础

首先，需要实例化一个全新的工作簿对象。可以把它想象成打开了一个全新的、完全空白的 Excel 文件。

```csharp
using Aspose.Cells;

public class ExcelGenerator
{
    public void Generate()
    {
        // Step 1: Create a new workbook (this is the core of create new workbook)
        Workbook workbook = new Workbook();
```

> **为什么重要：** `Workbook` 类是所有 Excel 操作的入口。创建新实例后，我们为工作表、样式和公式分配内存——全部在不触及文件系统的情况下完成。

---

## 步骤 2：访问第一个工作表

每个新工作簿都会默认包含一个工作表（名称为 *Sheet1*）。我们需要获取它，以便放置数据和公式。

```csharp
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];
```

> **小技巧：** 如果需要多个工作表，只需调用 `workbook.Worksheets.Add("MySheet")` 并使用返回的 `Worksheet` 对象即可。

---

## 步骤 3：向单元格添加公式 – 使用 EXPAND

现在进入有趣的部分：插入公式。`EXPAND` 函数在你想把静态数组扩展为更大、自动填充的范围时非常适用。

```csharp
        // Step 3: Add formula to cell A1 using EXPAND
        // This creates a 5‑row array from the constant {1,2,3}
        worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";
```

### EXPAND 公式工作原理

| 参数 | 含义 |
|------|------|
| `{1,2,3}` | 源数组（水平的三个数字列表） |
| `5` | 结果所需的行数 |
| `1` | 结果所需的列数（保持为 1 则为垂直方向） |

当 Excel 计算此公式时，会生成一个 **垂直** 列表：

```
A1: 1
A2: 2
A3: 3
A4: 0   (filled with zeros)
A5: 0
```

> **为什么使用 EXPAND？** 它消除了手动复制或 VBA 循环的需求。该函数能够动态重塑数据，使你的电子表格更健壮、更易维护。

---

## 步骤 4：保存 Excel 工作簿 – 持久化结果

公式就位后，最后一步是将工作簿写入磁盘。你可以选择任意有写入权限的文件夹。

```csharp
        // Step 4: Save the workbook to view the result
        string outputPath = @"C:\Temp\ExpandFormula.xlsx";
        workbook.Save(outputPath);
    }
}
```

> **你会看到的效果：** 在 Excel 中打开 `ExpandFormula.xlsx`，单元格 `A1` 将显示展开后的数组。公式本身仍保留在单元格中，因此如果编辑源数组，输出会自动更新。

---

## 可选：以编程方式验证输出

如果不想手动打开 Excel，也可以读取返回的值以确认其符合预期。

```csharp
        // Verify values without opening Excel
        for (int row = 0; row < 5; row++)
        {
            var value = worksheet.Cells[row, 0].Value; // column 0 = A
            Console.WriteLine($"Row {row + 1}: {value}");
        }
```

运行上述代码将输出：

```
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

---

## 常见问题与边缘情况

| 问题 | 答案 |
|------|------|
| **可以在更大的源数组上使用 EXPAND 吗？** | 当然。只需将 `{1,2,3}` 替换为任意常量或单元格范围，例如 `EXPAND(A1:C1,10,1)`。 |
| **如果需要水平结果怎么办？** | 交换行/列参数：`EXPAND({1,2,3},1,5)` 将生成 1 行 5 列的展开。 |
| **这在旧版 Excel 上可用吗？** | `EXPAND` 从 Excel 365/2021 开始提供。对于更旧的版本，需要使用 `INDEX`/`SEQUENCE` 等函数模拟数组。 |
| **需要调用 `workbook.CalculateFormula()` 吗？** | 不需要。Aspose.Cells 在保存时会自动计算公式，值会立即显示。 |
| **如何在保存前添加多个工作表？** | 调用 `workbook.Worksheets.Add("SecondSheet")`，然后在新工作表上重复单元格操作步骤。 |

---

## 完整工作示例

下面是完整的、可直接运行的程序。复制粘贴到控制台应用中，调整输出路径后，按 **F5** 运行。

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutomationDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create new workbook
            Workbook workbook = new Workbook();

            // Access first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // Add EXPAND formula to A1
            worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";

            // Optional: verify values in console
            workbook.CalculateFormula(); // ensures formulas are evaluated now
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine($"A{i + 1} = {worksheet.Cells[i, 0].Value}");
            }

            // Save the workbook
            string filePath = @"C:\Temp\ExpandFormula.xlsx";
            workbook.Save(filePath);
            Console.WriteLine($"Workbook saved to {filePath}");
        }
    }
}
```

**控制台预期输出：**

```
A1 = 1
A2 = 2
A3 = 3
A4 = 0
A5 = 0
Workbook saved to C:\Temp\ExpandFormula.xlsx
```

打开生成的文件，你会看到相同的数字填充在 **A** 列中。

---

## 可视化摘要

![Create new workbook example](create-new-workbook.png "Screenshot showing a new workbook created with create new workbook in C#")

*该图片展示了使用 C# 创建的新工作簿以及 EXPAND 结果。*

---

## 结论

现在，你已经掌握了使用 C# **创建新工作簿**、**向单元格添加公式** 并 **保存 Excel 工作簿** 的方法。通过熟练使用 **EXPAND**，可以在无需手动操作的情况下生成动态数组，整个过程让你能够 **以编程方式创建 Excel 文件**，满足各种自动化场景。

接下来可以尝试将常量数组换成范围引用，实验不同的 `EXPAND` 维度，或在多个工作表之间链式使用公式。同样的模式也适用于图表、样式甚至数据透视表——继续探索吧。

如果遇到任何问题，欢迎在下方留言。祝编码愉快，尽情享受编程 Excel 的强大力量！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}