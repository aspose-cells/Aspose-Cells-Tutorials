---
category: general
date: 2026-10-01
description: 使用 Aspose.Cells 在 C# 中从 Excel 创建 PowerPoint。快速将 Excel 导出为 PowerPoint，并将
  XLSX 转换为 PPTX，提供完整的代码示例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create PowerPoint from Excel
- export Excel to PowerPoint
- convert Excel to PPTX
- convert XLSX to PPTX
- generate PowerPoint from Excel
language: zh
lastmod: 2026-10-01
og_description: 使用 Aspose.Cells 在 C# 中将 Excel 创建为 PowerPoint。学习如何将 Excel 导出为 PowerPoint，并在几行代码内将
  XLSX 转换为 PPTX。
og_image_alt: Screenshot of a PowerPoint slide generated from Excel using Aspose.Cells
og_title: 使用 Aspose.Cells 从 Excel 创建 PowerPoint – 快速指南
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create PowerPoint from Excel using Aspose.Cells in C#. Export Excel
    to PowerPoint and convert XLSX to PPTX quickly with a complete code example.
  headline: Create PowerPoint from Excel with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Office automation
title: 使用 Aspose.Cells 将 Excel 转换为 PowerPoint – 步骤指南
url: /zh/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells 从 Excel 创建 PowerPoint – 步骤指南

如果您需要**从 Excel 创建 PowerPoint**，本教程将向您展示如何使用 Aspose.Cells for .NET 实现。您将学习**将 Excel 导出为 PowerPoint**，将 XLSX 工作簿转换为 PPTX 演示文稿，并在不离开 C# 项目的情况下自定义生成的幻灯片。

本指南涵盖在 .NET 6 或更高版本上运行代码所需的全部内容，包括项目设置、必需的 NuGet 包以及完整的可运行示例。完成后，您将拥有一个 PowerPoint 文件，其中包含原始 Excel 图表，且外观与工作簿中完全一致。

## 您需要的条件

| 前置条件 | 原因 |
|---|---|
| .NET 6 SDK 或更高版本 | 为 C# 控制台应用提供运行时 |
| Visual Studio 2022（或任何 IDE） | 便于项目创建和调试 |
| Aspose.Cells for .NET NuGet 包 | 提供 `Workbook` 类和导出 API |
| 包含至少一个图表的 Excel 文件（`.xlsx`） | PowerPoint 幻灯片的源数据 |

> **专业提示：** Aspose.Cells 可在 Windows、Linux 和 macOS 上运行，您可以在 Docker 容器或 CI 流水线中使用相同的代码。

## 第 1 步：创建新控制台项目并添加 Aspose.Cells

打开终端（或 Visual Studio 包管理器控制台）并运行：

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
dotnet add package Aspose.Cells
```

`dotnet add package` 命令会下载最新稳定版的 **Aspose.Cells**，其中包含后面将使用的 `ExportPptx` 方法。

## 第 2 步：添加源 Excel 工作簿

将您要转换的 Excel 文件放入项目文件夹。本文示例使用 `ChartOle.xlsx`，该文件在第一个工作表上包含一个图表。

```
/ExcelToPptxDemo
│   Program.cs
│   ChartOle.xlsx   ← your source workbook
```

## 第 3 步：编写**从 Excel 创建 PowerPoint**的代码

打开 `Program.cs`，将其内容替换为以下代码。示例演示了**核心导出**操作，并展示了如何处理常见的边缘情况，如文件缺失和不受支持的图表类型。

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelToPptxDemo
{
    class Program
    {
        static void Main()
        {
            // Define input and output paths
            string inputPath = Path.Combine(AppContext.BaseDirectory, "ChartOle.xlsx");
            string outputPath = Path.Combine(AppContext.BaseDirectory, "Exported.pptx");

            // Verify that the source workbook exists
            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: The file '{inputPath}' was not found.");
                return;
            }

            try
            {
                // Load the Excel workbook that contains the chart
                var workbook = new Workbook(inputPath);

                // Export the first worksheet as a PowerPoint presentation
                // This call performs the **convert Excel to PPTX** operation.
                workbook.Worksheets[0].ExportPptx(outputPath);

                Console.WriteLine($"Success: PowerPoint file created at '{outputPath}'.");
            }
            catch (Exception ex)
            {
                // Catch any errors thrown by Aspose.Cells (e.g., unsupported chart)
                Console.WriteLine($"Export failed: {ex.Message}");
            }
        }
    }
}
```

### 为什么这样可行

* `Workbook` 读取整个 Excel 文件，包括嵌入的图表、表格和格式。
* `ExportPptx` 将活动工作表转换为 PPTX 幻灯片集。该方法会自动将 Excel 图表转换为 PowerPoint 形状，保持视觉一致性。
* 代码将操作包装在 `try/catch` 块中，以捕获因文件损坏导致的 **convert XLSX to PPTX** 失败等错误。

## 第 4 步：运行程序并验证输出

执行应用程序：

```bash
dotnet run
```

您应该会看到控制台消息：

```
Success: PowerPoint file created at '.../Exported.pptx'.
```

在 Microsoft PowerPoint 或任何兼容的查看器中打开 `Exported.pptx`。第一张幻灯片会显示与 `ChartOle.xlsx` 中完全相同的图表。这表明您已成功**从 Excel 生成 PowerPoint**。

## 第 5 步：高级 – 导出多个工作表或自定义幻灯片布局

基础示例仅导出第一个工作表。在实际场景中，您可能需要：

* **导出多个工作表**为独立的幻灯片。
* **控制幻灯片尺寸**或添加标题占位符。
* **在转换中包含隐藏工作表**。

下面是一段简洁的代码片段，遍历所有工作表并将每个工作表添加为单独的幻灯片：

```csharp
// Export each worksheet as a separate slide
var pptxPath = Path.Combine(AppContext.BaseDirectory, "FullExport.pptx");
var presentation = new Presentation(); // Aspose.Slides.Presentation, if you have the Slides library

foreach (Worksheet ws in workbook.Worksheets)
{
    // Convert worksheet to an image first (optional for custom layout)
    var imgStream = new MemoryStream();
    ws.PageSetup.PrintArea = ws.Cells.MaxDisplayRange; // ensure full content
    ws.Pictures[0].ToImage(imgStream, ImageFormat.Png);

    // Add a new slide and insert the image
    var slide = presentation.Slides.AddEmptySlide(presentation.SlideSize.Size);
    slide.Shapes.AddPictureFrame(ShapeType.Rectangle, 0, 0, presentation.SlideSize.Size.Width, presentation.SlideSize.Size.Height, imgStream);
}

// Save the final presentation
presentation.Save(pptxPath, SaveFormat.Pptx);
```

> **注意：** 高级代码片段需要 **Aspose.Slides for .NET** 库。如果您只需要简单的单工作表转换，之前的 `ExportPptx` 调用即可满足需求。

## 常见陷阱及规避方法

| 问题 | 原因 | 解决方案 |
|---|---|---|
| 导出后出现空白幻灯片 | 工作表中没有可见对象 | 在调用 `ExportPptx` 前确保至少有一个图表、表格或形状。 |
| PowerPoint 中缺少字体 | 打开 PPTX 的机器未安装相应字体 | 在 Excel 工作簿中嵌入所需字体，或在目标系统上安装这些字体。 |
| 意外的缩放 | 大图表超出幻灯片尺寸 | 在导出前调整工作表的 `PageSetup.Zoom` 属性。 |
| `convert XLSX to PPTX` 抛出 `NotSupportedException` | Aspose.Cells 不支持的图表类型（例如 3‑D 地图） | 将图表替换为受支持的类型，或先将工作表导出为图像。 |

处理这些边缘情况可确保在生产环境中实现可靠的**导出 Excel 到 PowerPoint**工作流。

## 结论

现在，您已经掌握了使用 Aspose.Cells for .NET **从 Excel 创建 PowerPoint**的方法。教程涵盖了：

* 项目设置与 NuGet 安装
* 加载 Excel 工作簿并调用 `ExportPptx`
* 运行代码并确认生成的 PPTX
* 扩展方案以处理多个工作表和自定义布局
* 避免常见转换问题的实用技巧

有了这些知识，您可以实现报告自动化、构建演示流水线，或在任何 C# 应用中集成 Excel‑to‑PowerPoint 转换。尝试不同的图表类型、添加幻灯片标题，或将导出与 Aspose.Slides 结合，实现功能完整的演示文稿创建。

--- 

*准备好进一步探索吗？查看相关主题，如**将 Excel 转换为 PDF**、**在 Word 中嵌入 Excel 数据**或**使用 Aspose.Slides 编程编辑 PPTX 文件**。*

## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您在自己的项目中进一步掌握 API 功能并探索替代实现方案。每个资源都提供完整的可运行代码示例和逐步解释。

- [将 Excel 转换为 PowerPoint Aspose Cells .NET](/cells/german/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [将 Excel 转换为 PowerPoint Aspose Cells .NET](/cells/french/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [将 Excel 转换为 PowerPoint Aspose Cells .NET](/cells/spanish/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}