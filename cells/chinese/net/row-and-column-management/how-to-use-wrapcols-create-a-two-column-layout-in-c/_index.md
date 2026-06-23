---
category: general
date: 2026-02-15
description: 如何在 C# 工作表中使用 WRAPCOLS 创建两列布局、添加公式并生成序列数组——一步步指南。
draft: false
keywords:
- how to use wrapcols
- create two column layout
- how to add formula
- how to create columns
- generate sequence array
language: zh
og_description: 如何在 C# 工作表中使用 WRAPCOLS 构建两列布局、添加公式并生成序列数组——完整指南。
og_title: 如何使用 WRAPCOLS：C# 中的两列布局
tags:
- CSharp
- ExcelAutomation
- WorksheetFormula
title: 如何使用 WRAPCOLS：在 C# 中创建双列布局
url: /zh/net/row-and-column-management/how-to-use-wrapcols-create-a-two-column-layout-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 WRAPCOLS：在 C# 中创建两列布局

是否曾经想过 **如何使用 WRAPCOLS**，当你需要在类似 Excel 的工作表中快速实现两列视图时？你并不孤单。许多开发者在尝试将生成的列表拆分为整齐的列而不为每个单元格编写循环时会遇到瓶颈。好消息是？使用 `WRAPCOLS` 函数，你只需在 `A1` 中输入一个公式，让 Excel（或兼容的引擎）完成繁重的工作。

在本教程中，我们将逐步演示 **how to add formula**，它可以创建 **create two column layout**，向你展示如何动态 **how to create columns**，甚至实时 **generate sequence array**。结束时，你将拥有一个可直接运行的 C# 代码片段，复制到项目中运行，即可立即看到整齐的两列块。

## 你将学到

- `WRAPCOLS` 的用途以及它为何是手动循环的更佳替代方案。  
- 如何使用 C# **add a formula** 到工作表单元格。  
- 如何使用 `SEQUENCE` 生成序列数组并将其传递给 `WRAPCOLS`。  
- 关于重新计算工作表以使公式立即生效的技巧。  
- 边缘情况处理（例如，空工作表、自定义列数）。

不需要除标准 Excel 处理包之外的外部库——我们将使用 **ClosedXML**，因为它的 API 简洁明了，但这些概念同样适用于 EPPlus、SpreadsheetGear，甚至通过其 API 的 Google Sheets。

---

## 前提条件

- .NET 6.0 或更高版本（代码可在 .NET Core 和 .NET Framework 上编译）。  
- 对 **ClosedXML** 的引用（`dotnet add package ClosedXML`）。  
- 基本的 C# 知识——你应熟悉 `using` 语句和对象初始化。  

如果你已经打开了工作簿，可以跳过文件创建步骤，直接进入公式部分。

---

## 步骤 1：设置工作表（如何创建列）

首先我们需要一个 `Worksheet` 对象来操作。在 ClosedXML 中，你可以从 `XLWorkbook` 获取它。下面的代码片段创建了一个新工作簿，添加了名为 *Demo* 的工作表，并获取了一个名为 `worksheet` 的引用，以便于阅读。

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // Create a fresh workbook and add a worksheet named "Demo"
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");

            // Rename for clarity – this is the worksheet we’ll manipulate
            var worksheet = ws;   // <-- same object, just a clearer name

            // --------------------------------------------------------------
            // Next step: write the WRAPCOLS formula
            // --------------------------------------------------------------
```

> **为什么重命名？**  
> 将变量名保持简短（`worksheet`）可以让后续代码更易阅读，尤其是在链式调用多个操作时。它也与大多数文档中看到的命名风格保持一致，降低认知负担。

---

## 步骤 2：编写公式（如何添加公式 + 生成序列数组）

现在是关键代码行。我们将在单元格 **A1** 中放置一个公式，它会完成两件事：

1. **Generate a sequence array** 六个数字的序列数组（`SEQUENCE(6)` → 1,2,3,4,5,6）。  
2. **Wrap those numbers into two columns**（`WRAPCOLS(..., 2)`）。

```csharp
            // Write the WRAPCOLS formula into A1
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // --------------------------------------------------------------
            // Finally, force the engine to evaluate the formula
            // --------------------------------------------------------------
```

> **发生了什么？**  
> `SEQUENCE(6)` 创建了一个垂直数组 `{1;2;3;4;5;6}`。随后 `WRAPCOLS` 将该数组“包装”成指定列数——本例为 **2** 列。结果是一个 3 行 × 2 列的块，呈现如下：

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

如果将第二个参数改为 **3**，则会得到三列布局。这就是 **how to create columns** 在无需手动循环的情况下即时创建列的核心。

---

## 步骤 3：重新计算工作表（确保公式求值）

ClosedXML 在写入公式后不会自动求值。你需要在工作簿（或特定工作表）上调用 `Calculate()` 来强制求值。

```csharp
            // Recalculate so the formula is evaluated immediately
            worksheet.Calculate();

            // Optional: save the workbook to inspect the result
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

> **专业提示：** 如果你处理的是大型工作簿，只在实际更改的工作表上调用 `Calculate()`。这可以节省内存并加快处理速度。

打开 `WrapColsDemo.xlsx` 时，你会看到 **A1:B3** 中整齐填充的两列布局。无需额外代码遍历行或列——`WRAPCOLS` 已经完成所有工作。

---

## 步骤 4：验证输出（预期结果）

运行程序后，打开生成的文件。你应该看到：

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

如果数字垂直排列（即全部在 A 列），请再次确认你在设置公式 **之后** 调用了 `worksheet.Calculate()`。某些引擎还需要 `workbook.Calculate()`；上述代码片段适用于 ClosedXML 的内置求值器。

---

## 常见变体与边缘情况

### 更改列数

要 **create two column layout** 并使用不同的行数，只需调整 `SEQUENCE` 的大小或 `WRAPCOLS` 的第二个参数：

```csharp
worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(12), 3)";
```

这将生成一个 4 行 × 3 列的块（12 个数字分布在三列中）。

### 使用动态列数

如果列数来自变量，可使用字符串插值嵌入：

```csharp
int colCount = 4;
worksheet.Cell("A1").FormulaA1 = $"=WRAPCOLS(SEQUENCE(8), {colCount})";
```

现在你已经拥有 **how to add formula**，它可以在运行时自适应。

### 空工作表

如果工作表为空，`Calculate()` 仍然有效——公式会从 A1 开始填充单元格。然而，如果随后删除与输出范围相交的行/列，可能会出现 `#REF!` 错误。为避免此情况，请先清除目标范围：

```csharp
worksheet.Range("A1:Z100").Clear(); // wipes any leftovers
```

### 兼容性

`WRAPCOLS` 和 `SEQUENCE` 属于 Excel 的 **Dynamic Array** 函数，首次在 Office 365 中引入。如果你的目标是旧版 Excel，这些函数将不存在，需要手动循环。ClosedXML 的求值器模拟最新的 Excel 行为，适用于现代环境。

---

## 完整可运行示例（复制粘贴即可）

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook & worksheet
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");
            var worksheet = ws;   // clearer name

            // 2️⃣ Write WRAPCOLS formula that generates a sequence array
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // 3️⃣ Force calculation so the formula resolves immediately
            worksheet.Calculate();

            // 4️⃣ Save the file (optional, but handy for verification)
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

**预期结果：** 打开 *WrapColsDemo.xlsx*，会看到一个整齐的两列布局，数字 1‑6 按前述方式排列。

---

## 结论

我们已经介绍了 **how to use WRAPCOLS** 来 **create a two column layout**，演示了如何以编程方式 **how to add formula**，并看到 `SEQUENCE` 如何让你在无需循环的情况下 **generate sequence array**。通过在 C# 中利用 Excel 的动态数组函数，你可以让 **your code** 简洁、易读且 **maintainable**。

接下来，你可以探索：

- **Creating dynamic row counts** 使用 `ROWS` 或 `COUNTA`。  
- **Styling the output**（边框、数字格式）使用 ClosedXML 的样式 API。  
- **Exporting to CSV** 在布局完成后导出为 CSV，以便后续处理。

试一试，调整列数，看看 **you** 多快就能原型化 **complex spreadsheets**。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}