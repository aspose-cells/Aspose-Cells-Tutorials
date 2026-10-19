---
category: general
date: 2026-09-18
description: 如何在 Excel 工作簿中换行单元格并将其保存为 PowerPoint 文件。学习使用 WRAPCOLS、创建工作簿工作表以及导出为 PPTX。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to wrap cells
- convert excel to powerpoint
- save excel as powerpoint
- how to use wrapcols
- create workbook worksheet
language: zh
lastmod: 2026-09-18
og_description: 如何在 Excel 中换行单元格并使用 C# 将工作簿导出为可编辑的 PowerPoint 文件。请按照分步指南，掌握 WRAPCOLS
  与工作表的创建。
og_image_alt: Diagram showing how to wrap cells in Excel before exporting to PowerPoint
og_title: 如何在 C# 中换行单元格并将 Excel 转换为 PowerPoint
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: How to wrap cells in an Excel workbook and save it as a PowerPoint
    file. Learn to use WRAPCOLS, create workbook worksheet, and export to PPTX.
  headline: How to wrap cells and convert Excel to PowerPoint in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: 如何在 C# 中对单元格进行自动换行并将 Excel 转换为 PowerPoint
url: /zh/net/converting-excel-files-to-other-formats/how-to-wrap-cells-and-convert-excel-to-powerpoint-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中换行单元格并将 Excel 转换为 PowerPoint

如果你需要 **如何换行单元格** 并将该工作表转换为 PowerPoint 演示文稿，本指南提供了一个完整、可直接运行的解决方案。阅读前两句话后，你将明确哪些 API 调用实现换行，哪个方法将文件保存为 PPTX。

我们将使用 Aspose.Cells for .NET，这个库无需安装 Microsoft Office 即可操作 Excel 工作簿。教程涵盖 **将 Excel 转换为 PowerPoint**，演示 **如何使用 WRAPCOLS**，并解释 **创建工作簿工作表** 的最佳实践。无需任何外部工具——只需一个 .NET 开发环境。

## 前置条件

- .NET 6.0 或更高（代码同样适用于 .NET Framework 4.6+）
- Aspose.Cells for .NET NuGet 包（`Install-Package Aspose.Cells`）
- 对 C# 和工作表概念有基本了解
- Visual Studio、VS Code 等 IDE 任意一种

> **专业提示：** 在实验阶段使用 Aspose.Cells 的免费评估许可证；在正式上线前替换为正式许可证。

## 第一步：创建工作簿并添加工作表

首先必须 **创建工作簿工作表**，即实例化一个 `Workbook` 对象。默认情况下 Aspose.Cells 会创建一个工作表（索引 0），我们将在演示中使用它。

```csharp
using System;
using Aspose.Cells;

class WrapAndExport
{
    static void Main()
    {
        // Step 1: Initialize a new workbook (creates one worksheet automatically)
        Workbook workbook = new Workbook();

        // Reference the first worksheet for later operations
        Worksheet ws = workbook.Worksheets[0];
```

**为什么重要：** 初始化工作簿为你提供了一块干净的画布。默认工作表已经是 `Worksheets` 集合的一部分，除非需要额外的工作表，否则无需调用 `Add()`。

## 第二步：填充源范围 (A2:A10)

在我们能够 **如何换行单元格** 之前，需要一些待换行的数据。本步骤将在 A2 到 A10 单元格中填入示例文本。

```csharp
        // Fill cells A2:A10 with a long string to demonstrate wrapping
        for (int i = 2; i <= 10; i++)
        {
            ws.Cells[$"A{i}"].PutValue(
                "Lorem ipsum dolor sit amet, consectetur adipiscing elit. " +
                "Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");
        }
```

**边缘情况：** 如果源范围为空，`WRAPCOLS` 会返回 `#VALUE!`。请确保范围内至少有一个非空单元格。

## 第三步：应用 WRAPCOLS 公式

现在回答核心问题 **如何使用 WRAPCOLS**。该公式接受一个垂直范围，并将其按指定列数展开。我们将公式写入单元格 `A1`；生成的数组会自动溢出到相邻单元格。

```csharp
        // Step 3: Apply WRAPCOLS to wrap A2:A10 into 3 columns, result starts at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";
```

**内部原理：** `WRAPCOLS` 评估源范围，将项目尽可能均匀地分配到目标列中，并将值写入一个矩形块。块的大小是动态的，无需预先定义目标范围。

## 第四步：将工作簿保存为可编辑的 PowerPoint 文件

最后，我们处理 **将 Excel 转换为 PowerPoint** 与 **将 Excel 保存为 PowerPoint**。Aspose.Cells 可以直接将工作表导出为 PPTX，保持布局为可编辑的形状。

```csharp
        // Step 4: Export the worksheet to an editable PPTX presentation
        string outputPath = @"YOUR_DIRECTORY\ChartEditable.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Workbook exported successfully to {outputPath}");
    }
}
```

**为什么选择 PPTX？** 生成的 PowerPoint 包含一张幻灯片，换行后的单元格以表格形式呈现。你可以在 Microsoft PowerPoint 中打开文件，编辑文本、修改样式或添加更多幻灯片——所有内容均保持完全可编辑。

### 预期输出

- **Excel 端：** 单元格 `A1` 显示原始长字符串的 3 列数组，每列大致包含相同数量的行。
- **PowerPoint 端：** 打开 `ChartEditable.pptx` 时，会看到一张幻灯片，其中的表格与换行后的布局完全对应。该表格可以像原生 PowerPoint 对象一样被选中、调整大小或编辑。

## 常见变体及注意事项

| 场景 | 调整 |
|----------|------------|
| **换成更多列** | 更改 `WRAPCOLS` 的第二个参数，例如 `=WRAPCOLS(A2:A10,5)`。 |
| **换不同的范围** | 更新公式引用，例如 `=WRAPCOLS(B2:B15,2)`。 |
| **仅导出工作表的一部分** | 使用 `Worksheet.ExportDataTable` 提取 `DataTable`，随后使用 `Presentation` API 自定义 PPTX 创建。 |
| **大型工作表（> 10 000 行）** | 考虑将导出拆分为多张幻灯片，以避免性能瓶颈。 |

> **注意：** 当工作簿包含图表时，默认的 PPTX 导出会将工作表渲染为单张图片。使用 `WRAPCOLS` 可确保数据保持为表格，保持可编辑性。

## 完整源码，复制粘贴即用

```csharp
using System;
using Aspose.Cells;

class WrapAndExport
{
    static void Main()
    {
        // Create a new workbook (contains one default worksheet)
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Populate A2:A10 with sample long text
        for (int i = 2; i <= 10; i++)
        {
            ws.Cells[$"A{i}"].PutValue(
                "Lorem ipsum dolor sit amet, consectetur adipiscing elit. " +
                "Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");
        }

        // Apply WRAPCOLS to wrap the range into 3 columns, result starts at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";

        // Save as an editable PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\ChartEditable.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Workbook exported successfully to {outputPath}");
    }
}
```

将文件保存为 `Program.cs`，恢复 NuGet 包后运行：

```bash
dotnet run
```

你应该会在控制台看到确认导出的信息，PPTX 文件会出现在指定文件夹中。

## 结论

现在你已经掌握了 **如何换行单元格**、**如何使用 WRAPCOLS**，以及使用 Aspose.Cells **将 Excel 转换为 PowerPoint**（即 **将 Excel 保存为 PowerPoint**）的完整步骤。完整方案演示了 **创建工作簿工作表**、应用换行公式，并生成可编辑的 PPTX 文件，随时可进行演示微调。

### 后续步骤

- 在导出前探索其他 Excel 函数（如 `TRANSPOSE`、`FILTER`）。
- 使用循环将多个工作表合并为多张幻灯片的 PowerPoint 演示文稿。
- 在导出后通过集成 Aspose.Slides 添加自定义幻灯片标题或品牌标识。

欢迎尝试不同的列数、源范围，甚至在同一个 PPTX 中混合图表和表格。祝编码愉快！


## 接下来该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助你在项目中进一步掌握 API 功能并探索替代实现方式。

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [How to Wrap Text in Excel Using Aspose.Cells for .NET | Formatting Tutorial](/cells/english/net/formatting/wrap-text-excel-aspose-cells-net/)
- [Export Excel Workbook and Worksheet Properties to HTML Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-properties-to-html-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}