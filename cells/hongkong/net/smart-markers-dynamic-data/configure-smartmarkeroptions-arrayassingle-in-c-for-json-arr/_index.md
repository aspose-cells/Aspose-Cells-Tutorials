---
category: general
date: 2026-09-21
description: 在 C# 中設定 SmartMarkerOptions 的 ArrayAsSingle，以將 JSON 陣列匯出為 Excel 活頁簿中的單一儲存格值。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- configure smartmarkeroptions arrayassingle
- Aspose.Cells smart markers
- export JSON array
- C# DataTable
- Workbook ProcessSmartMarkers
language: zh-hant
lastmod: 2026-09-21
og_description: 在 C# 中設定 SmartMarkerOptions 的 ArrayAsSingle，以將 JSON 陣列匯出為單一儲存格值。了解完整的逐步解決方案。
og_image_alt: Screenshot of an Excel sheet showing a JSON array stored in a single
  cell after using SmartMarkerOptions
og_title: 在 C# 中設定 SmartMarkerOptions ArrayAsSingle – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Configure SmartMarkerOptions ArrayAsSingle in C# to export JSON arrays
    as a single cell value in an Excel workbook.
  headline: Configure SmartMarkerOptions ArrayAsSingle in C# for JSON arrays
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: 在 C# 中設定 SmartMarkerOptions 的 ArrayAsSingle 以用於 JSON 陣列
url: /zh-hant/net/smart-markers-dynamic-data/configure-smartmarkeroptions-arrayassingle-in-c-for-json-arr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中設定 SmartMarkerOptions ArrayAsSingle 以處理 JSON 陣列

如果您在使用 Aspose.Cells 產生 Excel 檔案時需要 **設定 SmartMarkerOptions ArrayAsSingle**，本指南將一步步示範如何操作。您將看到如何將 JSON 陣列完整保留在單一儲存格中，而不是將其元素分散到多列。

在試算表中處理 JSON 資料時，常常需要在「展平」與「緊湊」兩種呈現方式之間做選擇。在許多報表情境（例如儲存標籤列表或一組識別碼）中，您希望整個 JSON 字串保持在單一儲存格內。`SmartMarkerOptions` 的 **ArrayAsSingle** 旗標正是為此而設。

在本教學中，您將會：

* 建立一個在欄位中保存 JSON 陣列的 `DataTable`。
* 在 Excel 工作表中放置 Smart Markers。
* **設定 SmartMarkerOptions ArrayAsSingle**，使 JSON 陣列被視為單一儲存格值。
* 處理標記並儲存活頁簿。
* 驗證輸出結果。

> **先備條件** – 您需要 Aspose.Cells for .NET 套件（v23.12 或更新版本）以及 .NET 開發環境（建議使用 Visual Studio 2022）。假設您已具備 C# 與 DataTable 的基本知識。

---

## 步驟 1：以 JSON 陣列準備資料來源

首先，建立一個模擬從服務或資料庫取得資料的 `DataTable`。**Names** 欄位包含一個 JSON 編碼的字串，代表名稱陣列。

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable dataTable = new DataTable();
dataTable.Columns.Add("Id", typeof(int));
dataTable.Columns.Add("Names", typeof(string));

// Store the JSON array as a plain string
dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");
```

*為什麼要這樣做？*  
Smart Markers 直接從 .NET 物件讀取資料。將 JSON 陣列放在字串欄位中，可保留完整的 JSON 語法，之後寫入儲存格時不會被改變。

---

## 步驟 2：在新活頁簿中插入 Smart Markers

建立一個全新的活頁簿，選取第一個工作表，並寫入參照整個資料表與特定 **Names** 欄位的 Smart Markers。

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Smart marker for the entire table (optional, shown for completeness)
worksheet.Cells["A1"].PutValue("&=dataTable");

// Smart marker that targets only the Names column
worksheet.Cells["A2"].PutValue("&=dataTable.Names");
```

標記 `&=dataTable.Names` 告訴 Aspose.Cells 用 `dataTable` 中 **Names** 欄位的值取代該儲存格。因為只有一列，標記只會被處理一次。

---

## 步驟 3：**設定 SmartMarkerOptions ArrayAsSingle**

預設情況下，Aspose.Cells 會將類似陣列的字串展開為多列。將 `ArrayAsSingle` 設為 `true` 可覆寫此行為，強制整個 JSON 字串保留在單一儲存格。

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Export the JSON array as a single cell value
    ArrayAsSingle = true
};
```

*為什麼要啟用 `ArrayAsSingle`？*  
當 `ArrayAsSingle` 為 `false` 時，引擎會將 `["Alice","Bob"]` 解析為兩個獨立值，寫入相鄰的列。設為 `true` 後，字串會被視為原子值，這對於在 Excel 中保留 JSON 格式至關重要。

---

## 步驟 4：使用已設定的選項處理 Smart Markers

現在執行 Smart Marker 引擎，傳入剛剛設定好的選項物件。

```csharp
// Process smart markers using the custom options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

處理過程中，Aspose.Cells 會讀取 `dataTable`、套用標記，並遵守 `ArrayAsSingle` 旗標，讓 JSON 陣列保持原樣。

---

## 步驟 5：儲存活頁簿並驗證結果

最後，將活頁簿寫入磁碟。使用 Excel 或任何試算表檢視器開啟產生的檔案，確認儲存格 **A2** 含有完整的 JSON 字串。

```csharp
// Save the resulting workbook
string outputPath = @"C:\Temp\SmartMarkerJson.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### 預期輸出

| A   |
|-----|
| **["Alice","Bob"]** |

儲存格 **A2** 以單一文字值顯示 JSON 陣列，與 `DataTable` 中的內容完全相同，未產生額外列。

---

## 常見變化與邊緣案例處理

| 情境 | 應對方式 |
|-----------|--------------|
| **多列 JSON 陣列** | 同樣的 `ArrayAsSingle` 設定即可；每列的 JSON 陣列會保留在各自的儲存格中。 |
| **不同的 JSON 結構（物件、巢狀陣列）** | 只要 JSON 以字串形式存在，`ArrayAsSingle` 皆會保持完整。對於複雜物件，可能需要對引號進行跳脫。 |
| **使用其他資料來源（例如 List\<T\>）** | 將 `DataTable` 換成任意可列舉的集合；標記語法 (`&=myList.Property`) 保持不變。 |
| **匯出為 CSV 而非 XLSX** | `ArrayAsSingle` 仍然有效，但需注意 CSV 不會保留儲存格格式；建議將 JSON 包在引號內。 |

**小技巧：** 請務必在呼叫 `ProcessSmartMarkers` 之前設定 `ArrayAsSingle`。在處理之後再變更旗標不會影響已產生的儲存格。

---

## 完整可執行範例

以下程式碼可直接貼到 Console 應用程式中執行。內含所有 `using` 指示與說明註解。

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the data source with a JSON array
            DataTable dataTable = new DataTable();
            dataTable.Columns.Add("Id", typeof(int));
            dataTable.Columns.Add("Names", typeof(string));
            dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");

            // 2️⃣ Build a workbook and place smart markers
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Cells["A1"].PutValue("&=dataTable");          // whole table (optional)
            worksheet.Cells["A2"].PutValue("&=dataTable.Names");   // Names column

            // 3️⃣ Configure SmartMarkerOptions to treat arrays as single values
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process the markers with the custom options
            workbook.ProcessSmartMarkers(options);

            // 5️⃣ Save the file
            string path = @"C:\Temp\SmartMarkerJson.xlsx";
            workbook.Save(path);
            Console.WriteLine($"Workbook saved to {path}");
        }
    }
}
```

執行程式後，開啟 `SmartMarkerJson.xlsx`，即可在儲存格 **A2** 中看到保留的 JSON 陣列。

---

## 結論

現在您已掌握如何在 C# 中 **設定 SmartMarkerOptions ArrayAsSingle**，以在使用 Aspose.Cells 智慧標記時將 JSON 陣列保留為單一儲存格值。從準備 `DataTable`、插入標記、設定 `ArrayAsSingle`、處理到儲存的步驟，構成一套可重複使用的模式，適用於任何需要在 Excel 中緊湊呈現 JSON 的情境。

接下來，您可以探索：

* **Aspose.Cells 智慧標記** 的集合迴圈用法。
* 透過自訂儲存格格式匯出 **巢狀 JSON 物件**。
* 結合 **條件格式** 與智慧標記，打造更豐富的報表。

歡迎嘗試不同資料結構，並分享您的發現。祝開發順利！

## 接下來該學什麼？

以下教學與本指南緊密相關，能進一步深化您對相關技術的掌握。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您在專案中靈活運用更多 API 功能與替代實作方式。

- [Create Excel Workbook from JSON – Complete Aspose.Cells Guide](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Create Configure Excel Workbook Aspose Cells Net](/cells/hindi/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Create Configure Excel Workbook Aspose Cells Net](/cells/german/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}