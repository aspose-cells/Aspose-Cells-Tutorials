---
category: general
date: 2026-10-26
description: 學習如何在 C# 中使用日本曆法的 CultureInfo 解析元號日期，並使用 NPOI 將其插入 Excel 工作表。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use japanese calendar cultureinfo
- japanese era date parsing
- cultureinfo with japanese calendar
- datetime parse with cultureinfo
- npoi excel cultureinfo
language: zh-hant
lastmod: 2026-10-26
og_description: 在 C# 中使用日本曆法 CultureInfo 解析令和年代的日期，並寫入 Excel 工作表。完整、可執行的程式碼與說明。
og_image_alt: Screenshot of C# code parsing a Japanese era date and inserting it into
  an Excel cell
og_title: 在 C# 中使用日本曆法 CultureInfo – 完整 Excel 範例
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use Japanese calendar CultureInfo in C# when parsing era
    dates and inserting them into an Excel worksheet with NPOI.
  headline: How to use Japanese calendar CultureInfo in C# to write dates to Excel
  type: TechArticle
tags:
- C#
- CultureInfo
- Excel
- NPOI
- Internationalization
title: 如何在 C# 中使用日本曆法 CultureInfo 將日期寫入 Excel
url: /zh-hant/net/excel-custom-number-date-formatting/how-to-use-japanese-calendar-cultureinfo-in-c-to-write-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Japanese calendar CultureInfo 寫入日期至 Excel

如果你需要在 C# 中處理日期時 **使用 Japanese calendar CultureInfo**，本指南將會一步步說明。你將學會解析包含日本年號的日期字串（例如 *Reiwa 2/5/1*），然後使用 NPOI 函式庫將產生的 `DateTime` 寫入 Excel 工作表的第一個儲存格。

若未使用正確的 `CultureInfo` 解析以年號為基礎的日期，會導致 `FormatException` 或月份/日期錯誤。透過將 `CultureInfo` 設定為日本曆法，你可確保 .NET 執行環境正確解讀年號，且寫入 Excel 的值與原始的日本表示法相符。

在本教學中，你將會：

* 建立使用日本曆法的 `CultureInfo` 物件。
* 使用 `DateTime.Parse` 解析日本年號日期字串。
* 將解析後的 `DateTime` 插入 NPOI 工作表儲存格。
* 看到完整、可執行的程式碼與預期輸出。

> **先決條件** – .NET 6.0+（或 .NET Core 3.1+）、**NPOI** NuGet 套件，以及對 C# 與 Excel 檔案處理的基本了解。

---

## 你需要的項目

| 項目 | 原因 |
|------|------|
| **.NET SDK** (6.0 或更新) | 提供 `CultureInfo` 所需的執行時與函式庫。 |
| **NPOI** (`NPOI` NuGet 套件) | 讓你在未安裝 Office 的情況下建立與操作 Excel 檔案。 |
| **Visual Studio Code**、**Visual Studio** 或任何 C# IDE | 用於編譯與執行範例。 |
| **Japanese era date string**（例如 `"Reiwa 2/5/1"`） | 示範日本曆法的使用方式。 |

---

## 步驟 1：安裝 NPOI

在專案資料夾的終端機中執行：

```bash
dotnet add package NPOI --version 2.6.1
```

此套件提供稍後會使用的 `IWorkbook`、`ISheet` 與 `ICell` 型別。

---

## 步驟 2：建立使用日本曆法的 CultureInfo

日本曆法是一種以年號為基礎的曆法。你必須取得 `ja-JP` 區域的 *Japanese* 變體，並明確將 `Calendar` 設為 `JapaneseCalendar`。

```csharp
using System;
using System.Globalization;

// Create a CultureInfo based on Japanese locale and switch its calendar.
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

> **為什麼這很重要** – 預設的 `ja-JP` 文化使用公曆。重新指派 `Calendar` 屬性可確保像 *Reiwa* 這樣的年號在解析時被正確辨識。

---

## 步驟 3：解析日本年號日期字串

現在 `CultureInfo` 已配置完成，你可以安全地解析包含年號的字串。

```csharp
// Example Japanese era date: Reiwa 2 (2020) year, May 1st.
string eraDate = "Reiwa 2/5/1";

// Parse using the Japanese CultureInfo created earlier.
DateTime reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
Console.WriteLine($"Parsed DateTime (UTC): {reiwaDate:u}");
```

**輸出**

```
Parsed DateTime (UTC): 2020-05-01 00:00:00Z
```

`Parse` 方法會將 *Reiwa 2* 解析為公曆 2020 年 5 月 1 日。

### 邊緣情況：處理無效的年號

如果使用者提供不支援的年號（例如在平成結束後的 `"Heisei 31/4/30"`），`DateTime.Parse` 會拋出 `FormatException`。將呼叫包在 try‑catch 區塊中，以提供友善的錯誤訊息：

```csharp
try
{
    DateTime parsed = DateTime.Parse(input, japaneseCulture);
}
catch (FormatException)
{
    Console.Error.WriteLine($"'{input}' is not a valid Japanese era date.");
}
```

---

## 步驟 4：將解析後的 DateTime 寫入 Excel 工作表

`DateTime` 物件準備好後，你可以將它存入 Excel 儲存格。NPOI 會自動將 `DateTime` 值格式化為 Excel 日期。

```csharp
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;
using System.IO;

// Create a new workbook and a sheet.
IWorkbook workbook = new XSSFWorkbook();
ISheet sheet = workbook.CreateSheet("Japanese Dates");

// Write the DateTime into cell A1 (row 0, column 0).
IRow row = sheet.CreateRow(0);
ICell cell = row.CreateCell(0);
cell.SetCellValue(reiwaDate);

// Optionally apply a date style that shows the era (Excel does not have a built‑in era format,
// so we keep the Gregorian representation).
ICellStyle dateStyle = workbook.CreateCellStyle();
short dateFormatId = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
dateStyle.DataFormat = dateFormatId;
cell.CellStyle = dateStyle;

// Save the workbook to a file.
using (FileStream fs = new FileStream("JapaneseEraDate.xlsx", FileMode.Create, FileAccess.Write))
{
    workbook.Write(fs);
}
Console.WriteLine("Excel file 'JapaneseEraDate.xlsx' created successfully.");
```

**結果** – 開啟 *JapaneseEraDate.xlsx* 後，A1 儲存格會顯示日期 **2020‑05‑01**。

### 為什麼使用 NPOI？

*支援所有平台*（Windows、Linux、macOS），且 **不需要** Microsoft Office。這使得此解決方案適合 CI 流程、Docker 容器或伺服器端處理。

---

## 步驟 5：完整、可執行的程式

將所有步驟整合起來，以下是一個完整的主控台應用程式，示範整個流程：

```csharp
// File: Program.cs
using System;
using System.Globalization;
using System.IO;
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure CultureInfo for the Japanese calendar.
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // 2️⃣ Parse a Japanese era date string.
        string eraDate = "Reiwa 2/5/1";
        DateTime reiwaDate;
        try
        {
            reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
            Console.WriteLine($"Parsed DateTime: {reiwaDate:u}");
        }
        catch (FormatException)
        {
            Console.Error.WriteLine($"'{eraDate}' is not a valid Japanese era date.");
            return;
        }

        // 3️⃣ Create an Excel workbook and write the date.
        IWorkbook workbook = new XSSFWorkbook();
        ISheet sheet = workbook.CreateSheet("Japanese Dates");
        IRow row = sheet.CreateRow(0);
        ICell cell = row.CreateCell(0);
        cell.SetCellValue(reiwaDate);

        // Apply a simple Gregorian date format.
        ICellStyle style = workbook.CreateCellStyle();
        short fmt = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
        style.DataFormat = fmt;
        cell.CellStyle = style;

        // 4️⃣ Save the workbook.
        const string fileName = "JapaneseEraDate.xlsx";
        using (FileStream fs = new FileStream(fileName, FileMode.Create, FileAccess.Write))
        {
            workbook.Write(fs);
        }

        Console.WriteLine($"Excel file '{fileName}' created successfully.");
    }
}
```

**如何執行**

```bash
dotnet run
```

執行完畢後，你會在專案資料夾中找到 `JapaneseEraDate.xlsx`，其中的日期已正確解析。

---

## 常見陷阱與最佳實踐建議

| 陷阱 | 修正 / 建議 |
|------|------------|
| 忘記設定 `japaneseCulture.DateTimeFormat.Calendar` | 必須指派 `JapaneseCalendar` 實例；否則年號不會被辨識。 |
| 使用 `DateTime.TryParse` 卻未傳入自訂的 `CultureInfo` | 將相同的 `japaneseCulture` 傳給 `TryParse`，以保持行為一致。 |
| 期望 Excel 顯示年號 | Excel 內建的日期格式僅支援公曆。若需顯示年號，請將原始字串存入其他欄位或使用自訂文字格式。 |
| 未釋放 `FileStream` | 如範例所示使用 `using` 區塊，確保檔案句柄即時釋放。 |
| 在多執行緒間混用 `CultureInfo` 物件 | `CultureInfo` 讀取操作是執行緒安全的，但在初始設定後請避免再修改其 `Calendar` 屬性。 |

---

## 結論

你現在已掌握如何在 C# 中 **使用 Japanese calendar CultureInfo**，正確解析日本年號日期，並使用 NPOI 將產生的 `DateTime` 寫入 Excel 工作表。完整範例涵蓋設定、解析、錯誤處理與 Excel 輸出，為任何國際化報表或資料交換情境提供堅實基礎。

接下來，你可以探索：

* **以自訂文字格式化日期**，在 Excel 中保留年號。  
* **使用 `cell.DateCellValue` 從 Excel 讀取日期**，同時遵循日本曆法。  
* **將相同技巧套用於其他年號曆法**（例如泰國佛教曆），只需將 `JapaneseCalendar` 換成相應的 `Calendar` 子類別。

歡迎嘗試不同的年號字串、較大的資料集，或將此邏輯整合至產生即時 Excel 報表的 ASP.NET Core API 中。祝程式開發順利！

## 接下來該學什麼？

以下教學與本指南的技巧密切相關，能進一步擴展你的能力。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在自己的專案中探索替代實作方式。

- [Create Excel Workbook with Japanese Calendar Dates – Full Guide](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/)
- [Parse Japanese Era Dates in Excel – Full Guide for C# Developers](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [How to create Excel workbook and parse Japanese dates in C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}