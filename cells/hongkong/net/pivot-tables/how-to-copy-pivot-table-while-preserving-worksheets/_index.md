---
category: general
date: 2026-09-15
description: 學習如何使用 Aspose.Cells 在 C# 中複製樞紐分析表、複製含樞紐分析表的工作表，以及將工作簿另存為 pptx。完整的逐步指南。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy worksheet with pivot
- save workbook as pptx
language: zh-hant
lastmod: 2026-09-15
og_description: 如何使用 Aspose.Cells 複製樞紐分析表、複製含有樞紐分析表的工作表，並將工作簿另存為 pptx。請參考完整且可執行的 C#
  範例。
og_image_alt: Screenshot showing how to copy pivot table in a C# code editor
og_title: 如何複製樞紐分析表並匯出工作表 – 完整 C# 指南
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
title: 如何在保留工作表的情況下複製樞紐分析表
url: /zh-hant/net/pivot-tables/how-to-copy-pivot-table-while-preserving-worksheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在保留工作表的情況下複製樞紐分析表

如果您需要 **how to copy pivot table** 從一個工作簿複製到另一個工作簿而不遺失底層的樞紐快取，本文提供即用的解決方案。您還會看到如何 **copy worksheet with pivot** 以及如何 **save workbook as pptx** 同時保留可編輯的文字方塊。所有範例皆使用最新的 Aspose.Cells for .NET，您只要把程式碼貼到任何 C# 專案即可立即看到結果。

以程式方式操作 Excel 檔案時，常會涉及在工作簿之間搬移資料、匯出成簡報，或插入複雜的 Smart Markers。以下三段程式碼示範了這些常見情境，並說明每一步的意義。

## 前置條件

在開始之前，請確保您已具備：

* 已安裝 .NET 6.0 或更新版本  
* 已在專案中參考 Aspose.Cells for .NET（版本 25.11 或更新）  
* 一個名為 `YOUR_DIRECTORY` 的資料夾，用來讀寫範例檔案  

不需要額外的 NuGet 套件。

---

## How to copy pivot table with Aspose.Cells

在保留樞紐快取的情況下複製包含樞紐分析表的範圍是常見需求。以下步驟示範了正確的操作順序。

### Step 1 – Load the source workbook that holds the pivot table

```csharp
// Load the workbook that contains the pivot table you want to copy
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
```

*Why*: Aspose.Cells 會將工作簿載入記憶體，讓您可以存取工作表、儲存格與樞紐分析表。

### Step 2 – Create an empty destination workbook

```csharp
// Create a new, empty workbook that will receive the copied data
Workbook destinationWorkbook = new Workbook();
```

*Why*: 從空白工作簿開始，可確保不會有隱藏樣式或命名範圍干擾複製動作。

### Step 3 – Copy the rows that include the pivot table

```csharp
// Copy rows 0‑19 (A1:G20) from the first worksheet of the source
sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20);
```

*Why*: `CopyRows` 會複製原始儲存格值、格式以及底層的樞紐快取參考。範圍必須涵蓋整個樞紐分析表區域。

### Step 4 – Copy the columns that contain the pivot table

```csharp
// Copy columns 0‑6 (A‑G) from the same worksheet
sourceWorkbook.Worksheets[0].Cells.CopyColumns(0, 0, 7);
```

*Why*: 樞紐分析表同時佔用列與欄，複製欄可確保完整的表格佈局被保留。

### Step 5 – Transfer the prepared sheet into the destination workbook

```csharp
// Move the fully prepared worksheet into the destination workbook
sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]);
```

*Why*: `Copy` 方法會克隆工作表，包含樞紐快取，因此目的工作簿會顯示相同的樞紐分析表。

### Step 6 – Save the result – the pivot table remains intact

```csharp
// Save the destination workbook; the pivot table works exactly like the original
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Why*: 儲存工作簿會寫入所有內部結構，保證之後仍能重新整理樞紐。

**Pro tip**: 複製完成後，您可以呼叫 `destinationWorkbook.Worksheets[0].PivotTables[0].Refresh()` 以在來源資料變更時更新樞紐。

---

## Copy worksheet with pivot – a concise alternative

如果您只需要複製整個已包含樞紐分析表的工作表，可以省略列/欄的複製步驟，直接使用工作表層級的 `Copy` 方法。

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

此作法適用於工作表內沒有樞紐區域之外的額外資料。**copy worksheet with pivot** 操作會自動保留所有格式、命名範圍與樞紐快取。

---

## Save workbook as PPTX with editable text boxes

將包含可編輯文字方塊的 Excel 工作表匯出成 PowerPoint，常用於報表儀表板。以下程式碼示範 **save workbook as pptx** 同時保留文字方塊可編輯的方式。

### Step 1 – Load the workbook that includes the textbox

```csharp
// Load the Excel file that contains an editable textbox shape
Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
```

### Step 2 – Configure PPTX save options

```csharp
// Create PPTX save options and enable the editable textbox feature (available from v25.11)
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableTextBox = true
};
```

*Why*: 設定 `ExportEditableTextBox` 可讓 Aspose.Cells 將 Excel 文字方塊轉換為 PowerPoint 中仍可編輯的形狀。

### Step 3 – Save the workbook as PPTX

```csharp
// Export the workbook to a PPTX file; the textbox stays editable in PowerPoint
workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
```

**Expected result**: 在 PowerPoint 開啟 `Result.pptx`，選取文字方塊後即可像本機形狀般編輯內容。

**Common question**: *What if I need to keep the textbox locked?*  
將 `pptxOptions.ExportEditableTextBox = false`，形狀將會被轉換為靜態影像。

---

## Export a Smart Marker that contains a JSON array as a single cell value

Smart Markers 讓您以複雜資料結構填充 Excel 範本。以下完整範例示範 **how to copy pivot table**‑style 的資料處理，同時將 JSON 陣列插入單一儲存格。

### Step 1 – Prepare the SmartMarkerProcessor

```csharp
// Initialise the processor that will fill Smart Markers
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
```

### Step 2 – Insert a Smart Marker into cell A1

```csharp
// The marker ${Orders:ArrayAsSingle} tells the processor to write the whole array into one cell
Workbook workbook = new Workbook();
workbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
```

### Step 3 – Define the data source with a JSON‑style array

```csharp
// Anonymous object that mimics a JSON array
var dataModel = new { Orders = new[] { "A", "B", "C" } };
```

### Step 4 – Process the workbook

```csharp
// Fill the Smart Marker with the array data; the array becomes a comma‑separated string
smartMarkerProcessor.Process(workbook, dataModel);
```

### Step 5 – Save the resulting workbook

```csharp
// Persist the workbook; cell A1 now contains "A,B,C"
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
```

**Result verification**: 開啟 `JsonSingleCell.xlsx`，確認 A1 儲存格顯示 `A,B,C`。此示例說明了如何將集合視為單一儲存格值，這在匯出給下游系統時常見。

---

## Full working example

以下是一個結合上述三種情境的完整程式。將程式碼貼到 Console App、調整檔案路徑後執行，即可看到全部三個輸出。

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

執行此程式會產生：

* `CopyWithPivot.xlsx` – 完整複製原始樞紐分析表的檔案。  
* `Result.pptx` – 含可編輯文字方塊的 PowerPoint 投影片。  
* `JsonSingleCell.xlsx` – JSON 陣列顯示於單一儲存格的工作表。

---

## 結論

您現在已掌握 **how to copy pivot table** 的安全做法、如何在一次呼叫中 **copy worksheet with pivot**，以及如何 **save workbook as pptx** 同時保留可編輯文字方塊。這些模式涵蓋了企業自動化專案中最常見的 Excel → PowerPoint 與 Excel → JSON 工作流程。

接下來可以探索：

* 以程式方式重新整理已複製的樞紐分析表 (`PivotTable.Refresh()`)  
* 匯出至其他格式，例如 PDF 或 HTML (`PdfSaveOptions`, `HtmlSaveOptions`)  
* 使用進階 Smart Marker 功能，如自訂函式或條件格式化  

歡迎嘗試不同的範圍、 多工作表或更大的 JSON 結構。Aspose.Cells API 提供精細的控制，讓您能將這些範例套用到任何實務情境。祝開發順利！

## What Should You Learn Next?

以下教學與本指南緊密相關，能進一步深化您所學的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，並在專案中探索其他實作方式。

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step‑By‑Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}