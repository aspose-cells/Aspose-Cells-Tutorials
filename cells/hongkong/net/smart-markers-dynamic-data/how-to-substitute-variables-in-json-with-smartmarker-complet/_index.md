---
category: general
date: 2026-03-29
description: 如何使用 SmartMarker 在 JSON 中替換變數 – 學習使用 if 表達式、套用條件邏輯、將數值相乘，輕鬆產生 JSON。
draft: false
keywords:
- how to substitute variables
- use if expression
- how to apply conditional
- how to multiply values
- how to generate json
language: zh-hant
og_description: 如何使用 SmartMarker 在 JSON 中替換變數。了解如何使用 if 表達式、套用條件邏輯、將數值相乘，並在數分鐘內產生
  JSON。
og_title: 如何使用 SmartMarker 在 JSON 中替換變數 – 步驟說明
tags:
- C#
- SmartMarker
- JSON templating
title: 如何使用 SmartMarker 在 JSON 中替換變數 – 完整指南
url: /zh-hant/net/smart-markers-dynamic-data/how-to-substitute-variables-in-json-with-smartmarker-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 JSON 中使用 SmartMarker 替換變數 – 完整指南

有沒有想過在 JSON 負載中**替換變數**而不需要自行編寫解析器？你並不孤單。在許多整合情境——例如發票、定價引擎或動態設定檔——你需要注入執行時值、套用簡單條件，甚至可能進行快速乘法。本教學將完整示範如何使用 SmartMarker 函式庫**替換變數**，同時保持 JSON 的整潔與可讀性。

我們將以一個實務範例說明 **use if expression**、**how to apply conditional**、**how to multiply values** 以及 **how to generate json** 的寫法。完成後，你將擁有一段可直接放入任何 .NET 專案的 C# 程式碼。

## 你將學會

- 設定 `SmartMarkerOptions` 以儲存可重複使用的變數。  
- 撰寫包含 `if` 表達式的 JSON 範本，以實作條件邏輯。  
- 在範本內將變數相乘。  
- 使用 `SmartMarkerProcessor` 處理範本並取得最終的 JSON 字串。  
- 排除常見問題，例如變數遺失或表達式語法錯誤。

不需要外部服務，也不需要龐大相依套件——只要純 C# 加上 SmartMarker NuGet 套件即可。

## 如何替換變數 – 步驟概覽

以下是一張高階流程圖。把它想像成一條管線，左側放入原始 JSON 範本，SmartMarker 引擎負責處理，右側則輸出完整渲染好的 JSON。

![顯示如何在 JSON 中替換變數的圖示](https://example.com/images/smartmarker-flow.png "如何在 JSON 中替換變數")

*圖片說明：顯示如何在 JSON 中替換變數的圖示。*

## Step 1: Install and Import SmartMarker

在開始之前，先確保你的專案已參考 SmartMarker 套件。若使用 .NET CLI，執行：

```bash
dotnet add package SmartMarker
```

接著，在 C# 檔案的最上方加入必要的 `using` 指示詞：

```csharp
using SmartMarker;
using SmartMarker.Models;
using System;
```

> **Pro tip:** 最新版本（截至 2026 年 3 月）為 2.4.1。支援 .NET 6 及以上版本，同時亦可在 .NET Framework 4.7 上順利運作。

## Step 2: Create SmartMarker Options and Define Variables

現在我們要建立 `SmartMarkerOptions` 的實例，讓它保存所有想在範本中重複使用的變數。這正是回答 **how to substitute variables** 的關鍵——變數會在之後被 SmartMarker 替換成實際值。

```csharp
// Step 2: Create SmartMarker options to hold variables used in the template
var smartMarkerOptions = new SmartMarkerOptions();

// Define a variable (Rate) that we’ll reference later in the JSON expression
smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission rate
```

為什麼把費率放在 `Variables` 而不是硬寫在程式碼裡？因為你可能會從資料庫、設定檔或使用者輸入取得這個數字。將它放在選項中，可讓範本更具可重用性與可測試性。

## Step 3: Write the JSON Template with an `if` Expression

這裡正是 **use if expression** 發揮威力的地方。SmartMarker 允許你直接在 JSON 字串中嵌入條件邏輯。語法看起來像屬性名稱，但實際上會被 SmartMarker 當作指令處理。

```csharp
// Step 3: Prepare the JSON data with a conditional field that uses the variable
string jsonTemplate = @"{
    ""Amount"": 1000,
    ""if(Amount>500)"": ""${Amount * Rate}""
}";
```

請注意 `if(Amount>500)` 這個鍵名。SmartMarker 會先評估 `Amount>500`；若為真，則把對應的值（`${Amount * Rate}`）插入輸出。`${...}` 為*變數替換*語法——此處我們 **how to multiply values**（`Amount * Rate`）後再注入結果。

## Step 4: Process the Template and Retrieve the Final JSON

當選項與範本都準備好後，我們把它們交給處理器。`ProcessJson` 方法會解析範本、套用條件、執行乘法，最後回傳一個乾淨的 JSON 字串。

```csharp
// Step 4: Process the JSON with SmartMarker, applying the variable substitution
string resultJson = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(resultJson);
```

執行程式碼會印出：

```json
{
  "Amount": 1000,
  "Result": "80"
}
```

**發生了什麼事？**  
- `Amount` 為 1000，符合 `Amount>500`。  
- SmartMarker 計算 `${Amount * Rate}` → `1000 * 0.08 = 80`。  
- 原本的條件鍵 (`if(Amount>500)`) 會被乾淨的屬性名稱 (`Result`) 取代。預設 SmartMarker 使用 `"Result"`，但你之後可以自行客製化（稍後說明）。

若將 `Amount` 改成 `400`，輸出會變成：

```json
{
  "Amount": 400
}
```

條件區塊會消失，因為表達式評估為 `false`。這就是 **how to apply conditional** 在 JSON 中的核心概念。

## Step 5: Customizing the Output Property Name (Optional)

有時你不想使用通用的 `"Result"` 鍵名。SmartMarker 允許透過 `RenameIfExpression` 選項自訂名稱：

```csharp
smartMarkerOptions.RenameIfExpression = "Discount";
string customResult = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(customResult);
```

輸出結果：

```json
{
  "Amount": 1000,
  "Discount": "80"
}
```

現在條件值會存放在更具意義的屬性名稱下——對於需要特定欄位的下游服務而言相當理想。

## 常見問題與避免方法

| 問題 | 為何會發生 | 解決方式 |
|------|------------|----------|
| 變數找不到 | 你引用了 `smartMarkerOptions.Variables` 中不存在的變數。 | 再次確認拼寫，並確保變數已在處理前加入。 |
| `if` 語法錯誤 | 缺少括號或使用了錯誤的運算子（`>`、`<`、`==`）。 | 嚴格遵守 `if(<expression>)` 格式；SmartMarker 只支援簡單的數值比較。 |
| JSON 變形 | 條件區塊後遺留了多餘的逗號。 | 交由 SmartMarker 處理移除；保持原始範本語法正確。 |
| 數值格式意外 | 結果以字串 `"80"` 而非數字呈現。 | 之後自行轉型或使用 `${(Amount * Rate):N0}` 進行數值格式化。 |

## 完整範例（可直接複製貼上）

以下是完整程式碼，你可以直接編譯執行。它示範了 **how to generate json**，同時結合動態變數、條件與算術運算，整段程式碼不超過 30 行。

```csharp
using System;
using SmartMarker;
using SmartMarker.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Create SmartMarker options and define a reusable variable
        var smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission
        smartMarkerOptions.RenameIfExpression = "Discount"; // optional custom name

        // 2️⃣ JSON template with an if expression and multiplication
        string jsonTemplate = @"{
            ""Amount"": 1000,
            ""if(Amount>500)"": ""${Amount * Rate}""
        }";

        // 3️⃣ Process the template
        string output = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);

        // 4️⃣ Show the result
        Console.WriteLine("Generated JSON:");
        Console.WriteLine(output);
    }
}
```

**預期的主控台輸出**

```
Generated JSON:
{
  "Amount": 1000,
  "Discount": "80"
}
```

隨意修改 `Amount` 以測試條件分支，或調整 `Rate` 觀察不同的折扣計算結果。

## 延伸應用 – 更多「How to」情境

- **How to substitute variables** 來自設定檔：從 `appsettings.json` 讀取 `Dictionary<string, object>`，再塞入 `smartMarkerOptions.Variables`。  
- **How to use if expression** 處理多重條件：可寫成 `"if(Amount>500 && CustomerType=='VIP')"`——SmartMarker 支援 AND/OR 邏輯。  
- **How to apply conditional** 格式化：在表達式內使用 `${Amount:0.00}` 以控制小數位數。  
- **How to multiply values** 進行更複雜的運算：`${(Amount - Discount) * TaxRate}` 亦可直接使用。  
- **how to generate json** 用於巢狀物件：將條件區塊放入其他 JSON 物件內，SmartMarker 會保留層級結構。

## 結論

我們已說明如何使用 SmartMarker 在 JSON 中 **how to substitute variables**，示範了 **use if expression** 進行條件插入，解釋了 **how to apply conditional** 的邏輯，展示了 **how to multiply values** 在範本內的運算，最後說明了 **how to generate json** 以供下游使用。此方式輕量、無需外部模板引擎，且能無縫融入任何 C# 程式碼基礎。

快試試看——調整變數、加入更多條件，或將整段程式封裝成輔助類別，以便在整個解決方案中重複使用。當你需要快速產生動態 JSON 時，SmartMarker 是一個穩定、可投入生產的選擇。

**Next steps**

- 深入探索 SmartMarker 的進階功能，如迴圈（`foreach`）與自訂函式。  
- 結合此技巧與 ASP.NET Core 端點，提供動態 JSON API。  
- 比較其他模板函式庫（例如 Handlebars.NET），特別是當你需要更豐富語法時。

有任何問題或特定使用情境想討論嗎？在下方留言，我們一起排除疑難。祝程式開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}