---
category: general
date: 2026-07-26
description: 如何在幾個步驟內將 Excel 工作表的圖形匯出至 PowerPoint — 為開發者設計的快速 Excel 匯出至 PPTX 教學
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export shapes
- convert worksheet to powerpoint
- export excel to pptx
- excel to powerpoint tutorial
- export excel workbook powerpoint
language: zh-hant
lastmod: 2026-07-26
og_description: 一步一步教你如何將 Excel 中的圖形匯出至 PowerPoint。跟隨此 Excel 匯出至 PPTX 教學，讓你的工作表變成可編輯的投影片。
og_image_alt: Screenshot showing how to export shapes from Excel to PowerPoint using
  Aspose.Cells
og_title: 如何將 Excel 圖形匯出至 PowerPoint – 快速簡易
schemas:
- author: Aspose
  dateModified: '2026-07-26'
  description: How to export shapes from an Excel worksheet to PowerPoint in just
    a few steps – a quick export excel to pptx tutorial for developers.
  headline: How to Export Shapes from Excel to PowerPoint – Complete Guide
  type: TechArticle
- description: How to export shapes from an Excel worksheet to PowerPoint in just
    a few steps – a quick export excel to pptx tutorial for developers.
  name: How to Export Shapes from Excel to PowerPoint – Complete Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - A valid
      license for **Aspose.Cells for .NET** (the free trial works for testing). -
      An Excel workbook (e.g., `ShapesDemo.xlsx`) that contains at least one text
      box or shape. - A development environment—Visual Studio, Rider, or VS Co'
  - name: Multiple Worksheets
    text: If you need to export several sheets into a single PPTX, loop through `workbook.Worksheets`
      and call `worksheet.Save` with the same `pptxOptions`. Aspose.Cells will automatically
      add a new slide for each sheet.
  - name: Custom Slide Layouts
    text: You can specify `pptxOptions.SlideSize` (e.g., `SlideSizeType.Widescreen`)
      to match your corporate deck dimensions.
  - name: Missing Files or Permissions
    text: 'Wrap the whole `Main` method in a `try` block:'
  type: HowTo
- questions:
  - answer: Yes. `Workbook` can open `.xls`, `.xlsx`, and even CSV files. The shape
      export works the same way.
    question: Does this work with older Excel formats (.xls)?
  - answer: Charts are already exported as native PowerPoint charts; you don’t need
      extra flags.
    question: What if I need to keep charts editable?
  - answer: Absolutely—just replace `SaveFormat.Pptx` with `SaveFormat.Pdf` and omit
      the `PptxSaveOptions`.
    question: Can I export to PDF instead of PPTX?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Office Automation
title: 如何將 Excel 圖形匯出至 PowerPoint – 完整指南
url: /zh-hant/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何從 Excel 匯出圖形至 PowerPoint – 完整指南

有沒有想過 **如何匯出圖形** 從 Excel 檔案並在 PowerPoint 投影片中保持可編輯？你並不是唯一有此需求的人。無論你是在建立報告流程，或只是需要快速將試算表轉換成簡報，能夠 **convert worksheet to PowerPoint** 而不失去圖形可編輯性的能力，都能為你節省大量手動工作時間。

在本 **excel to powerpoint tutorial** 中，我們將逐步說明一個完整可執行的 C# 範例，該範例會載入活頁簿、設定正確的匯出選項，並產生 PPTX 檔案，使文字方塊與其他繪圖物件保持可編輯。沒有模糊的說明——只有你今天就能複製、貼上並執行的程式碼。

## 你將學到

- 在保持圖形可編輯性的前提下，執行 **export excel to pptx** 的完整步驟。  
- `Aspose.Cells` 函式庫的 `PptxSaveOptions` 如何控制匯出行為。  
- 處理多個工作表、檔案遺失以及自訂圖形設定的技巧。  
- 一個完整且可執行的程式，你可以直接放入任何 .NET 專案中使用。

### 前置條件

- .NET 6.0 或更新版本（程式碼亦可在 .NET Framework 4.7+ 上執行）。  
- 有效的 **Aspose.Cells for .NET** 授權（免費試用版可用於測試）。  
- 一個 Excel 活頁簿（例如 `ShapesDemo.xlsx`），內含至少一個文字方塊或圖形。  
- 開發環境—Visual Studio、Rider 或 VS Code 任一皆可。

如果你已具備上述條件，讓我們開始吧。

## 步驟 1：載入活頁簿 – 匯出圖形的起點

首先，我們需要開啟包含欲保持可編輯圖形的 Excel 檔案。

```csharp
using Aspose.Cells;
using System;

class ExportEditableShapes
{
    static void Main()
    {
        // Load the Excel workbook that contains text boxes and other shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesDemo.xlsx");
        Worksheet worksheet = workbook.Worksheets[0];
```

**為什麼這很重要：**  
`Workbook` 物件是檔案內所有儲存格、圖表與繪圖物件的入口。透過取得第一張工作表 (`Worksheets[0]`) 我們確保使用已知的工作表，但若需要特定分頁，可將索引改為名稱 (`workbook.Worksheets["Sheet2"]`)。

> **小技巧：** 將載入呼叫包在 `try / catch` 區塊中，以在檔案路徑錯誤時提供友善的錯誤訊息。

## 步驟 2：設定 PPTX 匯出選項 – 匯出圖形的核心

現在我們告訴 Aspose.Cells 在產生的 PPTX 中保持圖形可編輯。

```csharp
        // Configure PPTX export options to keep shapes editable
        var pptxOptions = new Aspose.Cells.Export.PptxSaveOptions
        {
            ExportEditableTextBoxes = true, // makes text boxes editable in the PPTX
            ExportEditableShapes = true     // makes other shapes editable in the PPTX
        };
```

**為什麼要使用這些旗標？**  
- `ExportEditableTextBoxes` 會將 Excel 文字方塊轉換為 PowerPoint 文字佔位符，讓你可以雙擊編輯。  
- `ExportEditableShapes` 對箭頭、矩形、SmartArt 等圖形執行相同操作。若未使用這些旗標，物件會變成靜態圖片，失去 **convert worksheet to powerpoint** 工作流程的意義。

你也可以調整 `PptxSaveOptions` 以控制投影片尺寸、主題或是否嵌入字型——當簡報必須符合公司品牌時相當有用。

## 步驟 3：將工作表儲存為 PPTX – 完成 Export Excel Workbook PowerPoint 的最後一步

設定好選項後，儲存相當簡單。

```csharp
        // Save the worksheet as a PPTX file with the editable shapes option
        worksheet.Save("YOUR_DIRECTORY/ShapesEditable.pptx", SaveFormat.Pptx, pptxOptions);
```

**背後發生了什麼？**  
Aspose.Cells 會遍歷工作表上的每個繪圖物件，將其對應到相應的 PowerPoint shape 類別，並寫入 PowerPoint 可讀取的 XML。由於我們啟用了可編輯旗標，XML 會將每個圖形標記為 `Shape` 而非 `Picture`，因此 PowerPoint 會將其視為可即時編輯的物件。

## 步驟 4：確認匯出 – 為使用者提供快速回饋

一條簡短的主控台訊息會告訴你流程已成功。

```csharp
        // Inform the user that the export is complete
        Console.WriteLine("Exported worksheet with editable shapes.");
    }
}
```

如果執行程式後看到訊息，請在 PowerPoint 中開啟 `ShapesEditable.pptx`。點擊任意文字方塊——你應該能直接編輯文字，拖曳圖形時也會像原生 PowerPoint 物件一樣移動。

## 步驟 5：處理實務情境

以下列出在進行 **excel to powerpoint tutorial** 時可能遇到的常見變化。

### 多工作表

如果需要將多張工作表匯出至同一個 PPTX，可遍歷 `workbook.Worksheets`，並使用相同的 `pptxOptions` 呼叫 `worksheet.Save`。Aspose.Cells 會自動為每張工作表新增投影片。

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.Save($"YOUR_DIRECTORY/{ws.Name}.pptx", SaveFormat.Pptx, pptxOptions);
}
```

### 自訂投影片版面

你可以設定 `pptxOptions.SlideSize`（例如 `SlideSizeType.Widescreen`）以符合公司簡報的尺寸。

```csharp
pptxOptions.SlideSize = SlideSizeType.Widescreen;
```

### 檔案遺失或權限問題

將整個 `Main` 方法包在 `try` 區塊中：

```csharp
try
{
    // ... existing code ...
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error: {ex.Message}");
}
```

這使得 **export excel workbook powerpoint** 流程在生產管線中更具韌性。

## 完整範例

以下是你現在即可編譯的完整程式。將其儲存為 `ExportEditableShapes.cs`，調整檔案路徑後執行 `dotnet run`。

```csharp
using Aspose.Cells;
using System;

class ExportEditableShapes
{
    static void Main()
    {
        try
        {
            // Step 1: Load the Excel workbook that contains text boxes and other shapes
            Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesDemo.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 2: Configure PPTX export options to keep shapes editable
            var pptxOptions = new Aspose.Cells.Export.PptxSaveOptions
            {
                ExportEditableTextBoxes = true, // makes text boxes editable in the PPTX
                ExportEditableShapes = true,    // makes other shapes editable in the PPTX
                SlideSize = SlideSizeType.Widescreen // optional: set slide size
            };

            // Step 3: Save the worksheet as a PPTX file with the editable shapes option
            worksheet.Save("YOUR_DIRECTORY/ShapesEditable.pptx", SaveFormat.Pptx, pptxOptions);

            // Step 4: Inform the user that the export is complete
            Console.WriteLine("Exported worksheet with editable shapes.");
        }
        catch (Exception ex)
        {
            // Step 5: Handle errors gracefully
            Console.Error.WriteLine($"Export failed: {ex.Message}");
        }
    }
}
```

**預期輸出** 當你執行程式時：

```
Exported worksheet with editable shapes.
```

開啟產生的 `ShapesEditable.pptx`，你會看到每個 Excel 圖形都成為完全可編輯的 PowerPoint 物件——正是你在搜尋 **how to export shapes** 時所期待的結果。

## 常見問題

- **這能支援較舊的 Excel 格式 (.xls) 嗎？**  
  是的。`Workbook` 能開啟 `.xls`、`.xlsx` 甚至 CSV 檔案。圖形匯出方式相同。

- **如果需要保持圖表可編輯該怎麼辦？**  
  圖表已會匯出為原生 PowerPoint 圖表，無需額外旗標。

- **可以匯出成 PDF 而非 PPTX 嗎？**  
  當然可以——只要將 `SaveFormat.Pptx` 改為 `SaveFormat.Pdf`，並省略 `PptxSaveOptions` 即可。

## 結論

現在你已擁有一套完整、端對端的解決方案，能將 Excel 中的 **how to export shapes** 匯出至可編輯的 PowerPoint 投影片。透過 `Aspose.Cells` 的 `PptxSaveOptions`，你可以保留每個文字方塊與繪圖物件，將靜態試算表轉變為動態簡報，且只需極少的工作量。

準備好接受下一個挑戰了嗎？試著加入自訂投影片母片、以程式方式插入圖片，或將此匯出流程串接至 CI/CD 管線，自動產生每週的業績簡報。**export excel workbook powerpoint** 的世界正等著你去探索！

--- 

*如果你覺得這篇 **excel to powerpoint tutorial** 有幫助，請在 GitHub 上給予星星或分享給仍然把試算表複製貼上到投影片的同事。祝開發愉快！*

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎延伸技術。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [如何使用 Aspose.Cells Java 將 Excel 工作表匯出為 PNG](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [如何使用 Aspose.Cells for Java 將 Excel 儲存格匯出為圖片](/cells/english/java/import-export/export-excel-cells-as-image-aspose-cells-java/)
- [如何使用 Aspose.Cells Java 將 Excel 圖表匯出為 SVG（可縮放向量圖形）](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}