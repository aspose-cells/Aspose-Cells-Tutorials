---
category: general
date: 2026-06-05
description: 如何使用 C# 从 PowerPoint 导出图表。包括导出 OLE 对象并使导出的 PPTX 中的图表可编辑——一步一步。
draft: false
keywords:
- how to export charts
- export ole objects
- how to export ole
- make charts editable
language: zh
og_description: 如何使用 C# 从 PowerPoint 导出图表。学习导出 OLE 对象并使保存的 PPTX 中的图表可编辑——一步一步教程。
og_title: 如何导出图表 – 完整的 PowerPoint C# 指南
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  headline: How to Export Charts – Complete PowerPoint C# Guide
  type: TechArticle
- description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  name: How to Export Charts – Complete PowerPoint C# Guide
  steps:
  - name: Full Working Example
    text: Below is the complete, self‑contained program you can compile and run. It
      includes `using` statements, proper disposal, and comments that explain each
      line.
  - name: What if the source file has no charts?
    text: The code will still run; `ExportEditableCharts` simply has no effect because
      there’s nothing to convert. No error is thrown.
  - name: Can I export only specific charts?
    text: Yes. Instead of using the global `ExportEditableCharts` flag, you can iterate
      through `presentation.Slides` and set `Chart.IsEditable = true` on individual
      chart objects before saving. This gives you granular control.
  - name: Does enabling OLE export increase file size?
    text: A little. The binary OLE streams are stored verbatim, so the resulting PPTX
      can be a few kilobytes larger. In most business scenarios the trade‑off is worth
      it because you retain full editability.
  - name: Which PowerPoint versions can open the resulting file?
    text: Any version that supports the OOXML standard (PowerPoint 2007 and later).
      The editable chart feature relies on the native chart editor introduced in Office
      2007, so older binaries like `.ppt` won’t benefit.
  type: HowTo
tags:
- PowerPoint
- C#
- Aspose.Slides
- OLE
- Charts
title: 如何导出图表——完整的 PowerPoint C# 指南
url: /zh/net/chart-rendering-and-conversion/how-to-export-charts-complete-powerpoint-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何导出图表 – 完整的 PowerPoint C# 指南

是否曾经想过 **如何导出图表** 从 PowerPoint 幻灯片而不失去后续编辑的能力？你并不是唯一有此疑问的人。在许多报告流程中，图表数据存储在 PPTX 中，一旦将文件交给他人，接收者通常需要微调某个数值或更改标签。好消息是，只需几行 C# 代码，你就可以保留可编辑性，甚至还能同时导出嵌入的 OLE 对象。

在本教程中，我们将演示一个实用的、可直接运行的示例，展示 **如何导出图表**、如何 **导出 OLE 对象**，以及如何在输出文件中 **使图表可编辑**。完成后，你将拥有一个可复用的代码片段，可直接嵌入使用 Aspose.Slides 库的任何 .NET 项目中。

> **专业提示：** 如果你是 Aspose.Slides 的新手，请确保已在项目中添加 NuGet 包 `Aspose.Slides.NET`——否则代码将无法编译。

## 你需要的条件

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6+ (or .NET Framework 4.7+) | 现代运行时提供更好的性能和更简便的包管理。 |
| Aspose.Slides for .NET (latest version) | 该库提供我们将使用的 `Presentation` 和 `PptxSaveOptions` 类。 |
| A sample PowerPoint file with at least one chart | 演示适用于任何包含图表的 `.pptx` 文件；导出后你将看到可编辑性。 |
| An IDE (Visual Studio, Rider, or VS Code) | 便于快速调试并查看生成的文件。 |

无需额外的第三方工具——所有操作均由 Aspose API 处理。

## 步骤 1 – 加载源演示文稿

首先，我们需要将原始 PPTX 加载到内存中。可以把它想象成在 Word 中打开文档后再进行编辑。

```csharp
using Aspose.Slides;

// Step 1: Load the source presentation
Presentation presentation = new Presentation(@"C:\MyProjects\input.pptx");
```

> **原因说明：** `Presentation` 对象是所有后续操作的入口。它解析文件，构建幻灯片、形状、图表和 OLE 对象的对象模型，并保持所有内容处于可变状态。

## 步骤 2 – 创建保存选项并启用可编辑图表

默认情况下，调用 `Save` 时库会将图表展平为静态图像。若要保持图表可编辑，需要切换 `ExportEditableCharts` 标志。

```csharp
// Step 2: Create PPTX save options and enable editable charts
PptxSaveOptions saveOptions = new PptxSaveOptions
{
    // This tells Aspose to keep chart data in a format PowerPoint can edit.
    ExportEditableCharts = true
};
```

> **工作原理：** 当 `ExportEditableCharts` 为 `true` 时，库会将图表的 XML 定义（`chart.xml`）写入 PPTX，而不是将其光栅化。PowerPoint 随后读取该 XML 并允许用户打开图表编辑器。

## 步骤 3 – 启用嵌入式 OLE 对象的导出

许多演示文稿将 Excel 工作表、Visio 图表，甚至 PDF 文件嵌入为 OLE 对象。如果希望这些对象在往返过程中保持完整，请启用 `ExportOLEObjects`。

```csharp
// Step 3: Enable export of embedded OLE objects
saveOptions.ExportOLEObjects = true;
```

> **“导出 OLE 对象” 的真实含义：** OLE 包作为二进制块存储在 PPTX 中。设置此标志会保留原始二进制数据，允许接收者双击对象并在其原生应用程序（例如 Excel）中打开。若不设置，该 OLE 对象将被剥离，导致链接断裂并丢失数据。

## 步骤 4 – 使用配置好的选项保存演示文稿

现在我们已经准备好选项，只需告诉 Aspose 将文件写出即可。

```csharp
// Step 4: Save the presentation with the configured options
presentation.Save(@"C:\MyProjects\editable.pptx", saveOptions);
```

> **结果：** `editable.pptx` 包含与 `input.pptx` 相同的幻灯片，但任何图表都可以直接在 PowerPoint 中编辑，且所有嵌入的 OLE 对象保持完整。

### 完整工作示例

下面是完整的、可独立运行的程序示例，你可以编译并执行。它包含 `using` 语句、正确的资源释放以及解释每行代码的注释。

```csharp
using System;
using Aspose.Slides;

namespace ExportChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the source PPTX
            string sourcePath = @"C:\MyProjects\input.pptx";
            // Path where the edited PPTX will be saved
            string destPath = @"C:\MyProjects\editable.pptx";

            // Load the presentation
            using (Presentation presentation = new Presentation(sourcePath))
            {
                // Configure save options
                PptxSaveOptions options = new PptxSaveOptions
                {
                    ExportEditableCharts = true,   // make charts editable
                    ExportOLEObjects = true        // export OLE objects such as embedded Excel sheets
                };

                // Save the new file
                presentation.Save(destPath, options);
            }

            Console.WriteLine("Presentation saved with editable charts and OLE objects.");
        }
    }
}
```

**预期输出：** 运行程序后，在 PowerPoint 中打开 `editable.pptx`。右键单击任意图表 → *编辑数据* → 图表编辑器打开，确认 **使图表可编辑** 成功。双击嵌入的 Excel 工作表，它将在 Excel 中打开，证明 **导出 OLE 对象** 已生效。

![如何导出图表的示意图](https://example.com/images/export-charts.png "如何导出图表 – 导出后 PowerPoint")

（Alt 文本：如何导出图表 – PowerPoint 中带有可编辑图表和 OLE 对象的截图）

## 常见问题与边缘情况

### 如果源文件没有图表怎么办？

代码仍会运行；`ExportEditableCharts` 因为没有可转换的内容而不起作用。不会抛出错误。

### 我可以只导出特定的图表吗？

可以。与其使用全局的 `ExportEditableCharts` 标志，你可以遍历 `presentation.Slides`，在保存前对单个图表对象设置 `Chart.IsEditable = true`。这样可以实现细粒度控制。

```csharp
foreach (ISlide slide in presentation.Slides)
{
    foreach (IChart chart in slide.Shapes.OfType<IChart>())
    {
        chart.IsEditable = true; // enable editability only for this chart
    }
}
```

### 启用 OLE 导出会增加文件大小吗？

会略有增加。二进制 OLE 流会原样存储，因此生成的 PPTX 可能会大几千字节。在大多数业务场景下，这种权衡是值得的，因为你保留了完整的可编辑性。

### 哪些 PowerPoint 版本可以打开生成的文件？

任何支持 OOXML 标准的版本（PowerPoint 2007 及以后）。可编辑图表功能依赖于 Office 2007 引入的原生图表编辑器，因此旧的二进制格式如 `.ppt` 不会受益。

## 生产环境代码的提示

| Tip | Reason |
|-----|--------|
| 使用 `using` 块（如示例所示）来释放 `Presentation` 对象。 | 防止内存泄漏，尤其是在批量处理大量文件时。 |
| 在加载之前验证文件路径。 | 避免导致后台服务崩溃的 `FileNotFoundException`。 |
| 记录 `ExportEditableCharts` 和 `ExportOLEObjects` 设置。 | 当用户报告图表不可编辑时，有助于排查问题。 |
| 单独捕获 `Aspose.Slides.Exception`。 | 提供更清晰的库错误信息（例如，不支持的图表类型）。 |
| 如果文件大小重要，可考虑 `PptxCompressionLevel`。 | 在保持可编辑性的同时压缩输出文件。 |

## 回顾 – 我们达成的目标

我们从一个明确的问题出发：**如何导出图表** 并保持其可编辑性，同时保留嵌入的 OLE 对象。通过加载演示文稿、配置 `PptxSaveOptions`（`ExportEditableCharts = true` 和 `ExportOLEObjects = true`），并保存文件，我们现在拥有满足这两个需求的 PPTX。相同的模式可用于批量转换、CI 流水线或任何自动化报告工具。

## 接下来可以探索的内容？

- **将图表导出为图像** 用于静态报告（`saveOptions.ExportEditableCharts = false`）。  
- **将 PPTX 转换为 PDF** 并保留矢量图形（`PdfSaveOptions`）。  
- **以编程方式操作图表数据**（例如，在导出前更新系列值）。  
- **与 Azure Functions 集成**，提供按需图表导出 API。

## 接下来应该学习什么？

以下教程涵盖与本指南技术密切相关的主题，构建在本指南展示的技巧之上。每个资源都包含完整的可运行代码示例和逐步说明，帮助你掌握更多 API 功能并在自己的项目中探索替代实现方案。

- [如何使用 Aspose.Cells for .NET 将 Excel 图表导出为 PDF：分步指南](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [如何使用 Aspose.Cells for .NET 将 Excel 图表转换为 SVG（分步指南）](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [如何使用 Aspose.Cells .NET 为 Excel 图表应用主题：分步指南](/cells/english/net/charts-graphs/apply-themes-charts-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}