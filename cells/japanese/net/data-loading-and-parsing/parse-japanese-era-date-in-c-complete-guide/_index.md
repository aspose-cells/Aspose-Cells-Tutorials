---
category: general
date: 2026-06-27
description: C#で和暦の日付を解析し、ISO出力用にdatetimeをyyyy‑mm‑dd形式でフォーマットする方法を学びましょう。ステップバイステップのコード、エッジケース、そしてヒント。
draft: false
keywords:
- parse japanese era date
- format datetime yyyy-mm-dd
- C# JapaneseCalendar
- CultureInfo date parsing
- .NET DateTime era handling
language: ja
og_description: C#で和暦日付を解析し、datetimeをyyyy‑mm‑dd形式に簡単にフォーマット。解説と落とし穴を含む完全なサンプル。
og_title: C#で和暦日付を解析する – 完全プログラミングウォークスルー
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
title: C#で和暦日付を解析する – 完全ガイド
url: /ja/net/data-loading-and-parsing/parse-japanese-era-date-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で和暦日付をパースする – 完全ガイド

.NET アプリで **和暦日付をパース** したいけど、結果が期待と違うことはありませんか？ 多くのレガシーシステムでは “R3‑04‑01” のような形式で日付が渡され、API やデータベース向けに **format datetime yyyy-mm-dd** の文字列に変換する必要があります。  

このチュートリアルでは、正確な手順を順を追って解説し、各ステップの重要ポイントと、開発者が陥りがちなエッジケースの対処方法を示します。

> **Note:** すべてのコードは .NET 6 以降を対象としたコンソールアプリにそのままコピペ可能です。

## 必要な環境

- .NET 6 SDK（またはそれ以降のバージョン）
- C# と `System.Globalization` 名前空間の基本的な知識
- IDE またはエディタ – Visual Studio、VS Code、Rider などお好みのもの

外部 NuGet パッケージは不要です。すべて BCL に含まれています。

## Step 1: 和暦カレンダーを使用した日本文化情報の設定

まず、和暦カレンダーを認識できる `CultureInfo` を用意します。既定の `ja-JP` はグレゴリオ暦を使用しているため、`DateTimeFormat.Calendar` を `JapaneseCalendar` に置き換えます。

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

> **Why this matters:** `JapaneseCalendar` は “R” （令和）などの元号記号を正しいグレゴリオ年に変換します。これがないと `DateTime.Parse` は `FormatException` をスローします。

## Step 2: 元号ベースの日付文字列をパースする

これで `"R3-04-01"` のような文字列を `DateTime.Parse` に渡すことができます。先ほど設定したカルチャが “R3” 部分の解釈方法を教えてくれます。

```csharp
        // Step 2: Parse a date string that uses the Japanese era format (e.g., "R3-04-01")
        string eraDate = "R3-04-01";
        DateTime parsedDate = DateTime.Parse(eraDate, japaneseCulture);
```

例外が発生しやすい入力を安全に扱いたい場合は、`Parse` の代わりに `TryParseExact` を使用します。

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

> **Pro tip:** カスタム書式文字列 `"ggy-MM-dd"` は、パーサに期待する形式を正確に伝えます。`gg` が元号、`y` が元号内の年を表します。

## Step 3: 結果を ISO 8601 (`format datetime yyyy-mm-dd`) に変換する

最後に、`DateTime` を標準的な ISO 形式で出力します。書式指定子 `"yyyy-MM-dd"` がそれを実現します。

```csharp
        // Step 3: Display the parsed date in a standard ISO format
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine(isoDate); // Expected output: 2021-04-01
    }
}
```

プログラムを実行すると次のように表示されます。

```
2021-04-01
```

これが求めていた **format datetime yyyy-mm-dd** で、JSON ペイロードや SQL 挿入、その他の下流システムでそのまま使用できます。

![parse japanese era date example](placeholder.png){alt="parse japanese era date example"}

## 他の元号やエッジケースの取り扱い

### 複数の元号

日本は明治・大正・昭和・平成・令和と複数の元号を経ています。`JapaneseCalendar` は自動的にマッピングするため、`"H30-12-31"`（平成30年）は `2018-12-31` に変換されます。パースロジックは同じで、カレンダーが重い処理を担います。

### 無効な入力

文字列が期待パターンに合わない場合、`Parse` は例外をスローします。先述の `TryParseExact` を使うか、正規表現で事前検証します。

```csharp
bool IsValidEraDate(string input) =>
    System.Text.RegularExpressions.Regex.IsMatch(
        input, @"^[RHS][0-9]+-\d{2}-\d{2}$", System.Text.RegularExpressions.RegexOptions.IgnoreCase);
```

### タイムゾーン

`DateTime` オブジェクトはデフォルトで「種別なし」です。UTC タイムスタンプが必要な場合は次のように呼び出します。

```csharp
DateTime utc = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
```

あるいは、完全なゾーン認識が必要なときは `DateTimeOffset` を使用します。

## 完全動作サンプル

新規コンソールプロジェクトにそのまま貼り付けられるコード全体は以下です。

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

**期待されるコンソール出力**

```
Original era date: R3-04-01
Converted ISO date: 2021-04-01
```

## まとめ

**和暦日付文字列** をパースする手順は次の通りです。

1. `ja-JP` 用の `CultureInfo` を作成し、`JapaneseCalendar` に差し替える。  
2. カスタム書式付きの `DateTime.Parse` または、より堅牢な `TryParseExact` を使用する。  
3. 結果の `DateTime` を `"yyyy-MM-dd"` でフォーマットし、**format datetime yyyy-mm-dd** を取得する。

以上で、レガシーな和暦データをモダンな ISO 準拠システムへ橋渡しする準備が整いました。

## 次にやることは？

- **バッチ処理:** CSV の和暦日付をループで走査し、ISO 文字列をデータベースに書き込む。  
- **ローカリゼーション:** ISO 日付を UI 表示用に和暦形式へ変換する（`ToString("ggyy年MM月dd日", japaneseCulture)`）。  
- **カスタムカレンダー:** `TaiwanCalendar` や `HijriCalendar` など、他地域向けカレンダーを探求する。

ぜひ試してみてください。元号文字列を入れ替えたり、エッジケースをテストしたり、ASP.NET Core エンドポイントに組み込んだりしてみましょう。質問や問題があればコメントで教えてください。Happy coding!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、API 機能の習得や代替実装アプローチの探求に役立ちます。

- [How to Implement Date Validation in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Change Excel Date System to 1904 using Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [How to Implement and Format Excel Comments Using Aspose.Cells for .NET: A Step‑By‑Step Guide](/cells/english/net/comments-annotations/implement-format-excel-comments-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}