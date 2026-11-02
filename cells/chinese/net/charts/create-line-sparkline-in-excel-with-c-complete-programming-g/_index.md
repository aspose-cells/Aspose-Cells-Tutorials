---
category: general
date: 2026-06-30
description: 使用 C# 快速在 Excel 中创建折线微图。学习如何添加微图、使用 C# 创建 Excel 工作簿，并在几步内将微图添加到单元格中。
draft: false
keywords:
- create line sparkline
- how to add sparkline
- add line sparkline
- create excel workbook c#
- add sparkline to cell
language: zh
og_description: 使用 C# 在 Excel 中创建折线微图表。本教程展示如何添加微图表、使用 C# 创建 Excel 工作簿，并将微图表嵌入单元格。
og_title: 使用 C# 在 Excel 中创建折线微型图 – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create line sparkline in Excel with C# quickly. Learn how to add sparkline,
    create Excel workbook C#, and add sparkline to cell in a few steps.
  headline: Create line sparkline in Excel with C# – Complete Programming Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: 使用 C# 在 Excel 中创建折线迷你图 – 完整编程指南
url: /zh/net/charts/create-line-sparkline-in-excel-with-c-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中使用 C# 创建折线微型图 – 完整编程指南

是否曾想过如何在 Excel 文件中使用 C# **创建折线微型图**？你并不是唯一的——开发者经常问：“如何在不手动打开 Excel 的情况下向报告添加微型图？”好消息是，只需几行代码，就能在工作簿内部直接生成精美的折线微型图，无需 UI。

在本教程中，我们将逐步讲解你需要了解的全部内容：从 **create Excel workbook C#** 基础、填充数据，到 **add line sparkline** 和 **add sparkline to cell** 的具体步骤。完成后，你将拥有一个可直接使用的 *.xlsx* 文件，一眼即可展示月度销售趋势。内容简洁实用，代码可直接运行。

---

## 你将构建的内容

- 一个名为 *KPI_Sparklines.xlsx* 的全新 Excel 工作簿  
- 一个名为 **KPI** 的工作表，包含示例销售数据  
- 一个放置在单元格 **D2**、引用数据范围 **B2:B13** 的 **折线微型图**  
- 基本格式设置（颜色、线宽），让微型图更醒目  

先决条件？只需 .NET SDK（3.1+ 或 .NET 6）以及免费提供的 Aspose.Cells for .NET 库（可通过 NuGet 获取）。如果你从未使用过 Aspose.Cells，可以把它视为一个强大的 Excel 引擎，可直接在代码中调用——无需 COM 互操作，也不需要安装 Excel。

![使用 C# 在 Excel 中创建折线微型图的代码示例](https://example.com/images/create-line-sparkline.png "使用 C# 在 Excel 中创建折线微型图")

*Image alt text: 使用 C# 在 Excel 中创建折线微型图的代码示例*

---

## 步骤 1：**Create Excel workbook C#** – 设置文件和工作表

首先，我们需要一个工作簿对象和一个用于存放数据的工作表。这是任何 Excel 自动化的基础，无论后续是 **add line sparkline** 还是编写公式。

```csharp
using Aspose.Cells;
using System.Drawing;

// Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0) and give it a meaningful name
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Name = "KPI";   // “KPI” will hold our key performance indicators
```

> **为什么重要：** `Workbook` 类代表整个文件，而 `Worksheet` 是行、列以及最终的微型图的画布。提前命名工作表可以使文件保持整洁并自我说明。

---

## 步骤 2：填充数据 – 微型图的数据源范围

微型图需要数据来绘制。我们来模拟 12 个月的销售数字。你可以从数据库中获取这些数据，但为保持示例简洁，我们将即时生成它们。

```csharp
// Fill column B (index 1) with monthly sales numbers
for (int month = 0; month < 12; month++)
{
    // Example pattern: start at 5,000 and increase by 750 each month
    worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
}
```

> **提示：** `PutValue` 会自动检测数据类型，无需将其强制转换为 `double` 或 `int`。如果需要对单元格进行格式化（货币、千位分隔符），可以稍后应用 `Style` 对象。

---

## 步骤 3：**Create line sparkline** – 将微型图添加到指定单元格

现在登场的是主角：**折线微型图**。Aspose.Cells 将微型图分组，因此我们首先创建一个类型为 `Line` 的 `SparklineGroup`，然后指定其显示位置。

```csharp
// Add a new SparklineGroup of type Line
int groupIndex = worksheet.SparklineGroups.Add(SparklineType.Line);
SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIndex];

// Add a sparkline that lives in D2 (row 1, column 3) and reads data from B2:B13
// Parameters: firstRow, firstColumn, lastRow, lastColumn, firstDataRow, lastDataRow
sparklineGroup.Add(1, 3, 1, 3, 1, 12);   // D2 ↔ B2:B13
```

> **工作原理：**  
> - `firstRow/firstColumn` 和 `lastRow/lastColumn` 定义 *目标单元格*（微型图显示的位置）。  
> - `firstDataRow/lastDataRow` 指向数据源范围。  
> 由于我们使用的是 **line sparkline**，因此可视化将是一条简单的细线，反映数字的趋势。

### 可选：使用自定义样式的 **How to add sparkline**

如果希望微型图更突出，可以调整几个属性：

```csharp
sparklineGroup.LineWeight = 1.0;               // Thickness of the line
sparklineGroup.SeriesColor = Color.DarkBlue;  // Color of the sparkline line
sparklineGroup.ShowMarkers = true;             // Show data markers (optional)
sparklineGroup.MarkerColor = Color.OrangeRed;  // Marker color
```

> **为什么要设置样式？** 深蓝色线条配白色背景视觉舒适，标记点还能快速提示各个数据点——在演示时非常实用。

---

## 步骤 4：保存工作簿 – 验证结果

微型图已就位后，只需将文件写入磁盘。请选择一个有写入权限的文件夹；示例中使用了占位路径，需要自行替换。

```csharp
// Save the workbook as an .xlsx file
string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
workbook.Save(outputPath);
```

> **验证方法：** 在 Excel（或任何支持 .xlsx 的查看器）中打开生成的文件。你应该会在单元格 **D2** 看到一条 **line sparkline**，它反映了列 **B** 中递增的销售数字。将鼠标悬停在微型图上会显示包含底层数值的工具提示。

---

## 步骤 5：在 **add sparkline to cell** 时的常见陷阱

即使是一个简单的示例，也可能让新手踩坑。以下是需要注意的几点：

| 问题 | 产生原因 | 解决方案 |
|-------|----------------|-----|
| 错误的单元格坐标 | 微型图目标使用零基列索引但行索引为一基 | 记住 `Cells[row, column]` 中 `row` 为零基，`column` 也为零基。在 `SparklineGroup.Add` 中，行列是 **1‑基** 的。 |
| 未显示数据 | 源范围为空或包含非数值。 | 确保范围（例如 `B2:B13`）中有数字。使用数值类型的 `PutValue`。 |
| 保存后微型图消失 | 库版本不匹配或缺少许可证。 | 使用最新的 Aspose.Cells 包，并在评估限制之外提供有效许可证。 |
| 未应用格式 | 在添加微型图之前更改了样式。 | 如上所示，在创建组之后 **再** 设置样式。 |

---

## 完整源代码 – 一键复制粘贴

下面是完整的可直接运行的程序。将其粘贴到新的控制台项目中，添加 Aspose.Cells NuGet 包，然后按 **F5** 运行。

```csharp
using Aspose.Cells;
using System.Drawing;

namespace SparklineDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create Excel workbook C#
            // -------------------------------------------------
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "KPI";

            // -------------------------------------------------
            // Step 2: Populate monthly sales data (B2:B13)
            // -------------------------------------------------
            for (int month = 0; month < 12; month++)
            {
                worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
            }

            // -------------------------------------------------
            // Step 3: Create line sparkline and add it to D2
            // -------------------------------------------------
            int groupIdx = worksheet.SparklineGroups.Add(SparklineType.Line);
            SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIdx];
            sparklineGroup.Add(1, 3, 1, 3, 1, 12); // D2 ↔ B2:B13

            // -------------------------------------------------
            // Step 4: Optional formatting (how to add sparkline with style)
            // -------------------------------------------------
            sparklineGroup.LineWeight = 1.0;
            sparklineGroup.SeriesColor = Color.DarkBlue;
            sparklineGroup.ShowMarkers = true;
            sparklineGroup.MarkerColor = Color.OrangeRed;

            // -------------------------------------------------
            // Step 5: Save the workbook
            // -------------------------------------------------
            string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
            workbook.Save(outputPath);

            System.Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**预期输出：** 打开 *KPI_Sparklines.xlsx* 时，列 **B** 列出十二个数字（5,000 → 13,250），单元格 **D2** 包含一条平滑的深蓝色折线微型图，呈稳步上升。如果启用了 `ShowMarkers`，标记会显示为微小的橙红色点。

---

## 接下来？扩展你的微型图技能

现在你已经掌握了使用 Aspose.Cells **create line sparkline**，可以进一步探索以下相关主题：

- **Add column sparkline** – 非常适合展示堆叠数据。  
- **Create multi‑sparkline groups** on the same sheet for side‑by‑side comparison. – 在同一工作表上创建多组微型图，以实现并排比较。  
- **Export to PDF** while preserving sparklines (Aspose.Cells supports PDF conversion). – 导出为 PDF 并保留微型图（Aspose.Cells 支持 PDF 转换）。  
- **Dynamic data sources** – 从 SQL 数据库获取真实销售数据，而非硬编码值。  

这些都基于相同的核心概念：**create Excel workbook C#**、填充数据，以及以所需样式 **add sparkline to cell**。

### TL;DR

我们演示了如何使用 C# 在 Excel 工作簿中 **create line sparkline**。步骤——*创建工作簿、填充数据、添加微型图、设置样式并保存*——全部封装在一个独立的程序中。欢迎根据你的报告需求调整颜色、线宽或数据源范围。

有想法想分享吗？在下方留言吧，祝编码愉快！

## 接下来该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于所示技术进行扩展。每个资源都包含完整的可运行代码示例和逐步说明，帮助你掌握更多 API 功能并在项目中探索替代实现方式。

- [Excel 自动化：使用 Aspose.Cells for .NET 创建工作簿并添加 ListBox](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Excel 自动化：创建工作簿并添加 ListBox（Aspose Cells）](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Excel 自动化：创建工作簿并添加 ListBox（Aspose Cells）](/cells/french/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}