---
category: general
date: 2026-09-21
description: 使用 Aspose.Cells 將 Excel 匯出至 PowerPoint，圖表保持可編輯。請依照此步驟指南，將工作表轉換為 PPTX，同時保留圖表的可編輯性。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- worksheet to powerpoint
- export excel chart pptx
- editable charts pptx
language: zh-hant
lastmod: 2026-09-21
og_description: 使用 Aspose.Cells 將 Excel 匯出至 PowerPoint，圖表可編輯。了解如何將工作表轉換為 PPTX，同時保留圖表的完整編輯功能。
og_image_alt: Screenshot of a PowerPoint slide showing an editable Excel chart after
  export
og_title: 匯出 Excel 至 PowerPoint，圖表可編輯 – C# 教學
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  headline: Export Excel to PowerPoint with editable charts in C#
  type: TechArticle
- description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  name: Export Excel to PowerPoint with editable charts in C#
  steps:
  - name: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
    text: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
  - name: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
    text: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
  - name: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
    text: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
  - name: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
    text: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel‑to‑PowerPoint
- PPTX export
title: 在 C# 中將 Excel 匯出至 PowerPoint，並保留可編輯的圖表
url: /zh-hant/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-editable-charts-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中將 Excel 匯出至 PowerPoint 並保留可編輯圖表

在需要於簡報中重複使用試算表視覺效果時，將 Excel 匯出至 PowerPoint 並保留可編輯圖表是一項常見需求。本指南將示範如何使用 Aspose.Cells for .NET **export Excel to PowerPoint**，同時保留圖表的可編輯性。

您將學習如何：

* 載入包含圖表和文字方塊的現有活頁簿。  
* 設定 PPTX 匯出選項，使圖表和形狀保持可編輯。  
* 將特定工作表轉換為可在 Microsoft PowerPoint 中開啟並編輯的 PowerPoint 檔案。

本教學假設您具備基本的 C# 知識，且使用較新版本的 .NET（≥ .NET 6）。不需要事先了解 Aspose.Cells。

---

## Export Excel to PowerPoint – 概觀

**export Excel to PowerPoint** 的核心概念是將每個工作表視為可渲染成 PPTX 投影片的影像來源。透過切換 `ExportChartAsEditableText` 與 `ExportShapeAsEditableText` 旗標，Aspose.Cells 會將底層圖表資料寫入為 PowerPoint 繪圖物件，而非平面點陣圖。如此產生的投影片即可完全編輯——就如同直接在 PowerPoint 中建立的圖表一般。

> **為何使用可編輯圖表？**  
> 可編輯圖表讓簡報者無需返回原始 Excel 檔，即可調整資料、顏色或標籤，加快最後時刻的變更，並保持簡報流程順暢。

---

## 將工作表轉換為 PowerPoint（worksheet to PowerPoint）

以下是一個完整且可執行的範例，示範 **worksheet to PowerPoint** 轉換。

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the chart and textbox
            // Replace YOUR_DIRECTORY with the actual folder path on your machine.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Configure PPTX export options to keep charts and shapes editable
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,               // Target format: PPTX
                ExportChartAsEditableText = true,           // Enable editable charts
                ExportShapeAsEditableText = true            // Enable editable shapes/textboxes
            };

            // Step 3: Export the first worksheet (index 0) to a PowerPoint file
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";
            workbook.Worksheets[0].ConvertToImage(exportOptions, outputPath);

            Console.WriteLine($"Worksheet successfully exported to {outputPath}");
        }
    }
}
```

### 每個步驟說明

| 步驟 | 程式碼功能 | 為何對 **export excel chart pptx** 重要 |
|------|-------------------|----------------------------------------------|
| 1️⃣   | 將 `input.xlsx` 載入 `Aspose.Cells.Workbook` 物件。 | 此活頁簿提供對欲匯出圖表的存取。 |
| 2️⃣   | 將 `ExportType` 設為 `Pptx`，並啟用 `ExportChartAsEditableText` 與 `ExportShapeAsEditableText`。 | 這些旗標是 **editable charts pptx** 的關鍵——它們告訴函式庫將圖表幾何寫入為 PowerPoint 繪圖物件，而非點陣圖。 |
| 3️⃣   | 對第一個工作表呼叫 `ConvertToImage`，產生 `Worksheet.pptx`。 | 此方法執行 **export excel to powerpoint** 操作，並寫入可直接在 PowerPoint 開啟的 PPTX 檔案。 |

> **專業提示：** 如果需要匯出*多個*工作表，可遍歷 `workbook.Worksheets`，對每個工作表呼叫 `ConvertToImage`，並可自行命名輸出檔案，例如 `Sheet1.pptx`、`Sheet2.pptx` 等。

---

## 在 PPTX 中啟用可編輯圖表（export excel chart pptx）

當 `ExportChartAsEditableText` 設為 `true` 時，Aspose.Cells 會將每個圖表寫入 PPTX XML 中的 `<a:graphic>` 元素集合。PowerPoint 隨即將這些元素視為原生圖表物件，您可雙擊以開啟圖表編輯器。

**常見陷阱**

* **缺少 Aspose.Cells 授權** – 若未授權，函式庫會在輸出檔案加上浮水印。請在程式一開始即註冊授權 (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`)。  
* **不支援的圖表類型** – 雖然大多數 2‑D 圖表（柱狀、折線、圓餅）皆可完全編輯，但某些複雜的 3‑D 或組合圖表可能會退回為影像。若需完整編輯性，請測試您的特定圖表類型。  
* **大型工作表** – 匯出非常大的工作表可能會佔用大量記憶體。可考慮在 `ImageOrPrintOptions` 中使用 `ExportMaxRows` 或 `ExportMaxColumns` 以限制轉換範圍。

---

## 保持圖表可編輯的技巧（editable charts pptx）

1. **保留圖表資料範圍** – 確保圖表的資料來源位於您正匯出的同一工作表。跨工作表的參照會在 PPTX 中轉換為靜態值。  
2. **使用最新的 Aspose.Cells 版本** – 新版會提升對更多圖表功能的支援，並修正與 PPTX 匯出相關的邊緣案例錯誤。  
3. **驗證輸出** – 轉換後，於 PowerPoint 開啟產生的 PPTX，確認您能編輯圖表標題、系列及座標軸標籤。若有任何元素顯示為影像，請再次確認已啟用 `ExportChartAsEditableText` 且圖表類型受支援。  
4. **批次處理** – 針對自動化情境（例如從多個 Excel 報表產生投影片套件），將轉換邏輯封裝於接受 `Workbook`、`int worksheetIndex` 與 `string outputPath` 的方法中。此方式可將 **export excel to powerpoint** 工作流程獨立，便於重複使用。

---

## 完整範例回顧

將所有內容整合起來，以下是您可以直接複製貼上至新 .NET 主控台專案的最小程式：

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Register license (optional but removes evaluation watermark)
            // var license = new License();
            // license.SetLicense("Aspose.Cells.lic");

            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";

            Workbook workbook = new Workbook(inputPath);

            ImageOrPrintOptions options = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,
                ExportChartAsEditableText = true,
                ExportShapeAsEditableText = true
            };

            workbook.Worksheets[0].ConvertToImage(options, outputPath);

            Console.WriteLine($"Export complete: {outputPath}");
        }
    }
}
```

**預期結果**

* 在 `YOUR_DIRECTORY` 中會產生名為 `Worksheet.pptx` 的檔案。  
* 在 Microsoft PowerPoint 開啟該檔案時，會顯示包含原始圖表與所有文字方塊的投影片。  
* 雙擊圖表會開啟 PowerPoint 的圖表編輯器，讓您可變更系列數值、顏色或座標軸標題——驗證 **editable charts pptx** 功能如預期運作。

---

## 結論

您現在擁有一套完整的 **export Excel to PowerPoint** 解決方案，能保持圖表可編輯。透過以 `ExportChartAsEditableText` 與 `ExportShapeAsEditableText` 設定 `ImageOrPrintOptions`，轉換過程會產生原生 PPTX 檔案，使圖表的行為如同直接在 PowerPoint 中建立的一樣。  

接下來您可以：

* 將程式碼擴充以處理多個工作表（每個工作表皆執行 **worksheet to PowerPoint**）。  
* 將匯出與其他 Aspose.Cells 功能結合，例如加入投影片標題或插入影像。  
* 探索相關主題，例如使用自訂主題的 **export Excel chart PPTX**，或自動化整個投影片套件產生流程。

歡迎嘗試不同的圖表類型、加入資料標籤，或將此工作流程整合至更大型的報表系統。祝開發順利！

## 接下來應該學什麼？

以下教學涵蓋與本指南技術密切相關的主題。每個資源皆提供完整的可執行程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索其他實作方式。

- [如何使用 Aspose.Cells for .NET 將 Excel 轉換為 PowerPoint：完整指南](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}