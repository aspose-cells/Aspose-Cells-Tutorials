---
category: general
date: 2026-05-04
description: 使用 C# 匯出工作表範圍並自訂格式。學習如何匯出 Excel 範圍以及如何在幾個簡單步驟中自訂儲存格匯出。
draft: false
keywords:
- export worksheet range
- how to export excel range
- how to customize cell export
- C# Excel export
- worksheet export options
language: zh-hant
og_description: 使用 C# 匯出工作表範圍。本指南示範如何快速且可靠地匯出 Excel 範圍並自訂儲存格匯出。
og_title: 在 C# 中匯出工作表範圍 – 完整程式設計指南
tags:
- C#
- Excel
- Data Export
title: 在 C# 中匯出工作表範圍 – 完整程式設計指南
url: /zh-hant/net/excel-data-export-retrieval/export-worksheet-range-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中匯出工作表範圍 – 完整程式指南

是否曾需要 **export worksheet range**，但預設輸出並非你想要的？你並非唯一遇到這種情況的人——許多開發者在嘗試將一段儲存格匯出為 CSV 或 JSON 檔案時，都會卡在這裡。好消息是？只要幾行 C# 程式碼，你不僅可以 **export excel range**，還能 **customize cell export**，以符合任何下游格式。

在本教學中，我們將示範一個實務情境：從 Excel 活頁簿中取得 *A1:D10* 的儲存格，將每個值轉換為帶括號的字串，並將結果寫入檔案。完成後，你將清楚了解 **how to export worksheet range**，並能完整掌控每個儲存格的呈現方式，同時獲得一些日後可能遇到的特殊情況的技巧。

## 需要的條件

- .NET 6 或更新版本（此程式碼亦相容於 .NET Framework 4.7+）  
- **GemBox.Spreadsheet** NuGet 套件（或任何提供 `ExportTableOptions` 的函式庫；此範例 API 取自 GemBox）  
- 對 C# 語法有基本了解 – 不需高深技巧，只要會使用一般的 `using` 陳述式與建立物件即可  

如果你已具備上述條件，即可開始動手。

## 第一步：設定匯出選項 – 主要控制點  

首先，你需要建立一個 `ExportTableOptions` 實例，並指示它將每個儲存格視為字串。這是 **how to export excel range** 的基礎，同時確保資料類型保持一致。

```csharp
using GemBox.Spreadsheet;

public class WorksheetExporter
{
    public void ExportRange(string sourcePath, string destinationPath)
    {
        // Load the workbook.
        var workbook = ExcelFile.Load(sourcePath);
        var worksheet = workbook.Worksheets[0]; // assume first sheet

        // Step 1: Create export options and enable string export.
        var exportOptions = new ExportTableOptions
        {
            ExportAsString = true // forces every cell to be exported as text
        };
```

*為何要強制字串匯出？*  
當你之後自訂每個儲存格時，會加入括號或其他符號。將所有內容保持為字串可避免類型轉換的意外（例如日期變成序號）。

## 第二步：掛接 CellExport 事件 – 自訂每個儲存格  

現在進入有趣的部分：**how to customize cell export**。GemBox 會為每個即將寫入的儲存格觸發 `CellExport` 事件。透過處理此事件，你可以將值包在括號內、加上前綴，甚至完全跳過某個儲存格。

```csharp
        // Step 2: Customize each cell's exported value.
        exportOptions.CellExport += (sender, e) =>
        {
            // e.Value holds the original cell content.
            // We'll wrap it in square brackets.
            e.Value = $"[{e.Value}]";
        };
```

*小技巧：* 若只想修改數值儲存格，請在套用括號前檢查 `e.Value.GetType()`。這個小小的防護可以避免不小心破壞標題文字。

## 第三步：匯出目標範圍 – 核心動作  

設定好選項後，呼叫 `ExportTable`。此方法接受已載入的活頁簿、欲匯出的範圍位址，以及剛剛配置好的選項。

```csharp
        // Step 3: Export the range A1:D10 using the configured options.
        worksheet.ExportTable(workbook, "A1:D10", exportOptions, destinationPath);
    }
}
```

我們使用的多載版本會直接寫入檔案（預設為 CSV）。如果你想要在記憶體中取得字串，只需將最後一個參數換成 `StringWriter`，之後再讀取結果即可。

### 完整範例

以下是一個獨立的 Console 應用程式範例，你可以直接貼到新專案中立即執行（只需自行替換檔案路徑）。

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License key (free version works with limited rows/columns).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        var exporter = new WorksheetExporter();
        exporter.ExportRange(
            sourcePath: @"C:\Temp\Sample.xlsx",
            destinationPath: @"C:\Temp\ExportedRange.csv");

        Console.WriteLine("Export completed. Check C:\\Temp\\ExportedRange.csv");
    }
}
```

**預期輸出（CSV 片段）：**

```
[Header1],[Header2],[Header3],[Header4]
[123],[456],[789],[012]
[ABC],[DEF],[GHI],[JKL]
...
```

從 *A1* 到 *D10* 的每個儲存格現在都被方括號包住，正如我們在 `CellExport` 處理程序中所定義的那樣。

## 處理常見的邊緣情況  

### 1. 空儲存格  

如果儲存格為空，`e.Value` 會是 `null`。使用字串插值格式化它會拋出例外。請做好防護：

```csharp
exportOptions.CellExport += (s, e) =>
{
    var raw = e.Value?.ToString() ?? string.Empty;
    e.Value = $"[{raw}]";
};
```

### 2. 大範圍  

匯出數百萬列可能會觸及記憶體限制。在此情況下，請以串流方式輸出，而非一次將整個活頁簿載入記憶體：

```csharp
using (var writer = new StreamWriter(destinationPath))
{
    worksheet.ExportTable(workbook, "A1:D1000000", exportOptions, writer);
}
```

### 3. 不同的分隔符  

CSV 並非唯一可能需要的格式。可透過調整 `ExportTableOptions.CsvSeparator` 來變更分隔符號：

```csharp
exportOptions.CsvSeparator = '\t'; // Tab‑delimited
```

## 常見問與答  

**Q: 這能否支援由 Excel 365 建立的 .xlsx 檔案？**  
**A:** 絕對可以。GemBox 能直接讀取現代的 OpenXML 格式，無需額外設定。

**Q: 我能一次匯出多個不相連的範圍嗎？**  
**A:** 無法透過單一 `ExportTable` 呼叫直接完成。必須對每個範圍字串（例如 `"A1:D10"`、`"F1:H5"` 等）迴圈處理，然後自行合併輸出。

**Q: 如果需要對每一欄套用不同的格式該怎麼辦？**  
**A:** 在 `CellExport` 處理程序中，你可以取得 `e.ColumnIndex`。使用 `switch` 陳述式即可對特定欄位套用相應的邏輯。

## 總結  

我們已說明 **how to export worksheet range**，並能完整控制每個儲存格的外觀；示範了使用 `ExportTableOptions` 的 **how to export excel range**；以及透過 `CellExport` 事件展示 **how to customize cell export**。完整解決方案僅需數十行 C# 程式碼，卻足以應付正式環境的需求。

接下來的步驟？可以嘗試將方括號改為 JSON 友善的格式，或實驗跳過隱藏列的條件邏輯。你也可以探索直接匯出至 `MemoryStream` 以供 Web API 回應使用——不需要暫存檔案。

如果你已跟著操作完畢，現在就擁有一套穩固且可重複使用的模式，能夠依需求精確匯出任何工作表範圍。祝開發順利，若遇到問題，歡迎留下評論！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}