---
category: general
date: 2026-11-16
description: 了解如何将 Excel 保存为 PowerPoint 并以编程方式将 Excel 转换为 PowerPoint。本分步指南还涵盖将 Excel
  导出为 PPTX 以及将工作簿保存为 PPTX。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- export excel to pptx
- how to convert excel slide
- save workbook as pptx
language: zh
lastmod: 2026-11-16
og_description: 使用 Aspose.Cells 将 Excel 保存为 PowerPoint。按照本指南，将 Excel 转换为 PowerPoint，导出
  Excel 为 PPTX，并在几分钟内将工作簿保存为 PPTX。
og_image_alt: Screenshot showing the result of saving Excel as PowerPoint with editable
  shapes
og_title: 将 Excel 保存为 PowerPoint – 完整 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to save Excel as PowerPoint and convert Excel to PowerPoint
    programmatically. This step‑by‑step guide also covers export Excel to PPTX and
    saving a workbook as PPTX.
  headline: How to save Excel as PowerPoint with Aspose.Cells in C#
  type: TechArticle
tags:
- Excel
- PowerPoint
- Aspose.Cells
- C#
- Export
title: 如何使用 Aspose.Cells 在 C# 中将 Excel 保存为 PowerPoint
url: /zh/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-with-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.Cells 在 C# 中将 Excel 保存为 PowerPoint

如果您需要以编程方式 **将 Excel 保存为 PowerPoint**，本教程为您提供一个完整、可直接运行的解决方案。无论您是在构建报表引擎还是自动化幻灯片生成器，下面的步骤都能让您仅用几行代码将 Excel 工作表转换为可编辑的 PPTX 幻灯片。

您将学习如何 **将 Excel 转换为 PowerPoint**，将工作表导出为 PPTX 文件，并保持文本框和形状可编辑——全部在 .NET 环境中完成。

## 前提条件

在开始之前，请确保您具备：

* .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.7.2+）
* 有效的 Aspose.Cells 许可证（免费试用可用于评估）
* Visual Studio 2022（或任何 C# IDE）
* 包含您想要导出的数据和形状的 Excel 工作簿

## 步骤 1：安装 Aspose.Cells

将 Aspose.Cells NuGet 包添加到您的项目中：

```bash
dotnet add package Aspose.Cells
```

> **小技巧：** 使用 `-v` 标志指定特定版本，例如 `Aspose.Cells.24.5`。

## 步骤 2：加载要导出的工作簿

在 **将 Excel 保存为 PowerPoint** 工作流中的第一步是加载源工作簿。

```csharp
using Aspose.Cells;
using System;

// Load the workbook that contains the shapes
Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");
```

*为什么重要：* 加载工作簿后，您可以访问其工作表、页面设置以及将成为可编辑 PowerPoint 形状的绘图对象。

## 步骤 3：为可编辑的 PPTX 幻灯片配置导出选项

要在 **将 Excel 转换为 PowerPoint** 时保持可编辑性，必须在 `ImageOrPrintOptions` 上设置若干属性。

```csharp
// Prepare export options to generate an editable PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // Export format
    ExportEditableText = true,        // Keep text boxes editable
    ExportEditableShapes = true       // Keep shapes editable
};
```

*说明：*  
* `SaveFormat = SaveFormat.Pptx` 告诉 Aspose.Cells 生成 PowerPoint 文件。  
* `ExportEditableText` 和 `ExportEditableShapes` 确保生成的幻灯片表现得像原生 PowerPoint 幻灯片——您可以点击文本框或形状并直接在 PowerPoint 中编辑它们。

## 步骤 4：定义导出区域并适配为单张幻灯片

当您 **将 Excel 导出为 PPTX** 时，通常希望特定范围出现在幻灯片上。设置打印区域和适配选项可确保输出整洁、仅一张幻灯片。

```csharp
// Define the area of the first worksheet to export
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G30";

// Fit the exported content to a single slide
sheet.PageSetup.FitToPagesTall = 1;
sheet.PageSetup.FitToPagesWide = 1;
```

*为什么重要：* `PrintArea` 将导出限制在 A1 到 G30 单元格范围内，而 `FitToPagesTall` 和 `FitToPagesWide` 将所有内容压缩到一张幻灯片，防止出现不需要的额外页。

## 步骤 5：将工作表保存为可编辑的 PPTX 文件

现在您终于可以 **将工作簿保存为 PPTX**，完成 **将 Excel 保存为 PowerPoint** 的整个过程。

```csharp
// Save the worksheet as an editable PPTX file
workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
Console.WriteLine("Export completed: EditableShapes.pptx");
```

运行程序后，在 Microsoft PowerPoint 中打开 `EditableShapes.pptx`。您会看到一张与所选 Excel 范围相对应的幻灯片，所有文本框和形状均可完全编辑。

### 预期输出

* 一个名为 `EditableShapes.pptx` 的文件，位于 `C:\Output\`。
* 包含 A1:G30 范围的单张 PowerPoint 幻灯片。
* 文本框、图表和形状，您可以双击并直接在 PowerPoint 中编辑。

## 完整源代码（可直接复制）

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the shapes
            Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");

            // Step 2: Prepare export options to generate an editable PPTX slide
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportEditableText = true,   // keep text boxes editable
                ExportEditableShapes = true  // keep shapes editable
            };

            // Step 3: Define the area of the first worksheet to export
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";

            // Step 4: Fit the exported content to a single slide
            sheet.PageSetup.FitToPagesTall = 1;
            sheet.PageSetup.FitToPagesWide = 1;

            // Step 5: Save the worksheet as an editable PPTX file
            workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
            Console.WriteLine("Export completed: EditableShapes.pptx");
        }
    }
}
```

## 常见问题与边缘情况处理

| Question | Answer |
|----------|--------|
| **如果我有多个工作表怎么办？** | 遍历 `workbook.Worksheets`，对每个工作表重复步骤 3‑5，并更改输出文件名（例如 `Sheet1.pptx`、`Sheet2.pptx`）。 |
| **我能将整个工作簿导出为单个 PowerPoint 演示文稿吗？** | 可以。 在 `ImageOrPrintOptions` 上设置 `ExportAllSheets = true`。每个工作表将成为单独的幻灯片。 |
| **我的形状显示为图像，而不是可编辑对象。** | 确保 `ExportEditableShapes = true`，并使用 Aspose.Cells 24.5+（早期版本不具备此功能）。 |
| **生成的 PPTX 文件太大。** | 缩小打印区域，或通过 `exportOptions.ImageResolution` 降低图像分辨率。 |
| **生产环境是否需要许可证？** | 付费许可证会去除评估水印并解锁全部性能。免费试用可用于测试。 |

## 稳健生产代码的技巧

* **验证文件路径** 在调用 `Workbook` 或 `Save` 之前，以避免 `FileNotFoundException`。  
* **将导出代码放入 try/catch 块**，以处理许可证错误（`Aspose.Cells.LicenseException`）。  
* **在完成后释放工作簿**（`workbook.Dispose()`），以释放非托管资源。  
* **使用异步 I/O**（`FileStream` 搭配 `await`），如果在 Web 服务中导出大量大型工作表。

## 后续步骤

既然您已经了解如何 **将 Excel 保存为 PowerPoint**，可以进一步探索相关主题：

* **使用自定义幻灯片布局导出 Excel 为 PPTX** – 调整 `SlideSize` 并添加母版幻灯片。  
* **将 Excel 幻灯片转换为 PDF** – 使用 `SaveFormat.Pdf` 获取可打印版本。  
* **批量转换文件夹中的工作簿** – 将上述循环与 `Directory.GetFiles` 结合使用。  

尝试不同的打印区域、缩放选项和 PowerPoint 主题，以使输出符合贵组织的品牌形象。

---

*祝编码愉快！如果本指南帮助您 **将 Excel 转换为 PowerPoint**，欢迎与团队成员分享，或在 Aspose.Cells 的 GitHub 仓库中提交 issue 以获取进一步帮助。*

## 接下来您应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于所示技术进行扩展。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [如何使用 C# 和 Aspose.Cells 将 Excel 保存为 PowerPoint](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/)
- [如何从 Excel 保存 PPTX – 导出 Excel 工作表为 PowerPoint 的完整指南](/cells/english/java/integration-interoperability/how-to-save-pptx-from-excel-complete-guide-to-export-excel-s/)
- [将 Excel 转换为 PowerPoint – 完整分步指南](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-full-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}