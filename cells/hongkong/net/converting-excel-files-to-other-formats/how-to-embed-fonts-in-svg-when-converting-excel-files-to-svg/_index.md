---
category: general
date: 2026-09-15
description: 學習如何在 SVG 中嵌入字型，並將 Excel 圖表匯出至 PowerPoint，內容涵蓋將 XLSX 轉換為 SVG 以及將 XLSX
  轉換為 PPTX，並提供完整程式碼範例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in SVG
- export excel chart to powerpoint
- convert xlsx to svg
- convert xlsx to pptx
- save workbook as svg
language: zh-hant
lastmod: 2026-09-15
og_description: 在 SVG 中嵌入字型，並使用逐步 C# 程式碼將 Excel 圖表匯出至 PowerPoint。快速且可靠地將 XLSX 轉換為
  SVG 及 PPTX。
og_image_alt: Screenshot showing an Excel chart exported to PowerPoint with embedded
  fonts in the resulting SVG file
og_title: 在 SVG 中嵌入字型並將 Excel 圖表匯出至 PowerPoint – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  headline: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  type: TechArticle
- description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  name: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  steps:
  - name: Open `EditableChart.pptx` in PowerPoint.
    text: Open `EditableChart.pptx` in PowerPoint.
  - name: Locate the slide containing the chart.
    text: Locate the slide containing the chart.
  - name: Choose **Chart Tools → Design → Edit Data**.
    text: Choose **Chart Tools → Design → Edit Data**.
  - name: Confirm that the Excel‑style data grid appears and that you can change values.
    text: Confirm that the Excel‑style data grid appears and that you can change values.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: 將 Excel 檔案轉換為 SVG 及 PowerPoint 時，如何在 SVG 中嵌入字型
url: /zh-hant/net/converting-excel-files-to-other-formats/how-to-embed-fonts-in-svg-when-converting-excel-files-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在將 Excel 檔案轉換為 SVG 及 PowerPoint 時於 SVG 中嵌入字型  

如果您需要在將 Excel 活頁簿轉換為 SVG 時 **在 SVG 中嵌入字型**，本指南會精確說明操作步驟。您還將學習如何 **將 Excel 圖表匯出至 PowerPoint**，以及如何 **將 XLSX 轉換為 SVG** 與 **將 XLSX 轉換為 PPTX**（含可編輯的圖表）。  

以程式方式處理 Excel 資料時，通常需要在不同檔案格式之間搬移相同的視覺內容。手動在 PowerPoint 重新製作圖表或在 SVG 中重新套用字型既容易出錯又耗時。完成本教學後，您將擁有一段可重複使用的 C# 程式碼片段，能夠：

* 將活頁簿儲存為含嵌入字型與字型變體選擇器的 SVG 檔案。  
* 將相同的活頁簿匯出為 PPTX 檔案，且圖表保持可編輯。  

唯一的前置條件是近期版本的 **Aspose.Cells for .NET**（2024‑x 或更新）以及 .NET 開發環境，例如 Visual Studio 2022。

---

## 您需要的環境  

* .NET 6.0 或更新版本（程式碼亦相容於 .NET Framework 4.8）。  
* Aspose.Cells for .NET NuGet 套件（`Install-Package Aspose.Cells`）。  
* 包含至少一個圖表的 Excel 檔案（`input.xlsx`）。  
* 具備寫入輸出目錄的權限。  

---

## 在將 XLSX 轉換為 SVG 時於 SVG 中嵌入字型  

嵌入字型可確保 SVG 在任何裝置上正確呈現，即使目標系統未安裝原始字型。`SvgSaveOptions` 類別提供兩個旗標，使此功能得以實現：`EmbedFonts` 與 `FontVariationSelectors`。

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// OPTIONAL: Use WRAPCOLS to reshape data before export (demonstrates a formula)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)"; // 2 columns per wrap
sheet.Calculate(); // Force calculation so the formula result appears

// Configure SVG options to embed fonts
SvgSaveOptions svgOptions = new SvgSaveOptions
{
    EmbedFonts = true,                // embed fonts in the SVG
    FontVariationSelectors = true    // include variation selectors for better Unicode handling
};

// Save the workbook as an SVG file
string svgPath = @"YOUR_DIRECTORY\WithFonts.svg";
workbook.Save(svgPath, svgOptions);
```

**為什麼這樣有效：**  
* `EmbedFonts = true` 會將字型檔案複製至 SVG 的 `<defs>` 區段，消除外部相依性。  
* `FontVariationSelectors = true` 會為支援 OpenType 功能的字型加入必要的選擇器，保留如連字等字形變體。  

**預期結果：** 在任何現代瀏覽器開啟 `WithFonts.svg`；圖表或儲存格內的文字會以 Excel 中使用的精確字型顯示，即使該機器未安裝此字型。

---

## 將 Excel 圖表匯出至 PowerPoint 並保留可編輯圖表  

當您需要將圖表嵌入 PowerPoint 投影片中，同時讓接收者能編輯圖表資料時，Aspose.Cells 的 `PptxSaveOptions` 提供 `ExportEditableChart` 旗標。

```csharp
// Configure PPTX options to keep charts editable after export
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableChart = true   // allow chart editing in PowerPoint
};

// Save the same workbook as a PPTX file
string pptxPath = @"YOUR_DIRECTORY\EditableChart.pptx";
workbook.Save(pptxPath, pptxOptions);
```

**為什麼這很重要：**  
將 `ExportEditableChart` 設為 `true` 會將圖表儲存為 Office Open XML 圖表物件，而非靜態影像。於 PowerPoint 開啟 `EditableChart.pptx` 時，您可右鍵點擊圖表 → **Edit Data**，如同原生 PowerPoint 圖表般修改系列資料。

**驗證步驟：**  

1. 在 PowerPoint 中開啟 `EditableChart.pptx`。  
2. 找到包含圖表的投影片。  
3. 選取 **Chart Tools → Design → Edit Data**。  
4. 確認出現 Excel 風格的資料格，且您可以變更數值。

---

## 將 XLSX 轉換為 SVG – 完整工作流程回顧  

以下提供一個精簡版，結合載入、可選的資料操作與儲存為 SVG。當您僅需要 SVG 輸出時可使用此版本。

```csharp
public void ConvertXlsxToSvg(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Example: apply a formula to demonstrate cell calculations
    Worksheet ws = wb.Worksheets[0];
    ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
    ws.Calculate();

    SvgSaveOptions opts = new SvgSaveOptions
    {
        EmbedFonts = true,
        FontVariationSelectors = true
    };

    wb.Save(outputPath, opts);
}
```

以如下方式呼叫此方法：

```csharp
ConvertXlsxToSvg(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.svg");
```

**邊緣案例提示：** 若活頁簿使用的自訂字型未在伺服器上安裝，請在呼叫 `Save` 前手動嵌入。可使用 `FontInfoCollection` 透過 `CustomFonts` 屬性將字型檔案加入 `SvgSaveOptions`（此功能在較新版的 Aspose.Cells 中提供）。

---

## 將 XLSX 轉換為 PPTX – 保留圖表可編輯性  

以下輔助方法示範 **將 XLSX 轉換為 PPTX** 的流程，同時確保圖表保持可編輯。

```csharp
public void ConvertXlsxToPptx(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Ensure any chart you want to keep editable is on the first worksheet
    // (Aspose.Cells exports only the first worksheet by default for PPTX)
    PptxSaveOptions opts = new PptxSaveOptions
    {
        ExportEditableChart = true
    };

    wb.Save(outputPath, opts);
}
```

使用方式：

```csharp
ConvertXlsxToPptx(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.pptx");
```

**常見問題：** *如果我的活頁簿有多個工作表且每個都有圖表怎麼辦？*  
**回答：** Aspose.Cells 預設只匯出第一個工作表。若要包含其他工作表，需遍歷 `workbook.Worksheets`，將每個圖表複製到新投影片，並使用 Aspose.Slides 的 `Presentation` 物件分別儲存每張投影片。此進階情境超出「將活頁簿儲存為 SVG」與「將 Excel 圖表匯出至 PowerPoint」的基本流程，但核心旗標仍相同。

---

## 實務技巧與常見陷阱  

* **效能：** 嵌入字型會增加 SVG 檔案大小。若檔案大小是考量因素，請將 `EmbedFonts = false`，改用網頁安全字型。  
* **字型授權：** 確保您有權嵌入所使用的字型；某些商業字型限制嵌入。  
* **圖表相容性：** 可編輯圖表會以 `chart.xml` 部分儲存在 PPTX 內。非常複雜的圖表（例如 3D 或組合圖）在 PowerPoint 編輯時可能會失去部分樣式。請測試您最常使用的圖表類型。  
* **版本不匹配：** `ExportEditableChart` 旗標需要 Aspose.Cells 20.10 或更新版本。使用較舊版本會默默退回為點陣圖。  
* **執行緒安全性：** Workbook 物件不是執行緒安全的。於 Web 服務情境下，請為每個請求建立新的 `Workbook` 實例。  

---

## 完整端對端範例  

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class ExcelExportDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputFile = @"YOUR_DIRECTORY\input.xlsx";
        string svgFile   = @"YOUR_DIRECTORY\WithFonts.svg";
        string pptxFile  = @"YOUR_DIRECTORY\EditableChart.pptx";

        // 1. Load workbook
        Workbook workbook = new Workbook(inputFile);

        // 2. Optional: reshape data using WRAPCOLS
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
        sheet.Calculate();

        // 3. Save as SVG with embedded fonts
        SvgSaveOptions svgOpts = new SvgSaveOptions
        {
            EmbedFonts = true,
            FontVariationSelectors = true
        };
        workbook.Save(svgFile, svgOpts);
        Console.WriteLine($"SVG saved with embedded fonts to: {svgFile}");

        // 4. Save as PPTX with editable chart
        PptxSaveOptions pptxOpts = new PptxSaveOptions
        {
            ExportEditableChart = true
        };
        workbook.Save(pptxFile, pptxOpts);
        Console.WriteLine($"PPTX saved with editable chart to: {pptxFile}");
    }
}
```

執行此程式會產生兩個檔案：

* **WithFonts.svg** – 產生的 SVG 與 Excel 檢視完全相同，已包含字型。  
* **EditableChart.pptx** – 產生的 PowerPoint 簡報，圖表可直接編輯。

---

## 結論  

現在您已了解在 **將 XLSX 轉換為 SVG 時嵌入字型** 的方法，以及在 **將 Excel 圖表匯出至 PowerPoint** 並保持圖表可編輯的技巧。同樣的程式碼亦示範了以最小工作量 **將活頁簿儲存為 SVG** 與 **將 XLSX 轉換為 PPTX** 的簡潔做法。  

接下來您可以探索以下進階主題：

* 以程式方式加入自訂字型（`svgOptions.CustomFonts`）。  
* 在背景服務中批次處理多個活頁簿。  
* 使用 Aspose.Slides 建立結合多個 Excel 圖表的多投影片 PPTX 檔案。  

請自行嘗試各項設定，將程式碼片段套用至您的專案，便能享受可靠的 Excel 轉 SVG/PPTX 轉換，免除手動後處理。祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索其他實作方式。

- [如何使用 Aspose.Cells for .NET（逐步指南）將 Excel 圖表轉換為 SVG](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [將 Excel 圖表轉換為 SVG Aspose Cells .NET](/cells/german/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [將 Excel 圖表轉換為 SVG Aspose Cells .NET](/cells/french/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}