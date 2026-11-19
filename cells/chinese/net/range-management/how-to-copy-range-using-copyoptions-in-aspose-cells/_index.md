---
category: general
date: 2026-11-19
description: 学习如何在 Aspose.Cells 中使用 CopyOptions 复制范围，在复制带格式的 Excel 区域时保留格式和数据透视表。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range using copyoptions
- copy excel range with formatting
- Aspose.Cells copy range
- preserve pivot tables Aspose
- Excel automation C#
language: zh
lastmod: 2026-11-19
og_description: 在 Aspose.Cells 中使用 CopyOptions 复制范围，可在保留完整格式和数据透视表的情况下复制 Excel 数据，实现可靠的工作簿操作。
og_image_alt: Screenshot of C# code that copies an Excel range using Aspose.Cells
  CopyOptions
og_title: 使用 Aspose.Cells 中的 CopyOptions 复制范围 – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  headline: How to copy range using CopyOptions in Aspose.Cells
  type: TechArticle
- description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  name: How to copy range using CopyOptions in Aspose.Cells
  steps:
  - name: Why `CopyOptions` matters
    text: '* **Performance** – The library performs a single internal operation rather
      than copying cells one‑by‑one. * **Accuracy** – All visual aspects (fonts, colors,
      borders) survive the move, which eliminates visual drift in generated reports.
      * **Reliability** – Pivot tables remain functional because the'
  - name: What if the destination area overlaps the source?
    text: 'Aspose.Cells throws an `ArgumentException`. To avoid this, calculate a
      destination that does not intersect the source, or copy to a different worksheet:'
  - name: How to copy between different workbooks?
    text: 'Create a second `Workbook` instance for the target file and use the same
      `CopyOptions` object:'
  - name: Does `CopyOptions` also copy merged cells?
    text: Yes. The `CopyStyle` flag includes merged‑cell information. If you need
      finer control, set `options.CopyMergedCells = true` (available in newer versions).
  - name: What about large ranges (thousands of rows)?
    text: The operation is memory‑efficient, but you may want to increase the `WorkbookSettings`
      `MemorySetting` to `MemorySetting.MemoryPreference` for very large files.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: 如何在 Aspose.Cells 中使用 CopyOptions 复制范围
url: /zh/net/range-management/how-to-copy-range-using-copyoptions-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.Cells 中的 CopyOptions 复制范围

如果您需要在 Aspose.Cells 中 **使用 CopyOptions 复制范围**，本指南将准确展示如何在保持所有格式和嵌入的透视表完整的情况下复制一块单元格。许多开发者在跨工作表移动数据时难以保留样式，而 `CopyOptions` 类能够在无需额外手动步骤的情况下解决此问题。

在本教程中，您将学习：

* 在 Excel 工作簿中定义源区域和目标区域。  
* 使用 `CopyOptions` 保留单元格格式、列宽以及透视表。  
* 将结果保存为新文件，以便后续处理。

该示例适用于任何 `.xlsx` 文件，仅需 Aspose.Cells for .NET 库。

## 前提条件

在开始之前，请确保您已具备：

* 已安装 .NET 6.0 或更高版本。  
* 有效的 Aspose.Cells for .NET 许可证（或免费评估密钥）。  
* Visual Studio 2022 或您喜欢的任何 C# IDE。  

除 `Aspose.Cells` 外，无需其他 NuGet 包。

## 第一步：设置项目并导入命名空间

创建一个新的控制台应用程序并添加 Aspose.Cells 引用：

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Your code will go here
        }
    }
}
```

`using Aspose.Cells;` 指令让您可以访问 `Workbook`、`CellArea` 和 `CopyOptions`。

## 第二步：加载要修改的工作簿

```csharp
// Step 2: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`Workbook` 代表整个 Excel 文件。将 `YOUR_DIRECTORY` 替换为包含源文件的文件夹路径。

## 第三步：定义源区域和目标区域

```csharp
// Step 3: Define the source range (A1:H30)
CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");

// Step 3b: Define the destination range (A35:H64)
CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");
```

`CellArea.CreateCellArea` 根据左上角和右下角单元格地址构建一个矩形区域。您可以根据需要复制的块大小调整坐标。

## 第四步：复制范围并保留格式和透视表

```csharp
// Step 4: Copy the range using CopyOptions
CopyOptions options = new CopyOptions
{
    // Preserve all cell styles, number formats, and column widths
    CopyStyle = true,
    // Keep formulas unchanged (they will still reference the original sheet)
    CopyFormula = true,
    // Preserve any pivot tables that intersect the copied area
    CopyPivotTables = true,
    // Retain data validation and conditional formatting
    CopyDataValidation = true,
    CopyConditionalFormatting = true
};

workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
```

`CopyOptions` 对象告诉 Aspose.Cells 需要保留哪些内容。将 `CopyPivotTables = true` 设置为 **使用 CopyOptions 复制范围** 的关键，当源区域包含透视表时必须如此。其他标志确保 **复制 Excel 范围并保留格式** 能自动实现——复制后无需额外代码重新应用样式。

### 为什么 `CopyOptions` 很重要

* **性能** – 库只执行一次内部操作，而不是逐个单元格复制。  
* **准确性** – 所有视觉属性（字体、颜色、边框）都会随移动保留下来，消除生成报告时的视觉漂移。  
* **可靠性** – 透视表保持可用，因为其缓存和源引用会被复制。

## 第五步：保存修改后的工作簿

```csharp
// Step 5: Save the workbook with the copied range
workbook.Save("YOUR_DIRECTORY/output.xlsx");
Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
```

调用 `Save` 后，文件 `output.xlsx` 将包含原始数据以及位于目标位置的复制块，完整保留格式和透视表。

## 完整源代码供参考

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // Define source and destination ranges
            CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");
            CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");

            // Configure copy options to preserve everything
            CopyOptions options = new CopyOptions
            {
                CopyStyle = true,
                CopyFormula = true,
                CopyPivotTables = true,
                CopyDataValidation = true,
                CopyConditionalFormatting = true
            };

            // Perform the copy operation
            workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);

            // Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");
            Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
        }
    }
}
```

运行此程序会输出：

```
Range copied successfully. Output saved to output.xlsx
```

在 Excel 中打开 `output.xlsx`——您会看到 A1:H30 区块被复制到 A35:H64，所有单元格颜色、边框、数字格式以及任何透视表均保持完整。

## 常见问题与边缘情况处理

### 如果目标区域与源区域重叠怎么办？

Aspose.Cells 会抛出 `ArgumentException`。为避免此情况，请计算一个不与源区域相交的目标位置，或复制到其他工作表：

```csharp
Worksheet destSheet = workbook.Worksheets.Add("CopySheet");
destSheet.Cells.CopyRange(sourceRange, CellArea.CreateCellArea("A1", "H30"), options);
```

### 如何在不同工作簿之间复制？

为目标文件创建第二个 `Workbook` 实例，并使用相同的 `CopyOptions` 对象：

```csharp
Workbook target = new Workbook();
target.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
target.Save("target.xlsx");
```

### `CopyOptions` 会复制合并单元格吗？

会。`CopyStyle` 标志包含合并单元格信息。如果需要更细粒度的控制，可设置 `options.CopyMergedCells = true`（在新版本中可用）。

### 大范围（数千行）怎么办？

该操作内存效率高，但对于超大文件，您可能需要将 `WorkbookSettings` 的 `MemorySetting` 调整为 `MemorySetting.MemoryPreference`。

## 专业技巧

* **复用同一个 `CopyOptions` 实例** 进行多次复制——可减少对象分配开销。  
* **在复制前验证区域**：`if (!CellArea.IsValid(sourceRange) || !CellArea.IsValid(destinationRange))` 有助于提前捕获因拼写错误导致的问题。  
* **关闭计算**（`workbook.Settings.CalcMode = CalculationMode.Manual`）在复制大数据集时可加速处理，复制完成后如需更新结果再调用 `workbook.CalculateFormula()`。

## 结论

现在您已经掌握了在 Aspose.Cells 中 **使用 CopyOptions 复制范围** 的方法，能够实现完整的 **复制 Excel 范围并保留格式**，同时保留透视表和其他高级特性。此方法消除了手动重新应用样式的步骤，确保您的 Excel 自动化既稳健又易于维护。

接下来您可以探索的方向：

* 使用 `CopyOptions` 复制整个工作表。  
* 将复制操作与 `WorksheetCollection.AddCopy` 结合，实现基于模板的报表生成。  
* 将代码集成到 ASP.NET Core API 中，提供即时的 Excel 转换服务。

欢迎尝试不同的源/目标坐标，并在评论区分享您的成果！

## 接下来应该学习什么？

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式。每篇资源均提供完整可运行的代码示例和逐步说明。

- [Excel Aspose Cells Dotnet Copy Range Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/french/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}