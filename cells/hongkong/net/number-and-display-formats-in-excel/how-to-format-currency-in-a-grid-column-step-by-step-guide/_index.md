---
category: general
date: 2026-02-15
description: 如何在 C# 中使用「設定欄位數字格式」快速格式化貨幣，並套用自訂數值格式。學習透過名稱取得欄位以及設定網格欄位對齊。
draft: false
keywords:
- how to format currency
- set column number format
- apply custom numeric format
- retrieve column by name
- set grid column alignment
language: zh-hant
og_description: 如何在 C# 中對資料格的欄位進行貨幣格式化。本教學示範如何依名稱取得欄位、設定欄位的數字格式、套用自訂數值格式，以及設定欄位對齊方式。
og_title: 如何在網格欄位中格式化貨幣 – 完整指南
tags:
- C#
- GridFormatting
- UI
title: 如何在網格欄位中格式化貨幣 – 步驟指南
url: /zh-hant/net/number-and-display-formats-in-excel/how-to-format-currency-in-a-grid-column-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Grid 欄位中格式化貨幣 – 完整程式教學

有沒有想過 **如何在資料格欄位中格式化貨幣**，卻又不想抓狂？你並不是唯一有此困擾的人。當你看到像 `1234.5` 這樣的純數字，卻希望它能神奇地顯示成 `$1,234.50` 時，答案通常只需要幾行設定。  

在本指南中，我們將 **依名稱取得欄位**、**設定欄位數字格式**，以及 **套用自訂數值格式**，以符合一般會計排版。過程中，我們還會 **設定資料格欄位對齊方式**，並加入細緻的邊框，使 UI 更加精緻。

> **TL;DR** – 完成後，你將擁有一段即時可執行的程式碼，能將原始小數轉換為在任何 `GridJs` 風格控制項中美觀的貨幣顯示。

---

## 需要的條件

- 一個 .NET 專案（任何支援 C# 8.0+ 的版本 – Visual Studio 2022 表現良好）。  
- 一個提供 `Columns` 集合的資料格元件（範例使用虛構的 `GridJs` 類別，但概念可套用於 DevExpress、Telerik 或 Syncfusion 等資料格）。  
- 基本熟悉 C# 語法 – 不需要進階技巧。

如果你已經具備上述條件，太好了。若沒有，只要建立一個 console 應用程式即可；資料格可以用模擬方式示範。

---

## 步驟實作說明

在每個步驟下方，你會看到簡潔的程式碼區塊、**為何** 此行重要的簡短說明，以及避免常見陷阱的小技巧。

### ## 步驟 1 – 依名稱取得 “Amount” 欄位

```csharp
// Step 1: Retrieve the "Amount" column from the grid
var amountColumn = gridJs.Columns["Amount"];
if (amountColumn == null)
{
    throw new InvalidOperationException("Column 'Amount' does not exist. Verify the column name or check the grid's schema.");
}
```

**為何重要：**  
大多數資料格 API 會以類似字典的索引子公開欄位。透過欄位標題名稱 (`"Amount"`) 取得欄位，即可在不觸及底層資料來源的情況下調整其外觀。  

**小技巧：** 永遠檢查 `null` 回傳 – 欄位名稱拼寫錯誤或動態結構變更，否則在執行時會拋出 `NullReferenceException`。

---

### ## 步驟 2 – 使用自訂貨幣遮罩設定欄位數字格式

```csharp
// Step 2: Apply a custom numeric format for currency values
amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";
```

**為何重要：**  
格式字串遵循 Excel 會計格式慣例：

- `_(* #,##0.00_)` → 正數，右對齊，貨幣符號前留一個空格。  
- `_(* (#,##0.00)` → 負數以括號包住。  
- `_(* \"-\"??_)` → 零值顯示為破折號。  
- `_(@_)` → 文字值保持不變。

使用 **套用自訂數值格式** 可完整掌控千位分隔符、 小數位數以及貨幣符號的位置。  

**邊緣情況：** 若應用程式需符合不同語系（例如歐元而非美元），請將前置空格換成相應符號，或在資料來源使用支援 `CultureInfo` 的格式化方式。

---

### ## 步驟 3 – 為提升可讀性將欄位內容右對齊

```csharp
// Step 3: Align the column contents to the right for better readability
amountColumn.Alignment = GridAlignment.Right;
```

**為何重要：**  
當貨幣值在小數點對齊時，更容易瀏覽。將 **set grid column alignment** 設為 `Right`，可模仿試算表顯示金額的方式。  

**注意事項：** 某些資料格會忽略包含自訂模板的儲存格對齊設定。若發現對齊未生效，請再次確認該欄位未使用自訂儲存格渲染器。

---

### ## 步驟 4 – 為欄位儲存格加入細灰色邊框

```csharp
// Step 4: Add a thin gray border around the column cells
amountColumn.Border = new GridBorder
{
    Color = Color.Gray,
    Style = BorderLineStyle.Thin
};
```

**為何重要：**  
細緻的邊框可將 “Amount” 欄位與相鄰欄位區隔開，特別是在資料格使用交錯列色時。這是一種視覺提示，表明該資料屬於獨立的財務數字。  

**小技巧：** 若列印時需要較粗的線條，可將 `BorderLineStyle` 調整為 `Medium`，或將 `Color` 改為 `Color.Black`。

---

## 完整範例

以下是完整程式碼片段，可直接放入使用 `GridJs` 風格控制項的 WinForms 或 WPF 專案。此範例同時會將格式化後的值輸出至主控台，讓你在沒有 UI 的情況下驗證結果。

```csharp
using System;
using System.Drawing;   // For Color
using GridLibrary;      // Hypothetical namespace for GridJs

namespace GridCurrencyDemo
{
    class Program
    {
        static void Main()
        {
            // Create a mock grid and add a sample column
            var gridJs = new GridJs();
            gridJs.Columns.Add(new GridColumn
            {
                Name = "Amount",
                Header = "Amount",
                DataType = typeof(decimal)
            });

            // Populate some sample data
            gridJs.Rows.Add(new { Amount = 1234.5m });
            gridJs.Rows.Add(new { Amount = -567.89m });
            gridJs.Rows.Add(new { Amount = 0m });

            // ---- Formatting steps ------------------------------------------------
            // 1️⃣ Retrieve the "Amount" column
            var amountColumn = gridJs.Columns["Amount"]
                ?? throw new InvalidOperationException("Column 'Amount' not found.");

            // 2️⃣ Apply custom numeric format for currency
            amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";

            // 3️⃣ Right‑align the values
            amountColumn.Alignment = GridAlignment.Right;

            // 4️⃣ Add a thin gray border
            amountColumn.Border = new GridBorder
            {
                Color = Color.Gray,
                Style = BorderLineStyle.Thin
            };
            // -----------------------------------------------------------------------

            // Render the grid (in a real UI you would call gridJs.Render() or similar)
            Console.WriteLine("Formatted Currency Grid:");
            foreach (var row in gridJs.Rows)
            {
                var rawValue = (decimal)row.Amount;
                // The grid library would automatically apply NumberFormat when displaying.
                // For console demo we mimic the formatting:
                string formatted = rawValue.ToString("#,##0.00", System.Globalization.CultureInfo.InvariantCulture);
                if (rawValue < 0)
                    formatted = $"({formatted.TrimStart('-')})";
                else if (rawValue == 0)
                    formatted = "-";

                Console.WriteLine($"| {formatted,15} |");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**預期的主控台輸出**

```
Formatted Currency Grid:
|        1,234.50 |
|       (567.89) |
|               - |
```

請注意，正數會右對齊，負數以括號顯示，零則顯示破折號——正是自訂格式字串所規定的行為。

---

## 常見問題與邊緣情況

| Question | Answer |
|----------|--------|
| *如果資料格使用不同的文化設定（例如 € 而非 $）？* | 將格式字串中的前置空格換成所需的符號，或讓資料來源使用 `CultureInfo.CurrentCulture` 產生預先格式化的字串。 |
| *我可以在多個欄位重複使用相同的格式嗎？* | 當然可以。將格式字串存於常數 (`const string CurrencyMask = "...";`) 中，於需要貨幣的地方直接指派即可。 |
| *如果欄位包含字串值會發生什麼事？* | 格式字串僅作用於數值型別。字串會保持原樣通過，這也是遮罩最後一段 (`_(@_)`) 的存在原因——保留非數值內容。 |
| *會不會影響效能？* | 可忽略不計。格式於渲染時套用，而非資料取得階段。除非每幀要渲染上千列，否則不會感受到任何延遲。 |
| *如何在列印報告時加粗邊框？* | 將 `BorderLineStyle.Thin` 換成 `BorderLineStyle.Medium` 或 `BorderLineStyle.Thick`。某些函式庫亦允許直接指定像素寬度。 |

---

## 結語

我們已完整說明了 **如何在資料格欄位中格式化貨幣**：從依名稱取得欄位、設定欄位數字格式、套用自訂數值格式、對齊儲存格，到加入雅緻的邊框。完整範例即插即用，展示了你可預期的視覺效果。

如果你想更進一步，試試以下方向：

- **動態語系** – 依使用者的語系切換格式字串。  
- **條件式**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}