---
category: general
date: 2026-10-26
description: 設定列印區域並在 C# 中將 Excel 工作表匯出為 PNG。了解影像匯出選項、如何匯出 PNG，以及如何從活頁簿取得可列印的影像。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area
- excel sheet to png
- how to export png
- export excel image
- image export options
language: zh-hant
lastmod: 2026-10-26
og_description: 設定列印區域並在 C# 中將 Excel 工作表匯出為 PNG。本逐步教學涵蓋影像匯出選項以及如何從活頁簿匯出 PNG。
og_image_alt: Screenshot showing an Excel worksheet with the print area set and exported
  as a PNG image
og_title: 設定列印範圍並將 Excel 工作表匯出為 PNG – C# 指南
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Set print area and export an Excel sheet to PNG in C#. Learn image
    export options, how to export PNG, and get a printable image from a workbook.
  headline: Set print area and export Excel sheet to PNG in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: 在 C# 中設定列印範圍並將 Excel 工作表匯出為 PNG
url: /zh-hant/net/rendering-and-export/set-print-area-and-export-excel-sheet-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 設定列印區域並將 Excel 工作表匯出為 PNG（C#）

如果您需要在將 Excel 工作表匯出為 PNG 之前 **設定列印區域**，本指南將示範如何操作。您將看到完整的 C# 範例，說明如何設定影像匯出選項、調整工作表的列印區域，並將結果儲存為圖片。

將 Excel 工作表匯出為 PNG 是在報告、電子郵件或網頁中嵌入工作表快照的常見需求。以下程式碼適用於任何包含樞紐分析表的活頁簿，且同樣適用於一般資料範圍。無需額外工具——只要使用 Aspose.Cells for .NET 套件即可。

## 前置條件

- .NET 6.0 或更新版本（範例以 .NET 6 為目標，但任何近期的 .NET 版本皆可）
- Aspose.Cells for .NET（透過 NuGet 安裝：`Install-Package Aspose.Cells`）
- 具備基本的 C# 與 Excel 概念，例如工作表與列印區域

## 步驟 1：設定影像匯出選項

首先建立一個 `ImageOrPrintOptions` 實例。此物件告訴 Aspose.Cells 如何將工作表渲染為影像。

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

// Define image export options (PNG format)
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    // Export quality settings can be adjusted here
    ImageFormat = ImageFormat.Png,
    // Optional: set resolution (DPI) for higher‑quality PNGs
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**為什麼重要：** `ImageOrPrintOptions` 控制輸出格式、解析度與其他渲染細節。使用 PNG 可確保無損品質，適合需要清晰文字與圖形的報告。

## 步驟 2：載入活頁簿並取得目標工作表

```csharp
// Load an existing workbook (replace with your file path)
Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

// Access the first worksheet in the workbook
Worksheet worksheet = wb.Worksheets[0];
```

**為什麼重要：** 必須針對特定的 `Worksheet` 物件操作，因為列印區域是工作表層級的設定。

## 步驟 3：找出要列印的範圍

在許多情況下，您關心的資料位於樞紐分析表內。以下程式碼會擷取工作表上第一個樞紐分析表的資料範圍。

```csharp
// Get the data range of the first pivot table on the worksheet
CellArea pivotDataRange = worksheet.PivotTables[0].PivotDataRange;
```

如果您的工作表不含樞紐分析表，您可以將 `pivotDataRange` 改為自行建立的任意 `CellArea`，例如：

```csharp
CellArea customRange = new CellArea(0, 0, 20, 10); // A1:K21
```

## 步驟 4：**設定列印區域** 以符合選取的範圍

```csharp
// Set the worksheet's print area to match the pivot table's data range
worksheet.PageSetup.PrintArea = pivotDataRange.RefersTo;
```

**為什麼重要：** 列印區域告訴 Excel（以及 Aspose.Cells）在渲染工作表為影像時應包含哪些儲存格。將列印區域與樞紐資料範圍對齊，可避免空白邊緣，確保匯出的 PNG 只包含相關資料。

## 步驟 5：將工作表匯出為 PNG 影像

```csharp
// Export the worksheet to an image using the defined options
// and assign the resulting image to the first picture shape on the sheet
worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);

// Optionally, save the image to a file for external use
worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);
```

**為什麼重要：** `worksheet.ToImage` 會遵循先前設定的列印區域，因此 PNG 檔案僅包含您定義的儲存格。將影像指派給圖片形狀可在需要時重新嵌入活頁簿，而儲存至磁碟則可得到獨立檔案。

## 完整範例

將所有步驟組合起來，即可得到一個可直接執行的完整程式。

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

class ExportExcelToPng
{
    static void Main()
    {
        // 1️⃣ Configure image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 2️⃣ Load the workbook
        Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

        // 3️⃣ Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // 4️⃣ Get the data range of the first pivot table (or define your own)
        CellArea dataRange = worksheet.PivotTables[0].PivotDataRange;

        // 5️⃣ **Set print area** to the data range
        worksheet.PageSetup.PrintArea = dataRange.RefersTo;

        // 6️⃣ Export the worksheet as PNG
        worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);
        worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);

        Console.WriteLine("Export complete: WorksheetExport.png created.");
    }
}
```

### 預期結果

執行程式後會產生 `C:\Temp\WorksheetExport.png`。開啟該檔案會看到一張清晰的 PNG 圖片，僅包含 **設定列印區域** 後的儲存格（本例為樞紐分析表資料）。此影像可直接插入 Word 文件、PowerPoint 投影片或網頁，無需額外轉換步驟。

## 處理多個工作表或樞紐分析表

- **多個工作表：** 迭代 `wb.Worksheets`，對每張需要匯出的工作表重複步驟 3‑5。
- **多個樞紐分析表：** 使用適當的 `PivotTables[index]`，或遍歷 `worksheet.PivotTables` 逐一匯出。
- **沒有樞紐分析表：** 手動建立 `CellArea`（參見步驟 3 的註解），並指派給 `PrintArea`。

## 實用技巧（E‑E‑A‑T）

- **專業提示：** 將 `HorizontalResolution` 與 `VerticalResolution` 設為 300 DPI，可產生列印品質的 PNG；若為網路使用，可降低解析度以減少檔案大小。
- **留意空的圖片形狀：** 若工作表沒有圖片形狀，請先新增一個再指派影像：

```csharp
if (worksheet.Pictures.Count == 0)
{
    worksheet.Pictures.Add(0, 0, 0, 0);
}
```

- **效能考量：** 對多個工作表重複使用同一個 `ImageOrPrintOptions` 實例，可避免不必要的記憶體配置。
- **相容性：** Aspose.Cells 23.9 以上完整支援 .NET 6 及更新版本；較舊版本可能需要調整 API 名稱。

## 結論

現在您已掌握如何 **設定列印區域** 並將 Excel 工作表匯出為 PNG。

## 接下來該學什麼？

以下教學與本指南緊密相關，提供完整的程式碼範例與逐步說明，協助您深入了解其他 API 功能，並在自己的專案中探索不同的實作方式。

- [How to export Excel to PNG – full step‑by‑step guide](/cells/english/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/)
- [How to export excel range as image with C# and Aspose.Cells](/cells/english/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/)
- [excel sheet to png – Export a Pivot Table as PNG in C#](/cells/english/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}