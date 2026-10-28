---
category: general
date: 2026-07-03
description: 如何在 C# 中使用 Aspose.Slides 保留图表并保持图表格式。请遵循以下分步指南。
draft: false
keywords:
- how to preserve charts
- preserve chart formatting
language: zh
og_description: 如何在 C# 中使用 Aspose.Slides 保持图表及其格式。完整的代码指南。
og_title: 如何保留图表 – 在 PowerPoint 中保持图表格式 (C#)
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  headline: how to preserve charts – preserve chart formatting in PowerPoint C#
  type: TechArticle
- description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  name: how to preserve charts – preserve chart formatting in PowerPoint C#
  steps:
  - name: Open `EditableCharts.pptx` in PowerPoint.
    text: Open `EditableCharts.pptx` in PowerPoint.
  - name: Click any chart → “Edit Data”.
    text: Click any chart → “Edit Data”.
  - name: The Excel‑like data sheet should appear, letting you modify series values.
    text: The Excel‑like data sheet should appear, letting you modify series values.
  type: HowTo
- questions:
  - answer: Directly no—`ExportEditableObjects` only applies to the PPTX format. Convert
      first, then export.
    question: Does this work with PowerPoint 2003 (PPT) files?
  - answer: Absolutely. The same `ExportEditableObjects` flag keeps SmartArt, tables,
      and diagrams editable.
    question: Can I preserve other objects like SmartArt?
  - answer: 'The slide size is stored in the presentation metadata and isn’t affected
      by these options. No extra code needed. --- ## Next steps – keep the momentum
      Now that you’ve nailed **how to preserve charts**, try exploring: - **preserve
      chart formatting** for specific chart types (e.g., stacked bar vs. rad'
    question: What if I need to keep the original slide size?
  type: FAQPage
tags:
- Aspose.Slides
- C#
- PowerPoint
- chart automation
title: 如何保留图表——在 PowerPoint C# 中保留图表格式
url: /zh/net/setting-chart-appearance/how-to-preserve-charts-preserve-chart-formatting-in-powerpoi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 PowerPoint C# 中保留图表 – 保持图表格式

是否曾经想过在需要以编程方式导出或操作 PowerPoint 文件时，**如何保留图表**？也许你尝试了快速保存，结果图表变成了静态图片，破坏了你所期望的可编辑性。  

在本教程中，我们将展示如何使用 Aspose.Slides for .NET **保留图表** **并且** 保持其 **保留图表格式** 完整。完成后，你将拥有一个可直接运行的 C# 代码片段，生成的 PPTX 中每个图表都保持为可编辑的 OOXML 对象——不再是扁平化的图片。

## 你将学到的内容

- 加载演示文稿、配置导出选项并保存，同时**保留图表格式**的完整步骤。  
- `ExportEditableObjects` 标志为何重要以及它如何防止图表被栅格化。  
- 常见陷阱（例如旧的 PPT 格式、缺失字体）及快速解决方案。  

不需要任何 Aspose 经验；只需基本的 C# 环境和一个你希望保持图表可编辑性的 PowerPoint 文件即可。

## 前提条件

- .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.7+）。  
- Aspose.Slides for .NET NuGet 包（`Install-Package Aspose.Slides.NET`）。  
- 一个包含至少一个图表的示例 `input.pptx`。  
- Visual Studio、Rider 或任何你喜欢的编辑器。

---

## 步骤 1：安装 Aspose.Slides 并创建新的控制台项目

首先，创建一个全新的控制台应用并引入该库：

```bash
dotnet new console -n PreserveChartsDemo
cd PreserveChartsDemo
dotnet add package Aspose.Slides.NET
```

> **小贴士：** 如果你在公司代理后面，添加 `--no-restore` 标志，并在之后使用代理设置进行恢复。

## 步骤 2：加载源演示文稿 – 应用 **如何保留图表** 的第一步

使用 `Presentation` 类打开你的 PPTX 文件。这是 **如何保留图表** 真正开始的地方。

```csharp
using Aspose.Slides;
using Aspose.Slides.Export;

namespace PreserveChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Load the source presentation
            // Replace the path with the location of your PPTX that contains charts.
            Presentation pres = new Presentation(@"YOUR_DIRECTORY\input.pptx");
```

请注意我们尚未触及任何图表对象——这是一种刻意的做法。按原样加载文件可确保保留原始 XML 结构，这对后续的 **保留图表格式** 至关重要。

## 步骤 3：配置导出选项 – **如何保留图表** 的核心

Aspose.Slides 提供了 `PresentationExportOptions` 类。将 `ExportEditableObjects` 设置为 `true` 可指示引擎将图表、表格和 SmartArt 保持为原生 OOXML 部分，而不是将其扁平化。

```csharp
            // Step 3: Configure export options to keep objects editable
            PresentationExportOptions exportOptions = new PresentationExportOptions
            {
                // This flag is the key to how to preserve charts.
                ExportEditableObjects = true
            };
```

这为何有效？当 `ExportEditableObjects` 为 `false`（默认值）时，库会为了兼容性而将复杂对象栅格化，这会破坏 **保留图表格式**。开启该选项则保留原始图表 XML，使最终用户打开 PPTX 时仍能编辑图表数据。

## 步骤 4：使用配置好的选项保存演示文稿

现在我们写入输出文件。使用接受 `SaveFormat` 和 `exportOptions` 的同一 `Save` 重载可确保图表保持可编辑。

```csharp
            // Step 4: Save the presentation with the configured options
            pres.Save(@"YOUR_DIRECTORY\EditableCharts.pptx", SaveFormat.Pptx, exportOptions);

            // Optional: Inform the user
            Console.WriteLine("Presentation saved with editable charts at: YOUR_DIRECTORY\\EditableCharts.pptx");
        }
    }
}
```

运行此程序会生成 `EditableCharts.pptx`。在 PowerPoint 中打开它，右键单击图表，你会看到常见的 “Edit Data” 选项——这证明我们已经成功掌握了 **如何保留图表** 和 **保留图表格式**。

## 步骤 5：验证结果并排查常见问题

### 验证

1. 在 PowerPoint 中打开 `EditableCharts.pptx`。  
2. 点击任意图表 → “Edit Data”。  
3. 应出现类似 Excel 的数据表，允许你修改系列值。

如果你只看到静态图片，请再次检查以下事项：

- 你使用的是最新版本的 Aspose.Slides（旧版本在 `ExportEditableObjects` 上存在 bug）。  
- 源 PPTX 实际包含图表对象（而非图表图片）。  
- 没有自定义主题或字体替换导致图表被渲染为图片。

### 边缘情况

- **旧的 PPT（二进制）文件：** 在应用导出选项之前先将其转换为 PPTX（`pres.Save("temp.pptx", SaveFormat.Pptx)`）。  
- **大型演示文稿：** 内存使用可能激增；考虑使用 `Presentation` 的 `Dispose` 模式或流式 API 处理大型文件。  
- **嵌入字体：** 如果目标环境缺少原始字体，PowerPoint 可能回退并将图表渲染为图片。请在源文件中嵌入字体或随应用程序一起提供。

---

## 常见问题解答 (FAQ)

**问：这是否适用于 PowerPoint 2003（PPT）文件？**  
**答：** 直接不适用——`ExportEditableObjects` 仅适用于 PPTX 格式。请先转换后再导出。

**问：我可以保留其他对象如 SmartArt 吗？**  
**答：** 当然可以。同样的 `ExportEditableObjects` 标志会保持 SmartArt、表格和图表可编辑。

**问：如果我需要保持原始幻灯片尺寸怎么办？**  
**答：** 幻灯片尺寸存储在演示文稿的元数据中，不受这些选项影响。无需额外代码。

## 下一步 – 持续前进

既然你已经掌握了 **如何保留图表**，可以尝试探索：

- 针对特定图表类型（例如堆叠柱形图 vs. 雷达图）**保留图表格式**。  
- 使用 `Chart` API 在保存前以编程方式修改数据。  
- 导出到其他格式（PDF、HTML），同时保持源 PPTX 中图表可编辑。  

这些都基于相同的原则：保持底层 OOXML 完整。

## 结论

我们已经演示了如何使用 Aspose.Slides for .NET 在 PowerPoint 文件中 **保留图表**，并展示了保持图表完全可编辑所需的 **保留图表格式** 的具体步骤。上面的完整代码片段可直接嵌入任何 C# 项目，解释阐述了每行代码背后的 *原因*——因此你不仅仅是复制粘贴，还能理解其原理。

试一试，调整导出选项，很快你就能在不失去微调图表数据能力的情况下自动化演示文稿更新。祝编码愉快！

## 接下来你应该学习什么？

以下教程涵盖与本指南技术密切相关的主题，构建在本指南演示的技巧之上。每个资源都包含完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能并在项目中探索替代实现方案。

- [如何使用 Aspose.Cells for .NET 将 Excel 图表导出为 PDF：一步步指南](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [如何使用 Aspose.Cells for .NET 将 Excel 图表转换为 SVG（一步步指南）](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [如何使用 Aspose.Cells for .NET 在 Excel 中创建图表：开发者指南](/cells/english/net/charts-graphs/create-charts-excel-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}