---
category: general
date: 2026-09-15
description: 在 C# 中创建 Excel 工作簿，并学习如何在使用 EXPAND 函数展开动态数组时将工作簿保存为 PDF。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save workbook as pdf
- spill dynamic array
- use expand function
- how to create dynamic array in excel
language: zh
lastmod: 2026-09-15
og_description: 在 C# 中创建 Excel 工作簿，并使用 EXPAND 函数展开动态数组，快速将工作簿保存为 PDF。
og_image_alt: Create Excel workbook screenshot showing dynamic array and PDF output
og_title: 创建 Excel 工作簿并使用动态数组保存为 PDF
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Create Excel workbook in C# and learn how to save workbook as PDF while
    spilling dynamic arrays using the EXPAND function.
  headline: Create Excel workbook and save as PDF with dynamic arrays
  type: TechArticle
tags:
- excel
- csharp
- aspose-cells
- pdf
- dynamic-array
title: 创建 Excel 工作簿并使用动态数组保存为 PDF
url: /zh/net/conversion-to-pdf/create-excel-workbook-and-save-as-pdf-with-dynamic-arrays/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建 Excel 工作簿并使用动态数组保存为 PDF

如果您需要以编程方式 **创建 Excel 工作簿**，随后 **将工作簿保存为 PDF**，本指南将在 C# 中为您展示完整的端到端解决方案。您还将看到如何通过 **EXPAND 函数** **溢出动态数组**，这是一种无需 VBA 即可生成数组的现代方式。

无论您是在构建报表服务、ERP 系统的导出功能，还是数据驱动的仪表盘，下面的步骤都可以帮助您生成工作簿、使用智能标记填充数据，并生成保留高级字体特性的 PDF。

## 前置条件

开始之前，请确保您具备：

* .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.8）
* 最近版本的 **Aspose.Cells for .NET**（v25.8 或更新）——提供 `Workbook`、`PdfSaveOptions` 和 `SmartMarkerProcessor`。
* 如 Visual Studio 2022 等 IDE（任何能够编译 C# 的编辑器均可）。

将 NuGet 包添加到项目中：

```bash
dotnet add package Aspose.Cells --version 25.8
```

## 步骤 1：创建 Excel 工作簿并设置第一个工作表

首要任务是 **创建 Excel 工作簿** 并获取默认工作表的引用。该工作表将承载动态数组和智能标记模板。

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook in memory
        Workbook wb = new Workbook();

        // Get the first (default) worksheet
        Worksheet ws = wb.Worksheets[0];
```

*为什么重要*：实例化 `Workbook` 会分配内部工作簿结构，而访问 `Worksheets[0]` 则直接得到一个可用的工作表，无需手动添加。

## 步骤 2：使用 EXPAND 函数溢出动态数组

Excel 的 **EXPAND 函数** 可以将静态数组文字转换为任意大小的溢出范围。这里我们让 Excel 将 `{1,2,3}` 扩展为从 `A1` 开始的 5 行 × 1 列范围。

```csharp
        // Write the EXPAND formula into A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // Force calculation so the spill occurs immediately
        ws.Calculate();
```

*为什么重要*：使用 `EXPAND` 可避免在 C# 中编写手动循环。引擎会计算溢出范围并直接将值写入工作表，随后这些值会出现在 PDF 中。

## 步骤 3：保存工作簿为 PDF 并保留字体变体选择器

当您需要 **将工作簿保存为 PDF** 时，还可以启用高级排版特性，例如字体变体选择器（自 Aspose.Cells v25.8 起可用）。这可确保 PDF 正确渲染复杂文字。

```csharp
        // Configure PDF options
        PdfSaveOptions pdfOpts = new PdfSaveOptions
        {
            FontVariationSelectors = true   // keeps variation selectors for OpenType fonts
        };

        // Save the current workbook (with the spilled array) as PDF
        wb.Save(@"YOUR_DIRECTORY\VarSelector.pdf", pdfOpts);
```

*为什么重要*：将 `FontVariationSelectors` 设置为 `true` 对依赖字形变体的语言（如中文、日文、表情符号）至关重要。生成的 PDF 与屏幕上的 Excel 视图保持一致。

## 步骤 4：插入引用嵌套数据源的智能标记模板

智能标记允许您直接在工作表中嵌入占位符。下面的模板将生成订单及其明细列表。

```csharp
        // Define a Smart Marker template in cell A1
        string template = "${Orders.OrderId}\n${Orders.Items:ItemName}\n";
        ws.Cells["A1"].PutValue(template);
```

*为什么重要*：将模板放在 `A1`，即告诉 Aspose.Cells 从该位置开始展开数据。`:` 语法（`Items:ItemName`）指示处理器遍历嵌套集合。

## 步骤 5：定义嵌套数据源（包含明细的订单）

我们创建一个匿名数组，每个订单都包含自己的明细集合。这对应典型的主从（master‑detail）场景。

```csharp
        // Sample nested data source
        var orders = new[]
        {
            new
            {
                OrderId = 1,
                Items = new[]
                {
                    new { ItemName = "Apple" },
                    new { ItemName = "Banana" }
                }
            },
            new
            {
                OrderId = 2,
                Items = new[]
                {
                    new { ItemName = "Carrot" }
                }
            }
        };
```

*为什么重要*：该嵌套结构演示了 **如何通过智能标记在 Excel 中创建动态数组**，无需编写任何 VBA 或手动单元格循环。

## 步骤 6：处理智能标记并保存最终的 Excel 文件

现在将工作簿和数据源交给 `SmartMarkerProcessor`。处理完成后，占位符会被实际行替换，我们将结果保存为普通的 `.xlsx` 文件。

```csharp
        // Process the Smart Markers
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Process(wb, orders);

        // Save the populated workbook
        wb.Save(@"YOUR_DIRECTORY\NestedSmartMarker.xlsx");
    }
}
```

*为什么重要*：`SmartMarkerProcessor` 会自动展开模板、创建所需行并填充数据。最终的工作簿可在 Excel 中打开，以验证每个订单及其明细是否正确显示。

## 预期输出

* **VarSelector.pdf** – 一个 PDF 文件，展示数字 1‑3 向下溢出五行，并使用您启用的任何 OpenType 字体变体进行渲染。
* **NestedSmartMarker.xlsx** – 一个 Excel 文件，包含以下行（从 `A1` 开始）：

| OrderId | ItemName |
|---------|----------|
| 1       | 苹果      |
| 1       | 香蕉      |
| 2       | 胡萝卜    |

PDF 版本保留相同的数字溢出，因为工作表状态在智能标记处理之前已保存；如果需要最终数据的 PDF，也可以在处理后再次保存。

## 专业技巧与常见陷阱

| 提示 | 说明 |
|-----|------|
| **复用同一个 `PdfSaveOptions`** | 只创建一次选项对象并重复使用，可避免渲染细微差异（例如缺失变体选择器）。 |
| **在设置公式后调用 `ws.Calculate()`** | 若未显式计算，溢出范围在程序化检查工作簿时可能保持为空。 |
| **将智能标记模板放在干净的工作表上** | 与已有数据混合可能导致意外的行插入。尽量使用专用工作表。 |
| **注意文件路径** | 使用 `Path.Combine(Environment.CurrentDirectory, "output.pdf")` 可避免在不同机器上出现硬编码目录。 |
| **版本检查** | `FontVariationSelectors` 仅在 25.8 及以上版本可用；旧版本会忽略该属性且不抛异常。 |

## 后续步骤

了解了如何 **创建 Excel 工作簿**、**溢出动态数组** 并 **将工作簿保存为 PDF** 后，您可以进一步探索：

* 在 PDF 转换前添加图表或图片。
* 使用 `Save` 重载将同一工作簿导出为其他格式（如 HTML、CSV）。
* 使用 **智能标记表达式**（`${Orders.Total:SUM(Items.Price)}`）实时计算聚合。
* 将此代码集成到 ASP.NET Core API 中，让用户直接从 Web 端点下载生成的 PDF。

---

**摘要** – 本教程展示了如何 **创建 Excel 工作簿**，使用 **EXPAND 函数** **溢出动态数组**，嵌入能够处理嵌套数据源的 **智能标记**，并在 **保存为 PDF** 时保留高级字体特性。完整、可运行的示例可复制到任意 C# 项目并根据自己的数据结构进行适配。祝编码愉快！


## 接下来您应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式，每篇资源均提供完整可运行的代码示例和逐步解释。

- [使用 Aspose.Cells 在 ASP.NET 中创建并保存 Excel 工作簿为 PDF](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [使用 Aspose.Cells for .NET 将 Excel 工作簿创建并保存为 ODS](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [使用 Aspose.Cells for Java 将 Excel 工作簿创建并保存为 SVG](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}