---
category: general
date: 2026-03-22
description: 如何在 C# 中使用主從模板產生 Excel 報表。快速學習使用 C# 填充 Excel 模板，並利用 SmartMarker 產生可重複的工作表。
draft: false
keywords:
- how to generate excel report
- populate excel template c#
- excel smartmarker c#
- master detail excel c#
- c# excel automation
language: zh-hant
og_description: 如何使用可重用模板在 C# 中產生 Excel 報表。此逐步指南會示範如何以主從資料填充 C# 的 Excel 模板。
og_title: 如何在 C# 中生成 Excel 報表 – 完整 SmartMarker 教程
tags:
- Excel
- C#
- SmartMarker
- Reporting
title: 如何在 C# 中生成 Excel 報表 – 使用 SmartMarker 的完整指南
url: /zh-hant/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中產生 Excel 報表 – 使用 SmartMarker 的完整指南

有沒有想過 **如何在 C# 中產生 Excel 報表**，而不必寫無盡的逐格程式碼？你並不是唯一有此疑問的人。大多數開發者在需要一份精緻、具多工作表且呈現主從關係的報表時（例如訂單與明細項目），常會卡關，卻又不想每次都重新發明輪子。

好消息是？只要有現成的 Excel 範本加上 Aspose.Cells 的 **SmartMarker** 引擎，你就能在幾行程式碼內 **populate Excel template C#**。在本教學中，我們將逐步示範真實情境、說明每一步的重要性，並提供一個完整、可直接執行的範例，讓你今天就能複製貼上使用。

> **你將得到：** 一份主從式 Excel 報表，每筆訂單會產生自己的工作表，全部由純 C# 物件驅動。無需手動迴圈處理儲存格，也不會有脆弱的公式——只有乾淨且易於維護的程式碼。

---

## 前置條件

Before we dive in, make sure you have:

- **.NET 6.0**（或更新版本）已安裝 – 程式碼以 .NET 6 為目標，但同樣可在 .NET Framework 4.7+ 上執行。
- **Aspose.Cells for .NET** NuGet 套件 (`Install-Package Aspose.Cells`) – 提供 `Workbook`、`SmartMarkerProcessor` 以及相關類別。
- 一個名為 **MasterDetailTemplate.xlsx** 的 Excel 檔案，放置於 `YOUR_DIRECTORY`。它應在第一張工作表包含如 `{{Orders.OrderId}}` 的 SmartMarker 區塊，並在明細項目上有嵌套區塊 `{{Orders.Items.Prod}}`。
- 對 C# 匿名型別有基本了解 – 我們將使用它來建模訂單與明細項目。

如果上述任一項目聽起來陌生，別擔心。我們稍後會提及替代方案（例如使用 EPPlus），但核心概念不變。

## 步驟 1：載入包含 SmartMarker 區塊的 Excel 範本

We first open the template file. Think of the template as a skeleton; SmartMarker will later flesh it out with real data.

```csharp
using Aspose.Cells;

// Load the template containing SmartMarker tags
var workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");
```

**為什麼這很重要：** 透過將版面配置（範本）與資料（C# 物件）分離，設計師與開發者都能保持快樂。設計師可以在不觸碰程式碼的情況下調整字型、顏色或公式。

## 步驟 2：建立主從資料來源

Next, we create the data that will populate the template. For a typical order report, you have a collection of orders, each with its own collection of items.

```csharp
// Master‑detail data: a list of orders, each with a list of items
var masterDetailData = new
{
    Orders = new[]
    {
        new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Prod = "A", Qty = 2 },
                new { Prod = "B", Qty = 1 }
            }
        },
        new
        {
            OrderId = 2,
            Items = new[]
            {
                new { Prod = "C", Qty = 5 }
            }
        }
    }
};
```

> **專業提示：** 若需在多個報表間重複使用，請改用強型別類別而非匿名型別。匿名型別的寫法讓範例更簡潔。

**為什麼這很重要：** SmartMarker 透過比對屬性名稱（`Orders`、`OrderId`、`Items`、`Prod`、`Qty`）與範本中的佔位符來運作。階層必須完全對應，否則引擎會跳過相關區段。

## 步驟 3：指示 SmartMarker 為每筆主記錄建立新工作表

By default SmartMarker writes all rows into a single sheet. We want each order on its own worksheet, which is perfect for printing or emailing per‑order PDFs later.

```csharp
// Enable a separate sheet for each master (order) record
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableRepeatingSheet = true // each Order gets its own sheet
};
```

**為什麼這很重要：** `EnableRepeatingSheet` 免除手動複製工作表的需求。引擎會複製原始工作表、注入訂單資料，並自動重新命名工作表（通常使用第一欄的值）。

## 步驟 4：使用資料處理範本

Now we bind everything together. The `SmartMarkerProcessor` walks through the workbook, replaces tags, and creates new sheets as instructed.

```csharp
// Apply the data to the workbook
workbook.Worksheets[0].SmartMarkerProcessor.Process(masterDetailData, smartMarkerOptions);
```

**為什麼這很重要：** 這一行程式碼完成了繁重的工作——解析範本、遍歷集合、處理巢狀表格。它就是 **populate Excel template C#** 的核心，無需任何手動迴圈。

## 步驟 5：儲存完成的報表

Finally, write the populated workbook to disk. You can also stream it directly to an HTTP response for web apps.

```csharp
// Save the generated report
workbook.Save("YOUR_DIRECTORY/MasterDetailResult.xlsx");
```

**為什麼這很重要：** 儲存為檔案可得到可直接在 Excel 開啟、與利害關係人分享，或供後續流程（如 PDF 轉換）使用的實體成果。

## 完整可執行範例（直接複製貼上）

Below is the complete program, including `using` directives and a `Main` method. Drop it into a console app, adjust the file paths, and run.

```csharp
using System;
using Aspose.Cells;

namespace ExcelReportDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template
            var workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");

            // 2️⃣ Build master‑detail data
            var masterDetailData = new
            {
                Orders = new[]
                {
                    new
                    {
                        OrderId = 1,
                        Items = new[]
                        {
                            new { Prod = "A", Qty = 2 },
                            new { Prod = "B", Qty = 1 }
                        }
                    },
                    new
                    {
                        OrderId = 2,
                        Items = new[]
                        {
                            new { Prod = "C", Qty = 5 }
                        }
                    }
                }
            };

            // 3️⃣ Enable a new sheet per order
            var smartMarkerOptions = new SmartMarkerOptions
            {
                EnableRepeatingSheet = true
            };

            // 4️⃣ Process the template with data
            workbook.Worksheets[0].SmartMarkerProcessor.Process(masterDetailData, smartMarkerOptions);

            // 5️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/MasterDetailResult.xlsx");

            Console.WriteLine("Excel report generated successfully!");
        }
    }
}
```

### 預期輸出

When you open `MasterDetailResult.xlsx` you’ll see:

- **工作表 “Order_1”** – 包含訂單 1 的標頭以及產品 A 與 B 的兩筆資料列。
- **工作表 “Order_2”** – 包含訂單 2 的標頭以及產品 C 的單筆資料列。
- 原始範本中的所有公式、格式與圖表皆被保留。

![每筆訂單分別工作表的 Excel 報表 – 已填充活頁簿範例](/images/excel-report-example.png "產生的 Excel 報表（主從資料）")

*圖片說明：已產生的 Excel 報表，每筆訂單分別在不同工作表，展示如何使用 C# 與 SmartMarker 產生 Excel 報表。*

## 常見問題與邊緣案例

### 如果我需要一個靜態工作表（例如彙總）與重複工作表同時存在怎麼辦？

僅在包含主區塊的工作表上將 `EnableRepeatingSheet = true` **設定**。其他工作表將保持不變，這樣你就能在原始範本中保留彙總頁面。

### 我可以使用 DataTable 取代匿名物件嗎？

當然可以。SmartMarker 能與任何實作 `IEnumerable` 的物件一起使用。只要將匿名型別換成 `DataTable`，並確保欄位名稱與標籤相符即可。

```csharp
DataTable ordersTable = GetOrdersFromDatabase();
var data = new { Orders = ordersTable };
```

### 如何變更產生工作表的命名慣例？

實作自訂的 `ISmartMarkerSheetNaming` 介面（或在處理完畢後操作 `workbook.Worksheets`）。大多數開發者會直接根據儲存格的值重新命名工作表：

```csharp
foreach (var sheet in workbook.Worksheets)
{
    sheet.Name = $"Order_{sheet.Cells["A1"].StringValue}";
}
```

### 如果我的範本使用不同的佔位符語法怎麼辦？

SmartMarker 允許透過 `SmartMarkerOptions` 設定自訂分隔符。例如，改用 `<< >>` 取代 `{{ }}`：

```csharp
smartMarkerOptions.StartTag = "<<";
smartMarkerOptions.EndTag = ">>";
```

## 擴展此方法的技巧

- **在記憶體中快取範本**，如果每個請求需要產生多份報表；每次從磁碟載入會增加延遲。
- **結合 PDF 轉換**（`workbook.Save("report.pdf", SaveFormat.Pdf)`）以產生適合電郵的輸出。
- **參數化檔案路徑**，使用設定檔或環境變數，使解決方案在開發、測試與正式環境間皆可移植。
- **單元測試資料層**，將其獨立測試；SmartMarker 本身是確定性的，你只需驗證輸入資料符合預期的結構。

## 結論

我們已完整說明 **如何在 C# 中產生 Excel 報表**，從載入支援 SmartMarker 的範本，到儲存具主從關係的多工作表活頁簿。只要以少量程式碼 **populate Excel template C#**，即可避免脆弱的逐格程式邏輯，並讓設計師自由打造最終外觀。

接下來，你可以探索：

- 使用 **populate Excel template C#** 搭配會依工作表自動更新的圖表。
- 將 **excel smartmarker c#** 整合至 ASP.NET Core，以直接串流報表至瀏覽器。
- 自動化 **c# excel automation** 工作流程，從 API 或資料庫取得資料。

試試看，微調範本，便能快速將原始資料轉換為精緻的 Excel 報表。有任何問題或酷炫的使用案例嗎？在下方留下評論吧——祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}