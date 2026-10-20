---
category: general
date: 2026-10-20
description: 學習如何在 Aspose.Cells 中使用 wrapcols、在 HTML 中嵌入字型，並使用完整的 C# 範例將 Excel 儲存為
  HTML。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- embed fonts in html
- save excel as html
- convert workbook to html
- use wrapcols function
language: zh-hant
lastmod: 2026-10-20
og_description: 如何在 Aspose.Cells 中使用 wrapcols、在 HTML 中嵌入字型，並將工作簿轉換為 HTML，提供開發人員清晰的
  C# 操作步驟說明。
og_image_alt: Screenshot of an Excel workbook saved as HTML with embedded fonts using
  Aspose.Cells
og_title: 如何在將 Excel 匯出為 HTML 時使用 wrapcols 及嵌入字型
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to use wrapcols in Aspose.Cells, embed fonts in HTML, and
    save Excel as HTML with a complete C# example.
  headline: How to use wrapcols and embed fonts saving Excel to HTML
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel to HTML
- Smart Markers
title: 如何在將 Excel 另存為 HTML 時使用 wrapcols 並嵌入字型
url: /zh-hant/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 wrapcols 以及在將 Excel 儲存為 HTML 時嵌入字型

如果您需要在 Aspose.Cells 公式中 **how to use wrapcols**，本指南將向您展示具體步驟。您還將學習如何 **在 HTML 中嵌入字型** 以及 **將 Excel 儲存為 HTML**，以確保輸出在各瀏覽器上保持一致。

本教學涵蓋三個實用情境：使用 `WRAPCOLS` 函式、匯出帶有嵌入字型的活頁簿，以及使用 Smart Markers 產生主從報表。完成後，您將擁有一個可執行的 C# 程式，示範所有這些功能。

## 前置條件

在開始之前，請確保您已具備：

* .NET 6.0（或更新版本）已安裝。
* 已將 Aspose.Cells for .NET 加入專案（`dotnet add package Aspose.Cells`）。
* 具備 C# 與 Excel 公式的基本知識。

不需要額外的第三方函式庫；Aspose.Cells 內部已處理 HTML 轉換與字型嵌入。

## 步驟 1：示範公式中的 **how to use wrapcols** 函式

`WRAPCOLS` 函式將一維範圍拆分為二維陣列，先填滿欄。當您需要為報表或圖表重新排列資料時，此功能非常有用。

```csharp
using Aspose.Cells;
using System;

class WrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Populate a vertical range A1:A3
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // Apply WRAPCOLS(A1:A3, 2) – this creates a 2‑column array {1,2}
        sheet.Cells["B1"].Formula = "=WRAPCOLS(A1:A3, 2)";

        // Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // Output the result to verify the function works
        Console.WriteLine("Result of WRAPCOLS: " + sheet.Cells["B1"].Value);
        // Expected output: Result of WRAPCOLS: 1
    }
}
```

**為什麼這樣有效：**`WRAPCOLS` 需要兩個參數——來源範圍與欄數。函式按欄位填充陣列，會捨棄多餘的值（範例中的 `3`）。結果會顯示在目標範圍左上角的儲存格（`B1`），若需要完整陣列，可手動擴展範圍。

> **小技巧：** 設定公式後，呼叫 `workbook.CalculateFormula()` 以確保在讀取儲存格值前結果已更新。

## 步驟 2：**將活頁簿轉換為 HTML** 並 **在 HTML 中嵌入字型**

將 Excel 檔案匯出為 HTML 時，字型常會被瀏覽器的預設字型取代，導致版面配置錯亂。Aspose.Cells 允許您直接將活頁簿中使用的字型嵌入至 HTML 檔案中。

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for HtmlSaveOptions
using System;

class HtmlExportDemo
{
    static void Main()
    {
        // Re‑use the workbook from the previous step
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue("Hello");
        sheet.Cells["A2"].PutValue("World");

        // Configure HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Embedding fonts ensures the output looks the same on any device
            EmbedFonts = true,
            // Optional: specify a folder for supporting files (images, CSS)
            ExportEmbeddedImages = true
        };

        // Save the workbook as an HTML file with embedded fonts
        string outputPath = @"C:\Temp\WorkbookWithFonts.html";
        workbook.Save(outputPath, htmlOptions);

        Console.WriteLine($"Workbook saved to HTML with embedded fonts at: {outputPath}");
    }
}
```

**為什麼嵌入字型很重要：** 當 `EmbedFonts` 為 `true` 時，Aspose.Cells 會將每個使用的 TrueType/OpenType 字型轉換為 Base64 編碼的 `@font-face` 規則，嵌入於產生的 HTML 中。這樣客戶端機器就不必安裝相同字型，確保像素級的完美呈現。

> **特殊情況：** 若來源活頁簿引用的字型未在伺服器上安裝，Aspose.Cells 會退回使用預設字型並發出警告。請確保所需字型已備妥。

## 接下來該學什麼？

以下教學涵蓋與本指南技術密切相關的主題，並以此為基礎。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索其他實作方式。

- [如何在 C# 中使用 WRAPCOLS – 建立帶有換列函式的 Excel 活頁簿](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [如何在 HTML 中嵌入字型 – 使用 C# 將 Excel 轉換為 HTML](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/)
- [如何使用 Aspose.Cells for .NET 將 Excel 檔案轉換為 HTML：隱藏重疊內容](/cells/english/net/workbook-operations/excel-to-html-hide-overlaid-content-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}