---
category: general
date: 2026-06-05
description: 快速使用 C# 创建 Excel 工作簿，并学习如何设置单元格数字格式、导出 Excel 单元格以及将单元格值转换为保留两位小数的字符串。
draft: false
keywords:
- create excel workbook
- set cell number format
- format number with two decimals
- how to export excel cell
- convert cell value to string
language: zh
og_description: 在 C# 中创建 Excel 工作簿，掌握设置单元格数字格式、将 Excel 单元格导出为字符串以及将数字格式化为两位小数。
og_title: 在 C# 中创建 Excel 工作簿 – 完整的逐步指南
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  headline: Create Excel Workbook in C# – Complete Programming Guide
  type: TechArticle
- description: Create Excel workbook in C# quickly and learn how to set cell number
    format, export Excel cell, and convert cell value to string with two‑decimal precision.
  name: Create Excel Workbook in C# – Complete Programming Guide
  steps:
  - name: What if the cell already has a style?
    text: The `GetStyle` method returns a copy of the existing style, so any previous
      formatting (font, color, etc.) is retained. You only overwrite the `Custom`
      property, leaving everything else untouched.
  - name: How does culture affect the decimal separator?
    text: 'Aspose.Cells respects the thread’s `CultureInfo`. If you need a comma instead
      of a dot, set:'
  - name: Can I export a range of cells at once?
    text: Yes—use `Worksheet.ExportDataTable` or `Worksheet.ExportString` with a range
      address. The `ExportTableOptions` you defined for a single cell can be reused
      for the whole range.
  - name: What if I don’t want the value rounded but truncated?
    text: 'Change the custom format to `"0.00"` with a rounding mode, or manually
      truncate before putting the value:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: 在 C# 中创建 Excel 工作簿 – 完整编程指南
url: /zh/net/excel-workbook/create-excel-workbook-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中创建 Excel 工作簿 – 完整编程指南

有没有想过如何在 C# 中 **create Excel workbook** 而不必与 COM interop 或混乱的 CSV 技巧斗争？你并不孤单。许多开发者需要一种干净的、.NET 原生的方式来生成 .xlsx 文件，将数字写入单元格，然后将该值导出为格式良好的字符串。

在本教程中，我们将逐步演示——从空工作簿开始，设置单元格数字格式，将数字格式化为两位小数，最后学习 **how to export Excel cell** 数据为字符串。结束时，你还会看到如何 **convert cell value to string** 而不丢失精度。

> **Pro tip:** 以下方法使用 **Aspose.Cells for .NET** 库，这是经过实战检验的商业级 API。如果你在寻找免费替代方案，EPPlus 或 ClosedXML 也有类似功能，但代码片段会略有不同。

## 前置条件

- 已安装 .NET 6.0 SDK（或任何近期的 .NET 版本）。
- 已安装 Visual Studio 2022 或带有 C# 扩展的 VS Code。
- **Aspose.Cells** NuGet 包 (`Install-Package Aspose.Cells`)。

不需要其他依赖——其余全部包含在库中。

## 第一步：安装 Aspose.Cells 并设置项目

打开终端（或包管理器控制台）并运行：

```powershell
dotnet new console -n ExcelDemo
cd ExcelDemo
dotnet add package Aspose.Cells
```

这将创建一个名为 `ExcelDemo` 的全新控制台应用，并引入 `Aspose.Cells` 程序集。

此步骤重要的原因：如果没有该库，你将无法 **create Excel workbook** 对象或以类型安全的方式操作单元格。

## 第二步：创建工作簿并获取第一个工作表

现在打开 `Program.cs`，将默认代码替换为下面的代码片段。它展示了在 **create Excel workbook** 时的第一步——实例化 `Workbook` 类并获取默认工作表的引用。

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates a new .xlsx in memory
        Worksheet ws = workbook.Worksheets[0];           // first (default) sheet

        // The rest of the steps will follow here...
```

**Why?** `Workbook` 对象是 Excel 文件的内存表示。默认情况下它包含一个工作表，我们通过零基索引访问它。

## 第三步：向特定单元格写入数值

让我们定位到第 5 行、第 2 列（零基索引），并插入一个小数。这将在后面演示 **format number with two decimals**。

```csharp
        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];          // corresponds to cell C6 in Excel UI
        cell.PutValue(12345.6789);          // raw value with many decimal places
```

`PutValue` 方法存储原始的 double 值。此时，Excel 会显示完整精度，除非我们应用格式。

## 第四步：设置单元格数字格式（两位小数）

这里我们 **set cell number format**。我们将使用 `Style` 对象定义自定义数字格式 `"0.00"`——恰好两位小数。

```csharp
        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();               // clone existing style
        style.Custom = "0.00";                       // forces two digits after the dot
        cell.SetStyle(style);                        // apply the style back to the cell
```

为什么使用样式而不是字符串转换？保持单元格为数值类型可以保留其可计算性（仍可求和、平均等），同时显示你需要的格式。

## 第五步：将单元格值导出为格式化字符串

有时你需要将 **how to export excel cell** 值导出为纯文本——比如写入日志文件或通过 Web API 发送。Aspose.Cells 允许你为单元格附加导出选项，指示库使用相同的数字格式将值渲染为字符串。

```csharp
        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // forces string output
            NumberFormat = "0.00"           // matches the style we set earlier
        };
        cell.ExportOptions = exportOptions; // attach options to the cell
```

## 第六步：获取格式化字符串（Convert Cell Value to String）

让我们实际执行导出并查看结果。`ExportString` 方法返回单元格内容的字符串形式，并应用我们附加的任何 `ExportTableOptions`。

```csharp
        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");
```

当你运行程序时，控制台会打印：

```
Formatted cell value: 12345.68
```

请注意 `12345.6789` 被四舍五入为 `12345.68`——这就是 **format number with two decimals** 的效果。

## 第七步：（可选）将工作簿保存到磁盘

如果你也想看到实际 `.xlsx` 文件中的结果，只需调用 `Save`：

```csharp
        // Optional: write the workbook to a file so you can open it in Excel
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

打开 `DemoWorkbook.xlsx` 可以看到单元格 **C6** 中的相同数字，已格式化为两位小数。

## 边缘情况与常见问题

### 如果单元格已经有样式怎么办？

`GetStyle` 方法返回现有样式的副本，因此之前的格式（字体、颜色等）会被保留。你只会覆盖 `Custom` 属性，其他保持不变。

### 文化设置如何影响小数分隔符？

Aspose.Cells 尊重线程的 `CultureInfo`。如果需要逗号而不是点，请设置：

```csharp
System.Threading.Thread.CurrentThread.CurrentCulture = new System.Globalization.CultureInfo("fr-FR");
```

相同的 `"0.00"` 格式现在会渲染为 `12 345,68`。

### 能一次导出一整块单元格吗？

可以——使用 `Worksheet.ExportDataTable` 或 `Worksheet.ExportString` 并指定范围地址。你为单个单元格定义的 `ExportTableOptions` 可以在整个范围内复用。

### 如果我不想四舍五入而是截断该值怎么办？

更改自定义格式为带有截断模式的 `"0.00"`，或在写入值之前手动截断：

```csharp
double raw = Math.Truncate(12345.6789 * 100) / 100; // yields 12345.67
cell.PutValue(raw);
```

## 完整工作示例（可直接复制粘贴）

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create a workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Step 3: Access the cell at row 5, column 2 (zero‑based) and insert a number
        Cell cell = ws.Cells[5, 2];
        cell.PutValue(12345.6789);

        // Step 4: Apply a number format to show only two decimal places
        Style style = cell.GetStyle();
        style.Custom = "0.00";
        cell.SetStyle(style);

        // Step 5: Configure export options to get the formatted string
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "0.00"
        };
        cell.ExportOptions = exportOptions;

        // Step 6: Export the cell as a formatted string
        string formattedValue = cell.ExportString();
        Console.WriteLine($"Formatted cell value: {formattedValue}");

        // Optional: save the workbook for visual verification
        workbook.Save("DemoWorkbook.xlsx");
    }
}
```

**预期的控制台输出**

```
Formatted cell value: 12345.68
```

打开 `DemoWorkbook.xlsx` → 定位到单元格 **C6** → 你会看到相同的数字，带有两位小数。

## 结论

我们已经覆盖了在 C# 中 **create Excel workbook**、**set cell number format**、**format number with two decimals**、了解 **how to export Excel cell** 数据以及 **convert cell value to string** 以供后续处理所需的全部内容。

关键要点如下：

1. 使用 `Workbook` 和 `Worksheet` 在内存中创建 Excel 文件。  
2. 应用自定义样式 (`"0.00"`) 以强制显示两位小数。  
3. 当需要遵循相同格式的字符串表示时，将 `ExportTableOptions` 附加到单元格。  

从这里你可以继续实验——添加更多单元格、应用条件格式，甚至生成图表。如果你对字体样式或添加公式感兴趣，请查阅 Aspose.Cells 文档中的 **cell styling** 和 **formula evaluation**。

对 C# 中的 Excel 自动化还有其他问题吗？留下评论吧，祝编码愉快！

## 接下来你应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题。每个资源都包含完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能，并在项目中探索替代实现方式。

- [Master Workbook Operations in Aspose.Cells .NET&#58; Load Excel Files and Trace Cell Precedents Effectively](/cells/english/net/workbook-operations/aspose-cells-net-master-workbook-operations/)
- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Master Aspose.Cells for .NET&#58; Advanced Excel Workbook and Cell Management](/cells/english/net/advanced-features/excel-aspose-cells-net-create-manage/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}