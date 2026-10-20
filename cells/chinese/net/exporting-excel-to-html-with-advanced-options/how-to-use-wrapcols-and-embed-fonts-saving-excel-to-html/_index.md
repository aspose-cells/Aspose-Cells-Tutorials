---
category: general
date: 2026-10-20
description: 学习如何在 Aspose.Cells 中使用 wrapcols、在 HTML 中嵌入字体，并使用完整的 C# 示例将 Excel 保存为
  HTML。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- embed fonts in html
- save excel as html
- convert workbook to html
- use wrapcols function
language: zh
lastmod: 2026-10-20
og_description: 如何在 Aspose.Cells 中使用 wrapcols、在 HTML 中嵌入字体，并通过清晰的 C# 步骤将工作簿转换为 HTML，适用于开发者。
og_image_alt: Screenshot of an Excel workbook saved as HTML with embedded fonts using
  Aspose.Cells
og_title: 如何在将 Excel 导出为 HTML 时使用 wrapcols 并嵌入字体
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to use wrapcols in Aspose.Cells, embed fonts in HTML, and
    save Excel as HTML with a complete C# example.
  headline: How to use wrapcols and embed fonts saving Excel to HTML
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel to HTML
- Smart Markers
title: 如何在将 Excel 保存为 HTML 时使用 wrapcols 并嵌入字体
url: /zh/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 wrapcols 并在保存 Excel 为 HTML 时嵌入字体

如果您需要在 Aspose.Cells 公式中 **how to use wrapcols**，本指南将为您展示具体步骤。您还将学习如何 **在 HTML 中嵌入字体** 并 **将 Excel 保存为 HTML**，以确保在各浏览器中的输出保持一致。  

本教程涵盖三个实用场景：使用 `WRAPCOLS` 函数、导出带嵌入字体的工作簿，以及使用 Smart Markers 生成主从报表。完成后，您将拥有一个完整的可运行 C# 程序，演示所有这些功能。

## Prerequisites

Before you start, make sure you have:

* .NET 6.0（或更高）已安装。
* 已在项目中添加 Aspose.Cells for .NET（`dotnet add package Aspose.Cells`）。
* 对 C# 和 Excel 公式有基本了解。

No additional third‑party libraries are required; Aspose.Cells handles HTML conversion and font embedding internally.

## 步骤 1：演示公式中 **how to use wrapcols** 函数的使用

The `WRAPCOLS` function splits a one‑dimensional range into a two‑dimensional array, filling columns first. This is useful when you need to reshape data for reporting or charting.

```csharp
using Aspose.Cells;
using System;

class WrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Populate a vertical range A1:A3
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // Apply WRAPCOLS(A1:A3, 2) – this creates a 2‑column array {1,2}
        sheet.Cells["B1"].Formula = "=WRAPCOLS(A1:A3, 2)";

        // Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // Output the result to verify the function works
        Console.WriteLine("Result of WRAPCOLS: " + sheet.Cells["B1"].Value);
        // Expected output: Result of WRAPCOLS: 1
    }
}
```

**为什么这样有效：**  
`WRAPCOLS` 接受两个参数——源范围和列数。函数按列方式填充数组，丢弃多余的值（示例中的 `3`）。结果显示在目标范围左上角的单元格 (`B1`) 中，如需完整数组可手动扩展范围。

> **技巧提示：** 设置公式后，调用 `workbook.CalculateFormula()` 以确保在读取单元格值之前结果是最新的。

## 步骤 2：**将工作簿转换为 HTML** 并 **在 html 中嵌入字体**

When you export an Excel file to HTML, fonts are often substituted by the browser’s defaults, which can break the visual layout. Aspose.Cells lets you embed the exact fonts used in the workbook directly into the HTML file.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for HtmlSaveOptions
using System;

class HtmlExportDemo
{
    static void Main()
    {
        // Re‑use the workbook from the previous step
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue("Hello");
        sheet.Cells["A2"].PutValue("World");

        // Configure HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Embedding fonts ensures the output looks the same on any device
            EmbedFonts = true,
            // Optional: specify a folder for supporting files (images, CSS)
            ExportEmbeddedImages = true
        };

        // Save the workbook as an HTML file with embedded fonts
        string outputPath = @"C:\Temp\WorkbookWithFonts.html";
        workbook.Save(outputPath, htmlOptions);

        Console.WriteLine($"Workbook saved to HTML with embedded fonts at: {outputPath}");
    }
}
```

**为什么嵌入字体很重要：**  
When `EmbedFonts` is `true`, Aspose.Cells converts each used TrueType/OpenType font into a Base64‑encoded `@font-face` rule inside the generated HTML. This eliminates the need for the client machine to have the same fonts installed, guaranteeing pixel‑perfect rendering.

> **特殊情况：** 如果源工作簿引用的字体未在服务器上安装，Aspose.Cells 将回退到默认字体并发出警告。请确保所需字体已可用。

## 接下来您应该学习什么？

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [如何在 C# 中使用 WRAPCOLS – 使用 Wrap 函数创建 Excel 工作簿](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [如何在 HTML 中嵌入字体 – 使用 C# 将 Excel 转换为 HTML](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/)
- [如何使用 Aspose.Cells for .NET 将 Excel 文件转换为 HTML：隐藏叠加内容](/cells/english/net/workbook-operations/excel-to-html-hide-overlaid-content-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}