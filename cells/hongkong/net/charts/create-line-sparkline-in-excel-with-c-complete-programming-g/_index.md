---
category: general
date: 2026-06-30
description: 快速使用 C# 在 Excel 中建立折線迷你圖。學習如何新增迷你圖、使用 C# 建立 Excel 活頁簿，以及在幾個步驟內將迷你圖加入儲存格。
draft: false
keywords:
- create line sparkline
- how to add sparkline
- add line sparkline
- create excel workbook c#
- add sparkline to cell
language: zh-hant
og_description: 使用 C# 在 Excel 中建立線條迷你圖。本教學示範如何加入迷你圖、使用 C# 建立 Excel 工作簿，並將迷你圖嵌入儲存格中。
og_title: 使用 C# 在 Excel 中建立折線迷你圖 – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create line sparkline in Excel with C# quickly. Learn how to add sparkline,
    create Excel workbook C#, and add sparkline to cell in a few steps.
  headline: Create line sparkline in Excel with C# – Complete Programming Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: 使用 C# 在 Excel 中建立折線迷你圖 – 完整程式設計指南
url: /zh-hant/net/charts/create-line-sparkline-in-excel-with-c-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中使用 C# 建立折線 Sparkline – 完整程式指南

有沒有想過如何在 Excel 檔案中使用 C# **建立折線 Sparkline**？你並不是唯一的開發者——大家常問：「如何在不手動開啟 Excel 的情況下，將 Sparkline 加入報表？」好消息是，只要幾行程式碼，就能在活頁簿內直接產生精緻的折線 Sparkline，完全不需要 UI。

在本教學中，我們將逐步說明您需要了解的全部內容：從 **create Excel workbook C#** 基礎、資料填充，到 **add line sparkline** 與 **add sparkline to cell** 的具體步驟。完成後，您將擁有一個可直接使用的 *.xlsx* 檔案，即可一眼看出每月銷售趨勢。內容精簡實用，直接可執行的解決方案。

---

## 您將建立的內容

- 一個全新的 Excel 活頁簿，檔名為 *KPI_Sparklines.xlsx*  
- 一個名為 **KPI** 的工作表，內含範例銷售數據  
- 一個放在儲存格 **D2**、參照資料範圍 **B2:B13** 的 **line sparkline**  
- 基本格式設定（顏色、線條粗細）讓 Sparkline 更醒目  

先決條件？只需要 .NET SDK（3.1 以上或 .NET 6）以及免費的 Aspose.Cells for .NET 函式庫（可透過 NuGet 取得）。如果您從未使用過 Aspose.Cells，請把它想像成一個強大的 Excel 引擎，您可以直接在程式碼中呼叫——不需要 COM 互操作，也不需要安裝 Excel。

![Create line sparkline in Excel using C#](https://example.com/images/create-line-sparkline.png "使用 C# 在 Excel 中建立折線 Sparkline")
*圖片說明：使用 C# 建立 Excel 折線 Sparkline 的程式範例*

## 步驟 1：**Create Excel workbook C#** – 設定檔案與工作表

首先，我們需要一個活頁簿物件以及一個用來放置資料的工作表。這是任何 Excel 自動化的基礎，無論之後要 **add line sparkline** 或是寫入公式，都離不開它。

```csharp
using Aspose.Cells;
using System.Drawing;

// Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0) and give it a meaningful name
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Name = "KPI";   // “KPI” will hold our key performance indicators
```

> **為什麼重要：** `Workbook` 類別代表整個檔案，而 `Worksheet` 則是行、列以及最終的 Sparkline 所繪製的畫布。提前命名工作表可讓檔案保持整潔且具備自說明性。

## 步驟 2：填充資料 – Sparkline 的來源範圍

Sparkline 需要資料才能繪製。這裡我們模擬 12 個月的銷售數字。您可以從資料庫取得這些資料，但為了說明簡潔，我們直接在程式中產生。

```csharp
// Fill column B (index 1) with monthly sales numbers
for (int month = 0; month < 12; month++)
{
    // Example pattern: start at 5,000 and increase by 750 each month
    worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
}
```

> **小技巧：** `PutValue` 會自動偵測資料類型，無需自行轉型為 `double` 或 `int`。若日後需要格式化儲存格（貨幣、千位分隔符），可再套用 `Style` 物件。

## 步驟 3：**Create line sparkline** – 在特定儲存格加入 Sparkline

現在重頭戲登場：**line sparkline**。Aspose.Cells 會將 Sparkline 分組，因此我們先建立類型為 `Line` 的 `SparklineGroup`，再指定它的顯示位置。

```csharp
// Add a new SparklineGroup of type Line
int groupIndex = worksheet.SparklineGroups.Add(SparklineType.Line);
SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIndex];

// Add a sparkline that lives in D2 (row 1, column 3) and reads data from B2:B13
// Parameters: firstRow, firstColumn, lastRow, lastColumn, firstDataRow, lastDataRow
sparklineGroup.Add(1, 3, 1, 3, 1, 12);   // D2 ↔ B2:B13
```

> **運作方式：**  
> - `firstRow/firstColumn` 與 `lastRow/lastColumn` 定義 *目標儲存格*（Sparkline 顯示的位置）。  
> - `firstDataRow/lastDataRow` 指向資料來源範圍。  
> 由於我們使用的是 **line sparkline**，視覺上會是一條簡單的細線，呈現數字的走勢。

### 可選：使用自訂樣式 **How to add sparkline**

如果想讓 Sparkline 更突出，可調整以下屬性：

```csharp
sparklineGroup.LineWeight = 1.0;               // Thickness of the line
sparklineGroup.SeriesColor = Color.DarkBlue;  // Color of the sparkline line
sparklineGroup.ShowMarkers = true;             // Show data markers (optional)
sparklineGroup.MarkerColor = Color.OrangeRed;  // Marker color
```

> **為什麼要樣式化？** 深藍色線條配上白色背景舒適視覺，且標記點能快速提示各個資料點——在簡報時相當實用。

## 步驟 4：儲存活頁簿 – 驗證結果

Sparkline 已就位後，只需將檔案寫入磁碟。選擇一個您有寫入權限的資料夾；範例使用的是佔位路徑，請自行替換。

```csharp
// Save the workbook as an .xlsx file
string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
workbook.Save(outputPath);
```

> **驗證方式：** 在 Excel（或任何支援 .xlsx 的檢視器）中開啟產生的檔案。您應該會在儲存格 **D2** 看到一條 **line sparkline**，其走勢與 B 欄遞增的銷售數字相符。將滑鼠移到 Sparkline 上會顯示包含底層數值的工具提示。

## 步驟 5：在 **add sparkline to cell** 時常見的陷阱

即使是簡單的範例，也可能讓新手卡關。以下列出幾個需要留意的地方：

| 問題 | 為什麼會發生 | 解決方式 |
|------|--------------|----------|
| 錯誤的儲存格座標 | Sparkline 目標使用零基礎的欄索引，但列索引為一基礎。 | 記得 `Cells[row, column]` 中 `row` 與 `column` 都是零基礎。在 `SparklineGroup.Add` 中，列與欄是 **1‑基礎**。 |
| 未顯示資料 | 來源範圍為空或包含非數值。 | 確保範圍（例如 `B2:B13`）內有數字。使用 `PutValue` 並傳入數值型別。 |
| 儲存後 Sparkline 消失 | 函式庫版本不匹配或缺少授權。 | 使用最新的 Aspose.Cells 套件，若超過評估限制，請提供有效授權。 |
| 格式未套用 | 在加入 Sparkline 前已變更樣式。 | 如上例，先建立群組後再設定樣式 **之後**。 |

## 完整原始碼 – 一次貼上即可

以下為完整、可直接執行的程式。將它貼到新的 Console 專案中，加入 Aspose.Cells NuGet 套件，然後按 **F5**。

```csharp
using Aspose.Cells;
using System.Drawing;

namespace SparklineDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create Excel workbook C#
            // -------------------------------------------------
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "KPI";

            // -------------------------------------------------
            // Step 2: Populate monthly sales data (B2:B13)
            // -------------------------------------------------
            for (int month = 0; month < 12; month++)
            {
                worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
            }

            // -------------------------------------------------
            // Step 3: Create line sparkline and add it to D2
            // -------------------------------------------------
            int groupIdx = worksheet.SparklineGroups.Add(SparklineType.Line);
            SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIdx];
            sparklineGroup.Add(1, 3, 1, 3, 1, 12); // D2 ↔ B2:B13

            // -------------------------------------------------
            // Step 4: Optional formatting (how to add sparkline with style)
            // -------------------------------------------------
            sparklineGroup.LineWeight = 1.0;
            sparklineGroup.SeriesColor = Color.DarkBlue;
            sparklineGroup.ShowMarkers = true;
            sparklineGroup.MarkerColor = Color.OrangeRed;

            // -------------------------------------------------
            // Step 5: Save the workbook
            // -------------------------------------------------
            string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
            workbook.Save(outputPath);

            System.Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**預期輸出：** 開啟 *KPI_Sparklines.xlsx* 後，B 欄會列出十二個數字（5,000 → 13,250），而儲存格 **D2** 會顯示一條平滑的深藍色折線 Sparkline，呈現持續上升的趨勢。若您啟用了 `ShowMarkers`，標記會以細小的橙紅點顯示。

## 接下來？擴展您的 Sparkline 技能

既然您已熟悉使用 Aspose.Cells **create line sparkline**，不妨進一步探索以下相關主題：

- **Add column sparkline** – 非常適合顯示堆疊資料。  
- **Create multi‑sparkline groups** on the same sheet for side‑by‑side comparison. – 在同一工作表上建立多個 Sparkline 群組，以便並排比較。  
- **Export to PDF** while preserving sparklines (Aspose.Cells supports PDF conversion). – 匯出為 PDF 同時保留 Sparkline（Aspose.Cells 支援 PDF 轉換）。  
- **Dynamic data sources** – 從 SQL 資料庫取得真實銷售數據，而非硬編碼值。  

上述每項皆以相同的核心概念為基礎：**create Excel workbook C#**、填充資料，並以所需樣式 **add sparkline to cell**。

### TL;DR

我們示範了如何使用 C# 在 Excel 活頁簿中 **create line sparkline**。步驟——*建立活頁簿、填充資料、加入 Sparkline、樣式化並儲存*——全部封裝在一個獨立程式中。您可以自由調整顏色、線條粗細或資料來源範圍，以符合報表需求。

有任何想法想分享嗎？歡迎在下方留言，祝編程愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，並在自己的專案中探索其他實作方式。

- [Excel 自動化：建立活頁簿並使用 Aspose.Cells for .NET 新增 ListBox](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Excel 自動化：建立活頁簿並新增 ListBox](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Excel 自動化：建立活頁簿並新增 ListBox](/cells/french/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}