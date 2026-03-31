---
category: general
date: 2026-03-30
description: 學習如何在 C# 中使用 WRAPCOLS 建立 Excel 工作簿、向 Excel 添加資料，並在使用 WRAPROWS 時強制公式計算。
draft: false
keywords:
- how to use wrapcols
- create excel workbook c#
- add data to excel
- force formula calculation
- how to use wraprows
language: zh-hant
og_description: 了解如何在 C# 中使用 WRAPCOLS 建立 Excel 工作簿、加入資料、強制公式計算，並利用 WRAPROWS 實作陣列公式。
og_title: 如何在 C# 中使用 WRAPCOLS – 完整指南
tags:
- Aspose.Cells
- C#
- Excel Automation
title: 如何在 C# 中使用 WRAPCOLS – 建立具換行功能的 Excel 活頁簿
url: /zh-hant/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 WRAPCOLS – 建立具 Wrap 函數的 Excel 活頁簿

有沒有想過在使用 C# 自動化 Excel 時 **如何使用 WRAPCOLS**？你並不孤單——許多開發者在需要將水平範圍轉換為垂直陣列而不想寫大量程式碼時，常會卡關。好消息是 Aspose.Cells 讓這件事變得輕而易舉。

在本教學中，我們將逐步示範一個完整且可執行的範例，說明 **如何使用 WRAPCOLS**、如何 **以 C# 方式建立 Excel 活頁簿**、如何 **將資料新增至 Excel**，甚至如何 **強制公式計算** 讓結果即時顯示。我們也會簡介 **如何使用 WRAPROWS** 以完成相反的轉換。完成後，你將擁有一個可直接執行的程式，並清楚了解每一步的意義。

---

![如何在 C# 中使用 WRAPCOLS 範例](alt="使用 WRAPCOLS 於 C# 後的 Excel 活頁簿螢幕截圖")

## 本指南涵蓋內容

* 使用 Aspose.Cells 建立全新的活頁簿。
* 以程式方式填入儲存格 (**add data to Excel**)。
* 套用 `WRAPCOLS` 函數將列轉換為欄。
* 使用 `WRAPROWS` 將欄翻回列 (**how to use wraprows**)。
* 立即強制引擎評估公式 (**force formula calculation**)。
* 儲存檔案並檢查輸出。

不需要外部文件說明——所有資訊皆在此處。

---

## 如何在 C# 中使用 WRAPCOLS – 步驟實作說明

以下為完整原始碼。你可以將它複製貼上到新的 Console 專案，加入 Aspose.Cells NuGet 套件，然後按 **F5** 執行。

```csharp
// ------------------------------------------------------------
// How to Use WRAPCOLS in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.Cells;

namespace WrapFunctionsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a fresh workbook (this is how we **create excel workbook c#** style)
            Workbook workbook = new Workbook();

            // 2️⃣ Grab the first worksheet – it's created by default
            Worksheet sheet = workbook.Worksheets[0];

            // 3️⃣ **Add data to Excel**: place two numbers side‑by‑side
            sheet.Cells["A1"].PutValue(1);   // first value
            sheet.Cells["B1"].PutValue(2);   // second value

            // 4️⃣ **How to use WRAPCOLS** – turn the horizontal range A1:B1 into a vertical array
            //    The second argument (1) tells WRAPCOLS to create 1 column per element.
            sheet["C1"].Formula = "WRAPCOLS(A1:B1, 1)";

            // 5️⃣ **How to use WRAPROWS** – the opposite; turn the same range into a horizontal array
            //    Here we ask for 2 rows per element, which produces a single row with both values.
            sheet["C2"].Formula = "WRAPROWS(A1:B1, 2)";

            // 6️⃣ **Force formula calculation** so the workbook reflects the results immediately
            workbook.CalculateFormula();

            // 7️⃣ Save the workbook to disk – change the path to a folder you own
            string outputPath = @"WrapFunctions.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
            Console.WriteLine("Check cells C1 and C2 for the WRAPCOLS / WRAPROWS results.");
        }
    }
}
```

### 為何每一行都很重要

| 步驟 | 說明 |
|------|------|
| **1️⃣ 建立全新活頁簿** | 這是基礎。Aspose.Cells 將 `Workbook` 物件視為整個 Excel 檔案，因此你實際上是在 **以 C# 方式建立 Excel 活頁簿**。 |
| **2️⃣ 取得第一個工作表** | 新活頁簿總會至少包含一個工作表 (`Worksheets[0]`)。提前取得可避免 null 參考的意外。 |
| **3️⃣ 新增資料至 Excel** | 使用 `PutValue` 我們 **add data to Excel**，且不必擔心儲存格格式。數字 `1` 與 `2` 為我們測試 wrap 函數的資料。 |
| **4️⃣ 如何使用 WRAPCOLS** | `WRAPCOLS(A1:B1, 1)` 告訴 Excel 將範圍 `A1:B1` 的值垂直展開，每列一個。結果放在 `C1`，向下展開 (`C1`, `C2`, …)。 |
| **5️⃣ 如何使用 WRAPROWS** | `WRAPROWS(A1:B1, 2)` 則相反：產生水平展開，將兩個值放入從 `C2` 開始的同一列。 |
| **6️⃣ 強制公式計算** | 預設情況下，Aspose.Cells 可能會延遲計算，直到在 Excel 中開啟檔案。呼叫 `CalculateFormula()` **forces formula calculation**，讓你在儲存後即可讀取結果。 |
| **7️⃣ 儲存活頁簿** | 最後一步將所有內容寫入磁碟。開啟產生的 `WrapFunctions.xlsx` 以檢視結果。 |

---

## 建立 Excel 活頁簿 C# – 環境設定

在執行程式碼之前，請確保已備妥以下工具：

1. **.NET 6.0+** – 建議使用最新的 LTS 版本。
2. **Visual Studio 2022**（或搭配 C# 擴充功能的 VS Code）。
3. **Aspose.Cells for .NET** – 透過 NuGet 安裝：  
   ```bash
   dotnet add package Aspose.Cells
   ```
4. 一個可寫入的資料夾，用於存放輸出檔案。

這些前置條件相當簡單；不需 COM interop 或安裝 Office，正因如此 Aspose.Cells 成為伺服器端產生 Excel 的熱門選擇。

---

## 新增資料至 Excel – 最佳實踐

以程式方式 **add data to Excel** 時，請參考以下建議：

* **使用 `PutValue`** 來寫入原始數字或字串；它會自動偵測資料類型。
* **避免在大型專案中硬編碼儲存格位址**——使用迴圈或命名範圍以提升可擴充性。
* **盡量少設定儲存格樣式**；每次樣式變更都會產生額外開銷。若需格式化，請建立單一樣式物件，並套用至多個儲存格。

在我們這個小範例中僅插入兩個數字，但相同的模式可擴充至數千列。

---

## 如何使用 WRAPROWS – 水平陣列範例

若需要 `WRAPCOLS` 的相反功能，`WRAPROWS` 就是你的首選。語法如下：

```
WRAPROWS(source_range, [rows_per_item])
```

* `source_range` – 你想要轉換的範圍。
* `rows_per_item` – 可選參數，告訴 Excel 每個元素佔用多少列。在本示範中，我們使用 `2` 讓兩個值放在同一列上。

你可以透過變更第二個參數來試驗：

```csharp
// Example: split each value into its own column, three rows per item
sheet["D1"].Formula = "WRAPROWS(A1:B1, 3)";
```

開啟活頁簿後，你會看到值橫向展開至三個欄位，每個欄位皆依需求重複原始數字。

---

## 強制公式計算 – 何時與為何

你可能會想，「真的需要呼叫 `CalculateFormula()` 嗎？」答案是 **是**，如果：

* 你打算在 **儲存** 後以 **程式方式** 讀取 **已計算** 的值。
* 你希望確保檔案在 **Excel** 中開啟時，已 **顯示正確** 的結果。
* 你在 **無介面環境**（例如 Web API）執行，沒有使用者會手動觸發重新計算。

跳過此步驟不會破壞活頁簿，但儲存格會顯示公式文字 (`=WRAPCOLS(...)`)，而非計算結果，直到 Excel 重新計算為止。

---

## 預期輸出 – 觀察要點

執行程式並開啟 `WrapFunctions.xlsx` 後：

| 儲存格 | 公式 | 顯示值 |
|--------|------|--------|
| **C1** | `=WRAPCOLS(A1:B1, 1)` | `1`（於 C1）與 `2`（於 C2）— 垂直清單 |
| **C2** | `=WRAPROWS(A1:B1, 2)` | `1`（於 C2）與 `2`（於 D2）— 水平清單 |

因此你會看到從 **C1** 開始的垂直欄位，以及從 **C2** 開始的水平列。這證實兩個 wrap 函數皆如預期運作。

---

## 邊緣情況與變形

| 情境 | 會有什麼變化？ | 建議調整 |
|------|----------------|----------|
| **大型範圍 (A1:Z1)** | 垂直展開的值更多 | 若想每組產生多欄，請增加 `WRAPCOLS` 的第二個參數。 |
| **非數值資料** | 文字字串會以相同方式處理 | 無需更改程式碼；`PutValue` 接受任何物件。 |
| **動態範圍** | 編譯時無法得知大小 | 使用 `sheet.Cells.MaxDataColumn` 與 `MaxDataRow` 來組成地址字串。 |
| **多工作表** | 需要在不同工作表上套用 wrap 函數 | 參照正確的工作表 (`workbook.Worksheets["Sheet2"]`)。 |

預先考慮這些變化，你即可將核心模式套用至幾乎所有自動化情境。

---

## 實務小技巧

* **Pro tip:** 若目標為 .NET Core 3.1+，請將活頁簿建立包在 `using` 區塊中，以確保即時釋放所有資源。
* **Watch out for:** 在大範圍內設定相同公式卻未呼叫 `CalculateFormula()`，可能導致效能瓶頸。盡可能批次處理公式。
* **Tip:** 若需在程式碼中讀回計算後的值，呼叫 `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}