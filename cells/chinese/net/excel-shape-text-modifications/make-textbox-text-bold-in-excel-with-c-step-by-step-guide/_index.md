---
category: general
date: 2026-02-21
description: 学习如何在完整可运行的示例中使用 Aspose.Cells 将 TextBox 文本设为粗体、修改 TextBox 字体大小，并加载 Excel
  工作簿（C#）。
draft: false
keywords:
- make textbox text bold
- change textbox font size
- load excel workbook c#
- format excel shape text
language: zh
og_description: 使用 C# 将 Excel 文件中的文本框文字加粗。本教程还展示了如何更改文本框字体大小以及使用 Aspose.Cells 在 C#
  中加载 Excel 工作簿。
og_title: 使用 C# 在 Excel 中将文本框文字加粗 – 完整指南
tags:
- C#
- Aspose.Cells
- Excel automation
title: 使用 C# 在 Excel 中将文本框文字加粗 – 步骤指南
url: /zh/net/excel-shape-text-modifications/make-textbox-text-bold-in-excel-with-c-step-by-step-guide/
---

at top and bottom.

Let's produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中使用 C# 将 TextBox 文本加粗 – 步骤指南

需要在 Excel 文件中使用 C# **将 TextBox 文本加粗** 吗？本教程将向您展示如何 *加载 Excel 工作簿*、**更改 TextBox 字体大小**，以及使用 Aspose.Cells 对形状文本进行格式化。  
如果您曾经盯着一张平淡的电子表格并想“我的文本框应该更突出”，那么您来对地方了。

我们将逐行讲解代码，说明每个调用的意义，并且涵盖当工作表根本没有文本框时该怎么办。结束时，您将拥有一个可在任何 .NET 项目中直接使用的代码片段——无需再查找“查看文档”之类的链接。

## 您需要准备的内容

- **Aspose.Cells for .NET**（免费试用或授权版）——我们用来操作 Excel 形状的 API。  
- .NET 6 或更高版本（代码同样适用于 .NET Framework 4.7+）。  
- 一个简单的 Excel 文件（`input.xlsx`），其中第一张工作表已经包含至少一个文本框。  

就这些。无需额外的 NuGet 包，无需 COM 互操作，纯 C#。

## 将 TextBox 文本加粗 – 加载工作簿并获取形状

第一步是打开工作簿并获取要编辑的文本框。  
我们还会进行一次快速的安全检查，以防工作表为空时代码崩溃。

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook (load excel workbook c#)
        var workbookPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];

        // Verify that at least one TextBox exists
        if (worksheet.TextBoxes.Count == 0)
        {
            Console.WriteLine("No TextBoxes found on the first sheet.");
            return;
        }

        // Step 3: Access the first TextBox shape
        Shape textBox = worksheet.TextBoxes[0];

        // From here on we can format the shape's text
```

**为什么这很重要：**  
*加载工作簿* 会为我们提供一个代表整个文件的 `Workbook` 对象。访问 `Worksheets[0]` 是安全的，因为每个 Excel 文件至少有一张工作表。防护语句（`if (worksheet.TextBoxes.Count == 0)`）可以防止 `IndexOutOfRangeException`——这是自动化现有文件时常见的陷阱。

## 更改 TextBox 字体大小

在加粗文本之前，先确保字体大小正是您需要的。  
更改大小只需修改 `Font.Size` 属性即可。

```csharp
        // Step 4: Set the font name (optional but often useful)
        textBox.Font.Name = "Calibri";

        // Step 5: Change the font size (change textbox font size)
        textBox.Font.Size = 12; // 12 points is a comfortable default
```

**小技巧：**  
如果需要根据用户输入动态设置大小，只需将 `12` 替换为变量即可。`Font` 对象在整个形状中共享，尺寸变化会立即影响文本框内的所有字符。

## 将 TextBox 文本加粗 – 核心操作

现在进入重点功能：让文本加粗。  
`IsBold` 标志会在不改变其他样式的前提下切换字体粗细。

```csharp
        // Step 6: Make the text bold (make textbox text bold)
        textBox.Font.IsBold = true;
```

**内部原理是什么？**  
Aspose.Cells 将文本格式存储在附加到形状的 `Font` 对象中。将 `IsBold = true` 会更新底层 XML（`<b>1</b>`），Excel 在渲染工作表时会读取该信息。这是一次 **非破坏性** 操作——如果以后将 `IsBold = false`，文本会恢复为普通粗细。

## 保存修改后的工作簿

完成格式化后，我们将更改写回磁盘。  
您可以覆盖原文件，也可以像下面示例那样创建新文件，以保持源文件不变。

```csharp
        // Step 7: Save the modified workbook
        var outputPath = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved. TextBox is now bold and 12pt Calibri in '{outputPath}'.");
    }
}
```

**预期结果：**  
在 Excel 中打开 `output.xlsx`。第一张工作表的第一个文本框应显示 **Calibri 12 pt，加粗** 的文字。其他形状不受影响。

## 格式化 Excel 形状文本 – 其他样式选项（可选）

虽然主要目标是 **将 TextBox 文本加粗**，但您可能还想：

| 选项 | 代码片段 | 使用场景 |
|------|----------|----------|
| 斜体 | `textBox.Font.IsItalic = true;` | 强调副标题 |
| 文字颜色 | `textBox.Font.Color = System.Drawing.Color.DarkBlue;` | 品牌配色 |
| 对齐方式 | `textBox.AlignmentHorizontal = TextAlignmentType.Center;` | 居中标题 |
| 多个 TextBox | 循环遍历 `worksheet.TextBoxes` | 批量格式化 |

```csharp
// Example: Apply a blue color and center alignment to all textboxes
foreach (Shape tb in worksheet.TextBoxes)
{
    tb.Font.Color = System.Drawing.Color.Blue;
    tb.AlignmentHorizontal = TextAlignmentType.Center;
}
```

这些额外的微调展示了 *format excel shape text* 如何超出单纯加粗的范围。

## 边缘情况与常见陷阱

1. **工作表上没有 TextBox** – 我们添加的防护语句（`if (worksheet.TextBoxes.Count == 0)`）会优雅地退出并提示用户。  
2. **隐藏的工作表** – 隐藏的工作表仍可通过 `Worksheets` 集合访问，只需确保引用正确的索引。  
3. **大型文件** – 加载巨大的工作簿会占用大量内存。考虑使用 `Workbook.LoadOptions` 只加载所需部分。  
4. **不同的 Excel 版本** – Aspose.Cells 支持 `.xls`、`.xlsx` 甚至 `.xlsb`。相同代码可跨版本使用，但旧版 Excel 可能会忽略某些新字体特性。

## 完整可运行示例（复制粘贴即用）

```csharp
using System;
using Aspose.Cells;

class MakeTextboxBoldDemo
{
    static void Main()
    {
        // Load the workbook (load excel workbook c#)
        var inputFile = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputFile);

        // Get the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // Ensure a textbox exists
        if (sheet.TextBoxes.Count == 0)
        {
            Console.WriteLine("No textbox found on the first sheet.");
            return;
        }

        // Access the first textbox
        Shape txtBox = sheet.TextBoxes[0];

        // Set font name and size (change textbox font size)
        txtBox.Font.Name = "Calibri";
        txtBox.Font.Size = 12;

        // Make the text bold (make textbox text bold)
        txtBox.Font.IsBold = true;

        // Optional: extra styling (format excel shape text)
        txtBox.Font.Color = System.Drawing.Color.DarkGreen;
        txtBox.AlignmentHorizontal = TextAlignmentType.Center;

        // Save the result
        var outputFile = @"YOUR_DIRECTORY\output.xlsx";
        workbook.Save(outputFile);

        Console.WriteLine($"Saved: {outputFile}");
    }
}
```

运行程序，打开生成的 `output.xlsx`，您将看到文本框内的文字已加粗、字号为 12 pt 的 Calibri。简单吧？

## 结论

现在您已经掌握了 **如何在 Excel 工作簿中使用 C# 将 TextBox 文本加粗**、**如何更改 TextBox 字体大小**，以及使用 Aspose.Cells **加载 Excel 工作簿 C#** 的基础。上面的完整示例可直接嵌入任何项目，同时您也了解了 **format Excel shape text** 的更多技巧，以实现更丰富的样式。

接下来可以尝试遍历所有工作表，对所有文本框统一加粗，或将其与数据驱动的内容生成结合——比如从数据库填充文本框。原理相同，代码依旧简洁。

有新的思路想分享，或遇到意外错误？欢迎留言，让我们一起讨论。祝编码愉快！

![在 Excel 中使用 C# 将文本框文本加粗](/images/make-textbox-text-bold-csharp.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}