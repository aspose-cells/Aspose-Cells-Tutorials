---
category: general
date: 2026-03-30
description: 快速使用 Aspose.Cells 與 Aspose.Slides 從 Excel 建立 PowerPoint。了解如何將工作表匯出為影像，並以
  C# 將簡報儲存為 PPTX。
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export worksheet as image
- save presentation as pptx
- export excel chart as picture
language: zh-hant
og_description: 使用 Aspose 在 C# 中從 Excel 建立 PowerPoint。將工作表匯出為圖像，保持形狀可編輯，並將結果儲存為 PPTX。
og_title: 從 Excel 建立 PowerPoint – 完整 C# 教學
tags:
- Aspose
- C#
- Office Automation
title: 從 Excel 建立 PowerPoint – C# 逐步指南
url: /zh-hant/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 Excel 建立 PowerPoint – 完整 C# 教學

是否曾經需要 **從 Excel 建立 PowerPoint**，卻不確定哪個函式庫能讓圖表保持可編輯？你並不孤單。在許多報表情境下，你會想把試算表轉成投影片，同時保留之後調整文字方塊的能力。本指南將示範如何使用 Aspose.Cells 與 Aspose.Slides **將 Excel 轉換為 PowerPoint**，並說明如何 **將工作表匯出為影像**，最後 **將簡報儲存為 PPTX**。

我們會逐行說明程式碼，解釋每個設定背後的原因，甚至討論當工作簿包含複雜圖表且你想將其以圖片形式匯出時的處理方式。完成後，你將擁有一個可直接執行的 C# 主控台應用程式，將 `ShapesDemo.xlsx` 轉成 `Result.pptx` – 並保有可編輯的文字方塊與清晰的影像。

## 需要的環境

- .NET 6.0 或更新版本（API 亦支援 .NET Framework，但 .NET 6 為最佳選擇）。  
- **Aspose.Cells** 與 **Aspose.Slides** NuGet 套件（免費試用授權即可測試）。  
- 基本的 C# 語法概念 – 只要會寫 `Console.WriteLine` 就足夠。  

不需要額外的 COM interop、伺服器上不必安裝 Office，也不必手動複製貼上圖片。一切皆以程式方式完成。

---

## 從 Excel 建立 PowerPoint – 載入活頁簿並設定匯出選項

首先，我們開啟 Excel 檔案，並告訴 Aspose.Cells 我們希望如何呈現工作表。`ImageOrPrintOptions` 物件就是魔法發生的地方：我們啟用 `ExportShapes` 與 `ExportEditableTextBoxes`，讓所有形狀（包括圖表）在投影片中保持 **可編輯**。

```csharp
using Aspose.Cells;
using Aspose.Slides;

// 1️⃣ Load the Excel workbook
string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
Workbook workbook = new Workbook(excelPath);
Worksheet worksheet = workbook.Worksheets[0];   // Grab the first sheet

// 2️⃣ Configure image export – keep shapes editable
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    OnePagePerSheet = true,          // Export the whole sheet as one slide
    ExportShapes = true,             // Include shapes (charts, drawings)
    ExportEditableTextBoxes = true   // Make text boxes editable in PPTX
};
```

**為什麼要設定這些旗標？**  
- `OnePagePerSheet` 可防止工作表被切割成多張投影片 – 只會產生單一完整大小的圖片。  
- `ExportShapes` 告訴 Aspose.Cells 要將圖表 *以及* 向量形狀光柵化，保留外觀。  
- `ExportEditableTextBoxes` 是讓你在 PowerPoint 中雙擊文字方塊即可編輯文字，而不必再開啟 Excel 的祕密武器。

> **小技巧：** 若你只需要圖表的靜態圖片，可將 `ExportShapes = false`，之後使用 `ExportExcelChartAsPicture` 方法（見最後一節）。

---

## 從 Excel 轉換為 PowerPoint – 從工作表產生影像

設定完成後，我們將工作表轉成 `System.Drawing.Image`。`WorksheetToImageConverter` 會執行主要工作，套用我們剛才定義的設定。

```csharp
// 3️⃣ Convert the worksheet to an image using the options above
WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
System.Drawing.Image sheetImage = converter.ConvertToImage(0, imageOptions);
```

`0` 參數代表第一頁（因為 `OnePagePerSheet` 只會有一頁）。產生的 `sheetImage` 會保留原始 DPI，確保投影片在高解析度螢幕上不會顯得模糊。

---

## 儲存簡報為 PPTX – 將影像插入投影片

接著，我們建立全新的 PowerPoint 檔案，新增一張投影片，並把位圖放上去。Aspose.Slides 會把圖片當作 *圖片框架*（picture frame）形狀，你之後可以像操作任何原生 PowerPoint 物件一樣調整大小或位置。

```csharp
// 4️⃣ Create a new PowerPoint presentation
Presentation presentation = new Presentation();
ISlide slide = presentation.Slides[0];   // The default blank slide

// Add the Excel‑derived image as a picture frame
slide.Shapes.AddPictureFrame(
    ShapeType.Rectangle,                 // Simple rectangle container
    0, 0,                                // Top‑left corner (0,0)
    sheetImage.Width,                    // Width of the picture
    sheetImage.Height,                   // Height of the picture
    sheetImage);                         // The bitmap we generated
```

> **如果影像大於投影片尺寸該怎麼辦？**  
> PowerPoint 會自動裁切超出投影片範圍的部分。快速解決方式是先縮放影像再插入：

```csharp
float scale = Math.Min(presentation.SlideSize.Size.Width / (float)sheetImage.Width,
                       presentation.SlideSize.Size.Height / (float)sheetImage.Height);
int newWidth  = (int)(sheetImage.Width * scale);
int newHeight = (int)(sheetImage.Height * scale);
```

然後把 `newWidth` 與 `newHeight` 傳給 `AddPictureFrame`。

---

## 匯出工作表為影像 – 儲存 PPTX 檔案

最後，我們把簡報寫入磁碟。`SaveFormat.Pptx` 旗標保證使用現代的 OpenXML 格式，適用於所有近期版本的 PowerPoint。

```csharp
// 5️⃣ Save the presentation as a PPTX file
string pptxPath = "YOUR_DIRECTORY/Result.pptx";
presentation.Save(pptxPath, SaveFormat.Pptx);
```

開啟 `Result.pptx` 後，你會看到只有一張投影片，外觀與 Excel 工作表完全相同，同時仍可直接在 PowerPoint 中點擊任意文字方塊進行編輯。

---

## 匯出 Excel 圖表為圖片 – 當需要光柵圖時

有時你不需要可編輯的形狀，只要一張高品質 PNG 圖表即可。Aspose.Cells 能夠將特定圖表匯出為影像，而不必轉換整個工作表：

```csharp
// Example: Export the first chart on the sheet as a PNG
int chartIndex = 0; // Adjust if you have multiple charts
Chart chart = worksheet.Charts[chartIndex];
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    OnePagePerSheet = false
};
chart.ToImage("chart.png", chartOptions);
```

之後你可以像插入 `sheetImage` 那樣把 `chart.png` 放入投影片。此作法可減少 PPTX 檔案大小，且在不需要周圍資料時特別有用。

---

## 常見問題與避免方式

| 問題 | 為什麼會發生 | 解決方法 |
|------|--------------|----------|
| **文字模糊** | 匯出時 DPI 較低（預設 96）。 | 在轉換前設定 `imageOptions.Dpi = 300;` |
| **形狀消失** | `ExportShapes` 為 `false`。 | 需要可編輯圖形時，確保 `ExportShapes = true` |
| **投影片尺寸不符** | 影像大於投影片尺寸。 | 縮放影像（參見程式碼片段）或透過 `presentation.SlideSize` 調整投影片大小 |
| **授權例外** | 使用試用版未正確啟用授權。 | 在 `Main` 開頭呼叫 `License license = new License(); license.SetLicense("Aspose.Total.lic");` |

---

## 完整範例（可直接複製貼上）

以下是完整程式碼，可直接放入新的主控台專案。將 `YOUR_DIRECTORY` 替換為放置 Excel 檔案的資料夾路徑。

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;
using System.Drawing;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook
            // -----------------------------------------------------------------
            string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
            Workbook workbook = new Workbook(excelPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -----------------------------------------------------------------
            // 2️⃣ Set up export options – keep shapes editable
            // -----------------------------------------------------------------
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                OnePagePerSheet = true,
                ExportShapes = true,
                ExportEditableTextBoxes = true,
                Dpi = 300                 // High‑resolution output
            };

            // -----------------------------------------------------------------
            // 3️⃣ Convert worksheet to an image
            // -----------------------------------------------------------------
            WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
            Image sheetImage = converter.ConvertToImage(0, imageOptions);

            // -----------------------------------------------------------------
            // 4️⃣ Create PowerPoint and add the image as a slide
            // -----------------------------------------------------------------
            Presentation presentation = new Presentation();
            ISlide slide = presentation.Slides[0];
            slide.Shapes.AddPictureFrame(
                ShapeType.Rectangle,
                0, 0,
                sheetImage.Width,
                sheetImage.Height,
                sheetImage);

            // -----------------------------------------------------------------
            // 5️⃣ Save the PPTX file
            // -----------------------------------------------------------------
            string pptxPath = "YOUR_DIRECTORY/Result.pptx";
            presentation.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine("✅ PowerPoint created successfully at: " + pptxPath);
        }
    }
}
```

**預期輸出：**  
執行程式會印出 `✅ PowerPoint created successfully at: YOUR_DIRECTORY/Result.pptx`。開啟 PPTX 後會看到單一投影片，與原始 Excel 工作表鏡像，且文字方塊仍可編輯。

---

## 重點回顧與後續步驟

你現在已掌握如何使用 Aspose 強大的 API **從 Excel 建立 PowerPoint**、**將工作表匯出為影像**，以及 **以 PPTX 格式儲存簡報**，同時保留可編輯性。同樣的模式也適用於多工作表的活頁簿——只要遍歷 `workbook.Worksheets`，為每張工作表新增一張投影片即可。

**接下來可以探索的方向？**  

- **批次轉換：** 迴圈處理資料夾內的多個 Excel 檔案，為每個檔案產生投影片套件。  
- **動態版面配置：** 使用 `slide.LayoutSlide` 套用預先設計好的 PowerPoint 範本。  
- **僅圖表匯出：** 結合「匯出 Excel 圖表為圖片」的程式碼，搭配投影片佔位符，打造更精簡的簡報。  
- **進階樣式：** 透過 Aspose.Slides 套用自訂投影片背景、過場動畫或動態效果。

盡情實驗吧——調整 DPI、將 `ShapeType.Ellipse` 換成圓形圖片框，甚至在同一投影片中嵌入多張圖片。只要掌握程式化的控制權，創意的可能性無限。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}