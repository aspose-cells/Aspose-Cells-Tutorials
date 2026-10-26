---
category: general
date: 2026-10-26
description: 在 C# 中设置打印区域并将 Excel 工作表导出为 PNG。了解图像导出选项、如何导出 PNG，以及如何从工作簿获取可打印的图像。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area
- excel sheet to png
- how to export png
- export excel image
- image export options
language: zh
lastmod: 2026-10-26
og_description: 在 C# 中设置打印区域并将 Excel 工作表导出为 PNG。本分步教程涵盖图像导出选项以及如何从工作簿导出 PNG。
og_image_alt: Screenshot showing an Excel worksheet with the print area set and exported
  as a PNG image
og_title: 设置打印区域并将 Excel 工作表导出为 PNG – C# 指南
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Set print area and export an Excel sheet to PNG in C#. Learn image
    export options, how to export PNG, and get a printable image from a workbook.
  headline: Set print area and export Excel sheet to PNG in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: 在 C# 中设置打印区域并将 Excel 工作表导出为 PNG
url: /zh/net/rendering-and-export/set-print-area-and-export-excel-sheet-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中设置打印区域并将 Excel 工作表导出为 PNG

如果您需要在将 Excel 工作表导出为 PNG 之前**设置打印区域**，本指南将向您展示具体做法。您将看到一个完整的 C# 示例，演示如何配置图像导出选项、调整工作表的打印区域，并将结果保存为图像。

将 Excel 工作表导出为 PNG 是在报告、电子邮件或网页中嵌入工作表快照的常见需求。下面的代码可用于包含数据透视表的任意工作簿，同样适用于普通数据范围。无需外部工具——只需 Aspose.Cells for .NET 库。

## 前置条件

- .NET 6.0 或更高版本（示例针对 .NET 6，但任何近期的 .NET 版本均可）
- Aspose.Cells for .NET（通过 NuGet 安装：`Install-Package Aspose.Cells`）
- 对 C# 和 Excel 概念（如工作表和打印区域）有基本了解

## 第一步：配置图像导出选项

首先创建一个 `ImageOrPrintOptions` 实例。该对象告诉 Aspose.Cells 如何将工作表渲染为图像。

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

// Define image export options (PNG format)
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    // Export quality settings can be adjusted here
    ImageFormat = ImageFormat.Png,
    // Optional: set resolution (DPI) for higher‑quality PNGs
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**原因说明：** `ImageOrPrintOptions` 控制输出格式、分辨率以及其他渲染细节。使用 PNG 可确保无损质量，适合需要清晰文字和图形的报告。

## 第二步：加载工作簿并访问目标工作表

```csharp
// Load an existing workbook (replace with your file path)
Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

// Access the first worksheet in the workbook
Worksheet worksheet = wb.Worksheets[0];
```

**原因说明：** 必须使用特定的 `Worksheet` 对象，因为打印区域是工作表级别的设置。

## 第三步：确定要打印的范围

在许多场景中，您关心的数据位于数据透视表内部。下面的代码提取工作表上第一个数据透视表的数据范围。

```csharp
// Get the data range of the first pivot table on the worksheet
CellArea pivotDataRange = worksheet.PivotTables[0].PivotDataRange;
```

如果工作表不包含数据透视表，您可以将 `pivotDataRange` 替换为手动创建的任意 `CellArea`，例如：

```csharp
CellArea customRange = new CellArea(0, 0, 20, 10); // A1:K21
```

## 第四步：**设置打印区域**以匹配选定的范围

```csharp
// Set the worksheet's print area to match the pivot table's data range
worksheet.PageSetup.PrintArea = pivotDataRange.RefersTo;
```

**原因说明：** 打印区域告诉 Excel（以及 Aspose.Cells）在将工作表渲染为图像时应包含哪些单元格。将打印区域与数据透视表数据范围对齐，可避免空白边距，确保导出的 PNG 仅包含相关数据。

## 第五步：将工作表导出为 PNG 图像

```csharp
// Export the worksheet to an image using the defined options
// and assign the resulting image to the first picture shape on the sheet
worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);

// Optionally, save the image to a file for external use
worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);
```

**原因说明：** `worksheet.ToImage` 会遵循先前设置的打印区域，因此 PNG 文件恰好包含您定义的单元格。将图像分配给图片形状可在需要时将其嵌入回工作簿，同时保存到磁盘可得到独立文件。

## 完整工作示例

将所有步骤组合在一起即可得到一个可直接运行的自包含程序。

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

class ExportExcelToPng
{
    static void Main()
    {
        // 1️⃣ Configure image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 2️⃣ Load the workbook
        Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

        // 3️⃣ Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // 4️⃣ Get the data range of the first pivot table (or define your own)
        CellArea dataRange = worksheet.PivotTables[0].PivotDataRange;

        // 5️⃣ **Set print area** to the data range
        worksheet.PageSetup.PrintArea = dataRange.RefersTo;

        // 6️⃣ Export the worksheet as PNG
        worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);
        worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);

        Console.WriteLine("Export complete: WorksheetExport.png created.");
    }
}
```

### 预期输出

运行程序后会生成 `C:\Temp\WorksheetExport.png`。打开该文件可看到一张清晰的 PNG 图像，仅包含通过**设置打印区域**定义的单元格（本例中为数据透视表数据）。该图像可直接插入 Word 文档、PowerPoint 幻灯片或网页，无需额外转换步骤。

## 处理多个工作表或数据透视表

- **多个工作表：**遍历 `wb.Worksheets`，对每个需要导出的工作表重复步骤 3‑5。
- **多个数据透视表：**选择相应的 `PivotTables[index]`，或遍历 `worksheet.PivotTables`，分别导出每个表。
- **无数据透视表：**手动创建 `CellArea`（参见第 3 步的注释），并将其赋给 `PrintArea`。

## 实用技巧（E‑E‑A‑T）

- **专业技巧：**将 `HorizontalResolution` 和 `VerticalResolution` 设置为 300 DPI，以获得适合打印的 PNG；较低的数值可减小网页使用时的文件大小。
- **注意空图片形状：**如果工作表没有图片形状，请在分配图像之前先添加一个：

```csharp
if (worksheet.Pictures.Count == 0)
{
    worksheet.Pictures.Add(0, 0, 0, 0);
}
```

- **性能优化：**对多个工作表复用同一个 `ImageOrPrintOptions` 实例，可避免不必要的分配。
- **兼容性：**Aspose.Cells 23.9+ 完全支持 .NET 6 及更高版本；早期版本可能需要对 API 名称进行相应调整。

## 结论

现在您已经掌握了如何**设置打印区域**并将 Excel 工作表导出为 PNG。

## 接下来您应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式，每篇资源均提供完整的可运行代码示例和逐步说明。

- [如何导出 Excel 为 PNG – 完整分步指南](/cells/english/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/)
- [如何使用 C# 和 Aspose.Cells 将 Excel 区域导出为图像](/cells/english/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/)
- [excel sheet to png – 在 C# 中将数据透视表导出为 PNG](/cells/english/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}