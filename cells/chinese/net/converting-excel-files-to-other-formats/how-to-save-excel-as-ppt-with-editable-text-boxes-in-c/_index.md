---
category: general
date: 2026-10-07
description: 在 C# 中将 Excel 保存为 PPT，同时保持文本框和形状可编辑。一步步学习如何使用 Aspose.Cells 将 Excel 转换为
  PowerPoint。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as ppt
- convert excel to powerpoint
- how to export excel
- how to keep textboxes
- convert spreadsheet to presentation
language: zh
lastmod: 2026-10-07
og_description: 在 C# 中将 Excel 保存为 PPT，同时保留文本框和形状。请按照本完整教程，将 Excel 转换为 PowerPoint，实现完整可编辑性。
og_image_alt: Diagram of Excel workbook being saved as PPT with editable text boxes
og_title: 将Excel保存为PPT – 可编辑转换指南
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Save Excel as PPT in C# while keeping text boxes and shapes editable.
    Learn step‑by‑step how to convert Excel to PowerPoint using Aspose.Cells.
  headline: How to save Excel as PPT with editable text boxes in C#
  type: TechArticle
- description: Save Excel as PPT in C# while keeping text boxes and shapes editable.
    Learn step‑by‑step how to convert Excel to PowerPoint using Aspose.Cells.
  name: How to save Excel as PPT with editable text boxes in C#
  steps:
  - name: Why each line matters
    text: 1. **Loading the workbook** – `Workbook` reads the `.xlsx` file into memory,
      giving you full access to worksheets, charts, and embedded objects. 2. **Configuring
      `PptxSaveOptions`** – Setting `ExportTextBoxesAsEditable` and `ExportShapesAsEditable`
      tells Aspose.Cells to write those objects as native
  - name: Tips for large files
    text: '- **Memory management:** Call `GC.Collect()` after the conversion if you
      process many files in a batch. - **Image quality:** Use `opts.ImageResolution
      = 300` to increase chart clarity when the source contains high‑resolution graphics.
      - **Performance:** Set `opts.CompressionLevel = CompressionLevel.'
  - name: 'Edge case: Converting a macro‑enabled workbook (`.xlsm`)'
    text: Aspose.Cells can read `.xlsm` files, but macros are **not** transferred
      to the PPTX because PowerPoint does not support VBA macros from Excel. If you
      need the macro logic, consider exporting the relevant data first, then recreating
      the macro in PowerPoint VBA manually.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel‑to‑PowerPoint
- document‑conversion
title: 如何在 C# 中将 Excel 保存为 PPT 并保留可编辑的文本框
url: /zh/net/converting-excel-files-to-other-formats/how-to-save-excel-as-ppt-with-editable-text-boxes-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中将 Excel 保存为 PPT 并保留可编辑的文本框

如果您需要 **将 Excel 保存为 PPT** 并保持所有文本框和形状可编辑，本指南将为您详细演示。使用 Aspose.Cells for .NET，您可以通过几行代码 **将 Excel 转换为 PowerPoint**，保留原始布局，使生成的演示文稿在 PowerPoint 中可编辑且不丢失任何对象。

除了转换本身，您还将学习 **如何导出 Excel** 并保留文本框，如何保持文本框可编辑，以及 **如何将电子表格转换为演示文稿**，该方法适用于大型工作簿和复杂图表。

## 您需要的环境

- .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.6+）
- Aspose.Cells for .NET 许可证（免费试用可用于评估）
- Visual Studio 2022（或任何支持 C# 的 IDE）
- 包含文本框、形状或图表的示例 Excel 文件（例如 `WithTextBoxes.xlsx`）

> **小技巧：** 如果您使用免费试用版，请在程序早期调用 `License.SetLicense("Aspose.Total.lic")` 以避免评估水印。

## 如何在保留文本框的情况下将 Excel 保存为 PPT

本节直接针对主要关键词 **save Excel as PPT**。下面的代码是完整的可运行示例，您可以将其粘贴到新的控制台项目中。

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Presentation;

class Program
{
    static void Main()
    {
        // Step 1: Load the Excel workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/WithTextBoxes.xlsx");

        // Step 2: Configure PPTX save options to keep text boxes and shapes editable
        PptxSaveOptions saveOptions = new PptxSaveOptions
        {
            ExportTextBoxesAsEditable = true,   // how to keep textboxes editable
            ExportShapesAsEditable = true       // also keep shapes editable
        };

        // Step 3: Save the workbook as an editable PowerPoint presentation
        workbook.Save("YOUR_DIRECTORY/ExportEditable.pptx", saveOptions);

        Console.WriteLine("Excel file has been successfully saved as PPT.");
    }
}
```

### 为什么每一行都很重要

1. **加载工作簿** – `Workbook` 将 `.xlsx` 文件读取到内存中，让您能够完整访问工作表、图表和嵌入对象。  
2. **配置 `PptxSaveOptions`** – 设置 `ExportTextBoxesAsEditable` 和 `ExportShapesAsEditable` 告诉 Aspose.Cells 将这些对象写为原生 PowerPoint 形状，而不是扁平化的图像。这是 **如何保持文本框** 在转换后可编辑的关键。  
3. **保存为 PPTX** – 使用 `PptxSaveOptions` 对象的 `Save` 方法执行实际的 **convert Excel to PowerPoint** 操作。输出文件（`ExportEditable.pptx`）可以在 Microsoft PowerPoint 中打开并像任何原生演示文稿一样进行编辑。

> **注意：** 输出保留了原始的列宽、行高和单元格格式，因此视觉布局与源 Excel 表完全一致。

![成功转换的控制台输出截图](/images/save-excel-as-ppt-console.png "将 Excel 保存为 PPT 后的控制台输出")

*图片替代文字：控制台窗口显示 “Excel file has been successfully saved as PPT.”*

## 将 Excel 转换为 PowerPoint – 处理大型工作簿

当您 **convert spreadsheet to presentation** 包含多个工作表时，您可能希望每个工作表生成单独的幻灯片。Aspose.Cells 会自动完成此操作，但您可以对行为进行微调：

```csharp
// Create save options with a custom slide layout
PptxSaveOptions opts = new PptxSaveOptions
{
    ExportTextBoxesAsEditable = true,
    ExportShapesAsEditable = true,
    // Each worksheet becomes a new slide (default behavior)
    // You can also set opts.OnePagePerSheet = false to merge sheets
};
workbook.Save("LargeExport.pptx", opts);
```

### 大文件的技巧

- **内存管理：** 如果批量处理多个文件，转换后调用 `GC.Collect()`。  
- **图像质量：** 当源包含高分辨率图形时，使用 `opts.ImageResolution = 300` 提高图表清晰度。  
- **性能：** 设置 `opts.CompressionLevel = CompressionLevel.Maximum` 可在不影响可编辑性的前提下降低 PPTX 文件大小。

## 如何在保留公式和图表的情况下导出 Excel

如果工作簿中包含公式，转换过程中会对其进行求值，结果值会出现在幻灯片上。原始公式 **不会** 被转移，因为 PowerPoint 本身不支持 Excel 公式。不过，您可以将源工作簿与演示文稿保持链接：

```csharp
PptxSaveOptions linkedOpts = new PptxSaveOptions
{
    ExportTextBoxesAsEditable = true,
    ExportShapesAsEditable = true,
    // Keep a link to the original Excel file for future updates
    LinkToSource = true
};
workbook.Save("LinkedExport.pptx", linkedOpts);
```

当用户在 PowerPoint 中打开 PPTX 时，会出现提示询问是否更新链接数据。这满足了 **how to export Excel** 的需求，同时仍然允许后续编辑。

## 常见陷阱及如何保持文本框完整

| 症状 | 原因 | 解决方案 |
|------|------|----------|
| 文本框显示为图像 | `ExportTextBoxesAsEditable` 保持默认 `false` | 设置 `ExportTextBoxesAsEditable = true` |
| 形状在 PowerPoint 中无法移动 | `ExportShapesAsEditable` 未启用 | 启用 `ExportShapesAsEditable = true` |
| 缺少图表图例 | 图表使用转换器不支持的自定义主题 | 在转换前应用标准主题 |
| 演示文稿为空白 | 工作簿路径不正确或文件被锁定 | 检查路径并确保文件未在其他位置打开 |

### 边缘情况：转换宏启用工作簿（`.xlsm`）

Aspose.Cells 可以读取 `.xlsm` 文件，但宏 **不会** 转移到 PPTX，因为 PowerPoint 不支持来自 Excel 的 VBA 宏。如果您需要宏逻辑，建议先导出相关数据，然后手动在 PowerPoint VBA 中重新创建宏。

## 验证输出 – 正确将电子表格转换为演示文稿

运行代码后，在 PowerPoint 中打开 `ExportEditable.pptx`：

1. **选择文本框** – 您应该看到常规的调整大小手柄，确认该对象可编辑。  
2. **右键单击形状** – 上下文菜单会显示 PowerPoint 形状选项（填充、线条等）。  
3. **检查幻灯片顺序** – 每个工作表应对应一张幻灯片，保留原始的标签顺序。

如果有任何对象不可编辑，请再次检查 `PptxSaveOptions` 标志。默认值（`false`）会导致转换器将对象光栅化，这就是为何将其设为 `true` 对于 **how to keep textboxes** 要求至关重要。

## 生产环境的最佳实践

- **尽早授权：** `License license = new License(); license.SetLicense("Aspose.Total.lic");`  
- **异常处理：** 将转换包装在 `try/catch` 块中，以捕获文件访问错误。  
- **日志记录：** 记录源路径和目标路径以及时间戳，以便审计追踪。  
- **单元测试：** 使用包含已知对象的小工作簿，断言生成的 PPTX 包含预期数量的可编辑形状。

```csharp
try
{
    // Conversion code from earlier sections
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Conversion failed: {ex.Message}");
    // Optionally rethrow or handle according to your error policy
}
```

## 结论

现在，您已经拥有一个完整的、可投入生产的解决方案，可 **将 Excel 保存为 PPT**，同时保留文本框、形状和整体布局。通过配置 `PptxSaveOptions`，您可以控制 **how to keep textboxes** 的可编辑性，实现转换后在 PowerPoint 中的无缝编辑。同样的方法还可以 **convert Excel to PowerPoint**、**export Excel** 数据以及 **convert spreadsheet to presentation**，适用于任何规模的工作簿。

接下来，您可以探索相关主题，例如 **将 Excel 图表导出为高分辨率图像**、**批量转换多个工作簿**，或 **将生成的 PPTX 嵌入到 Web 应用程序**。这些内容都基于本指南的基础，进一步发挥 Aspose.Cells 在实际文档自动化场景中的强大功能。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南技术密切相关的主题，帮助您进一步学习。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在自己的项目中探索替代实现方法。

- [如何使用 Aspose.Cells for .NET 将 Excel 转换为 PowerPoint：完整指南](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [如何使用 Aspose.Cells .NET 在 Excel 中添加和访问文本框 | 步骤指南](/cells/english/net/images-shapes/aspose-cells-net-add-text-boxes-excel/)
- [如何使用 Aspose.Cells .NET 将 Excel 工作表转换为图像（步骤指南）](/cells/english/net/workbook-operations/convert-excel-sheets-images-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}