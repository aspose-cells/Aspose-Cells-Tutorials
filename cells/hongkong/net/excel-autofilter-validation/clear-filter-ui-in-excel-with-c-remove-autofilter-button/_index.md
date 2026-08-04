---
category: general
date: 2026-02-09
description: 使用 C# 移除 AutoFilter 按鈕，清除 Excel 中的篩選介面。學習如何隱藏篩選按鈕、顯示標題列，並保持工作表整潔。
draft: false
keywords:
- clear filter UI
- remove autofilter excel
- how to remove autofilter
- show header row
- hide filter button
language: zh-hant
og_description: 使用 C# 清除 Excel 篩選介面。本指南說明如何隱藏篩選按鈕、顯示標題列，並保持工作表整潔。
og_title: 使用 C# 清除 Excel 篩選介面 – 移除自動篩選按鈕
tags:
- excel
- csharp
- epplus
- automation
title: 使用 C# 清除 Excel 篩選使用者介面 – 移除 AutoFilter 按鈕
url: /zh-hant/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中使用 C# 清除篩選 UI – 移除 AutoFilter 按鈕

有沒有曾經需要在 Excel 工作表中 **清除篩選 UI**，卻不確定哪一行程式碼實際上會隱藏那個小下拉箭頭？你並不是唯一遇到這個問題的人。當你將報表發送給不需要變更檢視的最終使用者時，篩選按鈕可能會顯得突兀。  

在本教學中，我們將逐步說明一個完整且可執行的範例，**從資料表中移除 AutoFilter 按鈕**，確保標題列仍保持可見，甚至還會提及如何永久 *隱藏篩選按鈕*。完成後，你將清楚了解 **如何在 C# 中移除 AutoFilter**，以及每個步驟背後的原因。

## 需要的環境

- .NET 6+（或 .NET Framework 4.7.2+） – 任何近期的執行環境皆可。
- **EPPlus** NuGet 套件（版本 6.x 或更新） – 它提供 `ExcelWorksheet`、`ExcelTable` 等類別。
- 一個簡單的 Excel 檔案，內含名為 **SalesTable** 的資料表（可輕鬆點幾下建立）。

就這樣。無需 COM interop，亦無額外 DLL，只需要少量的 `using` 陳述式與幾行程式碼。

## 清除篩選 UI：移除 AutoFilter 按鈕

解決方案的核心在於三行簡短的敘述。讓我們逐一說明，以便你了解 *為何* 需要這些步驟，而不僅是 *它們做了什麼*。

### 步驟 1 – 取得資料表的參考

```csharp
// Step 1: Get a reference to the "SalesTable" in the first worksheet
ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
```

為何這很重要：EPPlus 以 **資料表**（`ExcelTable`）而非原始儲存格範圍運作。取得資料表物件後，我們即可存取 `AutoFilter` 屬性，該屬性控制工作表上可見的 UI 元件。如果直接操作工作表，只會影響資料值，無法處理篩選按鈕。

### 步驟 2 – 移除 AutoFilter 按鈕所在的列

```csharp
// Step 2: Remove the AutoFilter button row (clears any applied filter UI)
salesTable.AutoFilter = null;
```

將 `AutoFilter` 設為 `null` 會告訴 EPPlus 刪除底層的篩選列。這就是大多數開發者在詢問「**如何移除 autofilter**」時尋找的 *清除篩選 UI* 操作。這是一行程式碼的簡潔做法，適用於 EPPlus 支援的任何 Excel 版本。

### 步驟 3 – 保持標題列可見

```csharp
// Step 3: Ensure the header row remains visible after removing the filter
salesTable.ShowHeader = true;
```

當你移除篩選 UI 時，若資料表的 `ShowHeader` 標誌為 false，Excel 可能會隱藏標題列。透過明確將其設為 `true`，我們確保欄位標題仍顯示在畫面上——這是讓最終報表更精緻的細微但重要的細節。

### 完整、可執行的範例

以下是一個最小化的主控台應用程式範例，會開啟既有活頁簿、執行上述三個步驟，並儲存結果。直接複製貼上，按下 **F5**，即可看到篩選按鈕消失。

```csharp
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

class Program
{
    static void Main()
    {
        // EPPlus requires a license context for non‑commercial use.
        ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

        // 1️⃣ Load the workbook (replace with your own path)
        var filePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
        if (!File.Exists(filePath))
        {
            Console.WriteLine($"File not found: {filePath}");
            return;
        }

        using var package = new ExcelPackage(new FileInfo(filePath));

        // 2️⃣ Get a reference to the table named "SalesTable"
        ExcelTable salesTable = package.Workbook.Worksheets[0].Tables["SalesTable"];
        if (salesTable == null)
        {
            Console.WriteLine("Table 'SalesTable' not found in the first worksheet.");
            return;
        }

        // 3️⃣ Remove the AutoFilter button (clear filter UI)
        salesTable.AutoFilter = null;

        // 4️⃣ Ensure the header row stays visible (show header row)
        salesTable.ShowHeader = true;

        // 5️⃣ Save the changes to a new file so you don’t overwrite the original
        var outputPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
        package.SaveAs(new FileInfo(outputPath));

        Console.WriteLine($"Filter button removed. Saved to {outputPath}");
    }
}
```

**預期結果：** 開啟 *SalesReport_NoFilter.xlsx* 後，篩選箭頭已消失，欄位標題仍然保留。再也不會出現「點擊篩選」的 UI 雜訊。

> **專業提示：** 若有 **多個資料表** 且想要為全部隱藏篩選按鈕，可遍歷 `worksheet.Tables`，在迴圈內套用相同的三行程式碼。

## 如何在 Excel 中使用 C# 移除 AutoFilter – 深入探討

你可能會想，「如果活頁簿已經套用篩選呢？將 `AutoFilter = null` 也會清除已篩選的列嗎？」答案是 **是**。EPPlus 會同時清除 UI 與底層的篩選條件，讓資料回復原始順序。  

如果你只想 *隱藏* 按鈕但保留篩選功能，可改為將 `AutoFilter` 屬性設定為 **新的空白篩選**：

```csharp
salesTable.AutoFilter = new ExcelAutoFilter(); // hides button, retains filter logic
```

此變體在你想要 *隱藏篩選按鈕* 以獲得更精緻外觀，同時仍允許進階使用者透過 VBA 或功能區切換篩選時相當實用。

### 邊緣情況：沒有標題列的資料表

某些舊版報表使用純儲存格範圍而非資料表。在此情況下，EPPlus 不會提供 `ExcelTable` 物件，以上程式碼會拋出例外。解決方法是先 **將範圍轉換為資料表**：

```csharp
var range = worksheet.Cells["A1:D100"];
var table = worksheet.Tables.Add(range, "TempTable");
table.ShowHeader = true;    // ensure header is visible
table.AutoFilter = null;    // clear filter UI
```

現在，即使是最初沒有正式資料表的範圍，你也已 *移除 autofilter excel* 風格的 UI。

## 隱藏篩選按鈕後顯示標題列 – 為何重要

常見的抱怨是隱藏篩選 UI 後，標題列有時會消失，尤其是活頁簿最初建立時已將「隱藏標題」開啟。透過明確設定 `salesTable.ShowHeader = true;` 可避免此情況。  

如果你需要 **隱藏篩選按鈕** 同時保持標題列隱藏（例如產生原始資料匯出），只要在清除篩選後將 `salesTable.ShowHeader = false;` 即可。程式碼前後對稱，便於根據設定旗標切換。

## 隱藏篩選按鈕 – 實用技巧與陷阱

- **版本相容性：** EPPlus 6+ 只支援 `.xlsx` 檔案。若處理較舊的 `.xls` 格式，需改用其他函式庫（例如 NPOI），因為 *清除篩選 UI* 的 API 不存在。
- **效能：** 僅為隱藏一個按鈕而載入大型活頁簿可能較慢。可考慮使用 `ExcelPackage.Load(stream, true)` 以 **唯讀** 模式開啟，套用變更後再儲存。
- **測試：** 首次執行時務必手動驗證輸出檔案。自動化 UI 測試可確認篩選箭頭確實消失（`worksheet.Tables[0].AutoFilter == null`）。
- **授權：** EPPlus 從第 5 版起採用雙授權模式。商業專案需購買授權或改用其他函式庫。

## 完整原始檔案供複製貼上

以下即為可直接放入新主控台專案的完整檔案。沒有隱藏的相依性，全部自包含。

```csharp
// File: Program.cs
using System;
using System.IO;
using OfficeOpenXml;
using OfficeOpenXml.Table;

namespace ExcelFilterCleaner
{
    class Program
    {
        static void Main()
        {
            // License context – required for EPPlus 5+
            ExcelPackage.LicenseContext = LicenseContext.NonCommercial;

            // Path to the original workbook (adjust as needed)
            string sourcePath = Path.Combine(Environment.CurrentDirectory, "SalesReport.xlsx");
            if (!File.Exists(sourcePath))
            {
                Console.WriteLine($"Source file not found: {sourcePath}");
                return;
            }

            // Load workbook
            using var package = new ExcelPackage(new FileInfo(sourcePath));

            // Assume the first worksheet contains the table
            var worksheet = package.Workbook.Worksheets[0];
            const string tableName = "SalesTable";

            // Grab the table; abort if missing
            var salesTable = worksheet.Tables[tableName];
            if (salesTable == null)
            {
                Console.WriteLine($"Table '{tableName}' not found.");
                return;
            }

            // ---- Clear filter UI ----
            salesTable.AutoFilter = null;   // removes the filter button row
            salesTable.ShowHeader = true;   // guarantees the header row stays visible

            // Save to a new file so the original stays untouched
            string destPath = Path.Combine(Environment.CurrentDirectory, "SalesReport_NoFilter.xlsx");
            package.SaveAs(new FileInfo(destPath));

            Console.WriteLine($"Successfully cleared filter UI. Output: {destPath}");
        }
    }
}
```

在建置之前執行 `dotnet add package EPPlus --version 6.0.8`（或最新版本），即可得到可供發佈的乾淨工作表。

## 結論

我們剛剛示範了如何使用 C# 在 Excel 活頁簿中 **移除 AutoFilter** 以及 **清除篩選 UI**。三行核心程式碼（`AutoFilter = null;`、`ShowHeader = true;`）負責主要工作，而周邊的樣板程式碼則讓解決方案 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}