---
category: general
date: 2026-02-21
description: 学习如何将 Excel 导出到 PowerPoint 并保留可编辑的图表。只需几行 C# 代码即可将 Excel 转换为 PowerPoint，或从
  Excel 创建 PowerPoint。
draft: false
keywords:
- how to export excel
- convert excel to powerpoint
- create powerpoint from excel
- save excel as powerpoint
- how to export charts
language: zh
og_description: 如何将 Excel 导出为带可编辑图表的 PowerPoint。按照本指南将 Excel 转换为 PowerPoint，从 Excel
  创建 PowerPoint，轻松将 Excel 保存为 PowerPoint。
og_title: 如何将 Excel 导出到 PowerPoint – 完整教程
tags:
- C#
- Aspose.Cells
- PowerPoint
title: 如何将 Excel 导出到 PowerPoint – 步骤指南
url: /zh/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何将 Excel 导出到 PowerPoint – 完整教程

是否曾想过 **如何将 Excel 导出** 到 PowerPoint，而不把您精美的图表转换为静态图像？您并非唯一有此困惑的人。在许多报告流程中，**将 Excel 转换为 PowerPoint** 的需求每天都会出现，而常用的复制‑粘贴技巧要么破坏布局，要么锁定图表数据。  

在本指南中，我们将演示一种简洁的编程解决方案，**从 Excel 创建 PowerPoint**，并保持图表可完全编辑。完成后，您只需一次方法调用即可 **将 Excel 保存为 PowerPoint**，并清楚每行代码的作用。

## 您将学习的内容

- 完整的 C# 代码，用于 **将 Excel 导出** 为 PPTX 文件。  
- 如何通过 `PresentationExportOptions` 保持图表可编辑。  
- 在何种情况下应优先使用此方法，而非手动导出或第三方转换器。  
- 前置条件、常见陷阱以及一些让过程万无一失的专业技巧。

> **专业提示：** 如果您在项目中已经使用 Aspose.Cells，则此方法几乎不增加额外开销。

### 前置条件

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 或更高版本 | 现代运行时，性能更佳，并完整支持 Aspose.Cells。 |
| Aspose.Cells for .NET（NuGet 包） | 提供我们依赖的 `Workbook`、`PresentationExportOptions` 和 `SaveToPptx` API。 |
| 至少包含一个图表的基础 Excel 文件 | 只有存在图表对象时导出才有效，否则 PPTX 将为空白。 |
| Visual Studio 2022（或您喜欢的任何 IDE） | 便于调试和包管理。 |

如果您已经准备好上述内容，让我们开始吧。

## 如何使用可编辑图表将 Excel 导出到 PowerPoint

下面是 **完整、可运行** 的示例，演示整个流程。每段代码块后都有解释，您可以直接复制粘贴并根据需要进行调整，而无需在文档中四处查找。

### 步骤 1：安装 Aspose.Cells

在项目文件夹的终端中运行：

```bash
dotnet add package Aspose.Cells
```

这将拉取最新的稳定版本（当前为 24.9），并将必要的引用添加到您的 `.csproj` 中。

### 步骤 2：加载 Excel 工作簿

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Step 2: Load the Excel workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

> **为什么重要：** `Workbook` 是所有 Excel 操作的入口。先加载文件可确保后续导出基于您在 Excel 中看到的确切数据和格式。

### 步骤 3：配置 PPTX 导出选项以保持图表可编辑

```csharp
// Step 3: Configure PPTX export options to keep charts editable
PresentationExportOptions exportOptions = new PresentationExportOptions
{
    ExportEditableCharts = true   // This flag ensures charts stay editable in PowerPoint
};
```

如果省略 `ExportEditableCharts`，Aspose 会将图表光栅化，变成平面图像。这将违背 **如何导出图表** 为可编辑形式的初衷。

### 步骤 4：将第一个工作表保存为 PPTX 文件

```csharp
// Step 4: Export the first worksheet as a PPTX file using the options
workbook.Worksheets[0].PageSetup.SaveToPptx(@"YOUR_DIRECTORY\Editable.pptx", exportOptions);
```

`SaveToPptx` 方法会生成一个 PowerPoint 文件，其中每个 Excel 单元格变为文本框，每个图表则成为原生 PowerPoint 图表对象。现在您可以在 PowerPoint 中打开 `Editable.pptx`，双击任意图表即可编辑其系列、坐标轴或样式。

### 步骤 5：验证结果

1. 在 Microsoft PowerPoint 中打开 `Editable.pptx`。  
2. 找到对应导出工作表的幻灯片。  
3. 点击图表 → 选择 **Edit Data** → 您应看到 Excel 样式的数据网格。

如果图表仍然是图像，请再次确认 `ExportEditableCharts` 已设置为 `true`，并且源工作表确实包含图表对象。

![展示从 Excel 到 PowerPoint 流程的图示 – 如何导出 Excel](/images/excel-to-pptx-flow.png "如何导出 Excel 示例")

## 将 Excel 转换为 PowerPoint – 常见陷阱与技巧

即使代码正确，开发者有时仍会遇到问题。以下是最常见的几类问题及其解决办法。

| Issue | Explanation | Fix |
|-------|-------------|-----|
| **未出现图表** | 工作簿可能没有任何图表对象，或图表被隐藏。 | 确保图表可见且不在隐藏的工作表上。 |
| **图表变成图像** | `ExportEditableCharts` 保持默认 `false`。 | 如步骤 3 所示，显式设置 `ExportEditableCharts = true`。 |
| **文件路径错误** | 使用相对路径但未正确 `Path.Combine`。 | 建议使用 `Path.Combine(Environment.CurrentDirectory, "input.xlsx")`。 |
| **大文件导致 OutOfMemory** | 导出包含数千行和大量图表的工作簿会占用大量内存。 | 在加载前使用 `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;`。 |
| **版本不匹配** | 使用的 Aspose.Cells 版本过旧，缺少 `PresentationExportOptions`。 | 升级到最新的 NuGet 包。 |

### 额外技巧：导出多个工作表

如果需要为多个工作表 **从 Excel 创建 PowerPoint**，可以遍历集合：

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string pptxPath = $@"YOUR_DIRECTORY\Sheet{i + 1}.pptx";
    workbook.Worksheets[i].PageSetup.SaveToPptx(pptxPath, exportOptions);
}
```

每个工作表都会生成各自的 PPTX 文件，保持图表的可编辑性。

## 将 Excel 保存为 PowerPoint – 高级场景

### 在图表旁嵌入图片

有时报告会混合图表和公司徽标。Aspose 将图片视为普通形状，导出时会自动出现在 PPTX 中。如需控制顺序，可在导出前通过 `Shape` 属性调整 Z‑index。

### 自定义幻灯片布局

PowerPoint 支持母版幻灯片。虽然 `SaveToPptx` 会创建默认布局，但您随后可以应用母版模板：

```csharp
using Aspose.Slides;

// Load the generated PPTX
Presentation pres = new Presentation(@"YOUR_DIRECTORY\Editable.pptx");

// Apply a master template (must be a .pptx file)
pres.Masters.AddFromFile(@"TEMPLATES\CorporateTemplate.pptx");

// Save the final version
pres.Save(@"YOUR_DIRECTORY\FinalPresentation.pptx", SaveFormat.Pptx);
```

此步骤可让您 **将 Excel 转换为 PowerPoint** 时保持企业品牌一致。

### 处理不同的图表类型

大多数常见图表类型（柱形、条形、折线、饼图）均能完美导出。但 **如何导出图表** 如雷达图或股票图可能需要在导入后进行额外样式调整。此时可以：

1. 按上述方式导出。  
2. 使用 Aspose.Slides 以编程方式打开 PPTX。  
3. 调整图表属性（例如 `Chart.Type = ChartType.Radar`）。

## 回顾与后续步骤

我们已经完整讲解了 **如何将 Excel 导出** 为 PowerPoint 并保持图表可编辑的全部要点。核心步骤——安装 Aspose.Cells、加载工作簿、配置 `PresentationExportOptions`，以及调用 `SaveToPptx`——只需几行 C# 代码，却能取代整套手动流程。

### 接下来可以尝试的方向

- 使用循环示例 **将整个 Excel 转换为 PowerPoint**。  
- 试验 **从 Excel 创建 PowerPoint** 用于每晚自动更新的动态仪表盘。  
- 将此导出与 **Aspose.Slides** 结合，应用自定义母版并实现品牌自动化。  
- 若希望在单个 PPTX 中包含多个工作表，可探索 `ExportAllSheetsAsPptx` 方法。

随意调整路径、导出选项，或将逻辑嵌入更大的报告服务中。唯一的限制就是您对数据可视化的创意程度。

---

*祝编码愉快！如果在 **将 Excel 保存为 PowerPoint** 时遇到任何问题，欢迎在下方留言或查阅 Aspose.Cells 文档获取最新更新。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}