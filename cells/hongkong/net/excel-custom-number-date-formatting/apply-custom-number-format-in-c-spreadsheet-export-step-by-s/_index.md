---
category: general
date: 2026-04-07
description: 在試算表儲存格套用自訂數字格式，並學習在使用 C# 匯出儲存格值時如何格式化數字。快速完整指南。
draft: false
keywords:
- apply custom number format
- format number in spreadsheet
- how to format numeric cell
- how to export cell value
language: zh-hant
og_description: 將自訂數字格式套用於試算表儲存格，並將其匯出為格式化字串。了解如何在試算表中格式化數字並匯出儲存格值。
og_title: 套用自訂數字格式 – 完整 C# 匯出教學
tags:
- C#
- Spreadsheet
- Number Formatting
title: 在 C# 試算表匯出中套用自訂數字格式 – 逐步指南
url: /zh-hant/net/excel-custom-number-date-formatting/apply-custom-number-format-in-c-spreadsheet-export-step-by-s/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 試算表匯出中套用自訂數字格式 – 完整教學

是否曾需要 **套用自訂數字格式** 到儲存格，然後再從試算表中取出該格式化的字串？你並不孤單。許多開發者在發現取得的是原始值，而非預期的美觀、符合語系的字串時，常會卡關。在本指南中，我們將示範如何在試算表儲存格中 **format number in spreadsheet**，以及如何使用熱門的 C# 試算表函式庫將儲存格值匯出為格式化字串。

完成本教學後，你將能夠 **套用自訂數字格式** 到任何數值儲存格，使用 `ExportTable` 匯出結果，並看到在 UI 或報表中顯示的正確輸出。無需額外文件——所有內容都在此。

## 前置條件

- .NET 6.0 或更新版本（此程式碼亦可於 .NET Framework 4.7+ 執行）
- 參考提供 `Workbook`、`Worksheet` 與 `ExportTableOptions` 的試算表函式庫（例如 **Aspose.Cells** 或 **GemBox.Spreadsheet**；此處示範的 API 與 Aspose.Cells 相符）
- 基本的 C# 知識——只要會寫 `Console.WriteLine` 即可上手

> **Pro tip:** 若使用其他函式庫，屬性名稱通常相似（`NumberFormat`、`ExportAsString`），只要對應即可。

## 本教學涵蓋內容

1. 建立工作簿並選取第一張工作表。  
2. 在儲存格中插入數值。  
3. 設定 `ExportTableOptions` 以 **套用自訂數字格式** 並回傳字串。  
4. 匯出儲存格並印出格式化結果。  
5. 邊緣案例處理——若儲存格內含公式或為 null 時該怎麼辦？

讓我們直接開始吧。

![套用自訂數字格式範例](https://example.com/image.png "apply custom number format")

## 步驟 1 – 建立工作簿並取得第一張工作表

首先需要一個工作簿物件。可以把它想像成你在 Office 應用程式中開啟的 Excel 檔案。取得工作簿後，抓取第一張工作表——大多數教學都從這裡開始，因為它能讓範例保持簡潔。

```csharp
// Step 1: Initialize the workbook and fetch the first worksheet
Workbook workbook = new Workbook();                 // creates an in‑memory workbook
Worksheet worksheet = workbook.Worksheets[0];      // first sheet (index 0)
```

**為什麼這很重要：** 全新的工作簿提供乾淨的起點，確保沒有隱藏的格式會干擾我們稍後套用的自訂數字格式。

## 步驟 2 – 將數值寫入 B2 儲存格（即將匯出的儲存格）

現在需要一些可供格式化的資料。**B2** 是個方便的位置——易於引用且遠離預設的 A1 角落，避免意外覆寫。

```csharp
// Step 2: Insert a raw numeric value
worksheet.Cells["B2"].Value = 1234.56;   // raw double, no formatting yet
```

**如果值是公式會怎樣？**  
若之後將原始值換成公式（例如 `=SUM(A1:A10)`），匯出程式仍會遵循我們在下一步設定的數字格式，因為格式是附加在儲存格上，而非值的類型。

## 步驟 3 – 設定匯出選項以取得格式化字串

這是教學的核心：告訴函式庫在匯出時 **套用自訂數字格式**。`NumberFormat` 字串遵循 Excel「自訂」類別的相同語法。

```csharp
// Step 3: Set up options for exporting as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,                         // forces string output
    NumberFormat = "#,##0.00;(#,##0.00)"           // custom format: 1,234.56 or (1,234.56) for negatives
};
```

- `ExportAsString = true` 確保方法回傳 `string` 而非原始的 double。  
- `NumberFormat = "#,##0.00;(#,##0.00)"` 與 Excel 的模式相同：千位使用逗號、保留兩位小數，負數以括號顯示。

> **為什麼要使用自訂格式？** 它能保證不同文化（例如美國與歐洲）的分隔符一致，並讓你加入會計用的括號等業務特定樣式。

## 步驟 4 – 使用設定好的選項匯出儲存格

現在真正從工作表取出值，讓函式庫負責套用我們先前定義的格式。

```csharp
// Step 4: Export the formatted value from B2
string formattedResult = worksheet.Cells.ExportTable(
    worksheet.Cells["B2"],   // the source cell
    exportOptions);         // our custom options
```

**邊緣案例 – 空儲存格：** 若 `B2` 為空，`formattedResult` 會是 `null`。你可以在印出前加上簡單的 null 檢查以避免例外。

## 步驟 5 – 顯示格式化字串

最後，我們把結果寫到主控台。實際應用中，你可能會把這個字串放入 PDF、電子郵件或 UI 標籤。

```csharp
// Step 5: Show the result
Console.WriteLine(formattedResult);   // Expected output: 1,234.56
```

**預期輸出**

```
1,234.56
```

如果將原始值改為 `-9876.54`，相同的格式會產生 `(9,876.54)`——正是許多會計報表所需的顯示方式。

## 完整、可執行的範例

以下是完整程式碼，你可以直接複製貼上到新的 Console 專案中。只要已加入相應的 NuGet 套件，即可編譯執行。

```csharp
using System;
using Aspose.Cells;   // Replace with your library’s namespace if different

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Insert numeric value into B2
        worksheet.Cells["B2"].Value = 1234.56;

        // 3️⃣ Set export options – apply custom number format
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00;(#,##0.00)"   // custom format
        };

        // 4️⃣ Export the cell as a formatted string
        string formattedResult = worksheet.Cells.ExportTable(
            worksheet.Cells["B2"], exportOptions);

        // 5️⃣ Output the result
        Console.WriteLine(formattedResult);   // → 1,234.56
    }
}
```

### 快速檢查

- **能編譯嗎？** 能——只要確保已參考 `Aspose.Cells`（或等價）DLL。  
- **能支援其他文化嗎？** 格式字串與文化無關；函式庫會依照你提供的模式處理。若需依語系調整分隔符，可在匯出前先加入 `CultureInfo` 處理。

## 常見問題與變化

### 如何使用不同的模式 **format number in spreadsheet**？

只要更換 `NumberFormat` 字串。例如，要顯示一位小數的百分比：

```csharp
NumberFormat = "0.0%";
```

### 如果我要 **how to export cell value** 為 HTML 而非純文字該怎麼做？

大多數函式庫都有接受匯出類型的重載。你可以設定 `ExportAsString = true` 並加入 `ExportHtml = true`（或類似屬性）。原理相同：先定義格式，再選擇輸出表現形式。

### 能否一次套用格式到整個範圍，而非單一儲存格？

當然可以。你可以將 `NumberFormat` 指派給 `Style` 物件，然後將該樣式套用到 `Range`。匯出呼叫保持不變，函式庫會自動取得樣式。

```csharp
Style style = workbook.CreateStyle();
style.Custom = "#,##0.00;(#,##0.00)";
Range range = worksheet.Cells.CreateRange("A1:C10");
range.ApplyStyle(style, new StyleFlag { NumberFormat = true });
```

### 當儲存格內含公式時會發生什麼？

匯出程式會先計算公式，然後再對計算結果套用數字格式。無需額外程式碼——只要在停用自動計算時先呼叫 `Calculate` 即可。

```csharp
worksheet.Cells["B2"].Formula = "=SUM(A1:A5)";
worksheet.Calculate();   // forces evaluation
```

## 結論

現在你已掌握 **套用自訂數字格式** 到試算表儲存格、在試算表情境中 **format number in spreadsheet**，以及 **how to export cell value** 為可直接顯示的字串。上述簡潔的程式碼範例涵蓋了從建立工作簿到最終輸出的每一步，讓你可以直接套用到正式專案中。

準備好迎接下一個挑戰了嗎？試著將此技巧與 **how to format numeric cell** 結合，處理日期、貨幣符號或條件格式。或探索在保留每個儲存格自訂格式的前提下，將多個儲存格匯出為 CSV。只要有這些基礎，你的可能性無限。

祝開發順利，別忘了多多實驗——有時最佳答案就藏在稍微調整格式字串的那一刻！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}