---
category: general
date: 2026-09-18
description: 使用 Aspose.Cells 從 Excel 建立 PowerPoint – 複製樞紐分析表、匯出範圍，並以幾行 C# 程式碼儲存為 PPTX。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create powerpoint from excel
- how to copy pivot table
- copy range between workbooks
- how to export excel to pptx
- save workbook as pptx
language: zh-hant
lastmod: 2026-09-18
og_description: 快速從 Excel 建立 PowerPoint。了解如何複製樞紐分析表、匯出範圍，並使用 Aspose.Cells 將活頁簿儲存為
  PPTX。
og_image_alt: Screenshot of a PowerPoint slide generated from Excel data
og_title: 使用 Aspose.Cells 從 Excel 建立 PowerPoint – 逐步指南
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
title: 如何使用 Aspose.Cells 從 Excel 建立 PowerPoint
url: /zh-hant/net/converting-excel-files-to-other-formats/how-to-create-powerpoint-from-excel-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.Cells 從 Excel 建立 PowerPoint

如果您需要從 Excel 建立 PowerPoint，本指南將提供簡潔、端到端的解決方案。您將看到如何複製樞紐分析表、匯出選取的範圍，並僅用幾行 C# 程式碼將結果儲存為 PPTX 檔案。

直接從試算表資料產生投影片，可省去手動複製貼上的步驟，提升報表工作流程的效率。本教學涵蓋從專案設定到最終 PPTX 檔案的全部步驟，且適用於最新的 Aspose.Cells for .NET。

## 前置條件

開始之前，請確保您已具備：

* **Aspose.Cells for .NET**（版本 23.12 或更新）。可透過 NuGet 安裝：`Install-Package Aspose.Cells`。
* **.NET 6+** 開發環境（Visual Studio 2022 或 VS Code 都可）。
* 一個包含欲重複使用資料與樞紐分析表的 Excel 活頁簿（`Source.xlsx`）。
* 輸出資料夾的寫入權限。

不需要額外的第三方函式庫。

## 從 Excel 建立 PowerPoint – 步驟說明

此流程分為四個邏輯步驟，與稍後的程式碼範例直接對應。

### 步驟 1：載入來源活頁簿並定義範圍

必須先載入包含來源資料與樞紐分析表的活頁簿。精確選取範圍可確保只傳輸所需的儲存格，讓最終投影片保持輕量。

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

**為什麼這很重要：**  
`CreateRange` 會建立一個可一次性複製的 `Range` 物件。將範圍限制在 `A1:G20`，即可避免拉入不相關的儲存格，防止 PowerPoint 檔案變得過大。

### 步驟 2：準備目的地活頁簿

Aspose.Cells 在儲存為 PPTX 格式時，會將 PowerPoint 投影片視為活頁簿。建立全新的活頁簿即可為複製的範圍提供乾淨的畫布。

```csharp
// Create a new empty workbook that will become the PowerPoint slide
Workbook destinationWorkbook = new Workbook();

// Use the first worksheet of the new workbook
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

**小技巧：** 若需要多張投影片，可加入額外的工作表，之後分別儲存為獨立的 PPTX 檔案。

### 步驟 3：複製範圍並保留樞紐分析表

`CopyRange` 方法接受一個 `PasteOptions` 物件。將 `CopyPivotTables = true` 設為 true，表示 Aspose.Cells 會保留樞紐分析表的結構，而不僅是渲染後的值。

```csharp
// Copy the defined range, preserving the pivot table definition
destinationSheet.Cells.CopyRange(
    sourceRange,
    new PasteOptions { CopyPivotTables = true });
```

**運作原理：**  
當 `CopyPivotTables` 為 true 時，目的工作表會同時取得來源資料與樞紐快取。這意味著樞紐分析表仍保持完整功能，日後若來源資料變更，仍可在 PowerPoint 中重新整理。

### 步驟 4：將活頁簿儲存為 PowerPoint 檔案

最後，將活頁簿匯出為 PPTX 格式。`SaveFormat.Pptx` 旗標告訴 Aspose.Cells 將工作表寫入為 PowerPoint 投影片。

```csharp
// Save the destination workbook as a PowerPoint presentation
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);
```

**結果：**  
`CopyWithPivot.pptx` 於 Microsoft PowerPoint（或任何相容檢視器）開啟時，會顯示一張投影片，內容為已複製的範圍，且包含可在 PowerPoint 中互動的即時樞紐分析表。

## 完整可執行範例

以下程式碼為完整範例，您可直接貼到新的 Console 專案中執行。

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

**預期輸出：**  
執行程式後會在主控台印出「PowerPoint file created successfully.」，並產生名為 `CopyWithPivot.pptx` 的檔案。於 PowerPoint 開啟該檔案時，會看到單一投影片，複製的 Excel 範圍與來源工作表完全相同，且樞紐分析表仍可在 PowerPoint 內重新整理。

## 常見變化與邊緣案例

| 情境 | 需要變更的地方 |
|-----------|----------------|
| **多個樞紐分析表** | 為每個表格定義獨立的 `Range` 物件，並分別呼叫 `CopyRange`；若它們共用相同資料來源，也可直接複製整張工作表。 |
| **大型資料集** | 增大範圍（例如 `"A1:Z5000"`）。可考慮啟用 `PasteOptions.CompressData = true` 以縮減 PPTX 大小。 |
| **不同投影片版面** | 儲存為 PPTX 後，於 PowerPoint 中套用自訂版面或佈景主題；資料仍保持可編輯。 |
| **儲存至串流** | 需要透過 Web API 回傳 PPTX 時，可使用 `destinationWorkbook.Save(stream, SaveFormat.Pptx)`。 |
| **保留儲存格格式** | 設定 `PasteOptions.PasteType = PasteType.All` 以保留字型、顏色與框線等格式。 |

**專業提示：** 在呼叫 `Save` 前務必確認目的資料夾已存在。若資料夾不存在，`Save` 會拋出 `DirectoryNotFoundException`。

## 結論

現在您已掌握如何使用 Aspose.Cells 從 Excel 建立 PowerPoint、複製樞紐分析表，並將結果匯出為 PPTX 檔案。整個流程包括載入來源活頁簿、定義範圍、以 `CopyPivotTables` 複製，最後以 PPTX 儲存，完整且適合投入生產環境。

接下來，您可以探索 **將多個工作表匯出為 PPTX**，或學習 **在工作簿之間複製範圍**，以在產生投影片前先合併多個來源的資料。這兩個主題皆基於相同的 API，能結合起來自動化複雜的報表管線。

祝開發順利，玩得開心，讓您的試算表變身為精緻的簡報吧！


## 接下來該學什麼？

以下教學與本指南緊密相關，能在此基礎上延伸更多 API 功能與實作方式，並提供完整可執行的程式碼範例與逐步說明，協助您在專案中靈活運用。

- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [How to Create and Save Excel Files with Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}