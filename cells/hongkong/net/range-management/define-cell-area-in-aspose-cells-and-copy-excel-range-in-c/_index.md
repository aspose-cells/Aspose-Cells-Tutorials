---
category: general
date: 2026-08-04
description: 在 Aspose.Cells 中定義儲存格範圍，並學習如何複製樞紐分析表、在 C# 中複製 Excel 範圍，以及在同一工作表中高效複製範圍。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- define cell area
- how to copy pivot
- copy excel range c#
- copy range same sheet
- aspose.cells copy range
language: zh-hant
lastmod: 2026-08-04
og_description: 在 Aspose.Cells 中定義儲存格區域，並在 C# 中複製 Excel 範圍，同時保留樞紐分析表。請遵循此一步一步的指南，以獲得可靠的結果。
og_image_alt: Screenshot showing how to define cell area and copy range in Aspose.Cells
og_title: 在 Aspose.Cells 中定義儲存格區域 – 使用 C# 複製 Excel 範圍
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  headline: Define cell area in Aspose.Cells and copy Excel range in C#
  type: TechArticle
- description: Define cell area in Aspose.Cells and learn how to copy pivot tables,
    copy Excel range C#, and copy range same sheet efficiently.
  name: Define cell area in Aspose.Cells and copy Excel range in C#
  steps:
  - name: The range A61:J110 contains a copy of the original data.
    text: The range A61:J110 contains a copy of the original data.
  - name: A new pivot table appears at the top of the copied range.
    text: A new pivot table appears at the top of the copied range.
  - name: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
    text: Refreshing the pivot reflects changes in the source data, confirming that
      **how to copy pivot** succeeded.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot tables
title: 在 Aspose.Cells 中定義儲存格區域並在 C# 中複製 Excel 範圍
url: /zh-hant/net/range-management/define-cell-area-in-aspose-cells-and-copy-excel-range-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Aspose.Cells 中定義儲存格區域並在 C# 複製 Excel 範圍

如果您需要 **定義儲存格區域** 以表示一個範圍，然後在同一工作表上複製該範圍，本教學將示範如何使用 Aspose.Cells for .NET 完成此操作。無論是搬移樞紐分析報表或是複製資料區塊，您只需幾個步驟即可掌握完整流程。

您還會學會 **如何複製樞紐** 表格而不失去其連結，並看到一個乾淨的 **copy excel range c#** 範例，適用於 **copy range same sheet** 的情境。無需額外工具——只要 Aspose.Cells 加上少量 C# 程式碼即可。

## 您需要的環境

- .NET 6.0 或更新版本（此程式碼同樣適用於 .NET Framework 4.7+）
- Aspose.Cells for .NET（NuGet 套件 `Aspose.Cells`）
- 一個包含樞紐分析表、範圍為 A1:J50 的 Excel 活頁簿（`input.xlsx`）
- 開發環境，例如 Visual Studio 2022

## 步驟 1：為來源範圍定義儲存格區域

第一件事是 **定義儲存格區域**，以表示您想要複製的區塊。Aspose.Cells 使用 `CellArea` 結構，該結構以零基索引儲存列與欄的編號。

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Define the source range that contains the pivot table (A1:J50)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 49,       // Row 50
    EndColumn = 9      // Column J
};
```

**為什麼這很重要：**`CellArea` 明確告訴 Aspose.Cells 要操作哪些儲存格。使用零基索引可以避免在將 Excel 的 A1 標記法轉換成程式碼時常見的「多或少一」錯誤。

## 步驟 2：在同一工作表上定義目的儲存格區域

若要 **copy range same sheet**，同時必須指定資料要貼到哪裡。目的位置可以從任意列開始；此處我們從第 61 列（零基索引 60）開始，以留下空白緩衝區。

```csharp
// Define the destination area on the same sheet (starting at row 61)
CellArea destinationRange = new CellArea
{
    StartRow = 60,     // Row 61
    StartColumn = 0,   // Column A
    EndRow = 109,      // Row 110 (same height as source)
    EndColumn = 9      // Column J (same width as source)
};
```

**為什麼這很重要：**透過鏡像來源的尺寸，您可以確保複製的區塊完整貼合，且不會被截斷。

## 步驟 3：在保留樞紐分析表的前提下複製範圍

現在您可以安全地 **how to copy pivot**。`CopyOptions` 類別提供 `CopyPivotTables` 屬性，可保留樞紐的定義、資料來源與格式。

```csharp
// Copy the range while preserving pivot tables
srcWorkbook.Worksheets[0].Cells.CopyRange(
    sourceRange,
    destinationRange,
    new CopyOptions
    {
        CopyPivotTables = true   // Ensure pivot tables are retained
    });
```

**為什麼這很重要：**若未將 `CopyPivotTables = true`，樞紐將變成靜態快照，失去互動性。此選項會複製底層快取與連結，使新樞紐的行為與原始樞紐完全相同。

## 步驟 4：儲存活頁簿

最後，將變更寫回磁碟。輸出檔案會顯示樞紐表已在同一工作表上成功複製。

```csharp
// Save the modified workbook
srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

**小技巧：**若需強制使用特定格式（例如處理較舊的 Excel 版本），可使用 `srcWorkbook.Save("CopyWithPivot.xlsx", SaveFormat.Xlsx)`。

## 步驟 5：驗證複製的樞紐分析表

在 Excel 中開啟 `CopyWithPivot.xlsx`，檢查以下項目：

1. 範圍 A61:J110 包含原始資料的副本。
2. 在複製範圍的上方出現新的樞紐分析表。
3. 重新整理樞紐時會反映來源資料的變更，證明 **how to copy pivot** 已成功。

若樞紐未能重新整理，請確認樞紐定義中的來源資料範圍仍指向原始活頁簿區域。當 `CopyPivotTables` 為 true 時，Aspose.Cells 會自動更新來源參照。

## 邊緣案例與變化

| 情境 | 需要變更的地方 |
|-----------|----------------|
| **複製到不同工作表** | 將 `srcWorkbook.Worksheets[0]` 改為目標工作表的索引或名稱，並相應調整 `destinationRange`。 |
| **複製合併儲存格區塊** | 設定 `CopyOptions.PasteType = PasteType.All` 以保留合併儲存格與格式。 |
| **僅複製值，不複製公式** | 使用 `CopyOptions.PasteType = PasteType.Values`，避免傳遞會參照原始工作表的公式。 |
| **大型範圍（> 10,000 列）** | 考慮使用 `Workbook.Copy` 複製整個工作表以提升效能，之後再刪除不需要的列。 |

上述變化說明，同一套 **aspose.cells copy range** 邏輯可靈活應用於各種實務情境。

## 完整範例程式

以下提供可直接執行的完整程式碼。請將 `YOUR_DIRECTORY` 替換為您機器上的實際資料夾路徑。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 1: Define the source cell area (A1:J50)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 49,
            EndColumn = 9
        };

        // Step 2: Define the destination cell area on the same sheet (A61:J110)
        CellArea destinationRange = new CellArea
        {
            StartRow = 60,
            StartColumn = 0,
            EndRow = 109,
            EndColumn = 9
        };

        // Step 3: Copy the range while preserving pivot tables
        srcWorkbook.Worksheets[0].Cells.CopyRange(
            sourceRange,
            destinationRange,
            new CopyOptions { CopyPivotTables = true });

        // Step 4: Save the modified workbook
        srcWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

**預期結果：**執行程式後，`CopyWithPivot.xlsx` 會包含原始資料，且在第 61 列開始出現一模一樣的區塊，且樞紐分析表功能完整。

## 結論

現在您已掌握在 Aspose.Cells 中 **定義儲存格區域**、**copy excel range c#**，以及在 **copy range same sheet** 時保留所有樞紐功能的技巧。此方法可避免手動複製貼上的錯誤，且能應付大型活頁簿。

接下來，您可以探索如 **how to copy pivot** 跨多工作表的相關主題，或使用 **aspose.cells copy range** 複製整張工作表並保留格式。試著調整不同的 `CopyOptions` 設定，以符合您專案的需求。

祝開發順利！


## 接下來您可以學習什麼？

以下教學與本指南的技巧密切相關，提供完整的程式碼範例與逐步說明，協助您熟悉更多 API 功能並在專案中嘗試其他實作方式。

- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}