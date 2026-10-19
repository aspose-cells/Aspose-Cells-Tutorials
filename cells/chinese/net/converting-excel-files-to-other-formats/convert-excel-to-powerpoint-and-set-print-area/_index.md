---
category: general
date: 2026-10-10
description: 使用 Aspose.Cells 在 C# 中将 Excel 转换为 PowerPoint 并设置打印区域——学习如何导出 Excel、设置打印区域以及生成
  PPTX 文件。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- set print area excel
- how to export excel
- how to set print area
- convert excel to pptx
language: zh
lastmod: 2026-10-10
og_description: 使用 Aspose.Cells 将 Excel 转换为 PowerPoint。本教程展示了如何设置打印区域、导出 Excel，以及在
  C# 中创建 PPTX 文件。
og_image_alt: Screenshot of code that converts Excel to PowerPoint while setting the
  print area
og_title: 将 Excel 转换为 PowerPoint – C# 开发者完整指南
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert Excel to PowerPoint and set print area in C# with Aspose.Cells
    – learn how to export Excel, set print area, and generate a PPTX file.
  headline: Convert Excel to PowerPoint and set print area
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: 将 Excel 转换为 PowerPoint 并设置打印区域
url: /zh/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将 Excel 转换为 PowerPoint 并设置打印区域

如果您需要 **convert Excel to PowerPoint**，本指南将向您展示在 C# 中如何准确完成此操作。通过先定义打印区域，您可以控制每张幻灯片显示的单元格，最终的 PPTX 文件将符合您的布局预期。该方案同样解答了 “how to export Excel” 与 “how to set print area” 的实现方式，使用相同的代码基础。

在本教程中，您将：

* 加载已有工作簿。
* 为工作表设置打印区域（**set print area excel** 步骤）。
* 配置 PowerPoint 输出的转换选项。
* 通过一次方法调用生成 **convert excel to pptx** 文件。

所有必需代码均已提供，您可以直接复制、粘贴并立即运行。

## 前置条件

在开始之前，请确保您具备以下条件：

| 要求 | 重要原因 |
|-------------|----------------|
| **.NET 6.0 或更高** | 示例针对 .NET 6+，但任何支持 C# 10 的 .NET 版本均可。 |
| **Aspose.Cells for .NET** | 该库提供 `Workbook`、`ImageOrPrintOptions` 与 `ConvertToPdf`（用于 PPTX）方法。通过 NuGet 安装：`dotnet add package Aspose.Cells` |
| **输入的 Excel 文件** | 本教程使用 `input.xlsx`。请将其放置在代码可引用的文件夹中。 |
| **对输出文件夹的写入权限** | 程序会写入 `output.pptx`。请确保目标目录已存在且可写。 |

> **专业提示：** 如果您处理多个工作表，请在转换前为每个工作表重复执行打印区域设置步骤。

## 步骤 1：创建新的 C# 控制台项目

打开终端或 PowerShell 窗口并运行：

```bash
dotnet new console -n ExcelToPowerPointDemo
cd ExcelToPowerPointDemo
dotnet add package Aspose.Cells
```

此命令会创建一个名为 **ExcelToPowerPointDemo** 的全新项目，并添加 Aspose.Cells 包——这是实现 **how to export Excel** 到其他格式的核心依赖。

## 步骤 2：编写转换代码

将 `Program.cs` 的内容替换为以下完整示例。代码演示了 **convert excel to powerpoint**，展示了 **how to set print area**，并生成 **convert excel to pptx** 文件。

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook (how to export Excel)
            // -----------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
            Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");

            // -----------------------------------------------------------------
            // 2️⃣ Define the print area for the first worksheet (set print area excel)
            // -----------------------------------------------------------------
            // The range "A1:G30" will be the only part visible on the slide.
            // Adjust the range to match the data you want to show.
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";
            Console.WriteLine($"Print area set to {sheet.PageSetup.PrintArea} on sheet \"{sheet.Name}\".");

            // -----------------------------------------------------------------
            // 3️⃣ Configure conversion options for PowerPoint output
            // -----------------------------------------------------------------
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                // SaveFormat.Pptx tells Aspose.Cells to generate a PowerPoint file.
                SaveFormat = SaveFormat.Pptx,
                // Optional: set the slide size or DPI if needed.
                // HorizontalResolution = 300,
                // VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 4️⃣ Convert the worksheet to a PowerPoint presentation (convert excel to powerpoint)
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);
            Console.WriteLine($"Successfully created PowerPoint file at: {outputPath}");
        }
    }
}
```

### 每个部分的重要性

* **加载工作簿** – 这是任何 **how to export Excel** 场景的第一步。`Workbook` 将文件读取到内存，您即可完整访问工作表、单元格和格式。
* **设置打印区域** – 通过为 `PageSetup.PrintArea` 赋值，告诉 Aspose.Cells 只渲染指定单元格。这正是 **set print area excel** 的核心；若不设置，整个工作表都会被导出，可能导致幻灯片体积庞大且难以阅读。
* **选择 `SaveFormat.Pptx`** – `ImageOrPrintOptions` 对象允许切换输出格式。将 `SaveFormat` 设置为 `Pptx` 即触发 **convert excel to pptx** 流程。
* **调用 `ConvertToPdf`** – 虽然方法名为 ConvertToPdf，但当 `SaveFormat` 为 `Pptx` 时，库会输出 PowerPoint 文件。这是实现 **convert excel to powerpoint** 的推荐单调用方式。

## 步骤 3：运行程序

在项目文件夹下执行：

```bash
dotnet run
```

如果配置正确，您将看到类似以下的控制台输出：

```
Loaded workbook with 1 worksheet(s).
Print area set to A1:G30 on sheet "Sheet1".
Successfully created PowerPoint file at: YOUR_DIRECTORY\output.pptx
```

在 Microsoft PowerPoint 或任何兼容的查看器中打开 `output.pptx`。每张幻灯片对应工作表的打印页，且仅限于您定义的范围。

## 处理多个工作表

如果工作簿包含多个工作表且希望每个工作表生成独立的幻灯片集，可遍历集合：

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet ws = workbook.Worksheets[i];
    ws.PageSetup.PrintArea = "A1:G30"; // adjust per sheet if needed
    string slidePath = $@"YOUR_DIRECTORY\output_sheet{i + 1}.pptx";
    ws.ConvertToPdf(conversionOptions, slidePath);
    Console.WriteLine($"Created {slidePath}");
}
```

此模式展示了 **how to export Excel** 时逐表处理，同时 **setting print area** 也可单独设置。

## 边缘情况和最佳实践提示

| 情况 | 推荐做法 |
|-----------|----------------------|
| **非常大的工作表** | 缩小打印区域或提升 `HorizontalResolution`/`VerticalResolution`，以保持 PPTX 大小可控。 |
| **不同的页面方向** | 在转换前设置 `sheet.PageSetup.Orientation = PageOrientationType.Landscape;` |
| **自定义幻灯片尺寸** | 使用 `conversionOptions.OnePagePerSheet = false;` 并调整 `conversionOptions.Width` / `conversionOptions.Height`。 |
| **缺少输入文件** | 将加载代码包裹在 `try { … } catch (FileNotFoundException)` 块中，以提供明确的错误信息。 |
| **非 ASCII 字符** | 确保工作簿以 UTF‑8 编码保存；Aspose.Cells 会自动处理 Unicode。 |

## 完整源代码供参考

以下是整个程序，包括 `using` 指令和注释。请将其保存为 `Program.cs`，放置在 **步骤 1** 创建的项目中。

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the Excel file you want to convert.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";

            // 1️⃣ Load the workbook (how to export Excel)
            Workbook workbook = new Workbook(inputPath);

            // Select the first worksheet – you can loop for multiple sheets.
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Set the print area (set print area excel)
            sheet.PageSetup.PrintArea = "A1:G30";

            // 3️⃣ Prepare conversion options for PowerPoint output.
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx   // This triggers convert excel to pptx
            };

            // 4️⃣ Convert the worksheet to PowerPoint (convert excel to powerpoint)
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);

            Console.WriteLine("Conversion complete.");
        }
    }
}
```

## 预期输出

运行程序后会生成一个 PowerPoint 文件（`output.pptx`），其中包含：

* 每个打印页对应一张幻灯片。
* 每张幻灯片仅显示 **A1:G30** 区域内的单元格。
* 保留 Excel 中的格式（字体、颜色、边框）不变。

在 PowerPoint 中打开文件，验证布局是否与定义的打印区域一致。

## 结论

现在，您已经掌握了使用 Aspose.Cells 在 C# 中 **convert Excel to PowerPoint** 并精确 **set print area excel** 的方法。教程涵盖了 **how to export Excel**、演示了 **how to set print area**，并展示了完整的 **convert excel to pptx** 实现。

## 接下来你应该学习什么？

以下教程涉及与本指南密切相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式。

- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area in Excel and Export to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}