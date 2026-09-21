---
category: general
date: 2026-09-21
description: 使用 Aspose.Cells 将 Excel 导出为 PowerPoint 并保持图表可编辑。请按照本分步指南将工作表转换为 PPTX，同时保持图表可编辑。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- worksheet to powerpoint
- export excel chart pptx
- editable charts pptx
language: zh
lastmod: 2026-09-21
og_description: 使用 Aspose.Cells 将 Excel 导出为 PowerPoint，并保留可编辑的图表。了解如何将工作表转换为 PPTX，同时保持图表的完整可编辑性。
og_image_alt: Screenshot of a PowerPoint slide showing an editable Excel chart after
  export
og_title: 将 Excel 导出到 PowerPoint 并保留可编辑图表 – C# 教程
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  headline: Export Excel to PowerPoint with editable charts in C#
  type: TechArticle
- description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  name: Export Excel to PowerPoint with editable charts in C#
  steps:
  - name: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
    text: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
  - name: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
    text: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
  - name: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
    text: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
  - name: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
    text: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel‑to‑PowerPoint
- PPTX export
title: 使用 C# 将 Excel 导出到 PowerPoint，图表可编辑
url: /zh/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-editable-charts-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中将 Excel 导出为 PowerPoint 并保持图表可编辑

Export Excel to PowerPoint with editable charts 是在需要将电子表格可视化复用于演示文稿时的常见需求。本文档展示了如何使用 Aspose.Cells for .NET **export Excel to PowerPoint** 并保留图表的可编辑性。

您将学习：

* 加载包含图表和文本框的现有工作簿。  
* 配置 PPTX 导出选项，使图表和形状保持可编辑。  
* 将特定工作表转换为 PowerPoint 文件，可在 Microsoft PowerPoint 中打开并编辑。

本教程假设您具备基本的 C# 知识，并使用最近的 .NET 版本（≥ .NET 6）。无需事先了解 Aspose.Cells。

---

## 导出 Excel 到 PowerPoint – 概述

**export Excel to PowerPoint** 的核心思路是将每个工作表视为可以渲染到 PPTX 幻灯片的图像源。通过切换 `ExportChartAsEditableText` 和 `ExportShapeAsEditableText` 标志，Aspose.Cells 将底层图表数据写入为 PowerPoint 绘图对象，而不是平面位图。这使得生成的幻灯片可以完全编辑——就像直接在 PowerPoint 中创建的图表一样。

> **为什么使用可编辑图表？**  
> 可编辑图表让演示者无需返回原始 Excel 文件即可调整数据、颜色或标签，加快临时修改的速度，保持演示工作流的流畅。

---

## 将工作表转换为 PowerPoint（worksheet to PowerPoint）

下面给出一个完整、可运行的示例，演示 **worksheet to PowerPoint** 转换。

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the chart and textbox
            // Replace YOUR_DIRECTORY with the actual folder path on your machine.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Configure PPTX export options to keep charts and shapes editable
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,               // Target format: PPTX
                ExportChartAsEditableText = true,           // Enable editable charts
                ExportShapeAsEditableText = true            // Enable editable shapes/textboxes
            };

            // Step 3: Export the first worksheet (index 0) to a PowerPoint file
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";
            workbook.Worksheets[0].ConvertToImage(exportOptions, outputPath);

            Console.WriteLine($"Worksheet successfully exported to {outputPath}");
        }
    }
}
```

### 每一步的说明

| 步骤 | 代码作用 | 为何对 **export excel chart pptx** 很重要 |
|------|----------|------------------------------------------|
| 1️⃣   | 将 `input.xlsx` 加载到 `Aspose.Cells.Workbook` 对象中。 | 工作簿提供了对要导出的图表的访问。 |
| 2️⃣   | 将 `ExportType` 设置为 `Pptx`，并启用 `ExportChartAsEditableText` 与 `ExportShapeAsEditableText`。 | 这些标志是 **editable charts pptx** 的关键——它们告诉库将图表几何信息写入为 PowerPoint 绘图对象，而不是光栅图像。 |
| 3️⃣   | 对第一个工作表调用 `ConvertToImage`，生成 `Worksheet.pptx`。 | 该方法执行 **export excel to powerpoint** 操作，并写入可直接在 PowerPoint 中打开的 PPTX 文件。 |

> **技巧提示：** 如果需要导出 *多个* 工作表，可遍历 `workbook.Worksheets` 并对每个工作表调用 `ConvertToImage`，可选地将输出文件命名为 `Sheet1.pptx`、`Sheet2.pptx` 等。

---

## 在 PPTX 中启用可编辑图表（export excel chart pptx）

当 `ExportChartAsEditableText` 设置为 `true` 时，Aspose.Cells 会将每个图表写入为 PPTX XML 中的 `<a:graphic>` 元素集合。PowerPoint 随后将这些元素视为原生图表对象，双击即可打开图表编辑器。

**常见陷阱**

* **缺少 Aspose.Cells 许可证** – 未授权时库会在输出中添加水印。请在程序早期注册许可证 (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`)。  
* **不受支持的图表类型** – 虽然大多数 2‑D 图表（柱形、折线、饼图）均可完全编辑，但某些复杂的 3‑D 或组合图表可能会回退为图像。若依赖完整可编辑性，请测试具体图表类型。  
* **大型工作表** – 导出非常大的工作表会消耗大量内存。考虑在 `ImageOrPrintOptions` 中使用 `ExportMaxRows` 或 `ExportMaxColumns` 限制要转换的区域。

---

## 保持图表可编辑的技巧（editable charts pptx）

1. **保留图表数据范围** – 确保图表的数据源位于正在导出的同一工作表中。跨工作表的引用会在 PPTX 中转换为静态值。  
2. **使用最新的 Aspose.Cells 版本** – 新版本提升了对更多图表特性的支持，并修复了与 PPTX 导出相关的边缘案例错误。  
3. **验证输出** – 转换后，在 PowerPoint 中打开生成的 PPTX，确认可以编辑图表标题、系列和坐标轴标签。如果某些元素显示为图像，请再次检查已启用 `ExportChartAsEditableText` 且图表类型受支持。  
4. **批量处理** – 对于自动化场景（例如从大量 Excel 报告生成幻灯片套件），将转换逻辑封装为接受 `Workbook`、`int worksheetIndex` 和 `string outputPath` 的方法。这样可以将 **export excel to powerpoint** 工作流隔离并复用。

---

## 完整示例回顾

将所有内容组合在一起，下面是可以直接复制粘贴到新 .NET 控制台项目中的最小程序：

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Register license (optional but removes evaluation watermark)
            // var license = new License();
            // license.SetLicense("Aspose.Cells.lic");

            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";

            Workbook workbook = new Workbook(inputPath);

            ImageOrPrintOptions options = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,
                ExportChartAsEditableText = true,
                ExportShapeAsEditableText = true
            };

            workbook.Worksheets[0].ConvertToImage(options, outputPath);

            Console.WriteLine($"Export complete: {outputPath}");
        }
    }
}
```

**预期结果**

* 在 `YOUR_DIRECTORY` 中生成名为 `Worksheet.pptx` 的文件。  
* 用 Microsoft PowerPoint 打开该文件时，会看到包含原始图表和所有文本框的幻灯片。  
* 双击图表即可打开 PowerPoint 的图表编辑器，能够更改系列值、颜色或坐标轴标题——验证 **editable charts pptx** 功能如预期工作。

---

## 结论

您现在拥有一个完整的 **export Excel to PowerPoint** 解决方案，能够保持图表可编辑。通过在 `ImageOrPrintOptions` 中配置 `ExportChartAsEditableText` 和 `ExportShapeAsEditableText`，转换过程会生成一个本机 PPTX 文件，图表的行为与直接在 PowerPoint 中创建的图表完全相同。  

接下来您可以：

* 将代码扩展为处理多个工作表（为每个工作表执行 **worksheet to PowerPoint**）。  
* 将导出与其他 Aspose.Cells 功能结合使用，例如添加幻灯片标题或插入图片。  
* 探索相关主题，如使用自定义主题的 **export Excel chart PPTX**，或自动化整个幻灯片生成流水线。

欢迎尝试不同的图表类型、添加数据标签，或将此工作流集成到更大的报表系统中。祝编码愉快！

## 接下来应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 的其他功能，并在项目中探索替代实现方式。每个资源都包含完整的可运行代码示例和逐步解释。

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}