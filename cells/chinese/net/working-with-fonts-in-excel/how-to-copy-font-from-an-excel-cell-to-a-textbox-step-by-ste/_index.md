---
category: general
date: 2026-02-15
description: 如何在 C# 中复制字体并应用单元格样式的简易示例。了解如何获取单元格样式并使用单元格格式设置文本框的字体大小。
draft: false
keywords:
- how to copy font
- apply cell style
- get cell style
- use cell formatting
- set textbox font size
language: zh
og_description: 如何从工作表单元格复制字体并将单元格样式应用于文本框。本指南展示了如何获取单元格样式、使用单元格格式以及设置文本框字体大小。
og_title: 如何从 Excel 单元格复制字体 – 完整 C# 教程
tags:
- C#
- EPPlus
- UI‑grid
- Excel‑interop
title: 如何将 Excel 单元格的字体复制到文本框 – 步骤指南
url: /zh/net/working-with-fonts-in-excel/how-to-copy-font-from-an-excel-cell-to-a-textbox-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何从 Excel 单元格复制字体到 TextBox – 完整 C# 教程

是否曾需要**复制字体**从电子表格单元格，并让 UI 文本框看起来完全一致？你并不是唯一遇到这种情况的人。在许多报表工具或自定义仪表板中，你会发现自己从 Excel 中提取数据，然后尝试保持视觉一致性——字体族、大小和颜色——不变。  

好消息是，只需几行 C# 代码，你就可以**获取单元格样式**，读取其字体属性，并**应用单元格样式**到任何 text‑box 控件。在本教程中，我们将演示一个完整、可运行的示例，展示如何**使用单元格格式**，甚至**以编程方式设置文本框字体大小**。

---

## 您将学习的内容

- 如何从网格组件（示例中的 `gridJs`）中检索 `TextBox` 对象
- 如何从特定的 Excel 单元格（`B2`）读取字体族、大小和颜色
- 如何将这些字体属性复制到文本框，使 UI 与电子表格保持一致
- 常见陷阱（例如颜色转换）以及一些**专业提示**，帮助你的代码更健壮
- 一个可直接运行的代码片段，可直接放入控制台应用或 WinForms 项目中

**Prerequisites**  
你应该具备：

1. .NET 6+（或 .NET Framework 4.8）已安装  
2. EPPlus NuGet 包（用于 Excel 处理）  
3. 一个公开 `TextBoxes` 字典的网格控件（示例使用了虚构的 `gridJs`，但该思路适用于任何 UI 库）

现在，让我们动手实践吧。

## 步骤 1：设置项目并加载工作表

首先，创建一个新的控制台或 WinForms 项目并添加 EPPlus：

```bash
dotnet add package EPPlus --version 6.*
```

然后，加载工作簿并获取你想复制样式的单元格。

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System.Drawing;

// ...

// Load the Excel file (make sure the file exists at the given path)
var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
using var package = new ExcelPackage(fileInfo);
ExcelWorksheet ws = package.Workbook.Worksheets["Sheet1"]; // adjust sheet name if needed

// Retrieve the style of cell B2
ExcelStyle cellStyle = ws.Cells["B2"].Style;
```

**为什么这很重要：** EPPlus 让你直接访问 `Style` 对象，其中包含 `Font` 子对象。由此你可以读取 `Name`、`Size` 和 `Color`。这就是**获取单元格样式**操作的核心。

---

## 步骤 2：从网格中获取目标 TextBox

假设你的 UI 网格（`gridJs`）将文本框存储在以列名为键的字典中，你可以这样检索所需的文本框：

```csharp
// Fake grid class for illustration – replace with your actual grid component
var gridJs = new MyGrid(); // MyGrid is a placeholder for your UI control

// Step 1: Retrieve the "Notes" text box from the grid
var notesTextBox = gridJs.TextBoxes["Notes"];
```

如果你使用 WinForms，`notesTextBox` 可以是 `TextBox` 控件；在 WPF 中它可能是 `TextBox` 元素；在基于 Web 的网格中，它可能是一个 JavaScript 互操作对象。关键是你拥有可以操作的引用。

## 步骤 3：转移字体族

现在我们已经拥有源样式和目标控件，复制字体族。

```csharp
// Apply the cell's font family to the text box
notesTextBox.FontFamily = cellStyle.Font.Name;
```

**专业提示：** 并非所有 UI 框架都公开接受普通字符串的 `FontFamily` 属性。在 WinForms 中，你可以设置 `notesTextBox.Font = new Font(cellStyle.Font.Name, notesTextBox.Font.Size);`。请相应调整。

## 步骤 4：转移字体大小

字体大小在 EPPlus 中以 `float` 存储。直接应用即可：

```csharp
// Apply the cell's font size to the text box
notesTextBox.FontSize = cellStyle.Font.Size;
```

如果你的控件使用点（大多数情况下是），可以直接赋值，无需转换。对于基于 CSS 的网格，可能需要在数值后追加 "pt"。

## 步骤 5：转移字体颜色

颜色转换是最棘手的部分，因为 EPPlus 将颜色存储为 ARGB 整数，而许多 UI 框架期望的是 `System.Drawing.Color` 或 CSS 十六进制字符串。

```csharp
// Apply the cell's font colour to the text box
// EPPlus stores colour as a System.Drawing.Color when using .Color property
var excelColor = cellStyle.Font.Color?.GetColor();

// Fallback to black if the cell has no explicit colour
var safeColor = excelColor ?? Color.Black;

// Convert to the format your UI expects (example for WinForms)
notesTextBox.FontColor = safeColor;
```

> **为什么这样有效：** `GetColor()` 解析基于主题的颜色并返回具体的 `System.Drawing.Color`。如果单元格使用默认颜色（未显式设置），我们默认使用黑色，以避免空引用异常。

## 完整工作示例

将所有内容组合在一起，下面是一个最小的控制台应用示例，它读取 Excel 文件，提取 **B2** 的字体，并将其应用到一个模拟的文本框。

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System;
using System.Collections.Generic;
using System.Drawing;

namespace FontCopyDemo
{
    // Mock grid control – replace with your real UI component
    public class MyGrid
    {
        public Dictionary<string, TextBoxMock> TextBoxes { get; } = new()
        {
            { "Notes", new TextBoxMock() }
        };
    }

    // Simple text box representation for demonstration
    public class TextBoxMock
    {
        public string FontFamily { get; set; }
        public float FontSize { get; set; }
        public Color FontColor { get; set; }

        public override string ToString()
        {
            return $"FontFamily: {FontFamily}, FontSize: {FontSize}, FontColor: {FontColor.Name}";
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Load Excel worksheet
            var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
            using var package = new ExcelPackage(fileInfo);
            var ws = package.Workbook.Worksheets["Sheet1"];
            var cellStyle = ws.Cells["B2"].Style;

            // 2️⃣ Grab the target TextBox from the grid
            var gridJs = new MyGrid();
            var notesTextBox = gridJs.TextBoxes["Notes"];

            // 3️⃣ Apply font family
            notesTextBox.FontFamily = cellStyle.Font.Name;

            // 4️⃣ Apply font size
            notesTextBox.FontSize = cellStyle.Font.Size;

            // 5️⃣ Apply font colour (with safety net)
            var excelColor = cellStyle.Font.Color?.GetColor();
            notesTextBox.FontColor = excelColor ?? Color.Black;

            // Output the result for verification
            Console.WriteLine("TextBox after copying font:");
            Console.WriteLine(notesTextBox);
        }
    }
}
```

**预期输出（假设 B2 使用 Arial，12 pt，蓝色）：**

```
TextBox after copying font:
FontFamily: Arial, FontSize: 12, FontColor: Blue
```

运行程序，打开你的 UI，你会看到 “Notes” 文本框现在完全复制了单元格 **B2** 的字体样式。无需手动调整。

## 常见问题与边缘情况

### 如果单元格使用主题颜色而不是显式的 RGB 值怎么办？

EPPlus 的 `GetColor()` 会自动将主题颜色解析为具体的 `System.Drawing.Color`。然而，如果你使用的旧库仅返回主题索引，则需要自行将该索引映射到颜色调色板。

### 我可以复制其他样式属性吗（例如，加粗、斜体）？

当然可以。`ExcelStyle.Font` 对象同样公开 `Bold`、`Italic`、`Underline` 和 `Strike`。只需在 UI 控件上设置相应属性：

```csharp
notesTextBox.FontBold = cellStyle.Font.Bold;
notesTextBox.FontItalic = cellStyle.Font.Italic;
```

### 如果网格控件没有公开 `FontColor` 属性怎么办？

大多数现代 UI 框架都有此属性，但如果你的框架只接受 CSS 字符串，需要将 `Color` 转换为十六进制：

```csharp
string hex = $"#{notesTextBox.FontColor.R:X2}{notesTextBox.FontColor.G:X2}{notesTextBox.FontColor.B:X2}";
notesTextBox.Style["color"] = hex; // for web‑based grids
```

### 如何一次处理多个单元格？

遍历所需范围，获取每个单元格的样式，并将其应用到相应的文本框。如果处理大量行，请记得缓存样式对象，以避免性能下降。

## 专业提示与常见陷阱

- **缓存 ExcelPackage** —— 为每个单元格打开和关闭文件代价高。一次加载工作簿，然后复用 `ExcelWorksheet` 对象。
- **注意空颜色** —— 继承默认颜色的单元格返回 `null`。始终提供回退颜色（黑色或控件默认颜色）。
- **注意 DPI 缩放** —— 针对高 DPI 显示器时，字体大小可能略大。如有需要，可使用 `Graphics.DpiX` 进行调整。
- **线程安全** —— EPPlus 不是线程安全的。如果并行处理多个工作表，请为每个线程创建单独的 `ExcelPackage`。

## 结论

现在你已经了解了如何使用 C# **从 Excel 单元格复制字体**并**将单元格样式应用**到任何 text‑box 控件。通过检索单元格的 `Style`，提取其 `Font` 属性，并将其分配给 UI 元素，你可以在无需手动复制的情况下保持视觉一致性。  

完整的解决方案——加载工作簿、获取单元格样式、设置文本框的字体族、大小和颜色——涵盖了**使用单元格格式**的核心，并演示了如何正确**设置文本框字体大小**。  

接下来，尝试扩展示例以复制背景颜色、边框，甚至整个单元格内容。如果你使用的 data‑grid 库支持丰富的单元格渲染，现在可以将从 Excel 提取的完全相同的样式信息提供给它，从而保持 UI 与报表的完美同步。  

还有其他问题吗？留下评论或探索相关主题，如“动态 Excel‑到‑UI 绑定”和“主题感知颜色转换”。祝编码愉快！

![如何复制字体示例](placeholder-image.jpg "如何从 Excel 单元格复制字体到 TextBox")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}