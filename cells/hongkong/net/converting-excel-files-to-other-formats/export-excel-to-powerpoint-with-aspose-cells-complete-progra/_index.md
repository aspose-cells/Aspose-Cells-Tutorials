---
category: general
date: 2026-08-14
description: 使用 Aspose.Cells 匯出 Excel 至 PowerPoint，並學習如何在程式碼中計算 Excel 公式。一步一步的 C#
  範例，附完整原始碼。
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
language: zh-hant
lastmod: 2026-08-14
og_description: 使用 Aspose.Cells 將 Excel 匯出至 PowerPoint，並在程式碼中計算 Excel 公式。遵循本完整指南，從活頁簿生成可編輯的
  PPTX 檔案。
og_image_alt: Screenshot showing an Excel sheet being exported to a PowerPoint slide
  with editable textboxes
og_title: 使用 Aspose.Cells 將 Excel 匯出至 PowerPoint – 完整 C# 教學
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
title: 使用 Aspose.Cells 將 Excel 匯出至 PowerPoint – 完整程式設計指南
url: /zh-hant/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-aspose-cells-complete-progra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將 Excel 匯出至 PowerPoint（使用 Aspose.Cells）– 完整程式指南

如果您需要以程式方式 **將 Excel 匯出至 PowerPoint**，本指南將向您展示如何使用 Aspose.Cells for .NET 完成此操作。您還將學習如何 **在程式碼中計算 Excel 公式**、在不遺失定義的情況下複製樞紐分析表，以及使用全新 Office‑365 EXPAND 函式處理動態陣列。

在以下章節中，我們將逐步示範一個真實的 C# 範例，說明每一行程式碼的意義，並探討常見的陷阱，讓您能將此解決方案套用到自己的專案中。

## 本教學涵蓋內容

* 載入既有活頁簿（`input.xlsx`）  
* 複製包含樞紐分析表的範圍，同時保留其定義  
* 將活頁簿匯出為 PowerPoint（`.pptx`）檔案，並保留可編輯的文字方塊與圖形  
* 使用自訂邏輯將儲存格範圍匯出為字串  
* 在程式碼中計算 Excel 公式，包含 Office‑365 EXPAND 函式  
* 儲存套用所有變更後的最終活頁簿  

**Prerequisites**  
* .NET 6.0 或更新版本（此程式碼同樣支援 .NET Framework 4.7.2+）  
* Aspose.Cells for .NET v25.11 或更新版本（`CopyPivotTable` 選項於 v25.11 引入）  
* 具備基本的 C# 與 Excel 概念，了解範圍、樞紐分析表與公式等  

> **Pro tip:** 透過 NuGet 安裝 Aspose.Cells（`Install-Package Aspose.Cells`）即可讓您的專案保持最新功能。

## Export Excel to PowerPoint with Aspose.Cells

將活頁簿轉換為 PowerPoint 簡報，同時保留所有視覺元素可編輯，這在需要自動產生財務報告或儀表板投影片時相當重要。

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

### 為什麼這樣可行

* **`Workbook`** 會將整個 Excel 檔案載入記憶體，讓您取得完整的 API 存取權限。  
* **`CopyRange`** 搭配 `CopyPivotTable = true` 可確保樞紐分析表的資料來源、快取與版面配置完整複製——這是舊版 Aspose.Cells 無法做到的。  
* 新增工作表（`Copy`）讓您保留原始工作表不被修改，對於稽核追蹤相當有用。  

## Export the workbook to PowerPoint with editable objects

現在我們將活頁簿轉成 PowerPoint 檔案。啟用 `ExportEditableObjects` 後，所有圖表、圖形或文字方塊都會變成 PowerPoint 原生物件，使用者在匯出後即可直接編輯。

```csharp
// Step 3: Export the workbook to PowerPoint with editable textboxes/shapes
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.Process();   // processes Smart Markers if present
designer.ExportToPptx("YOUR_DIRECTORY/output.pptx", new ExportOptions
{
    ExportEditableObjects = true   // makes objects editable in the PPTX
});
```

### Explanation

* **`WorkbookDesigner`** 是高階輔助類別，負責在匯出前準備活頁簿，處理 Smart Markers、命名範圍與版面調整。  
* 設定 `ExportEditableObjects = true` 會指示 Aspose.Cells 將 Excel 繪圖轉換為 PowerPoint 圖形，而非平面化為影像，從而產生 **完全可編輯** 的投影片。  

> **Edge case:** 若您的活頁簿包含從外部資料連線產生的複雜圖表，請務必在呼叫 `ExportToPptx` 前先解決這些連線，否則圖表可能會變成空白。

## Export a range as strings using custom logic

有時候您需要原始字串值以供後續處理（例如餵給 CSV 解析器）。`ExportTableOptions` 類別讓您自行決定每個儲存格的轉換方式。

```csharp
// Step 4: Export a range as strings using custom logic
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true,
    CustomExport = (cell, value) => value.ToString()   // simple conversion for each cell
};
workbook.Worksheets[0].Cells.ExportTableAsString(tableOptions, "A1:D10");
```

### 為什麼會這樣使用

* **Uniform data type:** 以字串匯出可避免當消費端預期文字時發生型別不匹配的錯誤。  
* **Custom formatting:** 可將 `value.ToString()` 替換為任何自訂格式（例如 `value.ToString("yyyy-MM-dd")` 以處理日期）。  

## Calculate Excel formulas in code

常見需求是 **在程式碼中計算 Excel 公式**，而不必開啟 Excel。Aspose.Cells 內建離線計算引擎，支援最新的 Office‑365 函式，包括 `EXPAND`。

```csharp
// Step 5: Use the new Office‑365 EXPAND function to create a dynamic array
Worksheet firstSheet = workbook.Worksheets[0];
firstSheet.Cells["A1"].Formula = "EXPAND(B1,5,3)";   // expands array starting at B1
workbook.CalculateFormula();   // forces recalculation of the formula
```

### How the calculation engine works

* `Formula` 屬性會完整保存您在 Excel 中輸入的公式字串。  
* `CalculateFormula()` 會觸發整本活頁簿的重新計算，並遵循儲存格之間的相依關係。  
* `EXPAND` 函式（Excel 365 可用）會根據來源儲存格（`B1`）以及指定的列數（`5`）與欄數（`3`）返回溢位範圍。  

> **Tip:** 若只需計算活頁簿的某個子集，請使用 `Worksheet.CalculateFormula()` 以限制計算範圍並提升效能。

## Save the workbook with all changes applied

最後，將修改過的活頁簿寫回磁碟。只要變更檔案副檔名，即可儲存為任何支援的格式（`.xlsx`、`.xls`、`.csv` 等）。

```csharp
// Step 6: Save the workbook with all changes applied
workbook.Save("YOUR_DIRECTORY/result.xlsx");
```

### What to verify

* 在 Excel 中開啟 `result.xlsx`，確認樞紐分析表已正確複製、`EXPAND` 公式結果正確，以及自訂匯出的字串是否如預期。  
* 在 PowerPoint 中開啟 `output.pptx`，您應該會看到與 Excel 版面相同的投影片，且所有圖表/文字方塊皆可編輯。  

## Common questions and troubleshooting

| Question | Answer |
|----------|--------|
| **Do I need a license to use Aspose.Cells?** | Yes. A trial works for evaluation, but a full license removes evaluation watermarks and unlocks the `CopyPivotTable` feature. |
| **What if the exported PPTX shows blank shapes?** | Verify that the workbook’s drawing objects are not hidden (`Visible = true`) and that any external image links are embedded before export. |
| **Can I export multiple worksheets to separate PPTX slides?** | Use `WorkbookDesigner.ExportToPptx` in a loop, specifying a different `ExportOptions` for each worksheet, or combine them into a single presentation by adding slides manually via Aspose.Slides. |
| **Is `CalculateFormula` thread‑safe?** | No. Perform calculations on a single thread or clone the workbook per thread to avoid race conditions. |

## Conclusion

您現在已掌握使用 Aspose.Cells **完整、端對端的 Excel 匯出至 PowerPoint 解決方案**，同時了解如何 **在程式碼中計算 Excel 公式**——包括現代的 `EXPAND` 函式。本教學涵蓋了載入活頁簿、複製樞紐分析表、匯出可編輯的 PowerPoint、客製字串匯出、公式計算與最終儲存等步驟。

接下來您可以：

* 將匯出擴充為每個工作表產生多張投影片（次要關鍵字：*calculate Excel formulas in code* 可在產生圖表資料時再次使用）。  
* 結合 Aspose.Slides 加入動畫或母片版面配置。  
* 用具備本地化格式的委派取代簡易的 `CustomExport`，以因應國際化專案需求。  

歡迎自行嘗試不同的儲存格範圍，探索其他 Office‑365 函式（例如 `FILTER`、`SORT`），並將此工作流程與自動化郵件傳送結合，打造全自動的報表管線。

---


## What Should You Learn Next?

以下教學與本指南緊密相關，能進一步深化您所學的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您在專案中掌握更多 API 功能或探索替代實作方式。

- [Automate Excel Data Export Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Export Excel Cells to Image Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}