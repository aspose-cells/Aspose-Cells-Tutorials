---
category: general
date: 2026-10-20
description: 使用 Aspose.Cells 将数据透视表复制到新工作簿，并在同一指南中学习如何将可编辑形状导出到 PowerPoint。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table to new workbook
- copy rows between worksheets
- Aspose.Cells copy rows
- export shape to PowerPoint
- editable textbox in PowerPoint
language: zh
lastmod: 2026-10-20
og_description: 使用 Aspose.Cells 将数据透视表复制到新工作簿，并将可编辑形状导出到 PowerPoint——一步一步的代码，您今天即可运行。
og_image_alt: Screenshot showing copy pivot table to new workbook using Aspose.Cells
og_title: 将数据透视表复制到新工作簿，导出形状到 PowerPoint
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  headline: Copy pivot table to new workbook, export shape to PowerPoint
  type: TechArticle
- description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  name: Copy pivot table to new workbook, export shape to PowerPoint
  steps:
  - name: – Load the source workbook and select the first worksheet
    text: '```csharp // Load the workbook that already contains the pivot table Workbook
      srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");'
  - name: – Define the cell area that includes the pivot table
    text: '```csharp // CellArea(startRow, startColumn, endRow, endColumn) // Here
      we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table CellArea
      sourceArea = new CellArea(0, 0, 20, 10); ```'
  - name: – Create the destination workbook and get its first worksheet
    text: '```csharp // Create an empty workbook that will receive the copied range
      Workbook destWorkbook = new Workbook();'
  - name: – Copy the rows from the source area to the destination sheet
    text: '```csharp // CopyRows(startRow, endRow, destinationCells, destinationStartRow)
      srcWorksheet.Cells.CopyRows( sourceArea.StartRow, sourceArea.EndRow, destWorksheet.Cells,
      0); // start at row 0 in the destination sheet ```'
  - name: – Save the new workbook
    text: '```csharp destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx"); ```'
  - name: – Create a new workbook and access its first worksheet
    text: '```csharp Workbook workbook = new Workbook(); // Empty workbook Worksheet
      worksheet = workbook.Worksheets[0]; // First (and only) sheet ```'
  - name: – Add a textbox shape to the worksheet
    text: '```csharp // AddTextBox(startRow, startColumn, width, height, text) int
      shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
      ```'
  - name: – Retrieve the shape and modify its text
    text: '```csharp Shape textShape = worksheet.Shapes[shapeIndex]; textShape.Text
      = "Change me in PowerPoint"; ```'
  - name: – Save the workbook as a PowerPoint presentation
    text: '```csharp workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
      ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Pivot Table
- PowerPoint Export
title: 复制数据透视表到新工作簿，导出形状到 PowerPoint
url: /zh/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 复制数据透视表到新工作簿，导出形状到 PowerPoint

如果您需要在保持功能的前提下 **复制数据透视表到新工作簿**，本指南将向您展示如何使用 Aspose.Cells 完成此操作。您还将看到 **导出可编辑形状到 PowerPoint** 的最快方法，以便在转换后文本框仍保持可编辑。

许多开发者认为复制包含数据透视表的范围会丢失数据透视逻辑，或者形状在保存为 PPTX 时会变成静态图像。本教程驳斥了这些误解，并为您提供可靠的、可投入生产的解决方案。

在以下章节中，您将：

* 加载源工作簿并复制包含数据透视表的范围。
* 创建包含相同数据透视表的目标工作簿。
* 添加文本框形状，修改其文本，并将工作簿保存为 PowerPoint 演示文稿，使文本框保持可编辑。
* 了解每个 API 调用的必要性以及如何避免常见陷阱。

**Prerequisites**

* .NET 6.0 或更高版本（代码同样适用于 .NET Framework 4.7+）。
* 已安装 Aspose.Cells for .NET（`Install-Package Aspose.Cells`）。
* 具备 C# 和 Visual Studio（或您偏好的任何 IDE）的基础知识。

---

## 复制数据透视表到新工作簿

本分步章节演示如何复制包含数据透视表的范围，并在新文件中保留数据透视定义。

### Step 1 – Load the source workbook and select the first worksheet

```csharp
// Load the workbook that already contains the pivot table
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// The first worksheet (index 0) holds the pivot table we want to copy
Worksheet srcWorksheet = srcWorkbook.Worksheets[0];
```

*Why?*  
`Workbook` 是 Aspose.Cells 中进行任何 Excel 操作的入口。选择正确的工作表可确保我们操作的是确切的数据透视表所在位置。

### Step 2 – Define the cell area that includes the pivot table

```csharp
// CellArea(startRow, startColumn, endRow, endColumn)
// Here we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table
CellArea sourceArea = new CellArea(0, 0, 20, 10);
```

*Why?*  
数据透视表位于特定的单元格块中。通过指定完整包围数据透视表的 `CellArea`，Aspose.Cells 能够同时复制其底层的数据透视缓存。

### Step 3 – Create the destination workbook and get its first worksheet

```csharp
// Create an empty workbook that will receive the copied range
Workbook destWorkbook = new Workbook();

// Destination worksheet (also index 0)
Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Why?*  
全新的工作簿可保证没有冲突的命名范围或已有的数据透视表，使复制操作更加干净。

### Step 4 – Copy the rows from the source area to the destination sheet

```csharp
// CopyRows(startRow, endRow, destinationCells, destinationStartRow)
srcWorksheet.Cells.CopyRows(
    sourceArea.StartRow,
    sourceArea.EndRow,
    destWorksheet.Cells,
    0); // start at row 0 in the destination sheet
```

*Why?*  
`CopyRows` 是 **Aspose.Cells copy rows** API 的一部分。它会复制单元格值以及隐藏的数据透视缓存，从而在移动后数据透视表仍保持可用。

### Step 5 – Save the new workbook

```csharp
destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Result*  
在 Excel 中打开 `CopyWithPivot.xlsx`。数据透视表与源文件完全一致，您可以正常刷新或修改它。

---

## Export editable shape to PowerPoint

接下来我们将添加一个文本框形状，修改其内容，并将工作簿保存为 PPTX 文件。打开 PowerPoint 时，形状仍保持完全可编辑。

### Step 1 – Create a new workbook and access its first worksheet

```csharp
Workbook workbook = new Workbook();          // Empty workbook
Worksheet worksheet = workbook.Worksheets[0]; // First (and only) sheet
```

### Step 2 – Add a textbox shape to the worksheet

```csharp
// AddTextBox(startRow, startColumn, width, height, text)
int shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
```

*Why?*  
`AddTextBox` 创建一个 **可在 PowerPoint 中编辑的文本框** 形状。坐标使用点（points）单位，请根据布局自行调整。

### Step 3 – Retrieve the shape and modify its text

```csharp
Shape textShape = worksheet.Shapes[shapeIndex];
textShape.Text = "Change me in PowerPoint";
```

*Why?*  
直接访问 `Shape` 对象可以更改 `Text`、`Font`、`Fill` 等属性。本步骤演示如何以编程方式设置初始内容。

### Step 4 – Save the workbook as a PowerPoint presentation

```csharp
workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
```

*Result*  
在 Microsoft PowerPoint 中打开 `Presentation.pptx`。文本框出现在第一张幻灯片上，您可以双击它像编辑原生 PowerPoint 形状一样进行编辑。

---

## Expected output

| File | What you’ll see |
|------|-----------------|
| `CopyWithPivot.xlsx` | 包含原始数据透视表的工作表，功能完整（可刷新）。 |
| `Presentation.pptx` | 单个幻灯片，包含可编辑的文本框，内容为 “Change me in PowerPoint”。 |

---

## Common pitfalls and best‑practice tips

* **Pivot cache loss** – 如果仅复制单元格值（例如使用 `CopyRows` 并将 `PasteOptions` 标志设为 `PasteValues`），则会省略数据透视缓存，表格会变为静态。请始终使用如示例所示的默认 `CopyRows` 重载。
* **Shape positioning** – `AddTextBox` 使用点单位，而非 Excel 单元格索引。请在示例文件中测试坐标，以避免形状偏离幻灯片。
* **File format mismatch** – 使用 `SaveFormat.Pptx` 将工作簿保存为 PPTX 时，所有受支持的形状会自动转换。若尝试保存为 `Pdf`，形状会被光栅化，导致不可编辑。

---

## Conclusion

您现在已经掌握了如何使用 Aspose.Cells for .NET **复制数据透视表到新工作簿**，以及如何 **导出可编辑形状到 PowerPoint**。完整、可运行的代码示例涵盖了所有必需的 API 调用，解释了每一步的意义，并展示了预期结果。

接下来，您可以进一步探索：

* **Working with charts** – copy charts together with pivot tables (`Aspose.Cells copy rows between worksheets`)。
* 

## What Should You Learn Next?

以下教程涵盖与本指南技术紧密相关的主题，帮助您进一步掌握 API 功能并在项目中探索替代实现方案。

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy pivot table and export Excel to PPTX with Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/)
- [Create New Workbook in C# – Copy Pivot Table](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}