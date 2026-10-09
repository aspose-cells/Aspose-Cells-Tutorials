---
category: general
date: 2026-06-27
description: 如何使用 C# 导出 Excel——学习将 Excel 转换为 PowerPoint、从 Excel 创建 PowerPoint，以及在几分钟内使用
  C# 加载 Excel 工作簿。
draft: false
keywords:
- how to export excel
- convert excel to powerpoint
- create powerpoint from excel
- load excel workbook c#
- export excel chart powerpoint
language: zh
og_description: 使用 C# 导出 Excel 很简单。请按照本分步教程，将 Excel 转换为 PowerPoint、从 Excel 创建 PowerPoint，并在
  C# 中加载 Excel 工作簿。
og_title: 如何将 Excel 导出到 PowerPoint – 完整 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to export Excel using C#—learn to convert Excel to PowerPoint,
    create PowerPoint from Excel, and load Excel workbook C# in minutes.
  headline: How to Export Excel to PowerPoint – Complete C# Guide
  type: TechArticle
- description: How to export Excel using C#—learn to convert Excel to PowerPoint,
    create PowerPoint from Excel, and load Excel workbook C# in minutes.
  name: How to Export Excel to PowerPoint – Complete C# Guide
  steps:
  - name: '**Load Excel workbook** – We read the `.xlsx` file into memory.'
    text: '**Load Excel workbook** – We read the `.xlsx` file into memory.'
  - name: '**Convert workbook to a PowerPoint presentation** – Aspose converts each
      worksheet (or selected chart) into a slide.'
    text: '**Convert workbook to a PowerPoint presentation** – Aspose converts each
      worksheet (or selected chart) into a slide.'
  - name: '**Save the generated presentation** – The final PPTX can be opened in PowerPoint,
      edited, or sent to stakeholders.'
    text: '**Save the generated presentation** – The final PPTX can be opened in PowerPoint,
      edited, or sent to stakeholders.'
  type: HowTo
- questions:
  - answer: Yes. Use `Workbook.Worksheets["Sheet1"]` to isolate a sheet, then call
      `SaveToPresentation` on that worksheet alone.
    question: Can I export only a single worksheet instead of the whole workbook?
  - answer: Macros are not transferred to PowerPoint—only visual objects (charts,
      tables) are exported. If you need macro functionality, consider generating the
      slides first, then adding VBA manually.
    question: What about preserving macros?
  - answer: Absolutely. Aspose.Cells supports legacy formats; just change the file
      extension in `excelPath`.
    question: Does this work with `.xls` files?
  - answer: 'After creating the `Presentation` object, set: ```csharp presentation.SlideSize.Size
      = SlideSizeType.Widescreen; ```'
    question: How do I change the slide size to widescreen (16:9)?
  - answer: 'Open‑source libraries like EPPlus can read Excel, but they don’t provide
      direct Excel‑to‑PowerPoint conversion. You’d need to manually render charts
      to images and insert them, which is far more code. ## Tips & Best Practices
      - **Batch processing:** If you have dozens of workbooks, wrap the conversio'
    question: Is there a free alternative?
  type: FAQPage
tags:
- C#
- Excel
- PowerPoint
- Aspose
title: 如何将 Excel 导出到 PowerPoint – 完整 C# 指南
url: /zh/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何将 Excel 导出到 PowerPoint – 完整 C# 指南

是否曾想过 **如何将 Excel** 数据直接导入 PowerPoint 幻灯片而不失去格式？你并不是唯一有此需求的人。在许多报告流程中，瓶颈在于将 Excel 工作簿中的图表和表格搬到精美的幻灯片中。好消息是，只需几行 C# 代码，你就可以 **将 Excel 转换为 PowerPoint**，生成可完全编辑的 PPTX，甚至保留图表的细节。

在本教程中，我们将演示如何在 C# 中加载 Excel 工作簿，将其内容转换为 PowerPoint 演示文稿，并保存结果。完成后，你将能够自动 **从 Excel 创建 PowerPoint**——无需手动复制粘贴。无需繁琐的 UI 操作，只需简洁的代码。

> **你需要的条件**  
> * .NET 6+（或 .NET Framework 4.7.2+）  
> * Aspose.Cells 和 Aspose.Slides NuGet 包（它们负责繁重的工作）  
> * 一个包含至少一个图表的示例 Excel 文件（我们称之为 `chartOle.xlsx`）  

如果你已经准备好这些，让我们开始吧。

![展示如何使用 C# 将 Excel 导出到 PowerPoint 的示意图](https://example.com/images/export-excel-to-pptx.png "如何将 Excel 导出到 PowerPoint 的示意图")

## 使用 C# 将 Excel 导出到 PowerPoint – 概览

在开始编码之前，了解三步流程会很有帮助：

1. **加载 Excel 工作簿** – 我们将 `.xlsx` 文件读取到内存中。  
2. **将工作簿转换为 PowerPoint 演示文稿** – Aspose 将每个工作表（或选定的图表）转换为一张幻灯片。  
3. **保存生成的演示文稿** – 最终的 PPTX 可以在 PowerPoint 中打开、编辑或发送给相关方。  

每一步都被刻意独立，以便后续可以替换自定义逻辑（例如，选择特定工作表、应用幻灯片主题等）。现在让我们逐步拆解。

## 步骤 1 – 使用 C# 加载 Excel 工作簿

首先要做的事是将 Excel 文件加载到你的应用程序中。使用 Aspose.Cells，代码非常简洁：

```csharp
using Aspose.Cells;   // Handles Excel files
using Aspose.Slides;  // Handles PowerPoint files
using System;

// Step 1: Load the Excel workbook
string excelPath = @"YOUR_DIRECTORY\chartOle.xlsx";

if (!System.IO.File.Exists(excelPath))
{
    throw new FileNotFoundException($"Excel file not found at {excelPath}");
}

// The Workbook class reads the .xlsx file into memory
Workbook workbook = new Workbook(excelPath);
```

**为什么这很重要：**  
`Workbook` 抽象了整个电子表格，提供对工作表、单元格以及——关键的——嵌入图表的访问。如果跳过存在性检查，稍后会出现模糊的 `FileNotFoundException`，在生产环境中调试会非常头疼。

**专业提示：** 如果只需要特定工作表，可以传入 `LoadOptions` 对象以限制内存使用：

```csharp
LoadOptions options = new LoadOptions(LoadFormat.Xlsx) { LoadDataOnly = true };
Workbook workbook = new Workbook(excelPath, options);
```

这个小技巧可以显著加快大型工作簿的加载速度。

## 步骤 2 – 将 Excel 转换为 PowerPoint（导出 Excel 图表到 PowerPoint）

现在进入魔法环节：将工作簿转换为 PPTX。Aspose.Slides 提供了一个一次性完成繁重工作的单一方法：

```csharp
// Step 2: Convert the workbook to a PowerPoint presentation (PPTX format)
Presentation presentation = workbook.SaveToPresentation(ExportToPresentationFormat.Pptx);
```

**内部实际在做什么？**  
`SaveToPresentation` 会遍历每个工作表，提取其中的图表对象，并为每个图表创建一张幻灯片。该方法保持原始图表的样式，颜色、字体和数据标签都保持不变。如果工作簿中包含普通表格，它们将以文本框的形式渲染在幻灯片上。

**边缘情况 – 多个图表：**  
如果一个工作表中有多个图表，Aspose 会将它们垂直堆叠在同一张幻灯片上。若想让每个图表单独占一张幻灯片，可以手动遍历图表：

```csharp
Presentation presentation = new Presentation();

foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (Chart chart in sheet.Charts)
    {
        // Export each chart as an individual slide
        ISlide slide = presentation.Slides.AddEmptySlide(presentation.SlideSize.Size);
        chart.ExportToSlide(presentation, slide);
    }
}
```

该代码片段提供了细粒度的控制——非常适合打造精致的幻灯片。

## 步骤 3 – 保存生成的演示文稿（从 Excel 创建 PowerPoint）

最后一步是将 PPTX 文件持久化到磁盘。操作非常简单：

```csharp
// Step 3: Save the generated presentation to a file
string pptxPath = @"YOUR_DIRECTORY\editable.pptx";
presentation.Save(pptxPath, Aspose.Slides.Export.SaveFormat.Pptx);

Console.WriteLine($"Presentation saved successfully to {pptxPath}");
```

**为何需要验证输出：**  
保存后，在 PowerPoint 中打开 `editable.pptx`。你应该会看到每个图表对应一张幻灯片，且全部可编辑（可以更改颜色、移动对象等）。如果某个图表显示异常，请再次确认原始 Excel 图表使用的是标准字体——某些自定义字体可能无法正确嵌入。

**常见陷阱：**  
将文件保存到没有适当权限的网络共享会抛出 `UnauthorizedAccessException`。确保运行账户对 `YOUR_DIRECTORY` 具有写入权限。

## 完整示例 – 步骤汇总

下面是完整的可直接运行的程序。将其粘贴到新的控制台应用项目中，恢复 NuGet 包，然后按 **F5** 运行。

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Paths – adjust to your environment
            string excelPath = @"YOUR_DIRECTORY\chartOle.xlsx";
            string pptxPath = @"YOUR_DIRECTORY\editable.pptx";

            // -------------------------------------------------
            // Step 1: Load the Excel workbook (load excel workbook c#)
            // -------------------------------------------------
            if (!System.IO.File.Exists(excelPath))
            {
                Console.WriteLine($"Error: File not found -> {excelPath}");
                return;
            }

            Workbook workbook = new Workbook(excelPath);
            Console.WriteLine("Excel workbook loaded successfully.");

            // -------------------------------------------------
            // Step 2: Convert Excel to PowerPoint (export excel chart powerpoint)
            // -------------------------------------------------
            Presentation presentation = workbook.SaveToPresentation(ExportToPresentationFormat.Pptx);
            Console.WriteLine("Workbook converted to PowerPoint.");

            // -------------------------------------------------
            // Step 3: Save the generated presentation (create powerpoint from excel)
            // -------------------------------------------------
            presentation.Save(pptxPath, Aspose.Slides.Export.SaveFormat.Pptx);
            Console.WriteLine($"Presentation saved at: {pptxPath}");
        }
    }
}
```

**预期输出（控制台）：**

```
Excel workbook loaded successfully.
Workbook converted to PowerPoint.
Presentation saved at: YOUR_DIRECTORY\editable.pptx
```

打开 `editable.pptx`，你会看到每个图表对应一张幻灯片，已准备好进一步调整。

## 常见问题 (FAQs)

**问：我可以只导出单个工作表而不是整个工作簿吗？**  
答：可以。使用 `Workbook.Worksheets["Sheet1"]` 来定位特定工作表，然后仅对该工作表调用 `SaveToPresentation`。

**问：宏会被保留吗？**  
答：宏不会转移到 PowerPoint——仅导出可视对象（图表、表格）。如果需要宏功能，建议先生成幻灯片，然后手动添加 VBA。

**问：这能用于 `.xls` 文件吗？**  
答：完全可以。Aspose.Cells 支持旧版格式，只需在 `excelPath` 中更改文件扩展名即可。

**问：如何将幻灯片尺寸改为宽屏（16:9）？**  
答：在创建 `Presentation` 对象后，设置：

```csharp
presentation.SlideSize.Size = SlideSizeType.Widescreen;
```

**问：有没有免费替代方案？**  
答：像 EPPlus 这样的开源库可以读取 Excel，但不提供直接的 Excel 到 PowerPoint 转换。你需要手动将图表渲染为图像并插入，这会涉及大量代码。

## 提示与最佳实践

- **批量处理：** 如果有数十个工作簿，可将转换包装在 `Parallel.ForEach` 循环中——但要注意 Aspose 对象的线程不安全性。  
- **内存管理：** 处理大文件时，调用 `presentation.Dispose()` 和 `workbook.Dispose()` 及时释放本机资源。  
- **幻灯片样式化：** 转换后，可使用 `presentation.SlideMaster` 应用母版主题，使所有幻灯片保持一致的外观。  
- **测试：** 自动化一个简单的单元测试，加载已知工作簿，执行转换，并断言生成的 PPTX 包含预期数量的幻灯片。

## 结论

我们已经演示了如何使用 C# **将 Excel** 数据导入 PowerPoint 幻灯片。通过加载工作簿、使用 Aspose 进行转换并保存 PPTX，你现在拥有一种可重复、可编程的方式来 **将 Excel 转换为 PowerPoint**、**从 Excel 创建 PowerPoint**，以及 **以 C# 方式加载 Excel 工作簿**，无需手动操作。代码是自包含的，兼容任何现代 .NET 运行时，并可扩展以适应复杂的报告流水线。

准备好迎接下一个挑战了吗？尝试在一张幻灯片中嵌入多个图表、应用自定义幻灯片布局，甚至自动生成演讲者备注。当你将 Excel 自动化与 PowerPoint 生成相结合时，可能性无限。

有任何问题或酷炫的使用案例吗？在下方留言吧，祝编码愉快！

## 接下来该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于所示技术进行扩展。每个资源均包含完整的可运行代码示例和逐步说明，帮助你掌握更多 API 功能，并在项目中探索替代实现方案。

- [如何使用 Aspose.Cells for .NET 将 Excel 转换为 PowerPoint：完整指南](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [如何使用 Aspose.Cells for .NET 将 Excel 图表导出为 PDF：分步指南](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [如何使用 Aspose.Cells for .NET 将 Excel 导出为带网格线的 HTML](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}