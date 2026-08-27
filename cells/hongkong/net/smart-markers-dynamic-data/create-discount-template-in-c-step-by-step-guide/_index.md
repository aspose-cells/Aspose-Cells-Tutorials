---
category: general
date: 2026-02-14
description: 快速建立折扣範本，並學習如何在試算表中套用折扣、將資料注入範本，以及為智慧標記定義變數前綴。
draft: false
keywords:
- create discount template
- apply discount in spreadsheet
- inject data into template
- define variable prefix
language: zh-hant
og_description: 使用 C# 建立折扣範本。學習在試算表中套用折扣、將資料注入範本，並為智慧標記定義變數前綴。
og_title: 建立折扣模板 – 完整 C# 教學
tags:
- C#
- SmartMarker
- Spreadsheet Automation
title: 在 C# 中建立折扣範本 – 逐步指南
url: /zh-hant/net/smart-markers-dynamic-data/create-discount-template-in-c-step-by-step-guide/
---

have # etc.

Now produce final content with all shortcodes and placeholders.

Let's assemble.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立折扣範本 – 完整 C# 教學

是否曾經需要為銷售報告 **create discount template**，但不確定如何自動將數字輸入試算表？你並不孤單。在本教學中，我們將會完整示範如何 **create discount template**，接著 **apply discount in spreadsheet** 單元格，**inject data into template**，甚至 **define variable prefix** 於你的智慧標記——全部使用簡潔的 C# 程式碼。

我們會先說明問題，然後直接跳到可直接 copy‑paste 的可行解決方案。完成後，你將擁有一套可重複使用的模式，無論是產生發票、價目表，或任何需要動態折扣的試算表，都能輕鬆應對。

---

## 您將學到

- 如何設計具備折扣感知的試算表範本。
- 如何設定自訂的 `VariablePrefix` / `VariableSuffix`，讓標記易於辨識。
- 如何將匿名物件 (`discountData`) 傳入 `SmartMarkerProcessor`。
- 結果公式 (`=IF(#Discount#>0, A1*(1-#Discount#), A1)`) 如何自動計算最終價格。
- 處理零折扣列或多層折扣等邊緣情況的技巧。

**Prerequisites** – 最近的 .NET 執行環境 (≥ .NET 6)、對 `Aspose.Cells`（或類似）函式庫的參考，該函式庫提供 `SmartMarkerProcessor`，以及對 C# 語法的基本了解。無需額外套件。

---

## 步驟 1：在試算表中建立折扣範本

首先，開啟一個新活頁簿（或使用既有的），並在要套用折扣的地方放置佔位符。將此範本視為一個普通的 Excel 檔案，內含將由處理器取代的「智慧標記」。

```csharp
using Aspose.Cells;          // SmartMarkerProcessor lives here
using System;

// Step 1: Load or create a workbook
Workbook wb = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = wb.Worksheets[0];
ws.Name = "Pricing";

// Put a header
ws.Cells["A1"].PutValue("Original Price");
ws.Cells["B1"].PutValue("Discounted Price");

// Sample data row – the formula will be injected later
ws.Cells["A2"].PutValue(100);               // original price = 100
ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";
```

**Why this matters:** 在公式中嵌入 `#Discount#`，我們告訴處理器折扣值應放置的位置。`SmartMarkerProcessor` 會在稍後將 `#Discount#` 替換為您提供的數字，公式的其他部分保持不變。

---

## 步驟 2：為智慧標記定義變數前綴

開箱即用時，許多函式庫會搜尋 `${Variable}` 或 `{{Variable}}`。在本例中，我們想要一個簡潔、易讀的標記，因此明確 **define variable prefix** 及其後綴。

```csharp
// Step 2: Configure how markers are identified
var smartMarkerOptions = new SmartMarkerOptions
{
    VariablePrefix = "#",   // start marker
    VariableSuffix = "#"    // end marker
};
```

**Pro tip:** 使用 `#` 可讓標記在 Excel 公式欄中既短小又易於辨識。若需避免與現有 Excel 函式衝突，可改用其他配對（例如 `[[` 與 `]]`）。

---

## 步驟 3：使用 SmartMarkerProcessor 將資料注入範本

現在將實際的折扣值傳入。處理器會掃描工作表，找到每一個 `#Discount#`，並以匿名物件中提供的值取代它。

```csharp
// Step 3: Prepare the data that will be injected
var discountData = new { Discount = 0.10, Total = 100 };

// Run the processor – it mutates the workbook in‑place
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);
```

此呼叫之後，`B2` 的公式會變成：

```
=IF(0.1>0, A2*(1-0.1), A2)
```

當活頁簿計算時，`B2` 會顯示 **90**，即對原價 100 套用 10 % 折扣的結果。

**Why it works:** `StartSmartMarkerProcessing` 會遍歷每個儲存格，尋找 `#Discount#` 代碼，並替換為數值。由於代碼位於 `IF` 陳述式內，試算表仍能處理折扣為零的情況。

---

## 步驟 4：在試算表中套用折扣 – 驗證結果

讓我們觸發計算，並將最終價格輸出至主控台。此步驟證明 **apply discount in spreadsheet** 工作流程已成功。

```csharp
// Step 4: Force calculation and read the result
wb.CalculateFormula();                     // ensures all formulas are up‑to‑date
double discountedPrice = ws.Cells["B2"].DoubleValue;

Console.WriteLine($"Original: {ws.Cells["A2"].DoubleValue}");
Console.WriteLine($"Discounted (10%): {discountedPrice}");
```

**Expected output**

```
Original: 100
Discounted (10%): 90
```

若將 `discountData.Discount` 改為 `0.25` 並重新執行處理器，輸出會自動顯示 25 % 折扣——不需額外程式碼。

---

## 步驟 5：處理邊緣情況與多重折扣

### Zero‑Discount Rows

有時商品未參加促銷。為了讓公式更健全，先前放置的 `IF` 已涵蓋此情況：當 `#Discount#` 為 `0` 時，原價會直接傳遞，不受影響。

```csharp
var noDiscountData = new { Discount = 0.0 };
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(noDiscountData, smartMarkerOptions);
wb.CalculateFormula();
Console.WriteLine($"No discount applied: {ws.Cells["B2"].DoubleValue}");
```

### Multiple Discount Columns

若需為每列設定不同折扣，可為每列使用獨立標記，例如 `#Discount1#`、`#Discount2#`，並傳入集合：

```csharp
var multiDiscountData = new[]
{
    new { Discount = 0.05 },   // row 2
    new { Discount = 0.15 }    // row 3
};

ws.SmartMarkerProcessor.StartSmartMarkerProcessing(multiDiscountData, smartMarkerOptions);
```

處理器會依序對應標記，因此每列皆取得正確的數值。

---

## 完整可執行範例

以下為完整、可直接複製的程式碼，涵蓋上述所有步驟。將其儲存為 `Program.cs`，加入對 `Aspose.Cells` 的參考，然後執行。

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook & template
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Pricing";
        ws.Cells["A1"].PutValue("Original Price");
        ws.Cells["B1"].PutValue("Discounted Price");
        ws.Cells["A2"].PutValue(100);
        ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";

        // 2️⃣ Define marker delimiters
        var smartMarkerOptions = new SmartMarkerOptions
        {
            VariablePrefix = "#",
            VariableSuffix = "#"
        };

        // 3️⃣ Inject a 10 % discount
        var discountData = new { Discount = 0.10 };
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);

        // 4️⃣ Calculate and display result
        wb.CalculateFormula();
        double original = ws.Cells["A2"].DoubleValue;
        double discounted = ws.Cells["B2"].DoubleValue;

        Console.WriteLine($"Original: {original}");
        Console.WriteLine($"Discounted (10%): {discounted}");

        // Optional: Save the workbook to verify manually
        wb.Save("DiscountedPricing.xlsx");
    }
}
```

執行後會印出預期的數字，並產生 `DiscountedPricing.xlsx` 檔案，您可在 Excel 中開啟，看到公式已正確解析。

---

## 結論

現在您已掌握如何 **create discount template**、**apply discount in spreadsheet**、**inject data into template**，以及為智慧標記 **define variable prefix**——只需幾行簡潔的 C# 程式碼。此模式具備可擴充性，只要更換匿名物件或傳入集合以進行批次更新，同一範本即可處理任何折扣情境。

想挑戰更高階的應用嗎？試試看：

- 在折扣之外加入稅金計算。
- 從資料庫取得折扣百分比，而非硬編碼。
- 使用條件格式化，將高折扣的列標示出來。

這些延伸功能不會改變核心概念，同時提升折扣範本的實用性。

有任何問題或酷炫的使用案例嗎？在下方留言，我們一起快樂寫程式！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}