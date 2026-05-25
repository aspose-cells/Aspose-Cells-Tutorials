---
category: general
date: 2026-04-07
description: 在电子表格单元格中应用自定义数字格式，并学习在使用 C# 导出单元格值时如何对数字进行格式化。快速、完整的指南。
draft: false
keywords:
- apply custom number format
- format number in spreadsheet
- how to format numeric cell
- how to export cell value
language: zh
og_description: 对电子表格单元格应用自定义数字格式，并将其导出为格式化字符串。了解如何在电子表格中格式化数字并导出单元格值。
og_title: 应用自定义数字格式 – 完整的 C# 导出教程
tags:
- C#
- Spreadsheet
- Number Formatting
title: 在 C# 电子表格导出中应用自定义数字格式 – 步骤指南
url: /zh/net/excel-custom-number-date-formatting/apply-custom-number-format-in-c-spreadsheet-export-step-by-s/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 电子表格导出中应用自定义数字格式 – 完整教程

是否曾经需要**应用自定义数字格式**到单元格，然后从电子表格中提取该格式化后的字符串？你并不孤单。许多开发者在发现得到的是原始数值而不是美观、符合地区设置的字符串时会卡住。本文将向你展示如何在电子表格单元格中**format number in spreadsheet**以及如何使用流行的 C# 电子表格库将单元格值导出为格式化字符串。

通过本教程，你将能够对任意数值单元格**apply custom number format**，使用 `ExportTable` 导出结果，并看到在 UI 或报表中显示的精确输出。无需查阅外部文档——所有内容都在这里。

## 前提条件

- .NET 6.0 或更高（代码同样适用于 .NET Framework 4.7+）
- 对提供 `Workbook`、`Worksheet` 和 `ExportTableOptions` 的电子表格库的引用（例如 **Aspose.Cells** 或 **GemBox.Spreadsheet**；示例 API 与 Aspose.Cells 相匹配）
- 基本的 C# 知识——只要会写 `Console.WriteLine`，就可以开始

> **专业提示：** 如果你使用的是其他库，属性名称通常类似（`NumberFormat`、`ExportAsString`），只需相应映射即可。

## 本教程涵盖内容

1. 创建工作簿并选择第一个工作表。  
2. 向单元格插入数值。  
3. 设置 `ExportTableOptions` 以**apply custom number format**并返回字符串。  
4. 导出单元格并打印格式化结果。  
5. 边缘情况处理——如果单元格包含公式或空值怎么办？

让我们开始吧。

![应用自定义数字格式示例](https://example.com/image.png "应用自定义数字格式")

## 步骤 1 – 创建工作簿并获取第一个工作表

你首先需要的是一个工作簿对象。可以把它想象成在 Office 应用中打开的 Excel 文件。获取到工作簿后，拿到第一张工作表——大多数教程从这里开始，因为这样可以让示例保持简洁。

```csharp
// Step 1: Initialize the workbook and fetch the first worksheet
Workbook workbook = new Workbook();                 // creates an in‑memory workbook
Worksheet worksheet = workbook.Worksheets[0];      // first sheet (index 0)
```

**为什么重要：** 全新的工作簿为你提供了干净的起点，确保没有隐藏的格式会干扰我们后续的自定义数字格式。

## 步骤 2 – 将数值放入单元格 B2（我们将要导出的单元格）

现在我们需要一些可以格式化的内容。单元格 **B2** 是一个方便的位置——易于引用且离默认的 A1 角落足够远，避免意外覆盖。

```csharp
// Step 2: Insert a raw numeric value
worksheet.Cells["B2"].Value = 1234.56;   // raw double, no formatting yet
```

**如果值是公式怎么办？**  
如果你随后将原始值替换为公式（例如 `=SUM(A1:A10)`），导出过程仍会遵循我们在下一步设置的数字格式，因为格式是附加在单元格上的，而不是值的类型。

## 步骤 3 – 配置导出选项以获取格式化后的字符串

这是本教程的核心：我们告诉库在导出时**apply custom number format**。`NumberFormat` 字符串遵循 Excel “自定义”类别中使用的相同模式。

```csharp
// Step 3: Set up options for exporting as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,                         // forces string output
    NumberFormat = "#,##0.00;(#,##0.00)"           // custom format: 1,234.56 or (1,234.56) for negatives
};
```

- `ExportAsString = true` 确保方法返回 `string` 而不是原始的 double。  
- `NumberFormat = "#,##0.00;(#,##0.00)"` 与 Excel 的模式相同：千位使用逗号、保留两位小数，负数使用括号。

> **为什么使用自定义格式？** 它保证了跨文化的**一致性**（例如美国与欧洲的数字分隔符），并且可以嵌入**业务特定的样式**，如会计用的括号。

## 步骤 4 – 使用配置好的选项导出单元格

现在我们真正从工作表中提取值，让库负责应用我们定义的格式。

```csharp
// Step 4: Export the formatted value from B2
string formattedResult = worksheet.Cells.ExportTable(
    worksheet.Cells["B2"],   // the source cell
    exportOptions);         // our custom options
```

**边缘情况 – 空单元格：** 如果 `B2` 为**空**，`formattedResult` 将为 `null`。你可以在**打印**之前使用简单的**空值检查**来防止这种情况。

## 步骤 5 – 显示格式化字符串

最后，我们**将**结果**写入**控制台**。**在实际的**应用中，你**可能会**把这个**字符串**推送到**PDF**、**电子邮件**或**UI 标签**中。

```csharp
// Step 5: Show the result
Console.WriteLine(formattedResult);   // Expected output: 1,234.56
```

**预期输出**

```
1,234.56
```

如果将原始值改为 `-9876.54`，相同的格式会得到 `(9,876.54)`——这正是许多会计报表所需的。

## 完整、可运行的示例

下面是完整的程序，你可以直接复制粘贴到新的控制台项目中。只要已添加相应的电子表格库 NuGet 包，它即可直接编译运行。

```csharp
using System;
using Aspose.Cells;   // Replace with your library’s namespace if different

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Insert numeric value into B2
        worksheet.Cells["B2"].Value = 1234.56;

        // 3️⃣ Set export options – apply custom number format
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00;(#,##0.00)"   // custom format
        };

        // 4️⃣ Export the cell as a formatted string
        string formattedResult = worksheet.Cells.ExportTable(
            worksheet.Cells["B2"], exportOptions);

        // 5️⃣ Output the result
        Console.WriteLine(formattedResult);   // → 1,234.56
    }
}
```

### 快速检查

- **它能编译吗？** 能——只需确保已引用 `Aspose.Cells`（或等价）DLL。  
- **它能在其他地区使用吗？** 格式字符串与地区无关；库会遵循你提供的模式。如果需要特定地区的分隔符，可以在导出前加入 `CultureInfo` 处理。

## 常见问题与变体

### 如何使用不同的模式**format number in spreadsheet**？

替换 `NumberFormat` 字符串。例如，显示带一位小数的百分比：

```csharp
NumberFormat = "0.0%";
```

### 如果我需要将**how to export cell value**导出为 HTML 而不是纯文本怎么办？

大多数库都有接受导出类型的重载。你可以设置 `ExportAsString = true` 并添加 `ExportHtml = true`（或类似选项）。原则保持不变：先定义格式，然后选择输出表示方式。

### 我能将格式应用于整个范围，而不是单个单元格吗？

当然可以。你可以将 `NumberFormat` 赋给 `Style` 对象，然后将该样式应用到 `Range`。导出调用保持不变，库会自动使用该样式。

```csharp
Style style = workbook.CreateStyle();
style.Custom = "#,##0.00;(#,##0.00)";
Range range = worksheet.Cells.CreateRange("A1:C10");
range.ApplyStyle(style, new StyleFlag { NumberFormat = true });
```

### 当单元格包含公式时会怎样？

导出过程会先计算公式，然后对得到的数值进行格式化。无需额外代码——如果关闭了自动计算，请确保已调用 `Calculate`。

```csharp
worksheet.Cells["B2"].Formula = "=SUM(A1:A5)";
worksheet.Calculate();   // forces evaluation
```

## 结论

现在你已经掌握了如何对电子表格单元格**apply custom number format**，以及在**format number in spreadsheet**场景中使用，并且能够**how to export cell value**为可直接显示的字符串。上面的简洁代码示例涵盖了从工作簿创建到最终输出的每一步，方便直接嵌入到生产项目中。

准备好接受下一个挑战了吗？尝试将此技巧与**how to format numeric cell**结合，用于日期、货币符号或条件格式。或者探索在导出为 CSV 时保留每个单元格的自定义格式。可能性无限，而这些基础为你奠定了坚实的基石。

祝编码愉快，别忘了多多实验——有时只要稍微调整一下格式字符串，就能得到最佳答案！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}