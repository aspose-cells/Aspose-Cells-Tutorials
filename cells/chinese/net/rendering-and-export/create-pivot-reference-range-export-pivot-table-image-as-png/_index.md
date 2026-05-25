---
category: general
date: 2026-02-09
description: 在 C# 中创建数据透视表引用范围并导出数据透视表图像。学习如何使用 Aspose.Cells 将 Excel 区域保存为 PNG——快速、完整的指南。
draft: false
keywords:
- create pivot reference range
- export pivot table image
- save excel range as png
- Aspose.Cells C#
- Excel automation C#
language: zh
og_description: 在 C# 中创建数据透视表引用范围并将数据透视表图像导出为 PNG。完整的逐步指南，教您将 Excel 区域保存为 PNG。
og_title: 创建透视参考范围 – 将透视表图像导出为 PNG
tags:
- Aspose.Cells
- C#
- Excel
title: 创建数据透视表参考范围 – 导出数据透视表图像为 PNG
url: /zh/net/rendering-and-export/create-pivot-reference-range-export-pivot-table-image-as-png/
---

PNG"

But keep the header as #.

Proceed.

Paragraph: "Need to **create pivot reference range** in an Excel workbook using C#? You can also **export pivot table image** and **save Excel range as png** with just a few lines of code. In my experience, turning a live pivot into a static image is a handy way to embed analytics into reports, emails, or dashboards without pulling the whole workbook along."

Translate.

Continue.

We'll keep bold formatting.

Proceed through each section.

Make sure to keep code block placeholders unchanged.

Table: translate column headers and cells.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建透视参考范围 – 将透视表图像导出为 PNG

需要在 Excel 工作簿中使用 C# **创建透视参考范围** 吗？您还可以仅用几行代码 **导出透视表图像** 并 **将 Excel 区域保存为 png**。根据我的经验，将实时透视表转换为静态图像是将分析嵌入报告、电子邮件或仪表板的便捷方式，而无需携带整个工作簿。

在本教程中，我们将逐步讲解您需要了解的全部内容：所需的库、完整代码、每个调用的意义以及可能遇到的一些坑。完成后，您将能够自信地生成任意透视表的 PNG 文件，并了解如何将此模式扩展到多个工作表或自定义图像格式。

## 前置条件

在开始之前，请确保您已具备：

- **Aspose.Cells for .NET**（免费试用版足以进行测试）。  
- **.NET 6.0** 或更高版本 —— 我们使用的 API 完全兼容 .NET Standard 2.0+，因此旧版框架也能编译。  
- 一个基本的 C# 项目（控制台应用、WinForms 或 ASP.NET —— 任何能够引用 NuGet 包的项目）。  

如果尚未安装 Aspose.Cells，请运行：

```bash
dotnet add package Aspose.Cells
```

就这么简单 —— 无需 COM 互操作，也不需要在服务器上安装 Excel。

## 第一步：打开工作簿并访问第一个工作表

首先加载工作簿文件并获取包含透视表的工作表。我们特意选择 **第一个工作表** (`Worksheets[0]`)，因为大多数演示文件都会把透视表放在那里，当然您也可以根据需要使用名称来替代索引。

```csharp
using Aspose.Cells;
using System;

// Load an existing Excel file (replace with your own path)
Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Access the first worksheet – this is where our pivot lives
Worksheet worksheet = wb.Worksheets[0];
```

*为什么重要：* `Worksheet` 是所有基于范围操作的入口。如果指向了错误的工作表，随后对 `PivotTables[0]` 的调用将抛出 `IndexOutOfRangeException`。

## 第二步：创建透视参考范围

接下来让透视表本身返回一个 **参考范围**。该范围代表构成透视表的所有单元格——标题、数据行以及合计行。`CreateReferenceRange()` 方法在内部完成繁重的工作，自动处理合并单元格和隐藏行。

```csharp
// Grab the first pivot table on the worksheet
PivotTable pivot = worksheet.PivotTables[0];

// Build a reference range that covers the whole pivot
Range pivotReferenceRange = pivot.CreateReferenceRange();
```

> **小贴士：** 如果工作簿中包含多个透视表，遍历 `worksheet.PivotTables` 并通过其 `Name` 属性挑选所需的透视表。

## 第三步：将参考范围渲染为图像

Aspose.Cells 能将任意 `Range` 渲染为图像。返回的对象同时支持光栅（PNG、JPEG）和矢量（SVG）格式。这里我们请求默认的光栅图像，它是一个兼容 `System.Drawing.Image` 的对象。

```csharp
// Convert the pivot reference range into an image object
ImageOrVector pivotImage = pivotReferenceRange.ToImage();
```

*内部发生了什么？* API 会快照该范围的可视布局，保留单元格样式、字体以及条件格式。它本质上等同于截图，只是以编程方式、无需 UI 完成。

## 第四步：将生成的图像保存到文件

最后，将图像持久化。`Save` 方法在您提供 “.png” 扩展名时会自动选择 PNG 格式。如果需要 DPI 控制或其他格式，也可以传入 `SaveOptions` 对象。

```csharp
// Save the image as PNG – the extension drives the format
pivotImage.Save("YOUR_DIRECTORY/pivot.png");
```

执行完此行后，打开 `pivot.png`，您将看到透视表的像素级快照，可随意嵌入任何位置。

## 完整工作示例

将上述步骤整合在一起，下面是一个可直接复制粘贴运行的自包含控制台程序：

```csharp
using Aspose.Cells;
using System;

namespace PivotExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

            // 2️⃣ Access first worksheet
            Worksheet worksheet = wb.Worksheets[0];

            // 3️⃣ Get first pivot table
            if (worksheet.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found on the first sheet.");
                return;
            }
            PivotTable pivot = worksheet.PivotTables[0];

            // 4️⃣ Create a reference range that covers the whole pivot
            Range pivotReferenceRange = pivot.CreateReferenceRange();

            // 5️⃣ Render the range to an image
            ImageOrVector pivotImage = pivotReferenceRange.ToImage();

            // 6️⃣ Save as PNG
            string outputPath = "YOUR_DIRECTORY/pivot.png";
            pivotImage.Save(outputPath);

            Console.WriteLine($"Pivot table image saved to {outputPath}");
        }
    }
}
```

**预期输出：** 在 `YOUR_DIRECTORY` 下生成名为 `pivot.png` 的文件。使用任意图像查看器打开，它应当完整呈现原始透视表的布局，包括列标题、数据行和总计行。

## 导出透视表图像 – 自定义尺寸和 DPI

有时默认图像对演示幻灯片来说太小。您可以通过传入 `ImageOrVectorSaveOptions` 对象来控制分辨率：

```csharp
using Aspose.Cells.Drawing;

// Define PNG options – 300 DPI for high‑quality print
ImageOrVectorSaveOptions options = new ImageOrVectorSaveOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300 // DPI
};

pivotImage.Save("YOUR_DIRECTORY/pivot_highres.png", options);
```

*为什么要调整 DPI？* 更高的 DPI 在 PowerPoint 或 PDF 中放大 PNG 时能够提供更锐利的边缘。

## 将 Excel 区域保存为 PNG – 处理多个工作表

如果需要从多个工作表导出透视表，遍历 `Workbook.Worksheets` 并重复上述步骤。下面是一段简洁的代码片段：

```csharp
foreach (Worksheet ws in wb.Worksheets)
{
    foreach (PivotTable pt in ws.PivotTables)
    {
        Range refRange = pt.CreateReferenceRange();
        ImageOrVector img = refRange.ToImage();
        string fileName = $"pivot_{ws.Name}_{pt.Name}.png";
        img.Save($"YOUR_DIRECTORY/{fileName}");
        Console.WriteLine($"Saved {fileName}");
    }
}
```

该模式会为工作簿中的每个透视表 **导出透视表图像**，并以工作表名称和透视表名称命名文件 —— 十分适合批量处理。

## 常见陷阱及规避方法

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| `IndexOutOfRangeException` 在 `PivotTables[0]` 处 | 工作表没有透视表 | 在访问前检查 `worksheet.PivotTables.Count` |
| 输出的图像为空白 | 透视表已过滤至隐藏所有行 | 确保透视表有可见数据，或在创建范围前调用 `pivot.RefreshData();` |
| PNG 分辨率低 | 默认 DPI 为 96 | 如上所示使用 `ImageOrVectorSaveOptions.Resolution` |
| 文件路径错误 | `YOUR_DIRECTORY` 中包含非法字符 | 使用 `Path.Combine` 并通过 `Path.GetInvalidPathChars()` 进行清理 |

## 验证 – 快速测试

运行完整示例后：

1. 在 Windows Photo Viewer 中打开 `pivot.png`。  
2. 核对列标题、数据行和合计行是否与 Excel 中的视图一致。  
3. 若发现缺失行，请再次确认在调用 `CreateReferenceRange()` 前已执行透视表的 **RefreshData** 方法。

## 进阶：将 PNG 嵌入 Word 文档

因为图像已经是 PNG 格式，您可以直接将其传递给 Aspose.Words：

```csharp
using Aspose.Words;
Document doc = new Document();
DocumentBuilder builder = new DocumentBuilder(doc);
builder.InsertImage("YOUR_DIRECTORY/pivot.png");
doc.Save("YOUR_DIRECTORY/report.docx");
```

现在您拥有一个包含透视表快照的 Word 报告 —— 无需手动复制粘贴。

## 结论

您已经学会了如何使用 Aspose.Cells 在 C# 中 **创建透视参考范围**、**导出透视表图像** 并 **将 Excel 区域保存为 png**。关键要点如下：

- 使用 `PivotTable.CreateReferenceRange()` 将透视表的可视区域隔离。  
- 通过 `Range.ToImage()` 将该区域转换为图像。  
- 将图像保存为 PNG，并可根据需要调节 DPI 以满足打印质量。  

接下来，您可以探索批量导出、不同图像格式（SVG、JPEG）或将 PNG 嵌入 PDF、Word 等文档的更多可能性。一旦将透视表捕获为静态图形，创意的空间几乎无限。

有任何问题或特殊场景需要讨论？欢迎在下方留言，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}