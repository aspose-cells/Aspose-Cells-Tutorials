---
category: general
date: 2026-02-26
description: 將工作簿匯出為嵌入字型的 PDF，並在 C# 中將圖表匯出至 PowerPoint。學習如何複製樞紐分析表工作表，並將工作簿另存為 PPTX。
draft: false
keywords:
- export workbook to pdf
- export charts to powerpoint
- copy pivot table worksheet
- embed fonts pdf export
- save workbook as pptx
language: zh-hant
og_description: 將工作簿匯出為嵌入字型的 PDF，並在 C# 中將圖表匯出至 PowerPoint。請依照一步一步的指南複製樞紐分析表並另存為 PPTX。
og_title: 匯出工作簿至 PDF – 完整 C# 指南
tags:
- Aspose.Cells
- Aspose.Slides
- C#
- Reporting
title: 匯出工作簿為 PDF – 完整 C# 指南
url: /zh-hant/net/conversion-to-pdf/export-workbook-to-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 匯出工作簿為 PDF – 完整 C# 指南

匯出工作簿為 PDF 是在需要與可能未安裝 Excel 的利害關係人分享報告時的常見需求。在本教學中，我們還會示範如何 **匯出圖表至 PowerPoint**、複製 **樞紐分析表工作表**，以及嵌入字型，使 PDF 看起來與螢幕上的設計完全相同。  

有沒有想過為什麼有些 PDF 會失去原始版面，或為什麼 PowerPoint 投影片會缺少圖形？答案通常是匯出過程中缺少了某些選項。閱讀完本指南後，你將擁有一個可重複使用的 C# 方法，解決所有這些痛點——不再需要手動複製貼上或調整匯出設定。

## 你將學會

- 如何建立工作簿、加入 Smart Marker 表達式，並處理它們。  
- 如何 **複製樞紐分析表工作表** 而不破壞資料來源。  
- 如何 **匯出圖表、圖形與文字方塊** 至 PowerPoint 簡報，同時保持可編輯。  
- 如何在 PDF 匯出時 **嵌入標準字型**，以確保在任何機器上都有一致的呈現。  
- 如何使用 `save workbook as pptx` 方法 **將工作簿儲存為 PPTX**。  

以上全部皆可搭配最新的 Aspose.Cells 與 Aspose.Slides .NET 函式庫（撰寫時的版本為 23.11）使用。無需外部工具、無需後處理腳本——僅使用純 C#。

> **專業提示：** 若你的專案已在使用 Aspose，直接套用程式碼片段即可；否則，請先加入 NuGet 套件 `Aspose.Cells` 與 `Aspose.Slides`。

## 前置條件

- .NET 6.0 或更新版本（此程式碼亦可在 .NET Framework 4.7.2 上執行）。  
- Visual Studio 2022（或任何你偏好的 IDE）。  
- 透過 NuGet 安裝 Aspose.Cells .NET 與 Aspose.Slides .NET。  
- 具備 C# 基礎以及 Excel 概念（如 Smart Markers 與 PivotTables）的熟悉度。  

---

![匯出工作簿為 PDF 圖示](export-workbook-to-pdf.png "匯出工作簿為 PDF 工作流程，顯示 PDF 與 PPTX 輸出")

## 匯出工作簿為 PDF – 步驟實作

以下為完整、可直接執行的範例。它會建立工作簿、注入 Smart Marker 表達式、處理它們、複製樞紐分析表範圍，最後同時儲存為 PDF 與 PowerPoint 檔案。

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides.Export;

namespace ReportExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Build the workbook and add Smart Markers
            // -------------------------------------------------
            var reportWorkbook = new Workbook();
            Worksheet dataSheet = reportWorkbook.Worksheets[0];

            // Header with a variable department name
            dataSheet.Cells["A1"].PutValue("Report for ${$dept=Department}");

            // Conditional text based on department
            dataSheet.Cells["A2"].PutValue("${if $dept == \"Sales\"}Sales Summary${else}Other Summary${/if}");

            // Table header for orders – this will be repeated for each order
            dataSheet.Cells["A5:D5"].PutValue("${Orders.Product}|${Orders.Quantity}|${Orders.Price}");

            // -------------------------------------------------
            // Step 2: Process Smart Markers and name the detail sheet
            // -------------------------------------------------
            reportWorkbook.SmartMarkerProcessor.Options.DetailSheetNewName = "Orders_${$dept}";
            reportWorkbook.SmartMarkerProcessor.Process();

            // -------------------------------------------------
            // Step 3: Copy the range that contains the pivot table
            // -------------------------------------------------
            // Assume the pivot table lives in A1:G30 on the original sheet
            Range sourceRange = dataSheet.Cells.CreateRange("A1", "G30");
            Worksheet copySheet = reportWorkbook.Worksheets.Add("Copy");
            sourceRange.Copy(copySheet.Cells["A1"]);   // Pivot table is duplicated intact

            // -------------------------------------------------
            // Step 4: Export to PowerPoint (keep charts, shapes, text boxes)
            // -------------------------------------------------
            var pptOptions = new PresentationOptions
            {
                ExportCharts = true,
                ExportShapes = true,
                ExportTextBoxes = true
            };
            string pptPath = @"C:\Temp\FinalPresentation.pptx";
            reportWorkbook.Save(pptPath, SaveFormat.Pptx, pptOptions);

            // -------------------------------------------------
            // Step 5: Export to PDF and embed standard fonts
            // -------------------------------------------------
            var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
            string pdfPath = @"C:\Temp\FinalReport.pdf";
            reportWorkbook.Save(pdfPath, pdfOptions);

            Console.WriteLine("Export completed:");
            Console.WriteLine($" • PDF saved to {pdfPath}");
            Console.WriteLine($" • PowerPoint saved to {pptPath}");
        }
    }
}
```

### 為什麼這樣可行

1. **Smart Marker processing** 讓你能從任何資料來源（JSON、DataTables 等）填充工作簿，無需撰寫迴圈。  
2. **DetailSheetNewName** 會為每個部門建立獨立的工作表，提供乾淨的部門分頁。  
3. **Copying the range** (`sourceRange.Copy`) 會複製樞紐分析表 *包括* 其快取，讓複製的工作表行為與原始工作表完全相同。  
4. **PresentationOptions** 搭配 `ExportCharts`、`ExportShapes` 與 `ExportTextBoxes`，告訴 Aspose 將這些物件以原生 PowerPoint 元素呈現，保留可編輯性。  
5. **PdfSaveOptions.EmbedStandardFonts** 確保 PDF 在未安裝原始字型的機器上仍呈現相同外觀。  

最終會產生兩個檔案——`FinalReport.pdf` 與 `FinalPresentation.pptx`——可透過電子郵件傳送、存檔，或在任何檢視器中顯示，且不會失真。

## 匯出圖表至 PowerPoint（將工作簿儲存為 PPTX）

如果你的報告包含圖表，你可能希望它們在 PowerPoint 中可編輯。`PresentationOptions` 類別是關鍵。以下是一段專注於圖表匯出部分的程式碼片段：

```csharp
// Assuming reportWorkbook already contains charts
var pptExportOptions = new PresentationOptions
{
    ExportCharts = true,      // Convert Excel charts to PowerPoint chart objects
    ExportShapes = false,    // Skip shapes if you don’t need them
    ExportTextBoxes = true   // Keep any text boxes editable
};

string pptFile = @"C:\Temp\ChartsOnly.pptx";
reportWorkbook.Save(pptFile, SaveFormat.Pptx, pptExportOptions);
```

**底層發生了什麼？** Aspose 會將每個 Excel 圖表轉換為原生 PowerPoint 圖表，保留系列、座標軸標題與格式。這遠比將圖表匯出為靜態影像更好，因為觀眾日後可以調整資料點。

## 複製樞紐分析表工作表而不遺失資料

樞紐分析表常是匯出時最棘手的部分，因為它們依賴隱藏的快取。簡單的 `Copy` 方法之所以可行，是因為 Aspose 同時複製可見範圍 **以及** 底層的快取物件。

```csharp
// Copy the whole sheet (including pivot table) to a new workbook
Workbook clone = new Workbook();
reportWorkbook.Worksheets[0].CopyTo(clone.Worksheets[0]);
clone.Save(@"C:\Temp\PivotCopy.xlsx", SaveFormat.Xlsx);
```

> **注意：** 若你只需要在同一工作簿內的新工作表上放置樞紐分析表，先前的 `sourceRange.Copy` 方法較為輕量，且避免建立整個新工作簿。

## 為 PDF 匯出嵌入字型 – 為何重要

當在未安裝原始字型的機器上開啟 PDF 時，文字可能會移位、換行改變，甚至字元消失。將 `EmbedStandardFonts = true` 設為 true，會指示 Aspose 將最常見的字型（如 Arial、Times New Roman 等）直接嵌入 PDF 串流中。

若使用自訂字型，請改為 `PdfSaveOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedAll`。以下為範例：

```csharp
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    FontEmbeddingMode = FontEmbeddingMode.EmbedAll   // For custom fonts
};
reportWorkbook.Save(@"C:\Temp\CustomFontReport.pdf", pdfOpts);
```

現在每位收件人都會看到與你設計完全相同的版面——不會有任何意外。

## 完整範例回顧

將所有步驟整合起來，完整程式（如前所示）會執行以下操作：

1. **Creates** 建立一個含有 Smart Marker 佔位符的工作簿。  
2. **Processes** 處理這些標記，產生以部門名稱命名的明細工作表。  
3. **Copies** 複製包含樞紐分析表的範圍至新工作表，保留其功能。  
4. **Exports** 將工作簿匯出為 PowerPoint，保持圖表、圖形與文字方塊可編輯。  
5. **Exports** 將相同的工作簿匯出為 PDF，並嵌入標準字型以確保可靠的呈現。  

執行程式，開啟產生的檔案，你會看到：

- **PDF**：清晰的表格、嵌入的字型，且視覺風格與 Excel 原始檔相同。  
- **PowerPoint**：可編輯的圖表，你可以在 PowerPoint 中右鍵點擊 → *Edit Data*，以及仍可完全操作的圖形。  

---

## 常見問題 (FAQ)

**Q: 這能在 .NET Core 上運作嗎？**  
是的——Aspose.Cells 與 Aspose.Slides 為跨平台。只要目標設定為 .NET 6 或更新版本，相同程式碼即可在 Windows、Linux 或 macOS 上執行。

**Q: 如果只想匯出部分工作表該怎麼辦？**  
使用 `Workbook.Save` 搭配可指定 `SheetNames` 的 `SaveOptions`。例如：`new PresentationOptions { SheetNames = new[] { "Copy" } }`。

**Q: 可以加密 PDF 嗎？**  
當然可以。在呼叫 `Save` 之前，使用 `PdfSaveOptions.EncryptionDetails` 設定密碼。

**Q: 我的樞紐分析表使用外部資料來源——複製會不會斷開連結？**  
複製操作會包含快取，而非外部連線。樞紐分析表仍可離線使用，但不會對原始來源重新整理。若需要即時重新整理，請將來源資料與工作簿一起匯出。

## 往後步驟與相關主題

- **Dynamic Data Sources** – 了解如何將 JSON 或 DataTable 塞入 Smart Markers，以進行即時報告。  
- **Advanced PDF Styling** – 探索 `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}