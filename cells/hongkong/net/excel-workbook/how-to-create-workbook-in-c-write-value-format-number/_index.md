---
category: general
date: 2026-03-01
description: 如何在 C# 中快速建立工作簿——學習寫入值到儲存格、設定儲存格數字格式，以及以簡單步驟格式化儲存格數字。
draft: false
keywords:
- how to create workbook
- write value to cell
- format cell number
- set cell number format
- how to write cell
language: zh-hant
og_description: 如何在 C# 中建立工作簿？本指南將示範如何將值寫入儲存格、設定儲存格數字格式，以及在僅幾行程式碼內格式化儲存格數字。
og_title: 如何在 C# 中建立工作簿 – 寫入值與格式化數字
tags:
- C#
- Aspose.Cells
- Excel Automation
title: 如何在 C# 中建立工作簿 – 寫入值與格式化數字
url: /zh-hant/net/excel-workbook/how-to-create-workbook-in-c-write-value-format-number/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中建立 Workbook – 寫入值與設定數字格式

在需要即時產生 Excel 檔案時，如何在 C# 中建立 workbook 是一項常見任務。本指南將一步步說明如何將值寫入儲存格，並設定儲存格的數字格式，讓最終的工作表看起來更專業。

如果你曾經盯著一張空白試算表，卻發現數字顯示了過多的小數位，別擔心。我們會從初始化 workbook 物件說起，教你設定自訂的數字格式，並提供一些在實作過程中可能遇到的邊緣情況的技巧。

## 你將學會

- **初始化** 一個新的 `Workbook` 實例。  
- 使用 `PutValue` 方法 **寫入儲存格值**。  
- 透過 `Style` 物件 **設定儲存格數字格式**，實現乾淨的兩位小數顯示。  
- 讀回儲存格或在 Excel 中開啟檔案，以驗證結果。  

不需要除 Aspose.Cells（或其他類似 API）之外的外部函式庫，程式碼可在 .NET 6+ 環境下直接執行，無需額外設定。

---

## 建立 Workbook – 初始化物件

首先，你需要一個 workbook 物件來容納工作表。把 `Workbook` 想成整個 Excel 檔案，而每個 `Worksheet` 則是其中的一個分頁。

```csharp
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

*為什麼這很重要*：建立 workbook 會配置內部結構，之後才能放入列、欄與格式。若沒有這個物件，就無法寫入儲存格值。

> **小技巧**：若要使用既有檔案，將 `new Workbook()` 改成 `new Workbook("template.xlsx")`，即可載入範本並保留其樣式。

## 寫入儲存格值

現在有了 workbook，讓我們把一個數字寫入第一個工作表的 **A1** 儲存格。

```csharp
// Step 2: Access cell A1 in the first worksheet
Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

// Step 3: Insert a numeric value into the cell
cellA1.PutValue(123.456789);
```

*為什麼使用 `PutValue`*：此方法會自動偵測資料類型，無需手動轉型或轉換。它也會保留儲存格原有的樣式，方便之後 **設定儲存格數字格式**。

### 快速檢查

若讀回儲存格，你會看到原始值：

```csharp
double raw = cellA1.DoubleValue; // raw == 123.456789
```

這就是套用任何格式前的數字。

## 設定儲存格數字格式

直接顯示帶有多位小數的 double 並不友善。我們將它限制為兩位有效數字。

```csharp
// Step 4: Apply a style that formats the number with two significant digits
cellA1.SetStyle(new Style() { Number = 2 });
```

`Number` 屬性對應 Excel 內建的數字格式 ID。`2` 代表「保留兩位小數的數字」。若需要其他格式（例如貨幣或日期），可使用其他 ID 或自訂格式字串。

### 替代方案：自訂格式字串

```csharp
Style customStyle = workbook.CreateStyle();
customStyle.Custom = "#,##0.00"; // forces two decimals with thousand separator
cellA1.SetStyle(customStyle);
```

*為什麼選擇自訂樣式*？當內建 ID 無法滿足你的區域設定時，自訂樣式提供完整的控制權。

## 驗證輸出（可選但建議）

套用樣式後，你可以儲存 workbook 並在 Excel 中開啟，以確認外觀是否如預期。

```csharp
// Save the workbook to a file
workbook.Save("FormattedWorkbook.xlsx");

// Or, for quick verification in code:
string displayed = cellA1.StringValue; // "123.46"
Console.WriteLine($"Displayed value: {displayed}");
```

你應該會在 A1 儲存格看到 **123.46**——正好兩位小數，這是因為我們設定了格式。

---

### 完整範例程式

以下是一個可直接貼到 Console App 的完整範例。

```csharp
using System;
using Aspose.Cells;   // Ensure you have the Aspose.Cells NuGet package

class Program
{
    static void Main()
    {
        // Initialize the workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet and cell A1
        Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

        // Write a numeric value
        cellA1.PutValue(123.456789);

        // Apply a two‑decimal number format
        cellA1.SetStyle(new Style() { Number = 2 });

        // Save to disk (optional)
        workbook.Save("FormattedWorkbook.xlsx");

        // Output the displayed text for verification
        Console.WriteLine($"Cell A1 shows: {cellA1.StringValue}");
    }
}
```

**執行程式時的預期輸出：**

```
Cell A1 shows: 123.46
```

開啟 `FormattedWorkbook.xlsx`，你會看到相同的格式化數值。

---

## 常見變化與邊緣案例

### 1. 不同的數字格式

| 目標 | 格式 ID | 程式碼片段 |
|------|-----------|--------------|
| 貨幣（兩位小數） | 5 | `cellA1.SetStyle(new Style() { Number = 5 });` |
| 百分比（無小數） | 10 | `cellA1.SetStyle(new Style() { Number = 10 });` |
| 科學記號 | 11 | `cellA1.SetStyle(new Style() { Number = 11 });` |

若內建 ID 都不符合需求，可回退使用前述的自訂字串。

### 2. 依文化設定的十進位分隔符

某些地區使用逗號作為小數點。你可以強制使用文化感知的格式：

```csharp
Style cultureStyle = workbook.CreateStyle();
cultureStyle.Custom = "#,##0.00"; // works for most European locales
cellA1.SetStyle(cultureStyle);
```

### 3. 寫入文字而非數字

若要 **how to write cell** 為字串，只需將字串傳給 `PutValue`：

```csharp
cellA1.PutValue("Total Revenue");
```

不需要設定數字格式，但仍可套用字型樣式。

### 4. 大量資料集

若要寫入上千列，使用批次插入 (`Cells.ImportArray`) 會比逐筆 `PutValue` 快。格式設定方式相同，只是將樣式套用到整個範圍：

```csharp
Range range = workbook.Worksheets[0].Cells.CreateRange("B2:B1001");
range.ApplyStyle(new Style() { Number = 2 });
```

---

## 常見問答

**Q: 這能在 .NET Core 上使用嗎？**  
A: 完全可以。Aspose.Cells 支援 .NET Standard 2.0 及以上版本，故可在 .NET 5、.NET 6 或 .NET 7 中直接使用，無需修改。

**Q: 若需要超過兩位小數該怎麼做？**  
A: 將 `Number` 屬性改為對應的內建 ID（例如 `3` 代表三位小數），或自行調整自訂格式字串（如 `"#,##0.000"`）。

**Q: 能一次套用整欄的格式嗎？**  
A: 可以。使用 `Cells["A:A"]` 取得整欄，然後呼叫 `SetStyle` 即可。

---

## 結論

現在你已掌握 **如何在 C# 中建立 workbook**、**寫入儲存格值**，以及 **設定儲存格數字格式**，讓數字呈現方式完全符合需求。熟悉這些基礎後，你就能輕鬆產生專業的 Excel 報表、發票或資料匯出，且只需極少的程式碼。

接下來，你可以探索 **格式化日期、百分比或條件格式**——這些都建立在本篇所介紹的原則之上。深入閱讀 Aspose.Cells 文件，了解更進階的樣式選項，或嘗試在同一本 workbook 中加入多個工作表，以製作更豐富的報告。

祝開發順利，記得：一份排版良好的試算表，就是

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}