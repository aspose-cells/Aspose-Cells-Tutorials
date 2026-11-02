---
category: general
date: 2026-05-23
description: 使用範本和 JSON 資料建立動態 Excel 表格。學習如何載入 Excel 範本、自動化 Excel 報表，並快速從 JSON 填充
  Excel。
draft: false
keywords:
- create dynamic excel table
- load excel template
- automate excel report
- populate excel from json
- generate excel report json
language: zh-hant
og_description: 只需幾分鐘，即可使用範本和 JSON 建立動態 Excel 表格。本教學示範如何載入 Excel 範本、自動化 Excel 報表，並從
  JSON 填充 Excel。
og_title: 建立動態 Excel 表格 – 智慧標記指南
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create dynamic excel table using a template and JSON data. Learn how
    to load excel template, automate excel report, and populate excel from json quickly.
  headline: Create Dynamic Excel Table – Smart Marker Guide
  type: TechArticle
tags:
- Excel
- Smart Markers
- JSON
- .NET
title: 建立動態 Excel 表格 – 智慧標記指南
url: /zh-hant/net/smart-markers-dynamic-data/create-dynamic-excel-table-smart-marker-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立動態 Excel 表格 – Smart Marker 指南

是否曾需要**建立動態 Excel 表格**，讓它能自動為資料集中的每筆記錄擴展？您並非唯一有此需求的人。無論您是在建立每月銷售儀表板或是客戶別的發票套件，能夠**從 JSON 填充 Excel**而不必編寫無盡迴圈，都能節省大量時間。

在本教學中，我們將逐步示範完整且實作導向的解決方案，說明如何**載入 Excel 範本**、嵌入 Smart Marker、提供 JSON，最後**自動化 Excel 報表**的產生。完成後，您將擁有一個可直接執行的 .NET 專案，能從單一 JSON 資料產出精緻的 Excel 活頁簿。

---

## 您需要的工具

- **Aspose.Cells for .NET**（或任何支援 Smart Markers 的函式庫）。範例使用 24.5 版，但任何較新的版本皆可運作。
- Visual Studio 2022（或您喜愛的 C# IDE）。
- 放置於您可控制的資料夾中的簡易 Excel 範本檔案（`template.xlsx`）。
- 含有名為 `Customers` 集合的 JSON 字串。

就這樣——不需要額外服務、不需資料庫連線，只有純粹的程式碼。

---

## 步驟 1：建立範本活頁簿 – 載入 Excel 範本

我們首先要**載入 Excel 範本**至記憶體。將範本想像成畫布，其中的特殊佔位符會告訴處理器何處需要重複列。

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook (make sure the path is correct)
Workbook workbook = new Workbook(@"C:\Reports\template.xlsx");

// Grab the first worksheet – this is where our Smart Marker lives
Worksheet worksheet = workbook.Worksheets[0];
```

> **為什麼這很重要**：只載入一次範本即可減少檔案 I/O，並讓您在多份報表中重複使用相同版面配置。它同時將 Smart Marker 邏輯與其他程式碼分離，實現了關注點的清晰分離。

---

## 步驟 2：插入 Smart Marker – 建立動態 Excel 表格

現在我們嵌入一個**Smart Marker**，它會為 `Customers` 集合中的每筆資料重複整個表格。語法 `${Customers.RepeatWorksheet}` 會指示 Aspose.Cells 為每位客戶複製整個工作表。

```csharp
// Place the Smart Marker in cell A1 (top‑left corner)
worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");
```

> **專業提示**：如果只需要重複列而非整個工作表，請在表格的第一列使用 `${Customers.Repeat}`。工作表層級的重複在每位客戶需要獨立分頁時相當方便。

---

## 步驟 3：準備 SmartMarkerProcessor – 自動化 Excel 報表

標記就緒後，我們建立 `SmartMarkerProcessor`。此物件負責協調 JSON 與 Excel 範本之間的資料繫結。

```csharp
// Initialize the processor with the workbook that contains the marker
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
```

此處理器相當輕量，若需要，可重複使用於多個 JSON 資料。

---

## 步驟 4：提供 JSON 資料 – 從 JSON 填充 Excel

這裡就是魔法發生的地方。我們提供一個包含客戶陣列的 JSON 字串。每位客戶可包含 `Name`、`Email`、`Total` 等欄位。

```csharp
// Sample JSON data – in a real scenario you might read this from a file or API
string customersJson = @"
{
  ""Customers"": [
    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
  ]
}";

// Apply the JSON to the processor – this populates the workbook
processor.ApplyJson(customersJson);
```

> **為什麼使用 JSON？** JSON 與語言無關，且易於從 API、資料庫或手動輸入產生。使用 `ApplyJson` 表示您不必手動映射物件；處理器會自行完成繁重的工作。

---

## 步驟 5：儲存結果 – 產生 Excel 報表 JSON

最後，我們將填充好的活頁簿寫入磁碟。輸出檔案現在包含每位客戶各自的工作表，且每個工作表皆填入我們的 JSON 資料。

```csharp
// Save the filled workbook – choose a path that makes sense for your app
workbook.Save(@"C:\Reports\output.xlsx");
```

### 預期輸出

- **output.xlsx** 會有三個工作表，名稱分別為 `Sheet1`、`Sheet2`、`Sheet3`（或依您範本的命名規則）。
- 每個工作表會顯示單一客戶的 `Name`、`Email`、`Total` 值。
- 您在 `template.xlsx` 中設計的版面配置（標頭、樣式、公式）會在所有產生的工作表中保留。

---

## 完整範例程式

以下是完整、可直接執行的程式。將其複製貼上至 Console 應用程式，調整檔案路徑，然後按 **F5**。

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace DynamicExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template workbook
            string templatePath = @"C:\Reports\template.xlsx";
            Workbook workbook = new Workbook(templatePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Insert the Smart Marker that repeats the worksheet per customer
            worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");

            // 3️⃣ Create the SmartMarkerProcessor
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

            // 4️⃣ JSON data containing a collection of customers
            string customersJson = @"
            {
                ""Customers"": [
                    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
                    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
                    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
                ]
            }";

            // Apply the JSON – this populates the workbook dynamically
            processor.ApplyJson(customersJson);

            // 5️⃣ Save the generated report
            string outputPath = @"C:\Reports\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Dynamic Excel report generated at: {outputPath}");
        }
    }
}
```

執行程式，開啟 `output.xlsx`，您將看到**建立動態 Excel 表格**的實際效果——每位客戶都有自己的工作表，且完全依您設計的格式呈現。

---

## 常見問題與邊緣情況

| Question | Answer |
|----------|--------|
| *如果我的 JSON 有巢狀物件呢？* | Smart Markers 支援點號表示法（`${Customers.Address.City}`），只要 JSON 結構相符即可。 |
| *我可以將產生的工作表以客戶名稱命名嗎？* | 可以——在工作表名稱儲存格加入 `${Customers.Name}` 標記，或在 `processor.ApplyJson(customersJson, "Customers")` 時使用命名模式。 |
| *大量資料集（10 k+ 列）該怎麼處理？* | 處理器會有效率地串流資料，但仍需留意記憶體使用。若遇到效能瓶頸，建議將報表拆分為多個檔案。 |
| *使用 Aspose.Cells 是否需要授權？* | 免費評估版可用於測試，但授權版會移除評估浮水印並提供完整功能。 |
| *我可以在 .NET Core 中使用此方法嗎？* | 當然可以——Aspose.Cells 支援 .NET 6/7/8。只要引用 NuGet 套件，程式碼即可保持不變。 |

---

## 生產環境實作技巧

- **Validate JSON** 在將資料傳入 `ApplyJson` 前先驗證 JSON。格式錯誤的資料會拋出 `JsonParseException`。
- **Cache the template** 若在短時間內產生大量報表，請快取範本；重複從磁碟載入會造成不必要的 I/O。
- **Lock the workbook** 在多執行緒的 Web 服務中處理時，請鎖定活頁簿以避免競爭條件。
- **Add error handling** 圍繞 `workbook.Save` 加入錯誤處理，以優雅地處理權限問題或檔案被鎖定的情況。
- **Customize styling** 在範本中自訂樣式（條件格式、公式），讓產生的工作表保留商業邏輯，無需額外程式碼。

---

## 結論

您現在已掌握一套完整、端對端的模式，能透過範本、Smart Markers 與 JSON 資料**建立動態 Excel 表格**。只要**載入 Excel 範本**、插入重複標記，並**從 JSON 填充 Excel**，即可僅用幾行 C# 程式碼**自動化 Excel 報表**的產生。

下一步？試著加入參照動態表格的圖表，或使用 Aspose.Words 將相同的 JSON 匯出為 PDF。您也可以嘗試從資料庫查詢**產生 Excel 報表 JSON**，完成全流程。

## 相關教學

- [使用 Aspose.Cells for .NET 在 Excel 中建立樞紐分析表](/cells/english/net/pivot-tables/create-pivot-table/)
- [使用 Aspose.Cells for .NET 在 Excel 中建立動態折線圖：逐步指南](/cells/english/net/charts-graphs/create-line-charts-excel-aspose-cells-dotnet/)
- [如何使用 Aspose.Cells for .NET 在 Excel 中建立核取方塊 | 資料驗證教學](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}