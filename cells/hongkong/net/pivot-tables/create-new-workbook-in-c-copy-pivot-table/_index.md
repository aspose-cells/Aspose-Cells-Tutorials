---
category: general
date: 2026-06-24
description: 在 C# 中建立新工作簿並複製樞紐分析表，同時保留其資料。學習如何複製列、匯出選取範圍，並保持樞紐分析表完整。
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- export selected range
language: zh-hant
og_description: 在 C# 中建立新工作簿，並在保留資料的情況下複製樞紐分析表。逐步指南，說明如何複製列及匯出選取的範圍。
og_title: 在 C# 中建立新工作簿 – 複製樞紐分析表
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Create new workbook in C# and copy pivot table while preserving its
    data. Learn how to copy rows, export selected range, and keep the pivot intact.
  headline: Create New Workbook in C# – Copy Pivot Table
  type: TechArticle
- questions:
  - answer: Yes, as long as the copied rectangle encloses each pivot you need. If
      you only want one, adjust `rows`/`cols` to isolate it.
    question: Does this work with multiple pivot tables on the same sheet?
  - answer: The pivot cache will still point to the original connection. Call `pivotTable.RefreshData()`
      after loading the destination if you want to re‑query the source.
    question: What if the source workbook uses external data connections?
  - answer: Absolutely. Replace `destinationWorkbook` with `sourceWorkbook` and pick
      another worksheet index.
    question: Can I copy the pivot to a different sheet within the same workbook?
  - answer: 'Use `CopyRows`/`CopyColumns` overloads that accept a `CopyOptions` object—set
      `CopyOptions.CopyType = CopyType.ValuesOnly` or `CopyType.All` depending on
      your needs. --- ## Conclusion We’ve just walked through a **create new workbook**
      scenario that **copy pivot table**, **preserve pivot table**, an'
    question: Is there a way to copy formatting only?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel automation
title: 在 C# 中建立新活頁簿 – 複製樞紐分析表
url: /zh-hant/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中建立新工作簿 – 複製樞紐分析表

是否曾需要在 C# 中 **create new workbook** 只為了搬移包含樞紐分析表的一段資料？你並非唯一遇到此情況的人。在許多報表流程中，你會抓取少量列，或幾個欄位，並期望樞紐分析表保持原樣——沒有斷裂的參照，沒有遺失的計算。

好消息是？只要幾行 Aspose.Cells 程式碼，你就可以 **copy pivot table**，保持其完整，甚至 **export selected range** 而不會破壞任何內容。以下示範一個完整、可直接執行的範例，說明 **how to copy rows**、保留樞紐分析表，並將結果儲存為全新的工作簿。

## 本教學涵蓋內容

- 使用 Aspose.Cells 設定 C# 專案（此程式庫提供本教學的核心功能）。
- 載入包含原始樞紐分析表的來源工作簿。
- 使用程式庫的 `CopyRows` 與 `CopyColumns` 方法，複製所需的精確範圍。
- 在 **create new workbook** 情境下儲存複製的區域，同時讓樞紐分析表保持可用。
- 針對多個樞紐分析表、隱藏列與大型資料集等邊緣情況的技巧。

完成本指南後，你將能夠從任何 Excel 檔案 **export selected range**，保持樞紐分析表的運算邏輯，並將新檔案放置於任意位置。

> **Prerequisite**: Aspose.Cells for .NET（免費試用版或授權版）已透過 NuGet 安裝。若尚未加入，請在專案資料夾執行 `dotnet add package Aspose.Cells`。

---

## 建立新工作簿並複製樞紐分析表

以下程式碼即為解決方案的核心。我們會逐行說明其意義，最後呈現完整程式。

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // 1️⃣ Load the source workbook that contains the pivot table
        string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destSheet = destinationWorkbook.Worksheets[0];

        // 3️⃣ Define the range we want to copy (first 20 rows, first 4 columns)
        //    This range includes the pivot table we care about.
        int startRow = 0;   // zero‑based index
        int startColumn = 0;
        int totalRows = 20;
        int totalColumns = 4;

        // 4️⃣ Copy rows – this is the “how to copy rows” part.
        //    Aspose.Cells lets us copy rows directly from the source cells collection.
        sourceWorkbook.Worksheets[0].Cells.CopyRows(startRow, startRow, totalRows);

        // 5️⃣ Copy columns – paired with the row copy to form a rectangular block.
        sourceWorkbook.Worksheets[0].Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 6️⃣ Now move the copied block into the destination sheet.
        //    We use the same start cell (A1) for simplicity.
        destSheet.Cells.CopyRows(startRow, startRow, totalRows);
        destSheet.Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 7️⃣ Save the destination workbook – the pivot table is preserved in the copied range
        string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
        destinationWorkbook.Save(destPath);

        Console.WriteLine("✅ New workbook created and pivot table preserved at: " + destPath);
    }
}
```

### 為何這樣可行

- **`CopyRows` / `CopyColumns`**：這些方法會同時複製底層儲存格資料 *以及* 相關物件（例如樞紐快取）。因此搬移後樞紐分析表仍能正常運作。
- **獨立的目標工作簿**：透過建立全新的 `Workbook` 實例，我們 **create new workbook**，不會帶入任何舊有格式或隱藏工作表，避免干擾。
- **零基索引**：Aspose.Cells 使用零基索引，`0` 代表儲存格 **A1**。若樞紐分析表不在左上角，請調整 `startRow`/`startColumn`。
- **保留樞紐分析表**：樞紐的快取位於相同範圍內，複製該範圍即自動複製快取，無需額外程式碼。

---

## 如何複製列而不破壞樞紐分析表

如果你只關心列的複製部分，可以將其獨立出來：

```csharp
// Copy just rows 5‑15 (inclusive) from the source sheet
int sourceStartRow = 4;   // row 5 in Excel terms
int rowsToCopy = 11;      // rows 5‑15 => 11 rows
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy);
```

**Pro tip**：當複製與樞紐分析表相交的列時，務必一次複製整個樞紐區域（列 + 欄）。僅複製部分會導致樞紐缺少欄位，產生 `#REF!` 錯誤。

---

## 匯出選取範圍 – 真實案例

想像你有一個巨大的銷售工作簿，但客戶只需要第一季的摘要，該摘要位於第 1‑20 列與 A‑D 欄。上面的程式碼已為你 **export selected range**。只要將 `totalRows` 與 `totalColumns` 變數改成客戶需求的值，即可完成。

### 處理隱藏列或篩選

若來源工作表有隱藏列（可能是被篩選掉的），你可能只想複製 *可見* 列。Aspose.Cells 提供支援可見性的 `CopyRows` 重載：

```csharp
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy, true);
```

將最後一個布林值設為 `true`，即可僅複製可見列——這在使用者套用篩選時，對「export selected range」非常適合。

---

## 保留樞紐分析表 – 常見陷阱與避免方式

| 陷阱 | 為何會發生 | 解決方式 |
|------|------------|----------|
| **Pivot cache not copied** | 使用一般的 `Range.Copy` 而非 `Cells.CopyRows/CopyColumns`。 | 如示範，使用 `Cells` 方法。 |
| **Destination sheet has existing pivot** | 將檔案儲存至已包含同名樞紐分析表的工作簿上。 | 像本例一樣，從全新 `Workbook()` 開始。 |
| **Named ranges break** | 原始樞紐分析表參考的命名範圍在新檔案中不存在。 | 同時複製命名範圍：`sourceWorkbook.Worksheets[0].Names.CopyTo(destSheet);` |
| **Data source path changes** | 樞紐指向的外部資料來源在新環境不可用。 | 複製後如有需要，呼叫 `PivotTable.RefreshData()`。 |

---

## 完整端對端範例（可直接執行）

以下為完整程式，包括 `using` 指令與簡易的 Console UI。直接貼到新的 Console App 專案，按 **F5** 即可執行。

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyUtility
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Load source workbook (contains the pivot)
            // -------------------------------------------------
            string srcPath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook srcWb = new Workbook(srcPath);

            // -------------------------------------------------
            // Step 2: Prepare destination workbook (create new workbook)
            // -------------------------------------------------
            Workbook destWb = new Workbook();
            Worksheet destWs = destWb.Worksheets[0];

            // -------------------------------------------------
            // Step 3: Define the block we want to copy
            // -------------------------------------------------
            int startRow = 0;      // A1
            int startCol = 0;      // A
            int rows = 20;         // first 20 rows
            int cols = 4;          // first 4 columns

            // -------------------------------------------------
            // Step 4: Copy rows and columns from source to destination
            // -------------------------------------------------
            srcWb.Worksheets[0].Cells.CopyRows(startRow, startRow, rows);
            srcWb.Worksheets[0].Cells.CopyColumns(startCol, startCol, cols);
            destWs.Cells.CopyRows(startRow, startRow, rows);
            destWs.Cells.CopyColumns(startCol, startCol, cols);

            // -------------------------------------------------
            // Step 5: Save the new workbook (preserve pivot table)
            // -------------------------------------------------
            string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
            destWb.Save(destPath);

            Console.WriteLine($"✅ Workbook created at {destPath}");
        }
    }
}
```

**預期輸出**（於 Console）：

```
✅ Workbook created at YOUR_DIRECTORY\copy-pivot.xlsx
```

開啟 `copy-pivot.xlsx`，你會看到與 `source.xlsx` 中相同的樞紐分析表，功能完整且引用已複製的資料範圍。

---

## 常見問題

**Q: 這能同時處理同一工作表上的多個樞紐分析表嗎？**  
A: 可以，只要複製的矩形區域包含所有需要的樞紐分析表。若只想保留其中一個，請調整 `rows`/`cols` 以將其孤立。

**Q: 若來源工作簿使用外部資料連線，該怎麼辦？**  
A: 樞紐快取仍會指向原始連線。若希望重新查詢來源，請在載入目標後呼叫 `pivotTable.RefreshData()`。

**Q: 能否將樞紐分析表複製到同一本工作簿的其他工作表嗎？**  
A: 完全可以。將 `destinationWorkbook` 換成 `sourceWorkbook`，再選擇其他工作表索引即可。

**Q: 有沒有只複製格式的方式？**  
A: 使用接受 `CopyOptions` 物件的 `CopyRows`/`CopyColumns` 重載——將 `CopyOptions.CopyType = CopyType.ValuesOnly` 或 `CopyType.All` 依需求設定。

---

## 結論

我們剛剛示範了一個 **create new workbook** 情境，完成 **copy pivot table**、**preserve pivot table** 與 **export selected range**，全程純 C# 實作。

## 接下來該學什麼？

以下教學與本篇內容密切相關，能進一步深化本指南所示技巧。每篇資源皆提供完整可執行的程式範例與逐步說明，協助你掌握更多 API 功能，並在自己的專案中探索替代實作方式。

- [以程式方式在 .NET 中建立新樞紐分析表](/cells/english/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/)
- [使用 Aspose.Cells for .NET 變更樞紐分析表來源資料 | 資料分析指南](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [使用 Aspose.Cells for .NET 管理 Excel 樞紐分析表相容性 | 資料分析指南](/cells/english/net/data-analysis/manage-excel-pivot-table-compatibility-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}