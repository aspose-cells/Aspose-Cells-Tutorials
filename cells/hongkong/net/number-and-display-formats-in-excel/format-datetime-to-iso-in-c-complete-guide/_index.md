---
category: general
date: 2026-03-22
description: 學習如何在從 Excel 提取日期時將日期時間格式化為 ISO，並使用 Aspose.Cells 在 C# 中顯示 ISO 日期。
draft: false
keywords:
- format datetime to iso
- extract date from excel
- display iso date
- Aspose.Cells date parsing
- Japanese era dates
language: zh-hant
og_description: 將日期時間格式化為 ISO 輕鬆搞定。此指南示範如何從 Excel 提取日期，並使用 Aspose.Cells 顯示 ISO 日期。
og_title: 在 C# 中將日期時間格式化為 ISO – 逐步教學
tags:
- C#
- Aspose.Cells
- DateTime
- Excel
- ISO 8601
title: 在 C# 中將日期時間格式化為 ISO – 完全指南
url: /zh-hant/net/number-and-display-formats-in-excel/format-datetime-to-iso-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中將 datetime 轉換為 ISO – 完整指南

是否曾經需要 **format datetime to iso**，但來源卻在 Excel 活頁簿內？或許儲存格內包含日文元號，例如「令和3年5月1日」，讓你摸不著頭腦，不知道該如何轉成 `2021‑05‑01` 這樣的乾淨字串。你並不孤單。在本教學中，我們將 **extract date from excel**、解析日文元號，然後在主控台上 **display iso date**——全部只需幾行 C# 程式碼與 Aspose.Cells。

我們會一步步說明你需要的所有內容：必備的 NuGet 套件、可以直接複製貼上的完整程式碼、每一行程式碼的意義，以及一些常見的邊緣案例技巧。完成後，你將擁有一段可重複使用的程式碼，無論原始 Excel 值多麼古怪，都能正確 **format datetime to iso**。

## 你需要的環境

- .NET 6.0 或更新版本（程式碼亦可在 .NET Framework 4.6+ 上編譯）
- Visual Studio 2022（或你慣用的任何編輯器）
- **Aspose.Cells for .NET** NuGet 套件 – `Install-Package Aspose.Cells`
- 一個包含日文元號格式日期的 Excel 檔（或一個全新的活頁簿）

就這些。沒有額外的函式庫、沒有 COM interop，只有一個寫得很清楚的方法。

## 步驟 1：建立活頁簿並寫入日文元號日期  

首先，我們需要一個活頁簿。如果你已經有 Excel 檔，可使用 `new Workbook("path")` 讀取。以下範例會在記憶體中建立新活頁簿，並將日文元號字串寫入 **A1** 儲存格。

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date (Reiwa 3 = 2021) into A1
        sheet.Cells["A1"].PutValue("令和3年5月1日");
```

> **為什麼要這麼做：** Aspose.Cells 預設將儲存格值視為字串。透過插入原始的元號文字，我們模擬了日本客戶以本地曆法輸入日期的真實情境。

## 步驟 2：啟用日文元號解析並擷取日期  

Aspose.Cells 能自動將日文元號字串轉換為 .NET `DateTime` 物件，只要告訴它使用 `DateTimeParseOptions.EnableJapaneseEra` 旗標即可。

```csharp
        // 3️⃣ Retrieve the cell value while enabling Japanese era parsing
        CellValue parsed = sheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

> **小技巧：** 若忘記加入 `EnableJapaneseEra` 選項，函式庫會回傳原始字串，導致後續轉換失敗。處理混合內容時，務必檢查 `parsed.Type`。

## 步驟 3：將解析後的 DateTime 轉為 ISO 8601  

取得正確的 `DateTime` 後，將它轉成 ISO 格式的字串非常簡單。`"yyyy-MM-dd"` 格式符合 ISO 8601 日期部份，這也是大多數 API 所期待的格式。

```csharp
        // 4️⃣ Convert to ISO 8601 (yyyy‑MM‑dd) and display it
        string isoDate = parsed.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

執行程式後會印出：

```
ISO date: 2021-05-01
```

這就是你想要的 **display iso date**。

## 完整、可執行的範例  

以下是可以直接貼到 Console 專案的完整程式碼。沒有隱藏的相依性，也不需要額外設定。

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a Japanese era date into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // Retrieve the cell value with Japanese era parsing enabled
        CellValue parsedValue = worksheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);

        // Convert the DateTime to ISO 8601 format and output it
        string isoDate = parsedValue.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

> **預期輸出：** `ISO date: 2021-05-01`

## 步驟說明（每一步的意義）

| 步驟 | 會發生什麼事 | 為什麼重要 |
|------|--------------|------------|
| **Create workbook** | 初始化一個記憶體中的 Excel 容器。 | 提供一個沙箱，讓你在不觸及檔案系統的情況下測試。 |
| **PutValue** | 將原始的日文元號字串存入 **A1**。 | 模擬真實資料輸入，確保解析器看到完整文字。 |
| **GetValue with `EnableJapaneseEra`** | 將元號字串轉換為 .NET `DateTime`。 | 自動完成曆法轉換，免除手動查表。 |
| **`ToString("yyyy-MM-dd")`** | 把 `DateTime` 格式化為 ISO 8601。 | 保證產生文化不依賴、可排序的日期字串，適用於 REST API、資料庫等。 |
| **Console.WriteLine** | 顯示最終的 ISO 日期。 | 確認整個流程端對端運作正常。 |

## 常見變化處理  

### 1. 不同的儲存格位置  

如果日期位於 **B2** 或命名範圍，只需將 `"A1"` 換成相對的位址：

```csharp
worksheet.Cells["B2"].PutValue("令和2年12月31日");
var value = worksheet.Cells["B2"]
    .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

### 2. 同欄位多筆日期  

若需要為多列 **extract date from excel**，可遍歷使用範圍：

```csharp
int lastRow = worksheet.Cells.MaxDataRow;
for (int i = 0; i <= lastRow; i++)
{
    var cell = worksheet.Cells[i, 0]; // column A
    var cv = cell.GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
    string iso = cv.DateTimeValue.ToString("yyyy-MM-dd");
    Console.WriteLine($"Row {i + 1}: {iso}");
}
```

### 3. 非元號日期的備援  

若儲存格已是標準日期字串，解析器仍能運作，但你可能想加一層保護：

```csharp
CellValue cv = cell.GetValue(CellValueType.DateTime,
    DateTimeParseOptions.EnableJapaneseEra | DateTimeParseOptions.TryParse);
```

`TryParse` 旗標可防止例外，並在轉換失敗時回傳原始值。

### 4. 含時間的情況  

若同時需要時間部分，可使用 `"yyyy-MM-ddTHH:mm:ss"`：

```csharp
string isoDateTime = parsedValue.DateTimeValue.ToString("yyyy-MM-ddTHH:mm:ss");
```

即可得到完整的 ISO 8601 時間戳記（`2021-05-01T00:00:00`）。

## 視覺說明  

![format datetime to iso example](image.png "An example of formatting datetime to iso in C#")

*Alt text:* *format datetime to iso example showing console output*

## 常見問答  

- **可以用於 .xls 檔案嗎？**  
  可以。Aspose.Cells 內建支援 `.xls`、`.xlsx`、`.csv` 等多種格式。

- **如果活頁簿有密碼保護該怎麼辦？**  
  使用 `new Workbook("file.xlsx", new LoadOptions { Password = "secret" })` 載入。

- **ISO 格式會依本地語系而變嗎？**  
  不會。`"yyyy-MM-dd"` 格式是文化不依賴的，保證在任何機器上產生相同字串。

- **這能在 .NET Core 上執行嗎？**  
  完全可以——Aspose.Cells 符合 .NET Standard 2.0。

## 結語  

我們已說明如何透過 **format datetime to iso**，先 **extract date from excel**、解析日文元號，最後在主控台 **display iso date**。核心步驟——建立活頁簿、寫入或載入元號文字、啟用日文元號解析、以 `ToString("yyyy-MM-dd")` 格式化——已足以應付大多數情境。

接下來，你可以：

- 將 ISO 日期寫回另一欄位，以供後續處理。
- 匯出轉換後的活頁簿為 CSV，進行批次匯入。
- 結合接受 Excel 上傳並回傳 JSON‑encoded ISO 日期的 Web API。

歡迎嘗試不同的日期格式、時區，甚至自訂曆法。Aspose.Cells 的彈性讓你很少會碰到瓶頸。

祝程式開發順利，願所有日期皆符合 ISO 標準！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}