---
category: general
date: 2026-05-30
description: 快速填寫 Excel 範本，並學習如何使用 Aspose.Cells SmartMarker 將資料填入 Excel。完整的 C# 指南，附可執行程式碼。
draft: false
keywords:
- populate excel template
- fill excel with data
- Aspose.Cells SmartMarker
- automate Excel reporting
- C# Excel automation
language: zh-hant
og_description: 使用 Aspose.Cells SmartMarker 填寫 Excel 模板並填入資料。跟隨此一步一步的 C# 教學，即可立即獲得結果。
og_title: 填寫 Excel 模板 – 透過 SmartMarker 填入 Excel 資料
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Populate Excel template quickly and learn how to fill Excel with data
    using Aspose.Cells SmartMarker. Complete C# guide with runnable code.
  headline: Populate Excel Template – Fill Excel Data via SmartMarker
  type: TechArticle
- description: Populate Excel template quickly and learn how to fill Excel with data
    using Aspose.Cells SmartMarker. Complete C# guide with runnable code.
  name: Populate Excel Template – Fill Excel Data via SmartMarker
  steps:
  - name: Empty Collections
    text: 'If `Items` is empty, SmartMarker will leave the table header intact but
      won’t insert any rows. To avoid a blank space, you can add a conditional block:'
  - name: Custom Number Formats
    text: 'Sometimes you need currency symbols or thousands separators. After processing,
      you can apply a style programmatically:'
  - name: Large Data Sets
    text: 'For thousands of rows, enable the `UseFastMode` option to improve performance:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: 填寫 Excel 模板 – 透過 SmartMarker 填寫 Excel 數據
url: /zh-hant/net/smart-markers-dynamic-data/populate-excel-template-fill-excel-data-via-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 填寫 Excel 範本 – 透過 SmartMarker 填入 Excel 資料

有沒有需要 **填寫 Excel 範本**，卻不曉得如何自動化的情況？在本教學中，我們將示範如何使用 Aspose.Cells SmartMarker **填入 Excel 資料**——一個能將靜態活頁簿變成動態報表產生器的工具。

想像一下，你有一張預先設計好的發票表、銷售儀表板，或任何可重複使用的表單。與其手動輸入值，不如將 C# 物件傳入，讓 SmartMarker 完成繁重的工作。閱讀完本指南後，你將擁有一個完整可執行的專案，能夠讀取範本、注入列、合計，甚至套用條件格式，全部不需要觸碰 UI。

## 你將學會

- 如何準備與 Excel 範本標記相符的資料來源。  
- 如何實例化 **SmartMarkerProcessor** 並啟用範圍支援。  
- 如何使用巢狀集合（例如訂單項目）**填寫 Excel 範本**。  
- 處理空集合或自訂數字格式等邊緣情況的技巧。  

不需要外部服務、VBA 巨集——只要純粹的 C# 與 Aspose.Cells。所需環境為 .NET 6（或更新版本）以及 Aspose.Cells NuGet 套件。

## 前置條件

- Visual Studio 2022（或你慣用的任何 IDE）。  
- 已安裝 .NET 6 SDK。  
- Aspose.Cells for .NET（可從 Aspose 官網取得免費試用版）。  
- 一個帶有 SmartMarker 標記的基本 Excel 範本（我們稍後會建立）。

如果上述任一項目聽起來陌生，別擔心；以下步驟會逐一說明每個需求。

## 步驟 1：使用 SmartMarker 標記設計 Excel 範本

首先，開啟一個新活頁簿，佈局靜態部分——公司標誌、標題等。然後在需要動態資料的地方插入 SmartMarker 佔位符。

| 儲存格 | 內容 |
|------|---------|
| A1   | **Invoice** |
| A3   | `{{CompanyName}}` |
| A5   | **Order Details** |
| A7   | `{{Orders.Items.Name}}` |
| B7   | `{{Orders.Items.Qty}}` |
| C7   | `{{Orders.Items.Price}}` |
| D7   | `{{Orders.Items.Price * Orders.Items.Qty}}` |

**為什麼這很重要：** SmartMarker 會讀取雙大括號內的內容，並將其對應到稍後傳入物件的屬性。`Orders.Items` 集合告訴引擎對清單中的每個項目重複該列。

> **專業提示：** 當需要引擎自動展開範圍（例如會增減的表格）時，請使用 `RangeSmartMarker` 選項（我們稍後會啟用）。

將檔案儲存為 `InvoiceTemplate.xlsx`，放在專案的 `Resources` 資料夾下。

## 步驟 2：準備與範本標記相符的資料來源

現在建立一個 C# 匿名物件（或強型別類別），其屬性名稱必須與標記完全對應。關鍵是要精確鏡像層級結構。

```csharp
// Step 2: Prepare the data source that matches the template markers
var data = new
{
    CompanyName = "Acme Corp.",
    Orders = new[]
    {
        new
        {
            Items = new[]
            {
                new { Name = "Pen",   Qty = 2, Price = 1.5m },
                new { Name = "Notebook", Qty = 1, Price = 3.75m },
                new { Name = "Stapler",  Qty = 1, Price = 5.0m }
            }
        }
    }
};
```

**為什麼這很重要：** `Orders` 陣列包含單一訂單，而每筆訂單內有 `Items` 陣列。SmartMarker 會遍歷 `Items`，為每個元素克隆該列。若日後需要多筆訂單，只要在 `Orders` 陣列中加入更多物件即可——不必更改程式碼。

## 步驟 3：載入範本並建立 SmartMarkerProcessor 實例

資料備妥後，我們載入活頁簿、建立處理器，並告訴它遵守範圍標記。

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook
Workbook workbook = new Workbook("Resources/InvoiceTemplate.xlsx");

// Get the first worksheet (where our markers live)
Worksheet ws = workbook.Worksheets[0];

// Step 3: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

**為什麼這很重要：** `SmartMarkerProcessor` 是負責解析標記、展開範圍、寫入值的引擎。將處理器與活頁簿分離，可讓程式碼保持乾淨且可重複使用。

## 步驟 4：以啟用 RangeSmartMarker 的方式處理工作表

當呼叫 `Process` 時，魔法就會發生。設定 `RangeSmartMarker = true` 會讓 SmartMarker 把整列範圍視為可重複區塊，依需求自動插入或刪除列。

```csharp
// Step 4: Process the worksheet using SmartMarker with range support enabled
processor.Process(ws, data, new SmartMarkerOptions { RangeSmartMarker = true });
```

此時引擎已完成：

1. 掃描工作表中的 `{{...}}` 標記。  
2. 將每個標記對映到 `data` 物件的屬性。  
3. 偵測表格範圍 (A7:D7) 並依項目數量複製三次。  
4. 計算 `Price * Qty` 表達式以產生總計欄位。

## 步驟 5：儲存產生的活頁簿

最後，將填寫好的活頁簿寫入磁碟（或回傳給 Web 用戶端）。

```csharp
// Step 5: Save the populated workbook
workbook.Save("Output/InvoicePopulated.xlsx");
```

開啟 `InvoicePopulated.xlsx`，你會看到一張整齊填好的表格：

| 名稱      | 數量 | 單價 | 總計 |
|-----------|-----|-------|-------|
| Pen       | 2   | 1.5   | 3.00 |
| Notebook  | 1   | 3.75  | 3.75 |
| Stapler   | 1   | 5.00  | 5.00 |

**填寫 Excel 範本** 的步驟已完成，你也成功 **填入 Excel 資料**，不論列數多少皆可。

## 處理常見邊緣情況

### 空集合

如果 `Items` 為空，SmartMarker 會保留表頭但不插入任何列。為避免留下空白，可加入條件區塊：

```csharp
{{#if Orders.Items.Length > 0}}
    ... table rows ...
{{else}}
    No items were ordered.
{{/if}}
```

### 自訂數字格式

有時需要貨幣符號或千位分隔符。處理完畢後，可程式化套用樣式：

```csharp
Style style = workbook.CreateStyle();
style.Number = 164; // Built‑in currency format
StyleFlag flag = new StyleFlag { NumberFormat = true };

foreach (Cell cell in ws.Cells["C8:D12"])
{
    cell.SetStyle(style, flag);
}
```

### 大量資料集

若需處理數千列，啟用 `UseFastMode` 選項以提升效能：

```csharp
processor.Process(ws, data, new SmartMarkerOptions { 
    RangeSmartMarker = true,
    UseFastMode = true
});
```

## 完整範例程式

以下是可直接貼到 Console App 的完整、獨立程式碼，包含所有 using 陳述式、資料準備、處理與儲存。

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace ExcelSmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the Excel template
            Workbook workbook = new Workbook("Resources/InvoiceTemplate.xlsx");
            Worksheet ws = workbook.Worksheets[0];

            // 2️⃣ Prepare the data source
            var data = new
            {
                CompanyName = "Acme Corp.",
                Orders = new[]
                {
                    new
                    {
                        Items = new[]
                        {
                            new { Name = "Pen",      Qty = 2, Price = 1.5m },
                            new { Name = "Notebook", Qty = 1, Price = 3.75m },
                            new { Name = "Stapler",  Qty = 1, Price = 5.0m }
                        }
                    }
                }
            };

            // 3️⃣ Create the processor
            SmartMarkerProcessor processor = new SmartMarkerProcessor();

            // 4️⃣ Process with range support
            processor.Process(ws, data, new SmartMarkerOptions { RangeSmartMarker = true });

            // 5


## 接下來該學什麼？

- [Populate Excel with Data Using Aspose.Cells and Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [How to Populate Excel Cells with Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/cell-operations/aspose-cells-dotnet-populate-excel-data/)
- [Automate Excel Data Export Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}