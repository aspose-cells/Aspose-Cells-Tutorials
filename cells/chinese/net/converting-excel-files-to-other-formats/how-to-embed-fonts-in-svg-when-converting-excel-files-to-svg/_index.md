---
category: general
date: 2026-09-15
description: 学习如何在 SVG 中嵌入字体并将 Excel 图表导出到 PowerPoint，涵盖将 XLSX 转换为 SVG 和将 XLSX 转换为
  PPTX 的完整代码示例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in SVG
- export excel chart to powerpoint
- convert xlsx to svg
- convert xlsx to pptx
- save workbook as svg
language: zh
lastmod: 2026-09-15
og_description: 在 SVG 中嵌入字体，并使用一步一步的 C# 代码将 Excel 图表导出到 PowerPoint。快速可靠地将 XLSX 转换为
  SVG 和将 XLSX 转换为 PPTX。
og_image_alt: Screenshot showing an Excel chart exported to PowerPoint with embedded
  fonts in the resulting SVG file
og_title: 在 SVG 中嵌入字体并将 Excel 图表导出到 PowerPoint – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  headline: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  type: TechArticle
- description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  name: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  steps:
  - name: Open `EditableChart.pptx` in PowerPoint.
    text: Open `EditableChart.pptx` in PowerPoint.
  - name: Locate the slide containing the chart.
    text: Locate the slide containing the chart.
  - name: Choose **Chart Tools → Design → Edit Data**.
    text: Choose **Chart Tools → Design → Edit Data**.
  - name: Confirm that the Excel‑style data grid appears and that you can change values.
    text: Confirm that the Excel‑style data grid appears and that you can change values.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: 在将 Excel 文件转换为 SVG 和 PowerPoint 时，如何在 SVG 中嵌入字体
url: /zh/net/converting-excel-files-to-other-formats/how-to-embed-fonts-in-svg-when-converting-excel-files-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在将 Excel 文件转换为 SVG 和 PowerPoint 时如何在 SVG 中嵌入字体  

如果您需要在转换 Excel 工作簿时 **在 SVG 中嵌入字体**，本指南将一步步教您如何操作。您还将学习如何 **将 Excel 图表导出到 PowerPoint**，以及如何 **将 XLSX 转换为 SVG** 和 **将 XLSX 转换为 PPTX**（图表可编辑）。  

以编程方式处理 Excel 数据通常意味着要在不同文件格式之间移动相同的可视内容。手动在 PowerPoint 中重新创建图表或重新应用 SVG 中的字体既容易出错又耗时。完成本教程后，您将拥有一个可复用的 C# 代码片段，它：

* 将工作簿保存为带有嵌入字体和字体变体选择器的 SVG 文件。  
* 将同一工作簿导出为 PPTX 文件，且图表保持可编辑。  

唯一的前置条件是拥有最近版本的 **Aspose.Cells for .NET**（2024‑x 或更高）以及 Visual Studio 2022 等 .NET 开发环境。

---

## 您需要准备的内容  

* .NET 6.0 或更高（代码同样适用于 .NET Framework 4.8）。  
* Aspose.Cells for .NET NuGet 包（`Install-Package Aspose.Cells`）。  
* 一个包含至少一个图表的 Excel 文件（`input.xlsx`）。  
* 对输出目录的写入权限。  

---

## 在将 XLSX 转换为 SVG 时嵌入字体  

嵌入字体可确保 SVG 在任何设备上均能正确渲染，即使目标系统缺少原始字体。`SvgSaveOptions` 类提供了两个标志来实现此功能：`EmbedFonts` 和 `FontVariationSelectors`。

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// OPTIONAL: Use WRAPCOLS to reshape data before export (demonstrates a formula)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)"; // 2 columns per wrap
sheet.Calculate(); // Force calculation so the formula result appears

// Configure SVG options to embed fonts
SvgSaveOptions svgOptions = new SvgSaveOptions
{
    EmbedFonts = true,                // embed fonts in the SVG
    FontVariationSelectors = true    // include variation selectors for better Unicode handling
};

// Save the workbook as an SVG file
string svgPath = @"YOUR_DIRECTORY\WithFonts.svg";
workbook.Save(svgPath, svgOptions);
```

**工作原理：**  
* `EmbedFonts = true` 将字体文件复制到 SVG 的 `<defs>` 部分，消除外部依赖。  
* `FontVariationSelectors = true` 为支持 OpenType 特性的字体添加必要的选择器，保留连字等字形变体。  

**预期结果：** 在任意现代浏览器中打开 `WithFonts.svg`；图表或单元格内的文字将使用 Excel 中的精确字体显示，即使机器上未安装该字体。

---

## 将 Excel 图表导出到 PowerPoint 并保持可编辑  

当您需要将图表嵌入 PowerPoint 幻灯片且仍希望接收者能够编辑图表数据时，Aspose.Cells 的 `PptxSaveOptions` 提供了 `ExportEditableChart` 标志。

```csharp
// Configure PPTX options to keep charts editable after export
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableChart = true   // allow chart editing in PowerPoint
};

// Save the same workbook as a PPTX file
string pptxPath = @"YOUR_DIRECTORY\EditableChart.pptx";
workbook.Save(pptxPath, pptxOptions);
```

**重要性说明：**  
将 `ExportEditableChart` 设置为 `true` 会将图表存储为 Office Open XML 图表对象，而不是静态图像。打开 `EditableChart.pptx` 后，右键单击图表 → **Edit Data**，即可像原生 PowerPoint 图表一样修改系列数据。

**验证步骤：**  

1. 在 PowerPoint 中打开 `EditableChart.pptx`。  
2. 定位包含图表的幻灯片。  
3. 选择 **Chart Tools → Design → Edit Data**。  
4. 确认出现 Excel 样式的数据网格，并且可以更改数值。

---

## 将 XLSX 转换为 SVG – 工作流回顾  

下面是一个精简版本，结合了加载、可选的数据处理以及保存为 SVG 的步骤。仅在需要 SVG 输出时使用此代码。

```csharp
public void ConvertXlsxToSvg(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Example: apply a formula to demonstrate cell calculations
    Worksheet ws = wb.Worksheets[0];
    ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
    ws.Calculate();

    SvgSaveOptions opts = new SvgSaveOptions
    {
        EmbedFonts = true,
        FontVariationSelectors = true
    };

    wb.Save(outputPath, opts);
}
```

按如下方式调用该方法：

```csharp
ConvertXlsxToSvg(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.svg");
```

**边缘情况提示：** 如果工作簿使用了服务器上未安装的自定义字体，请在调用 `Save` 之前手动嵌入它们。使用 `FontInfoCollection` 将字体文件通过 `CustomFonts` 属性添加到 `SvgSaveOptions`（此属性在较新版本的 Aspose.Cells 中可用）。

---

## 将 XLSX 转换为 PPTX – 保持图表可编辑  

下面的辅助方法演示了 **将 XLSX 转换为 PPTX** 的路径，并确保图表保持可编辑。

```csharp
public void ConvertXlsxToPptx(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Ensure any chart you want to keep editable is on the first worksheet
    // (Aspose.Cells exports only the first worksheet by default for PPTX)
    PptxSaveOptions opts = new PptxSaveOptions
    {
        ExportEditableChart = true
    };

    wb.Save(outputPath, opts);
}
```

使用方式：

```csharp
ConvertXlsxToPptx(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.pptx");
```

**常见问题：** *如果我的工作簿有多个工作表且每个工作表都有图表怎么办？*  
**回答：** Aspose.Cells 默认只导出第一个工作表。若需包含其他工作表，请遍历 `workbook.Worksheets`，将每个图表复制到新幻灯片，并使用 Aspose.Slides 的 `Presentation` 对象分别保存每张幻灯片。此高级场景超出“将工作簿保存为 SVG”以及“将 Excel 图表导出到 PowerPoint”的基本流程，但核心标志保持不变。

---

## 实用技巧与常见陷阱  

* **性能：** 嵌入字体会增大 SVG 文件体积。如果对大小敏感，可将 `EmbedFonts = false` 并使用网页安全字体。  
* **字体授权：** 确保您拥有嵌入所用字体的授权；某些商业字体限制嵌入。  
* **图表兼容性：** 可编辑图表以 `chart.xml` 部分存储在 PPTX 中。非常复杂的图表（如 3‑D 或组合图表）在 PowerPoint 中编辑时可能会丢失部分样式。请针对常用图表类型进行测试。  
* **版本不匹配：** `ExportEditableChart` 标志要求 Aspose.Cells 20.10 或更高。使用旧版本会默 silently 回退为光栅图像。  
* **线程安全：** Workbook 对象不是线程安全的。在 Web 服务等场景下，请为每个请求创建新的 `Workbook` 实例。  

---

## 完整端到端示例  

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class ExcelExportDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputFile = @"YOUR_DIRECTORY\input.xlsx";
        string svgFile   = @"YOUR_DIRECTORY\WithFonts.svg";
        string pptxFile  = @"YOUR_DIRECTORY\EditableChart.pptx";

        // 1. Load workbook
        Workbook workbook = new Workbook(inputFile);

        // 2. Optional: reshape data using WRAPCOLS
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
        sheet.Calculate();

        // 3. Save as SVG with embedded fonts
        SvgSaveOptions svgOpts = new SvgSaveOptions
        {
            EmbedFonts = true,
            FontVariationSelectors = true
        };
        workbook.Save(svgFile, svgOpts);
        Console.WriteLine($"SVG saved with embedded fonts to: {svgFile}");

        // 4. Save as PPTX with editable chart
        PptxSaveOptions pptxOpts = new PptxSaveOptions
        {
            ExportEditableChart = true
        };
        workbook.Save(pptxFile, pptxOpts);
        Console.WriteLine($"PPTX saved with editable chart to: {pptxFile}");
    }
}
```

运行该程序后会生成两个文件：

* **WithFonts.svg** – 一个渲染效果与 Excel 完全一致、已嵌入字体的 SVG。  
* **EditableChart.pptx** – 一个图表可直接编辑的 PowerPoint 演示文稿。

---

## 结论  

现在，您已经掌握了在 **将 XLSX 转换为 SVG** 时 **嵌入字体** 的方法，以及在 **将 Excel 图表导出到 PowerPoint** 时保持图表可编辑的技巧。同一段代码同样演示了如何简洁地 **将工作簿保存为 SVG** 和 **将 XLSX 转换为 PPTX**，几乎不需要额外工作。  

接下来，您可以进一步探索以下主题：

* 通过代码添加自定义字体（`svgOptions.CustomFonts`）。  
* 在后台服务中批量处理多个工作簿。  
* 使用 Aspose.Slides 创建包含多个 Excel 图表的多幻灯片 PPTX 文件。  

尝试各种选项，将代码片段适配到您的项目中，享受无需手动后处理的可靠 Excel‑to‑SVG/PPTX 转换吧。祝编码愉快！


## 接下来您应该学习什么？


以下教程涵盖了与本指南技术紧密相关的主题，每篇资源都提供了完整可运行的代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/german/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/french/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}