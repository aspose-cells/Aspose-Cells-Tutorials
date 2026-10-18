---
category: general
date: 2026-05-23
description: 在 C# 中创建 Excel 工作簿，并学习如何使用 EXPAND 实现动态数组公式。一步步教程，教你写入 Excel 文件并添加示例数据。
draft: false
keywords:
- create excel workbook
- how to use expand
- dynamic array formula
- write excel file
- add sample data
language: zh
og_description: 在 C# 中创建 Excel 工作簿，掌握使用 EXPAND 实现动态数组公式的技巧。学习编写 Excel 文件、添加示例数据并实现电子表格自动化。
og_title: 在 C# 中创建 Excel 工作簿 – EXPAND 与动态数组指南
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create excel workbook in C# and learn how to use expand for dynamic
    array formulas. Step-by-step tutorial to write excel file and add sample data.
  headline: Create Excel Workbook with C# – Complete Guide to Using EXPAND
  type: TechArticle
- description: Create excel workbook in C# and learn how to use expand for dynamic
    array formulas. Step-by-step tutorial to write excel file and add sample data.
  name: Create Excel Workbook with C# – Complete Guide to Using EXPAND
  steps:
  - name: '**Dynamic chart generation** – link the spilled range to a chart object
      for live dashboards.'
    text: '**Dynamic chart generation** – link the spilled range to a chart object
      for live dashboards.'
  - name: '**Conditional formatting** – apply rules to the expanded area to highlight
      outliers.'
    text: '**Conditional formatting** – apply rules to the expanded area to highlight
      outliers.'
  - name: '**Export to CSV** – Aspose.Cells can also `Save(..., SaveFormat.Csv)` if
      you need a plain‑text version.'
    text: '**Export to CSV** – Aspose.Cells can also `Save(..., SaveFormat.Csv)` if
      you need a plain‑text version.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel Automation
title: 使用 C# 创建 Excel 工作簿 – 使用 EXPAND 的完整指南
url: /zh/net/excel-workbook/create-excel-workbook-with-c-complete-guide-to-using-expand/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 创建 Excel 工作簿 – 完整的 EXPAND 使用指南

是否曾想过如何使用 C# **create excel workbook** 从零开始？在本教程中我们将完整演示这一过程，并展示 **how to use expand** 来构建 **dynamic array formula**。我们还会讲解 **write excel file** 的步骤以及 **add sample data**，让你能够立刻看到结果。

如果你曾盯着电子表格思考“一定有办法以编程方式扩展这个范围”，那么你来对地方了。阅读完本教程后，你将拥有一个可运行的控制台应用，它能够扩展范围、填充值并保存文件——全部无需手动打开 Excel。

## 所需环境

- .NET 6（或任何近期的 .NET 版本）— 代码在 .NET Framework 上也可运行。  
- **Aspose.Cells for .NET** NuGet 包 — 为我们提供 `Workbook`、`Worksheet` 和 `EXPAND` 支持。  
- 常用的 IDE（Visual Studio、Rider 或 VS Code）。  

无需额外安装 Excel；Aspose.Cells 在内存中完成所有操作。

## 创建 Excel 工作簿 – 项目设置

要开始，请新建一个控制台项目并引入 Aspose.Cells 库：

```bash
dotnet new console -n ExcelExpandDemo
cd ExcelExpandDemo
dotnet add package Aspose.Cells
```

现在打开 `Program.cs`。我们首先要 **create excel workbook** 并获取默认工作表：

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();               // <-- create excel workbook
        Worksheet ws = wb.Worksheets[0];

        // (Optional) Add sample data so we have something to expand
        ws.Cells["A1"].PutValue(10);
        ws.Cells["A2"].PutValue(20);
        ws.Cells["A3"].PutValue(30);
```

> **为什么重要：** `Workbook` 是表示 Excel 文件的顶层对象。实例化它是 **create excel workbook** 的第一步；没有它就无法添加工作表、公式或其他任何内容。  
> 
> **小技巧：** 如果已经有模板文件，可将 `new Workbook()` 替换为 `new Workbook("template.xlsx")`，仍然可以在现有内容之上 **add sample data**。

## 如何使用 EXPAND 实现动态数组公式

真正的魔法在于 `EXPAND` 函数。它接受一个源范围，并根据你指定的行列数输出更大的数组。可以把它看作 Excel 内置的“向下填充”，但可以通过代码驱动。

```csharp
        // Step 2: Apply the EXPAND formula to cell A1
        // Syntax: =EXPAND(source, rows, columns)
        ws.Cells["A1"].Formula = "=EXPAND(A1:A3,5,1)";

        // Step 3: Force calculation so the expanded values appear
        wb.CalculateFormula();
```

> **发生了什么？**  
> * `A1:A3` 是已经包含三个数字的源范围。  
> * `5` 告诉 `EXPAND` 生成 **5 行**；默认情况下，多出的两行会重复最后一个值（30）。  
> * `1` 将列数保持为 **1**，因此仍在 A 列。  
> 
> **边界情况：** 如果源范围大于请求的大小，Excel 会截断多余的部分。这在你想限制溢出范围时非常有用。  
> 
> **替代方案：** 可以为行或列传入 `0` 让 Excel 自动决定。例如，`=EXPAND(A1:A3,0,2)` 会在保持原始行数的同时向右展开到两列。

## 向工作表添加示例数据

我们已经放入了一些数字，但让我们演示一个更真实的场景：从列表中提取数据后再进行扩展。

```csharp
        // Imagine we fetched these from a database
        int[] sales = { 150, 275, 320, 410 };
        for (int i = 0; i < sales.Length; i++)
        {
            ws.Cells[i, 1].PutValue(sales[i]); // Column B gets the raw sales numbers
        }

        // Now expand the sales column to a summary table with 8 rows
        ws.Cells["B1"].Formula = "=EXPAND(B1:B4,8,1)";
        wb.CalculateFormula();
```

> **为什么要添加？** 添加额外数据可以看到 **dynamic array formula** 在源数据增长时的表现。这也展示了在实际 ETL 流程中会重复使用的 **add sample data** 模式。

## 写入 Excel 文件并验证输出

工作簿准备好后，我们 **write excel file** 到磁盘。Aspose.Cells 支持多种格式，这里我们使用经典的 `.xlsx`。

```csharp
        // Step 4: Save the workbook – this writes the Excel file
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "ExpandedWorkbook.xlsx");
        wb.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

> **预期结果：**  
> - 单元格 **A1:A5** 包含 `10, 20, 30, 30, 30`。  
> - 单元格 **B1:B8** 包含 `150, 275, 320, 410, 410, 410, 410, 410`。  

在 Excel 中打开文件，你会看到公式产生的溢出范围完全符合预期，无需手动拖拽。

![Excel 工作簿中展开范围的截图](/images/expanded-range.png "创建 Excel 工作簿示例")

*图片 alt 文本:* **create excel workbook** – 使用 EXPAND 后展开范围的截图。

## 常见陷阱与技巧

- **公式重新计算：** 在设置公式后如果修改了源单元格，需要再次调用 `wb.CalculateFormula()`。否则溢出区域不会更新。  
- **零基索引 vs A1 表示法：** Aspose.Cells 既支持 `ws.Cells[0,0]` 也支持 `ws.Cells["A1"]`。混用会导致混淆，建议选定一种风格并坚持使用。  
- **性能：** 对于超大工作表，在整个工作簿上调用 `CalculateFormula` 代价高昂。使用 `ws.CalculateFormula()` 限制计算范围。  
- **版本兼容性：** `EXPAND` 是在 Excel 365 中引入的。旧版 Excel 会显示 `#NAME?`。如果需要向后兼容，可考虑使用 `OFFSET` 或手动循环实现。

## 后续步骤 – 扩展解决方案

既然已经掌握了 **create excel workbook**、**how to use expand** 与 **write excel file**，可以进一步探索：

1. **动态图表生成** – 将溢出范围链接到图表对象，实现实时仪表盘。  
2. **条件格式** – 对展开区域应用规则，以突出异常值。  
3. **导出为 CSV** – Aspose.Cells 也可以使用 `Save(..., SaveFormat.Csv)` 导出纯文本版本。  

上述每一步都建立在我们刚才搭建的 **dynamic array formula** 基础之上。

---

## 结论

本指南完整演示了在 C# 中 **create excel workbook** 的全过程，展示了 **how to use expand** 来实现 **dynamic array formula**，并说明了 **add sample data** 与 **write excel file** 的操作。代码自包含，只需一次 `dotnet run` 即可生成可立即打开的电子表格。

欢迎随意修改行列计数、替换示例数据源，或将多个 `EXPAND` 调用串联起来。将编程式 Excel 生成与现代数组函数结合，几乎没有限制。

有问题或想分享酷炫的使用案例？在下方留言吧，祝编码愉快！

## 相关教程

- [Excel 自动化：使用 Aspose.Cells for .NET 创建工作簿并添加 ListBox](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [如何使用 Aspose.Cells for .NET 在 Excel 中创建复选框 | 数据验证教程](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [如何在 Excel 中使用 Aspose.Cells .NET 创建工作簿作用域的命名范围](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}