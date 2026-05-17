---
category: general
date: 2026-02-21
description: 使用 SmartMarker 快速在 Excel 中重複資料——學習如何輕鬆填充 Excel 模板並重複列。
draft: false
keywords:
- repeat data in excel
- populate excel template
- how to repeat rows
- repeat rows in excel
- populate excel from data
language: zh-hant
og_description: 使用 SmartMarker 在 Excel 中重複資料。學習如何填充 Excel 模板、重複列以及自動化您的試算表。
og_title: 在 Excel 中重複資料 – 使用 SmartMarker 填充模板
tags:
- excel
- csharp
- smartmarker
- automation
title: 在 Excel 中重複資料 – 使用 SmartMarker 填充範本
url: /zh-hant/net/smart-markers-dynamic-data/repeat-data-in-excel-populate-template-with-smartmarker/
---

codes.

Make sure to keep all shortcodes unchanged.

Now produce final content.

Let's craft translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中重複資料 – 使用 SmartMarker 填充範本

是否曾需要在 **Excel 中重複資料** 卻不知如何避免手動複製貼上？你並不孤單。在許多報告情境下，你會有一個項目清單必須自動展開成多列，手動操作很容易出錯。

事實上，只要使用 **GemBox.Spreadsheet** 函式庫中的 SmartMarkerProcessor，就能以一行 C# 程式碼 **填充 Excel 範本**，並讓每個集合項目自動產生重複的列。本指南將逐步說明操作步驟、完整程式碼，並解釋每個環節的意義，讓你能輕鬆在 Excel 中重複列而不費吹灰之力。

## 你將學到

* 如何定義驅動重複操作的資料結構。  
* 如何將 `SmartMarkerProcessor` 與包含隱藏範本工作表的活頁簿掛勾。  
* `${Repeat:Item}` 標記如何自動展開為多列。  
* 處理空集合或自訂格式等邊緣情況的技巧。  

完成本教學後，你將能以可擴充、易維護且適用於任何 .NET 專案的方式 **從資料填充 Excel**。

---

## 前置條件

* .NET 6.0 或更新版本（程式碼使用現代 C# 功能）。  
* **GemBox.Spreadsheet** NuGet 套件（免費版支援至 150 列）。  
* 一個包含隱藏工作表 `HiddenTemplate` 的基本 Excel 範本檔 (`Template.xlsx`)。  
* 具備 C# 物件與 LINQ 基礎知識較佳，但非必須。

---

## Step 1 – 定義重複資料結構

首先，你需要一個 SmartMarker 引擎可以遍歷的資料來源。實務上通常來自資料庫、API 或 CSV 檔。為了說明，我們使用一個匿名型別，裡面只有一個名為 `Item` 的字串陣列屬性。

```csharp
// Step 1: Define the data that will be repeated in the template
var repeatData = new { Item = new[] { "A", "B", "C" } };
```

> **為什麼這很重要：** Excel 範本內的 `${Repeat:Item}` 標記會尋找名為 `Item` 的屬性。若你更改屬性名稱，請同步更新標記。這種緊密耦合確保範本與程式碼保持一致，讓你在 **填充 Excel 範本** 時不必猜測欄位名稱。

### 常見變形

* **複雜物件：** 除了簡單的字串陣列，你也可以提供物件清單（`new[] { new { Name = "A", Qty = 10 } }`）。標記會重複列，且可在工作表中使用 `${Item.Name}` 與 `${Item.Qty}`。  
* **空集合：** 若 `Item` 為空，SmartMarker 只會移除重複區塊，保留原始範本——非常適合可選區段。

## Step 2 – 為隱藏範本工作表建立 SmartMarkerProcessor

接著，載入活頁簿並實例化 `SmartMarkerProcessor`。指向包含隱藏範本工作表的活頁簿；SmartMarker 會將該工作表複製為可見工作表，並展開重複標記。

```csharp
using GemBox.Spreadsheet;

// Load the workbook that holds the hidden template sheet.
var wb = ExcelFile.Load("Template.xlsx");

// Step 2: Create a SmartMarkerProcessor for the workbook that holds the hidden template sheet
var processor = new SmartMarkerProcessor(wb);
```

> **專業提示：** 若同一檔案內有多個範本，可在呼叫 `processor.Process` 時指定來源工作表名稱。這在需要為報表不同區段 **在 Excel 中重複列** 時非常有用。

### 邊緣案例處理

* **找不到範本工作表：** 將載入程式碼包在 try/catch 中，並記錄清晰的錯誤訊息——可避免檔案路徑錯誤導致的沉默失敗。  
* **大型資料集：** 若需處理上千列，建議將輸出串流寫入檔案（`processor.Save`），而非全部保留在記憶體中。

## Step 3 – 套用資料並展開 `${Repeat:Item}` 標記

現在只要一行魔法程式碼即可真正重複列。將 Step 1 中建立的物件傳入 `processor.Process`。SmartMarker 會找出每個 `${Repeat:Item}` 標記，為每個元素複製列，並以實際值取代佔位符。

```csharp
// Step 3: Apply the data to the template, expanding the ${Repeat:Item} marker
processor.Process(repeatData);

// Save the resulting workbook.
wb.Save("Result.xlsx");
```

### 你應該看到的結果

開啟 `Result.xlsx` 後，隱藏的範本工作表已被複製為一個新的可見工作表（預設名稱為 `Sheet1`）。原本包含 `${Repeat:Item}` 的列現在出現三次，儲存格分別顯示 **A**、**B**、**C**。

| 項目 |
|------|
| A    |
| B    |
| C    |

若你在範本中加入 `${Item.Price}` 等其他欄位，系統會自動從資料來源填入相應值。

## 如何在不使用 SmartMarker 的情況下在 Excel 中重複列（快速比較）

| 方法                     | 程式碼複雜度 | 維護性 | 效能   |
|--------------------------|--------------|--------|--------|
| 手動複製貼上             | 高           | 低     | 差     |
| VBA 巨集                 | 中           | 中     | 良好   |
| **SmartMarkerProcessor** | 低           | 高     | 優秀   |

如表所示，使用 SmartMarker 來 **在 Excel 中重複資料** 能提供最乾淨的範本設計與業務邏輯分離。此概念亦可跨語言使用，類似功能在 Java、Python、JavaScript 等函式庫中皆有實作。

## 進階技巧與常見陷阱

### 1. 格式化重複的列

SmartMarker 會複製整列，包括儲存格樣式、框線與條件格式。若需為首列或末列套用不同樣式，可加入 `${If:Item.IsFirst}` 等額外標記，並在 Excel 內使用條件公式。

### 2. 處理大型資料集

處理超過 10 000 列時，建議在處理前先停用 Excel 的自動計算功能：

```csharp
wb.WorkbookOptions = new WorkbookOptions { RecalculateAllFormulas = false };
```

處理完畢並儲存後再重新啟用，以保持效能。

### 3. 從真實資料庫填充 Excel

```csharp
var orders = dbContext.Orders
    .Where(o => o.Date >= start && o.Date <= end)
    .Select(o => new { o.OrderId, o.CustomerName, o.Total })
    .ToArray();

processor.Process(new { Order = orders });
```

然後在範本中使用 `${Repeat:Order}` 來列出每筆訂單。此模式展示了如何直接從 Entity Framework **從資料填充 Excel**。

### 4. 使用多個重複區塊

同一工作表或不同工作表上可以放置多個 `${Repeat:...}` 標記。SmartMarker 會依序處理，只有在某個區塊依賴另一個區塊的輸出時，順序才會產生影響。

## 完整可執行範例

以下是一個可直接貼到 Visual Studio 並立即執行的主控台應用程式，示範所有三個步驟以及檔案儲存。

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License free version (up to 150 rows). For production use, set your license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Define the data to repeat.
        var repeatData = new { Item = new[] { "A", "B", "C" } };

        // 2️⃣ Load the template workbook (ensure Template.xlsx exists next to the exe).
        var wb = ExcelFile.Load("Template.xlsx");

        // Create processor bound to the workbook.
        var processor = new SmartMarkerProcessor(wb);

        // 3️⃣ Process the data – this expands the ${Repeat:Item} marker.
        processor.Process(repeatData);

        // Save the populated workbook.
        wb.Save("Result.xlsx");

        Console.WriteLine("Excel file generated successfully – check Result.xlsx");
    }
}
```

**預期輸出：** `Result.xlsx` 內的工作表會出現三次 `${Repeat:Item}` 所在的列，分別顯示 A、B、C。無需任何手動調整。

## 結論

現在你已掌握如何透過 SmartMarkerProcessor **在 Excel 中重複資料**，只要定義簡單的資料物件、載入範本活頁簿，並呼叫 `Process`，即可 **填充 Excel 範本**、**在 Excel 中重複列**，以及一般的 **...**（此處內容略） 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}