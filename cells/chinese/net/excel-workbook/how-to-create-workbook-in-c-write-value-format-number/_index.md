---
category: general
date: 2026-03-01
description: 如何快速在 C# 中创建工作簿——学习向单元格写入值、设置单元格数字格式以及使用简易步骤格式化单元格数字。
draft: false
keywords:
- how to create workbook
- write value to cell
- format cell number
- set cell number format
- how to write cell
language: zh
og_description: 如何在 C# 中创建工作簿？本指南向您展示如何将值写入单元格、设置单元格数字格式，以及仅用几行代码对单元格数字进行格式化。
og_title: 如何在 C# 中创建工作簿 – 写入值并格式化数字
tags:
- C#
- Aspose.Cells
- Excel Automation
title: 如何在 C# 中创建工作簿 – 写入值并格式化数字
url: /zh/net/excel-workbook/how-to-create-workbook-in-c-write-value-format-number/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中创建工作簿 – 写入值并格式化数字

在需要即时生成 Excel 文件时，如何在 C# 中创建工作簿是一个常见任务。在本指南中，我们将一步步演示如何向单元格写入值并设置单元格数字格式，使最终的工作表看起来更专业。

如果你曾盯着空白的电子表格，疑惑为什么数字总是显示太多小数位，你并不孤单。我们将覆盖从初始化工作簿对象到设置自定义数字格式的全部内容，并提供一些后期可能遇到的边缘情况的技巧。

## 你将学习

- **Initialize** 一个新的 `Workbook` 实例。  
- 使用 `PutValue` 方法 **Write value to cell**。  
- 使用 `Style` 对象 **Set cell number format**，实现干净的两位数字显示。  
- 通过读取单元格或在 Excel 中打开文件来验证结果。  

无需除标准 Aspose.Cells（或任何类似 API）之外的外部库，代码可在 .NET 6+ 上直接运行，无需额外配置。

---

## 如何创建工作簿 – 初始化对象

首先，你需要一个工作簿对象来容纳工作表。把 `Workbook` 看作整个 Excel 文件，而每个 `Worksheet` 则是其中的一个标签页。

```csharp
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

*为什么这很重要：* 创建工作簿会分配内部结构，后续用于存放行、列和格式化信息。没有这个对象，就没有地方可以向单元格写入值。

> **Pro tip:** 如果你计划使用已有文件，将 `new Workbook()` 替换为 `new Workbook("template.xlsx")` 以加载模板并保留其样式。

## 写入单元格的值

现在我们已有工作簿，接下来把一个数字写入第一个工作表的 **A1** 单元格。

```csharp
// Step 2: Access cell A1 in the first worksheet
Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

// Step 3: Insert a numeric value into the cell
cellA1.PutValue(123.456789);
```

*为什么使用 `PutValue`：* 该方法会自动检测数据类型，无需手动强制转换或转换。它还会保留单元格已有的样式，这在后续 **set cell number format** 时非常方便。

### 快速检查

如果读取该单元格，你会看到原始值：

```csharp
double raw = cellA1.DoubleValue; // raw == 123.456789
```

这就是在任何格式化应用之前的数字。

## 设置单元格数字格式

直接显示带有许多小数位的原始 double 并不友好。我们将其限制为两位有效数字。

```csharp
// Step 4: Apply a style that formats the number with two significant digits
cellA1.SetStyle(new Style() { Number = 2 });
```

`Number` 属性对应 Excel 内置的数字格式 ID。`2` 表示 “带两位小数的数字”。如果需要其他格式——比如货币或日期——可以使用其他 ID 或自定义格式字符串。

### 替代方案：自定义格式字符串

```csharp
Style customStyle = workbook.CreateStyle();
customStyle.Custom = "#,##0.00"; // forces two decimals with thousand separator
cellA1.SetStyle(customStyle);
```

*为什么选择自定义样式？* 当内置 ID 无法满足你的地区设置时，自定义样式提供了完整的控制权。

## 验证输出（可选但推荐）

应用样式后，你可以保存工作簿并在 Excel 中打开以确认外观。

```csharp
// Save the workbook to a file
workbook.Save("FormattedWorkbook.xlsx");

// Or, for quick verification in code:
string displayed = cellA1.StringValue; // "123.46"
Console.WriteLine($"Displayed value: {displayed}");
```

你应该在 A1 单元格看到 **123.46**——恰好两位小数，正是我们设置的格式所致。

---

### 完整工作示例

将所有步骤组合在一起，下面是一个可以直接复制粘贴到控制台应用程序中的完整示例。

```csharp
using System;
using Aspose.Cells;   // Ensure you have the Aspose.Cells NuGet package

class Program
{
    static void Main()
    {
        // Initialize the workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet and cell A1
        Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

        // Write a numeric value
        cellA1.PutValue(123.456789);

        // Apply a two‑decimal number format
        cellA1.SetStyle(new Style() { Number = 2 });

        // Save to disk (optional)
        workbook.Save("FormattedWorkbook.xlsx");

        // Output the displayed text for verification
        Console.WriteLine($"Cell A1 shows: {cellA1.StringValue}");
    }
}
```

**运行程序时的预期输出：**

```
Cell A1 shows: 123.46
```

在 Excel 中打开 `FormattedWorkbook.xlsx`，你会看到相同的格式化数值。

---

## 常见变体与边缘情况

### 1. 不同的数字格式

| 目标 | 格式 ID | 代码片段 |
|------|-----------|--------------|
| 货币（两位小数） | 5 | `cellA1.SetStyle(new Style() { Number = 5 });` |
| 百分比（无小数） | 10 | `cellA1.SetStyle(new Style() { Number = 10 });` |
| 科学计数法 | 11 | `cellA1.SetStyle(new Style() { Number = 11 });` |

如果内置 ID 都不适用，可回退使用前面示例中的自定义字符串。

### 2. 区域特定的小数分隔符

某些地区使用逗号作为小数点。你可以强制使用区域感知的格式：

```csharp
Style cultureStyle = workbook.CreateStyle();
cultureStyle.Custom = "#,##0.00"; // works for most European locales
cellA1.SetStyle(cultureStyle);
```

### 3. 写入文本而非数字

当需要 **how to write cell** 为字符串时，只需将字符串传给 `PutValue`：

```csharp
cellA1.PutValue("Total Revenue");
```

不需要数字格式，但仍可应用字体样式。

### 4. 大数据集

如果要填充数千行，使用批量插入 (`Cells.ImportArray`) 比循环 `PutValue` 更快。格式化方式保持不变，只需将样式应用到一个范围：

```csharp
Range range = workbook.Worksheets[0].Cells.CreateRange("B2:B1001");
range.ApplyStyle(new Style() { Number = 2 });
```

---

## 常见问题

**Q: 这在 .NET Core 上能工作吗？**  
A: 完全可以。Aspose.Cells 支持 .NET Standard 2.0 及更高版本，因而可以在 .NET 5、.NET 6 或 .NET 7 上使用，无需修改。

**Q: 如果需要超过两位小数怎么办？**  
A: 将 `Number` 属性改为相应的内置 ID（例如 `3` 表示三位小数），或调整自定义格式字符串（`"#,##0.000"`）。

**Q: 能一次性对整列应用格式吗？**  
A: 可以。使用 `Cells["A:A"]` 获取整列，然后调用 `SetStyle`。

---

## 结论

现在你已经掌握了在 C# 中 **how to create workbook**、**write value to cell**，以及 **set cell number format** 的方法，使数字能够按照你期望的方式显示。通过熟练运用这些基础，你可以轻松生成专业外观的 Excel 报表、发票或数据导出。

接下来，你可以进一步探索 **format cell number** 用于日期、百分比或条件格式——这些都基于我们已经介绍的相同原理。深入阅读 Aspose.Cells 文档以获取更丰富的样式选项，或尝试将多个工作表合并到同一个工作簿中，以创建更丰富的报告。

祝编码愉快，记住：一个格式良好的电子表格只是

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}