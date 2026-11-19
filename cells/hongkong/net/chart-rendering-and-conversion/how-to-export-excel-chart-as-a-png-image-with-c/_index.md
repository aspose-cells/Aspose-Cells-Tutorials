---
category: general
date: 2026-11-19
description: 如何使用 Aspose.Cells 將 Excel 圖表匯出為 PNG 圖像。只需幾個步驟，即可學會儲存 Excel 圖表圖像並設定圖像格式為
  PNG。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel chart
- save excel chart image
- set image format png
- save excel picture file
language: zh-hant
lastmod: 2026-11-19
og_description: 如何使用 Aspose.Cells 將 Excel 圖表匯出為 PNG 圖像。請跟隨本步驟指南，輕鬆將 Excel 圖表儲存為 PNG
  格式的圖像。
og_image_alt: How to export Excel chart as a PNG image
og_title: 如何將 Excel 圖表匯出為 PNG 圖像 – 快速 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to export Excel chart as a PNG image using Aspose.Cells. Learn
    to save Excel chart image and set image format PNG in just a few steps.
  headline: How to export Excel chart as a PNG image with C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Chart export
title: 如何使用 C# 將 Excel 圖表匯出為 PNG 圖像
url: /zh-hant/net/chart-rendering-and-conversion/how-to-export-excel-chart-as-a-png-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 C# 將 Excel 圖表匯出為 PNG 圖像

如果您需要 **how to export Excel chart** 成為可攜式圖像，本指南提供完整、可直接執行的解決方案。使用 Aspose.Cells，您只需三行程式碼即可 **save Excel chart image** 為 PNG 格式，教學同時說明如何 **set image format png** 以及安全 **save Excel picture file**。

閱讀完本文後，您將得到一個可執行的程式，載入活頁簿、渲染第一個圖表，並將 `pivot.png` 檔寫入磁碟。無需額外工具、無需手動複製貼上——只要乾淨的 C# 程式碼，隨時可放入任何 .NET 專案。

## 前置條件

在開始之前，請確保您已具備：

* .NET 6.0 SDK 或更新版本（此程式碼亦相容 .NET Framework 4.6+）
* Visual Studio 2022 或任何 C# 編輯器
* Aspose.Cells for .NET 授權（或臨時評估金鑰）
* 一個包含至少一個圖表於第一個工作表的 Excel 檔 (`pivot.xlsx`)

以上項目即為唯一的外部相依性；本教學不需要在機器上安裝 Office。

## 第一步：安裝 Aspose.Cells

在專案資料夾的終端機中執行：

```bash
dotnet add package Aspose.Cells
```

此套件會加入 `Aspose.Cells` 命名空間，提供 `Workbook`、`ImageOrPrintOptions` 等類別，以 **save Excel chart image**。

## 第二步：建立最小化的主控台程式

建立新的主控台應用程式（`dotnet new console -n ExportChartDemo`），並將自動產生的 `Program.cs` 替換為以下程式碼。此程式示範 **how to export Excel chart**，並包含說明每個決策的註解。

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for ImageOrPrintOptions
using System.Drawing.Imaging;  // Provides ImageFormat enum

namespace ExportChartDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook that contains the pivot chart
            // -----------------------------------------------------------------
            // Replace the path with the actual location of your Excel file.
            string workbookPath = @"YOUR_DIRECTORY\pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -----------------------------------------------------------------
            // 2️⃣ Set up image export options (PNG format)
            // -----------------------------------------------------------------
            // This is where we **set image format png** for the exported picture.
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: control the resolution (DPI) of the output image.
                // Higher DPI yields larger files but sharper charts.
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 3️⃣ Render the first picture (the chart) on the first worksheet
            // -----------------------------------------------------------------
            // Aspose.Cells stores charts as Picture objects inside the worksheet.
            // The index [0] refers to the first chart; adjust if you have multiple.
            Worksheet sheet = workbook.Worksheets[0];
            if (sheet.Pictures.Count == 0)
            {
                Console.WriteLine("No pictures found on the first worksheet.");
                return;
            }

            // Render the picture to a PNG file.
            string outputPath = @"YOUR_DIRECTORY\pivot.png";
            sheet.Pictures[0].RenderToImage(imageOptions, outputPath);

            Console.WriteLine($"Chart exported successfully to: {outputPath}");
        }
    }
}
```

### 為何每個部分都很重要

* **Loading the workbook** – `Workbook` 會在不需要安裝 Microsoft Excel 的情況下解析 `.xlsx` 檔案。
* **ImageOrPrintOptions** – 此物件控制輸出格式。設定 `ImageFormat = ImageFormat.Png` **sets image format png**，此格式無損且廣受支援。
* **RenderToImage** – `RenderToImage` 方法將圖表（`Picture` 物件）轉換為圖像檔。此方法同時自動處理縮放、DPI 與透明度。
* **Error handling** – `sheet.Pictures.Count == 0` 的檢查可避免在工作表沒有圖表時拋出執行時例外，這是使用者指向錯誤工作表時常見的邊緣情況。

## 第三步：執行程式並驗證結果

1. 建置專案：`dotnet build`。
2. 執行程式：`dotnet run --project ExportChartDemo`。

若一切設定正確，您會看到：

```
Chart exported successfully to: YOUR_DIRECTORY\pivot.png
```

使用任何圖像檢視器開啟 `pivot.png`。您應該會看到與 Excel 圖表完全相同的視覺呈現，證明您已成功 **saved Excel picture file**。

### 預期輸出

以下為匯出 PNG 可能的樣子（實際圖表取決於您的來源檔案）。

![匯出 Excel 圖表已儲存為 PNG 圖像](images/exported-chart.png){: .center alt="如何將 Excel 圖表匯出為 PNG 圖像"}

## 第四步：進階選項 – 匯出多個圖表

如果活頁簿中包含多個圖表，您可以遍歷 `Pictures` 集合：

```csharp
for (int i = 0; i < sheet.Pictures.Count; i++)
{
    string chartPath = $@"YOUR_DIRECTORY\chart_{i + 1}.png";
    sheet.Pictures[i].RenderToImage(imageOptions, chartPath);
    Console.WriteLine($"Chart {i + 1} saved to {chartPath}");
}
```

此模式讓您能為工作表上的每個圖表 **save Excel chart image**，相當適合報表管線使用。

## 常見陷阱與避免方式

| 症狀 | 可能原因 | 解決方式 |
|------|----------|----------|
| `ArgumentOutOfRangeException` 於 `Pictures[0]` | 工作表沒有圖表，或圖表位於其他工作表。 | 確認工作表索引 (`Worksheets[0]`) 並確保圖表存在。必要時使用 `Worksheets["SheetName"]`。 |
| 匯出圖像模糊 | DPI 設定過低（預設 96）。 | 在 `ImageOrPrintOptions` 中提高 `HorizontalResolution` 與 `VerticalResolution`。 |
| PNG 檔案為空或損毀 | 缺少授權導致評估限制。 | 在載入活頁簿前套用有效的 Aspose.Cells 授權 (`License license = new License(); license.SetLicense("Aspose.Total.lic");`)。 |
| 檔案路徑錯誤 (`FileNotFoundException`) | `YOUR_DIRECTORY` 佔位符不正確。 | 使用絕對路徑或 `Path.Combine(Environment.CurrentDirectory, "pivot.xlsx")`。 |

解決上述問題即可確保順利 **save excel picture file**。

## 專業技巧：直接匯出至記憶體串流

有時您需要將圖像保留在記憶體中（例如上傳至 Web API），而非寫入磁碟：

```csharp
using (var ms = new MemoryStream())
{
    sheet.Pictures[0].RenderToImage(imageOptions, ms);
    // ms now contains the PNG bytes – you can send them over HTTP, store in DB, etc.
}
```

相同的 **set image format png** 邏輯仍然適用，只是將檔案路徑改為串流。

## 結論

現在您已掌握使用 Aspose.Cells for .NET **how to export Excel chart** 為 PNG 檔案的完整流程。本文涵蓋：

* 安裝函式庫
* 載入活頁簿
* **Setting image format png**
* **Saving Excel chart image** 至磁碟
* 處理多圖表與常見錯誤

有了這個基礎，您可以將圖表匯出整合至自動化報表、Web 服務或桌面工具。接下來，可探索如 **save excel picture file** 為 JPEG (`ImageFormat.Jpeg`) 或將圖表轉為 PDF 以產生可列印報告等相關主題。

祝開發順利！

## 接下來您可以學習什麼？

以下教學與本指南緊密相關，能在此基礎上延伸技巧。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索替代實作方式。

- [Convert Excel Pie Chart to Image Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)
- [Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/)
- [Export Excel Cells to Image Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}