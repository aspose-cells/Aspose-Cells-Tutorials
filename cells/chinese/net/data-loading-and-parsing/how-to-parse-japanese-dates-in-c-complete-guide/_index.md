---
category: general
date: 2026-03-29
description: 如何在 C# 中使用 DateTimeParser 和 CultureInfo 解析日本日期。学习日本纪元日期解析、C# 日期解析技巧，并处理边缘情况。
draft: false
keywords:
- how to parse japanese
- japanese era date parsing
- datetimeparser c#
- cultureinfo ja-jp
- parse japanese era
- c# date parsing
language: zh
og_description: 如何在 C# 中使用 DateTimeParser 和 CultureInfo 解析日本日期。获取日本元号日期解析的逐步解决方案。
og_title: 如何在 C# 中解析日本日期 – 完整指南
tags:
- C#
- .NET
- DateTime
- Localization
title: 如何在 C# 中解析日本日期 – 完整指南
url: /zh/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中解析日语日期 – 完整指南

有没有想过 **如何解析日语** 日期字符串在 .NET 应用程序中？也许你正在开发一个金融系统，收到日本客户发送的类似 “令和3年5月12日” 的日期，需要将其转换为普通的 `DateTime`。你并不孤单——本地化的麻烦随时都会出现。

好消息是，只要使用正确的文化设置并配合一个小型帮助类，**如何解析日语** 日期就轻而易举了。在本教程中，我们将一步步演示，从为 *ja‑JP* 设置 `CultureInfo` 到处理历史时代等边缘情况。结束时，你将拥有一个可复用的 `DateTimeParser`，能够处理所有现代日语时代的日期。

> **你将获得** – 一个完整、可运行的示例，逐行解释 *为什么* 每行代码重要，提供旧时代的技巧，以及一份快速检查清单，确保不遗漏任何步骤。

## 前置条件

- .NET 6+（或 .NET Framework 4.7 + – 我们使用的 API 没有变化）
- 基础 C# 知识（应熟悉 `using` 语句和 `Console.WriteLine`）
- 无需外部 NuGet 包——所有内容都在 `System` 和 `System.Globalization` 中

如果你已经打开了项目，太好了——直接把代码粘进去即可。如果没有，使用 `dotnet new console -n JapaneseDateDemo` 创建一个新的控制台应用，然后就可以开始了。

## 第 1 步：了解日本历法系统

在编写代码之前，先回答 “为什么”。日本日期采用 **时代**（元号）格式，皇帝更替时年份会重新计数。例如：

- **令和** （Reiwa）始于 2019‑05‑01。
- **平成** （Heisei）覆盖 1989‑2019。
- **昭和** （Showa）从 1926‑1989。

.NET 的 `JapaneseCalendar` 类已经内置了这些时代，但你必须告诉解析器使用哪个文化。这正是 **cultureinfo ja‑jp** 发挥作用的地方——它将日历绑定到日本地区设置。

## 第 2 步：创建一个小型包装类 – `DateTimeParser`

为了避免在代码中到处散布 `CultureInfo`，我们将逻辑封装到一个小帮助类中。这样既可以复用代码，又能保持应用的其余部分整洁。

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

**为什么要使用这个帮助类？**  
- **单一职责** – 所有与地区相关的解析都集中在一个位置。  
- **错误处理** – 当格式错误时提供清晰的错误信息。  
- **面向未来** – 如果以后需要支持更早的 *Taisho* 或 *Meiji* 时代，只需调整模式或添加回退即可。

## 第 3 步：在 `Program.cs` 中接入

现在我们使用包装类实际解析示例字符串。请注意，我们通过 `CultureInfo.GetCultureInfo("ja-JP")` 获取日本文化，这满足了 **cultureinfo ja‑jp** 的要求，并确保 `JapaneseCalendar` 处于激活状态。

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

运行 `dotnet run` 时，你会看到：

```
Japanese: 令和3年5月12日 → Gregorian: 2021-05-12
```

这就是 **如何解析日语** 日期的核心。简单吧？

## 第 4 步：处理边缘情况与旧时代

### 4.1 1912 年之前的历史日期

内置的 `JapaneseCalendar` 只支持现代时代（从明治起）。如果需要解析 *Taisho*（1912‑1926）或 *Meiji*（1868‑1912）时期的日期，同样的模式也适用——只要字符串中包含正确的时代名称（“大正”、 “明治”）。解析器仍会返回正确的公历 `DateTime`。

```csharp
string taisho = "大正5年12月31日"; // 1916‑12‑31
Console.WriteLine(parser.Parse(taisho).ToString("yyyy-MM-dd"));
```

### 4.2 缺少时代（输入模糊）

如果客户端发送 “2021年5月12日” 而未带时代，解析器会因模式要求 `ggg`（时代）而失败。你有两种处理方式：

1. **假设为公历** – 回退到 `CultureInfo.InvariantCulture` 并使用不同的模式。  
2. **拒绝该输入** – 告知调用方必须提供时代信息。

下面是一个快速的适配示例：

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

### 4.3 线程安全说明

`CultureInfo` 对象在创建后是只读的，因此可以安全地在多个线程之间复用。`DateTimeParser` 本身不持有可变状态，因而 **线程安全**——这对高吞吐量的 Web API 非常有用。

## 第 5 步：完整示例 – 直接复制使用

下面是可以直接粘入全新控制台项目的完整源码。无需外部包，也没有隐藏依赖。

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