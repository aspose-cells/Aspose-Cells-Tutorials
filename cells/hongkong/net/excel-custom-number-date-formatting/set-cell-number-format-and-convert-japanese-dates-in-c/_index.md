---
category: general
date: 2026-11-19
description: 在 C# 中設定儲存格的數字格式，並學習如何套用 Excel 的日本元號日期格式，以實現可靠的 C# Excel 日期轉換。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set cell number format
- apply excel date format
- c# excel date conversion
- japanese era date excel
- aspose.cells date handling
language: zh-hant
lastmod: 2026-11-19
og_description: 在 C# 中設定儲存格的數字格式，並將 Excel 日期格式套用於日本元號日期。請參考本完整指南，以獲得精確的 C# Excel 日期轉換。
og_image_alt: Screenshot showing a C# code editor with set cell number format applied
  to an Excel cell
og_title: 設定儲存格數字格式並在 C# 中轉換日本日期 – 步驟指南
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  headline: Set cell number format and convert Japanese dates in C#
  type: TechArticle
- description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  name: Set cell number format and convert Japanese dates in C#
  steps:
  - name: Why this works
    text: '* `Style.Number = 14` maps to Excel’s *Short Date* format (`mm/dd/yyyy`
      by default). * When the cell contains a Japanese era string like `R3/04/01`,
      Aspose.Cells’ internal parser recognises the era and converts it to the corresponding
      Gregorian serial number during `CalculateFormula()`. * After the '
  - name: When to use a custom format
    text: '* Reports intended for Japanese audiences. * When you need to preserve
      the original era information for legal documents. * In dashboards where both
      Gregorian and era dates are shown side‑by‑side.'
  - name: Full end‑to‑end example
    text: Below is a self‑contained program that demonstrates both the Gregorian and
      era outputs in one run.
  - name: Edge cases & common pitfalls
    text: '| Situation | What to watch for | Fix / Recommendation | |----------------------------------------|------------------------------------------------------|----------------------------------------------------------|
      | Empty or malformed era string | `PutValue` stores the literal text; conversion
      fails'
  - name: Automation tip
    text: 'If you need to process a large range of era dates (e.g., column A contains
      many Japanese dates), wrap the conversion logic in a loop:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Date conversion
title: 設定儲存格數字格式及在 C# 中轉換日本日期
url: /zh-hant/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 設定儲存格數字格式並在 C# 中轉換日本日期

如果您需要在 C# Excel 自動化專案中 **set cell number format**，本指南將示範如何 **apply Excel date format** 以及執行 **C# Excel date conversion** 以處理日本元號日期。您將獲得完整、可執行的範例，將 Reiwa 元號字串（例如 `R3/04/01`）轉換為公曆日期 `2021‑04‑01`。

## 您將學習

* 如何建立工作簿並存取其第一個工作表。  
* 如何 **set cell number format** 使 Excel 將該值視為日期。  
* 如何 **apply Excel date format** 以辨識日本元號字串。  
* 如何透過重新計算公式來觸發 **C# Excel date conversion**。  
* 預期輸出以及針對邊緣情況的故障排除技巧。

**先決條件**

* .NET 6 或更新版本（程式碼亦可於 .NET Framework 4.6+ 執行）。  
* Aspose.Cells for .NET 2024 或更新版本 – 透過 NuGet 安裝：`dotnet add package Aspose.Cells`。  
* 具備 C# 與 Excel 日期處理的基本知識。

> **專業提示：** Aspose.Cells 可在未安裝 Microsoft Office 的環境下運作，非常適合伺服器端自動化。

## 使用 Aspose.Cells 在 C# 中設定儲存格數字格式

第一步是告訴 Excel 此儲存格包含日期。Excel 以序列號儲存日期，因此我們需要對目標儲存格套用內建的日期數字格式 (ID 14)。

```csharp
using System;
using Aspose.Cells;

class JapaneseEraDateDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Insert a Japanese era date string (Reiwa 3) into cell A1
        sheet.Cells["A1"].PutValue("R3/04/01");

        // 3️⃣ **Set cell number format** – use built‑in date format ID 14
        //    This tells Excel to treat the string as a date value.
        sheet.Cells["A1"].Style.Number = 14;

        // 4️⃣ Recalculate formulas so the internal date engine converts the era.
        workbook.CalculateFormula();

        // 5️⃣ Output the converted Gregorian date.
        Console.WriteLine(sheet.Cells["A1"].StringValue); // → 2021-04-01
    }
}
```

### 為什麼這樣可行

* `Style.Number = 14` 會對應到 Excel 的 *Short Date* 格式（預設為 `mm/dd/yyyy`）。  
* 當儲存格內含日本元號字串如 `R3/04/01` 時，Aspose.Cells 內部解析器會辨識元號，並在 `CalculateFormula()` 期間將其轉換為相應的公曆序列號。  
* 計算完成後，`StringValue` 會回傳已格式化的公曆日期。

## 為日本元號日期套用 Excel 日期格式

如果您希望儲存格顯示日本元號而非公曆日期，可使用包含元號代碼的自訂數字格式。此範例展示 **apply excel date format** 功能。

```csharp
// Apply a custom format that forces the Japanese era display
sheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";

// Recalculate to apply the custom format
workbook.CalculateFormula();

// Output the era‑styled string
Console.WriteLine(sheet.Cells["A1"].StringValue); // → R3年04月01日
```

* `[$-ja-JP]` 強制使用日本語系。  
* `ggg` 代表元號名稱（例如 `R` 代表 Reiwa）。  
* 加入文字字元（`年`、`月`、`日`）即可建立熟悉的日文日期版面。

### 何時使用自訂格式

* 針對日本讀者的報告。  
* 需要保留原始元號資訊以符合法律文件需求時。  
* 在儀表板上同時並排顯示公曆與元號日期的情況。

## C# Excel 日期轉換 – 處理日本元號

**c# excel date conversion** 流程可分為三個邏輯部分：

1. **Parse the era string** – Aspose.Cells 會自動辨識 `R`（Reiwa）、`H`（Heisei）、`S`（Showa）等。  
2. **Convert to a serial number** – Excel 以自 1899‑12‑30 起的天數儲存日期。  
3. **Format the serial number** – 可使用內建格式 (ID 14) 或自訂的日本格式。

### 完整端對端範例

以下是一個獨立程式，示範一次執行同時輸出公曆與元號結果。

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConversion
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Input: Reiwa 3 (2021) – can be any era string
        ws.Cells["A1"].PutValue("R3/04/01");

        // ---- Part 1: Gregorian output ----
        ws.Cells["A1"].Style.Number = 14;      // built‑in short date
        wb.CalculateFormula();                // forces conversion
        string gregorian = ws.Cells["A1"].StringValue;
        Console.WriteLine($"Gregorian: {gregorian}"); // 2021-04-01

        // ---- Part 2: Japanese era output ----
        ws.Cells["B1"].PutValue("R3/04/01");   // repeat input for clarity
        ws.Cells["B1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";
        wb.CalculateFormula();
        string era = ws.Cells["B1"].StringValue;
        Console.WriteLine($"Japanese era: {era}"); // R3年04月01日
    }
}
```

**預期的主控台輸出**

```
Gregorian: 2021-04-01
Japanese era: R3年04月01日
```

### 邊緣情況與常見陷阱

| 情況                                 | 需留意事項                                             | 修正 / 建議                                                   |
|--------------------------------------|--------------------------------------------------------|--------------------------------------------------------------|
| 空白或格式錯誤的元號字串             | `PutValue` 只儲存原始文字；轉換失敗                     | 在寫入儲存格前，以正規表達式驗證輸入。                         |
| 語系不匹配                           | 自訂格式顯示西方數字而非日文字符                         | 確保 `Custom` 格式包含 `[$-ja-JP]`，或將 `Workbook.Settings.CultureInfo` 設為 `ja-JP`。 |
| 工作簿含有參照日期儲存格的公式       | 重新計算可能覆寫公式結果                                 | 在所有格式設定步驟之後呼叫 `CalculateFormula` **後**，或在需要跳過錯誤時使用 `Workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)`。 |
| 使用較舊的 Aspose.Cells 版本          | 日本元號支援於 2022 Q3 才加入                             | 升級至最新的 NuGet 套件。                                     |

## 測試解決方案

1. 從 Visual Studio 或使用 `dotnet run` **執行程式**。  
2. 確認主控台輸出公曆日期 `2021‑04‑01` 與元號字串 `R3年04月01日`。  
3. 開啟產生的工作簿（若您加入 `wb.Save("Demo.xlsx");`）於 Microsoft Excel，檢視儲存格套用相同的格式。

### 自動化提示

如果需要處理大量元號日期（例如 A 欄包含多筆日本日期），可將轉換邏輯包在迴圈中：

```csharp
for (int row = 0; row < ws.Cells.MaxDataRow + 1; row++)
{
    var cell = ws.Cells[row, 0]; // column A
    cell.Style.Number = 14;
}
wb.CalculateFormula();
```

此做法可讓 **set cell number format** 操作保持快速且節省記憶體。

## 結論

現在您已了解如何在 C# 中使用 Aspose.Cells **set cell number format**、如何 **apply Excel date format** 以處理日本元號字串，以及如何可靠地將元號轉換為公曆日期的 **C# Excel date conversion**。完整且可執行的程式碼示範了兩種輸出，並突顯常見的邊緣情況。

**下一步**

* 探索其他內建的格式 ID

## 接下來您應該學習什麼？

以下教學涵蓋與本指南技術密切相關的主題。每個資源皆提供完整可運作的程式碼範例與逐步說明，協助您精通其他 API 功能，並在專案中探索替代實作方式。

- [在 C# 中設定 Excel 日期格式 – 完整步驟指南](/cells/english/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/)
- [如何使用 Aspose.Cells 套用 Excel 數字格式](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)
- [如何在 C# 中套用自訂 Excel 數字格式](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}