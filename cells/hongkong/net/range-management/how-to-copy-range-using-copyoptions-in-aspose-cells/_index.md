---
category: general
date: 2026-11-19
description: 學習如何在 Aspose.Cells 中使用 CopyOptions 複製範圍，於複製帶有格式的 Excel 範圍時保留格式及樞紐分析表。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range using copyoptions
- copy excel range with formatting
- Aspose.Cells copy range
- preserve pivot tables Aspose
- Excel automation C#
language: zh-hant
lastmod: 2026-11-19
og_description: 在 Aspose.Cells 中使用 CopyOptions 複製範圍，可完整保留格式與樞紐分析表，讓您可靠地操作活頁簿。
og_image_alt: Screenshot of C# code that copies an Excel range using Aspose.Cells
  CopyOptions
og_title: 在 Aspose.Cells 中使用 CopyOptions 複製範圍 – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  headline: How to copy range using CopyOptions in Aspose.Cells
  type: TechArticle
- description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  name: How to copy range using CopyOptions in Aspose.Cells
  steps:
  - name: Why `CopyOptions` matters
    text: '* **Performance** – The library performs a single internal operation rather
      than copying cells one‑by‑one. * **Accuracy** – All visual aspects (fonts, colors,
      borders) survive the move, which eliminates visual drift in generated reports.
      * **Reliability** – Pivot tables remain functional because the'
  - name: What if the destination area overlaps the source?
    text: 'Aspose.Cells throws an `ArgumentException`. To avoid this, calculate a
      destination that does not intersect the source, or copy to a different worksheet:'
  - name: How to copy between different workbooks?
    text: 'Create a second `Workbook` instance for the target file and use the same
      `CopyOptions` object:'
  - name: Does `CopyOptions` also copy merged cells?
    text: Yes. The `CopyStyle` flag includes merged‑cell information. If you need
      finer control, set `options.CopyMergedCells = true` (available in newer versions).
  - name: What about large ranges (thousands of rows)?
    text: The operation is memory‑efficient, but you may want to increase the `WorkbookSettings`
      `MemorySetting` to `MemorySetting.MemoryPreference` for very large files.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: 如何在 Aspose.Cells 中使用 CopyOptions 複製範圍
url: /zh-hant/net/range-management/how-to-copy-range-using-copyoptions-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Aspose.Cells 中使用 CopyOptions 複製範圍

如果您需要 **使用 CopyOptions 複製範圍**，本指南將示範如何在保留所有格式與內嵌樞紐分析表的情況下，完整複製一段儲存格。許多開發者在將資料在工作表之間搬移時，常會遇到樣式遺失的問題，而 `CopyOptions` 類別正是為此而設，無需額外手動處理。

在本教學中您將學會：

* 定義 Excel 活頁簿中的來源與目標區域。  
* 使用 `CopyOptions` 保留儲存格格式、欄寬與樞紐分析表。  
* 將結果儲存為新檔案，以供後續處理使用。

此範例適用於任何 `.xlsx` 檔案，且僅需 Aspose.Cells for .NET 套件。

## 前置條件

開始之前，請確保您已具備：

* 已安裝 .NET 6.0 或更新版本。  
* 有效的 Aspose.Cells for .NET 授權（或免費評估金鑰）。  
* Visual Studio 2022 或您慣用的 C# IDE。  

除 `Aspose.Cells` 之外，無需其他 NuGet 套件。

## 第一步：建立專案並匯入命名空間

建立一個新的主控台應用程式，並加入 Aspose.Cells 參考：

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Your code will go here
        }
    }
}
```

`using Aspose.Cells;` 指令讓您可以使用 `Workbook`、`CellArea` 與 `CopyOptions`。

## 第二步：載入要修改的活頁簿

```csharp
// Step 2: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`Workbook` 代表整個 Excel 檔案。請將 `YOUR_DIRECTORY` 替換為放置來源檔案的資料夾路徑。

## 第三步：定義來源與目標範圍

```csharp
// Step 3: Define the source range (A1:H30)
CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");

// Step 3b: Define the destination range (A35:H64)
CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");
```

`CellArea.CreateCellArea` 會根據左上與右下儲存格位址建立矩形區域。您可以依需求調整座標，以符合要複製的區塊大小。

## 第四步：在保留格式與樞紐分析表的情況下複製範圍

```csharp
// Step 4: Copy the range using CopyOptions
CopyOptions options = new CopyOptions
{
    // Preserve all cell styles, number formats, and column widths
    CopyStyle = true,
    // Keep formulas unchanged (they will still reference the original sheet)
    CopyFormula = true,
    // Preserve any pivot tables that intersect the copied area
    CopyPivotTables = true,
    // Retain data validation and conditional formatting
    CopyDataValidation = true,
    CopyConditionalFormatting = true
};

workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
```

`CopyOptions` 物件告訴 Aspose.Cells 要保留哪些內容。將 `CopyPivotTables = true` 設為 **使用 CopyOptions 複製範圍** 時的關鍵，因為來源可能包含樞紐分析表。其他旗標則確保 **copy excel range with formatting** 能自動完成——不需要在複製後額外重新套用樣式。

### 為何 `CopyOptions` 如此重要

* **效能** – 函式庫只執行一次內部操作，而非逐格複製。  
* **精確度** – 所有視覺屬性（字型、顏色、框線）皆會保留下來，避免產生報表視覺漂移。  
* **可靠性** – 樞紐分析表仍可正常運作，因為其快取與來源參照會一併複製。

## 第五步：儲存已修改的活頁簿

```csharp
// Step 5: Save the workbook with the copied range
workbook.Save("YOUR_DIRECTORY/output.xlsx");
Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
```

呼叫 `Save` 後，`output.xlsx` 會包含原始資料以及在目標位置複製的區塊，且格式與樞紐分析表完整保留。

## 完整來源程式碼供參考

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // Define source and destination ranges
            CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");
            CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");

            // Configure copy options to preserve everything
            CopyOptions options = new CopyOptions
            {
                CopyStyle = true,
                CopyFormula = true,
                CopyPivotTables = true,
                CopyDataValidation = true,
                CopyConditionalFormatting = true
            };

            // Perform the copy operation
            workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);

            // Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");
            Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
        }
    }
}
```

執行此程式會輸出：

```
Range copied successfully. Output saved to output.xlsx
```

在 Excel 中開啟 `output.xlsx`，您會看到 A1:H30 的區塊已在 A35:H64 複製，所有儲存格顏色、框線、數字格式以及任何樞紐分析表皆保持不變。

## 常見問題與特殊情況處理

### 目標區域與來源區域重疊會怎樣？

Aspose.Cells 會拋出 `ArgumentException`。為避免此情況，請計算不與來源交叉的目標位置，或改為複製到不同的工作表：

```csharp
Worksheet destSheet = workbook.Worksheets.Add("CopySheet");
destSheet.Cells.CopyRange(sourceRange, CellArea.CreateCellArea("A1", "H30"), options);
```

### 如何在不同活頁簿之間複製？

為目標檔案建立第二個 `Workbook` 實例，並使用相同的 `CopyOptions` 物件：

```csharp
Workbook target = new Workbook();
target.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
target.Save("target.xlsx");
```

### `CopyOptions` 會同時複製合併儲存格嗎？

會。`CopyStyle` 旗標已包含合併儲存格資訊。如需更細緻的控制，可設定 `options.CopyMergedCells = true`（較新版本支援）。

### 大範圍（數千列）會有問題嗎？

此操作具備記憶體效能，但對於極大型檔案，建議將 `WorkbookSettings` 的 `MemorySetting` 設為 `MemorySetting.MemoryPreference`。

## 專業小技巧

* **重複使用同一個 `CopyOptions`** 實例進行多次複製，可減少物件配置開銷。  
* **在複製前驗證區域**：`if (!CellArea.IsValid(sourceRange) || !CellArea.IsValid(destinationRange))` 能提前捕捉拼寫錯誤。  
* **關閉計算**（`workbook.Settings.CalcMode = CalculationMode.Manual`）在大量資料複製時可加速，完成後再呼叫 `workbook.CalculateFormula()` 以取得最新結果。

## 結論

現在您已掌握如何在 Aspose.Cells 中 **使用 CopyOptions 複製範圍**，同時實現 **copy excel range with formatting**，並保留樞紐分析表與其他進階功能。此方法省去手動樣式重新套用的步驟，確保 Excel 自動化流程既穩定又易於維護。

接下來您可以探索：

* 使用 `CopyOptions` 複製整個工作表。  
* 結合 `WorksheetCollection.AddCopy` 進行模板式報表產生。  
* 將程式碼整合至 ASP.NET Core API，提供即時的 Excel 轉換服務。

歡迎嘗試不同的來源/目標座標，並在留言區分享您的成果！

## 接下來該學什麼？

以下教學與本篇內容緊密相關，能進一步深化您對 API 功能的掌握，並提供其他實作方式的範例：

- [Excel Aspose Cells Dotnet Copy Range Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/french/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}