---
category: general
date: 2026-09-18
description: 学习如何在 Excel 中使用 EXPAND 函数展开数组、填充 Excel 模板，并使用 C# 创建动态范围的 Excel 工作表。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- populate excel template
- dynamic range excel
- use expand function
- expand array formula
language: zh
lastmod: 2026-09-18
og_description: 如何使用 EXPAND 函数在 Excel 中展开数组、填充 Excel 模板，并使用 C# 代码构建动态范围的 Excel 解决方案。
og_image_alt: Excel worksheet showing expanded 5x5 array and Smart Markers result
og_title: 如何在 Excel 中展开数组并填充模板
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to expand array in Excel using the EXPAND function, populate
    an Excel template, and create a dynamic range Excel worksheet with C#.
  headline: How to expand array in Excel and populate a template
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: 如何在 Excel 中展开数组并填充模板
url: /zh/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Excel 中展开数组并填充模板

如果您需要在填充预先设计好的模板时 **how to expand array**，本指南将为您展示一个完整的端到端解决方案。通过将 `EXPAND` 函数与 Aspose.Cells 的 Smart Markers 结合使用，您可以将单个单元格引用转换为 5 × 5 的范围，并自动将 `{IsActive}` 等标记替换为实时数据。

您将看到如何 **populate excel template**、创建 **dynamic range excel**，以及在 C# 项目中正确 **use expand function**。教程结束时，您将拥有一个可运行的程序，它加载 `.xlsx` 文件，展开数组公式，应用 Smart Markers，并保存结果。

## 前置条件

* .NET 6.0 或更高版本（代码同样适用于 .NET Core 3.1+）
* Aspose.Cells for .NET（NuGet 包 `Aspose.Cells`）
* 包含占位公式单元格（例如 `B2`）和 Smart Marker 如 `{IsActive}` 的 Excel 工作簿
* 对 C# 和 Excel 公式有基本了解

> **专业提示：** `EXPAND` 函数仅在 Microsoft 365 版 Excel 和 Excel 2021+ 中可用。旧版本会返回 `#NAME?` 错误。

## 步骤 1：使用 EXPAND 函数展开数组

第一步是加载工作簿并编写一个 `EXPAND` 公式，将单个源单元格转换为更大的矩阵。  

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains the template layout
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Apply the EXPAND function to cell B2.
        // =EXPAND(A2,5,5) expands the array that starts at A2 into a 5‑row by 5‑column range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";
```

这样做的意义在于：`EXPAND` 消除了手动在行列之间复制公式的需求。当源单元格（`A2`）更改时，整个 5 × 5 区块会自动更新，为您提供一个 **dynamic range excel**，能够响应数据变化。

## 步骤 2：使用 Smart Markers 填充 Excel 模板

Smart Markers 允许您在模板中嵌入占位符，这些占位符会被来自 C# 对象的值替换。这是 **populate excel template** 的最便捷方式，无需编写逐单元格的代码。

```csharp
        // Prepare an anonymous object that matches the marker names in the template.
        var data = new { IsActive = true };

        // Apply Smart Markers. The marker {IsActive} inside a formula like
        // =IF({IsActive}, "Active", "Inactive") will be replaced with the value from the object.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);
```

`SmartMarkersProcessor().Apply` 调用会扫描整张工作表，找到 `{IsActive}` 并注入布尔值。随后公式会自动计算为 `"Active"` 或 `"Inactive"`。

## 步骤 3：验证展开的范围和填充结果

在同时应用 `EXPAND` 公式和 Smart Markers 后，您可以以编程方式读取几个单元格，以确保一切如预期工作。

```csharp
        // Optional: read a cell from the expanded block to confirm the value.
        var sampleValue = ws.Cells["B2"].Value; // top‑left cell of the expanded range
        Console.WriteLine($"Top‑left of expanded range: {sampleValue}");

        // Read the marker result cell (assume it is C2)
        var status = ws.Cells["C2"].StringValue;
        Console.WriteLine($"Status from Smart Marker: {status}");
```

运行程序后应打印出 `A2` 的原始值（或数组结果），以及根据 `IsActive` 标志显示的 **Active** 或 **Inactive**。

## 步骤 4：保存工作簿 – 最终输出

最后，将修改后的工作簿写入磁盘。此步骤展示了从加载、展开、填充到持久化文件的完整流程。

```csharp
        // Save the workbook with the expanded array and populated markers.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

保存后的 `output.xlsx` 现在包含由 `EXPAND` 公式生成的 5 × 5 矩阵，以及一个反映 `{IsActive}` 值的单元格。用 Excel 打开文件即可看到动态范围的实际效果。

## 边缘情况和最佳实践

| 情况                                      | 建议                                                                                 |
|-------------------------------------------|--------------------------------------------------------------------------------------|
| Excel 版本不支持 `EXPAND`                | 回退使用经典的 `=OFFSET` 或 `=INDEX` 公式，或升级到 Office 365。                     |
| 需要展开到可变大小                        | 在 `EXPAND` 中使用 `ROWS(source)` 和 `COLUMNS(source)` 实现真正的动态性。          |
| 同一工作表中有多个 Smart Markers          | 使用复合数据对象一次性调用 `SmartMarkersProcessor().Apply`。                        |
| 大型工作簿（> 10 000 行）                 | 写入公式时关闭计算 (`workbook.Settings.CheckFormula = false`)。                    |

## 完整工作示例

下面是完整的、可自行复制粘贴到新控制台项目中的程序代码。

```csharp
using System;
using Aspose.Cells;

class ExpandArrayDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook that serves as the template.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Write the EXPAND formula to create a 5x5 dynamic range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";

        // 3️⃣ Prepare data for Smart Markers.
        var data = new { IsActive = true };

        // 4️⃣ Apply Smart Markers – replaces {IsActive} in any formula or text.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);

        // 5️⃣ (Optional) Verify a couple of cells.
        Console.WriteLine($"Expanded top‑left: {ws.Cells["B2"].Value}");
        Console.WriteLine($"Marker result: {ws.Cells["C2"].StringValue}");

        // 6️⃣ Save the final workbook.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
        Console.WriteLine("Workbook saved successfully.");
    }
}
```

**运行程序时的预期输出**（假设 `A2` 包含数字 `42`）：

```
Expanded top‑left: 42
Marker result: Active
Workbook saved successfully.
```

打开 `output.xlsx` 可看到一个 5 × 5 区块，其值来源于 `A2`，以及一个显示 **Active** 的单元格。

## 结论

您现在已经掌握了在 Excel 中使用 `EXPAND` 函数 **how to expand array**、如何使用 Smart Markers **populate excel template**，以及如何构建能够自动适应源数据的 **dynamic range excel**。示例还演示了在真实的 C# 自动化场景中正确 **use expand function** 与 **expand array formula** 的方式。

接下来，您可以进一步扩展该方案：

* 将固定的 `5,5` 维度替换为 `ROWS(A2:A10), COLUMNS(A2:E2)`，实现真正的可变范围。
* 组合多个 Smart Markers 生成完整报告（例如员工列表、销售表格）。
* 探索 Aspose.Cells 的样式 API，自动为展开的区块设置格式。

欢迎尝试不同的源数组、标记名称和工作簿布局。祝编码愉快！


## 接下来您应该学习什么？

以下教程涵盖了与本指南技术密切相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式。每个资源都包含完整的可运行代码示例和逐步解释。

- [Export Data to Excel: Populate a Template from an Array in C#](/cells/english/net/smart-markers-dynamic-data/export-data-to-excel-populate-a-template-from-an-array-in-c/)
- [How to create array in Excel with C# – Step-by-Step Guide](/cells/english/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/)
- [Processing Data Using Array Function in Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}