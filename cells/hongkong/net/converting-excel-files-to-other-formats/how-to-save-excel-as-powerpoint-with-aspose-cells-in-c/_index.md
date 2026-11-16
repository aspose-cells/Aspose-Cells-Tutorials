---
category: general
date: 2026-11-16
description: 學習如何將 Excel 儲存為 PowerPoint，並以程式方式將 Excel 轉換為 PowerPoint。本分步指南亦涵蓋將 Excel
  匯出為 PPTX 以及將活頁簿儲存為 PPTX。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- export excel to pptx
- how to convert excel slide
- save workbook as pptx
language: zh-hant
lastmod: 2026-11-16
og_description: 使用 Aspose.Cells 將 Excel 另存為 PowerPoint。跟隨本指南即可將 Excel 轉換為 PowerPoint、匯出
  Excel 為 PPTX，並在數分鐘內將工作簿另存為 PPTX。
og_image_alt: Screenshot showing the result of saving Excel as PowerPoint with editable
  shapes
og_title: 將 Excel 另存為 PowerPoint – 完整 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to save Excel as PowerPoint and convert Excel to PowerPoint
    programmatically. This step‑by‑step guide also covers export Excel to PPTX and
    saving a workbook as PPTX.
  headline: How to save Excel as PowerPoint with Aspose.Cells in C#
  type: TechArticle
tags:
- Excel
- PowerPoint
- Aspose.Cells
- C#
- Export
title: 如何在 C# 中使用 Aspose.Cells 將 Excel 另存為 PowerPoint
url: /zh-hant/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-with-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.Cells 在 C# 中將 Excel 儲存為 PowerPoint

如果您需要以程式方式 **save Excel as PowerPoint**，本教學提供完整、可直接執行的解決方案。無論您是建立報表引擎或自動化投影片產生器，以下步驟都能讓您僅用幾行程式碼將 Excel 工作表轉換為可編輯的 PPTX 投影片。

您將學會如何 **convert Excel to PowerPoint**、將工作表匯出為 PPTX 檔案，並保持文字方塊與圖形可編輯——全部在 .NET 環境中完成。

## 前置條件

* .NET 6.0 或更新版本（此程式碼亦支援 .NET Framework 4.7.2+）
* 有效的 Aspose.Cells 授權（免費試用版可供評估）
* Visual Studio 2022（或任何 C# IDE）
* 包含您想匯出的資料與圖形之 Excel 活頁簿

## 第一步：安裝 Aspose.Cells

將 Aspose.Cells NuGet 套件加入您的專案：

```bash
dotnet add package Aspose.Cells
```

> **專業提示：** 使用 `-v` 參數以指定特定版本，例如 `Aspose.Cells.24.5`。

## 第二步：載入要匯出的活頁簿

在 **save Excel as PowerPoint** 工作流程中的第一個操作是載入來源活頁簿。

```csharp
using Aspose.Cells;
using System;

// Load the workbook that contains the shapes
Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");
```

*為什麼這很重要：* 載入活頁簿可讓您存取其工作表、頁面設定，以及將會變成可編輯 PowerPoint 圖形的繪圖物件。

## 第三步：設定可編輯 PPTX 投影片的匯出選項

若要在 **convert Excel to PowerPoint** 時保留可編輯性，必須在 `ImageOrPrintOptions` 上設定幾個屬性。

```csharp
// Prepare export options to generate an editable PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // Export format
    ExportEditableText = true,        // Keep text boxes editable
    ExportEditableShapes = true       // Keep shapes editable
};
```

*說明：*  
* `SaveFormat = SaveFormat.Pptx` 告訴 Aspose.Cells 產生 PowerPoint 檔案。  
* `ExportEditableText` 與 `ExportEditableShapes` 確保產生的投影片行為如同原生 PowerPoint 投影片——您可以點擊文字方塊或圖形，直接在 PowerPoint 中編輯。

## 第四步：定義匯出區域並調整為單一投影片

當您 **export Excel to PPTX** 時，通常希望特定範圍顯示於投影片上。設定列印區域與調整選項可確保輸出為整潔的單張投影片。

```csharp
// Define the area of the first worksheet to export
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G30";

// Fit the exported content to a single slide
sheet.PageSetup.FitToPagesTall = 1;
sheet.PageSetup.FitToPagesWide = 1;
```

*為什麼這很重要：* `PrintArea` 限制匯出範圍為 A1 至 G30，而 `FitToPagesTall` 與 `FitToPagesWide` 會將所有內容壓縮至單一投影片，避免產生不必要的額外頁面。

## 第五步：將工作表儲存為可編輯的 PPTX 檔案

現在您終於可以 **save workbook as PPTX**，完成 **save Excel as PowerPoint** 的流程。

```csharp
// Save the worksheet as an editable PPTX file
workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
Console.WriteLine("Export completed: EditableShapes.pptx");
```

執行程式後，於 Microsoft PowerPoint 開啟 `EditableShapes.pptx`。您會看到一張與所選 Excel 範圍相同的投影片，且所有文字方塊與圖形皆可完整編輯。

### 預期輸出

* 一個名為 `EditableShapes.pptx`，位於 `C:\Output\` 的檔案。
* 一張包含 A1:G30 範圍的 PowerPoint 投影片。
* 文字方塊、圖表與圖形，您可直接在 PowerPoint 中雙擊編輯。

## 完整原始碼（可直接複製）

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the shapes
            Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");

            // Step 2: Prepare export options to generate an editable PPTX slide
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportEditableText = true,   // keep text boxes editable
                ExportEditableShapes = true  // keep shapes editable
            };

            // Step 3: Define the area of the first worksheet to export
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";

            // Step 4: Fit the exported content to a single slide
            sheet.PageSetup.FitToPagesTall = 1;
            sheet.PageSetup.FitToPagesWide = 1;

            // Step 5: Save the worksheet as an editable PPTX file
            workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
            Console.WriteLine("Export completed: EditableShapes.pptx");
        }
    }
}
```

## 常見問題與特殊情況處理

| Question | Answer |
|----------|--------|
| **如果我有多個工作表怎麼辦？** | 迭代 `workbook.Worksheets`，對每張工作表重複第 3‑5 步，並變更輸出檔名（例如 `Sheet1.pptx`、`Sheet2.pptx`）。 |
| **能否將整個活頁簿匯出為單一 PowerPoint 簡報？** | 可以。於 `ImageOrPrintOptions` 設定 `ExportAllSheets = true`。每張工作表會成為獨立的投影片。 |
| **我的圖形顯示為圖片，無法編輯。** | 確認 `ExportEditableShapes = true`，且使用 Aspose.Cells 24.5 以上版本（較早版本不支援此功能）。 |
| **產生的 PPTX 檔案太大。** | 縮小列印區域，或透過 `exportOptions.ImageResolution` 降低影像解析度。 |
| **正式環境需要授權嗎？** | 付費授權會移除評估水印並解鎖完整效能。免費試用版可供測試使用。 |

## 生產環境穩健程式碼的提示

* **驗證檔案路徑** 在呼叫 `Workbook` 或 `Save` 前，以避免 `FileNotFoundException`。  
* **將匯出程式碼包在 try/catch** 區塊中，以處理授權錯誤（`Aspose.Cells.LicenseException`）。  
* **釋放活頁簿**（`workbook.Dispose()`）使用完畢後，以釋放非受控資源。  
* **使用非同步 I/O**（`FileStream` 搭配 `await`）若在 Web 服務中匯出大量大型工作表。  

## 後續步驟

既然您已了解如何 **save Excel as PowerPoint**，接下來可以探索相關主題：

* **使用自訂投影片版面匯出 Excel 為 PPTX** – 調整 `SlideSize` 並加入母片投影片。  
* **將 Excel 投影片轉為 PDF** – 使用 `SaveFormat.Pdf` 產生可列印版本。  
* **批次轉換資料夾中的活頁簿** – 結合上述迴圈與 `Directory.GetFiles`。  

嘗試不同的列印區域、縮放選項與 PowerPoint 主題，以符合貴公司的品牌形象。

---

*祝程式開發愉快！若本指南協助您 **convert Excel to PowerPoint**，歡迎與同事分享，或在 Aspose.Cells GitHub 倉庫開立 issue 以取得進一步協助。*

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並以此為基礎延伸。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索替代實作方式。

- [如何使用 C# 與 Aspose.Cells 將 Excel 儲存為 PowerPoint](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/)
- [如何從 Excel 儲存 PPTX – 完整的 Excel 工作表匯出 PowerPoint 指南](/cells/english/java/integration-interoperability/how-to-save-pptx-from-excel-complete-guide-to-export-excel-s/)
- [將 Excel 轉換為 PowerPoint – 完整逐步指南](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-full-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}