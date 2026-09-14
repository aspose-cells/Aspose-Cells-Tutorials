---
category: general
date: 2026-09-11
description: 使用 Aspose.Cells 复制数据透视表并将 Excel 导出为 PPTX。学习在 C# 中生成可编辑的 PPTX 并将工作簿保存为
  PPTX。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- export excel to pptx
- generate editable pptx
- save workbook as pptx
- export excel sheet pptx
language: zh
lastmod: 2026-09-11
og_description: 在 C# 中使用 Aspose.Cells 复制数据透视表并将 Excel 导出为 PPTX。只需几行代码即可生成可编辑的 PPTX
  并将工作簿保存为 PPTX。
og_image_alt: Screenshot of copy pivot table code and generated editable PPTX slide
og_title: 复制数据透视表并将 Excel 导出为 PPTX – 完整 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Copy pivot table and export Excel to PPTX using Aspose.Cells. Learn
    to generate editable PPTX and save workbook as PPTX in C#.
  headline: Copy pivot table and export Excel to PPTX with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel
- PPTX
- Pivot Table
title: 使用 Aspose.Cells 复制数据透视表并将 Excel 导出为 PPTX
url: /zh/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 复制数据透视表并将 Excel 导出为 PPTX（使用 Aspose.Cells）

如果您需要将数据透视表从一个工作表复制到另一个工作表，然后将 Excel 文件导出为 PowerPoint 演示文稿，本指南将手把手教您如何操作。使用 Aspose.Cells，您只需几行 C# 代码即可生成可编辑的 PPTX 并将工作簿保存为 PPTX。

本教程涵盖了移动数据透视表、保留其功能以及生成 PPTX 文件（其中图表和形状保持可编辑）的所有必要步骤。无需任何外部工具——仅需 Aspose.Cells 库和 .NET 开发环境。

## 您将实现的目标

* **复制数据透视表**：将源工作表中的数据透视表复制到目标工作表，同时保持所有数据连接完整。  
* **导出 Excel 为 PPTX**：生成的幻灯片可在 PowerPoint 中编辑。  
* **生成可编辑的 PPTX**：图表、表格和形状不会被平铺为图片。  
* **使用相同的 Aspose.Cells API 调用将工作簿保存为 PPTX**。  

### 前置条件

* .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.6+）。  
* Aspose.Cells for .NET（NuGet 包 `Aspose.Cells`）。  
* 对 C# 控制台应用有基本了解。  

> **专业提示：** 通过 CLI 安装 NuGet 包以确保使用最新版本：  
> ```bash
> dotnet add package Aspose.Cells
> ```

## 如何在工作表之间复制数据透视表

首要操作是移动数据透视表并保留其定义。Aspose.Cells 提供了带有 `CopyOptions` 对象的 `CopyRange` 方法，其中包含 `CopyPivotTable` 标志。

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Load the workbook that contains the source and destination worksheets.
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Identify the worksheets by name.
Worksheet sourceSheet = workbook.Worksheets["Source"];
Worksheet destinationSheet = workbook.Worksheets["Destination"];

// Define the range that encloses the pivot table on the source sheet.
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

// Copy the range to the destination sheet, preserving the pivot table.
destinationSheet.Cells.CopyRange(
    sourceRange,
    0,                     // destination row index
    0,                     // destination column index
    new CopyOptions { CopyPivotTable = true });
```

**工作原理：**  
`CopyRange` 会复制单元格数据、格式，并在 `CopyPivotTable` 为 true 时复制数据透视表的缓存和元数据。目标范围从单元格 `A1`（第 0 行，第 0 列）开始，您可以更改偏移量以将数据透视表放置在其他位置。

**常见边缘情况：** 如果目标工作表已经包含同名的数据透视表，Aspose.Cells 会自动重命名新导入的表，以避免名称冲突。

## 导出 Excel 为 PPTX 并生成可编辑的 PPTX

数据透视表就位后，您可以将整个工作簿导出为 PPTX 文件。`ImageOrPrintOptions` 类允许您指定 `ExportImageFormat = ImageFormat.Pptx`，这会让 Aspose.Cells 将输出视为 PowerPoint 演示文稿，而不是光栅图像。

```csharp
// Configure export options to produce an editable PPTX.
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ExportImageFormat = ImageFormat.Pptx
};

// Save the workbook as an editable PPTX file.
workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);
```

**工作原理：**  
当 `ExportImageFormat` 设置为 `Pptx` 时，Aspose.Cells 会将每个工作表转换为一张幻灯片。形状、图表和数据透视表会以原生 PowerPoint 对象的形式写入，因此您可以在 PowerPoint 中双击它们并编辑底层数据。

**大工作簿的技巧：** 如果只需要导出部分工作表，请在调用 `Save` 之前使用 `workbook.Worksheets.RemoveAt(index)` 删除不需要的工作表，从而减小 PPTX 文件体积。

## 完整可运行示例

下面是将前述步骤串联起来的完整程序。请将 `YOUR_DIRECTORY` 替换为您机器上的实际路径。

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Export;

class Example
{
    static void Main()
    {
        // 1. Load the workbook that contains the source and destination worksheets.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Identify the source and destination worksheets.
        Worksheet sourceSheet = workbook.Worksheets["Source"];
        Worksheet destinationSheet = workbook.Worksheets["Destination"];

        // 3. Define the range that holds the pivot table.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // 4. Copy the range, preserving the pivot table.
        destinationSheet.Cells.CopyRange(
            sourceRange,
            0,
            0,
            new CopyOptions { CopyPivotTable = true });

        // 5. Set up export options to generate an editable PPTX.
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
        {
            ExportImageFormat = ImageFormat.Pptx
        };

        // 6. Save the workbook as a PPTX document.
        workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);

        Console.WriteLine("Pivot table copied and workbook exported to PPTX successfully.");
    }
}
```

### 预期输出

运行程序后会打印：

```
Pivot table copied and workbook exported to PPTX successfully.
```

在 Microsoft PowerPoint 中打开 `output.pptx` 时，您会看到一张包含已复制数据透视表的可编辑图表的幻灯片。双击该图表即可打开 PowerPoint 图表编辑器，修改系列、坐标轴和数据标签，而无需返回 Excel。

## 处理常见陷阱

| 问题 | 原因 | 解决方案 |
|-------|-------|-----|
| 数据透视表显示为静态图片 | 未设置 `CopyPivotTable` 标志或 `ExportImageFormat` 为 `Png` | 确保 `CopyPivotTable = true` 且 `ExportImageFormat = ImageFormat.Pptx`。 |
| 目标工作表出现空白单元格 | 源范围未覆盖整个数据透视表区域 | 扩大范围（例如 `"A1:H30"`）以包含所有透视字段。 |
| 导出的 PPTX 文件体积过大 | 包含了不必要的工作表 | 在调用 `Save` 前删除不需要的工作表。 |
| PowerPoint 无法编辑图表 | 使用的 Aspose.Cells 版本过旧，不支持 PPTX | 升级到最新的 Aspose.Cells 版本（查看发行说明）。 |

## 后续步骤及相关主题

* **使用自定义幻灯片布局导出 Excel 工作表为 PPTX** – 探索 `WorksheetToPdfConverter` 以获得更细致的幻灯片外观控制。  
* **导出 Excel 为 PDF** – 将 `ImageFormat.Pptx` 替换为 `ImageFormat.Pdf` 即可生成 PDF。  
* **导出后对 PPTX 进行编程修改** – 使用 `Aspose.Slides` 库添加动画或演讲者备注。  

通过掌握 **复制数据透视表**、**导出 Excel 为 PPTX** 和 **生成可编辑 PPTX**，您可以构建端到端的报告流水线，实现从电子表格直接转入演示文稿且保持可编辑性。

---


## 接下来应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方案。每个资源都提供完整的可运行代码示例和逐步解释。

- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Create a Pivot Table in Excel Using Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}