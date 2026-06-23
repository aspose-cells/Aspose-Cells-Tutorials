---
category: general
date: 2026-05-30
description: 使用 C# 更改 Excel 文本框的字体大小。学习如何通过一步步的代码快速修改 Excel 文本框的字体。
draft: false
keywords:
- change textbox font size
- modify excel textbox font
language: zh
og_description: 使用 C# 更改 Excel 文本框字体大小。本指南展示了如何安全高效地修改 Excel 文本框字体。
og_title: 使用 C# 更改 Excel 文本框字体大小 – 完整教程
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  headline: Change Textbox Font Size in Excel with C# – Complete Guide
  type: TechArticle
- description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  name: Change Textbox Font Size in Excel with C# – Complete Guide
  steps:
  - name: Why this matters
    text: Opening the workbook via COM gives us a live object model—meaning any change
      we make reflects instantly in the file. Setting `Visible = false` speeds things
      up and avoids popping windows during automation.
  - name: Why we use `TextFrame2`
    text: '`TextFrame2` is the newer object model introduced with Office 2007. It
      supports advanced typographic features and is generally more reliable than the
      older `TextFrame`. Using it ensures our **change textbox font size** operation
      works across modern Excel versions.'
  - name: 1. Change *all* textboxes on a sheet
    text: '```csharp foreach (Excel.Shape s in xlWorksheet.Shapes) { if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
      { var tr = s.TextFrame2.TextRange; tr.Font.Name = fontName; tr.Font.Size = newSize;
      } } ```'
  - name: 2. Identify a textbox by its **Name** instead of index
    text: 'If you gave your textbox a meaningful name (e.g., “TitleBox”), you can
      fetch it directly:'
  type: HowTo
tags:
- Excel Interop
- C#
- Office Automation
title: 使用 C# 更改 Excel 文本框字体大小 – 完整指南
url: /zh/net/excel-shape-text-modifications/change-textbox-font-size-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中使用 C# 更改文本框字体大小 – 完整指南

需要在 C# 中 **更改 Excel 工作表的文本框字体大小** 吗？您来对地方了。无论是生成报告、构建仪表板，还是仅仅微调模板，调整文本框的外观都能让您的电子表格看起来更专业。

在本教程中，我们还将 **修改 Excel 文本框字体**，不仅限于大小——包括字体族、粗体以及处理多个形状。完成后，您将拥有一个可直接运行的代码片段，涵盖从打开工作簿到清理 COM 对象的整个过程。没有冗余，只提供您今天即可投入项目的实用代码。

## 前置条件 — 您需要的内容

| Requirement | 为什么重要 |
|-------------|------------|
| **.NET 6+** (or .NET Framework 4.7.2+) | 提供 C# 编译器和运行时。 |
| **Microsoft.Office.Interop.Excel** NuGet package | 提供与 Excel 通信所需的 COM 互操作类型。 |
| **Excel installed** (any recent version) | 只有在安装了 Office 应用时，Interop 层才能工作。 |
| **Basic C# knowledge** | 您可以轻松跟随，但我们会解释每一行代码。 |

如果缺少上述任何项，请立即暂停并进行安装；本指南的其余部分假设它们已就绪。

## 步骤 1：设置项目并导入命名空间

首先，创建一个新的控制台应用程序（或集成到现有项目），并引入 Interop 命名空间。

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll call the helper method that does the heavy lifting.
            ChangeTextboxFontSize(@"C:\Temp\Sample.xlsx", "Sheet1", 0, 14, "Calibri");
        }
    }
}
```

> **技巧提示：** 如果您面向 .NET 6+，请通过 `dotnet add package Microsoft.Office.Interop.Excel` 添加 `Microsoft.Office.Interop.Excel` 包。这可确保 `Excel` 别名正确解析。

## 步骤 2：打开工作簿并获取目标工作表

现在我们需要启动 Excel，打开文件，并定位到包含文本框的工作表。将其包装在 `try/finally` 块中，可确保即使出现错误也能释放 COM 对象。

```csharp
static void ChangeTextboxFontSize(string workbookPath,
                                  string sheetName,
                                  int textboxIndex,
                                  double newSize,
                                  string fontName)
{
    Excel.Application xlApp = null;
    Excel.Workbook xlWorkbook = null;
    Excel.Worksheet xlWorksheet = null;

    try
    {
        xlApp = new Excel.Application
        {
            // Keep Excel hidden; set to true if you want to watch the changes.
            Visible = false,
            DisplayAlerts = false
        };

        xlWorkbook = xlApp.Workbooks.Open(workbookPath);
        xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;
        if (xlWorksheet == null)
            throw new ArgumentException($"Worksheet '{sheetName}' not found.");
```

### 为什么这很重要

通过 COM 打开工作簿可获得实时对象模型——这意味着我们所做的任何更改都会立即反映在文件中。将 `Visible = false` 设置为隐藏，可加快速度并避免在自动化过程中弹出窗口。

## 步骤 3：获取文本框形状

Excel 将文本框视为 `Shapes` 集合下的 `Shape` 对象，而不是专用的 `TextBox` 集合。这就是下面的代码看起来与您在线上看到的示例略有不同的原因。

```csharp
        // Excel stores all drawing objects (including textboxes) in the Shapes collection.
        Excel.Shapes shapes = xlWorksheet.Shapes;

        // Guard against an out‑of‑range index.
        if (textboxIndex < 0 || textboxIndex >= shapes.Count)
            throw new IndexOutOfRangeException("Textbox index is out of range.");

        // Grab the specific shape; we assume it’s a textbox.
        Excel.Shape textboxShape = shapes.Item(textboxIndex + 1); // COM collections are 1‑based.
        if (!textboxShape.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
            throw new InvalidOperationException("Selected shape is not a textbox.");
```

> **注意：** `Shapes` 集合是基于 1 的，因此我们对您传入的零基 `textboxIndex` 加 `+1`。忘记此操作会导致 “索引超出范围” 错误，调试起来会很令人沮丧。

## 步骤 4：更改文本框字体大小（及名称）

这里我们终于 **更改文本框字体大小**。`TextFrame2` 属性让我们可以访问富文本格式选项，其中包括 `Font.Name` 和 `Font.Size`。

```csharp
        // Access the text range inside the textbox.
        Excel.TextRange2 textRange = textboxShape.TextFrame2.TextRange;

        // Change the font name – this also “modifies excel textbox font”.
        textRange.Font.Name = fontName;

        // Change the font size – the core of our tutorial.
        textRange.Font.Size = newSize;

        // Optional: make the text bold for extra emphasis.
        // textRange.Font.Bold = Microsoft.Office.Core.MsoTriState.msoTrue;
```

### 为什么使用 `TextFrame2`

`TextFrame2` 是自 Office 2007 起引入的新版对象模型。它支持高级排版功能，通常比旧的 `TextFrame` 更可靠。使用它可确保我们的 **更改文本框字体大小** 操作在现代 Excel 版本中均能正常工作。

## 步骤 5：保存、清理并验证

在调整字体后，我们需要保存更改并释放所有 COM 引用。跳过清理可能导致孤立的 Excel 进程在后台残留。

```csharp
        // Save the workbook – you can also use SaveAs to create a copy.
        xlWorkbook.Save();

        Console.WriteLine($"Successfully changed textbox font size to {newSize} pt and font to '{fontName}'.");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error: {ex.Message}");
    }
    finally
    {
        // Release COM objects in reverse order of creation.
        if (xlWorksheet != null) System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorksheet);
        if (xlWorkbook != null)
        {
            xlWorkbook.Close(false);
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorkbook);
        }
        if (xlApp != null)
        {
            xlApp.Quit();
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlApp);
        }

        // Force garbage collection to clean up any remaining RCWs.
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```

> **技巧提示：** 如果需要在多个工作表上 **修改 Excel 文本框字体**，请将内部逻辑包装在遍历 `Workbook.Worksheets` 的循环中。只需记得为每个工作表重置 `textboxIndex` 即可。

## 处理边缘情况 — 多个文本框和缺失形状

实际的电子表格很少只有一个文本框。下面提供两种快速策略，您可以在不重写整个方法的情况下采用。

### 1. 更改工作表上的 *所有* 文本框

```csharp
foreach (Excel.Shape s in xlWorksheet.Shapes)
{
    if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
    {
        var tr = s.TextFrame2.TextRange;
        tr.Font.Name = fontName;
        tr.Font.Size = newSize;
    }
}
```

### 2. 通过 **名称** 而非索引来识别文本框

如果您为文本框指定了有意义的名称（例如 “TitleBox”），可以直接获取它：

```csharp
Excel.Shape namedBox = xlWorksheet.Shapes.Item("TitleBox");
namedBox.TextFrame2.TextRange.Font.Size = newSize;
```

这两种方法都能让您 **修改 Excel 文本框字体**，精准且不受工作簿结构影响。

## 可视化概览（可选）

如果您更喜欢快速的视觉提示，请想象下面的示意图：

![在 Excel 中更改文本框字体大小 – 高亮的文本框已准备好进行字体修改](change-textbox-font-size.png)

## 完整工作示例

将所有内容整合在一起，这里提供一个单文件示例，您可以复制粘贴到控制台项目并立即运行（只需更新文件路径和工作表名称）。

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these parameters for your environment.
            string workbookPath = @"C:\Temp\Sample.xlsx";
            string sheetName = "Sheet1";
            int textboxIndex = 0;          // First textbox on the sheet.
            double newFontSize = 14;       // Desired font size.
            string newFontName = "Calibri";

            ChangeTextboxFontSize(workbookPath, sheetName, textboxIndex, newFontSize, newFontName);
        }

        static void ChangeTextboxFontSize(string workbookPath,
                                          string sheetName,
                                          int textboxIndex,
                                          double newSize,
                                          string fontName)
        {
            Excel.Application xlApp = null;
            Excel.Workbook xlWorkbook = null;
            Excel.Worksheet xlWorksheet = null;

            try
            {
                xlApp = new Excel.Application { Visible = false, DisplayAlerts = false };
                xlWorkbook = xlApp.Workbooks.Open(workbookPath);
                xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;

                if (xlWorksheet == null)


## 接下来您应该学习什么？

- [在 Excel 中更改字体大小](/cells/english/net/working-with-fonts-in-excel/changing-font-size/)
- [如何使用 Aspose.Cells .NET 自定义 Excel 单元格字体大小 | 完整指南](/cells/english/net/formatting/customize-font-size-excel-aspose-cells-dotnet/)
- [如何使用 Aspose.Cells for .NET 在 Excel 中设置字体样式（分步指南）](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}