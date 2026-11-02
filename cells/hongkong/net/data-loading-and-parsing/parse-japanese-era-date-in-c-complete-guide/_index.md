---
category: general
date: 2026-06-27
description: 學習如何在 C# 中解析日本年號日期，然後將日期時間格式化為 yyyy‑mm‑dd 以符合 ISO 輸出。提供逐步程式碼、邊緣案例與技巧。
draft: false
keywords:
- parse japanese era date
- format datetime yyyy-mm-dd
- C# JapaneseCalendar
- CultureInfo date parsing
- .NET DateTime era handling
language: zh-hant
og_description: 在 C# 中解析日本年號日期，輕鬆將日期時間格式化為 yyyy‑mm‑dd。完整範例附說明與常見陷阱。
og_title: 在 C# 中解析日本年號日期 – 完整程式設計教學
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Learn how to parse Japanese era date in C# and then format datetime
    yyyy-mm-dd for ISO output. Step‑by‑step code, edge cases, and tips.
  headline: Parse Japanese era date in C# – Complete Guide
  type: TechArticle
- description: Learn how to parse Japanese era date in C# and then format datetime
    yyyy-mm-dd for ISO output. Step‑by‑step code, edge cases, and tips.
  name: Parse Japanese era date in C# – Complete Guide
  steps:
  - name: Multiple Eras
    text: Japan has gone through several eras (Meiji, Taishō, Shōwa, Heisei, Reiwa).
      The `JapaneseCalendar` automatically maps them, so `"H30-12-31"` (Heisei 30)
      becomes `2018-12-31`. Just keep the same parsing logic; the calendar does the
      heavy lifting.
  - name: Invalid Input
    text: 'If a string doesn’t match the expected pattern, `Parse` throws. Use `TryParseExact`
      as shown earlier, or pre‑validate with a regular expression:'
  - name: Time Zones
    text: '`DateTime` objects are “kind‑agnostic” by default. If you need a UTC timestamp,
      call:'
  type: HowTo
tags:
- C#
- .NET
- DateTime
- Localization
title: 在 C# 中解析日本年號日期 – 完整指南
url: /zh-hant/net/data-loading-and-parsing/parse-japanese-era-date-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中解析日本元號日期 – 完整指南

是否曾在 .NET 應用程式中需要 **parse Japanese era date**，卻發現結果怪怪的？你並不孤單。在許多舊有系統中，日期以 “R3‑04‑01” 形式出現，而你需要將它轉換成乾淨的 **format datetime yyyy-mm-dd** 字串，以供 API 或資料庫使用。  

在本教學中，我們將逐步說明如何完成此操作，解釋每個環節為何重要，並示範如何處理常讓開發者頭疼的棘手邊緣案例。

> **Note:** All code is ready to copy‑paste into a console app targeting .NET 6 or later.

## 需要的環境

- .NET 6 SDK（或任何較新版本）
- 具備 C# 與 `System.Globalization` 命名空間的基本知識
- 任意 IDE 或編輯器 – Visual Studio、VS Code、Rider，隨你喜好

不需要額外的 NuGet 套件；所有功能皆內建於 BCL 中。

## 步驟 1：設定使用皇紀的日本文化

首先，我們需要一個能識別日本皇紀的 `CultureInfo`。預設情況下，`ja-JP` 使用的是 Gregorian（公曆）日曆，因此我們要將其 `DateTimeFormat.Calendar` 替換為 `JapaneseCalendar` 實例。

```csharp
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 1: Create a Japanese culture and switch to the Japanese imperial calendar
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // (The rest of the code follows...)
```

> **Why this matters:** `JapaneseCalendar` 會將元號符號（例如 “R” 代表 Reiwa）轉換為正確的公曆年份。若未使用它，`DateTime.Parse` 會拋出 `FormatException`。

## 步驟 2：解析基於元號的日期字串

現在，我們可以將類似 `"R3-04-01"` 的字串傳給 `DateTime.Parse`。剛才設定的文化資訊會告訴解析器如何解讀 “R3” 部分。

```csharp
        // Step 2: Parse a date string that uses the Japanese era format (e.g., "R3-04-01")
        string eraDate = "R3-04-01";
        DateTime parsedDate = DateTime.Parse(eraDate, japaneseCulture);
```

如果你想採用更安全的方式，避免在輸入錯誤時拋出例外，可將 `Parse` 換成 `TryParseExact`：

```csharp
        // Safer alternative with TryParseExact
        if (DateTime.TryParseExact(
                eraDate,
                "ggy-MM-dd",               // ggy = era+year, MM = month, dd = day
                japaneseCulture,
                DateTimeStyles.None,
                out DateTime safeDate))
        {
            parsedDate = safeDate;
        }
        else
        {
            Console.WriteLine("Unable to parse the Japanese era date.");
            return;
        }
```

> **Pro tip:** 自訂格式字串 `"ggy-MM-dd"` 明確告訴解析器預期的格式。`gg` 代表元號標誌，`y` 代表該元號內的年份。

## 步驟 3：將結果轉換為 ISO 8601（`format datetime yyyy-mm-dd`）

最後，我們以標準的 ISO 格式輸出 `DateTime`。格式說明子 `"yyyy-MM-dd"` 正是執行此功能。

```csharp
        // Step 3: Display the parsed date in a standard ISO format
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine(isoDate); // Expected output: 2021-04-01
    }
}
```

執行程式後會輸出：

```
2021-04-01
```

這就是你想要的 **format datetime yyyy-mm-dd**，可直接用於 JSON 載荷、SQL 插入或任何下游系統。

![parse japanese era date example](placeholder.png){alt="parse japanese era date example"}

## 處理其他元號與邊緣案例

### 多個元號

日本歷經多個元號（明治、大正、昭和、平成、令和）。`JapaneseCalendar` 會自動對應它們，因此 `"H30-12-31"`（平成 30）會轉換為 `2018-12-31`。只需使用相同的解析邏輯，日曆會自行處理繁雜的對應。

### 無效輸入

若字串未符合預期模式，`Parse` 會拋出例外。可如前所示使用 `TryParseExact`，或先以正規表達式進行驗證：

```csharp
bool IsValidEraDate(string input) =>
    System.Text.RegularExpressions.Regex.IsMatch(
        input, @"^[RHS][0-9]+-\d{2}-\d{2}$", System.Text.RegularExpressions.RegexOptions.IgnoreCase);
```

### 時區

`DateTime` 物件預設為「種類不明」(kind‑agnostic)。若需要 UTC 時間戳記，可呼叫：

```csharp
DateTime utc = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
```

或使用 `DateTimeOffset` 以取得完整的時區感知。

## 完整範例

以下是完整程式碼片段，可直接放入全新的主控台專案中：

```csharp
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Initialize Japanese culture with the imperial calendar
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // The era‑based date you want to convert
        string eraDate = "R3-04-01";

        // Try parsing – safer than Parse when input may be malformed
        if (!DateTime.TryParseExact(
                eraDate,
                "ggy-MM-dd",
                japaneseCulture,
                DateTimeStyles.None,
                out DateTime parsedDate))
        {
            Console.WriteLine("Failed to parse the Japanese era date.");
            return;
        }

        // Convert to ISO 8601 (format datetime yyyy-mm-dd)
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine($"Original era date: {eraDate}");
        Console.WriteLine($"Converted ISO date: {isoDate}");
    }
}
```

**預期的主控台輸出**

```
Original era date: R3-04-01
Converted ISO date: 2021-04-01
```

## 重點回顧

我們已說明如何 **parse Japanese era date** 字串，步驟如下：

1. 為 `ja-JP` 建立 `CultureInfo`，並換成 `JapaneseCalendar`。
2. 使用 `DateTime.Parse` 或更穩健的 `TryParseExact` 搭配自訂格式。
3. 以 `"yyyy-MM-dd"` 格式化得到的 `DateTime`，以取得所需的 **format datetime yyyy-mm-dd**。

這就是將舊有日本元號資料轉換為現代 ISO 相容系統所需的全部步驟。

## 接下來可以做什麼？

- **批次處理：** 逐行讀取包含元號日期的 CSV，並將 ISO 字串寫入資料庫。
- **在地化：** 將 ISO 日期轉回元號格式以供 UI 顯示（`ToString("ggyy年MM月dd日", japaneseCulture)`）。
- **自訂日曆：** 探索 `TaiwanCalendar` 或 `HijriCalendar` 以滿足其他區域需求。

歡迎自行實驗——更換元號字串、測試邊緣案例，或將此邏輯整合至 ASP.NET Core 端點。若遇到問題，請在下方留言；祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此技術為基礎。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [如何在 .NET 使用 Aspose.Cells 實作日期驗證：完整指南](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [使用 Aspose.Cells .NET 將 Excel 日期系統改為 1904](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [如何在 .NET 使用 Aspose.Cells 實作與格式化 Excel 註解：逐步教學](/cells/english/net/comments-annotations/implement-format-excel-comments-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}