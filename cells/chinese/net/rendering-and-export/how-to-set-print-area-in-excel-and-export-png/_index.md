---
category: general
date: 2026-09-27
description: 在 Excel 中设置打印区域，并学习如何导出所选单元格的 PNG 图像。本指南还涵盖将范围保存为图像以及向工作表添加图片。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- how to export png
- save range as image
- add picture to worksheet
- export selected cells image
language: zh
lastmod: 2026-09-27
og_description: 在 Excel 中设置打印区域并使用 Aspose.Cells 导出 PNG。按照本分步指南，将范围保存为图像并将图片添加到工作表中。
og_image_alt: Screenshot showing set print area excel and exported PNG file
og_title: 在 Excel 中设置打印区域 – 使用 C# 导出 PNG
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Set print area in Excel and learn how to export PNG images of selected
    cells. This guide also covers saving range as image and adding picture to worksheet.
  headline: How to set print area in Excel and export PNG
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: 如何在 Excel 中设置打印区域并导出 PNG
url: /zh/net/rendering-and-export/how-to-set-print-area-in-excel-and-export-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Excel 中设置打印区域并导出 PNG

如果您需要在创建图像之前 **set print area excel**，本指南将准确展示如何操作。您还将学习如何从特定范围 **how to export png** 文件、**save range as image**，以及在单一、可重复的工作流中 **add picture to worksheet**。

以编程方式使用 Excel 通常意味着您只想将某些单元格（例如数据透视表或图表）转换为图像。通过先定义打印区域，您可以确保导出的 PNG 恰好包含您期望的单元格，既不多也不少。本教程将逐步引导您完成从加载工作簿到保存最终 PNG 文件的每一步，并解释每个设置的意义。

## 前提条件

* 已安装 .NET 6.0 或更高版本  
* Visual Studio 2022（或任何 C# IDE）  
* **Aspose.Cells for .NET** NuGet 包 (`Install-Package Aspose.Cells`)  
* 位于已知目录的 Excel 文件（`input.xlsx`）  

这些要求可确保代码在无需额外配置的情况下运行。

## 步骤 1：加载要处理的工作簿

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Load the workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

`Workbook` 类代表整个 Excel 文件。首先加载它可让您访问工作表、单元格以及页面设置选项。

## 步骤 2：为目标范围 **Set print area excel**

```csharp
// Define the range you want to capture
string printArea = "A1:G20";

// Apply the range as the print area on the first worksheet
workbook.Worksheets[0].PageSetup.PrintArea = printArea;
```

设置 **print area** 告诉 Excel（以及 Aspose.Cells）哪些单元格属于可打印页面。当您随后将工作表导出为图像时，仅渲染该区域，这对于实现干净的 **export selected cells image** 至关重要。

## 步骤 3：配置图像导出选项 – **how to export png**

```csharp
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG ensures lossless quality
    OnePagePerSheet = true           // Export the defined print area as a single page
};
```

`ImageOrPrintOptions` 控制输出格式。选择 `ImageFormat.Png` 可确保获得高分辨率、透明背景的图像，适用于网页和桌面环境。

## 步骤 4：从已定义的范围创建图片并 **add picture to worksheet**

```csharp
// Create a picture object from the selected range
Picture picture = workbook.Worksheets[0].Pictures.Add(
    0,                                     // top‑left row index where the picture will be placed
    0,                                     // top‑left column index where the picture will be placed
    workbook.Worksheets[0].Cells.CreateRange(printArea));
```

`Pictures.Add` 方法将在工作表中插入新图片。通过传入步骤 2 中创建的范围，您可以直接在工作表上 **save range as image**，这在后续需要在工作簿其他位置引用该图片时非常有用。

## 步骤 5：**Save the picture as an image file** – 完成 **export selected cells image** 工作流

```csharp
// Save the picture to disk as a PNG file
picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);
```

调用 `Save` 会使用步骤 3 中定义的选项将图片写入文件系统。生成的 `selected_range.png` 恰好包含由 **set print area excel** 命令定义的单元格。

## 完整、可运行的示例

将所有代码片段组合在一起，即可得到一个紧凑的程序，您可以将其放入任何控制台应用程序中：

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

class ExportExcelRangeAsPng
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Set print area excel
        string printArea = "A1:G20";
        workbook.Worksheets[0].PageSetup.PrintArea = printArea;

        // 3️⃣ Configure how to export png
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            OnePagePerSheet = true
        };

        // 4️⃣ Add picture to worksheet (save range as image)
        Picture picture = workbook.Worksheets[0].Pictures.Add(
            0,
            0,
            workbook.Worksheets[0].Cells.CreateRange(printArea));

        // 5️⃣ Export selected cells image
        picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);

        Console.WriteLine("PNG exported successfully to YOUR_DIRECTORY\\selected_range.png");
    }
}
```

### 预期输出

```
PNG exported successfully to YOUR_DIRECTORY\selected_range.png
```

您将会在 `selected_range.png` 文件中看到仅包含 `input.xlsx` 中 A1 到 G20 单元格的内容。

## 常见陷阱及避免方法

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| 导出的图像包含整张工作表 | 未定义打印区域 | 在创建图片之前确保已 **set print area excel** |
| PNG 模糊 | 默认 DPI 较低 | 将 `imageOptions.DpiX` 和 `imageOptions.DpiY` 设置为更高的值（例如 300） |
| 文件未找到错误 | 目录路径错误 | 使用 `Path.Combine` 或再次确认文件夹是否存在 |
| 图片位置偏移 | 行/列索引不正确 | `Pictures.Add` 的前两个参数是图片放置的左上单元格；保持它们为 `0,0` 可实现干净的导出 |

## 专业提示：一次运行导出多个范围

如果您需要对多个区域 **export selected cells image**，请在循环中重复步骤 2‑5，并在每次迭代中更改 `printArea`。记得为每个图片指定唯一的文件名，否则后续保存会覆盖之前的文件。

## 结论

现在您已经掌握了使用 Aspose.Cells **set print area excel**、配置 **how to export png**、**save range as image** 以及 **add picture to worksheet** 的方法。此端到端解决方案只需几行 C# 代码，即可将任意单元格块转换为高质量的 PNG。

接下来，您可以探索：

* 为导出的 PNG 添加边框或水印（搜索 *add picture to worksheet* 并进行样式设置）
* 直接导出为 PDF 以生成可打印报告（*export selected cells image* → PDF 工作流）
* 在批处理作业中自动化处理多个工作簿的过程

欢迎尝试不同的范围、DPI 设置或图像格式，以满足项目需求。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于所示技术进行扩展。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [在 Excel 中设置打印区域并导出到 PowerPoint – 步骤指南](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [使用 Aspose.Cells Java 将 Excel 打印区域导出为 HTML](/cells/english/java/workbook-operations/export-excel-print-area-html-aspose-cells-java/)
- [如何使用 Aspose.Cells for .NET 在 Excel 中设置打印区域](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}