---
category: general
date: 2026-08-04
description: 使用 Aspose.Cells 於 C# 匯出 Excel 圖表至 PowerPoint。遵循此逐步 Excel 到 PowerPoint
  轉換指南，並保持形狀可編輯。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel chart to powerpoint
- Aspose.Cells PPTX export
- editable shapes in PowerPoint
- Excel to PowerPoint conversion
- C# chart export
language: zh-hant
lastmod: 2026-08-04
og_description: 使用 C# 的 Aspose.Cells 匯出 Excel 圖表至 PowerPoint。了解如何建立可編輯的 PPTX、保留圖表資料，並自動化
  Excel 到 PowerPoint 的轉換。
og_image_alt: Screenshot of an Excel chart rendered as an editable PowerPoint slide
og_title: 使用 C# 匯出 Excel 圖表至 PowerPoint – 完整 Aspose.Cells 教學
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  headline: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  type: TechArticle
- description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  name: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  steps:
  - name: Expected output
    text: '| File name | Content on slide | |--------------------------|------------------------------------------|
      | `ShapesExport.pptx` | The chart from `Shapes.xlsx` rendered as an editable
      PowerPoint chart, with axis labels, legends, and data series intact. |'
  - name: Exporting multiple worksheets
    text: If you need a slide for each worksheet, loop through `workbook.Worksheets`
      and call `Save` with a unique file name for each iteration.
  - name: Controlling slide layout
    text: Aspose.Slides lets you add a custom slide layout after the export. Create
      a new presentation, import the generated slide, and then apply a master theme.
  - name: Handling charts with external data sources
    text: If a chart references a data range outside the defined print area, extend
      the `PrintArea` to include those cells. Otherwise the chart may lose data series
      during export.
  - name: Licensing considerations
    text: 'Aspose libraries work in evaluation mode with a watermark. To remove the
      watermark, set the license before any API call:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- PowerPoint
title: 使用 C# 匯出 Excel 圖表至 PowerPoint — 完整 Aspose.Cells 指南
url: /zh-hant/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 將 Excel 圖表匯出至 PowerPoint – 完整 Aspose.Cells 教學

如果您需要 **將 Excel 圖表匯出至 PowerPoint**，本教學將示範如何使用 Aspose.Cells 與 Aspose.Slides 於 C# 完成。您將取得一個可完整編輯的 PPTX，保留圖表資料與形狀，讓轉換後的檔案可直接進行後續設計工作。

將 Excel 圖表匯出至 PowerPoint 是在建置自動化報表管線、銷售簡報或訓練教材時的常見需求。在本指南中，您將學會執行 **Excel 轉 PowerPoint** 的精確步驟，確保所有圖表元素皆可編輯。無需手動複製貼上，且程式碼同時支援 .NET 6+ 以及傳統 .NET Framework。

## 前置條件

開始之前，請確保您已具備：

- 有效的 Aspose.Cells 授權（或免費評估金鑰）  
- 已將 Aspose.Slides for .NET 加入專案（此函式庫負責 PPTX 輸出）  
- 已安裝 .NET 6 SDK 或更新版本  
- 含有至少一個圖表的 Excel 活頁簿（本範例使用 `Shapes.xlsx`）  

您可以使用以下指令安裝 NuGet 套件：

```bash
dotnet add package Aspose.Cells
dotnet add package Aspose.Slides
```

## 步驟 1：載入 Excel 活頁簿

第一步是開啟包含欲匯出圖表的活頁簿。`Workbook` 類別代表整個 Excel 檔案。

```csharp
using Aspose.Cells;
using Aspose.Slides;   // required for PPTX output

// Load the Excel workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

**為什麼這很重要：** 載入活頁簿後即可存取其工作表、圖表與格式設定。Aspose.Cells 直接讀取檔案，無需安裝 Microsoft Office，讓解決方案保持輕量且適合伺服器環境。

## 步驟 2：選取工作表並定義列印區域

工作表可能包含多個圖表，但通常只會匯出特定區域。設定 `PrintArea` 可告訴 Aspose.Cells 哪些儲存格（含圖表）需要被渲染。

```csharp
// Choose the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Define the area that contains the chart and any supporting data
worksheet.PageSetup.PrintArea = "A1:G30";
```

**為什麼這很重要：** 透過限制匯出範圍，可避免產生不必要的空白投影片，並保持 PPTX 檔案尺寸較小。列印區域可依圖表實際範圍調整。

## 步驟 3：設定可編輯 PPTX 的匯出選項

Aspose.Cells 使用 `ImageOrPrintOptions` 類別來控制輸出格式與可編輯性。將 `ImageFormat` 設為 `ImageFormat.Pptx` 即可產生 PowerPoint 檔案，而 `ExportEditableShapes = true` 則會保留圖表物件為可編輯形狀。

```csharp
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Pptx,   // Target format
    ExportEditableShapes = true       // Keep shapes/textboxes editable
};

// Attach the options to the worksheet's print settings
worksheet.PageSetup.PrintOptions = exportOptions;
```

**為什麼這很重要：** `ExportEditableShapes` 旗標是實現 **PowerPoint 可編輯形狀** 結果的關鍵。若未啟用，圖表會被光柵化為影像，失去日後修改資料點或樣式的能力。

## 步驟 4：將工作表儲存為 PowerPoint 簡報

最後，對 `Workbook` 物件呼叫 `Save` 方法。`SaveFormat.Pptx` 列舉值告訴 Aspose.Cells 產生 PowerPoint 檔案。

```csharp
// Export the selected worksheet to a PPTX file
workbook.Save("YOUR_DIRECTORY/ShapesExport.pptx", SaveFormat.Pptx);
```

程式執行完畢後，於 PowerPoint 開啟 `ShapesExport.pptx`。您會看到一張投影片，內含原始 Excel 圖表的原生 PowerPoint 圖表物件。雙擊圖表即可編輯資料、變更顏色或加入動畫——就像直接在 PowerPoint 中建立的圖表一樣。

### 預期輸出

| 檔案名稱                | 投影片內容                                 |
|--------------------------|--------------------------------------------|
| `ShapesExport.pptx`      | 從 `Shapes.xlsx` 轉換而來的可編輯 PowerPoint 圖表，保留坐標軸標籤、圖例與資料系列。 |

## 完整可執行範例

以下提供完整程式碼，您可直接複製、貼上並執行。程式碼已包含所有必要的 `using` 陳述式、錯誤處理與註解。

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;   // Required for PPTX output

class ExcelToPowerPoint
{
    static void Main()
    {
        // Path to the source Excel file – adjust as needed
        const string excelPath = "YOUR_DIRECTORY/Shapes.xlsx";
        // Path for the generated PowerPoint file
        const string pptxPath = "YOUR_DIRECTORY/ShapesExport.pptx";

        try
        {
            // Load the workbook
            Workbook workbook = new Workbook(excelPath);

            // Use the first worksheet (you can change the index or name)
            Worksheet worksheet = workbook.Worksheets[0];

            // Define the area that contains the chart
            worksheet.PageSetup.PrintArea = "A1:G30";

            // Set export options for PPTX with editable shapes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Pptx,
                ExportEditableShapes = true
            };
            worksheet.PageSetup.PrintOptions = exportOptions;

            // Save as PPTX
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export successful. PPTX saved to: {pptxPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**各區塊說明**

| 區塊 | 目的 |
|-------|---------|
| `using` directives | 引入 Aspose.Cells 與 Aspose.Slides 命名空間。 |
| `Workbook workbook = new Workbook(excelPath);` | 在不需要安裝 Office 的情況下載入 Excel 檔案。 |
| `worksheet.PageSetup.PrintArea = "A1:G30";` | 限制匯出範圍為圖表所在的區域。 |
| `ImageOrPrintOptions` | 設定 PPTX 輸出並啟用 **Aspose.Cells PPTX 匯出** 的可編輯形狀。 |
| `workbook.Save(pptxPath, SaveFormat.Pptx);` | 將 PowerPoint 檔案寫入磁碟。 |
| `try / catch` | 提供基本的錯誤處理，處理檔案遺失或授權問題。 |

執行此程式後，會產生一張 PowerPoint 投影片，您可在 Microsoft PowerPoint、Google Slides（轉換後）或任何相容檢視器中開啟。

## 常見變形與例外情況

### 匯出多個工作表

若需要為每個工作表產生一張投影片，可遍歷 `workbook.Worksheets`，並為每次迭代使用唯一的檔名呼叫 `Save`。

```csharp
int index = 1;
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.PageSetup.PrintOptions = exportOptions;
    string fileName = $"Slide{index++}.pptx";
    workbook.Save(fileName, SaveFormat.Pptx);
}
```

### 控制投影片版面配置

Aspose.Slides 允許您在匯出後加入自訂投影片版面。建立新簡報、匯入產生的投影片，然後套用母片主題。

```csharp
using Aspose.Slides.Export;

// Load the PPTX created by Aspose.Cells
Presentation pres = new Presentation(pptxPath);

// Apply a built‑in layout (e.g., Title and Content)
pres.Slides[0].LayoutSlide = pres.LayoutSlides[(int)SlideLayoutType.TitleAndContent];

// Save the final presentation
pres.Save("FinalPresentation.pptx", SaveFormat.Pptx);
```

### 處理使用外部資料來源的圖表

若圖表參考的資料範圍位於列印區域之外，請擴大 `PrintArea` 以包含這些儲存格。否則匯出時圖表可能遺失資料系列。

### 授權考量

Aspose 函式庫在評估模式下會加上浮水印。若要移除浮水印，請在任何 API 呼叫之前設定授權：

```csharp
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

若使用 Aspose.Slides 的進階功能，也請同樣設定授權。

## 專業小技巧

- **重複使用匯出選項：** 建立單一 `ImageOrPrintOptions` 實例，並指派給每個工作表，以保持程式碼 DRY。  
- **批次處理：** 針對大規模報表，可將此匯出邏輯結合背景工作者或 Azure Function，按需產生 PPTX 檔案。  
- **效能調校：** 若只需要圖表影像（不需編輯），將 `ExportEditableShapes = false`。此設定可減少記憶體使用並加速轉換。  
- **測試建議：** 在 Windows 與 macOS 的 PowerPoint 版本上驗證產生的 PPTX，因為不同平台的渲染細節可能略有差異。

## 結論

您現在已掌握使用 C# **將 Excel 圖表匯出至 PowerPoint** 的完整端對端解決方案。教學涵蓋載入活頁簿、選取列印區域、設定 **Aspose.Cells PPTX 匯出** 以及 **PowerPoint 可編輯形狀**，最後將結果儲存為完整可編輯的 PPTX 檔案。

接下來，您可以探索更多 **Excel 轉 PowerPoint** 的情境，例如批次匯出、自訂投影片版面，或將此流程整合至 Web API。嘗試不同圖表類型、加入圖片，或將多個工作表合併成單一簡報，以符合您的業務需求。

準備好自動化您的報表工作流程了嗎？試著更換來源檔案、調整列印區域，並將程式碼整合至現有的 .NET 服務中。祝開發順利！

## 接下來您可以學習什麼？

以下教學與本指南緊密相關，能進一步深化您對 API 功能的掌握，並探索在專案中實作的其他方式。

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Export Excel Cells to Image Using Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}