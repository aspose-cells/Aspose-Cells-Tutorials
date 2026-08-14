---
category: general
date: 2026-08-14
description: 使用 Aspose.Cells 将 Excel 导出到 PowerPoint，并学习如何在代码中计算 Excel 公式。一步一步的 C#
  示例，附完整源码。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- calculate excel formulas in code
- Aspose.Cells copy pivot table
- export editable objects pptx
- dynamic array EXPAND function
- C# workbook automation
language: zh
lastmod: 2026-08-14
og_description: 使用 Aspose.Cells 将 Excel 导出为 PowerPoint，并在代码中计算 Excel 公式。请遵循本完整指南，从工作簿生成可编辑的
  PPTX 文件。
og_image_alt: Screenshot showing an Excel sheet being exported to a PowerPoint slide
  with editable textboxes
og_title: 使用 Aspose.Cells 将 Excel 导出到 PowerPoint – 完整 C# 教程
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  headline: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  type: TechArticle
- description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  name: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  steps:
  - name: Why this works
    text: '* **`Workbook`** loads the entire Excel file into memory, giving you full
      API access. * **`CopyRange`** with `CopyPivotTable = true` ensures the pivot
      table’s data source, cache, and layout are duplicated exactly—something older
      versions of Aspose.Cells could not do. * Adding a new worksheet (`Copy`'
  - name: Explanation
    text: '* **`WorkbookDesigner`** is a high‑level helper that prepares the workbook
      for export, handling Smart Markers, named ranges, and layout adjustments. *
      Setting `ExportEditableObjects = true` tells Aspose.Cells to translate Excel
      drawings into PowerPoint shapes rather than flattening them into images.'
  - name: Why you might use this
    text: '* **Uniform data type:** Exporting as strings avoids type‑mismatch errors
      when the consumer expects text. * **Custom formatting:** Replace `value.ToString()`
      with any custom formatter (e.g., `value.ToString("yyyy-MM-dd")` for dates).'
  - name: How the calculation engine works
    text: '* The `Formula` property stores the expression exactly as you would type
      it in Excel. * `CalculateFormula()` triggers a full workbook recalculation,
      respecting dependencies between cells. * The `EXPAND` function (available in
      Excel 365) returns a spill range based on the source cell (`B1`) and the s'
  - name: What to verify
    text: '* Open `result.xlsx` in Excel to confirm the pivot table copy, the `EXPAND`
      formula result, and any custom‑exported strings. * Open `output.pptx` in PowerPoint;
      you should see a slide that mirrors the Excel layout, and all charts/textboxes
      should be editable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
- Office 365 functions
title: 使用 Aspose.Cells 将 Excel 导出到 PowerPoint – 完整编程指南
url: /zh/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-aspose-cells-complete-progra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells 将 Excel 导出为 PowerPoint – 完整编程指南

如果您需要以编程方式 **export Excel to PowerPoint**，本指南将向您展示如何使用 Aspose.Cells for .NET 完成此操作。您还将学习如何 **calculate Excel formulas in code**、在不丢失定义的情况下复制数据透视表，以及使用新的 Office‑365 EXPAND 函数进行动态数组。

在接下来的章节中，我们将逐步演示一个真实的 C# 示例，解释每行代码的意义，并覆盖常见的陷阱，以便您能够将该解决方案应用到自己的项目中。

## 本教程涵盖内容

* 加载已有工作簿 (`input.xlsx`)  
* 复制包含数据透视表的范围，同时保留其定义  
* 将工作簿导出为 PowerPoint (`.pptx`) 文件，包含可编辑的文本框和形状  
* 使用自定义逻辑将单元格范围导出为字符串  
* 在代码中计算 Excel 公式，包括 Office‑365 EXPAND 函数  
* 保存已应用所有更改的最终工作簿  

**先决条件**  
* .NET 6.0 或更高（代码同样适用于 .NET Framework 4.7.2+）  
* Aspose.Cells for .NET v25.11 或更高（`CopyPivotTable` 选项在 v25.11 中引入）  
* 对 C# 以及 Excel 概念（如范围、数据透视表和公式）有基本了解  

> **专业提示：** 通过 NuGet 安装 Aspose.Cells (`Install-Package Aspose.Cells`)，以保持项目使用最新功能。

## 使用 Aspose.Cells 将 Excel 导出为 PowerPoint

首要任务是将工作簿转换为 PowerPoint 演示文稿，同时保持所有视觉元素可编辑。当您需要自动从财务报告或仪表板生成幻灯片时，这一点尤为重要。

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;      // ExportTableOptions, ExportOptions, etc.
using Aspose.Cells.Pivot;      // Pivot‑table APIs
using Aspose.Cells.Drawing;    // Shapes, textboxes, etc.

// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Step 2: Copy a range that contains a pivot table (preserves the definition)
Worksheet sourceSheet = workbook.Worksheets["Source"];
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");   // includes a pivot table
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
destinationSheet.Cells.CopyRange(sourceRange, destinationSheet.Cells, new CopyOptions
{
    CopyPivotTable = true   // new option in v25.11
});
```

### 为什么这样有效

* **`Workbook`** 将整个 Excel 文件加载到内存中，提供完整的 API 访问权限。  
* **`CopyRange`** 设置 `CopyPivotTable = true` 可确保数据透视表的数据源、缓存和布局完全复制——这是旧版本 Aspose.Cells 所不具备的功能。  
* 添加新工作表 (`Copy`) 可让原始工作表保持不变，这对审计追踪很有帮助。

## 将工作簿导出为带可编辑对象的 PowerPoint

现在我们将工作簿转换为 PowerPoint 文件。通过启用 `ExportEditableObjects`，每个图表、形状或文本框都会成为原生的 PowerPoint 对象，用户在导出后即可直接编辑。

```csharp
// Step 3: Export the workbook to PowerPoint with editable textboxes/shapes
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.Process();   // processes Smart Markers if present
designer.ExportToPptx("YOUR_DIRECTORY/output.pptx", new ExportOptions
{
    ExportEditableObjects = true   // makes objects editable in the PPTX
});
```

### 说明

* **`WorkbookDesigner`** 是一个高级助手，用于准备工作簿导出，处理 Smart Markers、命名范围和布局调整。  
* 将 `ExportEditableObjects = true` 设置为 true，指示 Aspose.Cells 将 Excel 绘图转换为 PowerPoint 形状，而不是将其展平为图像。这将产生一个 **完全可编辑** 的幻灯片文稿。

> **特殊情况：** 如果工作簿包含基于外部数据连接的复杂图表，请确保在调用 `ExportToPptx` 之前已解析这些连接，否则图表可能会显示为空白。

## 使用自定义逻辑将范围导出为字符串

有时您需要原始字符串值用于下游处理（例如，提供给 CSV 解析器）。`ExportTableOptions` 类允许您控制每个单元格的转换方式。

```csharp
// Step 4: Export a range as strings using custom logic
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true,
    CustomExport = (cell, value) => value.ToString()   // simple conversion for each cell
};
workbook.Worksheets[0].Cells.ExportTableAsString(tableOptions, "A1:D10");
```

### 为什么可能会使用此方法

* **统一的数据类型：** 将导出为字符串可避免在消费者期望文本时出现类型不匹配错误。  
* **自定义格式化：** 将 `value.ToString()` 替换为任意自定义格式化器（例如，日期使用 `value.ToString("yyyy-MM-dd")`）。

## 在代码中计算 Excel 公式

一个常见需求是 **calculate Excel formulas in code**，而无需打开 Excel。Aspose.Cells 提供了内置的计算引擎，可离线工作并支持最新的 Office‑365 函数，包括 `EXPAND`。

```csharp
// Step 5: Use the new Office‑365 EXPAND function to create a dynamic array
Worksheet firstSheet = workbook.Worksheets[0];
firstSheet.Cells["A1"].Formula = "EXPAND(B1,5,3)";   // expands array starting at B1
workbook.CalculateFormula();   // forces recalculation of the formula
```

### 计算引擎工作原理

* `Formula` 属性存储的表达式与在 Excel 中输入的完全相同。  
* `CalculateFormula()` 触发整个工作簿的重新计算，遵循单元格之间的依赖关系。  
* `EXPAND` 函数（在 Excel 365 中可用）根据源单元格 (`B1`) 以及指定的行数 (`5`) 和列数 (`3`) 返回一个溢出范围。  

> **提示：** 如果只需计算工作簿的某个子集，请使用 `Worksheet.CalculateFormula()` 限制范围并提升性能。

## 保存已应用所有更改的工作簿

最后，将修改后的工作簿写回磁盘。通过更改文件扩展名，您可以保存为任何受支持的格式（`.xlsx`、`.xls`、`.csv` 等）。

```csharp
// Step 6: Save the workbook with all changes applied
workbook.Save("YOUR_DIRECTORY/result.xlsx");
```

### 验证要点

* 在 Excel 中打开 `result.xlsx`，确认数据透视表已复制、`EXPAND` 公式结果以及任何自定义导出的字符串。  
* 在 PowerPoint 中打开 `output.pptx`；您应看到与 Excel 布局相同的幻灯片，且所有图表/文本框均可编辑。

## 常见问题与故障排除

| 问题 | 答案 |
|----------|--------|
| **我需要许可证才能使用 Aspose.Cells 吗？** | 是的。试用版可用于评估，但完整许可证会去除评估水印并解锁 `CopyPivotTable` 功能。 |
| **如果导出的 PPTX 显示空白形状怎么办？** | 确认工作簿的绘图对象未被隐藏（`Visible = true`），并在导出前将任何外部图像链接嵌入。 |
| **我可以将多个工作表导出为单独的 PPTX 幻灯片吗？** | 在循环中使用 `WorkbookDesigner.ExportToPptx`，为每个工作表指定不同的 `ExportOptions`，或通过 Aspose.Slides 手动添加幻灯片将它们合并为一个演示文稿。 |
| **`CalculateFormula` 是线程安全的吗？** | 不是。请在单线程上执行计算，或为每个线程克隆工作簿以避免竞争条件。 |

## 结论

现在，您已经拥有使用 Aspose.Cells 的 **完整、端到端的 Excel 导出为 PowerPoint 解决方案**，并且了解了如何 **calculate Excel formulas in code**——包括现代的 `EXPAND` 函数。本教程涵盖了加载工作簿、复制数据透视表、导出为可编辑的 PowerPoint、自定义字符串导出、公式计算以及最终保存。

从这里您可以：

* 将导出扩展为每个工作表包含多张幻灯片（次要关键字：*calculate Excel formulas in code* 可在生成图表数据时重复使用）。  
* 集成 Aspose.Slides 以添加动画或母版幻灯片布局。  
* 将简单的 `CustomExport` 委托替换为支持本地化的格式，以适用于国际化项目。  

欢迎尝试不同的范围，探索其他 Office‑365 函数（例如 `FILTER`、`SORT`），并将此工作流与自动化邮件发送相结合，实现全自动的报告流水线。

---


## 接下来应该学习什么？

以下教程涵盖与本指南演示的技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [使用 Aspose.Cells for .NET 自动化 Excel 数据导出：分步指南](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)
- [使用 Aspose.Cells for .NET 将 Excel 图表导出为 PDF：分步指南](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [使用 Aspose.Cells .NET 将 Excel 单元格导出为图像：分步指南](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}