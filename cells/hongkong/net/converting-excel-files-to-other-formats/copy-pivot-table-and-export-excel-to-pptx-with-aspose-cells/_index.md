---
category: general
date: 2026-09-11
description: 使用 Aspose.Cells 複製樞紐分析表並將 Excel 匯出為 PPTX。學習如何產生可編輯的 PPTX 並在 C# 中將工作簿另存為
  PPTX。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- export excel to pptx
- generate editable pptx
- save workbook as pptx
- export excel sheet pptx
language: zh-hant
lastmod: 2026-09-11
og_description: 使用 Aspose.Cells 在 C# 中複製樞紐分析表並將 Excel 匯出為 PPTX。只需幾行程式碼即可產生可編輯的 PPTX，並將活頁簿另存為
  PPTX。
og_image_alt: Screenshot of copy pivot table code and generated editable PPTX slide
og_title: 複製樞紐分析表並將 Excel 匯出至 PPTX – 完整 C# 教學
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Copy pivot table and export Excel to PPTX using Aspose.Cells. Learn
    to generate editable PPTX and save workbook as PPTX in C#.
  headline: Copy pivot table and export Excel to PPTX with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel
- PPTX
- Pivot Table
title: 複製樞紐分析表並使用 Aspose.Cells 將 Excel 匯出為 PPTX
url: /zh-hant/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 複製樞紐分析表並將 Excel 匯出為 PPTX（使用 Aspose.Cells）

如果您需要將樞紐分析表從一個工作表複製到另一個工作表，然後將 Excel 檔案匯出為 PowerPoint 簡報，本指南將教您如何操作。使用 Aspose.Cells，您只需幾行 C# 程式碼即可產生可編輯的 PPTX，並將活頁簿另存為 PPTX。

本教學涵蓋了移動樞紐分析表、保留其功能以及產生 PPTX 檔案的每一步，圖表與圖形將保持可編輯。無需任何外部工具——只需 Aspose.Cells 程式庫與 .NET 開發環境。

## 您將達成的目標

* **Copy pivot table**：將樞紐分析表從來源工作表複製到目標工作表，同時保留所有資料連結。  
* **Export Excel to PPTX**：使產生的投影片可在 PowerPoint 中編輯。  
* **Generate editable PPTX**：產生的 PPTX 中圖表、表格與圖形不會被平面化為圖片。  
* **Save workbook as PPTX**：使用相同的 Aspose.Cells API 呼叫將活頁簿另存為 PPTX。  

### 前置條件

* .NET 6.0 或更新版本（程式碼亦相容於 .NET Framework 4.6 以上）。  
* Aspose.Cells for .NET（NuGet 套件 `Aspose.Cells`）。  
* 具備 C# 主控台應用程式的基本概念。  

> **專業提示:** 透過 CLI 安裝 NuGet 套件，以確保取得最新版本：  
> ```bash
> dotnet add package Aspose.Cells
> ```

## 如何在工作表之間複製樞紐分析表

第一個動作是搬移樞紐分析表，同時保留其定義。Aspose.Cells 提供 `CopyRange` 方法，搭配包含 `CopyPivotTable` 旗標的 `CopyOptions` 物件。

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Load the workbook that contains the source and destination worksheets.
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Identify the worksheets by name.
Worksheet sourceSheet = workbook.Worksheets["Source"];
Worksheet destinationSheet = workbook.Worksheets["Destination"];

// Define the range that encloses the pivot table on the source sheet.
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

// Copy the range to the destination sheet, preserving the pivot table.
destinationSheet.Cells.CopyRange(
    sourceRange,
    0,                     // destination row index
    0,                     // destination column index
    new CopyOptions { CopyPivotTable = true });
```

**為什麼這樣有效：**  
`CopyRange` 會複製儲存格資料、格式，且當 `CopyPivotTable` 為 true 時，會一併複製樞紐分析表的快取與中繼資料。目的範圍預設從儲存格 `A1`（第 0 列，第 0 欄）開始，您可以調整偏移量以將樞紐分析表放置於其他位置。

**常見邊緣情況：** 若目標工作表已存在同名的樞紐分析表，Aspose.Cells 會自動重新命名新匯入的表格，以避免名稱衝突。

## 匯出 Excel 為 PPTX 並產生可編輯的 PPTX

樞紐分析表就位後，您可以將整個活頁簿匯出為 PPTX 檔案。`ImageOrPrintOptions` 類別允許您設定 `ExportImageFormat = ImageFormat.Pptx`，告訴 Aspose.Cells 將輸出視為 PowerPoint 簡報，而非點陣圖。

```csharp
// Configure export options to produce an editable PPTX.
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ExportImageFormat = ImageFormat.Pptx
};

// Save the workbook as an editable PPTX file.
workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);
```

**為什麼這樣有效：**  
當 `ExportImageFormat` 設為 `Pptx` 時，Aspose.Cells 會將每個工作表轉換為一張投影片。圖形、圖表與樞紐分析表會以原生 PowerPoint 物件寫入，您可在 PowerPoint 中雙擊它們並編輯底層資料。

**大型活頁簿的提示：** 若只需要匯出部分工作表，可在呼叫 `Save` 前使用 `workbook.Worksheets.RemoveAt(index)` 移除不需要的工作表，這樣可減少 PPTX 檔案大小。

## 完整、可執行的範例

以下是將前述步驟串接起來的完整程式。請將 `YOUR_DIRECTORY` 替換為您機器上的實際路徑。

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Export;

class Example
{
    static void Main()
    {
        // 1. Load the workbook that contains the source and destination worksheets.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Identify the source and destination worksheets.
        Worksheet sourceSheet = workbook.Worksheets["Source"];
        Worksheet destinationSheet = workbook.Worksheets["Destination"];

        // 3. Define the range that holds the pivot table.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // 4. Copy the range, preserving the pivot table.
        destinationSheet.Cells.CopyRange(
            sourceRange,
            0,
            0,
            new CopyOptions { CopyPivotTable = true });

        // 5. Set up export options to generate an editable PPTX.
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
        {
            ExportImageFormat = ImageFormat.Pptx
        };

        // 6. Save the workbook as a PPTX document.
        workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);

        Console.WriteLine("Pivot table copied and workbook exported to PPTX successfully.");
    }
}
```

### 預期輸出

執行程式會印出：

```
Pivot table copied and workbook exported to PPTX successfully.
```

當您在 Microsoft PowerPoint 中開啟 `output.pptx` 時，會看到一張投影片，內含已複製的樞紐分析表，且以可編輯的圖表形式呈現。雙擊圖表即可開啟 PowerPoint 圖表編輯器，讓您在不返回 Excel 的情況下修改系列、座標軸與資料標籤。

## 處理常見陷阱

| 問題 | 原因 | 解決方案 |
|-------|-------|-----|
| 樞紐分析表顯示為靜態圖片 | `CopyPivotTable` 旗標未設定或 `ExportImageFormat` 設為 `Png` | 確保 `CopyPivotTable = true` 且 `ExportImageFormat = ImageFormat.Pptx`。 |
| 目標工作表顯示空白儲存格 | 來源範圍未涵蓋整個樞紐分析表區域 | 擴大範圍（例如 `"A1:H30"`）以包含所有樞紐欄位。 |
| 匯出的 PPTX 體積過大 | 包含了不必要的工作表 | 在呼叫 `Save` 前移除不需要的工作表。 |
| PowerPoint 無法編輯圖表 | 使用不支援 PPTX 的舊版 Aspose.Cells | 升級至最新的 Aspose.Cells 版本（請參閱發行說明）。 |

## 下一步與相關主題

* **Export Excel sheet to PPTX with custom slide layouts** – 探索 `WorksheetToPdfConverter` 以更細緻地控制投影片外觀。  
* **Export Excel to PDF** – 將 `ImageFormat.Pptx` 改為 `ImageFormat.Pdf` 即可產生 PDF。  
* **Programmatically modify PPTX after export** – 使用 `Aspose.Slides` 套件加入動畫或講者備註。  

透過精通 **copy pivot table**、**export excel to pptx** 與 **generate editable pptx**，您可以建立端對端的報表管線，將資料直接從試算表移至簡報檔案，同時保持可編輯性。

---


## 您接下來應該學習什麼？

以下教學涵蓋與本指南技術緊密相關的主題，並在此基礎上延伸。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，並在自己的專案中探索替代實作方式。

- [如何在 C# 中複製樞紐分析表 – 將 Excel 轉為 PPTX、複製範圍與建立文字方塊](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [建立新 Excel 活頁簿 – 複製與重製樞紐分析表](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [使用 Aspose.Cells for .NET 在 Excel 中建立樞紐分析表](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}