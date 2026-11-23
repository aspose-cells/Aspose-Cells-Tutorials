---
category: general
date: 2026-11-22
description: 學習如何在 C# 中使用 Aspose.Cells Smart Marker 從 JSON 資料建立 Excel。一步一步的指南涵蓋範本設計、JSON
  處理及檔案匯出。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json data
- Aspose.Cells
- Smart Marker
- C# Excel generation
- JSON to Excel
- Excel template
language: zh-hant
lastmod: 2026-11-22
og_description: 使用 Aspose.Cells Smart Marker 從 JSON 資料建立 Excel。跟隨本簡明教學，從 JSON 陣列生成完整格式化的工作簿。
og_image_alt: Screenshot showing Excel workbook created from JSON data using Aspose.Cells
og_title: 在 C# 中從 JSON 資料建立 Excel – 完整 Aspose.Cells 教學
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn to create Excel from JSON data in C# using Aspose.Cells Smart
    Marker. Step‑by‑step guide covers template design, JSON handling, and file export.
  headline: How to create Excel from JSON data with Aspose.Cells and Smart Marker
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: 如何使用 Aspose.Cells 與 Smart Marker 從 JSON 資料建立 Excel
url: /zh-hant/net/smart-markers-dynamic-data/how-to-create-excel-from-json-data-with-aspose-cells-and-sma/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.Cells 與 Smart Marker 從 JSON 資料建立 Excel

如果您需要在 .NET 應用程式中 **從 JSON 資料建立 Excel**，本教學將向您展示一個完整、可投入生產的解決方案。您將會看到如何將 JSON 陣列嵌入單一儲存格、使用 **Aspose.Cells** 的 **Smart Marker** 功能，並在不需要手動逐格編寫程式碼的情況下產生最終活頁簿。

此方法適用於任何 JSON 資料——無論是匯出 API 結果、序列化物件，或是建立報表。完成本指南後，您將擁有一個可直接執行的 C# 專案，能讀取 JSON 字串、套用至 **Excel 範本**，並將結果儲存為新檔案。

## 前置條件

- .NET 6.0 或更新版本（程式碼亦相容 .NET Framework 4.6+）
- Visual Studio 2022（或任何支援 C# 的 IDE）
- **Aspose.Cells for .NET** NuGet 套件（版本 23.10 或更新）
- 包含 Smart Marker 標記 `<%=Fruits:ArrayAsSingle%>` 的簡易 Excel 範本檔案，放置於目標儲存格

> **專業提示：** 請將範本放在應用程式執行時可存取的資料夾中（例如 `Resources` 或可設定的路徑）。

## 步驟 1：準備 JSON 資料

首先，定義您想插入工作表的 JSON 陣列。本範例使用水果名稱清單。

```csharp
// Step 1 – JSON array that will be placed in a single cell
string fruitsJson = "[\"Apple\",\"Banana\",\"Cherry\"]";
```

JSON 字串可以動態產生（例如 `JsonSerializer.Serialize(myList)`）或從外部來源（如 REST API）讀取。關鍵在於字串必須是有效的 JSON 陣列，因為 **Smart Marker** 在使用 `ArrayAsSingle` 選項時需要 JSON 表示形式。

## 步驟 2：建立 Smart Marker 資料來源

Aspose.Cells 的 Smart Marker 引擎可與任何 .NET 物件配合使用。我們建立一個匿名物件，將 JSON 字串放在名為 `Fruits` 的屬性下。屬性名稱必須與範本中使用的標記名稱相符。

```csharp
// Step 2 – Anonymous object serving as the Smart Marker data source
var dataSource = new
{
    Fruits = fruitsJson   // Property name "Fruits" matches the marker <%=Fruits...%>
};
```

> **為何使用匿名物件？** 它讓您在不定義專屬類別的情況下傳遞輕量級資料容器，從而加快原型開發。對於較大的專案，您可以改用強型別 DTO。

## 步驟 3：設計含 Smart Marker 佔位符的 Excel 範本

建立一個 Excel 檔案（`SmartMarkerTemplate.xlsx`），其中包含 JSON 將顯示的佔位符。將以下標記放入目標儲存格（例如 **A1**）：

```
<%=Fruits:ArrayAsSingle%>
```

- `Fruits` – 與資料來源的屬性名稱相符。
- `ArrayAsSingle` – 告訴 Smart Marker 將整個 JSON 陣列寫入為單一字串，保留方括號與引號。

![Excel template with Smart Marker placeholder](excel-template.png){alt="包含 <%=Fruits:ArrayAsSingle%> 以從 JSON 資料建立 Excel 的 Excel 範本"}

## 步驟 4：載入活頁簿並初始化 Smart Marker 處理器

現在將範本檔案載入 `Aspose.Cells.Workbook` 實例，並建立一個負責取代的 `SmartMarkerProcessor`。

```csharp
// Step 4 – Load the template workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/SmartMarkerTemplate.xlsx");

// Initialise the Smart Marker processor with the loaded workbook
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor(workbook);
```

一次載入活頁簿並重複使用相同的 `SmartMarkerProcessor` 實例，比為每個儲存格建立新處理器更有效率。

## 步驟 5：套用資料來源以取代標記

`ApplyTemplate` 方法會掃描活頁簿中的所有標記，並以提供的物件值取代它們。

```csharp
// Step 5 – Replace the Smart Marker with the JSON content
smartMarkerProcessor.ApplyTemplate(dataSource);
```

因為我們使用了 `ArrayAsSingle`，儲存格現在包含原始的 JSON 字串：

```
["Apple","Banana","Cherry"]
```

如果您需要其他格式（例如以逗號分隔的清單），可以改用 `ArrayAsCommaSeparated` 取代 `ArrayAsSingle`。

## 步驟 6：儲存處理後的活頁簿

最後，將修改後的活頁簿寫入新檔案。您可以選擇任何支援的格式（`.xlsx`、`.xls`、`.csv` 等）。

```csharp
// Step 6 – Save the workbook with the JSON inserted
workbook.Save("YOUR_DIRECTORY/JsonExported.xlsx");
```

產生的 `JsonExported.xlsx` 檔案可在 Excel、Google Sheets 或任何相容檢視器中開啟，且會如同插入時一樣顯示 JSON 陣列。

## 完整可執行範例

將所有部件組合在一起，即可得到一個自包含的主控台程式：

```csharp
using Aspose.Cells;

class SmartMarkerJsonDemo
{
    static void Main()
    {
        // 1️⃣ Define the JSON array
        string fruitsJson = "[\"Apple\",\"Banana\",\"Cherry\"]";

        // 2️⃣ Create the data source object
        var dataSource = new
        {
            Fruits = fruitsJson
        };

        // 3️⃣ Load the Excel template that contains <%=Fruits:ArrayAsSingle%>
        Workbook workbook = new Workbook("YOUR_DIRECTORY/SmartMarkerTemplate.xlsx");

        // 4️⃣ Initialise the Smart Marker processor
        SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor(workbook);

        // 5️⃣ Apply the data source – the marker is replaced with the JSON string
        smartMarkerProcessor.ApplyTemplate(dataSource);

        // 6️⃣ Save the result
        workbook.Save("YOUR_DIRECTORY/JsonExported.xlsx");
    }
}
```

### 預期輸出

| A                                   |
|-------------------------------------|
| `["Apple","Banana","Cherry"]`       |

JSON 會以字串形式精確顯示於 `JsonExported.xlsx` 的 **A1** 儲存格中。

## 處理常見變化與邊緣情況

| 情況                                 | 建議調整 |
|--------------------------------------|----------|
| **大型 JSON 物件**（巢狀字典） | 使用 `ArrayAsJson` 嵌入整個物件層級，或將 JSON 對映至強型別模型，並使用巢狀標記（`<%=Parent.Child%>`）。 |
| **多個 JSON 陣列** 位於不同儲存格 | 在匿名物件中加入額外屬性（例如 `Vegetables = vegJson`），並使用相對應的標記（`<%=Vegetables:ArrayAsSingle%>`）。 |
| **需要將陣列拆分為多列** | 將 `ArrayAsSingle` 改為 `Array` —— Smart Marker 會為每個元素建立新列。 |
| **範本作為嵌入式資源儲存** | 從串流載入活頁簿：`Assembly.GetExecutingAssembly().GetManifestResourceStream("Namespace.Template.xlsx")`。 |
| **在 ASP.NET Core 中執行** | 使用 `IWebHostEnvironment.ContentRootPath` 來組合範本與輸出檔案的完整路徑。 |

## 效能考量

- **重複使用 `Workbook` 物件** 於批次處理大量記錄時；每個活頁簿僅建立一次處理器。
- **停用計算**（`workbook.CalculateFormula = false`），若範本包含大量公式且在 JSON 插入步驟中不需要計算時。
- **串流儲存**（`workbook.Save(stream, SaveFormat.Xlsx)`）可減少將檔案直接回傳給客戶端時的 I/O 開銷。

## 結論

您現在已了解如何在 C# 中使用 **Aspose.Cells** 及 **Smart Marker** 功能 **從 JSON 資料建立 Excel**。本教學涵蓋了 JSON 準備、資料來源建立、範本設計、標記處理與檔案儲存——全部於一個可執行的程式中完成。

您可以：

- 為範本加入額外的 **Smart Marker** 標記，以產生更豐富的報表。
- 改用 `Array` 或 `ArrayAsJson` 以將 JSON 輸出為多列或巢狀結構。
- 若需要免費替代方案，可將此技巧與 **C# Excel 產生** 函式庫（如 EPPlus 或 ClosedXML）結合使用。

祝開發順利，盡情將 JSON 轉換為精美的 Excel 活頁簿吧！

## 接下來該學什麼？

以下教學涵蓋與本指南技術緊密相關的主題。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通其他 API 功能，並在專案中探索替代實作方式。

- [使用 Aspose.Cells Java 匯入 JSON 資料至 Excel：完整指南](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Aspose Cells GridJs 教學 – 使用延遲載入將 Excel 資料匯出為 JSON](/cells/english/python/import-and-export/aspose-cells-gridjs-tutorial-export-excel-data-to-json-with/)
- [使用 Aspose.Cells 的 Smart Marker 從 JSON 建立 Excel](/cells/spanish/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}