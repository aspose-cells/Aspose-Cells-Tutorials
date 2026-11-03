---
category: general
date: 2026-09-27
description: 學習如何使用 Aspose.Cells 在 C# 中複製樞紐分析表。包括帶格式的複製列、將樞紐分析表複製到其他工作表，以及將樞紐分析表匯出至新工作簿。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy rows with formatting
- copy pivot table to another sheet
- how to copy excel rows
- export pivot table to new workbook
language: zh-hant
lastmod: 2026-09-27
og_description: 如何在 C# 中使用 Aspose.Cells 複製樞紐分析表。請依照步驟說明，將帶格式的列複製、將樞紐分析表移至其他工作表，並匯出至新活頁簿。
og_image_alt: Excel sheet showing a copied pivot table after using Aspose.Cells
og_title: 如何在 C# 中複製樞紐分析表 – 完整 Aspose.Cells 教學
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to copy a pivot table in C# using Aspose.Cells. Includes
    copy rows with formatting, copy pivot table to another sheet, and export pivot
    table to a new workbook.
  headline: How to copy a pivot table in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot table
title: 如何在 C# 中使用 Aspose.Cells 複製樞紐分析表
url: /zh-hant/net/pivot-tables/how-to-copy-a-pivot-table-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Aspose.Cells 複製樞紐分析表

如果您需要 **copy a pivot table** 從一個工作表複製到另一個工作表，學習 **how to copy pivot table** 在 C# 中使用 Aspose.Cells 可以為您節省數小時的手動工作。此方法亦可讓您 **copy rows with formatting**，保持樞紐快取完整，甚至 **export pivot table to a new workbook**，當您需要獨立檔案時。

本教學將帶您完成完整工作流程：

* 建立工作簿，  
* 複製樞紐分析表範圍，同時保留格式，  
* 將複製的資料放置於新工作表，  
* 將結果儲存為單獨檔案。

您將了解為何內建的 `CopyRows` 方法是 **copy pivot table to another sheet**（將樞紐分析表複製到另一工作表）最可靠的方式，並取得處理隱藏列或外部資料來源等邊緣情況的技巧。

## 前置條件

在開始之前，請確保您具備以下條件：

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 or later | Aspose.Cells 支援 .NET 6+，提供最佳效能。 |
| Visual Studio 2022 (or any C# IDE) | 您需要能還原 NuGet 套件的編輯器。 |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | 此函式庫提供範例中使用的 `CopyRows` API。 |
| A source Excel file (`source.xlsx`) that contains a pivot table in the range `A1:G20` | 程式碼會複製此特定範圍；若您的樞紐分析表較大，請調整範圍。 |

Install the library with the NuGet CLI or Package Manager Console:

```bash
dotnet add package Aspose.Cells
```

## 步驟 1：載入包含樞紐分析表的工作簿

第一行會建立一個代表整個 Excel 檔案的 `Workbook` 物件。一次載入檔案即可取得對所有工作表的讀寫存取權限。

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **此步驟的重要性** – 若未載入工作簿，後續的 `CopyRows` 呼叫將無法參照來源資料或樞紐快取。

## 步驟 2：準備來源與目標工作表

您需要一個目標工作表來放置複製的樞紐分析表。以下程式碼會取得第一個工作表（原始樞紐分析表所在位置），並新增一個名為 **Copy** 的工作表。

```csharp
// Get the source worksheet (index 0 = first sheet)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a new worksheet that will receive the copied rows
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
```

> **專業提示**：若目標工作表已存在，請先呼叫 `Worksheets.RemoveAt(index)` 以避免名稱重複。

## 步驟 3：定義包含樞紐分析表的儲存格區域

`CellArea` 物件描述您欲搬移範圍的左上與右下儲存格。在此範例中，樞紐分析表佔用 `A1:G20`。若表格較大，請調整座標。

```csharp
// Define the range that includes the pivot table (A1:G20)
CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");
```

## 步驟 4：複製帶格式的列並保留樞紐快取

`CopyRows` 方法會將 **rows**（列）從來源工作表複製到目標工作表。傳入 `CopyOptions.CopyAll` 可確保值、格式、圖表以及嵌入物件——所有屬於樞紐分析表的內容——皆被轉移。

```csharp
// Copy the rows from the source area to the destination sheet
sourceSheet.CopyRows(
    sourceArea.StartRow,          // start row in the source sheet
    destinationSheet,            // target worksheet
    0,                            // start row in the destination sheet
    sourceArea.RowCount,          // number of rows to copy
    CopyOptions.CopyAll);        // copy everything (values, formats, objects, etc.)
```

### 為何 `CopyRows` 比 `Copy` 更適合用於樞紐分析表

* `CopyRows` 會尊重內部樞紐快取，因此複製的樞紐分析表仍保持功能。
* 它會完整保留 **copy rows with formatting**，與原始工作表完全相同。
* 不同於簡單的範圍 `Copy`，它亦會搬移隱藏列及任何相關的切片器。

## 步驟 5：儲存含有複製樞紐分析表的工作簿

最後，將修改後的工作簿寫入磁碟。新檔案包含原始工作表以及一個名為 **Copy** 的工作表，內含原始樞紐分析表的完整功能複本。

```csharp
// Save the workbook to a new file
workbook.Save(@"YOUR_DIRECTORY\pivot_copied.xlsx");
```

### 預期結果

當您開啟 `pivot_copied.xlsx` 時：

* 工作表 **Sheet1** 仍保留原始資料與樞紐分析表。
* 工作表 **Copy** 顯示相同的樞紐分析表，版面、篩選條件與格式皆相同。
* 所有公式與資料連結保持完整，因為樞紐快取已隨列一起複製。

## 如何在同一活頁簿中將樞紐分析表複製到另一工作表

如果您只需要將樞紐分析表放在另一個已存在的工作表（例如 “Report”），請將建立目標工作表的步驟改為參照該目標工作表：

```csharp
Worksheet destinationSheet = workbook.Worksheets["Report"]; // existing sheet
sourceSheet.CopyRows(sourceArea.StartRow, destinationSheet, 0,
                     sourceArea.RowCount, CopyOptions.CopyAll);
```

此程式碼片段示範 **copy pivot table to another sheet**，而不需建立新工作表。

## 匯出樞紐分析表至新活頁簿

有時您希望將樞紐分析表放在完全獨立的檔案中。完成複製後，您可以移除除包含複製樞紐分析表之外的所有工作表，然後儲存：

```csharp
// Keep only the copied sheet
for (int i = workbook.Worksheets.Count - 1; i >= 0; i--)
{
    if (workbook.Worksheets[i].Name != "Copy")
        workbook.Worksheets.RemoveAt(i);
}

// Save as a new workbook containing only the pivot table
workbook.Save(@"YOUR_DIRECTORY\pivot_only.xlsx");
```

現在 `pivot_only.xlsx` 只包含一個帶有複製樞紐分析表的工作表，滿足 **export pivot table to new workbook** 的需求。

## 如何在不失去格式的情況下複製 Excel 列

相同的 `CopyRows` 呼叫適用於任何範圍，不僅限於樞紐分析表。若您需要 **copy excel rows**，且包含條件格式、資料驗證或合併儲存格，請使用相同的方法：

```csharp
// Example: copy rows 30‑40 from Sheet1 to Sheet2
sourceSheet.CopyRows(29, // zero‑based index for row 30
                     workbook.Worksheets["Sheet2"],
                     0,
                     11, // rows 30‑40 = 11 rows
                     CopyOptions.CopyAll);
```

由於 `CopyOptions.CopyAll` 會傳輸所有內容，目標列將與來源列完全相同。

## 常見陷阱與避免方法

| 問題點 | 徵兆 | 解決方式 |
|---------|---------|-----|
| 來源範圍未包含整個樞紐分析表 | 複製的樞紐分析表被截斷。 | 確認 `CellArea` 包含樞紐分析表的所有列/欄。 |
| 目標工作表已包含資料 | 被覆寫的列導致資料遺失。 | 選擇全新工作表或從較高的列索引開始複製。 |
| 樞紐分析表使用外部資料來源 | 複製後失去連結。 | 複製後呼叫 `pivotTable.RefreshData()` 以重新建立連結。 |
| 隱藏列被省略 | 部分列在複製時消失。 | `CopyRows` 會自動複製隱藏列；請確認未使用 `CopyOptions.CopyValuesOnly`。 |

## 完整、可執行範例

以下是一個獨立的程式，您可貼入新的 Console 專案中。它示範了上述所有步驟。

```csharp
using System;
using Aspose.Cells;

namespace PivotTableCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains the pivot table
            string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2️⃣ Get source and destination worksheets
            Worksheet sourceSheet = workbook.Worksheets[0]; // first sheet
            Worksheet destinationSheet = workbook.Worksheets.Add("Copy");

            // 3️⃣ Define the cell area that holds the pivot table (A1:G20)
            CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");

            // 4️⃣ Copy rows with formatting and keep the pivot cache
            sourceSheet.CopyRows(
                sourceArea.StartRow,      // start row index (0‑based)
                destinationSheet,        // target sheet
                0,                        // start row in destination
                sourceArea.RowCount,      // number of rows to copy
                CopyOptions.CopyAll);    // copy everything

            // 5️⃣ Save the workbook with the copied pivot table
            string destPath = @"YOUR_DIRECTORY\pivot_copied.xlsx";
            workbook.Save(destPath);

            Console.WriteLine("Pivot table copied successfully to " + destPath);
        }
    }
}
```

**執行程式** 後會產生 `pivot_copied.xlsx`，其中包含一個名為 **Copy** 的新工作表，內有原始樞紐分析表的複本。

## 結論

您現在已了解如何在 C# 中 **how to copy a pivot table** using

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在本篇示範的技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy Pivot Table in C# – Complete Step‑by‑Step Guide](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [How to copy range with pivot tables in C# – Complete Guide](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}