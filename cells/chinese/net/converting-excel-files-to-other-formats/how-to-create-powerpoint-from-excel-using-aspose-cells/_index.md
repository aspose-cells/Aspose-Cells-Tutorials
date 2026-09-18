---
category: general
date: 2026-09-18
description: 使用 Aspose.Cells 从 Excel 创建 PowerPoint —— 复制数据透视表、导出范围，并用几行 C# 代码保存为 PPTX。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create powerpoint from excel
- how to copy pivot table
- copy range between workbooks
- how to export excel to pptx
- save workbook as pptx
language: zh
lastmod: 2026-09-18
og_description: 快速从 Excel 创建 PowerPoint。了解如何复制数据透视表、导出范围，并使用 Aspose.Cells 将工作簿保存为
  PPTX。
og_image_alt: Screenshot of a PowerPoint slide generated from Excel data
og_title: 使用 Aspose.Cells 从 Excel 创建 PowerPoint – 步骤指南
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  headline: How to create PowerPoint from Excel using Aspose.Cells
  type: TechArticle
- description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  name: How to create PowerPoint from Excel using Aspose.Cells
  steps:
  - name: Load the source workbook and define the range
    text: You must load the workbook that holds the source data and the pivot table.
      Selecting a precise range ensures that only the needed cells are transferred,
      which keeps the resulting slide lightweight.
  - name: Prepare the destination workbook
    text: Aspose.Cells treats a PowerPoint slide as a workbook when you save it in
      PPTX format. Creating a fresh workbook gives you a clean canvas for the copied
      range.
  - name: Copy the range while preserving the pivot table
    text: The `CopyRange` method accepts a `PasteOptions` object. Setting `CopyPivotTables
      = true` tells Aspose.Cells to keep the pivot table structure intact, not just
      the rendered values.
  - name: Save the workbook as a PowerPoint file
    text: Finally, export the workbook to PPTX format. The `SaveFormat.Pptx` flag
      tells Aspose.Cells to write the worksheet as a PowerPoint slide.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel to PowerPoint
title: 如何使用 Aspose.Cells 从 Excel 创建 PowerPoint
url: /zh/net/converting-excel-files-to-other-formats/how-to-create-powerpoint-from-excel-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.Cells 从 Excel 创建 PowerPoint

如果您需要从 Excel 创建 PowerPoint，本指南将为您展示一个简洁的端到端解决方案。您将看到如何复制数据透视表、导出选定范围，并仅用几行 C# 代码将结果保存为 PPTX 文件。

直接从电子表格数据生成幻灯片，省去了手动复制粘贴的步骤，从而加快报告工作流。教程涵盖了从项目设置到最终 PPTX 文件的全部内容，并且适用于最新的 Aspose.Cells for .NET。

## 前置条件

在开始之前，请确保您具备以下条件：

* **Aspose.Cells for .NET**（版本 23.12 或更高）。通过 NuGet 安装：`Install-Package Aspose.Cells`。
* **.NET 6+** 开发环境（Visual Studio 2022 或 VS Code 均可）。
* 包含数据和您想复用的数据透视表的 Excel 工作簿（`Source.xlsx`）。
* 对输出文件夹的写入权限。

不需要额外的第三方库。

## 从 Excel 创建 PowerPoint – 步骤详解

该过程由四个逻辑步骤组成，直接对应后面代码示例。

### 步骤 1：加载源工作簿并定义范围

您必须加载包含源数据和数据透视表的工作簿。精确选择范围可确保仅传输所需单元格，从而保持生成的幻灯片轻量。

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// Select the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that contains the pivot table and surrounding data
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

**为什么重要：**  
`CreateRange` 会创建一个可以整体复制的 `Range` 对象。将范围限制在 `A1:G20`，可以避免拉取无关单元格，防止 PowerPoint 文件体积膨胀。

### 步骤 2：准备目标工作簿

Aspose.Cells 在保存为 PPTX 格式时会将 PowerPoint 幻灯片视为工作簿。创建一个全新的工作簿即可为复制的范围提供干净的画布。

```csharp
// Create a new empty workbook that will become the PowerPoint slide
Workbook destinationWorkbook = new Workbook();

// Use the first worksheet of the new workbook
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

**提示：** 如果需要多个幻灯片，可以添加额外的工作表，随后分别保存为独立的 PPTX 文件。

### 步骤 3：复制范围并保留数据透视表

`CopyRange` 方法接受一个 `PasteOptions` 对象。将 `CopyPivotTables = true` 设置为 true，告诉 Aspose.Cells 保持数据透视表结构完整，而不仅仅是渲染后的数值。

```csharp
// Copy the defined range, preserving the pivot table definition
destinationSheet.Cells.CopyRange(
    sourceRange,
    new PasteOptions { CopyPivotTables = true });
```

**工作原理：**  
当 `CopyPivotTables` 为 true 时，目标工作表会同时收到源数据和数据透视缓存。这意味着数据透视表保持完整功能，后续若源数据变化仍可在 PowerPoint 中刷新。

### 步骤 4：将工作簿保存为 PowerPoint 文件

最后，将工作簿导出为 PPTX 格式。`SaveFormat.Pptx` 标志指示 Aspose.Cells 将工作表写入为 PowerPoint 幻灯片。

```csharp
// Save the destination workbook as a PowerPoint presentation
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);
```

**结果：**  
`CopyWithPivot.pptx` 可在 Microsoft PowerPoint（或任何兼容的查看器）中打开，包含一张显示复制范围的幻灯片，且其中的实时数据透视表可在 PowerPoint 中交互使用。

## 完整可运行示例

下面是完整程序代码，您可以将其粘贴到新的控制台项目中并立即运行。

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook and select the range containing the pivot table
            Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
            Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
            Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

            // 2️⃣ Create a fresh workbook that will become the PowerPoint slide
            Workbook destinationWorkbook = new Workbook();
            Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

            // 3️⃣ Copy the range, preserving the pivot table definition
            destinationSheet.Cells.CopyRange(
                sourceRange,
                new PasteOptions { CopyPivotTables = true });

            // 4️⃣ Export the workbook as a PPTX file
            destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);

            Console.WriteLine("PowerPoint file created successfully.");
        }
    }
}
```

**预期输出：**  
运行程序后会打印 “PowerPoint file created successfully.”，并生成名为 `CopyWithPivot.pptx` 的文件。用 PowerPoint 打开该文件，可看到一张幻灯片，复制的 Excel 范围与源工作表完全一致，并且包含一个可在 PowerPoint 中刷新 的活动数据透视表。

## 常见变体和边缘情况

| 情况 | 需要更改的内容 |
|-----------|----------------|
| **多个数据透视表** | 为每个表定义单独的 `Range` 对象并分别调用 `CopyRange`，或在它们共享同一数据源时复制整张工作表。 |
| **大数据集** | 增大范围（例如 `"A1:Z5000"`）。考虑启用 `PasteOptions.CompressData = true` 以减小 PPTX 大小。 |
| **不同的幻灯片布局** | 将文件保存为 PPTX 后，在 PowerPoint 中应用自定义布局或主题；数据仍保持可编辑。 |
| **保存到流** | 当需要通过 Web API 返回 PPTX 时，使用 `destinationWorkbook.Save(stream, SaveFormat.Pptx)`。 |
| **保留单元格格式** | 设置 `PasteOptions.PasteType = PasteType.All` 以保留字体、颜色和边框等格式。 |

**专业提示：** 在调用 `Save` 之前务必确认目标文件夹已存在。若文件夹不存在，`Save` 会抛出 `DirectoryNotFoundException`。

## 结论

现在您已经掌握了如何使用 Aspose.Cells 从 Excel 创建 PowerPoint、复制数据透视表并将结果导出为 PPTX 文件。加载源工作簿、定义范围、使用 `CopyPivotTables` 复制以及保存为 PPTX 的步骤，完整覆盖了可靠的生产级工作流。

接下来，您可以探索 **将多个工作表导出为 PPTX**，或学习 **在工作簿之间复制范围**，以在生成幻灯片之前合并来自多个源的数据。这两个主题基于相同的 API，能够组合使用，实现复杂的自动化报告管道。

祝编码愉快，玩转将电子表格转化为精美演示文稿的过程！

## 接下来您应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方式。

- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [How to Create and Save Excel Files with Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}