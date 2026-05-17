---
category: general
date: 2026-02-21
description: 快速在 C# 中创建单元格样式。学习如何将样式应用于单元格、在单元格中居中文本、设置单元格对齐方式，以及掌握单元格格式化。
draft: false
keywords:
- create cell style
- apply style to cell
- center text in cell
- set cell alignment
- how to center text
language: zh
og_description: 在 C# 中创建单元格样式，并学习如何将样式应用于单元格、在单元格中居中文本以及设置单元格对齐方式，提供清晰的分步指南。
og_title: 在 C# 中创建单元格样式 – 将样式应用于单元格并居中文本
tags:
- C#
- Aspose.Cells
- Excel automation
title: 在 C# 中创建单元格样式 – 如何将样式应用于单元格并居中文本
url: /zh/net/excel-formatting-and-styling/create-cell-style-in-c-how-to-apply-style-to-a-cell-and-cent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中创建单元格样式 – 应用样式和居中文本的完整指南

是否曾经需要在 Excel 工作表中 **create cell style**，但不知从何入手？你并不孤单。在许多自动化项目中，**apply style to cell** 对象的能力决定了电子表格是平淡无奇还是精致报告。  

在本教程中，我们将通过一个完整、可运行的示例，向你展示 **how to center text** 在单元格内部、设置对齐方式并添加细边框——仅需几行 C# 代码。结束时，你将清楚每一步的意义，并能根据自己的场景进行调整。

## 您将收获的内容

- 对使用 Aspose.Cells（或任何类似库）进行 **create cell style** 工作流有清晰的了解。  
- 可以直接复制粘贴到控制台应用程序中的完整代码，用于 **apply style to cell**。  
- 深入了解 **center text in cell**、**set cell alignment**，以及处理合并单元格或自定义数字格式等边缘情况。  
- 扩展样式的技巧——不同字体、背景颜色或条件格式化。

> **先决条件：** Visual Studio 2022（或任意 C# IDE）以及 Aspose.Cells for .NET NuGet 包。无需其他依赖。

---

## 步骤 1：设置项目并导入命名空间

在我们能够 **create cell style** 之前，需要一个引用 Excel 库的项目。

```csharp
// Program.cs – entry point
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

class Program
{
    static void Main()
    {
        // We'll fill in the rest of the steps here.
    }
}
```

*为什么这很重要：* 导入 `Aspose.Cells` 让我们可以使用 `Workbook`、`Worksheet`、`Style` 和 `Border` 类。如果使用其他库（例如 EPPlus），类名会有所不同，但概念保持不变。

---

## 步骤 2：创建工作簿并获取第一个单元格

现在我们通过先获取要格式化的单元格引用来 **create cell style**。

```csharp
// Inside Main()
Workbook workbook = new Workbook();           // New, empty workbook
Worksheet ws = workbook.Worksheets[0];        // First worksheet (index 0)

// Step 1: Get a reference to the first cell (row 0, column 0) in the worksheet
Cell firstCell = ws.Cells[0, 0];               // A1 in Excel terms
firstCell.PutValue("Hello, styled world!");
```

请注意我们使用了 `Cell` 而不是通用的 `var`——显式类型让新手更易读。调用 `PutValue` 写入字符串，以便后续看到样式效果。

---

## 步骤 3：定义样式 – 居中文本，添加细边框

下面是 **create cell style** 操作的核心。我们将设置水平对齐、细边框以及一些可选的细节。

```csharp
// Step 2: Define a style that centers the text and adds a thin border
Style cellStyle = workbook.CreateStyle();          // Create a fresh Style object
cellStyle.HorizontalAlignment = TextAlignmentType.Center; // Center text horizontally
cellStyle.VerticalAlignment = TextAlignmentType.Center;   // Center vertically – often forgotten
cellStyle.Borders[BorderType.TopBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.LeftBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.RightBorder].LineStyle = CellBorderType.Thin;

// Optional: set a light gray background to make the border pop
cellStyle.ForegroundColor = System.Drawing.Color.LightGray;
cellStyle.Pattern = BackgroundType.Solid;
```

*我们这样做的原因：*  
- **HorizontalAlignment** 与 **VerticalAlignment** 共同回答了 “**how to center text** in a cell?” 的问题。  
- 添加四条边框确保单元格看起来像一个盒式标签，这对标题非常有用。  
- 背景颜色不是必需的，但它演示了后续如何扩展样式。

---

## 步骤 4：将定义好的样式应用到选定单元格

样式已经创建好后，我们只需一次方法调用即可 **apply style to cell**。

```csharp
// Step 3: Apply the defined style to the selected cell
firstCell.SetStyle(cellStyle);
```

就这么简单——Aspose.Cells 会把样式复制到单元格的内部样式集合中。如果需要对一段范围使用相同的格式，可以使用 `ws.Cells.CreateRange("A1:D1").ApplyStyle(cellStyle, new StyleFlag { All = true });`。

---

## 步骤 5：保存工作簿并验证结果

快速保存后即可在 Excel 中打开文件，确认文本已真正居中且边框出现。

```csharp
// Save the workbook to disk
string outputPath = "StyledCell.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
```

*预期输出：* 当你打开 **StyledCell.xlsx** 时，单元格 **A1** 包含 “Hello, styled world!” 并在水平和垂直方向上居中，四周有细灰色边框，背景为浅灰色。

---

## 常见变体与边缘情况

### 1. 在合并区域中居中文本

如果合并单元格 **A1:C1** 并仍希望文本居中，需要在合并后对左上角单元格 **apply style to cell**：

```csharp
ws.Cells.Merge(0, 0, 1, 3); // Merge A1:C1
firstCell.SetStyle(cellStyle); // Style still works because it’s applied to the anchor cell
```

### 2. 使用数值格式

有时需要 **set cell alignment** 的同时以特定格式显示数字：

```csharp
cellStyle.Custom = "#,##0.00"; // Two decimal places
firstCell.PutValue(12345.678);
firstCell.SetStyle(cellStyle);
```

对齐仍保持居中，而数字显示为 `12,345.68`。

### 3. 高效复用样式

为每个单元格创建新 `Style` 会影响性能。相反，创建一个样式对象并在多个单元格或范围间复用。`StyleFlag` 类允许只应用你关心的部分，从而节省内存。

```csharp
StyleFlag flag = new StyleFlag { HorizontalAlignment = true, Borders = true };
ws.Cells.CreateRange("B2:B10").ApplyStyle(cellStyle, flag);
```

---

## 实用技巧与常见坑点

- **别忘了垂直对齐**——仅水平居中在行高较大时会显得不自然。  
- **边框类型**：`CellBorderType.Thin` 适用于大多数报表，但你可以切换为 `Medium` 或 `Dashed` 来实现视觉层次。  
- **颜色处理**：在 .NET Core 环境下，使用 `System.Drawing.Color` 需要引用 `System.Drawing.Common` 包，否则会出现运行时错误。  
- **保存格式**：如果需要兼容旧版 Excel，将 `SaveFormat.Xlsx` 改为 `SaveFormat.Xls`。

---

![创建单元格样式示例](https://example.com/images/create-cell-style.png "在 C# 中创建单元格样式")

*Alt text: 截图显示一个通过创建单元格样式教程生成的、文本居中且带细边框的单元格。*

---

## 完整可运行示例（复制‑粘贴即可）

```csharp
using System;
using Aspose.Cells;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Grab the first cell and put a sample value
        Cell firstCell = ws.Cells[0, 0];
        firstCell.PutValue("Hello, styled world!");

        // 3️⃣ Create the style: center text, thin border, light gray background
        Style cellStyle = workbook.CreateStyle();
        cellStyle.HorizontalAlignment = TextAlignmentType.Center;
        cellStyle.VerticalAlignment   = TextAlignmentType.Center;
        cellStyle.Borders[BorderType.TopBorder].LineStyle    = CellBorderType.Thin;
        cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
        cellStyle.Borders[BorderType.LeftBorder].LineStyle   = CellBorderType.Thin;
        cellStyle.Borders[BorderType.RightBorder].LineStyle  = CellBorderType.Thin;
        cellStyle.ForegroundColor = Color.LightGray;
        cellStyle.Pattern = BackgroundType.Solid;

        // 4️⃣ Apply the style to the cell
        firstCell.SetStyle(cellStyle);

        // 5️⃣ Save the result
        string outputPath = "StyledCell.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
    }
}
```

运行此程序，打开 **StyledCell.xlsx**，即可看到前文描述的确切效果。随意更改文本、边框样式或背景颜色，以匹配你的品牌需求。

---

## 结论

我们已经从零 **created cell style**，**applied style to cell**，并演示了如何 **how to center text** 在水平和垂直方向上居中。掌握这些基础块后，你可以格式化标题、突出合计，甚至构建完整的报告模板，而无需离开 C#。  

如果你想进一步探索，可以尝试：

- **将相同样式应用于整行**（`ws.Cells.CreateRange("A2:E2").ApplyStyle(cellStyle, new StyleFlag { All = true });`）。  
- **添加条件格式**，根据单元格值动态更改背景。  
- **导出为 PDF**，同时保留样式。

记住，样式不仅关乎美观，更关系可读性。多实验、不断迭代，你的电子表格很快就会和代码一样专业。

*编码愉快！*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}