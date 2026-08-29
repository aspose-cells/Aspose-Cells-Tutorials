---
category: general
date: 2026-08-04
description: 使用 Aspose.Cells 在 C# 中将 Excel 图表导出到 PowerPoint。遵循此一步步的 Excel 到 PowerPoint
  转换指南，并保持形状可编辑。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel chart to powerpoint
- Aspose.Cells PPTX export
- editable shapes in PowerPoint
- Excel to PowerPoint conversion
- C# chart export
language: zh
lastmod: 2026-08-04
og_description: 使用 Aspose.Cells 在 C# 中将 Excel 图表导出到 PowerPoint。了解如何创建可编辑的 PPTX，保留图表数据，并实现
  Excel 到 PowerPoint 的自动转换。
og_image_alt: Screenshot of an Excel chart rendered as an editable PowerPoint slide
og_title: 使用 C# 将 Excel 图表导出到 PowerPoint – 完整 Aspose.Cells 教程
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  headline: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  type: TechArticle
- description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  name: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  steps:
  - name: Expected output
    text: '| File name | Content on slide | |--------------------------|------------------------------------------|
      | `ShapesExport.pptx` | The chart from `Shapes.xlsx` rendered as an editable
      PowerPoint chart, with axis labels, legends, and data series intact. |'
  - name: Exporting multiple worksheets
    text: If you need a slide for each worksheet, loop through `workbook.Worksheets`
      and call `Save` with a unique file name for each iteration.
  - name: Controlling slide layout
    text: Aspose.Slides lets you add a custom slide layout after the export. Create
      a new presentation, import the generated slide, and then apply a master theme.
  - name: Handling charts with external data sources
    text: If a chart references a data range outside the defined print area, extend
      the `PrintArea` to include those cells. Otherwise the chart may lose data series
      during export.
  - name: Licensing considerations
    text: 'Aspose libraries work in evaluation mode with a watermark. To remove the
      watermark, set the license before any API call:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- PowerPoint
title: 使用 C# 将 Excel 图表导出到 PowerPoint – 完整的 Aspose.Cells 指南
url: /zh/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 将 Excel 图表导出到 PowerPoint – 完整 Aspose.Cells 指南

如果您需要 **export Excel chart to PowerPoint**，本教程将向您展示如何使用 C# 中的 Aspose.Cells 和 Aspose.Slides 完成此操作。您将获得一个完全可编辑的 PPTX，保留图表数据和形状，使转换后可直接进行进一步的设计工作。

在构建自动化报告流水线、销售演示文稿或培训材料时，将 Excel 图表导出到 PowerPoint 是常见需求。在本指南中，您将学习执行 **Excel to PowerPoint conversion** 的确切步骤，确保所有图表元素保持可编辑。无需手动复制粘贴，代码兼容 .NET 6+ 以及经典的 .NET Framework。

## 前提条件

- 有效的 Aspose.Cells 许可证（或免费评估密钥）  
- 已在项目中添加 Aspose.Slides for .NET（该库负责 PPTX 输出）  
- 已安装 .NET 6 SDK 或更高版本  
- 包含至少一个图表的 Excel 工作簿（本示例使用 `Shapes.xlsx`）  

您可以使用以下命令安装 NuGet 包：

```bash
dotnet add package Aspose.Cells
dotnet add package Aspose.Slides
```

## 步骤 1：加载 Excel 工作簿

第一步是打开包含要导出图表的工作簿。`Workbook` 类表示整个 Excel 文件。

```csharp
using Aspose.Cells;
using Aspose.Slides;   // required for PPTX output

// Load the Excel workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

**为什么这很重要：**  
加载工作簿后，您即可访问其工作表、图表和格式。Aspose.Cells 在读取文件时不需要安装 Microsoft Office，从而保持解决方案轻量且适合服务器环境。

## 步骤 2：选择工作表并定义打印区域

一个工作表可能包含多个图表，但通常只导出特定区域。设置 `PrintArea` 可告知 Aspose.Cells 哪些单元格（包括图表）需要渲染。

```csharp
// Choose the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Define the area that contains the chart and any supporting data
worksheet.PageSetup.PrintArea = "A1:G30";
```

**为什么这很重要：**  
通过将导出限制在定义的打印区域，可避免生成不必要的空白幻灯片并保持 PPTX 文件体积小。该区域可根据图表的实际范围进行调整。

## 步骤 3：配置可编辑 PPTX 的导出选项

Aspose.Cells 使用 `ImageOrPrintOptions` 类来控制输出格式和可编辑性。将 `ImageFormat` 设置为 `ImageFormat.Pptx` 可生成 PowerPoint 文件，而 `ExportEditableShapes = true` 则将图表对象保留为可编辑形状。

```csharp
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Pptx,   // Target format
    ExportEditableShapes = true       // Keep shapes/textboxes editable
};

// Attach the options to the worksheet's print settings
worksheet.PageSetup.PrintOptions = exportOptions;
```

**为什么这很重要：**  
`ExportEditableShapes` 标志是实现 **editable shapes in PowerPoint** 结果的关键。若不设置此标志，图表将被光栅化为图像，后续将无法修改数据点或样式。

## 步骤 4：将工作表保存为 PowerPoint 演示文稿

最后，对 `Workbook` 对象调用 `Save` 方法。`SaveFormat.Pptx` 枚举指示 Aspose.Cells 生成 PowerPoint 文件。

```csharp
// Export the selected worksheet to a PPTX file
workbook.Save("YOUR_DIRECTORY/ShapesExport.pptx", SaveFormat.Pptx);
```

代码执行完毕后，在 PowerPoint 中打开 `ShapesExport.pptx`。您会看到一张幻灯片，其中包含原始 Excel 图表，作为原生 PowerPoint 图表对象。双击图表即可编辑数据、更改颜色或添加动画——就像直接在 PowerPoint 中创建的图表一样。

### 预期输出

| 文件名                | 幻灯片内容                         |
|----------------------|-----------------------------------|
| `ShapesExport.pptx`  | `Shapes.xlsx` 中的图表呈现为可编辑的 PowerPoint 图表，轴标签、图例和数据系列保持完整。 |

## 完整、可运行的示例

下面是完整的程序，您可以复制、粘贴并运行。它包含所有必要的 `using` 语句、错误处理和注释。

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;   // Required for PPTX output

class ExcelToPowerPoint
{
    static void Main()
    {
        // Path to the source Excel file – adjust as needed
        const string excelPath = "YOUR_DIRECTORY/Shapes.xlsx";
        // Path for the generated PowerPoint file
        const string pptxPath = "YOUR_DIRECTORY/ShapesExport.pptx";

        try
        {
            // Load the workbook
            Workbook workbook = new Workbook(excelPath);

            // Use the first worksheet (you can change the index or name)
            Worksheet worksheet = workbook.Worksheets[0];

            // Define the area that contains the chart
            worksheet.PageSetup.PrintArea = "A1:G30";

            // Set export options for PPTX with editable shapes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Pptx,
                ExportEditableShapes = true
            };
            worksheet.PageSetup.PrintOptions = exportOptions;

            // Save as PPTX
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export successful. PPTX saved to: {pptxPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**各代码块说明**

| 代码块 | 用途 |
|--------|------|
| `using` directives | 引入 Aspose.Cells 和 Aspose.Slides 命名空间。 |
| `Workbook workbook = new Workbook(excelPath);` | 在无需安装 Office 的情况下加载 Excel 文件。 |
| `worksheet.PageSetup.PrintArea = "A1:G30";` | 将导出限制在包含图表的区域。 |
| `ImageOrPrintOptions` | 配置 PPTX 输出并启用带可编辑形状的 **Aspose.Cells PPTX export**。 |
| `workbook.Save(pptxPath, SaveFormat.Pptx);` | 将 PowerPoint 文件写入磁盘。 |
| `try / catch` | 提供基本的错误处理，以应对文件缺失或授权问题。 |

运行该程序后会生成一张 PowerPoint 幻灯片，您可以在 Microsoft PowerPoint、Google Slides（转换后）或任何兼容的查看器中打开。

## 常见变体和边缘情况

### 导出多个工作表

如果需要为每个工作表生成一张幻灯片，可遍历 `workbook.Worksheets`，并在每次迭代时使用唯一的文件名调用 `Save`。

```csharp
int index = 1;
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.PageSetup.PrintOptions = exportOptions;
    string fileName = $"Slide{index++}.pptx";
    workbook.Save(fileName, SaveFormat.Pptx);
}
```

### 控制幻灯片布局

Aspose.Slides 允许在导出后添加自定义幻灯片布局。创建新演示文稿，导入生成的幻灯片，然后应用母版主题。

```csharp
using Aspose.Slides.Export;

// Load the PPTX created by Aspose.Cells
Presentation pres = new Presentation(pptxPath);

// Apply a built‑in layout (e.g., Title and Content)
pres.Slides[0].LayoutSlide = pres.LayoutSlides[(int)SlideLayoutType.TitleAndContent];

// Save the final presentation
pres.Save("FinalPresentation.pptx", SaveFormat.Pptx);
```

### 处理使用外部数据源的图表

如果图表引用的数据显示范围超出已定义的打印区域，请扩展 `PrintArea` 以包含这些单元格。否则在导出时图表可能会丢失数据系列。

### 授权注意事项

Aspose 库在评估模式下会显示水印。要去除水印，请在任何 API 调用之前设置授权：

```csharp
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

如果使用 Aspose.Slides 的高级功能，也请同样设置授权。

## 专业技巧

- **复用导出选项：** 创建单个 `ImageOrPrintOptions` 实例并分配给每个工作表，以保持代码 DRY。  
- **批量处理：** 对于大规模报告，可将此导出逻辑与后台工作者或 Azure Function 结合，实现按需生成 PPTX 文件。  
- **性能：** 如果只需要图表图像（而非可编辑），将 `ExportEditableShapes = false`。这可降低内存使用并加快转换速度。  
- **测试：** 在 Windows 和 macOS 的 PowerPoint 上验证生成的 PPTX，因为某些渲染细节在平台之间有所不同。

## 结论

现在，您已经拥有使用 C# 完成 **export Excel chart to PowerPoint** 的完整端到端解决方案。教程涵盖了加载工作簿、选择打印区域、配置带 **editable shapes in PowerPoint** 的 **Aspose.Cells PPTX export**，以及将结果保存为完全可编辑的 PPTX 文件。

接下来，您可以探索更多 **Excel to PowerPoint conversion** 场景，例如批量导出、自定义幻灯片布局或将该过程集成到 Web API 中。尝试不同的图表类型、添加图片，或将多个工作表合并为一个演示文稿，以满足业务需求。

准备好自动化您的报告工作流了吗？尝试更换源文件、调整打印区域，并将代码集成到现有的 .NET 服务中。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于所示技术进行扩展。每个资源都提供完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [如何使用 Aspose.Cells for .NET 将 Excel 转换为 PowerPoint：完整指南](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [如何使用 Aspose.Cells for .NET 将 Excel 图表导出为 PDF：分步指南](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [使用 Aspose.Cells .NET 将 Excel 单元格导出为图像：分步指南](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}