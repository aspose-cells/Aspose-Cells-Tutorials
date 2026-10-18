---
category: general
date: 2026-02-09
description: 在 C# 中建立樞紐分析表參照範圍並匯出樞紐分析表圖像。學習如何使用 Aspose.Cells 將 Excel 範圍儲存為 PNG——快速完整指南。
draft: false
keywords:
- create pivot reference range
- export pivot table image
- save excel range as png
- Aspose.Cells C#
- Excel automation C#
language: zh-hant
og_description: 在 C# 中建立樞紐分析表參考範圍，並將樞紐分析表圖像匯出為 PNG。完整的逐步教學，說明如何將 Excel 範圍儲存為 PNG。
og_title: 建立樞紐參考範圍 – 匯出樞紐分析表圖片為 PNG
tags:
- Aspose.Cells
- C#
- Excel
title: 建立樞紐參考範圍 – 匯出樞紐分析表圖像為 PNG
url: /zh-hant/net/rendering-and-export/create-pivot-reference-range-export-pivot-table-image-as-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立樞紐參考範圍 – 匯出樞紐表圖像為 PNG

需要在 Excel 活頁簿中使用 C# **建立樞紐參考範圍** 嗎？您也可以只用幾行程式碼 **匯出樞紐表圖像** 並 **將 Excel 範圍另存為 png**。依我的經驗，將即時的樞紐轉換為靜態圖像是一種方便的方式，可將分析嵌入報告、電郵或儀表板，而不必攜帶整個活頁簿。

在本教學中，我們會逐步說明您需要了解的所有內容：所需的函式庫、完整程式碼、每個呼叫的意義，以及可能遇到的幾個注意事項。完成後，您將能自信地產生任意樞紐表的 PNG 檔案，並了解如何將此模式套用到多個工作表或自訂圖像格式。

## 前置條件

- **Aspose.Cells for .NET**（免費試用版足以測試）。  
- **.NET 6.0** 或更新版本 – 我們使用的 API 完全相容於 .NET Standard 2.0+，因此舊版框架也能編譯。  
- 基本的 C# 專案（Console App、WinForms 或 ASP.NET – 任何能引用 NuGet 套件的環境）。  

如果您尚未安裝 Aspose.Cells，請執行：

```bash
dotnet add package Aspose.Cells
```

就這樣 – 不需要 COM interop，也不需要在伺服器上安裝 Excel。

## 步驟 1：開啟活頁簿並存取第一個工作表

首先要載入活頁簿檔案，並取得包含樞紐表的工作表。我們特意選取 **第一個工作表** (`Worksheets[0]`)，因為大多數示範檔案都把樞紐放在那裡，但您也可以改用名稱來取代索引。

```csharp
using Aspose.Cells;
using System;

// Load an existing Excel file (replace with your own path)
Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Access the first worksheet – this is where our pivot lives
Worksheet worksheet = wb.Worksheets[0];
```

*為什麼這很重要：* `Worksheet` 是任何基於範圍操作的入口點。如果指向錯誤的工作表，隨後的 `PivotTables[0]` 呼叫會拋出 `IndexOutOfRangeException`。

## 步驟 2：建立樞紐參考範圍

現在請求樞紐表本身提供一個 **參考範圍**。此範圍代表構成樞紐的所有儲存格——標題、資料列與彙總列。`CreateReferenceRange()` 方法在內部完成繁重的工作，處理合併儲存格與隱藏列。

```csharp
// Grab the first pivot table on the worksheet
PivotTable pivot = worksheet.PivotTables[0];

// Build a reference range that covers the whole pivot
Range pivotReferenceRange = pivot.CreateReferenceRange();
```

> **專業提示：** 若活頁簿中有多個樞紐，請遍歷 `worksheet.PivotTables`，並依其 `Name` 屬性挑選所需的那一個。

## 步驟 3：將參考範圍渲染為圖像

Aspose.Cells 能將任何 `Range` 渲染成圖像。回傳的物件同時支援點陣圖（PNG、JPEG）與向量圖（SVG）格式。此處我們要求預設的點陣圖，即相容於 `System.Drawing.Image` 的物件。

```csharp
// Convert the pivot reference range into an image object
ImageOrVector pivotImage = pivotReferenceRange.ToImage();
```

*底層發生了什麼？* API 會快照該範圍的視覺佈局，保留儲存格樣式、字型與條件格式化。這基本上等同於程式化的螢幕截圖，且不需要 UI。

## 步驟 4：將產生的圖像儲存為檔案

最後，我們將圖像寫入磁碟。當您提供「.png」副檔名時，`Save` 方法會自動選擇 PNG 格式。若需要 DPI 控制或其他格式，也可以傳入 `SaveOptions` 物件。

```csharp
// Save the image as PNG – the extension drives the format
pivotImage.Save("YOUR_DIRECTORY/pivot.png");
```

執行此行程式後，開啟 `pivot.png`，您會看到樞紐表的像素完美快照，隨時可嵌入任何地方。

## 完整範例

將上述步驟整合起來，以下是一個可直接複製貼上執行的自包含 Console 程式：

```csharp
using Aspose.Cells;
using System;

namespace PivotExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

            // 2️⃣ Access first worksheet
            Worksheet worksheet = wb.Worksheets[0];

            // 3️⃣ Get first pivot table
            if (worksheet.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found on the first sheet.");
                return;
            }
            PivotTable pivot = worksheet.PivotTables[0];

            // 4️⃣ Create a reference range that covers the whole pivot
            Range pivotReferenceRange = pivot.CreateReferenceRange();

            // 5️⃣ Render the range to an image
            ImageOrVector pivotImage = pivotReferenceRange.ToImage();

            // 6️⃣ Save as PNG
            string outputPath = "YOUR_DIRECTORY/pivot.png";
            pivotImage.Save(outputPath);

            Console.WriteLine($"Pivot table image saved to {outputPath}");
        }
    }
}
```

**預期輸出：** 產生一個名為 `pivot.png` 的檔案，位於 `YOUR_DIRECTORY`。使用任何影像檢視器開啟，它應該完整呈現原始樞紐的版面，包括欄位標題、資料列與總計列。

## 匯出樞紐表圖像 – 自訂大小與 DPI

有時預設圖像對於簡報投影片來說太小。您可以透過傳入 `ImageOrVectorSaveOptions` 物件來控制解析度：

```csharp
using Aspose.Cells.Drawing;

// Define PNG options – 300 DPI for high‑quality print
ImageOrVectorSaveOptions options = new ImageOrVectorSaveOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300 // DPI
};

pivotImage.Save("YOUR_DIRECTORY/pivot_highres.png", options);
```

*為什麼要調整 DPI？* 較高的 DPI 會產生更銳利的邊緣，特別是當 PNG 在 PowerPoint 或 PDF 中放大時。

## 將 Excel 範圍另存為 PNG – 處理多個工作表

若需從多個工作表匯出樞紐，請遍歷 `Workbook.Worksheets` 並重複上述步驟。以下是一段簡潔的程式碼片段：

```csharp
foreach (Worksheet ws in wb.Worksheets)
{
    foreach (PivotTable pt in ws.PivotTables)
    {
        Range refRange = pt.CreateReferenceRange();
        ImageOrVector img = refRange.ToImage();
        string fileName = $"pivot_{ws.Name}_{pt.Name}.png";
        img.Save($"YOUR_DIRECTORY/{fileName}");
        Console.WriteLine($"Saved {fileName}");
    }
}
```

此模式會 **匯出樞紐表圖像** 給活頁簿中的每個樞紐，且每個檔案皆以其工作表與樞紐名稱命名——非常適合批次處理。

## 常見陷阱與避免方法

| 問題 | 為什麼會發生 | 解決方式 |
|------|--------------|----------|
| `IndexOutOfRangeException` on `PivotTables[0]` | 工作表沒有樞紐表。 | 在存取前先檢查 `worksheet.PivotTables.Count`。 |
| Blank image output | 樞紐已過濾至隱藏所有列。 | 確保樞紐有可見資料，或在建立範圍前呼叫 `pivot.RefreshData();`。 |
| Low‑resolution PNG | 預設 DPI 為 96。 | 如上例使用 `ImageOrVectorSaveOptions.Resolution`。 |
| File‑path errors | `YOUR_DIRECTORY` 中有無效字元。 | 使用 `Path.Combine` 並搭配 `Path.GetInvalidPathChars()` 進行清理。 |

## 驗證 – 快速測試

執行完整範例後：

1. 在 Windows Photo Viewer 中開啟 `pivot.png`。  
2. 核對欄位標題、資料列與總計列是否與 Excel 畫面相符。  
3. 若發現遺漏的列，請再次確認在呼叫 `CreateReferenceRange()` 前已執行樞紐的 **RefreshData** 方法。

## 加分項：將 PNG 嵌入 Word 文件

因為圖像已是 PNG 格式，您可以直接將它餵給 Aspose.Words：

```csharp
using Aspose.Words;
Document doc = new Document();
DocumentBuilder builder = new DocumentBuilder(doc);
builder.InsertImage("YOUR_DIRECTORY/pivot.png");
doc.Save("YOUR_DIRECTORY/report.docx");
```

現在您擁有一份包含樞紐快照的 Word 報告——不需要手動複製貼上。

## 結論

您剛剛學會如何使用 Aspose.Cells 在 C# 中 **建立樞紐參考範圍**、**匯出樞紐表圖像**，以及 **將 Excel 範圍另存為 png**。重點如下：

- 使用 `PivotTable.CreateReferenceRange()` 取得樞紐的可視區域。  
- 以 `Range.ToImage()` 將該範圍轉換為圖像。  
- 以 PNG 格式儲存圖像，必要時調整 DPI 以符合列印品質。  

接下來，您可以探索批次匯出、不同圖像格式（SVG、JPEG），甚至將 PNG 嵌入 PDF 或 Word 文件。只要將樞紐捕捉為靜態圖形，創意的可能性無限。

有任何問題或特殊情境想討論？歡迎在下方留言，祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}