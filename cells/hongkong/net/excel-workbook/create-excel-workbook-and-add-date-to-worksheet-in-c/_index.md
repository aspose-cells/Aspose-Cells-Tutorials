---
category: general
date: 2026-10-13
description: 在 C# 中建立 Excel 活頁簿，並使用 Aspose.Cells 將日期寫入 Excel。學習如何將檔案儲存為 xlsx，並在工作表中加入日期，提供完整程式碼。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save excel file
- write date to excel
- save workbook as xlsx
- add date to worksheet
language: zh-hant
lastmod: 2026-10-13
og_description: 在 C# 中建立 Excel 活頁簿並寫入日期。請參考此完整指南，使用 Aspose.Cells 將 Excel 檔案儲存為 xlsx，並將日期加入工作表。
og_image_alt: Excel workbook screenshot showing a Japanese imperial date in cell A1
og_title: 建立 Excel 活頁簿並在工作表中加入日期 – C# 步驟說明
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Create excel workbook in C# and write date to excel using Aspose.Cells.
    Learn to save excel file as xlsx and add date to worksheet with full code.
  headline: Create excel workbook and add date to worksheet in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: 在 C# 中建立 Excel 工作簿並在工作表中加入日期
url: /zh-hant/net/excel-workbook/create-excel-workbook-and-add-date-to-worksheet-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 Excel 活頁簿並在工作表中加入日期（C#）

如果您需要 **以程式方式建立 Excel 活頁簿**，本教學將示範如何 **將日期寫入 Excel** 以及 **將 Excel 檔案儲存** 為 *.xlsx* 活頁簿。您將看到一個完整、可執行的範例，該範例會解析日文皇紀字串，並將產生的 `DateTime` 儲存於儲存格 A1。

在 C# 中操作 Excel 通常需要三個步驟：建立活頁簿、將資料寫入工作表，最後將檔案寫入磁碟。本教學會逐一說明每個步驟、解釋為何如此撰寫程式碼，並指出常見的陷阱（例如文化特定的解析與檔案系統權限）。完成後，您即可 **在工作表加入日期**、**將活頁簿儲存為 xlsx**，並可將此模式套用到任何資料類型。

> **先備條件** – 本範例使用 **Aspose.Cells for .NET** 函式庫（版本 23.10 或更新）。請透過 NuGet 安裝：

```bash
dotnet add package Aspose.Cells
```

您同時需要 .NET 6+ SDK 以及一個可寫入的目錄來放置輸出檔案。

---

## 建立 Excel 活頁簿並設定工作表

第一步是建立一個空的活頁簿，並取得其預設工作表。Aspose.Cells 會自動建立一個名為「Sheet1」的工作表。

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

// Step 1: Create a new workbook
Workbook workbook = new Workbook();

// Step 2: Get the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];
```

**為何重要** – `Workbook` 是所有 Excel 操作的入口點。以不帶參數的方式建立它，可取得一個乾淨的活頁簿，之後您可以 **儲存 Excel 檔案** 為任意格式。

---

## 解析日文皇紀日期

日文皇紀日期使用皇紀符號（例如「R」代表 Reiwa）加上兩位數年份。當您提供自訂的 `DateTimeParseOptions` 物件，告訴解析器使用日本天皇曆時，.NET 的 `DateTime.ParseExact` 方法即可處理此格式。

```csharp
// Step 3: Define a date string in the Japanese imperial era
string imperialDate = "R3/04/01"; // Reiwa 3, April 1st

// Step 4: Configure parsing options for the Japanese Emperor calendar
var parseOptions = new DateTimeParseOptions
{
    Calendar = DateTimeParseOptions.CalendarType.JapaneseEmperor
};

// Step 5: Parse the string into a .NET DateTime
DateTime parsedDate = DateTime.ParseExact(
    imperialDate,
    "ggyy/MM/dd",
    CultureInfo.InvariantCulture,
    DateTimeStyles.None,
    parseOptions);
```

**說明** –  
* `gg` 讀取皇紀符號（`R` 代表 Reiwa）。  
* `yy` 讀取該皇紀內的兩位數年份。  
* `MM/dd` 讀取月份與日期。  

若省略 `parseOptions`，解析器會預設使用公曆，進而拋出 `FormatException`。這是處理非公曆時常見的邊緣案例。

---

## 將日期寫入工作表

取得 `DateTime` 值後，您即可將它寫入儲存格。Aspose.Cells 會根據值的類型自動設定儲存格格式。

```csharp
// Step 6: Write the parsed date into cell A1
sheet.Cells["A1"].PutValue(parsedDate);

// Optional: Apply a date format for better readability
Style style = workbook.CreateStyle();
style.Custom = "yyyy-mm-dd";
sheet.Cells["A1"].SetStyle(style);
```

**為何要設定樣式？** – 若不設定樣式，Excel 可能會使用系統預設的日期格式顯示，對其他地區的使用者而言可能會造成混淆。明確指定 `"yyyy-mm-dd"` 可確保顯示一致。

---

## 將 Excel 檔案儲存為 xlsx

最後，將活頁簿寫入磁碟。`Save` 方法會根據檔案副檔名決定輸出格式，使用「.xlsx」即會自動採用 Office Open XML 格式。

```csharp
// Step 7: Define the output path (adjust to your environment)
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "JapaneseDate.xlsx");

// Step 8: Save the workbook
workbook.Save(outputPath, SaveFormat.Xlsx);
```

**小技巧** – 若目標目錄不存在或您沒有寫入權限，`Save` 會拋出 `IOException`。請務必在呼叫 `Save` 前先確認路徑是否正確。

---

## 完整可執行範例

以下是完整程式碼，您可以直接複製、貼上並執行。範例包含所有 `using` 指令、錯誤處理，以及說明每個操作的註解。

```csharp
using Aspose.Cells;
using System;
using System.Globalization;
using System.IO;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Define the Japanese imperial date string
            string imperialDate = "R3/04/01"; // Reiwa 3, April 1st

            // 3️⃣ Set up parsing options for the Japanese Emperor calendar
            var parseOptions = new DateTimeParseOptions
            {
                Calendar = DateTimeParseOptions.CalendarType.JapaneseEmperor
            };

            // 4️⃣ Parse the string into a .NET DateTime
            DateTime parsedDate = DateTime.ParseExact(
                imperialDate,
                "ggyy/MM/dd",
                CultureInfo.InvariantCulture,
                DateTimeStyles.None,
                parseOptions);

            // 5️⃣ Write the date to cell A1
            sheet.Cells["A1"].PutValue(parsedDate);

            // Apply a consistent date format
            Style dateStyle = workbook.CreateStyle();
            dateStyle.Custom = "yyyy-mm-dd";
            sheet.Cells["A1"].SetStyle(dateStyle);

            // 6️⃣ Determine the output file location
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "JapaneseDate.xlsx");

            // 7️⃣ Save the workbook as an .xlsx file
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Workbook saved successfully to: {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

**預期結果**

開啟 `JapaneseDate.xlsx` 後，儲存格 A1 會顯示日期 **2021‑04‑01**（Reiwa 3 / 04 / 01 的公曆等價），且格式為 `yyyy‑mm‑dd`。

![Excel workbook with date in cell A1](excel-date-screenshot.png){alt="顯示日文皇紀日期於儲存格 A1 的 Excel 活頁簿截圖"}

---

## 常見問題與邊緣案例

| Question | Answer |
|----------|--------|
| *如果皇紀變更（例如從平成到令和）會怎樣？* | `JapaneseEmperor` 曆法會自動將皇紀符號（`H`、`R` 等）對應到正確的公曆範圍，您只需更新輸入字串即可。 |
| *可以在同一欄位寫入多筆日期嗎？* | 可以。於迴圈中呼叫 `sheet.Cells[row, column].PutValue(dateValue)` 即可寫入每一列。 |
| *如果需要不同的日期格式該怎麼辦？* | 將 `dateStyle.Custom` 改成任意 Excel 日期格式字串，例如 `"dd-mmm-yyyy"` 或 `"mm/dd/yyyy"`。 |
| *寫入日期後能否保護工作表？* | 在儲存之前使用 `sheet.Protect(ProtectOptions.All, "password")` 即可。 |
| *要如何處理時區問題？* | `DateTime` 會保存 UTC 或本地時間。可在呼叫 `PutValue` 前使用 `DateTime.SpecifyKind` 或 `TimeZoneInfo.ConvertTime` 進行轉換。 |

---

## 結論

您現在已掌握如何使用 Aspose.Cells 在 C# 中 **建立 Excel 活頁簿**、**將日期寫入 Excel**、**在工作表加入日期**，以及 **將活頁簿儲存為 xlsx**。完整範例示範了日文皇紀字串的解析、統一樣式的套用，以及檔案系統相關的注意事項。

接下來您可以


## 接下來該學什麼？

以下教學與本篇內容緊密相關，能進一步擴展您所學的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您熟悉其他 API 功能，並在專案中探索替代實作方式。

- [Create Excel Workbook C# – Add Comment & Save as XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)
- [Create New Workbook in C# – Add Formula and Save Excel File](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Create Excel Workbook – Wrap Columns and Save as XLSX](/cells/english/net/formatting-rows-and-columns-in-excel/create-excel-workbook-wrap-columns-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}