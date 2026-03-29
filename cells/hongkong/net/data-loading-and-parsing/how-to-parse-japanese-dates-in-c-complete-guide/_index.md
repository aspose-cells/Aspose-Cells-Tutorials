---
category: general
date: 2026-03-29
description: 如何在 C# 中使用 DateTimeParser 和 CultureInfo 解析日本日期。了解日本元號日期解析、C# 日期解析技巧，並處理邊緣案例。
draft: false
keywords:
- how to parse japanese
- japanese era date parsing
- datetimeparser c#
- cultureinfo ja-jp
- parse japanese era
- c# date parsing
language: zh-hant
og_description: 如何在 C# 中使用 DateTimeParser 和 CultureInfo 解析日本日期。獲取日本元號日期解析的逐步解決方案。
og_title: 如何在 C# 中解析日本日期 – 完整指南
tags:
- C#
- .NET
- DateTime
- Localization
title: 如何在 C# 中解析日本日期 – 完整指南
url: /zh-hant/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中解析日文日期 – 完整指南

有沒有想過 **如何在 .NET 應用程式中解析日文** 日期字串？或許你正開發一個金融系統，收到日本客戶傳來的「令和3年5月12日」等日期，必須將它轉換成一般的 `DateTime`。你並不孤單——本地化的問題常常讓人頭疼。  

好消息是，只要設定正確的文化資訊並使用一個小型輔助類別，**如何解析日文** 日期就變得輕而易舉。在本教學中，我們會一步步說明，從為 *ja‑JP* 設定 `CultureInfo` 到處理歷史時代等邊緣案例。完成後，你將擁有一個可重用的 `DateTimeParser`，能處理任何現代日文時代的日期。

> **你將獲得** – 完整可執行的範例、每行程式碼背後原因的說明、舊時代的使用技巧，以及快速檢查清單，讓你不會遺漏任何步驟。

## 前置條件

- .NET 6+（或 .NET Framework 4.7 +——我們使用的 API 未變）
- 基本的 C# 知識（應該熟悉 `using` 陳述式與 `Console.WriteLine`）
- 不需要外部 NuGet 套件——全部位於 `System` 與 `System.Globalization` 中

如果你已經開啟專案，太好了——直接把程式碼貼上即可。若還沒有，請使用 `dotnet new console -n JapaneseDateDemo` 建立新的主控台應用程式，即可開始。

## 第一步：了解日本曆法系統

在開始寫程式之前，我們先說明「為什麼」這麼做。日本日期採用 **年號**（元号）格式，當新天皇即位時年份會重新計算。例如：

- **令和**（Reiwa）於 2019‑05‑01 開始。
- **平成**（Heisei）涵蓋 1989‑2019。
- **昭和**（Showa）從 1926‑1989 持續。

.NET 的 `JapaneseCalendar` 類別已內建這些年號，但必須告訴解析器使用哪個文化。這就是 **cultureinfo ja‑jp** 發揮作用的地方——它將曆法與日本語系統結合。

## 第二步：建立小型封裝 – `DateTimeParser`

與其在程式碼各處散布 `CultureInfo`，我們將把邏輯封裝在一個小型輔助類別中。這樣程式碼更易重用，且能讓應用程式的其他部分保持乾淨。

```csharp
// File: DateTimeParser.cs
using System;
using System.Globalization;

public class DateTimeParser
{
    private readonly CultureInfo _culture;
    private readonly JapaneseCalendar _japaneseCalendar;

    public DateTimeParser(CultureInfo culture)
    {
        // Ensure the supplied culture uses the Japanese calendar.
        if (culture.Calendar is not JapaneseCalendar)
            throw new ArgumentException("Culture must use JapaneseCalendar.", nameof(culture));

        _culture = culture;
        _japaneseCalendar = (JapaneseCalendar)culture.Calendar;
    }

    /// <summary>
    /// Parses a Japanese era date string (e.g., "令和3年5月12日") into a Gregorian DateTime.
    /// </summary>
    /// <param name="japaneseDate">The era‑based date string.</param>
    /// <returns>A DateTime representing the same day in the Gregorian calendar.</returns>
    public DateTime Parse(string japaneseDate)
    {
        if (string.IsNullOrWhiteSpace(japaneseDate))
            throw new ArgumentNullException(nameof(japaneseDate));

        // The standard pattern for Japanese era dates.
        // "gggy年M月d日" -> era name (ggg), year (y), month (M), day (d)
        const string pattern = "gggy年M月d日";

        // TryParseExact respects the culture's calendar (JapaneseCalendar here).
        if (DateTime.TryParseExact(
                japaneseDate,
                pattern,
                _culture,
                DateTimeStyles.None,
                out DateTime result))
        {
            return result;
        }

        // If parsing fails, give a helpful exception.
        throw new FormatException(
            $"Unable to parse '{japaneseDate}'. Expected format: {pattern}");
    }
}
```

**為什麼需要這個輔助類別？**  
- **單一職責** – 所有與語系相關的解析都集中在同一處。  
- **錯誤處理** – 當格式不正確時會拋出清晰的訊息。  
- **未來可擴充** – 若日後需要支援較舊的 *大正* 或 *明治* 年號，只要調整模式或加入備援即可。

## 第三步：在 `Program.cs` 中串接所有元件

現在，我們使用這個封裝來實際解析範例字串。請注意，我們透過 `CultureInfo.GetCultureInfo("ja-JP")` 取得日本文化資訊。這滿足了 **cultureinfo ja‑jp** 的需求，並確保 `JapaneseCalendar` 已啟用。

```csharp
// File: Program.cs
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 3‑1: Grab the Japanese culture (ja-JP) which uses JapaneseCalendar.
        var japaneseCulture = CultureInfo.GetCultureInfo("ja-JP");

        // Step 3‑2: Initialise our DateTimeParser with that culture.
        var parser = new DateTimeParser(japaneseCulture);

        // Step 3‑3: The era string we want to convert.
        string eraDate = "令和3年5月12日";

        try
        {
            // Step 3‑4: Parse it.
            DateTime gregorian = parser.Parse(eraDate);

            // Step 3‑5: Show the result – expected: 2021‑05‑12.
            Console.WriteLine($"Japanese: {eraDate} → Gregorian: {gregorian:yyyy-MM-dd}");
        }
        catch (Exception ex)
        {
            // Friendly error output – useful in real‑world apps.
            Console.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

執行 `dotnet run` 後，你會看到：

```
Japanese: 令和3年5月12日 → Gregorian: 2021-05-12
```

這就是 **如何解析日文** 日期的核心。簡單吧？

## 第四步：處理邊緣案例與舊時代

### 4.1 1912 年之前的歷史日期

內建的 `JapaneseCalendar` 只支援現代年號（自明治起）。若需解析 *大正*（1912‑1926）或 *明治*（1868‑1912）時期的日期，使用相同的模式亦可——只要確保字串包含正確的年號名稱（「大正」、「明治」）。解析器仍會回傳正確的公曆 `DateTime`。

```csharp
string taisho = "大正5年12月31日"; // 1916‑12‑31
Console.WriteLine(parser.Parse(taisho).ToString("yyyy-MM-dd"));
```

### 4.2 缺少年號（輸入模糊）

若客戶傳來「2021年5月12日」但未包含年號，解析器會失敗，因為模式要求年號（`ggg`）。你有兩個選擇：

1. **假設為公曆** – 改用 `CultureInfo.InvariantCulture` 並使用不同的模式。  
2. **拒絕此輸入** – 告知呼叫端必須提供年號。

以下是一個快速的調整範例：

```csharp
public DateTime ParseFlexible(string input)
{
    // Try era‑based first.
    try { return Parse(input); } catch { /* ignore */ }

    // Fallback to plain Gregorian pattern.
    const string gregPattern = "yyyy年M月d日";
    if (DateTime.TryParseExact(
            input,
            gregPattern,
            _culture,
            DateTimeStyles.None,
            out DateTime gResult))
    {
        return gResult;
    }

    throw new FormatException("Unable to parse the provided date string.");
}
```

### 4.3 執行緒安全說明

`CultureInfo` 物件在建立後即為唯讀，因此可安全地在多執行緒間重複使用同一實例。`DateTimeParser` 本身不保有可變狀態，使其 **執行緒安全**——對高吞吐量的 Web API 來說相當有用。

## 第五步：整合示範 – 可直接複製的範例

以下是完整的原始碼，你可以直接貼到全新的主控台專案中。無需外部套件，亦無隱藏相依性。

```csharp
// DateTimeParser.cs
using System;
using System.Globalization;

public class DateTimeParser
{
    private readonly CultureInfo _culture;
    private readonly JapaneseCalendar _japaneseCalendar;

    public DateTimeParser(CultureInfo culture)
    {
        if (culture.Calendar is not JapaneseCalendar)
            throw new ArgumentException("Culture must use JapaneseCalendar.", nameof(culture));

        _culture = culture;
        _japaneseCalendar = (JapaneseCalendar)culture.Calendar;
    }

    public DateTime Parse(string japaneseDate)
    {
        if (string.IsNullOrWhiteSpace(japaneseDate))
            throw new ArgumentNullException(nameof(japaneseDate));

        const string pattern = "gggy年M月d日";

        if (DateTime.TryParseExact(
                japaneseDate,
                pattern,
                _culture,
                DateTimeStyles.None,
                out DateTime result))
        {
            return result;
        }

        throw new FormatException(
            $"Unable to parse '{japaneseDate}'. Expected format: {pattern}");
    }

    // Optional flexible parser for non‑era inputs.
    public DateTime ParseFlexible(string input)
    {
        try { return Parse(input); } catch { /* fall through */ }

        const string gregPattern = "yyyy年M月d日";
        if (DateTime.TryParseExact(
                input,
                gregPattern,
                _culture,
                DateTimeStyles.None,
                out DateTime gResult))
        {
            return gResult;
        }

        throw new FormatException("Unable to parse the provided date string.");
    }
}
```

```csharp
// Program.cs
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        var japaneseCulture = CultureInfo.GetCultureInfo("ja-JP");
        var parser = new DateTimeParser(japaneseCulture);

        string[] samples = {
            "令和3年5月12日",   // 2021‑05‑12
            "平成31年4月30日", // 2019‑04‑30 (last day of Heisei)
            "大正5年12月31日", // 1916‑12‑31 (historical)
            "2022年1月1日"      // ambiguous – no era
        };

        foreach (var s in samples)
        {
            try
            {
                DateTime dt = parser.ParseFlexible(s);
                Console.WriteLine($"{s} → {dt:yyyy-MM-dd}");

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}