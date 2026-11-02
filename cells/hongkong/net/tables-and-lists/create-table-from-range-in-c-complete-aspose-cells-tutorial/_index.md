---
category: general
date: 2026-03-30
description: 在 C# 使用 Aspose.Cells 從範圍建立表格 – 向儲存格加入資料，將範圍轉換為 ListObject，並儲存 Excel 而不套用篩選。
draft: false
keywords:
- create table from range
- create excel workbook c#
- add data to cells
- convert range to listobject
- save excel without filter
language: zh-hant
og_description: 在 C# 中使用 Aspose.Cells 從範圍建立表格。了解如何向儲存格加入資料、將範圍轉換為 ListObject，並在不使用篩選的情況下儲存
  Excel。
og_title: 在 C# 中從範圍建立表格 – 完整 Aspose.Cells 教程
tags:
- Aspose.Cells
- C#
- Excel Automation
title: 在 C# 中從範圍建立表格 – 完整 Aspose.Cells 教程
url: /zh-hant/net/tables-and-lists/create-table-from-range-in-c-complete-aspose-cells-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中從範圍建立表格 – 完整 Aspose.Cells 教程

是否曾經需要在 C# 中 **create table from range**，卻不確定要如何把一段普通資料區塊轉換成完整功能的 Excel 表格？你並非唯一遇到這個問題的人。無論是自動化報表、產生成績卡，或只是為後續分析清理資料，掌握這個小技巧都能為你省下大量手動工作。

在本指南中，我們將完整示範整個流程：**create excel workbook c#**、**add data to cells**、**convert range to ListObject**，最後 **save excel without filter**。完成後，你將擁有一段可直接在任何引用 Aspose.Cells 的 .NET 專案中執行的程式碼片段。

---

## Prerequisites

- 已安裝 .NET 6+（或 .NET Framework 4.7.2+）  
- Aspose.Cells for .NET（NuGet 套件 `Aspose.Cells`）— 以撰寫本文時的最新版本 (23.10) 為例，完全相容。  
- 具備基本的 C# 語法概念 — 不需要深入的 Excel interop 知識。

如果你已滿足上述條件，讓我們開始吧。

---

## Step 1: Create an Excel Workbook in C#

首先，我們需要一個全新的 Workbook 物件。可以把它想像成未來將存放表格的空白 Excel 檔案。

```csharp
using Aspose.Cells;

// Initialize a new workbook – this is equivalent to opening a blank .xlsx file.
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];   // Grab the first (default) worksheet.
```

> **Pro tip:** `Workbook()` 若不帶參數會建立一個僅含預設工作表的活頁簿，對於快速示範相當方便。若需要多張工作表，可稍後使用 `workbook.Worksheets.Add()` 追加。

---

## Step 2: Add Data to Cells

接下來，我們在工作表中填入一小段資料——兩個欄位（Name、Score）以及三列值。此範例說明了 **add data to cells** 的簡潔寫法。

```csharp
// Header row
worksheet.Cells["A1"].PutValue("Name");
worksheet.Cells["B1"].PutValue("Score");

// Data rows
worksheet.Cells["A2"].PutValue("Alice");
worksheet.Cells["B2"].PutValue(85);
worksheet.Cells["A3"].PutValue("Bob");
worksheet.Cells["B3"].PutValue(92);
```

為什麼使用 `PutValue`？它會自動偵測資料類型（字串或數值），並依據類型套用相應的格式，讓你在簡單情境下免除手動設定 `Style` 物件的麻煩。

> **Expected output:** 完成此步驟後，若在 Excel 中開啟活頁簿，會看到一個兩欄的格子，標題分別為「Name」與「Score」，下方緊接兩列資料。

---

## Step 3: Convert the Range into a ListObject (Table)

這一步就是魔法所在：將普通範圍轉換為 Excel 表格（在 Aspose.Cells API 中稱為 **ListObject**）。除了提供視覺樣式外，還能啟用內建的排序、篩選與結構化參照等功能。

```csharp
// Define the range boundaries.
// startRow and startColumn are zero‑based indexes.
// rowCount includes the header row.
int startRow = 0;          // Row 1 in Excel
int startColumn = 0;       // Column A
int rowCount = 3;          // Header + 2 data rows
int columnCount = 2;       // Two columns: Name & Score

// Add a ListObject to the worksheet and retrieve the object.
int listIndex = worksheet.ListObjects.Add(startRow, startColumn, rowCount, columnCount);
ListObject table = worksheet.ListObjects[listIndex];

// Turn on the UI filter dropdowns so users can interact with the table.
table.ShowAutoFilter = true;
```

> **Why use a ListObject?**  
> - **Structured references**：公式可直接以欄位名稱引用。  
> - **Auto‑filter UI**：使用者會看到下拉箭頭，方便快速篩選。  
> - **Styling**：之後只需一行程式碼即可套用內建表格樣式。

---

## Step 4: Remove the AutoFilter UI (Save Excel Without Filter)

有時候需要一張沒有篩選箭頭的乾淨工作表，例如最終報告的交付版。Aspose.Cells 23.10 提供了直接移除篩選 UI 的簡易方法。

```csharp
// Remove the filter UI completely.
table.AutoFilter = null;        // Clears the underlying filter object.
table.ShowAutoFilter = false;   // Hides the dropdown arrows.
```

請注意，我們並未刪除資料，只是關閉了視覺上的篩選控制元件，滿足 **save excel without filter** 的需求。

---

## Step 5: Save the Workbook

最後，將活頁簿寫入磁碟。檔案中仍保留表格，但不會顯示任何篩選箭頭。

```csharp
// Choose a folder you have write access to.
string outputPath = @"C:\Temp\NoAutoFilter.xlsx";
workbook.Save(outputPath);
```

開啟 `NoAutoFilter.xlsx` 後，你會看到表格已套用預設格式，卻沒有篩選箭頭。資料完整，檔案即可直接分發。

---

![Screenshot showing create table from range in Excel using Aspose.Cells](image.png "Create table from range screenshot")

*Image alt text:* **Screenshot showing create table from range in Excel using Aspose.Cells** – 以視覺方式證明表格已建立且沒有篩選下拉選單。

---

## Full, Runnable Example

以下是完整程式碼，可直接貼到 Console 應用程式中執行。程式碼包含上述所有步驟，並加入少許說明註解以提升可讀性。

```csharp
using System;
using Aspose.Cells;

namespace AsposeTableDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook.
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Add data to cells – this is the “add data to cells” part.
            worksheet.Cells["A1"].PutValue("Name");
            worksheet.Cells["B1"].PutValue("Score");
            worksheet.Cells["A2"].PutValue("Alice");
            worksheet.Cells["B2"].PutValue(85);
            worksheet.Cells["A3"].PutValue("Bob");
            worksheet.Cells["B3"].PutValue(92);

            // 3️⃣ Convert the range into a ListObject (i.e., create table from range).
            int startRow = 0, startColumn = 0, rowCount = 3, columnCount = 2;
            int listIdx = worksheet.ListObjects.Add(startRow, startColumn, rowCount, columnCount);
            ListObject table = worksheet.ListObjects[listIdx];
            table.ShowAutoFilter = true;   // optional UI filter

            // 4️⃣ Remove the AutoFilter UI – “save excel without filter”.
            table.AutoFilter = null;
            table.ShowAutoFilter = false;

            // 5️⃣ Save the workbook.
            string filePath = @"C:\Temp\NoAutoFilter.xlsx";
            workbook.Save(filePath);

            Console.WriteLine($"Workbook saved to {filePath}");
        }
    }
}
```

執行程式後，開啟 `C:\Temp\NoAutoFilter.xlsx`，即可看到格式良好的表格、沒有篩選箭頭，且資料與我們輸入的完全相同。這就是 **create excel workbook c#** 流程的全部內容，總計不到 60 行程式碼。

---

## Frequently Asked Questions & Edge Cases

**Q: 如果我的資料範圍不是連續的怎麼辦？**  
A: `ListObjects.Add` 需要矩形範圍。若資料不連續，請先將各段資料複製至新工作表形成暫時的連續範圍，再執行轉換。

**Q: 可以套用自訂的表格樣式嗎？**  
A: 當然可以。建立 `ListObject` 後，設定 `table.TableStyleType = TableStyleType.TableStyleMedium9;`（或任意 65 種內建樣式之一），即可讓表格符合企業品牌風格。

**Q: 想保留篩選功能但隱藏箭頭該怎麼做？**  
A: 篩選邏輯屬於 `table.AutoFilter`。將 `ShowAutoFilter = false` 只會隱藏 UI，實際的篩選條件仍然存在，之後仍可程式化地篩選列。

**Q: 大型資料集（10k+ 列）會有問題嗎？**  
A: API 本身支援大資料量，但建議在大量寫入前先關閉自動計算 (`workbook.CalcEngine = false`) 以提升效能，寫入完成後再重新啟用。

---

## Wrap‑Up

我們已完整說明如何在 C# 中使用 Aspose.Cells **create table from range**，從 **create excel workbook c#**、**add data to cells**、**convert range to ListObject**，最後 **save excel without filter**，一步步實作。程式碼已完整、可執行，且適合直接投入生產環境。

接下來，你可以進一步探索：

- 加入條件格式以突顯最高分數。  
- 使用 `workbook.Save("Report.pdf", SaveFormat.Pdf);` 將活頁簿匯出為 PDF。  
- 透過 `table.Columns["Score"].DataBodyRange.Sort` 程式化排序表格。

歡迎自行嘗試不同的資料集、表格樣式，或是多工作表的情境。Aspose.Cells API 足夠彈性，能處理從小型計分表到大型財務帳本的各種需求。

有任何問題或卡關嗎？歡迎在下方留言或於 GitHub 私訊我。祝開發順利，玩得開心，盡情把原始範圍變成精緻的 Excel 表格吧！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}