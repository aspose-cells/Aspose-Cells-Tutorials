---
category: general
date: 2026-10-26
description: 学习如何使用 C# 将 Excel 图表导出到 PowerPoint。保持形状可编辑性，并用几行代码保存为 PPTX。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel charts to powerpoint
- Aspose.Cells export
- C# Excel to PowerPoint conversion
- preserve shape editability
- SaveFormat.Pptx
- Workbook.Save method
language: zh
lastmod: 2026-10-26
og_description: 使用 C# 将 Excel 图表导出到 PowerPoint。本指南展示如何保持形状可编辑，并使用 Aspose.Cells 保存为
  PPTX。
og_image_alt: Export Excel charts to PowerPoint example showing a chart transferred
  from Excel to a slide
og_title: 使用 C# 将 Excel 图表导出到 PowerPoint – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  headline: How to export Excel charts to PowerPoint using C#
  type: TechArticle
- description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  name: How to export Excel charts to PowerPoint using C#
  steps:
  - name: Load the Excel workbook
    text: '```csharp using Aspose.Cells;'
  - name: (Optional) Adjust workbook settings
    text: In most cases the default settings are sufficient for a clean export. However,
      if you need to change the calculation mode, page setup, or hide certain sheets,
      you can do it here.
  - name: Save the workbook as a PowerPoint file
    text: '```csharp // Export the workbook to PPTX while keeping chart shapes editable
      workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx); ```'
  - name: Verify the result
    text: 'Open `Shapes.pptx` in PowerPoint and:'
  - name: 'Edge case: Exporting multiple worksheets with separate charts'
    text: If your Excel file contains several worksheets, each with its own chart,
      Aspose.Cells creates a separate slide for each chart automatically. You can
      control slide order by rearranging worksheets before the save operation.
  - name: 'Performance tip: Stream the output instead of writing to disk'
    text: When generating PowerPoint files in a web API, avoid temporary files by
      writing to a `MemoryStream`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- PowerPoint
title: 如何使用 C# 将 Excel 图表导出到 PowerPoint
url: /zh/net/chart-rendering-and-conversion/how-to-export-excel-charts-to-powerpoint-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 C# 将 Excel 图表导出到 PowerPoint

如果您需要 **将 Excel 图表导出到 PowerPoint**，本指南将带您完成一个完整、可直接运行的解决方案。无论您是在构建报告仪表板还是自动化幻灯片，都可以看到几行 C# 代码如何在转换后保持图表形状的完全可编辑性。

在本教程中，您将学习如何：

* 加载包含图表的现有 Excel 工作簿。  
* （可选）在转换前微调工作簿设置。  
* 将工作簿保存为 PowerPoint 文件，同时保留形状的可编辑性。  

所有这些都使用 **Aspose.Cells for .NET** 完成，该库在服务器上无需 Microsoft Office 即可处理 Excel 到 PowerPoint 的转换。

## 您需要的条件

| 需求 | 原因 |
|------|------|
| .NET 6.0 或更高版本 | 现代运行时，具备完整的语言特性 |
| Visual Studio 2022（或任何 IDE） | 方便的编辑器和调试器 |
| **Aspose.Cells for .NET** NuGet 包 | 提供 `Workbook` 类和 `SaveFormat.Pptx` 支持 |
| 包含至少一个图表的 Excel 文件（`ChartAndShapes.xlsx`） | 您想要导出的图表来源 |

> **专业提示：** 使用免费的 **Aspose.Cells Evaluation** 版本来测试代码；许可证密钥可以去除评估水印。

```bash
dotnet add package Aspose.Cells
```

## 将 Excel 图表导出到 PowerPoint – 完整工作流

下面是实现导出并 **保留形状可编辑性** 的端到端代码。每一步都将详细说明。

### 步骤 1：加载 Excel 工作簿

```csharp
using Aspose.Cells;

// Load the workbook that holds the charts you want to export
Workbook workbook = new Workbook(@"C:\Projects\ChartAndShapes.xlsx");
```

*`Workbook` 类表示整个 Excel 文件。加载文件会将所有工作表、图表和形状读取到内存中，这是进行后续操作的前提。*

### 步骤 2：（可选）调整工作簿设置

在大多数情况下，默认设置已足以实现干净的导出。然而，如果需要更改计算模式、页面设置或隐藏某些工作表，可以在此进行操作。

```csharp
// Example: ensure all formulas are calculated before export
workbook.CalculateFormula();

// Example: hide a sheet that you don’t want in the PowerPoint
workbook.Worksheets["SecretData"].IsVisible = false;
```

> **为什么重要：** 在转换前调整设置可确保生成的幻灯片准确反映您想要的状态，尤其是当公式或隐藏的工作表可能影响图表数据时。

### 步骤 3：将工作簿保存为 PowerPoint 文件

```csharp
// Export the workbook to PPTX while keeping chart shapes editable
workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx);
```

*`SaveFormat.Pptx` 常量告诉 Aspose.Cells 写入 PowerPoint 演示文稿。库内部会将每个 Excel 图表转换为 PowerPoint 形状，且在 Microsoft PowerPoint 中保持完全可编辑。*

### 步骤 4：验证结果

在 PowerPoint 中打开 `Shapes.pptx`，并：

1. 选中任意幻灯片上的图表。  
2. 右键 → **Edit Data**。  
3. 确认图表数据表出现并且可以修改数值。

如果图表打开了 **Edit Data** 面板，则说明转换成功，且 **形状可编辑性** 已被保留。

![Export Excel charts to PowerPoint example](export-excel-charts-to-powerpoint.png){.img-fluid alt="导出 Excel 图表到 PowerPoint 示例"}

## 常见陷阱及避免方法

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| 图表显示为静态图像 | 使用不支持 PPTX 导出的旧版 Aspose.Cells | 升级到最新的 Aspose.Cells 23.x 或更高版本 |
| PowerPoint 图表中缺少数据 | 导出前工作簿未完全计算 | 在 `Save` 之前调用 `workbook.CalculateFormula()` |
| 形状不可编辑 | 使用 `SaveFormat.Xlsx` 而不是 `SaveFormat.Pptx` 保存 | 确保在 `Workbook.Save` 时传入 `SaveFormat.Pptx` |
| 运行时许可证异常 | 未注册许可证的评估版 | 使用 `License license = new License(); license.SetLicense("Aspose.Cells.lic");` 注册许可证 |

### 边缘情况：导出包含多个工作表的独立图表

如果您的 Excel 文件包含多个工作表，每个工作表都有自己的图表，Aspose.Cells 会自动为每个图表创建单独的幻灯片。您可以通过在保存操作前重新排列工作表来控制幻灯片顺序。

```csharp
// Move the worksheet that should appear first in the slide deck
workbook.Worksheets.MoveTo(2, 0); // move sheet index 2 to position 0
```

### 性能提示：使用流而非写入磁盘

在 Web API 中生成 PowerPoint 文件时，避免使用临时文件，可将输出写入 `MemoryStream`。

```csharp
using (MemoryStream pptStream = new MemoryStream())
{
    workbook.Save(pptStream, SaveFormat.Pptx);
    // Return the stream as a file download
    FileContentResult result = new FileContentResult(pptStream.ToArray(),
        "application/vnd.openxmlformats-officedocument.presentationml.presentation")
    {
        FileDownloadName = "Charts.pptx"
    };
    return result;
}
```

## 完整、可运行的示例

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1. Load the workbook containing charts
            string excelPath = @"C:\Projects\ChartAndShapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2. (Optional) Ensure formulas are up‑to‑date
            workbook.CalculateFormula();

            // 3. Export to PowerPoint while preserving shape editability
            string pptxPath = @"C:\Projects\Shapes.pptx";
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export complete. PowerPoint saved to: {pptxPath}");
        }
    }
}
```

**预期输出：** 控制台会打印确认信息，`Shapes.pptx` 在 PowerPoint 中打开后，每个 Excel 图表都会出现在单独的幻灯片上。选中图表后可以编辑其数据，证明 **形状可编辑性** 已被保留。

## 回顾与后续步骤

您现在已经掌握了使用 C# **将 Excel 图表导出到 PowerPoint** 并保持图表完全可编辑的技巧。解决方案的核心是使用 `Workbook.Save` 方法并传入 `SaveFormat.Pptx`，这是 **Aspose.Cells export** 提供的功能，可抽象掉复杂的 Open XML 处理。

接下来您可以探索：

* 使用 **Aspose.Slides** API 添加自定义幻灯片标题或备注。  
* 将其他 Excel 对象（表格、图片）与图表一起转换。  
* 在后台服务中对多个工作簿进行批量处理自动化。

欢迎尝试上述可选设置，并将此模式集成到您的报告流水线中，以实现快速、可靠的 PowerPoint 生成。

## 接下来应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方案。每个资源都提供完整的可运行代码示例和逐步解释。

- [Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide](/cells/english/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/)
- [How to Export Excel to PowerPoint with C# – Complete Guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)
- [How to Export Shapes from Excel to PowerPoint – Complete Guide](/cells/english/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}