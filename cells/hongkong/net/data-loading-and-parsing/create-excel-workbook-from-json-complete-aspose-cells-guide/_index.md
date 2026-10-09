---
category: general
date: 2026-02-14
description: 使用 Aspose.Cells 建立 Excel 活頁簿，並學習如何處理 JSON、將 JSON 轉換為 Excel，以及在幾個簡單步驟中將
  JSON 載入 Excel。
draft: false
keywords:
- create excel workbook
- how to process json
- convert json to excel
- load json into excel
- aspose cells json
language: zh-hant
og_description: 使用 Aspose.Cells 建立 Excel 活頁簿，學習如何處理 JSON，將 JSON 轉換為 Excel，並快速且可靠地將
  JSON 載入 Excel。
og_title: 從 JSON 建立 Excel 工作簿 – 步驟教學 Aspose.Cells
tags:
- Aspose.Cells
- C#
- JSON
- Excel automation
title: 從 JSON 建立 Excel 活頁簿 – 完整 Aspose.Cells 指南
url: /zh-hant/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 JSON 建立 Excel 活頁簿 – 完整 Aspose.Cells 指南

是否曾需要從一段 JSON **建立 Excel 活頁簿**，卻不知從何下手？你並不孤單。許多開發者在手握 JSON 資料時，想要一個整齊的試算表來進行報告或資料交換，卻常卡在這裡。  

好消息是？使用 **Aspose.Cells**，只需幾行程式碼就能將 JSON 轉換為功能完整的 Excel 檔案。在本教學中，我們將逐步說明 **如何處理 JSON**、**將 JSON 轉換為 Excel**，以及使用強大的 `SmartMarkerProcessor` **將 JSON 載入 Excel**。完成後，你將擁有可直接儲存的活頁簿，並清楚了解可調整的選項。

## 你將學會

- 如何為 JSON 處理設定 Aspose.Cells 專案。  
- 建立 Excel 活頁簿 所需的完整程式碼，從 JSON 陣列轉換。  
- `ArrayAsSingle` 選項的重要性以及何時需要變更。  
- 處理較大 JSON 結構、錯誤處理與檔案儲存的技巧。  

> **先決條件：** .NET 6+（或 .NET Framework 4.6+）、Aspose.Cells for .NET NuGet 套件，以及基本的 C# 知識。無需其他函式庫。

---

## 步驟 1：安裝 Aspose.Cells 並加入必要的命名空間

在執行任何程式碼之前，需要在專案中參考 Aspose.Cells 程式庫。

```bash
dotnet add package Aspose.Cells
```

```csharp
using Aspose.Cells;   // Core namespace for workbook manipulation
```

> **小技巧：** 若使用 Visual Studio，NuGet 套件管理員 UI 也能完成相同操作——只要搜尋 *Aspose.Cells* 並點擊安裝即可。

---

## 步驟 2：準備要轉換的 JSON 資料

`SmartMarkerProcessor` 可處理任何 JSON 字串，但必須決定程式庫如何解讀陣列。在此範例中，我們將簡單的數值陣列視為 **單一記錄**，這在只需要平面值清單時相當方便。

```csharp
// Step 2: Define the JSON payload – an array of three numbers
string jsonData = "[1,2,3]";   // You could also load this from a file or API response
```

> **為何重要：** 預設情況下，Aspose.Cells 會將每個陣列元素視為獨立記錄。將 `ArrayAsSingle = true` 設為 true 會將整個陣列合併為單一記錄，符合許多報告情境。

---

## 步驟 3：建立新的 Workbook 實例

現在我們實際在記憶體中 **建立 Excel 活頁簿**。尚未寫入任何檔案，我們僅在準備容器。

```csharp
// Step 3: Initialise a fresh workbook – starts with a single empty worksheet
Workbook workbook = new Workbook();
```

此時 `workbook.Worksheets[0]` 為一張名為 *Sheet1* 的空白工作表。若需要，可稍後重新命名。

---

## 步驟 4：設定 SmartMarker 選項以處理 JSON

`SmartMarkerOptions` 類別讓你細緻控制 JSON 的解讀方式。我們情境中關鍵的旗標是 `ArrayAsSingle`。

```csharp
// Step 4: Set SmartMarker options – treat the JSON array as a single record
SmartMarkerOptions options = new SmartMarkerOptions
{
    ArrayAsSingle = true   // Important when your JSON is a simple list
};
```

> **何時更改：** 若你的 JSON 代表多列集合（例如物件陣列），請將 `ArrayAsSingle` 保持為 `false`。每個物件將自動成為新的一列。

---

## 步驟 5：在工作表上執行 Smart Marker 處理

當活頁簿與選項準備好後，我們將 JSON 傳入處理器。處理器會掃描工作表中的 smart marker（佔位符），並以 JSON 資料取代。由於我們未設定明確的標記，處理器會直接產生預設版面配置。

```csharp
// Step 5: Execute Smart Marker processing on the first worksheet
workbook.Worksheets[0].SmartMarkerProcessor.StartSmartMarkerProcessing(jsonData, options);
```

若想控制資料起始的確切儲存格，可在執行處理器前於儲存格 **A1** 加入標記如 `"${Array}"`。本教學採用預設行為，將陣列值寫入從 **A1** 開始的連續儲存格。

---

## 步驟 6：將活頁簿儲存至磁碟（或串流）

最後一步是將活頁簿持久化。你可以儲存至檔案、記憶體串流，甚至直接從 Web API 回傳。

```csharp
// Step 6: Save the workbook as an .xlsx file
string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonToExcel.xlsx");
workbook.Save(outputPath, SaveFormat.Xlsx);

Console.WriteLine($"Workbook saved to {outputPath}");
```

執行完整程式後，會產生一個 Excel 檔案，數字 **1**、**2**、**3** 分別放置於儲存格 **A1**、**A2**、**A3**。

---

## 完整範例程式

以下為完整、可直接執行的主控台應用程式，將所有步驟串接起來。將其複製貼上至新的 C# 主控台專案，然後按 **F5**。

```csharp
// ---------------------------------------------------------------
// Complete example: Create Excel workbook from JSON using Aspose.Cells
// ---------------------------------------------------------------
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Prepare JSON data
        string jsonData = "[1,2,3]";

        // 2️⃣ Create a new workbook (empty Excel file)
        Workbook workbook = new Workbook();

        // 3️⃣ Configure SmartMarker options – treat the array as a single record
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            ArrayAsSingle = true
        };

        // 4️⃣ Process the JSON on the first worksheet
        workbook.Worksheets[0].SmartMarkerProcessor.StartSmartMarkerProcessing(jsonData, options);

        // 5️⃣ Optionally, add a header for clarity
        workbook.Worksheets[0].Cells["A1"].PutValue("Numbers");
        // Shift data down one row so the header stays on top
        workbook.Worksheets[0].Cells.InsertRows(1, 1);

        // 6️⃣ Save the workbook
        string outputPath = Path.Combine(Environment.CurrentDirectory, "JsonToExcel.xlsx");
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"✅ Excel workbook created at: {outputPath}");
    }
}
```

**Excel 中的預期輸出**

| 數字 |
|------|
| 1 |
| 2 |
| 3 |

標題列（「Numbers」）是可選的，但示範了如何將手動儲存格編輯與 smart‑marker 處理結合。

---

## 常見問題與特殊情況

### 如果我的 JSON 是物件而非陣列該怎麼辦？

```json
{
  "Name": "Alice",
  "Age": 30,
  "Country": "USA"
}
```

仍然可以使用 `SmartMarkerProcessor`。在工作表中放置 `${Name}`、`${Age}`、`${Country}` 等標記，然後呼叫 `StartSmartMarkerProcessing`。處理器會以相對應的值取代每個標記。

### 如何處理大型 JSON 檔案（數 MB）？

- **串流 JSON**：不要一次載入整個字串，而是使用 `StreamReader` 讀取檔案，並將文字傳給 `StartSmartMarkerProcessing`。  
- **提升記憶體上限**：若遇到 `OutOfMemoryException`，可設定 `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference;`。  
- **分塊處理**：將 JSON 分割為較小的陣列，並在新工作表上逐塊處理。

### 能否匯出為 CSV 而非 XLSX？

當然可以。處理完成後，只需呼叫：

```csharp
workbook.Save("output.csv", SaveFormat.Csv);
```

資料版面保持不變，僅檔案格式改為 CSV。

### 若在載入 JSON 後需要格式化儲存格（字型、顏色）該怎麼辦？

可以在 smart‑marker 步驟之後套用格式：

```csharp
Style style = workbook.CreateStyle();
style.Font.IsBold = true;
workbook.Worksheets[0].Cells["A1"].SetStyle(style);
```

因為處理器先執行，之後套用的格式不會被覆寫。

---

## 小技巧與最佳實踐

- **始終明確設定 `ArrayAsSingle`**——遺忘此旗標是導致意外列重複的常見原因。  
- **在處理前驗證 JSON**——格式錯誤的字串會拋出 `JsonParseException`。將呼叫包在 `try/catch` 中以優雅處理錯誤。  
- **使用具名 smart marker**（`${Orders}`）提升可讀性，特別是處理巢狀 JSON 物件時。  
- **若從 Web API 回傳，請將活頁簿保留在記憶體中**；傳送 `MemoryStream` 可避免不必要的磁碟 I/O。  
- **版本相容性**：上述程式碼適用於 Aspose.Cells 23.12 及以上版本。若使用較舊版本，請檢查發行說明。

---

## 結論

我們剛剛示範了如何使用 Aspose.Cells **從 JSON 建立 Excel 活頁簿**，涵蓋從安裝程式庫到儲存最終檔案的全部步驟。掌握 `SmartMarkerProcessor` 及其選項後，你即可 **將 JSON 載入 Excel**、**將 JSON 轉換為 Excel**，甚至為複雜的報告情境自訂輸出。

準備好進一步了嗎？試著輸入巢狀的 JSON 物件陣列、加入條件格式，或將結果匯出為 PDF——全部皆可使用相同的 Aspose.Cells API。你的資料到 Excel 的管線現在只需幾行程式碼即可完成。

如果有任何問題或遇到困難，歡迎在下方留言。祝開發愉快，盡情將 JSON 轉換成美觀的試算表吧！

![使用 JSON 資料建立 Excel 活頁簿](/images/create-excel-workbook-json.png "示意圖：JSON 陣列轉換為 Excel 工作表")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}