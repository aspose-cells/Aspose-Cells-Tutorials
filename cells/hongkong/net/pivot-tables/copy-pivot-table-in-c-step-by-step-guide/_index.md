---
category: general
date: 2026-03-18
description: 在 C# 中使用 Aspose.Cells 複製樞紐分析表。學習如何複製 Excel 範圍、複製 Excel 樞紐、將範圍複製到新工作表以及在幾分鐘內將樞紐分析表複製到工作表。
draft: false
keywords:
- copy pivot table
- copy excel range
- duplicate excel pivot
- copy range to new
- copy pivot to sheet
language: zh-hant
og_description: 使用 Aspose.Cells 在 C# 中複製樞紐分析表。學習如何複製 Excel 樞紐分析表、將 Excel 範圍複製到新位置，以及將樞紐分析表複製到工作表，並提供完整程式碼範例。
og_title: 在 C# 中複製樞紐分析表 – 完整程式設計指南
tags:
- Aspose.Cells
- C#
- Excel automation
title: 在 C# 中複製樞紐分析表 – 逐步指南
url: /zh-hant/net/pivot-tables/copy-pivot-table-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中複製樞紐分析表 – 完整程式指南

是否曾需要 **copy pivot table** 從工作簿的一個區域移到另一個區域，但又不確定如何在不失去底層資料連結的情況下完成？你並不孤單。許多開發者在自動化 Excel 報表時都會卡在這裡，尤其是當樞紐分析表位於較大的資料區塊內時。好消息是？使用 Aspose.Cells，你可以 **exactly as it appears** 複製樞紐分析表，同時也會學會如何 **copy excel range**、**duplicate excel pivot**，甚至 **copy pivot to sheet**，只需幾行 C# 程式碼。

在本教學中，我們將示範一個真實情境：將佔據 *A1:J20* 的樞紐分析表搬移到同一工作表的 *M1:V20* 新區域。完成後，你將擁有可執行的程式、了解每一步的意義，並能將程式碼套用到其他範圍或不同工作表。所有說明都在此，不需額外文件。

---

## 前置條件

在開始之前，請確保你已具備：

- **Aspose.Cells for .NET**（版本 23.9 或更新）。可透過 NuGet 取得：`Install-Package Aspose.Cells`。
- 基本的 C# 開發環境（Visual Studio 2022、Rider，或安裝 C# 擴充功能的 VS Code）。
- 一個 Excel 檔案（`source.xlsx`），其中的樞紐分析表位於 *A1:J20* 範圍內。

就這些。如果你已會建立 Console 應用程式，即可開始。

---

## 如何在 Aspose.Cells 中複製樞紐分析表

解決方案的核心只需要一次呼叫 `Worksheet.Cells.CopyRange`。此方法不僅會複製原始儲存格值，還會自動保留樞紐分析表、圖表及其他豐富物件。讓我們一步步拆解。

### Step 1: 載入來源工作簿

首先，我們需要將工作簿載入記憶體。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Why this matters:** 載入工作簿會在記憶體中建立可供 Aspose.Cells 操作的表示，無需啟動 Excel。速度快、執行緒安全，且適用於伺服器環境。

### Step 2: 取得第一張工作表

大多數範例使用第一張工作表，但你也可以指定任意索引或名稱。

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = sourceWorkbook.Worksheets[0];
```

> **Tip:** 若要 **copy pivot to sheet** 到其他工作表，只需將 `worksheet` 參考改為另一個 `Worksheet` 物件。

### Step 3: 定義來源與目標範圍

我們會使用 `CellArea` 結構來描述要搬移的區塊。

```csharp
        // Define the source range (A1:J20) that contains the pivot table
        CellArea sourceRange = new CellArea(0, 0, 19, 9);   // rows 0‑19, columns 0‑9

        // Define the target range (M1:V20) where the data will be copied
        CellArea targetRange = new CellArea(0, 12, 19, 21); // rows 0‑19, columns 12‑21
```

> **Explanation:** 列與欄的索引是從 0 開始計算。欄 0 = **A**，欄 12 = **M**，以此類推。若你的樞紐分析表位於其他位置，請調整這些數字。

### Step 4: 執行複製操作

現在魔法發生了。將最後一個布林參數設為 `true`，即告訴 Aspose.Cells 複製所有物件——包括樞紐分析表。

```csharp
        // Copy the source range to the target range; pivot tables are copied automatically
        worksheet.Cells.CopyRange(
            sourceRange.StartRow, sourceRange.StartColumn,
            sourceRange.EndRow, sourceRange.EndColumn,
            targetRange.StartRow, targetRange.StartColumn,
            true);
```

> **Why `true`?** 此旗標表示「複製所有物件」。若設為 `false`，只會搬移純儲存格值，樞紐分析表將會遺失。

### Step 5: 儲存工作簿

最後，將修改後的工作簿寫回磁碟。

```csharp
        // Save the workbook with the copied range
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copy-pivot.xlsx");
    }
}
```

> **Result:** `copy-pivot.xlsx` 現在同時包含原始的樞紐分析表（*A1:J20*）**以及**在 *M1:V20* 的完全相同副本。開啟 Excel 檢查，兩個樞紐分析表皆可正常運作且保留資料連結。

---

## 複製 Excel 範圍到新位置 – 快速變形

有時只需要 **copy excel range** 而不在乎樞紐分析表。相同的 `CopyRange` 方法即可，只要將最後參數設為 `false`。

```csharp
worksheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    false); // plain values only
```

> **When to use:** 若你只是搬移原始資料至暫存計算表，關閉物件複製可節省記憶體並加快執行速度。

---

## 在多個工作表上 **duplicate excel pivot**

如果想要在不同工作表上 **duplicate excel pivot**，模式相同，只需把目的地 `Worksheet` 換成另一張。

```csharp
// Assume we have a second sheet already created
Worksheet destSheet = sourceWorkbook.Worksheets.Add("PivotCopy");

// Copy the pivot (and its data source) to the new sheet starting at A1
destSheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    0, 0, // destination at A1
    true);
```

> **Edge case:** 若來源樞紐分析表使用的資料表位於原始工作表，Aspose.Cells 也會同時複製底層資料表定義，確保新樞紐分析表即插即用。

---

## 常見問題與避免方式

| 常見問題 | 發生原因 | 解決方法 |
|---------|----------|----------|
| **樞紐分析表失去快取** | 使用 `CopyRange` 並將最後參數設為 `false`，或自訂複製程式碼忽略物件。 | 需要保留樞紐分析表時，務必傳入 `true`。 |
| **目標儲存格已包含資料** | 會靜默覆寫，可能導致現有公式受損。 | 先清除目標區域：`worksheet.Cells.ClearRange(targetRange.StartRow, targetRange.StartColumn, targetRange.EndRow, targetRange.EndColumn, true);` |
| **來源範圍未包含整個樞紐分析表** | 樞紐分析表可能跨越比預期更多的列/欄（例如隱藏列）。 | 使用 `worksheet.PivotTables[0].DataRange` 以程式方式取得精確範圍。 |
| **跨工作簿複製** | `CopyRange` 只能在同一工作簿內使用。 | 先使用 `sourceWorksheet.Cells.CopyRange` 複製到暫存範圍，然後 `destWorkbook.Worksheets.AddCopy(sourceWorksheet);` |

---

## 預期輸出與驗證

執行程式後：

1. 開啟 `copy-pivot.xlsx`。
2. 你會看到兩個相同的樞紐分析表——一個在 **A1:J20**，另一個在 **M1:V20**。
3. 重新整理任一樞紐分析表，兩者皆會反映相同的底層資料。
4. 若你已複製到其他工作表，新工作表亦會包含可正常運作的副本。

以下程式碼可快速驗證：

```csharp
int pivotCount = worksheet.PivotTables.Count; // should be 2 after copy
Console.WriteLine($"Pivot tables on the sheet: {pivotCount}");
```

---

## 專業提示：自動偵測範圍

硬寫 `CellArea` 只適合靜態報表，實務上常需要動態定位樞紐分析表。

```csharp
// Find the first pivot table on the sheet
PivotTable pt = worksheet.PivotTables[0];
CellArea ptRange = pt.DataRange;

// Use the detected range for copying
worksheet.Cells.CopyRange(
    ptRange.StartRow, ptRange.StartColumn,
    ptRange.EndRow, ptRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    true);
```

> **Why bother?** 讓你的解決方案能抵禦版面變動——不再出現「哎呀，樞紐分析表搬到 B2」的錯誤。

---

![copy pivot table example](copy-pivot.png){alt="複製樞紐分析表範例"}

*此螢幕截圖（佔位）顯示左側的原始樞紐分析表與右側的複製版本。*

---

## 重點回顧

我們剛剛說明了如何在 C# 中使用 Aspose.Cells **copy pivot table**，並探討了 **copy excel range**、**duplicate excel pivot**，甚至 **copy pivot to sheet** 的各種做法。關鍵要點如下：

- 使用 `Worksheet.Cells.CopyRange` 並將 `true` 旗標傳入，以保留豐富物件。
- 以零基索引定義來源與目標的 `CellArea` 物件。
- 若需 **copy pivot to sheet**，請調整目的工作表。
- 留意既有資料、隱藏列以及跨工作簿情境等邊緣案例。

---

## 接下來可以做什麼？

- **動態樞紐發現**：建立輔助程式，掃描工作簿中所有樞紐分析表並自動複製。
- **匯出為 PDF/HTML**：複製完成後，可將工作表渲染成報表格式——Aspose.Cells 也支援此功能。
- **效能調校**：對於大型工作簿，考慮在複製前關閉計算，完成後再重新啟用。

隨意實驗：變更目標座標、複製至全新工作簿，或在多個工作表上迴圈產生彙總報表。可能性無窮，而有了現在的基礎，你將能將程式碼套用到幾乎所有 Excel 自動化任務。

祝編程愉快，願你的樞紐分析表永遠保持完美同步！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}