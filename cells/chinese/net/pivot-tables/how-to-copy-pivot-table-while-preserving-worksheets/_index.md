---
category: general
date: 2026-09-15
description: 学习如何使用 Aspose.Cells 在 C# 中复制数据透视表、复制包含数据透视表的工作表，以及将工作簿保存为 PPTX。完整的分步指南。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy worksheet with pivot
- save workbook as pptx
language: zh
lastmod: 2026-09-15
og_description: 如何使用 Aspose.Cells 复制数据透视表、复制包含数据透视表的工作表，并将工作簿保存为 pptx。请参阅完整可运行的 C#
  示例。
og_image_alt: Screenshot showing how to copy pivot table in a C# code editor
og_title: 如何复制透视表并导出工作表 – 完整的 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  headline: How to copy pivot table while preserving worksheets
  type: TechArticle
- description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  name: How to copy pivot table while preserving worksheets
  steps:
  - name: – Load the source workbook that holds the pivot table
    text: '```csharp // Load the workbook that contains the pivot table you want to
      copy Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx"); ```'
  - name: – Create an empty destination workbook
    text: '```csharp // Create a new, empty workbook that will receive the copied
      data Workbook destinationWorkbook = new Workbook(); ```'
  - name: – Copy the rows that include the pivot table
    text: '```csharp // Copy rows 0‑19 (A1:G20) from the first worksheet of the source
      sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20); ```'
  - name: – Copy the columns that contain the pivot table
    text: '```csharp // Copy columns 0‑6 (A‑G) from the same worksheet sourceWorkbook.Worksheets[0].Cells.CopyColumns(0,
      0, 7); ```'
  - name: – Transfer the prepared sheet into the destination workbook
    text: '```csharp // Move the fully prepared worksheet into the destination workbook
      sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]); ```'
  - name: – Save the result – the pivot table remains intact
    text: '```csharp // Save the destination workbook; the pivot table works exactly
      like the original destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
      ```'
  - name: – Load the workbook that includes the textbox
    text: '```csharp // Load the Excel file that contains an editable textbox shape
      Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
      ```'
  - name: – Configure PPTX save options
    text: '```csharp // Create PPTX save options and enable the editable textbox feature
      (available from v25.11) PptxSaveOptions pptxOptions = new PptxSaveOptions {
      ExportEditableTextBox = true }; ```'
  - name: – Save the workbook as PPTX
    text: '```csharp // Export the workbook to a PPTX file; the textbox stays editable
      in PowerPoint workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
      ```'
  - name: – Prepare the SmartMarkerProcessor
    text: '```csharp // Initialise the processor that will fill Smart Markers SmartMarkerProcessor
      smartMarkerProcessor = new SmartMarkerProcessor(); ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: 如何在保留工作表的情况下复制数据透视表
url: /zh/net/pivot-tables/how-to-copy-pivot-table-while-preserving-worksheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在保留工作表的情况下复制数据透视表

如果您需要 **how to copy pivot table** 从一个工作簿复制到另一个工作簿而不丢失底层的 pivot cache，本指南提供了可直接运行的解决方案。您还将看到如何 **copy worksheet with pivot** 以及如何 **save workbook as pptx** 同时保持可编辑的文本框完整。所有示例均使用最新的 Aspose.Cells for .NET，您可以将代码直接放入任何 C# 项目并立即看到效果。

以编程方式处理 Excel 文件时，通常会涉及在工作簿之间移动数据、导出到演示文稿或插入复杂的 Smart Markers。下面的三个代码片段覆盖了这些常见场景，并解释了每一步的意义。

## 先决条件

开始之前，请确保您具备：

* 已安装 .NET 6.0 或更高版本  
* 项目中已引用 Aspose.Cells for .NET（版本 25.11 或更新）  
* 一个名为 `YOUR_DIRECTORY` 的文件夹，用于读取和写入示例文件  

无需额外的 NuGet 包。

---

## 如何使用 Aspose.Cells 复制数据透视表

在保留 pivot cache 的情况下复制包含数据透视表的范围是常见需求。以下步骤演示了您需要的准确顺序。

### 第一步 – 加载包含数据透视表的源工作簿

```csharp
// Load the workbook that contains the pivot table you want to copy
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
```

*原因*：Aspose.Cells 将工作簿读取到内存中，您即可访问工作表、单元格和数据透视表。

### 第二步 – 创建一个空的目标工作簿

```csharp
// Create a new, empty workbook that will receive the copied data
Workbook destinationWorkbook = new Workbook();
```

*原因*：从空白工作簿开始可确保没有隐藏的样式或命名范围干扰复制操作。

### 第三步 – 复制包含数据透视表的行

```csharp
// Copy rows 0‑19 (A1:G20) from the first worksheet of the source
sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20);
```

*原因*：`CopyRows` 会复制原始单元格值、格式以及底层的 pivot cache 引用。范围必须覆盖整个数据透视表区域。

### 第四步 – 复制包含数据透视表的列

```csharp
// Copy columns 0‑6 (A‑G) from the same worksheet
sourceWorkbook.Worksheets[0].Cells.CopyColumns(0, 0, 7);
```

*原因*：数据透视表跨越行和列，复制列可确保完整的表格布局被保留。

### 第五步 – 将准备好的工作表转移到目标工作簿

```csharp
// Move the fully prepared worksheet into the destination workbook
sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]);
```

*原因*：`Copy` 方法会克隆工作表，包括 pivot cache，因此目标工作簿会显示完全相同的数据透视表。

### 第六步 – 保存结果 – 数据透视表保持完整

```csharp
// Save the destination workbook; the pivot table works exactly like the original
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*原因*：持久化工作簿会写入所有内部结构，保证以后可以刷新数据透视表。

**技巧提示**：复制后，您可以调用 `destinationWorkbook.Worksheets[0].PivotTables[0].Refresh()` 来在源数据更改后更新数据透视表。

---

## 复制带数据透视表的工作表 – 简洁替代方案

如果您只需要复制已经包含数据透视表的整个工作表，可以跳过行/列复制步骤，直接使用工作表级别的 `Copy` 方法。

```csharp
// Load source workbook
Workbook src = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

// Create destination workbook
Workbook dst = new Workbook();

// Copy the first worksheet (including its pivot table) to the destination
src.Worksheets[0].Copy(dst.Worksheets[0]);

// Save the new file
dst.Save("YOUR_DIRECTORY/WorksheetCopy.xlsx");
```

此方法适用于工作表中没有数据透视区域之外的额外数据的情况。**copy worksheet with pivot** 操作会自动保留所有格式、命名范围和 pivot cache。

---

## 将工作簿另存为 PPTX 并保持可编辑文本框

在报告仪表板中，可能需要将包含可编辑文本框的 Excel 工作表导出为 PowerPoint。下面的代码展示了 **save workbook as pptx** 同时保持文本框可编辑的实现方式。

### 第一步 – 加载包含文本框的工作簿

```csharp
// Load the Excel file that contains an editable textbox shape
Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
```

### 第二步 – 配置 PPTX 保存选项

```csharp
// Create PPTX save options and enable the editable textbox feature (available from v25.11)
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableTextBox = true
};
```

*原因*：设置 `ExportEditableTextBox` 可让 Aspose.Cells 将 Excel 文本框转换为 PowerPoint 中仍可编辑的形状。

### 第三步 – 将工作簿保存为 PPTX

```csharp
// Export the workbook to a PPTX file; the textbox stays editable in PowerPoint
workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
```

**预期结果**：在 PowerPoint 中打开 `Result.pptx`，选中文本框后即可像原生形状一样编辑其内容。

**常见问题**：*如果我需要将文本框锁定怎么办？*  
将 `pptxOptions.ExportEditableTextBox = false;`，形状将被转换为静态图片。

---

## 导出包含 JSON 数组的 Smart Marker 为单元格值

Smart Markers 让您可以使用复杂的数据结构填充 Excel 模板。下面的完整示例演示了 **how to copy pivot table** 风格的数据处理，同时将 JSON 数组插入单个单元格。

### 第一步 – 准备 SmartMarkerProcessor

```csharp
// Initialise the processor that will fill Smart Markers
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
```

### 第二步 – 在单元格 A1 中插入 Smart Marker

```csharp
// The marker ${Orders:ArrayAsSingle} tells the processor to write the whole array into one cell
Workbook workbook = new Workbook();
workbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
```

### 第三步 – 使用 JSON 风格的数组定义数据源

```csharp
// Anonymous object that mimics a JSON array
var dataModel = new { Orders = new[] { "A", "B", "C" } };
```

### 第四步 – 处理工作簿

```csharp
// Fill the Smart Marker with the array data; the array becomes a comma‑separated string
smartMarkerProcessor.Process(workbook, dataModel);
```

### 第五步 – 保存生成的工作簿

```csharp
// Persist the workbook; cell A1 now contains "A,B,C"
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
```

**结果验证**：打开 `JsonSingleCell.xlsx`，确认单元格 A1 显示 `A,B,C`。这演示了如何将集合视为单元格值的模式，常用于将数据导出到下游系统。

---

## 完整工作示例

下面是一段将上述三种场景合并的完整程序。您可以将代码复制到控制台应用中，调整文件路径后运行，即可看到全部输出。

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1. How to copy pivot table (preserve pivot cache)
        // -------------------------------------------------
        Workbook srcPivot = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Workbook dstPivot = new Workbook();
        srcPivot.Worksheets[0].Cells.CopyRows(0, 0, 20);
        srcPivot.Worksheets[0].Cells.CopyColumns(0, 0, 7);
        srcPivot.Worksheets[0].Copy(dstPivot.Worksheets[0]);
        dstPivot.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");

        // -------------------------------------------------
        // 2. Save workbook as PPTX with editable textbox
        // -------------------------------------------------
        Workbook txtWorkbook = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
        PptxSaveOptions pptxOpts = new PptxSaveOptions { ExportEditableTextBox = true };
        txtWorkbook.Save("YOUR_DIRECTORY/Result.pptx", pptxOpts);

        // -------------------------------------------------
        // 3. Export Smart Marker containing a JSON array
        // -------------------------------------------------
        SmartMarkerProcessor smProcessor = new SmartMarkerProcessor();
        Workbook smWorkbook = new Workbook();
        smWorkbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
        var model = new { Orders = new[] { "A", "B", "C" } };
        smProcessor.Process(smWorkbook, model);
        smWorkbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
    }
}
```

运行该程序后会生成：

* `CopyWithPivot.xlsx` – 完全复制原始数据透视表的文件。  
* `Result.pptx` – 包含可编辑文本框的 PowerPoint 幻灯片。  
* `JsonSingleCell.xlsx` – JSON 数组出现在单个单元格中的工作表。

---

## 结论

您现在已经掌握了安全 **how to copy pivot table** 的方法，了解了如何通过一次调用 **copy worksheet with pivot**，以及在 **save workbook as pptx** 时保持可编辑文本框的技巧。这些模式覆盖了企业自动化项目中最常见的 Excel‑to‑PowerPoint 与 Excel‑to‑JSON 工作流。

接下来可以进一步探索：

* 以编程方式刷新复制后的数据透视表 (`PivotTable.Refresh()`)  
* 导出为其他格式，如 PDF 或 HTML (`PdfSaveOptions`, `HtmlSaveOptions`)  
* 使用高级 Smart Marker 选项，如自定义函数或条件格式  

欢迎尝试不同的范围、多个工作表或更大的 JSON 结构。Aspose.Cells API 为您提供细粒度的控制，能够将这些示例适配到任何真实场景。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖了与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方案。

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step‑By‑Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}