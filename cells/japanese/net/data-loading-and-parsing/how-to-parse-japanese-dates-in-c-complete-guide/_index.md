---
category: general
date: 2026-03-29
description: DateTimeParser と CultureInfo を使用して C# で日本の日付を解析する方法。日本の元号日付の解析、C# の日付解析のコツ、そしてエッジケースの対処方法を学びましょう。
draft: false
keywords:
- how to parse japanese
- japanese era date parsing
- datetimeparser c#
- cultureinfo ja-jp
- parse japanese era
- c# date parsing
language: ja
og_description: C# の DateTimeParser と CultureInfo を使用して日本の日付を解析する方法。日本の元号日付解析のステップバイステップソリューションを入手してください。
og_title: C#で日本の日付を解析する方法 – 完全ガイド
tags:
- C#
- .NET
- DateTime
- Localization
title: C#で日本の日付を解析する方法 – 完全ガイド
url: /ja/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#で日本の日付を解析する方法 – 完全ガイド

Ever wondered **how to parse japanese** date strings inside a .NET application? Maybe you’re working on a finance system that receives dates like “令和3年5月12日” from a Japanese client, and you need that into a regular `DateTime`. You’re not alone—localization headaches pop up all the time.  

.NET アプリケーション内で **how to parse japanese** 日付文字列を解析する方法を考えたことがありますか？ たとえば、日本のクライアントから “令和3年5月12日” のような日付を受け取る金融システムを開発していて、それを通常の `DateTime` に変換する必要があるとします。あなた一人ではありません—ローカリゼーションの頭痛の種は常に出てきます。  

The good news is that with the right culture settings and a tiny helper class, **how to parse japanese** dates becomes a piece of cake. In this tutorial we’ll walk through every step, from setting up `CultureInfo` for *ja‑JP* to handling edge‑cases like historic eras. By the end you’ll have a reusable `DateTimeParser` that works for any modern Japanese era date.

> **What you’ll get** – 完全な実行可能サンプル、各行が重要な理由の解説、古い元号に関するヒント、そして手順を忘れないための簡単なチェックリストを提供します。

## 前提条件

- .NET 6+（または .NET Framework 4.7 + – 使用している API は変更されていません）
- 基本的な C# の知識（`using` 文や `Console.WriteLine` に慣れていること）
- 外部 NuGet パッケージは不要です—すべて `System` と `System.Globalization` にあります

既にプロジェクトが開いている場合は、コードをそのまま貼り付けるだけで大丈夫です。まだの場合は、`dotnet new console -n JapaneseDateDemo` で新しいコンソールアプリを作成すれば準備完了です。

## Step 1: 日本のカレンダーシステムを理解する

コードに入る前に、まず “なぜ” を説明しましょう。日本の日付は **era**（元号）形式で表され、皇帝が即位すると年番号がリセットされます。例として：

- **令和** (Reiwa) は 2019‑05‑01 に開始しました。
- **平成** (Heisei) は 1989‑2019 をカバーしました。
- **昭和** (Showa) は 1926‑1989 まで続きました。

.NET の `JapaneseCalendar` クラスはすでにこれらの元号を認識していますが、パーサーに使用するカルチャを指定する必要があります。ここで **cultureinfo ja‑jp** が登場し、カレンダーを日本のロケールに結び付けます。

## Step 2: 小さなラッパー `DateTimeParser` を作成する

`CultureInfo` を至る所に散らす代わりに、ロジックを小さなヘルパーにカプセル化します。これによりコードが再利用可能になり、アプリケーションの他の部分がすっきりします。

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

**Why this helper?**  
- **Single responsibility** – ロケール固有のパースがすべて一箇所に集約されます。  
- **Error handling** – フォーマットが間違っているときに明確なメッセージを表示します。  
- **Future‑proof** – 後で古い *Taisho* や *Meiji* 元号をサポートする必要がある場合は、パターンを調整するかフォールバックを追加するだけです。

## Step 3: `Program.cs` ですべてを接続する

ここではラッパーを使ってサンプル文字列を実際に解析します。`CultureInfo.GetCultureInfo("ja-JP")` で日本のカルチャを取得していることに注目してください。これにより **cultureinfo ja‑jp** の要件が満たされ、`JapaneseCalendar` が有効になります。

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

`dotnet run` を実行すると、次のように表示されます：

```
Japanese: 令和3年5月12日 → Gregorian: 2021-05-12
```

これが **how to parse japanese** 日付の核心です。シンプルですよね？

## Step 4: エッジケースと古い元号の処理

### 4.1 1912 年以前の歴史的な日付

組み込みの `JapaneseCalendar` は近代の元号（明治以降）しかサポートしていません。*Taisho*（1912‑1926）や *Meiji*（1868‑1912）期間の日付を解析する必要がある場合でも、同じパターンが機能します—文字列に正しい元号名（“大正”、 “明治”）が含まれていることを確認してください。パーサーは正しいグレゴリオ暦の `DateTime` を返します。

```csharp
string taisho = "大正5年12月31日"; // 1916‑12‑31
Console.WriteLine(parser.Parse(taisho).ToString("yyyy-MM-dd"));
```

### 4.2 元号がない（曖昧な入力）

クライアントが元号なしで “2021年5月12日” を送ってきた場合、パターンが元号（`ggg`）を期待しているためパーサーは失敗します。次の 2 つの選択肢があります：

1. **Assume Gregorian** – `CultureInfo.InvariantCulture` にフォールバックし、別のパターンを使用する。  
2. **Reject the input** – 呼び出し元に元号が必須であることを通知する。  

以下は簡易的な適応例です：

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

### 4.3 スレッド安全性に関する注意

`CultureInfo` オブジェクトは作成後は読み取り専用なので、スレッド間で同じインスタンスを安全に再利用できます。`DateTimeParser` 自体は可変状態を持たないため **thread‑safe** です—高スループットの Web API に便利な事実です。

## Step 5: すべてをまとめる – コピーしてすぐ使える例

以下は新しいコンソールプロジェクトにそのまま貼り付けられる完全なソースです。外部パッケージや隠れた依存関係はありません。

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