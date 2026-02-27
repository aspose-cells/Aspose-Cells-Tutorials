---
category: general
date: 2026-02-26
description: 使用 C# 從 Excel 匯出圖表至 PowerPoint。了解如何將 Excel 轉換為 PowerPoint、將 Excel 儲存為
  PowerPoint，並保持形狀可編輯。
draft: false
keywords:
- export chart to powerpoint
- convert excel to powerpoint
- save excel as powerpoint
- how to convert excel to ppt
- save workbook as pptx
language: zh-hant
og_description: 使用 C# 從 Excel 匯出圖表至 PowerPoint。本指南說明如何將 Excel 轉換為 PowerPoint、將活頁簿另存為
  PPTX，並保持圖形可編輯。
og_title: 使用 C# 匯出圖表至 PowerPoint – 完整程式設計教學
tags:
- Aspose.Cells
- C#
- Office Automation
title: 匯出圖表至 PowerPoint（使用 C#）– 完整逐步指南
url: /zh-hant/net/chart-rendering-and-conversion/export-chart-to-powerpoint-with-c-complete-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 匯出圖表至 PowerPoint – 完整程式教學

有沒有想過要 **匯出圖表至 PowerPoint** 同時保留可編輯性？在許多報表情境下，你需要在投影片中放入即時圖表，但手動複製貼上非常麻煩。好消息是，只要幾行 C# 程式碼，就能以程式方式完成。

本指南將一步步說明整個流程：從載入包含圖表與文字方塊的 Excel 活頁簿、設定匯出讓文字方塊與圖形保持可編輯，最後將結果儲存為 **PowerPoint** 檔案。完成後，你也會知道如何 **將 Excel 轉換為 PowerPoint**、**將 Excel 儲存為 PowerPoint**，甚至調整選項以因應特殊情況。

## 需要的條件

- **Aspose.Cells for .NET**（版本 23.10 以上）。這是讓轉換變得輕鬆的函式庫。
- **.NET 6+** 執行環境 – 任何近期的 SDK 都可。
- 一個簡易的 Excel 檔案（`ChartWithTextbox.xlsx`），內含至少一個圖表與一個文字方塊。
- Visual Studio 或你慣用的 IDE。

除 Aspose.Cells 之外不需要額外的 NuGet 套件，但具備基本的 C# 語法概念會更順利。

## 匯出圖表至 PowerPoint – 步驟說明

以下將解決方案拆解為多個易於跟隨的步驟。每一步都提供完整程式碼，並附上說明「為什麼」需要這麼做。

### 步驟 1：載入包含圖表的 Excel 活頁簿

首先必須將來源檔案載入記憶體。使用 Aspose.Cells 的 `Workbook` 會讀取整個試算表，包括圖表、影像與內嵌物件。

```csharp
using Aspose.Cells;

// Step 1: Load the Excel workbook that contains the chart with a textbox
Workbook workbook = new Workbook(@"C:\Samples\ChartWithTextbox.xlsx");

// Verify that the workbook actually contains a chart
if (workbook.Worksheets[0].Charts.Count == 0)
{
    throw new InvalidOperationException("No chart found in the first worksheet.");
}
```

*為什麼這很重要：* 若未正確指定路徑開啟活頁簿，會拋出 `FileNotFoundException`。這個簡單的檢查可避免之後匯出出空白投影片。

### 步驟 2：設定匯出選項以保留圖形可編輯

Aspose.Cells 允許你決定文字方塊、圖形，甚至圖表本身在匯出後是否保持 **可編輯**。將 `ExportTextBoxes` 與 `ExportShapes` 設為 `true`，即可將這些物件保留為原生 PowerPoint 元素，而非平面圖像。

```csharp
using Aspose.Cells.Drawing;

// Step 2: Set up presentation options to keep textboxes and shapes editable in the output
PresentationOptions presentationOptions = new PresentationOptions
{
    ExportTextBoxes = true, // Preserve editable textboxes
    ExportShapes    = true  // Preserve shapes such as the chart itself
};
```

*為什麼這很重要：* 若這些旗標保留預設值（`false`），最終投影片會只得到圖表的位圖，無法再編輯系列或更改標題。開啟兩個選項即可得到與手動繪製相同的 PowerPoint 圖表。

### 步驟 3：將 Excel 轉換為 PowerPoint 並儲存檔案

接著呼叫 `Save` 方法，傳入 `SaveFormat.Pptx` 列舉以及剛剛設定的選項。函式庫會負責將 Excel 圖表物件轉換成 PowerPoint 圖表形狀。

```csharp
// Step 3: Save the workbook as a PowerPoint presentation using the configured options
workbook.Save(@"C:\Samples\Result.pptx", SaveFormat.Pptx, presentationOptions);
```

*為什麼這很重要：* `Save` 會完成所有繁重工作——將 Excel 系列對映到 PowerPoint 系列、保留坐標軸格式、複製任何連結的文字方塊。執行完此行後，你會得到一個完整可編輯的 `.pptx` 檔案，隨時可在 Microsoft PowerPoint 開啟。

### 驗證結果

在 PowerPoint 中開啟 `Result.pptx`。你應該會看到投影片包含：

- 原始圖表，仍與資料連結（雙擊即可編輯系列）。
- Excel 工作表中的文字方塊，現在是原生 PowerPoint 文字方塊。
- 投影片版面自動選擇（通常是空白投影片）。

若發現遺漏的元素，請再次確認來源活頁簿確實有可見物件，且 `ExportTextBoxes` / `ExportShapes` 已設為 `true`。

### 將 Excel 轉換為 PowerPoint：處理多工作表

通常活頁簿會有多個工作表，各自擁有圖表。預設情況下 Aspose.Cells 會將 **所有** 工作表的 **所有** 圖表匯出為獨立投影片。若只需要部份圖表，可在儲存前先過濾：

```csharp
// Example: Export only charts from the first worksheet
Worksheet firstSheet = workbook.Worksheets[0];
foreach (Chart chart in firstSheet.Charts)
{
    chart.IsVisible = true; // Ensure visibility
}

// Hide charts from other sheets
for (int i = 1; i < workbook.Worksheets.Count; i++)
{
    foreach (Chart chart in workbook.Worksheets[i].Charts)
    {
        chart.IsVisible = false;
    }
}
```

*小技巧：* 將 `chart.IsVisible = false` 的成本比完全移除圖表低，且可在不修改來源檔的前提下切換是否匯入。

### 將 Excel 儲存為 PowerPoint – 自訂投影片尺寸

PowerPoint 預設投影片尺寸為 10 吋 × 5.63 吋。若圖表顯得擁擠，可透過 `PresentationOptions` 物件調整尺寸：

```csharp
presentationOptions.SlideSize = new SizeF(13.33f, 7.5f); // 16:9 widescreen
```

如此一來匯出的圖表會有更多呼吸空間，文字方塊也會保留原始版面配置。

### 如何將 Excel 轉換為 PPT：處理隱藏物件

隱藏的列、欄或圖形有時會不小心被匯入。可在儲存前先執行簡易清理：

```csharp
// Remove hidden rows/columns that might affect chart layout
foreach (Worksheet sheet in workbook.Worksheets)
{
    sheet.Cells.HideRows = false;
    sheet.Cells.HideColumns = false;
}
```

此步驟不是必須的，但可避免最終投影片出現意外的空白。

### 儲存活頁簿為 PPTX – 完整範例程式

以下提供一個可直接執行的 Console 程式，示範完整流程：

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing; // For SizeF

class ExportChartDemo
{
    static void Main()
    {
        // Load workbook (Step 1)
        string sourcePath = @"C:\Samples\ChartWithTextbox.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // Verify chart existence
        if (workbook.Worksheets[0].Charts.Count == 0)
        {
            Console.WriteLine("No chart found. Exiting.");
            return;
        }

        // Configure presentation options (Step 2)
        PresentationOptions options = new PresentationOptions
        {
            ExportTextBoxes = true,
            ExportShapes    = true,
            SlideSize       = new SizeF(13.33f, 7.5f) // optional widescreen
        };

        // Optional: export only first worksheet charts
        for (int i = 1; i < workbook.Worksheets.Count; i++)
        {
            foreach (Chart c in workbook.Worksheets[i].Charts)
                c.IsVisible = false;
        }

        // Save as PowerPoint (Step 3)
        string targetPath = @"C:\Samples\Result.pptx";
        workbook.Save(targetPath, SaveFormat.Pptx, options);

        Console.WriteLine($"Export complete! File saved to {targetPath}");
    }
}
```

執行此程式會產生 `Result.pptx`，內含可編輯的圖表與文字方塊，正是手動 **將活頁簿儲存為 pptx** 時的預期結果。

![匯出圖表至 PowerPoint 範例](/images/export-chart-to-powerpoint.png "匯出圖表至 PowerPoint – 可編輯投影片")

## 常見問題與特殊情況

**如果 Excel 檔案的圖表使用了外部資料來源，會怎樣？**  
Aspose.Cells 會將*目前*的資料值複製到 PowerPoint 圖表中，**不會**保留外部連結，因為 PowerPoint 無法以相同方式引用 Excel 資料連接。若需要即時更新，可考慮將原始 Excel 檔案以 OLE 物件嵌入 PPTX。

**能否匯出使用自訂佈景主題的圖表？**  
可以。函式庫會嘗試將 Excel 佈景主題顏色對映到 PowerPoint 佈景主題槽位。對於極度自訂的調色盤，可能需要在匯出後使用 PowerPoint API（例如 Aspose.Slides）自行調整顏色。

**圖表數量有上限嗎？**  
實際上沒有——Aspose.Cells 以串流方式處理資料，即使活頁簿內有數十個圖表也能匯出，只是產生的 PPTX 檔案大小會線性增長。

**使用 Aspose.Cells 是否需要授權？**  
免費評估版可用，但會在第一張投影片加上浮水印。正式上線時請取得正式授權，以移除浮水印並解鎖完整效能。

## 重點回顧

我們說明了如何使用 C# **匯出圖表至 PowerPoint**，展示了載入 Excel 活頁簿、設定 `PresentationOptions` 以保留文字方塊與圖形可編輯，最後儲存為 `.pptx` 的完整程式碼。你也學會了 **將 Excel 轉換為 PowerPoint**、**將 Excel 儲存為 PowerPoint**，以及如何回答「**如何將 Excel 轉換為 ppt**」的問題，並提供可直接執行的範例。

## 往後可以怎麼做？

- **將活頁簿儲存為 PPTX** 並產生多張投影片：遍歷每個工作表，對每張工作表呼叫帶有 `PresentationOptions` 的 `Save`。
- 若需進一步程式化修改產生的 PPTX（加入轉場、講者備註等），可探索 **Aspose.Slides**。
- 嘗試匯出 **樞紐分析圖表** 或 **3D 圖表**——相同選項仍適用，只是匯出後可能需要微調坐標軸格式。

若在實作過程中遇到問題，歡迎在下方留言或查閱官方 Aspose.Cells 文件以取得最新 API 變更資訊。祝開發順利，玩得開心，讓 Excel 圖表只需幾行 C# 就能變身為精美的 PowerPoint 投影片！

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}