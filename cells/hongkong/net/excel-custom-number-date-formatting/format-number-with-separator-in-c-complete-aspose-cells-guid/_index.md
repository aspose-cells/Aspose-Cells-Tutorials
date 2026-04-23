---
category: general
date: 2026-03-30
description: 學習如何在 C# 中使用 Aspose.Cells 進行帶分隔符的數字格式設定。內容包括設定自訂數字格式、加入千位分隔符、格式化小數位，以及儲存格的格式設定。
draft: false
keywords:
- format number with separator
- set custom number format
- add thousands separator
- format decimal places
- how to format cell
language: zh-hant
og_description: 在 C# 中使用分隔符格式化數字。本指南說明如何設定自訂數字格式、加入千位分隔符、格式化小數位，以及如何使用 Aspose.Cells
  進行儲存格格式化。
og_title: 在 C# 中使用分隔符格式化數字 – Aspose.Cells 教學
tags:
- C#
- Aspose.Cells
- Number Formatting
title: 在 C# 中使用分隔符格式化數字 – 完整 Aspose.Cells 指南
url: /zh-hant/net/excel-custom-number-date-formatting/format-number-with-separator-in-c-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中使用分隔符格式化數字 – 完整 Aspose.Cells 指南

是否曾經需要在試算表中 **format number with separator**，卻不確定該使用哪個 API 呼叫？你並非唯一遇到此問題的人——開發人員在匯出資料時，常常要與千位分隔符、小數位數和自訂格式模式奮戰。  

好消息：Aspose.Cells 讓這件事變得輕而易舉。在本教學中，我們將逐步示範一個實務範例，涵蓋 **sets a custom number format**、**adds a thousands separator**、**formats decimal places**，以及展示 **how to format cell** 輸出為字串。完成後，你將擁有一段可直接放入任何 .NET 專案的即用程式碼。

## 本指南涵蓋內容

* 你需要的確切 NuGet 套件以及如何安裝它。  
* 一步一步的程式碼，建立工作簿、寫入數值，並套用自訂格式。  
* 說明為何 `ExportTableOptions.ExportAsString` 是取得格式化值的首選方式。  
* 常見陷阱——例如忘記啟用 `ExportAsString` 或使用錯誤的格式遮罩。  
* 如何調整格式遮罩，以符合不同的小數位數或不同的分隔符樣式。

不需要外部文件連結；所有資訊皆在此。讓我們開始吧。

---

## 前置條件

| 需求 | 原因 |
|-------------|--------|
| .NET 6.0 或更新版本 | Aspose.Cells 23.10+ 目標為 .NET Standard 2.0+，因此 .NET 6 安全且為最新版本。 |
| Visual Studio 2022（或任何 C# IDE） | 讓除錯與套件管理變得輕鬆。 |
| Aspose.Cells for .NET NuGet 套件 | 提供我們將使用的 `Workbook`、`Worksheet` 與 `ExportTableOptions` 類別。 |

你可以透過套件管理員主控台安裝此套件：

```powershell
Install-Package Aspose.Cells
```

就這樣——不需要額外的 DLL、也不需要 COM interop，只要一個 NuGet 參考即可。

## 步驟 1：初始化新工作簿（How to Format Cell）

我們首先建立一個全新的 `Workbook` 實例。可以把它想像成一個尚未寫入資料的空白 Excel 檔案。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is where we’ll format the cell.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
```

> **為何重要：** `Workbook` 是 Aspose.Cells 所有操作的入口。透過取得第一個工作表 (`Worksheets[0]`) 我們即可得到一個乾淨的畫布，而不必先命名工作表。

## 步驟 2：將數值寫入目標儲存格

接著，我們將原始數字寫入儲存格 **A1**。此數值尚未套用格式——僅為 double 型別。

```csharp
        // Step 2: Insert a raw numeric value.
        worksheet.Cells["A1"].PutValue(12345.6789);
```

> **專業提示：** 若之後要套用數值格式，請使用 `PutValue` 而非 `PutString`。這樣可保留底層資料型別，讓 Excel 兼容的計算得以執行。

## 步驟 3：設定自訂數字格式（加入千位分隔符與設定小數位數）

現在進入本教學的核心：定義一個格式遮罩，告訴 Aspose.Cells 如何顯示數字。遮罩 `#,##0.00` 具備三個功能：

1. **`#,##0`** – 加入千位分隔符（預設為逗號）。  
2. **`.00`** – 強制顯示兩位小數。  

如果需要不同的小數位數，只要更改小數點後的 `0` 數量即可。

```csharp
        // Step 3: Configure the custom number format.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // Return the value as a formatted string.
            NumberFormat = "#,##0.00"       // Add thousands separator and fix to 2 decimals.
        };
```

> **為何使用 `ExportAsString`**：預設情況下，`ExportString` 會回傳原始值。將 `ExportAsString = true` 設為 true，會在轉換為文字前套用 `NumberFormat` 遮罩。當你需要精確的字串表示（例如報表、JSON 輸出或 UI 顯示）時，這是必須的。

## 步驟 4：匯出格式化文字（How to Format Cell）

設定好選項後，我們在同一個儲存格上呼叫 `ExportString`。此方法會遵循剛才定義的遮罩，回傳格式化好的字串。

```csharp
        // Step 4: Export the formatted value.
        string formattedCellText = worksheet.Cells["A1"].ExportString(exportOptions);

        // Step 5: Show the result.
        Console.WriteLine(formattedCellText); // Expected output: 12,345.68
    }
}
```

執行程式後，會在主控台印出 **`12,345.68`**——正是我們要求的格式。

> **邊緣情況：** 若來源數字超過兩位小數，遮罩會進行四捨五入。若需要截斷而非四捨五入，必須在呼叫 `PutValue` 前先以 `Math.Truncate` 處理數值。

## 步驟 5：微調格式 – 常見變化

### 5.1 更改小數精度

想要三位小數嗎？只要更換遮罩即可：

```csharp
NumberFormat = "#,##0.000"   // → 12,345.679
```

### 5.2 使用不同的千位分隔符

某些語系偏好使用空格或句點作為分隔符。你可以直接將字元寫入遮罩：

```csharp
NumberFormat = "# ##0.00"    // Uses a non‑breaking space as separator.
```

或是依賴工作簿的文化設定：

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("de-DE");
NumberFormat = "#.##0,00";   // German style: 12.345,68
```

### 5.3 前綴或後綴（貨幣、百分比）

直接在遮罩中加入美元符號或百分比符號：

```csharp
NumberFormat = "$#,##0.00";   // → $12,345.68
NumberFormat = "0.00%";       // → 1,234,568.00%
```

> **注意：** 遮罩區分大小寫。`$` 與 `%` 為字面符號；不會影響底層數值。

## 步驟 6：完整可執行範例（即貼即用）

以下是完整程式碼，你可以直接複製到新的主控台應用程式中。它包含所有步驟、註解以及最終輸出驗證。

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise workbook and worksheet.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write raw numeric value to A1.
        worksheet.Cells["A1"].PutValue(12345.6789);

        // 3️⃣ Define custom format: thousands separator + two decimals.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00"
        };

        // 4️⃣ Export the formatted string.
        string result = worksheet.Cells["A1"].ExportString(exportOptions);

        // 5️⃣ Display the outcome.
        Console.WriteLine(result); // Output: 12,345.68

        // Optional: keep console open.
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

執行程式（在終端機輸入 `dotnet run` 或在 Visual Studio 按 F5），即可看到如圖所示的格式化數字。

## 常見問題 (FAQ)

**Q: 這在較舊版本的 Excel 上也能運作嗎？**  
A: 可以。格式遮罩遵循 Excel 原生的數字格式語法，只要支援 `#,##0.00` 的版本都會呈現相同的字串。

**Q: 如果需要一次格式化多個儲存格該怎麼辦？**  
A: 迭代目標範圍，對每個儲存格套用相同的 `ExportTableOptions`，或是在整個範圍設定 `Style.Custom` 屬性，然後在單一儲存格上呼叫 `ExportString`。

**Q: 能否直接匯出為 CSV 並保留這些格式？**  
A: 完全可以。在每個儲存格設定格式後，使用 `Workbook.Save("output.csv", SaveFormat.CSV);`。Aspose.Cells 會在產生 CSV 時遵循儲存格的 `Style`。

## 結論

我們剛剛示範了如何在 C# 中使用 Aspose.Cells **format number with separator**，涵蓋了從 **set custom number format**、**add thousands separator**、**format decimal places** 到關鍵的 **how to format cell** 以匯出字串的全部步驟。程式碼完整且獨立，適用於 .NET 6+，且可依任何語系或精度需求調整。

接下來，你可以探索：

* 將相同技巧套用於日期與時間（`NumberFormat = "dd‑MMM‑yyyy"`）。  
* 自動化大量匯出，讓每一欄位使用不同的遮罩。  
* 將格式化字串整合至使用 Aspose.Words 的 PDF 報告中。

試試看這些範例，你將很快成為團隊中負責試算表格式化的首選人物。祝開發愉快！   (Image: ![Screenshot showing formatted number with separator in Aspose.Cells](image-placeholder.png){alt="Formatted number with separator displayed in Aspose.Cells output"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}