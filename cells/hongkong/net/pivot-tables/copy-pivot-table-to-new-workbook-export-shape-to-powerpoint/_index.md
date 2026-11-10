---
category: general
date: 2026-10-20
description: 使用 Aspose.Cells 複製樞紐分析表至新活頁簿，並在單一指南中學習如何將可編輯的圖形匯出至 PowerPoint。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table to new workbook
- copy rows between worksheets
- Aspose.Cells copy rows
- export shape to PowerPoint
- editable textbox in PowerPoint
language: zh-hant
lastmod: 2026-10-20
og_description: 使用 Aspose.Cells 複製樞紐分析表至新活頁簿，並將可編輯的圖形匯出至 PowerPoint——一步一步的程式碼，您今天即可執行。
og_image_alt: Screenshot showing copy pivot table to new workbook using Aspose.Cells
og_title: 將樞紐分析表複製到新工作簿，將形狀匯出至 PowerPoint
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
title: 將樞紐分析表複製到新工作簿，匯出形狀至 PowerPoint
url: /zh-hant/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 複製樞紐分析表至新活頁簿，將圖形匯出至 PowerPoint

如果您需要在保留功能的前提下 **copy pivot table to new workbook**，本指南將向您展示如何使用 Aspose.Cells 完成。您還會看到將 **export an editable shape to PowerPoint** 的最快方法，讓文字方塊在轉換後仍可編輯。

許多開發人員會假設，複製包含樞紐分析表的範圍會失去樞紐分析的邏輯，或是圖形在儲存為 PPTX 時會變成靜態圖片。本教學將推翻這些迷思，並提供可靠、可投入生產環境的解決方案。

在以下章節中您將：

* 載入來源活頁簿並複製包含樞紐分析表的範圍。  
* 建立包含相同樞紐分析表的目標活頁簿。  
* 新增文字方塊圖形、修改其文字，並將活頁簿儲存為 PowerPoint 簡報，使文字方塊保持可編輯。  
* 了解每個 API 呼叫的必要性以及如何避免常見陷阱。

**Prerequisites**

* .NET 6.0 或更新版本（程式碼同樣適用於 .NET Framework 4.7+）。  
* 已安裝 Aspose.Cells for .NET（`Install-Package Aspose.Cells`）。  
* 具備 C# 與 Visual Studio（或您偏好的任何 IDE）的基本知識。

---

## Copy pivot table to new workbook

本步驟說明將示範如何複製包含樞紐分析表的範圍，並在新檔案中保留樞紐分析的定義。

### Step 1 – Load the source workbook and select the first worksheet

```csharp
// Load the workbook that already contains the pivot table
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// The first worksheet (index 0) holds the pivot table we want to copy
Worksheet srcWorksheet = srcWorkbook.Worksheets[0];
```

*Why?*  
`Workbook` 是 Aspose.Cells 進行任何 Excel 操作的入口點。選取正確的工作表可確保我們操作的正是目標樞紐分析表所在位置。

### Step 2 – Define the cell area that includes the pivot table

```csharp
// CellArea(startRow, startColumn, endRow, endColumn)
// Here we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table
CellArea sourceArea = new CellArea(0, 0, 20, 10);
```

*Why?*  
樞紐分析表位於特定的儲存格區塊。透過指定完整包住樞紐的 `CellArea`，Aspose.Cells 便會同時複製底層的樞紐快取。

### Step 3 – Create the destination workbook and get its first worksheet

```csharp
// Create an empty workbook that will receive the copied range
Workbook destWorkbook = new Workbook();

// Destination worksheet (also index 0)
Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Why?*  
全新活頁簿可避免命名範圍或既有樞紐衝突，使複製作業更加乾淨。

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
`CopyRows` 屬於 **Aspose.Cells copy rows** API。它會同時複製儲存格值與隱藏的樞紐快取，讓樞紐分析表在搬移後仍保持功能。

### Step 5 – Save the new workbook

```csharp
destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Result*  
在 Excel 中開啟 `CopyWithPivot.xlsx`。樞紐分析表會與來源檔案完全相同，且可正常重新整理或修改。

---

## Export editable shape to PowerPoint

接下來我們會新增文字方塊圖形、變更內容，並將活頁簿儲存為 PPTX 檔案。開啟於 PowerPoint 時，圖形仍可完整編輯。

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
`AddTextBox` 會建立 **editable textbox in PowerPoint** 相容的圖形。座標單位為點（points），請依需求調整以符合版面配置。

### Step 3 – Retrieve the shape and modify its text

```csharp
Shape textShape = worksheet.Shapes[shapeIndex];
textShape.Text = "Change me in PowerPoint";
```

*Why?*  
直接存取 `Shape` 物件即可變更 `Text`、`Font`、`Fill` 等屬性。此步驟示範如何以程式方式設定初始內容。

### Step 4 – Save the workbook as a PowerPoint presentation

```csharp
workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
```

*Result*  
在 Microsoft PowerPoint 中開啟 `Presentation.pptx`。文字方塊會出現在第一張投影片上，您可以雙擊它來編輯文字，就像原生 PowerPoint 圖形一樣。

---

## Expected output

| File | What you’ll see |
|------|-----------------|
| `CopyWithPivot.xlsx` | 包含原始樞紐分析表的工作表，功能完整（可重新整理）。 |
| `Presentation.pptx` | 單一投影片，內有可編輯的文字方塊，內容為 “Change me in PowerPoint”。 |

---

## Common pitfalls and best‑practice tips

* **Pivot cache loss** – 若僅複製儲存格值（例如使用 `CopyRows` 並將 `PasteOptions` 設為 `PasteValues`），樞紐快取會被省略，表格會變成靜態。請務必使用如範例所示的預設 `CopyRows` 重載。  
* **Shape positioning** – `AddTextBox` 使用點為單位，而非 Excel 的儲存格索引。建議先在樣本檔案上測試座標，以免圖形跑到投影片外。  
* **File format mismatch** – 以 `SaveFormat.Pptx` 儲存活頁簿時會自動轉換所有支援的圖形。若改以 `Pdf` 儲存，圖形會被光柵化，失去可編輯性。

---

## Conclusion

您現在已掌握如何 **copy pivot table to new workbook** 以及如何 **export an editable shape to PowerPoint**，全部使用 Aspose.Cells for .NET。完整且可執行的程式碼範例涵蓋所有必要的 API 呼叫，說明每一步的原因，並展示預期結果。

接下來，您可以探索：

* **Working with charts** – copy charts together with pivot tables (`Aspose.Cells copy rows between worksheets`)。  
* 

## What Should You Learn Next?

以下教學與本指南的技巧密切相關，能進一步深化您的應用：

- [建立新活頁簿 – 複製含樞紐分析表的工作表](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [複製樞紐分析表並將 Excel 匯出為 PPTX（使用 Aspose.Cells）](/cells/english/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/)
- [C# 建立新活頁簿 – 複製樞紐分析表](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}