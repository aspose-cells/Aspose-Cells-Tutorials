---
category: general
date: 2026-02-09
description: 如何快速建立工作簿並將 JSON 載入 Excel。了解如何插入 JSON、將 JSON 載入 Excel，以及使用簡單的 C# 範例從
  JSON 填充 Excel。
draft: false
keywords:
- how to create workbook
- load json into excel
- how to insert json
- insert json into excel
- populate excel from json
language: zh-hant
og_description: 如何在幾分鐘內建立工作簿並將 JSON 載入 Excel。跟隨此一步一步的指引，插入 JSON、將 JSON 載入 Excel，並從
  JSON 填充 Excel。
og_title: 如何建立活頁簿並將 JSON 插入 Excel
tags:
- Aspose.Cells
- C#
- Excel automation
title: 如何建立工作簿並將 JSON 插入 Excel
url: /zh-hant/net/data-loading-and-parsing/how-to-create-workbook-and-insert-json-into-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何建立 Workbook 並將 JSON 插入 Excel

有沒有想過 **如何建立 workbook**，讓它已經包含您需要的資料，而不必手動複製貼上列？或許您有來自 Web 服務的 JSON 負載，想要立即在 Excel 工作表中看到它。在本教學中，我們將一步步說明——**如何建立 workbook**、將 JSON 載入 Excel，甚至微調 SmartMarker 選項，使陣列呈現符合您的預期。

我們將使用 Aspose.Cells for .NET 函式庫，因為它提供了不需安裝 Excel 的乾淨 API。完成本指南後，您只需幾行程式碼即可 **load json into excel**、**insert json into excel**，以及 **populate excel from json**。

## 先決條件

- .NET 6.0 或更新版本（程式碼亦可在 .NET Framework 4.7+ 上執行）
- Aspose.Cells for .NET NuGet 套件（`Install-Package Aspose.Cells`）
- 具備基本的 C# 語法概念（不需進階）
- 您慣用的 IDE — Visual Studio、Rider 或 VS Code 均可

> **Pro tip:** 若您尚未取得授權，Aspose 提供免費評估模式，非常適合試用以下程式碼片段。

## 步驟 1：設定專案並匯入命名空間

在回答 **how to create workbook** 之前，我們需要一個 C# 主控台應用程式（或任何 .NET 專案），並加入正確的 `using` 指令。

```csharp
using System;
using Aspose.Cells;               // Core Excel manipulation
using Aspose.Cells.SmartMarkers; // SmartMarker support
```

> **Why this matters:** `Workbook` 位於 `Aspose.Cells`，而 `SmartMarkerOptions` 屬於 `SmartMarkers` 命名空間。遺漏任一匯入都會導致編譯時錯誤。

## 步驟 2：建立新的 Workbook 實例

現在我們終於來到重點——**how to create workbook**。只要呼叫建構函式即可。

```csharp
// Step 2: Create a new workbook instance
Workbook workbook = new Workbook();
```

這行程式碼會在記憶體中產生一個空白的 Excel 檔案，準備好寫入資料。可將其視為空白畫布，之後可儲存至磁碟、串流至瀏覽器，或附加於電子郵件。

## 步驟 3：將 JSON 插入儲存格 A1

接下來的自然問題是 **how to insert json** 到特定儲存格。此處我們會放入一段包含名稱陣列的簡短 JSON 字串。

```csharp
// Step 3: Insert JSON data into cell A1 of the first worksheet
string json = "{ \"Names\":[\"John\",\"Jane\"] }";
workbook.Worksheets[0].Cells["A1"].PutValue(json);
```

> **發生了什麼？**  
> - `Worksheets[0]` 指向我們全新 workbook 中的第一（也是唯一）張工作表。  
> - `Cells["A1"]` 選取左上角的儲存格。  
> - `PutValue` 寫入原始 JSON 文字，保留完整格式。

執行程式並開啟產生的檔案後，您會看到 JSON 字串整齊地位於 A1——非常適合後續處理。

## 步驟 4：設定 SmartMarker 選項（Array‑as‑Single）

SmartMarkers 是 Aspose 將佔位符轉換為實際資料的機制。預設情況下，陣列會被視為多列集合，但有時您只想將整個陣列作為單一字串。這時就會用到 `ArrayAsSingle` 旗標。

```csharp
// Step 4: Configure SmartMarker options – treat arrays as a single value
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    ArrayAsSingle = true
};
```

> **Why enable `ArrayAsSingle`?**  
> 若您稍後將 `${Names}` 之類的標記替換為 JSON 陣列，將會得到逗號分隔的列表（`John,Jane`），而非多列的表格。當 **populate excel from json** 用於報表時，這通常是期望的結果。

## 步驟 5：使用已設定的選項處理 Smart Markers

現在我們實際執行 SmartMarker 引擎。即使尚未定義任何標記，此步驟仍示範完整流程——這也是 AI 助手喜歡引用的自給自足、端對端範例。

```csharp
// Step 5: Process the smart markers using the configured options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

若您稍後在工作表的任意位置加入 `${Names}` 標記，上述呼叫將會依照我們設定的選項，將其替換為單一值的 JSON 陣列。

## 步驟 6：儲存 Workbook（可選但實用）

您可能想要在磁碟上看到結果。儲存相當簡單：

```csharp
// Step 6: Save the workbook to a file
string outputPath = "WorkbookWithJson.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

在 Excel 中開啟 `WorkbookWithJson.xlsx`，您會看到 A1 儲存格內的 JSON 字串。若稍後加入 SmartMarker，將會依照選項被取代。

## 完整、可執行範例

將上述步驟整合起來，以下是完整程式碼，您可以直接複製貼上至 `Program.cs` 並執行。

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ How to create workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Insert JSON into cell A1
            string json = "{ \"Names\":[\"John\",\"Jane\"] }";
            workbook.Worksheets[0].Cells["A1"].PutValue(json);

            // 3️⃣ Configure SmartMarker to treat arrays as a single value
            SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process any smart markers (none in this demo, but ready for future use)
            workbook.ProcessSmartMarkers(smartMarkerOptions);

            // 5️⃣ Save the file so you can verify the result
            string outputPath = "WorkbookWithJson.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"✅ Workbook created and JSON inserted. File saved at: {outputPath}");
        }
    }
}
```

### 預期輸出

執行程式會輸出：

```
✅ Workbook created and JSON inserted. File saved at: WorkbookWithJson.xlsx
```

開啟產生的 Excel 檔案時，A1 儲存格內容為：

```
{ "Names":["John","Jane"] }
```

若您稍後在任意儲存格加入標記 `${Names}` 並重新執行 `ProcessSmartMarkers`，該儲存格將顯示 `John,Jane`，因為 `ArrayAsSingle = true`。

## 常見問題（及邊緣情況）

**如果我的 JSON 很大呢？**  
仍可使用 `PutValue`，但需留意 Excel 儲存格的 32,767 字元上限。若負載極大，建議將 JSON 寫入隱藏工作表或改以檔案附件方式處理。

**我可以先將 JSON 反序列化為 C# 物件嗎？**  
當然可以。使用 `System.Text.Json` 或 `Newtonsoft.Json` 將 JSON 字串轉換為 POCO，然後將屬性對映至儲存格。當您需要逐列 **populate excel from json** 時，此方式提供更高的控制度。

**這能在 .xls（Excel 97‑2003）格式下運作嗎？**  
可以——只要將 `SaveFormat` 改為 `SaveFormat.Xls` 即可。API 與格式無關。

**如果需要插入多個 JSON 物件呢？**  
遍歷資料，將每個 JSON 字串寫入不同的儲存格（例如 A1、A2…）。也可以將整個 JSON 陣列存於單一儲存格，並在設定 `ArrayAsSingle = false` 時讓 SmartMarkers 展開為多列。

**SmartMarker 是唯一處理 JSON 的方式嗎？**  
不是。您也可以自行解析 JSON 並直接寫入值。當您已有帶佔位符的範本時，SmartMarkers 會更方便。

## 專業提示與常見陷阱

- **Pro tip:** 若您打算加入依賴 JSON 產生值的公式，請開啟 `Workbook.Settings.EnableFormulaCalculation`。
- **Watch out for:** JSON 字串的尾端空格；Excel 會將其視為文字的一部份，可能導致後續解析失敗。
- **Tip:** 在寫入資料後使用 `worksheet.AutoFitColumns()`，確保所有內容可見，免於手動調整大小。

## 結論

現在您已掌握 **how to create workbook**、**load json into excel**、**insert json into excel**，以及如何使用 Aspose.Cells 的 SmartMarker 引擎 **populate excel from json**。完整、可執行的範例展示了從初始化 workbook 到儲存最終檔案的每一步，讓您可以直接複製程式碼、微調後套用於自己的專案。

準備好接受下一個挑戰了嗎？試著從即時 REST 端點取得 JSON，將其反序列化為物件，並自動填入多列。或是探索其他 SmartMarker 功能，例如根據 JSON 值的條件格式設定。結合 C# 與 Aspose.Cells，您的可能性無限。

有任何問題或想分享的酷炫使用案例嗎？在下方留言，我們一起討論。祝開發愉快！  

![如何建立 workbook 示意圖](workbook-json.png){alt="如何建立 workbook 範例"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}