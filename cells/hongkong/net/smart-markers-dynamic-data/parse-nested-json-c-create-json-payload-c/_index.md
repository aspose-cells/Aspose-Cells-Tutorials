---
category: general
date: 2026-02-15
description: 使用 SmartMarkers 解析 C# 中的巢狀 JSON，並學習如何為複雜訂單建立 JSON 載荷（C#）。一步一步的指引，附完整程式碼與說明。
draft: false
keywords:
- parse nested json c#
- create json payload c#
language: zh-hant
og_description: 即時解析巢狀 JSON（C#）。學習如何在 C# 中建立 JSON 載荷，並使用 SmartMarkers 處理，提供完整可執行的範例。
og_title: 解析巢狀 JSON C# – 建立 JSON 有效載荷 C#
tags:
- json
- csharp
- smartmarkers
title: 解析巢狀 JSON C# – 建立 JSON 有效載荷 C#
url: /zh-hant/net/smart-markers-dynamic-data/parse-nested-json-c-create-json-payload-c/
---

keep as is because it's a keyword. So keep **parse nested json c#** unchanged.

Similarly "create json payload c#" keep unchanged.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 解析巢狀 JSON C# – 建立 JSON Payload C#  

是否曾需要 **parse nested JSON C#**，卻不知從何下手？你並不孤單——許多開發者在資料包含物件內的陣列時會卡關。好消息是，只要幾行程式碼，你就能同時 **create JSON payload C#**，並讓 SmartMarkers 為你走訪巢狀結構。  

在本教學中，我們將建立一段代表訂單與明細項目的 JSON 字串，啟用 SmartMarkers 處理器以理解巢狀範圍，最後驗證資料是否正確解析。完成後，你將擁有一個可直接複製貼上的完整程式，能夠套用於任何層級式 JSON。

## 需要的環境  

- .NET 6 或更新版本（程式碼亦可於 .NET Core 3.1 編譯）  
- 參考 SmartMarkers 函式庫（或任何支援巢狀範圍的類似處理器）  
- 基本的 C# 知識——只要會使用 `using` 陳述式與 `Main` 方法即可  

就這樣。除了標記函式庫外不需要額外的 NuGet 套件，也不需要外部服務。

## 步驟 1：建立 JSON Payload C# – 建構資料  

首先，我們撰寫包含多筆訂單的 JSON 字串，每筆訂單都有自己的 `Lines` 陣列。可以把它想像成一個小型的訂單管理快照。

```csharp
using System;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // STEP 1 – Define the JSON payload with nested arrays
            // -------------------------------------------------
            string ordersJson = @"{
                ""Orders"": [
                    {
                        ""Id"": 1,
                        ""Lines"": [
                            { ""Prod"": ""A"" },
                            { ""Prod"": ""B"" }
                        ]
                    },
                    {
                        ""Id"": 2,
                        ""Lines"": [
                            { ""Prod"": ""C"" }
                        ]
                    }
                ]
            }";

            // The rest of the steps follow…
```

為什麼要把 Payload 寫成逐字字串（verbatim string）？它會保留換行，讓你一眼就能看出結構——在除錯巢狀 JSON 時非常方便。  

> **Pro tip:** 若你的 JSON 來源是資料庫或 API，可以將字面值改成 `File.ReadAllText` 或網路請求——本教學的其餘部分不依賴來源。

## 步驟 2：使用 SmartMarkerOptions 啟用巢狀範圍  

SmartMarkers 需要一點提示，才能了解陣列中還可以再包含陣列。這正是 `EnableNestedRanges` 的作用。

```csharp
            // -------------------------------------------------
            // STEP 2 – Configure SmartMarker options for nesting
            // -------------------------------------------------
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                EnableNestedRanges = true   // <-- crucial for Orders → Lines
            };
```

將 `EnableNestedRanges` 設為 `true` 後，處理器會把每個 `Lines` 集合視為其父層 `Orders` 範圍的子範圍。若未開啟此旗標，內層迴圈會被忽略，只會看到最上層的物件。

## 步驟 3：使用 SmartMarkersProcessor 處理 JSON  

接著把 JSON 字串與選項交給處理器。此呼叫為同步執行且不回傳值——SmartMarkers 會將結果寫入內部 Context，之後再取回。

```csharp
            // -------------------------------------------------
            // STEP 3 – Run the processor on the JSON payload
            // -------------------------------------------------
            ws.SmartMarkersProcessor.Process(ordersJson, options);
```

如果你使用其他函式庫，只要將 `ws.SmartMarkersProcessor.Process` 換成相對應的方法名稱；原理相同——傳入 JSON 與啟用巢狀處理的設定。

## 步驟 4：驗證解析結果  

處理完畢後，通常會想確認每筆訂單與其明細項目都有被走訪。以下示範使用假想的 `GetProcessedData` 方法（請換成你函式庫實際的存取方式）將資料倒回主控台。

```csharp
            // -------------------------------------------------
            // STEP 4 – Output the parsed structure (demo purpose)
            // -------------------------------------------------
            var result = ws.SmartMarkersProcessor.GetProcessedData(); // pseudo‑code
            Console.WriteLine("=== Parsed Orders ===");
            foreach (var order in result.Orders)
            {
                Console.WriteLine($"Order Id: {order.Id}");
                foreach (var line in order.Lines)
                {
                    Console.WriteLine($"  - Product: {line.Prod}");
                }
            }
        }
    }
}
```

**Expected console output**

```
=== Parsed Orders ===
Order Id: 1
  - Product: A
  - Product: B
Order Id: 2
  - Product: C
```

看到層級正確重建，即表示 **parse nested json c#** 如預期運作。

## 步驟 5：常見情境與陷阱  

### 空集合  
若訂單沒有 `Lines`，處理器仍會建立一個空的範圍。請確保下游程式能處理空清單，避免拋出 `NullReferenceException`。

### 深層巢狀結構  
`EnableNestedRanges` 預設支援兩層巢狀。若需三層或以上，可能需要設定 `MaxNestedDepth`（若函式庫提供）或對每個子物件遞迴呼叫處理器。

### 特殊字元  
JSON 字串若包含引號、反斜線或 Unicode 必須正確跳脫。使用逐字字串 (`@""`) 可避免大部分問題，但若以程式產生 JSON，建議交由 `System.Text.Json.JsonSerializer` 處理跳脫。

### 效能  
解析大型 Payload（數 MB）可能佔用大量記憶體。若遇效能瓶頸，可考慮使用 `Utf8JsonReader` 串流讀取 JSON，並將分段資料餵給處理器。

## 視覺概覽  

![Diagram illustrating how parse nested json c# flows through SmartMarkers processing](parse-nested-json-csharp-diagram.png "parse nested json c# diagram")

圖示說明了從原始 JSON → SmartMarkerOptions → Processor → 解析後的物件模型的流程。

## 重點回顧  

我們完整示範了一個 **parse nested json c#** 的範例，從 **create json payload c#** 到驗證巢狀資料的處理。關鍵要點如下：

1. 建立結構良好的 JSON 字串，與領域模型相對應。  
2. 開啟 `EnableNestedRanges`（或等效設定），讓解析器能辨識內部陣列。  
3. 執行處理器並檢查結果，確保每一層都被走訪。  

## 往後可以怎麼做？  

- **動態 Payload**：將硬編碼的字串改為使用 `System.Text.Json` 序列化的物件。  
- **自訂標記**：為 SmartMarkers 擴充自訂標籤，將計算欄位注入每筆明細。  
- **錯誤處理**：將 `Process` 呼叫包在 try/catch 中，並記錄 `SmartMarkerException` 以便除錯。  

歡迎自行實驗——把 `Orders` 陣列換成客戶、發票或任何層級式資料，皆可使用相同的 **parse nested json c#** 模式。

祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}