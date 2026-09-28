---
category: general
date: 2026-09-27
description: 在 Excel 中設定列印範圍，並學習如何匯出所選儲存格的 PNG 圖片。本指南亦說明如何將範圍另存為圖像以及將圖片加入工作表。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- how to export png
- save range as image
- add picture to worksheet
- export selected cells image
language: zh-hant
lastmod: 2026-09-27
og_description: 在 Excel 中設定列印區域，並使用 Aspose.Cells 匯出 PNG。請依照此步驟指南將範圍儲存為圖像並將圖片加入工作表。
og_image_alt: Screenshot showing set print area excel and exported PNG file
og_title: 設定 Excel 列印範圍 – 在 C# 中匯出 PNG
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Set print area in Excel and learn how to export PNG images of selected
    cells. This guide also covers saving range as image and adding picture to worksheet.
  headline: How to set print area in Excel and export PNG
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: 如何在 Excel 設定列印區域並匯出 PNG
url: /zh-hant/net/rendering-and-export/how-to-set-print-area-in-excel-and-export-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Excel 中設定列印區域並匯出 PNG

如果您需要在建立圖像之前 **set print area excel**，本指南將精確說明如何操作。您還將學習如何從特定範圍 **how to export png** 檔案、**save range as image**，以及 **add picture to worksheet**，全部在單一且可重複的工作流程中完成。

以程式方式操作 Excel 通常意味著您只想將某些儲存格（例如樞紐分析表或圖表）轉換為圖像。先定義列印區域可確保匯出的 PNG 正好包含您預期的儲存格，既不多也不少。本教學將逐步說明從載入活頁簿到儲存最終 PNG 檔案的每個步驟，並解釋每個設定的原因。

## 前置條件

* 已安裝 .NET 6.0 或更新版本  
* Visual Studio 2022（或任何 C# IDE）  
* **Aspose.Cells for .NET** NuGet 套件 (`Install-Package Aspose.Cells`)  
* 位於已知目錄的 Excel 檔案 (`input.xlsx`)  

這些需求可確保程式碼在無需額外設定的情況下執行。

## 步驟 1：載入您要處理的活頁簿

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Load the workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

`Workbook` 類別代表整個 Excel 檔案。先載入它即可取得工作表、儲存格以及頁面設定等功能。

## 步驟 2：為目標範圍 **Set print area excel**

```csharp
// Define the range you want to capture
string printArea = "A1:G20";

// Apply the range as the print area on the first worksheet
workbook.Worksheets[0].PageSetup.PrintArea = printArea;
```

設定 **print area** 可告訴 Excel（以及 Aspose.Cells）哪些儲存格屬於可列印的頁面。之後將工作表匯出為圖像時，僅會呈現此區域，對於取得乾淨的 **export selected cells image** 至關重要。

## 步驟 3：設定影像匯出選項 – **how to export png**

```csharp
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG ensures lossless quality
    OnePagePerSheet = true           // Export the defined print area as a single page
};
```

`ImageOrPrintOptions` 控制輸出格式。選擇 `ImageFormat.Png` 後，可確保產生高解析度、透明背景的影像，適用於網頁與桌面環境。

## 步驟 4：從已定義的範圍建立圖片並 **add picture to worksheet**

```csharp
// Create a picture object from the selected range
Picture picture = workbook.Worksheets[0].Pictures.Add(
    0,                                     // top‑left row index where the picture will be placed
    0,                                     // top‑left column index where the picture will be placed
    workbook.Worksheets[0].Cells.CreateRange(printArea));
```

`Pictures.Add` 方法會在工作表中插入新圖片。傳入步驟 2 中建立的範圍，即可 **save range as image** 直接放置於工作表上，若之後需要在活頁簿其他位置引用此圖片非常方便。

## 步驟 5：**Save the picture as an image file** – 完成 **export selected cells image** 工作流程

```csharp
// Save the picture to disk as a PNG file
picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);
```

呼叫 `Save` 會根據步驟 3 中定義的選項將圖片寫入檔案系統。產生的 `selected_range.png` 正好包含 **set print area excel** 指令所定義的儲存格。

## 完整、可執行的範例

將所有步驟組合起來，即可得到一個可直接放入任何主控台應用程式的精簡程式碼：

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

class ExportExcelRangeAsPng
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Set print area excel
        string printArea = "A1:G20";
        workbook.Worksheets[0].PageSetup.PrintArea = printArea;

        // 3️⃣ Configure how to export png
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            OnePagePerSheet = true
        };

        // 4️⃣ Add picture to worksheet (save range as image)
        Picture picture = workbook.Worksheets[0].Pictures.Add(
            0,
            0,
            workbook.Worksheets[0].Cells.CreateRange(printArea));

        // 5️⃣ Export selected cells image
        picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);

        Console.WriteLine("PNG exported successfully to YOUR_DIRECTORY\\selected_range.png");
    }
}
```

### 預期輸出

執行程式會輸出：

```
PNG exported successfully to YOUR_DIRECTORY\selected_range.png
```

您會在目錄中看到 `selected_range.png` 檔案，僅顯示 `input.xlsx` 中 A1 至 G20 的儲存格。

## 常見問題與避免方法

| 問題 | 發生原因 | 解決方式 |
|-------|----------------|-----|
| 匯出的影像包含整張工作表 | 未定義列印區域 | 確保在建立圖片前 **set print area excel** |
| PNG 影像模糊 | 預設 DPI 較低 | 將 `imageOptions.DpiX` 與 `imageOptions.DpiY` 設為較高的值（例如 300） |
| 找不到檔案錯誤 | 目錄路徑錯誤 | 使用 `Path.Combine` 或再次確認資料夾是否存在 |
| 圖片位置偏移 | 列/行索引不正確 | `Pictures.Add` 的前兩個參數代表圖片放置的左上角儲存格；請保持為 `0,0` 以獲得乾淨的匯出 |

## 專業提示：一次執行匯出多個範圍

如果您需要為多個區域 **export selected cells image**，可在迴圈中重複步驟 2‑5，並在每次迭代時更改 `printArea`。請務必為每張圖片指定唯一的檔名，否則後續的儲存會覆寫先前的檔案。

## 結論

現在您已了解如何使用 Aspose.Cells **set print area excel**、設定 **how to export png**、**save range as image**，以及 **add picture to worksheet**。此端對端解決方案只需幾行 C# 程式碼，即可將任意儲存格區塊轉換為高品質 PNG。

接下來您可能想探索：

* 為匯出的 PNG 加上邊框或浮水印（搜尋 *add picture to worksheet* 並加入樣式）
* 直接匯出為 PDF 以產生可列印報告（*export selected cells image* → PDF 工作流程）
* 在批次作業中自動化處理多個活頁簿

歡迎嘗試不同的範圍、DPI 設定或影像格式，以符合您的專案需求。祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並在此基礎上延伸。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索替代實作方式。

- [Set Print Area in Excel and Export to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Export Excel Print Area to HTML with Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-print-area-html-aspose-cells-java/)
- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}