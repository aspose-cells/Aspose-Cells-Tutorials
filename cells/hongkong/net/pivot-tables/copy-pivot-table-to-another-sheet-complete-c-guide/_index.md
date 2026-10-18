---
category: general
date: 2026-06-27
description: 使用 Aspose.Cells 在 C# 中將樞紐分析表複製到另一個工作表。逐步學習如何保留樞紐分析表的資料與格式。
draft: false
keywords:
- copy pivot table to another sheet
- Aspose.Cells copy pivot
- Excel pivot duplication
- preserve pivot formatting
- copy range with pivot
language: zh-hant
og_description: 在 C# 中使用 Aspose.Cells 複製樞紐分析表至另一個工作表。本教學將精確說明如何在保持其格式完整的情況下複製樞紐分析表。
og_title: 將樞紐分析表複製至其他工作表 – 完整 C# 指南
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Copy pivot table to another sheet in C# using Aspose.Cells. Learn step‑by‑step
    how to preserve pivot data and formatting.
  headline: Copy Pivot Table to Another Sheet – Complete C# Guide
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: 將樞紐分析表複製到其他工作表 – 完整 C# 指南
url: /zh-hant/net/pivot-tables/copy-pivot-table-to-another-sheet-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將樞紐分析表複製到另一工作表 – 完整 C# 指南

是否曾需要**將樞紐分析表複製到另一工作表**，卻擔心會失去切片器、計算欄位或格式？您並不孤單。許多開發人員在自動化 Excel 報表時都會遇到這個問題，且確實令人沮喪。在本指南中，我們將逐步說明一個乾淨、端對端的解決方案，**完整保留樞紐分析表**的原始樣貌。

我們將使用 **Aspose.Cells for .NET**，這是一個強大的函式庫，可讓您在不開啟 Excel 本身的情況下操作 Excel 檔案。完成本教學後，您將擁有一段可直接執行的 C# 程式碼片段，能將樞紐分析表從一個工作表複製到另一個工作表，同時保留所有底層資料連結。

## 本教學涵蓋內容

- 設定 .NET 專案並加入 Aspose.Cells NuGet 套件。  
- 載入已包含樞紐分析表的現有活頁簿。  
- 定義來源範圍（原始樞紐）以及不同工作表上的目標範圍。  
- 使用 `CopyOptions` 在複製時**保留樞紐分析表**。  
- 儲存結果並驗證樞紐分析表在新位置是否正常運作。  

不需外部工具、手動複製貼上，也沒有隱藏的魔法——只要簡單直接的程式碼，您即可將其放入任何 C# 主控台應用程式或服務中。

> **為何您應該在意：** 自動化樞紐分析表的複製可節省數小時的手動工作，尤其在每晚的報表管線中，數十本活頁簿需要在多個工作表上擁有相同的樞紐結構。

---

## 步驟 1：設定專案並加入 Aspose.Cells

首先，若尚未建立，請建立一個新的 .NET 主控台專案：

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
```

接著加入 Aspose.Cells 套件：

```bash
dotnet add package Aspose.Cells
```

> **專業提示：** 使用最新的穩定版（截至 2026 年 6 月 v23.12）。此版本已修正 `CopyPivotTable` 的相關問題。

## 步驟 2：載入活頁簿並存取工作表

開啟包含來源樞紐分析表的活頁簿。在大多數實務情境中，檔案位於共享磁碟上，但此示範假設它位於名為 `YOUR_DIRECTORY` 的本機資料夾中。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook containing the source pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Step 2: Access the first worksheet (source sheet)
        Worksheet sourceSheet = workbook.Worksheets[0];

        // We'll also create (or reference) a destination sheet
        Worksheet destSheet = workbook.Worksheets.Add("CopyDestination");
```

此處我們建立一個名為 **CopyDestination** 的新工作表，作為放置樞紐分析表的目的地。若您已經有目標工作表，只需依索引或名稱取得即可。

## 步驟 3：定義來源與目標範圍

樞紐分析表位於一個矩形儲存格區塊內。您必須告訴 Aspose.Cells 要複製哪個區塊。在此範例中，樞紐分析表佔用第 0‑20 行與第 0‑10 列（以零為基礎的索引）。

```csharp
        // Step 3: Define the source range that includes the pivot table (rows 0‑20, columns 0‑10)
        CellArea sourceRange = new CellArea(0, 0, 20, 10);

        // Step 4: Define the destination start cell (row 30, column 0) on the destination sheet
        // and calculate the target area size to match the source dimensions
        CellArea destinationRange = new CellArea(
            30,                                 // start row on destination sheet
            0,                                  // start column
            30 + sourceRange.RowCount - 1,     // end row (same height as source)
            sourceRange.ColumnCount - 1        // end column (same width as source)
        );
```

請注意，我們動態計算結束行與列。如此一來，即使之後變更來源範圍大小，目標範圍也會自動調整。

## 步驟 4：執行複製並保留樞紐分析表

現在魔法發生了。透過傳入 `CopyOptions` 物件並設定 `CopyPivotTable = true`，Aspose.Cells 會保留樞紐分析表的定義不變。

```csharp
        // Step 5: Copy the range, preserving the pivot table
        destSheet.Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTable = true }
        );
```

在底層，Aspose.Cells 會重新建立樞紐快取、刷新資料來源參考，並重新套用所有格式。這就是您一直在尋找的 **Excel 樞紐分析表複製**。

## 步驟 5：儲存並驗證結果

最後，將活頁簿寫回磁碟。您可以透過另存新檔的方式，保持原始檔案不被修改。

```csharp
        // Step 6: Save the workbook with the copied pivot table
        workbook.Save("YOUR_DIRECTORY/copy-pivot.xlsx");

        // Optional: open the file automatically (Windows only)
        System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
        {
            FileName = "YOUR_DIRECTORY/copy-pivot.xlsx",
            UseShellExecute = true
        });
    }
}
```

開啟產生的 `copy-pivot.xlsx`，您會看到樞紐分析表已在 **CopyDestination** 工作表上完整複製，包含切片器、計算欄位與格式。底層資料來源仍指向原始表格，刷新功能如同以前一樣正常。

> **如果來源樞紐分析表跨越動態範圍該怎麼辦？**  
> 使用 `Worksheet.PivotTables[0].CacheDefinition.SourceData` 取得實際範圍，然後根據該資訊建立 `sourceRange`。此方法可處理行或列隨時間擴展的情況。

## 加分項：在多次複製中保留樞紐格式

有時預設的複製會遺失條件格式或自訂數字格式。為避免此情況，可擴充 `CopyOptions`：

```csharp
        var options = new CopyOptions
        {
            CopyPivotTable = true,
            CopyFormatting = true,      // copies cell styles, colors, fonts
            CopyConditionalFormatting = true
        };
        destSheet.Cells.CopyRange(sourceRange, destinationRange, options);
```

啟用 `CopyFormatting` 可確保 **保留樞紐格式** 的需求得到滿足，讓您得到像素級完美的複製品。

## 預期輸出

執行程式時，主控台將靜默結束（除非您加入日誌）。開啟 `copy-pivot.xlsx` 應會看到：

- Sheet 1：原始資料與樞紐分析表保持不變。  
- **CopyDestination**：樞紐分析表的完整副本，起始於第 31 行（因為 Excel UI 中的行號是從 1 開始）。  
- 所有切片器與篩選器皆可正常使用；點擊「刷新」會同時更新兩個樞紐分析表。

## 結論

我們剛剛示範了如何使用 Aspose.Cells 在 C# 中**將樞紐分析表複製到另一工作表**。這些步驟——設定專案、載入活頁簿、定義範圍、以 `CopyPivotTable = true` 複製，最後儲存——形成一個可靠的模式，您可在任何自動化管線中重複使用。  

若想更進一步，可考慮：

- **Excel 樞紐分析表複製**於多個活頁簿之間（迴圈處理檔案）。  
- 使用 **Aspose.Cells 複製範圍並保留樞紐** 的選項，將樞紐在不同活頁簿之間移動。  
- 在複製後使用 `PivotTable.RefreshData()` 自動刷新。  

歡迎嘗試不同的來源範圍，或將此技巧與圖表產生結合，打造全自動化的報表儀表板。有任何問題，請留言，祝編程愉快！

![顯示已複製樞紐分析表於新工作表的螢幕截圖](copy-pivot-screenshot.png "將樞紐分析表複製到另一工作表範例")

## 接下來您可以學習什麼？

以下教學涵蓋與本指南技術密切相關的主題。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索其他實作方式。

- [如何使用 Aspose.Cells for .NET 更改樞紐分析表來源資料 | 資料分析指南](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [精通 .NET 中的樞紐分析表格式設定（使用 Aspose.Cells）](/cells/english/net/formatting/format-pivot-tables-dotnet-aspose-cells/)
- [在 .NET 中使用 Aspose.Cells 存取樞紐分析表的外部資料來源](/cells/english/net/data-analysis/access-pivot-table-data-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}