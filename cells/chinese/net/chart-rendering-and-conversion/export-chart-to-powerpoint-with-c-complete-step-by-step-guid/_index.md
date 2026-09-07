---
category: general
date: 2026-02-26
description: 使用 C# 将 Excel 中的图表导出到 PowerPoint。了解如何将 Excel 转换为 PowerPoint，将 Excel 保存为
  PowerPoint，并保持形状可编辑。
draft: false
keywords:
- export chart to powerpoint
- convert excel to powerpoint
- save excel as powerpoint
- how to convert excel to ppt
- save workbook as pptx
language: zh
og_description: 使用 C# 将 Excel 中的图表导出到 PowerPoint。本指南展示了如何将 Excel 转换为 PowerPoint，将工作簿保存为
  PPTX，并保持形状可编辑。
og_title: 使用 C# 将图表导出到 PowerPoint – 完整编程教程
tags:
- Aspose.Cells
- C#
- Office Automation
title: 使用 C# 将图表导出到 PowerPoint – 完整的逐步指南
url: /zh/net/chart-rendering-and-conversion/export-chart-to-powerpoint-with-c-complete-step-by-step-guid/
---

Let's craft final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将图表导出到 PowerPoint – 完整编程教程

是否曾想过如何在不失去可编辑性的情况下 **export chart to PowerPoint**？在许多报告场景中，你需要在幻灯片中嵌入实时图表，但手动复制粘贴非常麻烦。好消息是，只需几行 C# 代码即可实现程序化导出。

在本指南中，我们将完整演示整个过程：从加载包含图表和文本框的 Excel 工作簿、配置导出以保持文本框和形状可编辑，最后将结果保存为 **PowerPoint** 文件。结束时，你还将了解如何 **convert Excel to PowerPoint**、**save Excel as PowerPoint**，以及针对特殊情况微调选项。

## 您需要的条件

- **Aspose.Cells for .NET**（23.10 版或更高）。这是让转换毫不费力的库。
- **.NET 6+** 运行时 – 任意近期的 SDK 都可使用。
- 一个简单的 Excel 文件（`ChartWithTextbox.xlsx`），其中至少包含一个图表和一个文本框。
- Visual Studio 或你喜欢的 IDE。

无需除 Aspose.Cells 之外的其他 NuGet 包，但掌握基本的 C# 语法肯定有帮助。

## 将图表导出到 PowerPoint – 步骤详解

下面我们将解决方案拆分为离散、易于跟随的步骤。每一步都包含所需的完整代码以及解释其背后原理的简短段落。

### 步骤 1：加载包含图表的 Excel 工作簿

首先需要将源文件加载到内存中。使用 Aspose.Cells 提供的 `Workbook` 可以读取整个电子表格，包括图表、图片和嵌入对象。

```csharp
using Aspose.Cells;

// Step 1: Load the Excel workbook that contains the chart with a textbox
Workbook workbook = new Workbook(@"C:\Samples\ChartWithTextbox.xlsx");

// Verify that the workbook actually contains a chart
if (workbook.Worksheets[0].Charts.Count == 0)
{
    throw new InvalidOperationException("No chart found in the first worksheet.");
}
```

*为什么重要：* 如果未正确指定路径打开工作簿，会抛出 `FileNotFoundException`。此快速检查可防止后续导出出空白幻灯片。

### 步骤 2：准备演示选项以保持形状可编辑

Aspose.Cells 允许你决定在导出后文本框、形状乃至图表本身是否保持 **editable**。将 `ExportTextBoxes` 和 `ExportShapes` 设置为 `true` 可将这些对象保留为原生 PowerPoint 元素，而不是扁平化为静态图像。

```csharp
using Aspose.Cells.Drawing;

// Step 2: Set up presentation options to keep textboxes and shapes editable in the output
PresentationOptions presentationOptions = new PresentationOptions
{
    ExportTextBoxes = true, // Preserve editable textboxes
    ExportShapes    = true  // Preserve shapes such as the chart itself
};
```

*为什么重要：* 若保持默认值（`false`），生成的幻灯片将只包含图表的位图，之后无法编辑系列或更改标题。启用这两个选项后，你将得到一个真正的 PowerPoint 图表，行为完全等同于手动绘制的图表。

### 步骤 3：将 Excel 转换为 PowerPoint 并保存文件

现在调用 `Save` 方法，传入 `SaveFormat.Pptx` 枚举以及刚才配置的选项。库会负责将 Excel 图表对象转换为 PowerPoint 图表形状。

```csharp
// Step 3: Save the workbook as a PowerPoint presentation using the configured options
workbook.Save(@"C:\Samples\Result.pptx", SaveFormat.Pptx, presentationOptions);
```

*为什么重要：* `Save` 调用完成所有繁重工作——将 Excel 系列映射到 PowerPoint 系列、保留坐标轴格式、复制任何关联的文本框。执行此行后，你将得到一个可在 Microsoft PowerPoint 中打开的完整可编辑 `.pptx` 文件。

### 验证结果

在 PowerPoint 中打开 `Result.pptx`。你应该看到一张幻灯片，包含：

- 原始图表，仍然链接到其数据（双击即可编辑系列）。
- Excel 工作表中的任何文本框，现在成为原生 PowerPoint 文本框。
- 幻灯片布局会自动选择（通常是空白幻灯片）。

如果发现缺失元素，请再次确认源工作簿确实包含可见对象，并且 `ExportTextBoxes` / `ExportShapes` 已设为 `true`。

### 将 Excel 转换为 PowerPoint：处理多个工作表

通常工作簿会包含多个工作表，每个工作表都有自己的图表。默认情况下，Aspose.Cells 会将 **所有** 工作表中的 **所有** 图表导出为单独的幻灯片。如果只需要其中的一部分，可以在保存前进行过滤：

```csharp
// Example: Export only charts from the first worksheet
Worksheet firstSheet = workbook.Worksheets[0];
foreach (Chart chart in firstSheet.Charts)
{
    chart.IsVisible = true; // Ensure visibility
}

// Hide charts from other sheets
for (int i = 1; i < workbook.Worksheets.Count; i++)
{
    foreach (Chart chart in workbook.Worksheets[i].Charts)
    {
        chart.IsVisible = false;
    }
}
```

*小技巧：* 将 `chart.IsVisible = false` 的成本低于完全删除图表，并且可以在不修改源文件的情况下切换是否包含该图表。

### 将 Excel 保存为 PowerPoint – 自定义幻灯片尺寸

PowerPoint 默认使用 10 英寸 × 5.63 英寸的幻灯片。如果图表显得拥挤，可以通过 `PresentationOptions` 对象修改幻灯片尺寸：

```csharp
presentationOptions.SlideSize = new SizeF(13.33f, 7.5f); // 16:9 widescreen
```

现在导出的图表将拥有更多呼吸空间，文本框也会保留原始布局。

### 如何将 Excel 转换为 PPT：处理隐藏对象

隐藏的行、列或形状有时会悄悄进入导出结果。为将其剔除，可在保存前执行一次快速清理：

```csharp
// Remove hidden rows/columns that might affect chart layout
foreach (Worksheet sheet in workbook.Worksheets)
{
    sheet.Cells.HideRows = false;
    sheet.Cells.HideColumns = false;
}
```

此步骤并非总是必需，但可防止最终幻灯片出现意外空白。

### 将工作簿保存为 PPTX – 完整示例

将上述所有内容整合在一起，下面是一个可直接运行的控制台程序，演示完整流程：

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing; // For SizeF

class ExportChartDemo
{
    static void Main()
    {
        // Load workbook (Step 1)
        string sourcePath = @"C:\Samples\ChartWithTextbox.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // Verify chart existence
        if (workbook.Worksheets[0].Charts.Count == 0)
        {
            Console.WriteLine("No chart found. Exiting.");
            return;
        }

        // Configure presentation options (Step 2)
        PresentationOptions options = new PresentationOptions
        {
            ExportTextBoxes = true,
            ExportShapes    = true,
            SlideSize       = new SizeF(13.33f, 7.5f) // optional widescreen
        };

        // Optional: export only first worksheet charts
        for (int i = 1; i < workbook.Worksheets.Count; i++)
        {
            foreach (Chart c in workbook.Worksheets[i].Charts)
                c.IsVisible = false;
        }

        // Save as PowerPoint (Step 3)
        string targetPath = @"C:\Samples\Result.pptx";
        workbook.Save(targetPath, SaveFormat.Pptx, options);

        Console.WriteLine($"Export complete! File saved to {targetPath}");
    }
}
```

运行此程序后，将生成 `Result.pptx`，其中包含可编辑的图表和文本框，正是手动 **save workbook as pptx** 时所期望的效果。

![导出图表到 PowerPoint 示例](/images/export-chart-to-powerpoint.png "导出图表到 PowerPoint – 可编辑幻灯片")

## 常见问题与边缘案例

**如果 Excel 文件中的图表使用了外部数据源链接怎么办？**  
Aspose.Cells 会将 *当前* 数据值复制到 PowerPoint 图表中。它 **不会** 保留外部链接，因为 PowerPoint 无法以相同方式引用 Excel 数据连接。若需要实时更新，可考虑将原始 Excel 文件作为 OLE 对象嵌入到 PPTX 中。

**能导出使用自定义主题的图表吗？**  
可以。库会尝试将 Excel 主题颜色映射到 PowerPoint 主题槽位。对于极度自定义的调色板，可能需要在导出后使用 PowerPoint 自身的 API（例如 Aspose.Slides）进行颜色微调。

**图表数量有限制吗？**  
实际上没有——Aspose.Cells 采用流式处理，即使工作簿中有数十个图表也能导出，只是生成的 PPTX 文件大小会线性增长。

**使用 Aspose.Cells 是否需要许可证？**  
免费评估版可以使用，但会在首张幻灯片添加水印。生产环境请获取正式许可证，以去除水印并解锁全部性能。

## 小结

我们已经介绍了如何使用 C# **export chart to PowerPoint**，演示了加载 Excel 工作簿、配置 `PresentationOptions` 以保持文本框和形状可编辑，以及最终保存为 `.pptx` 的完整代码。你还学会了 **convert Excel to PowerPoint**、**save Excel as PowerPoint**，并掌握了回答 “**how to convert Excel to ppt**” 的完整可运行示例。

## 接下来可以做什么？

- **将工作簿保存为 PPTX** 并生成多张幻灯片：遍历每个工作表，对每个工作表调用带 `PresentationOptions` 的 `Save`。
- 如需进一步编程修改生成的 PPTX（添加切换、演讲者备注等），可探索 **Aspose.Slides**。
- 尝试导出 **数据透视图表** 或 **3‑D 图表**——相同选项适用，只是导出后可能需要微调坐标轴格式。

如果遇到任何问题，欢迎在下方留言或查阅官方 Aspose.Cells 文档获取最新 API 变更。祝编码愉快，尽情用几行 C# 将 Excel 图表转化为精美的 PowerPoint 演示文稿吧！

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}