---
category: general
date: 2026-02-09
description: 几分钟内将 Excel 创建为 PowerPoint——学习如何将 Excel 转换为 PowerPoint，并使用简单的 C# 代码示例将
  Excel 导出为 PPT。
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export excel to ppt
- generate ppt from excel
- how to convert excel to pptx
language: zh
og_description: 快速从 Excel 创建 PowerPoint。本指南展示了如何将 Excel 转换为 PowerPoint、将 Excel 导出为
  PPT，以及使用 C# 从 Excel 生成 PPT。
og_title: 从 Excel 创建 PowerPoint – 完整编程指南
tags:
- C#
- Aspose.Cells
- PowerPoint automation
- Office interop
title: 从Excel创建PowerPoint – 步骤指南
url: /zh/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 从 Excel 创建 PowerPoint – 完整编程指南

是否曾经需要**从 Excel 创建 PowerPoint**但不确定该调用哪个 API？你并不孤单。许多开发者在想将电子表格转换为幻灯片而不进行手动复制粘贴时会遇到瓶颈。  

好消息：只需几行 C# 代码，你就可以**将 Excel 转换为 PowerPoint**，导出工作表中的形状，并得到一个可直接演示的 PPTX 文件。在本教程中，我们将完整演示整个过程，解释每一步的意义，并展示如何处理最常见的坑点。

## 你将学到

- 如何加载包含图表、图片或 SmartArt 的 Excel 工作簿。  
- 使用 Aspose.Cells 库**导出 Excel 为 PPT**的精确调用方式。  
- 如何保存生成的演示文稿并验证结果。  
- 处理没有形状的工作簿、调整幻灯片尺寸以及排查版本不匹配的技巧。

无需外部工具，无需 COM 互操作，只需纯 .NET 代码，支持 .NET Core 或 .NET 5+ 的任何环境即可运行。

---

## 前置条件

在开始之前，请确保你拥有：

1. **Aspose.Cells for .NET**（提供 `SaveToPresentation` 的库）。可通过 NuGet 获取：  

   ```bash
   dotnet add package Aspose.Cells
   ```
2. 最近的 .NET SDK（推荐 6.0 或更高）。  
3. 一个 Excel 文件（`shapes.xlsx`），其中至少包含一个你希望在幻灯片中显示的形状、图表或图片。

就这些——无需安装 Office，也不需要为本示例额外处理授权（免费评估版完全足够）。

---

## 第 1 步：加载 Excel 工作簿（Create PowerPoint from Excel）

我们首先需要一个指向源文件的 `Workbook` 对象。该对象代表整个 Excel 文档，包括所有工作表、图表和嵌入对象。

```csharp
using Aspose.Cells;
using Aspose.Slides;

// Step 1: Load the Excel workbook containing the shapes
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\shapes.xlsx");

// Why this matters:
// - `Workbook` abstracts the file format, so you don’t have to worry about .xls vs .xlsx.
// - Loading the file early lets you inspect its contents (e.g., count of worksheets) before conversion.
```

> **小贴士：** 如果不确定文件是否存在，可将构造函数放在 `try/catch` 中并提供友好的错误信息。这样可以避免后期出现晦涩的 `FileNotFoundException`。

---

## 第 2 步：将工作簿转换为 PowerPoint 演示文稿（Export Excel to PPT）

Aspose.Cells 内置了一个导出器，可将整个工作簿或选定的工作表转换为 PowerPoint 演示文稿。`SaveToPresentation` 方法负责完成这项繁重工作。

```csharp
// Step 2: Convert the workbook to a PowerPoint presentation (PPTX format)
Presentation presentation = workbook.SaveToPresentation(ExportTo.Pptx);

// How it works:
// - Each worksheet becomes a separate slide.
// - Shapes, charts, and images are rasterized and placed on the slide preserving their layout.
// - You can later tweak the `Presentation` object (e.g., add a title slide) before saving.
```

如果只需要**从 Excel 生成 ppt**的部分工作表，可以使用接受 `SheetOptions` 集合的重载。对大多数场景而言，默认转换已经足够。

---

## 第 3 步：保存生成的演示文稿（How to Convert Excel to PPTX）

现在我们拥有了 `Presentation` 实例， 将其持久化到磁盘非常简单。输出将是标准的 `.pptx` 文件，任何现代版本的 PowerPoint 都能打开。

```csharp
// Step 3: Save the generated presentation to a file
presentation.Save(@"C:\MyProjects\ExcelToPpt\shapes.pptx");

// Verification:
// Open the file in PowerPoint or use Aspose.Slides to programmatically inspect slide count.
```

> **如果工作簿没有形状怎么办？**  
> 导出器仍会创建幻灯片，但会是空白的。你可以在转换前检查 `workbook.Worksheets[i].Shapes.Count`，决定是否跳过该工作表。

---

## 可选：微调输出（Advanced Export Excel to PPT）

有时默认的幻灯片尺寸（标准 4:3）并不适合宽屏演示。你可以在保存之前调整幻灯片尺寸：

```csharp
// Set slide size to widescreen (16:9)
presentation.SlideSize.SetSize(SlideSizeType.Widescreen, SlideSizeScaleType.DoNotScale);

// Add a custom title slide (optional)
ISlide titleSlide = presentation.Slides.InsertEmptySlide(0, presentation.LayoutSlides[0]);
titleSlide.Shapes.AddAutoShape(ShapeType.Rectangle, 50, 50, 600, 100)
          .TextFrame.Text = "Quarterly Report – Exported from Excel";
```

这些调整展示了**如何将 Excel 转换为 PowerPoint**并获得专业外观，而不仅仅是原始数据的转储。

---

## 完整工作示例（All Steps Combined）

下面是完整的、可直接运行的程序。复制粘贴到控制台应用，修改文件路径后按 **F5** 运行。

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string excelPath = @"C:\MyProjects\ExcelToPpt\shapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2️⃣ Convert to PPTX
            Presentation presentation = workbook.SaveToPresentation(ExportTo.Pptx);

            // Optional: set widescreen layout
            presentation.SlideSize.SetSize(SlideSizeType.Widescreen, SlideSizeScaleType.DoNotScale);

            // Optional: add a title slide
            ISlide titleSlide = presentation.Slides.InsertEmptySlide(0, presentation.LayoutSlides[0]);
            titleSlide.Shapes.AddAutoShape(ShapeType.Rectangle, 50, 50, 600, 100)
                      .TextFrame.Text = "Quarterly Report – Exported from Excel";

            // 3️⃣ Save the PPTX file
            string pptxPath = @"C:\MyProjects\ExcelToPpt\shapes.pptx";
            presentation.Save(pptxPath);

            Console.WriteLine($"✅ Successfully created PowerPoint from Excel! File saved at: {pptxPath}");
        }
    }
}
```

**预期结果：** 在 PowerPoint 中打开 `shapes.pptx`。你会看到每个工作表对应一张幻灯片，保留了原始的图表、图片和其他形状。可选的标题幻灯片会出现在最前面，为整个文稿提供精致的引言。

---

## 常见问题与边缘情况

| 问题 | 回答 |
|----------|--------|
| *如果只需要单个工作表怎么办？* | 使用 `Workbook.Worksheets[0]` 并通过 `SheetOptions` 调用 `SaveToPresentation`。 |
| *能保留 Excel 公式吗？* | 不能——公式会在幻灯片中渲染为静态值。如果需要实时数据，可考虑后期将 PPTX 链接到 Excel 文件。 |
| *这在 Linux/macOS 上能运行吗？* | 能。Aspose.Cells 与平台无关，只需安装 .NET 运行时即可。 |
| *密码保护的工作簿怎么办？* | 在调用 `SaveToPresentation` 前，使用包含密码的 `LoadOptions` 加载。 |
| *为什么会出现空白幻灯片？* | 检查工作簿是否真的包含形状（`Shapes.Count > 0`）。空白幻灯片是为没有形状的工作表创建的。 |

---

## 结论

现在，你已经掌握了使用 C# **从 Excel 创建 PowerPoint**的完整端到端解决方案。通过加载工作簿、调用 `SaveToPresentation` 并保存结果，你可以**将 Excel 转换为 PowerPoint**、**导出 Excel 为 PPT**，以及**从 Excel 生成 PPT**，仅需几行代码。  

接下来，你可以探索：

- 使用 Aspose.Slides 为生成的幻灯片添加动画。  
- 自动化整个流水线（例如，从文件夹读取文件并批量转换）。  
- 将代码集成到 ASP.NET Core API 中，让用户上传 Excel 文件后即时获取 PPTX。

动手试一试，调整幻灯片尺寸，加入自定义标题——输出完全可以根据你的需求进行个性化。有什么问题或遇到困难？在下方留言吧，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}