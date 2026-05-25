---
category: general
date: 2026-02-26
description: 将工作簿导出为嵌入字体的 PDF，并将图表导出到 PowerPoint（使用 C#）。学习如何复制数据透视表工作表并将工作簿保存为 PPTX。
draft: false
keywords:
- export workbook to pdf
- export charts to powerpoint
- copy pivot table worksheet
- embed fonts pdf export
- save workbook as pptx
language: zh
og_description: 将工作簿导出为嵌入字体的 PDF，并在 C# 中将图表导出至 PowerPoint。按照分步指南复制数据透视表并保存为 PPTX。
og_title: 将工作簿导出为 PDF – 完整 C# 指南
tags:
- Aspose.Cells
- Aspose.Slides
- C#
- Reporting
title: 将工作簿导出为 PDF – 完整 C# 指南
url: /zh/net/conversion-to-pdf/export-workbook-to-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将工作簿导出为 PDF – 完整 C# 指南

将工作簿导出为 PDF 是在需要向可能没有安装 Excel 的利益相关者共享报告时的常见需求。在本教程中，我们还将展示如何 **将图表导出到 PowerPoint**、复制 **数据透视表工作表**，以及嵌入字体，使 PDF 看起来与屏幕上的设计完全一致。  

是否曾经想过为什么有些 PDF 会失去原始布局，或者 PowerPoint 幻灯片会出现缺失的形状？答案通常在于导出过程中的选项缺失。阅读完本指南后，你将拥有一个可复用的 C# 方法，解决所有这些痛点——不再需要手动复制粘贴或调试导出设置。

## 你将学到的内容

- 如何创建工作簿、添加 Smart Marker 表达式并对其进行处理。  
- 如何 **复制数据透视表工作表** 而不破坏数据源。  
- 如何 **将图表、形状和文本框导出到 PowerPoint 演示文稿**，并保持可编辑。  
- 如何 **在 PDF 导出时嵌入标准字体**，确保在任何机器上渲染一致。  
- 如何 **使用 `save workbook as pptx` 方法** 将工作簿保存为 PPTX。  

所有这些都基于最新的 Aspose.Cells 和 Aspose.Slides .NET 库（撰写时版本为 23.11）。无需外部工具、后处理脚本——纯 C# 实现。

> **专业提示：** 如果你的项目已经在使用 Aspose，只需直接复制代码片段；否则，请先通过 NuGet 添加 `Aspose.Cells` 和 `Aspose.Slides` 包。

## 前置条件

- .NET 6.0 或更高（代码同样可以在 .NET Framework 4.7.2 上运行）。  
- Visual Studio 2022（或你喜欢的任何 IDE）。  
- 通过 NuGet 安装 Aspose.Cells .NET 和 Aspose.Slides .NET。  
- 对 C# 以及 Excel 概念（如 Smart Markers 和数据透视表）有基本了解。

---

![导出工作簿为 PDF 示意图](export-workbook-to-pdf.png "导出工作簿为 PDF 工作流，展示 PDF 和 PPTX 输出")

## 将工作簿导出为 PDF – 步骤实现

下面是完整、可直接运行的示例代码。它会创建工作簿、注入 Smart Marker 表达式、处理它们、复制数据透视表范围，最后分别保存为 PDF 和 PowerPoint 文件。

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides.Export;

namespace ReportExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Build the workbook and add Smart Markers
            // -------------------------------------------------
            var reportWorkbook = new Workbook();
            Worksheet dataSheet = reportWorkbook.Worksheets[0];

            // Header with a variable department name
            dataSheet.Cells["A1"].PutValue("Report for ${$dept=Department}");

            // Conditional text based on department
            dataSheet.Cells["A2"].PutValue("${if $dept == \"Sales\"}Sales Summary${else}Other Summary${/if}");

            // Table header for orders – this will be repeated for each order
            dataSheet.Cells["A5:D5"].PutValue("${Orders.Product}|${Orders.Quantity}|${Orders.Price}");

            // -------------------------------------------------
            // Step 2: Process Smart Markers and name the detail sheet
            // -------------------------------------------------
            reportWorkbook.SmartMarkerProcessor.Options.DetailSheetNewName = "Orders_${$dept}";
            reportWorkbook.SmartMarkerProcessor.Process();

            // -------------------------------------------------
            // Step 3: Copy the range that contains the pivot table
            // -------------------------------------------------
            // Assume the pivot table lives in A1:G30 on the original sheet
            Range sourceRange = dataSheet.Cells.CreateRange("A1", "G30");
            Worksheet copySheet = reportWorkbook.Worksheets.Add("Copy");
            sourceRange.Copy(copySheet.Cells["A1"]);   // Pivot table is duplicated intact

            // -------------------------------------------------
            // Step 4: Export to PowerPoint (keep charts, shapes, text boxes)
            // -------------------------------------------------
            var pptOptions = new PresentationOptions
            {
                ExportCharts = true,
                ExportShapes = true,
                ExportTextBoxes = true
            };
            string pptPath = @"C:\Temp\FinalPresentation.pptx";
            reportWorkbook.Save(pptPath, SaveFormat.Pptx, pptOptions);

            // -------------------------------------------------
            // Step 5: Export to PDF and embed standard fonts
            // -------------------------------------------------
            var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
            string pdfPath = @"C:\Temp\FinalReport.pdf";
            reportWorkbook.Save(pdfPath, pdfOptions);

            Console.WriteLine("Export completed:");
            Console.WriteLine($" • PDF saved to {pdfPath}");
            Console.WriteLine($" • PowerPoint saved to {pptPath}");
        }
    }
}
```

### 为什么这样可行

1. **Smart Marker 处理** 让你无需编写循环即可从任意数据源（JSON、DataTable 等）填充工作簿。  
2. **DetailSheetNewName** 为每个部门创建单独的工作表，得到干净的部门标签页。  
3. **复制范围** (`sourceRange.Copy`) 会连同缓存一起复制数据透视表，复制后的工作表行为与原始完全相同。  
4. **PresentationOptions** 中的 `ExportCharts`、`ExportShapes` 和 `ExportTextBoxes` 告诉 Aspose 将这些对象渲染为原生 PowerPoint 元素，保持可编辑性。  
5. **PdfSaveOptions.EmbedStandardFonts** 确保在没有原始字体的机器上 PDF 仍然保持一致外观。

最终会得到两个文件——`FinalReport.pdf` 和 `FinalPresentation.pptx`——可以通过电子邮件发送、归档或在任何查看器中打开而不失真。

## 将图表导出到 PowerPoint（将工作簿保存为 PPTX）

如果报告中包含图表，你可能希望它们在 PowerPoint 中保持可编辑。`PresentationOptions` 类是关键。下面的代码片段专注于图表导出部分：

```csharp
// Assuming reportWorkbook already contains charts
var pptExportOptions = new PresentationOptions
{
    ExportCharts = true,      // Convert Excel charts to PowerPoint chart objects
    ExportShapes = false,    // Skip shapes if you don’t need them
    ExportTextBoxes = true   // Keep any text boxes editable
};

string pptFile = @"C:\Temp\ChartsOnly.pptx";
reportWorkbook.Save(pptFile, SaveFormat.Pptx, pptExportOptions);
```

**内部是如何工作的？** Aspose 会把每个 Excel 图表转换为原生 PowerPoint 图表，保留系列、坐标轴标题和格式。这远比将图表导出为静态图片要好，因为观众以后可以直接在 PowerPoint 中调整数据点。

## 复制数据透视表工作表而不丢失数据

数据透视表是导出时最棘手的部分，因为它依赖隐藏的缓存。简单的 `Copy` 方法之所以有效，是因为 Aspose 同时复制了可见范围 **以及** 底层缓存对象。

```csharp
// Copy the whole sheet (including pivot table) to a new workbook
Workbook clone = new Workbook();
reportWorkbook.Worksheets[0].CopyTo(clone.Worksheets[0]);
clone.Save(@"C:\Temp\PivotCopy.xlsx", SaveFormat.Xlsx);
```

> **注意：** 如果你只需要在同一工作簿内的新工作表上保留数据透视表，前面的 `sourceRange.Copy` 方法更轻量，且无需创建全新的工作簿。

## 为 PDF 导出嵌入字体 – 为什么重要

在没有原始字体的机器上打开 PDF 时，文字可能会位移、换行改变，甚至字符消失。将 `EmbedStandardFonts = true` 设置为 true，告诉 Aspose 将最常用的字体（Arial、Times New Roman 等）直接嵌入 PDF 流中。

如果使用自定义字体，请改为 `PdfSaveOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedAll`。示例代码如下：

```csharp
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    FontEmbeddingMode = FontEmbeddingMode.EmbedAll   // For custom fonts
};
reportWorkbook.Save(@"C:\Temp\CustomFontReport.pdf", pdfOpts);
```

现在每位收件人看到的布局都与你设计的一模一样——没有意外。

## 完整示例回顾

将所有内容组合在一起，完整程序（前文已展示）实现以下步骤：

1. **创建** 包含 Smart Marker 占位符的工作簿。  
2. **处理** 标记，生成以部门命名的明细工作表。  
3. **复制** 包含数据透视表的范围到新工作表，保留其功能。  
4. **导出** 工作簿为 PowerPoint，保持图表、形状和文本框可编辑。  
5. **导出** 同一工作簿为 PDF，同时嵌入标准字体以确保可靠渲染。

运行程序，打开生成的文件，你会看到：

- **PDF**：表格清晰、嵌入字体、视觉风格与 Excel 源文件完全一致。  
- **PowerPoint**：可编辑的图表，可在 PowerPoint 中右键 → *Edit Data*，以及保持完全可操作的形状。

---

## 常见问题解答 (FAQ)

**问：这在 .NET Core 上能工作吗？**  
答：能——Aspose.Cells 和 Aspose.Slides 是跨平台的。只要目标为 .NET 6 或更高，代码即可在 Windows、Linux 或 macOS 上运行。

**问：如果只想导出部分工作表怎么办？**  
答：使用 `Workbook.Save` 并配合 `SaveOptions` 指定 `SheetNames`。示例：`new PresentationOptions { SheetNames = new[] { "Copy" } }`。

**问：可以对 PDF 加密吗？**  
答：完全可以。在调用 `Save` 之前设置 `PdfSaveOptions.EncryptionDetails` 并提供密码。

**问：我的数据透视表使用外部数据源——复制会破坏链接吗？**  
答：复制操作会包含缓存，而不是外部连接。数据透视表仍可离线使用，但不会对原始源进行刷新。如果需要实时刷新，请将源数据一起导出。

---

## 后续步骤与相关主题

- **动态数据源** – 学习如何将 JSON 或 DataTable 注入 Smart Markers，实现实时报告。  
- **高级 PDF 样式** – 探索 `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}