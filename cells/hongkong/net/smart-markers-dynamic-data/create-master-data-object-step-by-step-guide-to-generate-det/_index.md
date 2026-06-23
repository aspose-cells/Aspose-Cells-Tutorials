---
category: general
date: 2026-02-14
description: 在 C# 中建立主資料物件，輕鬆產生明細表。透過實用程式碼範例，學習完整的 SmartMarker 工作流程。
draft: false
keywords:
- create master data object
- generate detail sheet
- smartmarker processing
- worksheet automation
- c# data binding
language: zh-hant
og_description: 在 C# 中建立主資料物件，並使用 SmartMarker 產生詳細工作表。跟隨我們的詳細教學，即可獲得可直接執行的解決方案。
og_title: 建立主資料物件 – 完整指南
tags:
- C#
- SmartMarker
- Excel Automation
title: 建立主資料物件 – 逐步指南產生明細表
url: /zh-hant/net/smart-markers-dynamic-data/create-master-data-object-step-by-step-guide-to-generate-det/
---

.SaveAsPdf(...)`" => "使用 `workbook.SaveAsPdf(...)` 將產生的活頁簿匯出為 PDF"

Final sentence: "Feel free to experiment, break things, and then bring them back together. That’s the fastest way to master worksheet automation. Happy coding!" => "盡情試驗、打破再重組吧。這是掌握工作表自動化的最快方式。祝開發愉快！"

Now ensure we keep shortcodes at start and end.

Also preserve the backticks and code placeholders.

Make sure to keep the markdown list formatting.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立主資料物件 – 完整教學

有沒有曾經需要為 Excel 工作表 **建立主資料物件**，卻不確定如何將它連結到 SmartMarker 明細工作表？你並不孤單。在許多報表情境中，主物件會驅動動態的明細工作表，而正確的配接往往感覺像在沒有圖示的情況下拼拼圖。  

本指南將逐步說明完整流程——建立主資料物件、設定 SmartMarker 選項以 **產生明細工作表**，最後執行處理器。完成後，你將擁有一段可直接貼入任何使用 GrapeCity Documents for Excel (GcExcel) 函式庫的 .NET 專案的可執行程式碼片段。

## 你需要的條件

- .NET 6+ (or .NET Framework 4.7.2) with a reference to `GcExcel.dll`
- Basic C# familiarity (variables, anonymous types, object initializers)
- An Excel workbook that already contains SmartMarker tags like `{{OrderId}}` and a table for line items
- Visual Studio, Rider, or any editor you prefer

就這樣——除了核心 GcExcel 發行版外，無需額外的 NuGet 套件。

## Step 1: Create the Master Data Object

首先，你必須 **建立主資料物件**，其結構需與 SmartMarker 標記所期待的相符。可以把它想像成一個小型的記憶體內報表模型。

```csharp
// Step 1: Build the master data object that feeds the SmartMarkers.
// It contains an OrderId and a collection of line items.
var orderData = new
{
    OrderId = 1,
    Items = new[]
    {
        new { Product = "A", Quantity = 2 },
        new { Product = "B", Quantity = 5 }
    }
};
```

為什麼在此使用匿名型別？因為它允許你在不宣告完整類別的情況下定義輕量級容器——非常適合快速示範或資料形狀不太可能變動的情況。日後若需要可重複使用的模型，只要把 `var` 換成正式的 POCO 即可。

> **小技巧：**保持屬性名稱（`OrderId`、`Product`、`Quantity`）與工作表中的佔位符完全相同；SmartMarker 會不分大小寫進行匹配。

## Step 2: Configure SmartMarker Options to Generate a Detail Sheet

現在我們告訴 SmartMarker 我們需要為明細項目表格建立一個獨立的工作表。這時 **generate detail sheet** 關鍵字就會發揮作用。

```csharp
// Step 2: Set up SmartMarker options.
// Enabling DetailSheet creates a new sheet for each master record.
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheet = true,
    // The new sheet will be named using the OrderId value.
    DetailSheetNewName = "Order_{OrderId}"
};
```

`DetailSheetNewName` 模式使用大括號佔位符，會在執行時替換。以我們的範例來說，工作表會被命名為 `Order_1`。若之後遍歷多筆訂單，每筆都會產生自己的分頁——正是大多數會計師所期待的行為。

## Step 3: Run the SmartMarker Processor

資料與選項都準備好後，最後一步是對目標工作表呼叫處理器。

```csharp
// Step 3: Execute SmartMarker processing on the worksheet.
// 'worksheet' is an IWorksheet instance that points to the template sheet.
worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);
```

在背後，SmartMarker 會掃描工作表中的標記，注入 `orderData` 的值，且因為 `DetailSheet` 為 `true`，它會將範本複製成名為 `Order_1` 的新工作表。所有明細項目會顯示在明細區域，且保留你在範本中設定的任何格式。

### Full Working Example

以下是一個獨立的 Console 程式，會開啟範本活頁簿（`Template.xlsx`），執行上述三個步驟，並將結果儲存為 `Result.xlsx`。你可以將它複製貼上到新的 Console 專案，然後按 **F5** 執行。

```csharp
using System;
using GrapeCity.Documents.Excel;

class Program
{
    static void Main()
    {
        // Load the Excel template that contains SmartMarker tags.
        var workbook = new Workbook();
        workbook.Open("Template.xlsx");

        // -------------------------------------------------
        // Step 1: Create the master data object.
        // -------------------------------------------------
        var orderData = new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Product = "A", Quantity = 2 },
                new { Product = "B", Quantity = 5 }
            }
        };

        // -------------------------------------------------
        // Step 2: Configure SmartMarker options to generate detail sheet.
        // -------------------------------------------------
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheet = true,
            DetailSheetNewName = "Order_{OrderId}"
        };

        // -------------------------------------------------
        // Step 3: Process the worksheet.
        // -------------------------------------------------
        // Assume the first sheet holds the master template.
        var worksheet = workbook.Worksheets[0];
        worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);

        // Save the populated workbook.
        workbook.Save("Result.xlsx");
        Console.WriteLine("Done! Check Result.xlsx – a new sheet named Order_1 should exist.");
    }
}
```

#### Expected Output

- **Result.xlsx** 內含名為 `Order_1` 的工作表。
- 儲存格 `A1`（或你放置 `{{OrderId}}` 的位置）現在顯示 `1`。
- 從 SmartMarker 區塊開始的表格列出兩筆資料：
  | Product | Quantity |
  |---------|----------|
  | A       | 2        |
  | B       | 5        |

如果你開啟檔案，會看到來自範本的格式仍然保留——框線、字型、條件格式……全部完整。

## 常見問題與邊緣案例

### 如果有多筆訂單怎麼辦？

將主物件包在集合中，讓 SmartMarker 自動迭代：

```csharp
var orders = new[]
{
    new {
        OrderId = 1,
        Items = new[] { new { Product = "A", Quantity = 2 } }
    },
    new {
        OrderId = 2,
        Items = new[] { new { Product = "C", Quantity = 3 } }
    }
};

worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);
```

每筆訂單會產生自己的工作表（`Order_1`、`Order_2`…）。處理器會將外層陣列視為主集合。

### 如何控制工作表的位置？

設定 `smartMarkerOptions.DetailSheetInsertIndex = 2;` 可將新工作表放在第二個分頁之後，或使用 `DetailSheetInsertAfter = "Summary"` 於指定名稱的工作表之後插入。

### 可以在特定執行時停用明細工作表嗎？

只要將 `DetailSheet = false;` 切換即可。SmartMarker 會將明細項目寫入與主標記同一個工作表。

### 大量資料集該怎麼處理？

SmartMarker 能有效串流資料，但若超過數十萬列，可能會觸及 Excel 的 1,048,576 列上限。此時可將資料分割成多筆主記錄，或考慮匯出為 CSV。

## Visual Overview

![Diagram illustrating how to create master data object and generate detail sheet using SmartMarker](/images/smartmarker-flow.png)

*此圖示說明了從 C# 主物件 → SmartMarker 選項 → 工作表處理 → 新的明細工作表的流程。*

## 結論

現在你已了解如何在 C# 中 **建立主資料物件**，以及如何設定 SmartMarker 自動 **產生明細工作表**。資料、選項、處理器的三步驟模式涵蓋了大多數使用 GcExcel 的 Excel 自動化情境。  

接下來，你可以探索：

- 為每個明細工作表加入頁首/頁尾資料
- 根據訂單狀態使用條件格式
- 使用 `workbook.SaveAsPdf(...)` 將產生的活頁簿匯出為 PDF

盡情試驗、打破再重組吧。這是掌握工作表自動化的最快方式。祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}