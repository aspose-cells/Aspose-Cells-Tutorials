---
category: general
date: 2026-03-22
description: 學習如何將 Excel 匯出至 PowerPoint、設定列印範圍，以及將 Excel 儲存為可編輯圖表與 OLE 物件的 PPTX，只需幾個步驟。
draft: false
keywords:
- export excel to powerpoint
- set print area excel
- save excel as pptx
- editable charts PowerPoint
- OLE objects export
language: zh-hant
og_description: 快速將 Excel 匯出至 PowerPoint。本教學示範如何設定 Excel 的列印區域，並將 Excel 儲存為 PPTX，內含可編輯的圖表與
  OLE 物件。
og_title: 將 Excel 匯出至 PowerPoint – 完整 C# 指南
tags:
- Aspose.Cells
- C#
- Office Automation
title: 匯出 Excel 至 PowerPoint – 完整 C# 指南
url: /zh-hant/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 匯出 Excel 至 PowerPoint – 完整 C# 指南

需要 **export Excel to PowerPoint** 嗎？你來對地方了。無論你是在製作每週的銷售簡報，或是自動化報告流程，將 Excel 工作表轉換成 PowerPoint 投影片組合，都能為你節省大量的複製貼上時間。  

在本教學中，我們將示範一個實作範例，不僅能 **export excel to powerpoint**，還會教你如何 **set print area Excel** 與 **save excel as pptx**，讓產生的投影片保留圖表與 OLE 物件的完整可編輯性。完成後，你將擁有一個可直接執行的 C# 程式，產出外觀專業的 `.pptx` 檔案，且不需任何手動調整。

## 需要的條件

- **.NET 6+**（任何近期的 .NET 執行環境皆可；程式碼使用 C# 10 語法）
- **Aspose.Cells for .NET** – 提供匯出功能的函式庫。你可以從 NuGet 取得（`Install-Package Aspose.Cells`）。
- 一個包含至少一個圖表和/或 OLE 物件的 Excel 活頁簿（範例檔案 `ChartAndOle.xlsx` 於程式碼中使用）。
- 你喜愛的 IDE（Visual Studio、Rider 或 VS Code – 任選其一）。

就這樣。無需 COM interop，也不需要安裝 Office。  

> **為什麼要使用函式庫？**  
> 內建的 Office Interop 脆弱、需要在伺服器上安裝 Office，且常會產生點陣圖，而你真正需要的是向量且可編輯的圖形。Aspose.Cells 承擔繁重的工作，並確保所有內容在 PowerPoint 中皆可編輯。

## 步驟 1：載入 Excel 活頁簿  

首先，我們將來源檔案載入記憶體。`Workbook` 類別抽象化整個 Excel 檔案，讓我們能存取工作表、圖表與 OLE 物件。

```csharp
using Aspose.Cells;

try
{
    // Load the Excel file that contains the chart and OLE object.
    // Adjust the path to point to your own workbook.
    Workbook workbook = new Workbook(@"C:\MyProjects\ChartAndOle.xlsx");
}
catch (Exception ex)
{
    Console.WriteLine($"Failed to load workbook: {ex.Message}");
    return;
}
```

**為什麼這很重要：** 載入活頁簿是基礎。如果路徑錯誤或檔案損毀，後續流程將無法執行。`try…catch` 區塊會提供友善的錯誤訊息，而非直接當機。

## 步驟 2：在 Excel 中設定列印區域  

在匯出之前，你通常會想限制輸出範圍。這時 **set print area excel** 就派上用場。透過定義列印區域，你告訴 Aspose.Cells 哪些儲存格（以及相關物件）應該出現在投影片上。

```csharp
// Assuming we want to export only the range A1:H30 on the first worksheet.
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:H30";
```

> **專業提示：** 若有多個工作表，請為每個欲匯出的工作表重複設定 `PrintArea`。未設定列印區域會匯出整張工作表，可能導致 PowerPoint 檔案過大。

## 步驟 3：設定匯出選項 – 保持圖表與 OLE 可編輯  

Aspose.Cells 提供功能豐富的 `ImageOrPrintOptions` 物件。透過切換 `ExportChartObjects` 與 `ExportOleObjects`，我們可保留圖表的向量特性以及 OLE 物件（如嵌入的 Word 文件或 PDF）的即時可編輯性。

```csharp
ImageOrPrintOptions pptExportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,   // We want a PPTX, not a PNG or PDF.
    ExportChartObjects = true,      // Charts stay editable in PowerPoint.
    ExportOleObjects = true         // OLE objects remain live (you can double‑click to edit).
};
```

**底層發生了什麼？**  
當 `ExportChartObjects` 為 `true` 時，Aspose 會將圖表轉換為原生 PowerPoint 圖表形狀，保留系列、座標軸與格式。啟用 `ExportOleObjects` 後，嵌入的物件會以 OLE 框架插入，於 PowerPoint 中雙擊即可開啟原始應用程式（Word、Excel 等）進行編輯。

## 步驟 4：將工作表儲存為可編輯的 PowerPoint 檔案  

現在把所有步驟串起來。`Save` 方法會依照先前設定的選項寫入 `.pptx` 檔案。最終產出的是一套投影片，每張工作表會變成一張投影片（若列印區域跨多頁，則會產生多張投影片）。

```csharp
// Save the first worksheet as an editable PowerPoint presentation.
workbook.Save(@"C:\MyProjects\EditableChartOle.pptx", pptExportOptions);
Console.WriteLine("Export completed! Check EditableChartOle.pptx.");
```

### 預期結果

- **檔案位置：** `C:\MyProjects\EditableChartOle.pptx`
- **內容：**  
  - 一張投影片顯示範圍 `A1:H30`，與 Excel 中的呈現完全相同。  
  - 所有圖表皆為 PowerPoint 圖表物件——點擊柱狀圖即可編輯資料。  
  - OLE 物件（例如嵌入的 Word 文件）可直接在投影片上開啟並編輯。

若在 PowerPoint 中開啟此 PPTX，應會看到乾淨的投影片，且所有元件皆可完整編輯——不會出現點陣圖截圖。

## 邊緣情況與變化  

### 多個工作表 → 多張投影片  
若希望每個工作表各自成為一張投影片，只需遍歷 `workbook.Worksheets`，並使用針對特定工作表索引的 `SheetToImageOptions` 呼叫 `Save`。Aspose 會自動為每次迭代產生新投影片。

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    ImageOrPrintOptions opts = new ImageOrPrintOptions
    {
        SaveFormat = SaveFormat.Pptx,
        ExportChartObjects = true,
        ExportOleObjects = true,
        OnePagePerSheet = true   // Ensures each sheet starts on a new slide.
    };
    workbook.Save($"Sheet{i + 1}.pptx", opts);
}
```

### 大範圍與效能  
匯出巨大的列印區域（例如 `A1:Z1000`）可能會增加記憶體使用量。為減輕此問題，可考慮：

- 將範圍拆分為較小的區塊，分別匯出為獨立投影片。  
- 若遭遇 `OutOfMemoryException`，可使用 `WorkbookSettings` 提升 `MemorySetting`。

### 相容性考量  
產生的 PPTX 可在 PowerPoint 2016 及更新版本使用。舊版仍能開啟檔案，但可能失去部分進階圖表功能。若要廣泛發佈投影片，務必在目標 Office 版本上測試。

## 完整可執行範例（直接複製貼上）

```csharp
// ---------------------------------------------------------------
// Export Excel to PowerPoint – Complete C# Example
// ---------------------------------------------------------------

using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook.
            string excelPath = @"C:\MyProjects\ChartAndOle.xlsx";
            Workbook workbook;
            try
            {
                workbook = new Workbook(excelPath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error loading Excel file: {ex.Message}");
                return;
            }

            // 2️⃣ Set the print area (set print area excel).
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:H30";

            // 3️⃣ Configure export options – keep charts & OLE objects editable.
            ImageOrPrintOptions pptExportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportChartObjects = true,
                ExportOleObjects = true
            };

            // 4️⃣ Save as PPTX (save excel as pptx).
            string pptxPath = @"C:\MyProjects\EditableChartOle.pptx";
            try
            {
                workbook.Save(pptxPath, pptExportOptions);
                Console.WriteLine($"Success! PPTX created at: {pptxPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Failed to save PPTX: {ex.Message}");
            }
        }
    }
}
```

> **提示：** 請將硬編碼的路徑改為設定值或命令列參數，以提升工具彈性。

## 常見問答  

**Q: 我可以只匯出圖表而不包含周圍儲存格嗎？**  
A: 可以。僅使用 `ExportChartObjects`，並將列印區域設定為圖表的邊界範圍。圖表會置中顯示於投影片上。

**Q: 若我的活頁簿包含巨集怎麼辦？**  
A: Aspose.Cells 在匯出時會忽略 VBA 巨集。若需在 PowerPoint 中保有巨集功能，必須使用 PowerPoint VBA 或外掛自行重新實作。

**Q: 這在 Linux/macOS 上能運作嗎？**  
A: 完全可以。Aspose.Cells 是純 .NET 函式庫，只要安裝 .NET 執行環境，即可跨平台執行程式碼。

## 結論  

你剛剛學會了如何 **export Excel to PowerPoint**，同時精確 **set print area excel** 與 **save excel as pptx**，讓圖表與 OLE 物件保持完整可編輯。關鍵步驟包括載入活頁簿、定義列印區域、設定 `ImageOrPrintOptions`，最後儲存 PPTX。  

接下來你可以探索：  
- 將多個工作表匯出至同一套投影片。  
- 以程式方式加入自訂投影片標題或備註。  
- 將 PPTX 轉換為 PDF 以供發佈（使用 `SaveFormat.Pdf`）。  

執行程式碼、調整列印區域，便能看到 Excel 資料神奇地出現在 PowerPoint 中——不再需要手動複製貼上。若遇到問題，請參考 Aspose.Cells 文件或在下方留言。祝開發愉快！  

![Diagram showing export excel to powerpoint workflow](/images/export-excel-to-powerpoint.png "export excel to powerpoint workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}