---
category: general
date: 2026-03-29
description: 快速學習如何在 GridJs 中插入行。本指南亦說明如何新增行以及透過批次操作一次新增多行。
draft: false
keywords:
- how to insert rows
- how to add rows
- add multiple rows grid
- batch row insertion
- large grid performance
language: zh-hant
og_description: 快速學習如何在 GridJs 中插入行。本指南展示如何新增行、在網格中新增多行，以及處理大量批次插入。
og_title: 如何在 GridJs 中插入行 – 高效新增多行
tags:
- GridJs
- C#
- data‑grid
title: 如何在 GridJs 中插入行 – 高效新增多行
url: /zh-hant/net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-grid-efficien/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 GridJs 中插入列 – 高效新增多列

有沒有想過 **如何在大型 GridJs 表格中插入列**，卻不會讓 UI 卡住？或許你已經嘗試過 **逐一新增列**，結果效能直線下降。好消息是 GridJs 提供了批次 API，讓你可以在一次呼叫中 **新增多列**，即使面對數百萬筆資料也能保持流暢。

在本教學中，我們將示範一個完整、可執行的範例，說明如何使用 `InsertRowsBatch` **插入列**。你會了解為什麼批次處理很重要、如何驗證結果，以及在目標索引極大時需要注意的事項。完成後，你就能自信地一次加入上千筆新記錄到任何 GridJs 實例。

## 前置條件

在開始之前，請確保你已具備：

- .NET 6.0 或更新版本（程式碼可在任何近期 SDK 編譯）
- 參考 `GridJs` NuGet 套件（或自行編譯的 DLL）
- 基本的 C# 知識 – 不需要成為大師，只要對類別與方法有基本概念即可
- 任意你慣用的 IDE 或編輯器（Visual Studio、Rider、VS Code… 都可）

> **專業小技巧：** 若你要處理真正巨大的表格（上千萬列），請啟用 `gridJs.EnableVirtualization = true;`，以減輕 UI 渲染負擔。

## 步驟 1：建立並設定 GridJs 實例

首先，你需要一個可使用的 `GridJs` 物件。把它想成你要在上面「畫」列的畫布。

```csharp
using System;
using GridJsLibrary;   // Assume this is the namespace for GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Initialize the grid
            GridJs gridJs = new GridJs();

            // Optional: turn on virtualization for huge data sets
            gridJs.EnableVirtualization = true;

            // Populate the grid with some dummy data so we can see the effect
            SeedInitialData(gridJs);

            // Now we’re ready to insert rows in bulk
            InsertRowsInBatch(gridJs);
        }

        // Helper: add 2 000 000 rows so our batch lands at index 2 000 001
        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }
```

> **為什麼這一步很重要：** 初始化 Grid 並（可選）先行填充資料，模擬實務上表格已經有大量資訊的情境。稍後要執行的批次插入必須遵守零基索引，因此我們先預先填充，以示範確切的插入位置。

## 步驟 2：使用 `InsertRowsBatch` **一次新增多列**

接下來就是教學的核心 – 透過一次呼叫 **大量新增列**。方法簽名為 `InsertRowsBatch(int startIndex, int count)`。本例中，我們從索引 2 000 000（即第 2 000 001 列）開始，新增十列。

```csharp
        // Step 2 – Insert a batch of rows
        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based, so this is row 2 000 001
            int rowsToAdd = 10;

            // The batch call creates placeholder rows; you can later populate them
            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Verify by reading back a few rows
            VerifyInsertion(grid, startIndex, rowsToAdd);
        }
```

> **運作原理：** `InsertRowsBatch` 會在內部配置所需的列數，並將既有列往下移。因為整個操作只在單一交易中完成，UI 只會刷新一次，這也是此方法被推薦用來 **高效新增列** 的原因。

## 步驟 3：驗證插入 – 列是否如預期落位？

批次操作完成後，你需要確認新列真的出現在正確的位置。以下輔助程式會讀取新加入區塊的第一列與最後一列，並將結果印到主控台。

```csharp
        // Step 3 – Simple verification
        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

**預期輸出**

```
Initial seed completed – 2 000 000 rows present.
Inserted 10 rows starting at index 2000001.
Verifying inserted rows:
Row 2000001: , 
Row 2000002: , 
...
Row 2000010: , 
```

空白儲存格代表該列目前是佔位符，尚未填入資料。之後你可以逐一填入，或再執行一次批次更新。

> **邊緣案例說明：** 若 `startIndex` 超過目前的列數，GridJs 會自動把新列加在最末端。相反地，負值索引會拋出 `ArgumentOutOfRangeException`，因此務必先驗證使用者提供的索引。

## 步驟 4：填入新列（可選但常見）

通常你不只想要空的列，還需要填入有意義的資料。你可以遍歷剛建立的範圍，呼叫 `SetCell` 或類似的 API。

```csharp
        // Optional: fill the newly added rows with sample data
        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }
```

如果需要立即顯示，可在批次插入後直接呼叫 `PopulateNewRows(gridJs, startIndex, rowsToAdd);`。

## 步驟 5：超大型表格的效能技巧

當你要 **一次新增多列** 的規模達到百萬級別時，請記住以下技巧：

1. **批次大小很關鍵** – 一次插入 10 000 列往往比十次各插入 1 000 列更快，因為每個批次只會觸發一次 UI 刷新。
2. **暫停 UI 更新** – 部分 GridJs 版本提供 `grid.SuspendLayout()` / `grid.ResumeLayout()`。若發現卡頓，可將批次程式碼包在這兩個呼叫之間。
3. **使用虛擬化** – 如前所述，`EnableVirtualization` 能大幅降低記憶體使用與渲染時間。
4. **避免深層拷貝** – 傳入簡單值型別或輕量物件；重量級物件會迫使 Grid 複製資料，進而拖慢效能。

## 完整可執行範例

把所有步驟整合起來，以下是可直接貼到新 Console 專案的完整程式碼：

```csharp
using System;
using GridJsLibrary;   // Replace with the actual namespace of your GridJs library

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            GridJs gridJs = new GridJs
            {
                EnableVirtualization = true
            };

            SeedInitialData(gridJs);
            InsertRowsInBatch(gridJs);
        }

        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }

        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based index for row 2 000 001
            int rowsToAdd = 10;

            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Optional: fill them with data
            PopulateNewRows(grid, startIndex, rowsToAdd);

            VerifyInsertion(grid, startIndex, rowsToAdd);
        }

        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }

        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

執行程式後，你會在主控台看到確認訊息，證明十列已正確插入指定位置並完成填充。

## 結論

我們已說明如何使用批次 API 在 GridJs 中 **插入列**，示範了 **高效新增列** 的作法，並探討了在 **一次新增多列** 時不會卡住 UI 的技巧。重點如下：

- 使用 `InsertRowsBatch(startIndex, count)` 進行任何批次操作。
- 必須驗證索引，且對於巨量資料建議啟用虛擬化。
- 若需要即時內容，可在批次後再填入列。

接下來，你可以進一步研究 **如何刪除列**、實作 **批次編輯的復原/重做**，或將 GridJs 與即時串流的後端服務整合。上述主題皆直接建立在本教學的概念之上。

盡情實驗吧——改變批次大小、嘗試在表格最前端插入，或在同一交易中合併多個批次。玩得越多，你對大型 GridJs 的操作就會越得心應手。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}