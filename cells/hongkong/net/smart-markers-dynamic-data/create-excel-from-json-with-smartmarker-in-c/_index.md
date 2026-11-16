---
category: general
date: 2026-11-16
description: 使用 SmartMarker 從 JSON 建立 Excel。了解如何將 JSON 轉換為 Excel、在 Excel 中嵌入 JSON，並在數分鐘內儲存為
  xlsx 工作簿。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json
- convert json to excel
- embed json in excel
- save workbook xlsx
language: zh-hant
lastmod: 2026-11-16
og_description: 快速從 JSON 建立 Excel。本教學示範如何將 JSON 轉換為 Excel、在 Excel 中嵌入 JSON，並使用 Aspose.Cells
  儲存工作簿為 xlsx。
og_image_alt: Screenshot of an Excel worksheet showing JSON data inserted into a single
  cell
og_title: 使用 SmartMarker 從 JSON 建立 Excel – 步驟式 C# 教學
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  headline: Create Excel from JSON with SmartMarker in C#
  type: TechArticle
- description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  name: Create Excel from JSON with SmartMarker in C#
  steps:
  - name: Build and run the console app (`dotnet run`).
    text: Build and run the console app (`dotnet run`).
  - name: Verify the console prints the full path to the generated file.
    text: Verify the console prints the full path to the generated file.
  - name: Open the file in Excel or any spreadsheet viewer.
    text: Open the file in Excel or any spreadsheet viewer.
  - name: Confirm that cell A1 holds the JSON array string exactly as shown above.
    text: Confirm that cell A1 holds the JSON array string exactly as shown above.
  type: HowTo
tags:
- SmartMarker
- Aspose.Cells
- C#
- JSON
title: 使用 C# 的 SmartMarker 從 JSON 建立 Excel
url: /zh-hant/net/smart-markers-dynamic-data/create-excel-from-json-with-smartmarker-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 透過 SmartMarker 從 JSON 建立 Excel

如果您需要在 .NET 專案中 **從 JSON 建立 Excel**，本指南提供完整且可執行的解決方案。使用 Aspose.Cells 的 Smart Marker 處理器，您可以 **將 JSON 轉換為 Excel**、將 JSON 字串直接嵌入儲存格，並 **儲存工作簿為 xlsx**，無需撰寫任何手動解析程式碼。

您將會看到如何註冊 JSON 資料來源、插入會將整個陣列輸出為單一 JSON 字串的 Smart Marker、處理工作表，最後將檔案寫入磁碟。完成本教學後，您即可產生一個 Excel 檔案，於儲存格 A1 中包含原始 JSON 資料，供後續處理或報表使用。

## 前置條件

- .NET 6.0 或更新版本（此程式碼亦相容 .NET Framework 4.7+）
- Aspose.Cells for .NET（NuGet 套件 `Aspose.Cells`）
- 具備 C# 與 JSON 格式的基本知識
- 使用 Visual Studio 或 VS Code 等開發環境

## 步驟 1：設定專案並匯入命名空間

建立一個新的主控台應用程式，並加入 Aspose.Cells 套件：

```bash
dotnet new console -n JsonToExcelDemo
cd JsonToExcelDemo
dotnet add package Aspose.Cells
```

接著在 `Program.cs` 的頂部加入必要的命名空間：

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
```

**為什麼？**  
`Aspose.Cells` 提供工作簿模型，而 `Aspose.Cells.SmartMarkers` 包含 `SmartMarkerProcessor` 類別，用於解析工作表中的 `&=` 標記。

## 步驟 2：定義 JSON 資料來源

將 JSON 字串放入變數中。在此範例中，我們有一個訂單陣列：

```csharp
// Step 2: Define the JSON data source
string json = @"{
    ""Orders"": [
        { ""Id"": 1, ""Amount"": 100 },
        { ""Id"": 2, ""Amount"": 150 }
    ]
}";
```

**為什麼？**  
Smart Marker 可處理任何符合格式的 JSON。將 JSON 以字串形式保存，可直接註冊而無需磁碟上的檔案。

## 步驟 3：使用 SmartMarkerProcessor 註冊 JSON 資料

建立 `SmartMarkerProcessor` 實例，並將 JSON 字串與稍後在工作表中會使用的名稱關聯起來：

```csharp
// Step 3: Register the JSON data with the Smart Marker processor
SmartMarkerProcessor processor = new SmartMarkerProcessor();
processor.RegisterJsonDataSource("OrdersJson", json);
```

**為什麼？**  
`RegisterJsonDataSource` 會解析 JSON，並將其層級結構提供給 Smart Marker 使用。名稱 `"OrdersJson"` 成為標記表達式中的根物件。

## 步驟 4：建立工作簿並插入 Smart Marker

建立新的工作簿，取得第一個工作表，並在儲存格 A1 中寫入 Smart Marker，以輸出整個 `Orders` 陣列為單一 JSON 字串：

```csharp
// Step 4: Create a workbook and get the first worksheet
Worksheet ws = new Workbook().Worksheets[0];

// Insert a Smart Marker that outputs the whole array as a single JSON string
ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");
```

**為什麼？**  
`OrdersJson.Orders.ArrayAsSingle` 表示 Smart Marker 取得 `Orders` 陣列並重新序列化為 JSON，將結果放入目標儲存格。這是 **在 Excel 中嵌入 JSON** 最直接的方式。

## 步驟 5：處理工作表

執行處理器，使其將標記取代為實際的 JSON 字串：

```csharp
// Step 5: Process the worksheet – the marker is replaced with the JSON array string
processor.Process(ws);
```

**為什麼？**  
處理過程會檢查每個儲存格的 `&=` 標記，根據已註冊的資料來源評估，並將計算結果寫回工作表。

## 步驟 6：將工作簿儲存為 .xlsx 檔案

最後，將工作簿寫入磁碟。請將路徑調整為您有寫入權限的資料夾：

```csharp
// Step 6: Save the workbook
string outputPath = Path.Combine(
    Environment.CurrentDirectory,
    "JsonArraySingleCell.xlsx");

ws.Workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

**為什麼？**  
`SaveFormat.Xlsx` 可確保檔案以現代的 Office Open XML 格式儲存，符合 **save workbook xlsx** 的需求。

## 完整原始碼

將所有部件組合起來，以下是完整、可直接執行的程式碼：

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // Step 2: Define the JSON data source
        string json = @"{
            ""Orders"": [
                { ""Id"": 1, ""Amount"": 100 },
                { ""Id"": 2, ""Amount"": 150 }
            ]
        }";

        // Step 3: Register the JSON data with the Smart Marker processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.RegisterJsonDataSource("OrdersJson", json);

        // Step 4: Create a workbook and get the first worksheet
        Worksheet ws = new Workbook().Worksheets[0];

        // Insert a Smart Marker that will output the whole array as a single JSON string
        ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");

        // Step 5: Process the worksheet – the marker is replaced with the JSON array string
        processor.Process(ws);

        // Step 6: Save the workbook
        string outputPath = Path.Combine(
            Environment.CurrentDirectory,
            "JsonArraySingleCell.xlsx");
        ws.Workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### Excel 中的預期輸出

開啟 `JsonArraySingleCell.xlsx`。儲存格 A1 會包含：

```
[{"Id":1,"Amount":100},{"Id":2,"Amount":150}]
```

## 常見變化與邊緣情況

| 情況 | 調整 |
|-----------|------------|
| **Multiple JSON objects** | Register each object with a distinct name (e.g., `processor.RegisterJsonDataSource("CustomerJson", customerJson);`) and reference them with separate markers. |
| **Pretty‑printed JSON in a cell** | Use the `ArrayAsSinglePretty` option: `ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSinglePretty");` |
| **Large JSON payloads** | Consider writing the JSON to a hidden sheet or using `DataTable` conversion for better performance. |
| **Embedding JSON in multiple cells** | Place different markers in other cells, e.g., `&=OrdersJson.Orders[0].Id` to pull individual fields. |

**小技巧：** 處理非常大的 JSON 時，請增加工作簿的記憶體緩衝區 (`WorkbookSettings.MemorySetting`) 以避免 `OutOfMemoryException`。

## 測試解決方案

1. 建置並執行主控台應用程式（`dotnet run`）。  
2. 確認主控台輸出產生檔案的完整路徑。  
3. 在 Excel 或任何試算表檢視器中開啟該檔案。  
4. 確認儲存格 A1 正好包含如上所示的 JSON 陣列字串。

如果儲存格顯示的是標記文字（`&=OrdersJson...`）而非 JSON，請再次確認處理器是在放置標記 **之後** 被呼叫，且 JSON 字串是有效的。

## 結論

現在您已了解如何使用 Aspose.Cells Smart Markers **從 JSON 建立 Excel**、**將 JSON 轉換為 Excel**、將 JSON 資料直接嵌入儲存格，以及使用單行程式碼 **儲存工作簿為 xlsx**。此方法免除手動解析，適用於任何 JSON 結構，並產生符合標準的乾淨 Excel 檔案。

### 後續步驟

- 探索 **Smart Marker 迴圈**（`&=OrdersJson.Orders`），為每筆訂單產生一列，而非單一 JSON 字串。  
- 結合此技巧與 **Excel 公式**，從嵌入的資料計算總計。  
- 研究如何使用 `Workbook.Load` 以及反向的 `SmartMarkerProcessor` **從 Excel 讀回 JSON**。

歡迎嘗試不同的 JSON 結構、多個工作表，或匯出為 CSV、PDF 等其他格式。祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並在此基礎上延伸。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索其他實作方式。

- [使用 Aspose.Cells Smart Marker 從 JSON 建立 Excel](/cells/english/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/)
- [從 JSON 建立 Excel 工作簿 – 完整 Aspose.Cells 指南](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [從 JSON 儲存 Excel 工作簿 – 完整指南](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}