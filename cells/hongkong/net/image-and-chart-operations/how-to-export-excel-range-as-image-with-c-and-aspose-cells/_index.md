---
category: general
date: 2026-09-24
description: 使用 C# 及 Aspose.Cells 匯出 Excel 範圍為圖像 – 步驟教學，將工作表區域儲存為 PNG 或 JPEG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- Aspose.Cells export range
- C# Excel to PNG
- ImageOrPrintOptions usage
- export pivot table as image
language: zh-hant
lastmod: 2026-09-24
og_description: 使用 C# 及 Aspose.Cells 匯出 Excel 範圍為圖像。了解如何在數分鐘內將任何工作表區域（包括樞紐分析表）轉換為
  PNG 或 JPEG。
og_image_alt: Screenshot of a C# program exporting an Excel range to a PNG image
og_title: 使用 C# 匯出 Excel 範圍為影像 – 完整 Aspose.Cells 教學
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  headline: How to export excel range as image with C# and Aspose.Cells
  type: TechArticle
- description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  name: How to export excel range as image with C# and Aspose.Cells
  steps:
  - name: '**Load** the workbook from disk.'
    text: '**Load** the workbook from disk.'
  - name: '**Define** the cell area that will become the image (the *print area*).'
    text: '**Define** the cell area that will become the image (the *print area*).'
  - name: '**Export** the area using `ImageOrPrintOptions` and write the file.'
    text: '**Export** the area using `ImageOrPrintOptions` and write the file.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Image export
title: 如何使用 C# 與 Aspose.Cells 將 Excel 範圍匯出為圖片
url: /zh-hant/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 C# 與 Aspose.Cells 匯出 Excel 範圍為圖片

如果您需要在 .NET 應用程式中 **export excel range as image**，本指南將提供完整、可直接執行的解決方案。無論您是要發布儀表板、在網頁中嵌入樞紐分析表，或產生報告縮圖，都只需幾行 C# 程式碼，即可將任何工作表區域轉換為 PNG（或 JPEG）圖像。

在本教學中您將學會：

* 載入現有的活頁簿（`Workbook` 類別）  
* 定義要擷取的精確儲存格範圍（`PrintArea`）  
* 設定影像匯出選項（`ImageOrPrintOptions`）  
* 將產生的圖片儲存至磁碟  

已涵蓋所有先決條件、邊緣情況與常見陷阱，讓您能無後顧之憂地將程式碼套用到自己的專案中。

## 前置條件

| Requirement | Reason |
|-------------|--------|
| **Aspose.Cells for .NET**（最新版本） | 提供範例中使用的 `Workbook`、`Worksheet` 與 `ImageOrPrintOptions` API。 |
| **.NET 6.0 or later** | 此範例以 .NET 6 為目標，但任何支援 Aspose.Cells 的 .NET Core/Framework 版本皆可使用。 |
| **有效的 Excel 檔案**（例如 `input.xlsx`） | 您想要轉換的活頁簿。 |
| **對輸出資料夾的寫入權限** | `Save` 成功所必需的權限。 |

您可以透過 NuGet 安裝 Aspose.Cells：

```bash
dotnet add package Aspose.Cells
```

## 匯出 Excel 範圍為圖片 – 流程概觀

此操作由三個邏輯階段組成：

1. **Load** 從磁碟載入活頁簿。  
2. **Define** 會成為圖片的儲存格區域（*print area*）。  
3. **Export** 使用 `ImageOrPrintOptions` 匯出該區域並寫入檔案。  

以下每個階段皆細分為專屬步驟，並附上完整程式碼與說明。

## 步驟 1：載入活頁簿

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Path to the source Excel file
string inputPath = @"YOUR_DIRECTORY\input.xlsx";

// Create a Workbook object – this reads the file into memory
Workbook workbook = new Workbook(inputPath);
```

**為何重要**：  
`Workbook` 是所有 Excel 操作的入口點。一次載入檔案可降低記憶體使用，且之後可存取任何工作表。

## 步驟 2：存取目標工作表

```csharp
// Get the first worksheet (index 0). Change the index or use the sheet name as needed.
Worksheet sheet = workbook.Worksheets[0];
```

**提示**：如果需要依名稱取得特定工作表，請將索引改為 `workbook.Worksheets["SheetName"]`。這可避免工作簿版面變更時產生錯誤。

## 步驟 3：定義要匯出的範圍

```csharp
// Define the cell range that will be exported.
// Example: A1:G20 captures a typical pivot‑table area.
sheet.PageSetup.PrintArea = "A1:G20";
```

**為何設定 `PrintArea`？**  
Aspose.Cells 在產生影像時會以 *print area* 為基礎。將其限制在精確範圍內，可避免多餘的空白並提升效能。

### 替代方案：匯出整張工作表

如果想匯出整張工作表，只需省略 `PrintArea` 設定。Aspose.Cells 會預設使用工作表的已使用範圍。

## 步驟 4：設定影像匯出選項

```csharp
// Create an ImageOrPrintOptions object to control the output format.
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    // Choose PNG for lossless quality; change to Jpeg for smaller files.
    ImageFormat = ImageFormat.Png,

    // Optional: set the resolution (DPI). Higher DPI yields sharper images.
    HorizontalResolution = 300,
    VerticalResolution = 300,

    // Optional: set the page orientation if the range is wide.
    PageOrientation = PageOrientationType.Landscape
};
```

**Explanation of key properties:**  

* `ImageFormat` – 決定檔案類型（`Png`、`Jpeg`、`Bmp` 等）。PNG 適合圖表與文字，因為可保留清晰的邊緣。  
* `HorizontalResolution` / `VerticalResolution` – 控制像素密度。網頁縮圖使用 96 DPI 已足夠；列印品質建議使用 300 DPI。  
* `PageOrientation` – 當選取的範圍寬度大於高度時可協助調整。  

## 步驟 5：將範圍匯出為影像檔案

```csharp
// Define the output path for the image
string outputPath = @"YOUR_DIRECTORY\range.png";

// Save the first picture on the worksheet as an image.
// The Pictures collection is automatically populated after setting PrintArea.
sheet.Pictures[0].Save(outputPath, imgOptions);
```

**背後的運作原理**：  
當設定 `PrintArea` 後，Aspose.Cells 會產生代表該區域的暫時圖片。接著使用您提供的選項將 `Pictures[0]` 物件儲存。

### 處理未含圖片的工作表

如果工作表尚未包含圖片（例如全新檔案），您可以即時建立一張圖片：

```csharp
// Create a picture from the defined range and add it to the sheet
Picture pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
pic.Save(outputPath, imgOptions);
```

## 完整、可執行範例

將所有程式碼整合後，以下是一個可自行複製、貼上並執行的獨立主控台應用程式：

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // 2️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Define the range to export (e.g., a pivot table)
        sheet.PageSetup.PrintArea = "A1:G20";

        // 4️⃣ Set image export options (PNG, 300 DPI, landscape)
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300,
            PageOrientation = PageOrientationType.Landscape
        };

        // 5️⃣ Save the picture as an image file
        string outputPath = @"YOUR_DIRECTORY\range.png";

        // Ensure a picture exists; create one if necessary
        Picture pic;
        if (sheet.Pictures.Count == 0)
        {
            pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
        }
        else
        {
            pic = sheet.Pictures[0];
        }

        pic.Save(outputPath, imgOptions);

        System.Console.WriteLine($"Export completed: {outputPath}");
    }
}
```

**預期輸出**：  
會在 `YOUR_DIRECTORY` 中產生名為 `range.png` 的檔案。開啟後可看到 **A1 到 G20** 的精確儲存格以清晰的 PNG 圖像呈現。

## 常見變形與邊緣情況處理

| Scenario | Adjustment |
|----------|------------|
| **匯出為 JPEG** | 將 `ImageFormat = ImageFormat.Jpeg`，並可選擇設定 `Quality = 90`（範圍 0‑100）。 |
| **多重範圍** | 對每個範圍呼叫 `sheet.Pictures.Add`，並以不同檔名儲存每張圖片。 |
| **大型工作表** | 僅對需要的範圍提升 `HorizontalResolution`/`VerticalResolution`，以避免記憶體激增。 |
| **未產生圖片** | 確認 `PrintArea` 格式正確（`"A1:G20"`）。若地址無效，`Pictures` 集合會為空。 |
| **儲存至串流** | 當需要將影像保留於記憶體中（例如 ASP.NET 回應）時，使用 `pic.Save(Stream, imgOptions)`。 |

## 專業技巧：可靠的影像匯出

* **Validate the print area** – 使用 `CellArea` 解析（`CellArea area = CellArea.CreateCellArea("A1", "G20")`）以程式方式建立範圍，避免拼寫錯誤。  
* **Dispose of resources** – 若大量處理檔案，請將 `Workbook` 包於 `using` 區塊，以即時釋放原生資源。  
* **Batch processing** – 匯出數十個範圍時，重複使用同一個 `ImageOrPrintOptions` 實例，以減少物件分配開銷。  
* **Thread safety** – Aspose.Cells 物件 **不**具備執行緒安全性。請為每個執行緒建立獨立的 `Workbook`，或對存取進行同步。  

## 結論

您現在已擁有完整、可投入生產的 **export excel range as image** 方法，使用 C# 與 Aspose.Cells。這些步驟——載入活頁簿、設定列印區域、配置 `ImageOrPrintOptions`，以及儲存圖片——同時說明「如何」與「為何」，確保您能將程式碼套用於樞紐分析表、圖表或任何自訂儲存格區塊。

接下來，您可能會探索：

* **Export excel range as image** 以其他格式（SVG、BMP）匯出——可嘗試的次要關鍵字。  
* **Embedding the PNG in a PDF** 使用 Aspose.PDF 進行端到端報告產生。  
* **Automating batch exports** 透過簡單的主控台迴圈，對多個活頁簿執行批次匯出。  

歡迎嘗試不同的解析度、方向與輸出目錄。祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索替代實作方式。

- [使用 Aspose.Cells .NET 匯出 Excel 儲存格為圖片：逐步指南](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)
- [使用 Aspose.Cells for Java 匯出 Excel 活頁簿為圖片](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [如何使用 Aspose.Cells Java 將 Excel 工作表匯出為 PNG](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}