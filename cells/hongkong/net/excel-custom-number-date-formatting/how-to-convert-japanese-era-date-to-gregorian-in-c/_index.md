---
category: general
date: 2026-10-01
description: 使用 Aspose.Cells 在 C# 中將日本年號日期轉換為公曆 DateTime。快速學會如何轉換日本曆。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert japanese era date
- how to convert japanese calendar
language: zh-hant
lastmod: 2026-10-01
og_description: 在 C# 中將日本年號日期轉換為公曆 DateTime。本教學說明如何使用 Aspose.Cells 精確地將日本曆法轉換為公曆。
og_image_alt: Code example converting a Japanese era date string to a Gregorian DateTime
  in a C# console app
og_title: 在 C# 中將日本年號日期轉換為公曆 – 步驟指南
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  headline: How to convert Japanese era date to Gregorian in C#
  type: TechArticle
- description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  name: How to convert Japanese era date to Gregorian in C#
  steps:
  - name: Why each step matters
    text: '| Step | Purpose | How it helps the conversion | |------|---------|-----------------------------|
      | **Create workbook** | Provides a container that understands Excel formulas
      and date systems. | The library’s internal date engine is activated only inside
      a workbook. | | **Insert era string** | Suppl'
  - name: Handling invalid or ambiguous strings
    text: '* **Invalid era name** – Aspose.Cells throws a `FormatException`. Wrap
      the conversion in `try/catch` to provide a friendly error message. * **Missing
      year/month/day** – The library expects a full “Era Year/Month/Day” pattern.
      If you receive partial data, prepend missing parts or reject the input ear'
  - name: Next steps
    text: '* Explore **formatting options** to write the Gregorian date back into
      the worksheet with a custom number format. * Combine this conversion with **data
      import pipelines** (e.g., reading CSV files that contain era dates). * Review
      other Aspose.Cells features such as **date arithmetic** and **regional'
  type: HowTo
tags:
- Aspose.Cells
- C#
- date conversion
title: 如何在 C# 中將日本年號日期轉換為公曆
url: /zh-hant/net/excel-custom-number-date-formatting/how-to-convert-japanese-era-date-to-gregorian-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中將日本年號日期轉換為公曆

如果您需要在 C# 中將 **convert Japanese era date** 字串轉換為公曆日期，本指南將完整說明做法。無論是處理舊有資料、讀取使用者輸入，或是產生報表，Aspose.Cells 函式庫都能讓轉換變得簡單。此外，您還會了解在試算表中 **how to convert Japanese calendar** 值的最佳方法。

本教學涵蓋每一步——從建立工作簿到取得 `DateTime` 值——讓您可以直接複製貼上完整、可執行的程式。無需外部文件說明，只要依照以下程式碼與說明操作即可。

## 前置條件

* .NET 6.0 或更新版本（程式碼亦相容 .NET Framework 4.6+）
* **Aspose.Cells** 授權（免費試用版可用於測試）
* 開發環境，例如 Visual Studio 2022 或 VS Code
* 具備 C# 主控台應用程式的基本知識

## 使用 Aspose.Cells 轉換日本年號日期

轉換的核心只需幾個簡單的 API 呼叫。Aspose.Cells 會自動解析日本年號字串（例如 “Reiwa 2/04/01”），並在工作表重新計算後以 `DateTime` 物件形式提供結果。

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                // creates an empty Excel file in memory
        var worksheet = workbook.Worksheets[0];       // the default sheet is at index 0

        // Step 2: Insert a Japanese era date string into cell A1
        // The string follows the Japanese calendar format: Era Year/Month/Day
        worksheet.Cells[0, 0].PutValue("Reiwa 2/04/01");

        // Step 3: Apply a default style to the cell (required for proper calculation)
        // Without a style, Aspose.Cells may treat the content as plain text and skip conversion.
        worksheet.Cells[0, 0].SetStyle(workbook.CreateStyle());

        // Step 4: Recalculate the worksheet so the date string is converted to a Gregorian date
        // The Calculate method parses the era string and updates the cell's internal value.
        worksheet.Calculate();

        // Step 5: Retrieve and display the converted DateTime value (2020‑04‑01)
        DateTime gregorian = worksheet.Cells[0, 0].DateTimeValue;
        Console.WriteLine($"Gregorian date: {gregorian:yyyy-MM-dd}");
    }
}
```

### 為何每一步都很重要

| 步驟 | 目的 | 如何協助轉換 |
|------|---------|-----------------------------|
| **建立工作簿** | 提供能理解 Excel 公式與日期系統的容器。 | 只有在工作簿內，函式庫的內部日期引擎才會被啟動。 |
| **插入年號字串** | 提供您想要轉換的原始日本曆文字。 | Aspose.Cells 能辨識 *Reiwa*、*Heisei*、*Showa* 等年號名稱。 |
| **設定樣式** | 強制儲存格被視為值儲存格，而非純文字。 | 若未設定樣式，`Calculate` 方法可能會忽略該儲存格，導致文字保持不變。 |
| **計算** | 觸發年號字串的解析並轉換為內部序列日期號。 | 函式庫將 “Reiwa 2/04/01” → 序列號 → 公曆 `DateTime`。 |
| **讀取 `DateTimeValue`** | 回傳已轉換的 .NET `DateTime` 物件。 | 您現在擁有可在任何 .NET API 中使用的標準 `DateTime`。 |

## 在其他情境下轉換日本曆

相同的方法適用於 Aspose.Cells 支援的所有日本年號名稱：

```csharp
// Example: converting a Heisei era date
worksheet.Cells[0, 0].PutValue("Heisei 30/12/31"); // corresponds to 2018‑12‑31
worksheet.Calculate();
Console.WriteLine(worksheet.Cells[0, 0].DateTimeValue); // 2018-12-31
```

### 處理無效或模糊的字串

* **Invalid era name** – Aspose.Cells 會拋出 `FormatException`。請將轉換包在 `try/catch` 中，以提供友善的錯誤訊息。
* **Missing year/month/day** – 函式庫需要完整的 “Era Year/Month/Day” 格式。若收到不完整資料，請在前面補上缺少的部分或提前拒絕該輸入。
* **Different locale settings** – 轉換 **不會** 依賴目前執行緒的文化設定；它始終使用內建於 Aspose.Cells 的日本年號對照表。此特性使方法在伺服器端處理時更安全。

```csharp
try
{
    worksheet.Cells[0, 0].PutValue(userInput);
    worksheet.Calculate();
    DateTime result = worksheet.Cells[0, 0].DateTimeValue;
    // Use result...
}
catch (FormatException ex)
{
    Console.WriteLine($"Unable to parse Japanese era date: {ex.Message}");
}
```

## 實用技巧與常見陷阱

* **Always call `SetStyle`** before `Calculate`. 跳過此步驟是常見錯誤來源，因為儲存格會仍被視為純文字。
* **Reuse the same workbook** if you need to convert many dates. 為多筆日期轉換重複使用同一工作簿。每次建立新工作簿會增加不必要的開銷。
* **Batch conversion** – 在一欄填入年號字串，呼叫一次 `worksheet.Calculate()`，再讀取整欄的 `DateTimeValue`。這比逐儲存格重新計算更有效率。
* **Version compatibility** – 年號轉換邏輯於 Aspose.Cells 22.9 引入。請確保使用該版本或更新版本；較舊的版本會將字串視為純文字。

## 完整可執行範例（主控台應用程式）

以下是一個獨立的程式，您可以直接編譯執行。它示範了 Reiwa 與 Heisei 兩種年號的轉換，並能優雅地處理錯誤。

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConverter
{
    static void Main()
    {
        // Initialize workbook once
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        var style = workbook.CreateStyle();
        sheet.Cells[0, 0].SetStyle(style);
        sheet.Cells[1, 0].SetStyle(style);

        // Sample inputs
        string[] eraDates = { "Reiwa 2/04/01", "Heisei 30/12/31", "InvalidEra 1/01/01" };

        for (int i = 0; i < eraDates.Length; i++)
        {
            sheet.Cells[i, 0].PutValue(eraDates[i]);
        }

        // Perform conversion for all populated cells
        sheet.Calculate();

        // Output results
        for (int i = 0; i < eraDates.Length; i++)
        {
            try
            {
                DateTime dt = sheet.Cells[i, 0].DateTimeValue;
                Console.WriteLine($"{eraDates[i]} → {dt:yyyy-MM-dd}");
            }
            catch (Exception)
            {
                Console.WriteLine($"{eraDates[i]} → conversion failed");
            }
        }
    }
}
```

**預期的主控台輸出**

```
Reiwa 2/04/01 → 2020-04-01
Heisei 30/12/31 → 2018-12-31
InvalidEra 1/01/01 → conversion failed
```

執行此程式可證實函式庫正確 **convert japanese era date** 字串，並能優雅地回報不支援的值。

## 結論

您現在已了解如何使用 Aspose.Cells 在 C# 中將 **convert Japanese era date** 字串轉換為標準的公曆 `DateTime` 物件。此流程只需插入年號文字、套用樣式、重新計算工作表，然後讀取 `DateTimeValue`。依循上述步驟，您亦能解決 **how to convert Japanese calendar** 大量資料的轉換、錯誤處理與效能最佳化等更廣泛的問題。

### 往後步驟

* 探索 **formatting options**，將公曆日期寫回工作表，並使用自訂數字格式。
* 將此轉換與 **data import pipelines** 結合（例如讀取包含年號日期的 CSV 檔）。
* 檢視其他 Aspose.Cells 功能，如 **date arithmetic** 與 **regional settings**，以處理更複雜的曆法情境。

祝開發順利，歡迎自行調整範例以符合您的資料處理工作流程！

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索其他實作方式。

- [Parse Japanese Era Date in C# with Aspose.Cells – Full Guide](/cells/english/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/)
- [Enable Japanese Era Parsing in C# with Aspose.Cells](/cells/english/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/)
- [How to create workbook and convert string to date in C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}