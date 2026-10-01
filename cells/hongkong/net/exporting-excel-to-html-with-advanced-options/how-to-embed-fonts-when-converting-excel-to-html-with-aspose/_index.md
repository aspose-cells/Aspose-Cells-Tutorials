---
category: general
date: 2026-10-01
description: 學習如何在使用 Aspose.Cells 將 Excel 轉換為 HTML 時嵌入字型。只需幾個步驟，即可將 Excel 匯出為帶有嵌入字型的
  HTML。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- convert excel to html
- embed fonts in html
- how to export excel
- export excel as html
language: zh-hant
lastmod: 2026-10-01
og_description: 在匯出 Excel 檔案時，如何在 HTML 中嵌入字型。請跟隨本逐步指南，將 Excel 轉換為嵌入字型的 HTML。
og_image_alt: Screenshot of Aspose.Cells code embedding fonts in exported HTML
og_title: 如何從 Excel 嵌入字型至 HTML – Aspose.Cells 指南
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  headline: How to embed fonts when converting Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  name: How to embed fonts when converting Excel to HTML with Aspose.Cells
  steps:
  - name: 'Edge case: unsupported fonts'
    text: If the workbook uses a font that is not installed on the server, Aspose.Cells
      falls back to a default system font. To avoid this, install the required fonts
      on the server or embed them manually after export.
  - name: Converting multiple worksheets
    text: If you need to **convert Excel to HTML** for all worksheets, set `ExportActiveWorksheetOnly
      = false` (the default). Aspose.Cells will create a separate HTML file for each
      sheet.
  - name: Controlling CSS output
    text: 'You can reduce the HTML size by disabling inline CSS:'
  - name: Using a stream instead of a file
    text: 'When integrating into a web API, write the HTML to a `MemoryStream` and
      return it directly:'
  type: HowTo
tags:
- Aspose.Cells
- .NET
- Excel conversion
title: 如何在使用 Aspose.Cells 將 Excel 轉換為 HTML 時嵌入字型
url: /zh-hant/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-converting-excel-to-html-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在使用 Aspose.Cells 將 Excel 轉換為 HTML 時嵌入字型

在將 Excel 活頁簿轉換為 HTML 時嵌入字型，可確保在不同瀏覽器中保持原始外觀。若您需要在轉換過程中保留自訂字型，本指南將完整說明操作步驟。您還會了解如何將 Excel 匯出為 HTML，以及為何在 HTML 中嵌入字型對於一致的呈現至關重要。

本教學涵蓋您需要了解的全部內容：必備函式庫、程式碼設定以及產生的 HTML 檔案驗證。完成後，您只需幾行 C# 程式碼，即可將 Excel 匯出為帶有嵌入字型的 HTML。

## 您需要的環境

開始之前，請確保您已具備：

* **.NET 6.0 或更新版本** – 程式碼以 .NET 6 為目標，但任何支援 Aspose.Cells 的 .NET 版本皆可使用。
* **Aspose.Cells for .NET** – 從 Aspose 官方網站取得授權或使用免費評估版。
* **C# 開發環境**（Visual Studio、Rider 或 VS Code）– 任何能編譯 .NET 專案的 IDE。
* 一個使用自訂字型的 Excel 活頁簿（`Styled.xlsx`），您希望在 HTML 中保留這些字型。

## 步驟 1：在 .NET 專案中設定 Aspose.Cells

首先，將 Aspose.Cells NuGet 套件加入您的專案：

```bash
dotnet add package Aspose.Cells
```

接著在 C# 檔案的最上方加入命名空間：

```csharp
using Aspose.Cells;
```

加入套件後，即可使用 `Workbook`、`HtmlSaveOptions` 以及相關類別。

## 步驟 2：載入 Excel 活頁簿

載入活頁簿是 **如何匯出 Excel** 資料的第一步。`Workbook` 建構式會從磁碟讀取檔案：

```csharp
// Step 1: Load the Excel workbook
var workbook = new Workbook("YOUR_DIRECTORY/Styled.xlsx");
```

*為什麼這很重要：* Aspose.Cells 會解析活頁簿，包括儲存格樣式、公式與字型資訊。若找不到檔案會拋出例外，請確認路徑正確。

## 步驟 3：設定 HTML 儲存選項以嵌入字型

**在 html 中嵌入字型** 的核心是 `HtmlSaveOptions` 類別。將 `EmbedFonts` 設為 `true`，即可將活頁簿中使用的每種字型以 Base64 編碼的 `@font-face` 規則寫入 HTML 輸出。

```csharp
// Step 2: Set HTML save options to embed fonts in the output
var htmlOptions = new HtmlSaveOptions
{
    EmbedFonts = true,
    // Optional: keep the original worksheet name as the HTML file name
    ExportActiveWorksheetOnly = true
};
```

*為什麼這很重要：* 預設情況下 Aspose.Cells 只會引用外部字型檔，若客戶端機器沒有該字型就會顯示不一致。啟用 `EmbedFonts` 可保證無論檢視者安裝了什麼字型，HTML 都會與原始 Excel 表格外觀相同。

### 邊緣情況：不支援的字型

如果活頁簿使用的字型未在伺服器上安裝，Aspose.Cells 會回退至系統預設字型。為避免此情況，請先在伺服器上安裝所需字型，或在匯出後手動嵌入。

## 步驟 4：使用已設定的選項將活頁簿儲存為 HTML

現在可以寫入 HTML 檔案。`Save` 方法接受輸出路徑與 `HtmlSaveOptions` 實例：

```csharp
// Step 3: Save the workbook as an HTML file using the configured options
workbook.Save("YOUR_DIRECTORY/Styled.html", htmlOptions);
```

執行完畢後，`Styled.html` 內含試算表資料以及一段 `<style>` 區塊，裡面有每種自訂字型的 Base64 編碼 `@font-face` 定義。

## 步驟 5：驗證嵌入的字型

在瀏覽器中開啟 `Styled.html`，檢查 `<head>` 區段，您應該會看到類似以下內容：

```html
<style>
@font-face {
    font-family: 'Calibri';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
}
...
</style>
```

若表格渲染時字型正確顯示，表示嵌入成功。若發現缺字或字形異常，請再次確認執行轉換的機器已安裝來源字型檔。

## 常見變化與其他選項

### 轉換多個工作表

若需 **將 Excel 轉換為 HTML** 時包含所有工作表，將 `ExportActiveWorksheetOnly = false`（預設值）即可。Aspose.Cells 會為每個工作表產生獨立的 HTML 檔案。

```csharp
htmlOptions.ExportActiveWorksheetOnly = false;
workbook.Save("YOUR_DIRECTORY/AllSheets.html", htmlOptions);
```

### 控制 CSS 輸出

您可以透過停用內嵌 CSS 來減少 HTML 大小：

```csharp
htmlOptions.ExportCssSeparately = true; // Generates a .css file alongside the .html
```

### 使用串流而非檔案

在 Web API 中整合時，可將 HTML 寫入 `MemoryStream`，直接回傳：

```csharp
using var stream = new MemoryStream();
workbook.Save(stream, htmlOptions);
stream.Position = 0; // Reset for reading
// Return stream as a file download in ASP.NET Core
```

## 小技巧：授權產品以移除評估水印

若使用評估版，產生的 HTML 可能會包含水印註解。請在載入活頁簿前先套用 Aspose.Cells 授權，以產生乾淨的輸出：

```csharp
var license = new License();
license.SetLicense("Aspose.Total.lic");
```

## 完整範例程式

以下是一個完整、可執行的範例，示範 **如何嵌入字型**、**將 Excel 轉換為 HTML**，以及 **匯出 Excel 為 HTML** 的完整流程：

```csharp
using System;
using Aspose.Cells;

class ExcelToHtmlWithEmbeddedFonts
{
    static void Main()
    {
        // Apply license if you have one (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Total.lic");

        // 1️⃣ Load the Excel workbook
        var workbookPath = @"YOUR_DIRECTORY/Styled.xlsx";
        var workbook = new Workbook(workbookPath);

        // 2️⃣ Configure HTML save options to embed fonts
        var htmlOptions = new HtmlSaveOptions
        {
            EmbedFonts = true,
            ExportActiveWorksheetOnly = true, // Export only the first sheet
            ExportCssSeparately = false        // Keep CSS inline for a single file
        };

        // 3️⃣ Save as HTML
        var htmlPath = @"YOUR_DIRECTORY/Styled.html";
        workbook.Save(htmlPath, htmlOptions);

        Console.WriteLine($"Excel workbook '{workbookPath}' has been exported to HTML with embedded fonts at '{htmlPath}'.");
    }
}
```

**預期結果：** 執行程式後，`Styled.html` 會出現在 `YOUR_DIRECTORY`。在任何現代瀏覽器開啟該檔案，都會看到與原始 Excel 檔案相同的字型，即使該機器未安裝這些字型。

## 結論

現在您已掌握 **在使用 Aspose.Cells 將 Excel 轉換為 HTML 時嵌入字型** 的方法，並了解從載入活頁簿到驗證嵌入字型的完整流程。此做法可確保 Excel 檔案的視覺忠實度在產生的 HTML 中得以保留，適用於網頁報表、電子報或任何需要 **將 Excel 匯出為 HTML** 且保留自訂排版的情境。

接下來，您可以探索以下相關主題，如 **將 Excel 匯出為 PDF**、**使用自訂 CSS 美化 HTML 輸出**，或 **批次處理多本活頁簿**。這些皆以相同的 `HtmlSaveOptions` 為基礎，只需稍作調整即可應用。

祝開發順利！

## 接下來您可以學習什麼？

以下教學與本指南的技術緊密相關，提供完整的程式碼範例與逐步說明，協助您掌握更多 API 功能或在專案中嘗試其他實作方式。

- [How to Export Excel to HTML – Step‑by‑Step Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-step-by-step-guide/)
- [How to Embed Fonts in HTML – Complete C# Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/)
- [How to embed fonts when converting Excel to PDF – Step‑by‑Step Guide](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}