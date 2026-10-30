---
category: general
date: 2026-09-24
description: C#でAspose.Cellsを使用して日本の天皇の元号でDateTimeを解析します。日本の元号カレンダーを有効にし、元号文字列を書き込み、正確なDateTime値を取得します。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Parse DateTime with Japanese Emperor Reign
- Aspose.Cells
- C# date parsing
- Japanese era calendar
- Workbook Settings
- DateTimeValue
language: ja
lastmod: 2026-09-24
og_description: Aspose.Cells を使用して C# で日本の天皇在位期間の DateTime を解析する。このチュートリアルでは、日本の元号カレンダーを有効にし、元号文字列を書き込み、正しい
  DateTime を読み戻す方法を示します。
og_image_alt: Screenshot of C# code parsing a Japanese era date with Aspose.Cells
og_title: Aspose.Cells を使用した日本の天皇在位期間での DateTime 解析 – C# ガイド
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  headline: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  type: TechArticle
- description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  name: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  steps:
  - name: Multiple era formats
    text: 'Aspose.Cells recognises several era representations:'
  - name: Invalid strings
    text: 'When the string cannot be parsed (e.g., `"令和99年13月40日"`), `DateTimeValue`
      returns `DateTime.MinValue`. You can check for this condition:'
  - name: Disabling the feature
    text: 'If you later need to store raw era strings without conversion, set the
      flag back to `false`:'
  - name: Performance tip
    text: Enabling the era calendar adds a small overhead to every `PutValue` call
      that involves strings. If you only parse a handful of cells, enable the flag
      right before the operation and disable it afterward to minimise impact.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DateTime
- Japanese era
- .NET
title: Aspose.Cells を使用して日本の元号で DateTime を解析する
url: /ja/net/excel-custom-number-date-formatting/parse-datetime-with-japanese-emperor-reign-using-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells を使用した日本の元号で DateTime を解析する

.NET アプリケーションで **日本の元号で DateTime を解析** する必要がある場合、このガイドでは Aspose.Cells を使用した具体的な手順を示します。日本の元号カレンダーを有効にし、元号ベースの文字列を書き込み、結果として得られる `DateTime` 値を取得することで、手動で文字列を操作することなく、信頼性の高い文化対応の日付を得ることができます。

日本の元号日付の取り扱いは、金融、政府、そして「令和3年5月10日」のように日付を保存しているレガシーシステムで一般的です。このチュートリアルでは、プロジェクトのセットアップから計算やログ、UI 表示に使用できる `DateTime` オブジェクトの取得まで、完全なワークフローをカバーします。

## 学習内容

- C# プロジェクトに Aspose.Cells NuGet パッケージを追加する方法。  
- `Workbook.Settings` を使用して **Japanese era calendar** を有効にする方法。  
- セルに日本の元号日付文字列を書き込み、Aspose.Cells に自動的に解析させる方法。  
- `DateTimeValue` プロパティを使用して解析された `DateTime` を読み取る方法。  

**Prerequisites**  
- .NET 6.0 以降（コードは .NET Framework 4.7+ でも動作します）。  
- C# と Visual Studio（または任意の IDE）に関する基本的な知識。  
- Aspose.Cells パッケージをダウンロードするためのインターネット接続。

---

## 手順 1: Aspose.Cells のインストール

ターミナルまたは NuGet パッケージ マネージャ コンソールでプロジェクト フォルダーを開き、次のコマンドを実行します：

```bash
dotnet add package Aspose.Cells
```

または、Visual Studio でプロジェクトを右クリック → **Manage NuGet Packages** → **Aspose.Cells** を検索し、**Install** をクリックします。  
これにより `Aspose.Cells` アセンブリが追加され、`Workbook`、`Worksheet`、および必要な解析機能が提供されます。

## 手順 2: 日本の元号カレンダーを有効にする

Aspose.Cells はデフォルトで日本の元号解析を無効にしています。`Workbook.Settings.UseJapaneseEraCalendar` フラグで有効にする必要があります。

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Enable parsing of Japanese era dates (e.g., 令和, 平成)
        workbook.Settings.UseJapaneseEraCalendar = true;
```

`UseJapaneseEraCalendar` を `true` に設定すると、ライブラリは元号名（`令和`、`平成`、`昭和` など）を含む文字列を公式の日本カレンダー規則に従って解釈します。

## 手順 3: セルに日本の元号日付文字列を書き込む

次に、最初のワークシートを取得し、セル **A1** に日本の元号日付文字列を配置します。

```csharp
        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Write the era‑based date string into cell A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");
```

**この動作の理由:**  
`UseJapaneseEraCalendar` が有効な場合、`PutValue` は文字列を調べ、元号プレフィックス（`令和`）を検出し、内部的に対応するグレゴリオ暦の年（2021）に変換します。ライブラリはこの値をテキストではなく、実際の `DateTime` オブジェクトとして保存します。

## 手順 4: 解析された `DateTime` 値を取得する

セルの `DateTimeValue` を読み取ります。Aspose.Cells は自動的にグレゴリオ暦の日付を返します。

```csharp
        // Retrieve the parsed DateTime from cell A1
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Output the result to the console
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
    }
}
```

プログラムを実行すると次が出力されます：

```
Parsed Gregorian date: 2021-05-10
```

出力は、**Parse DateTime with Japanese Emperor Reign** が “令和3年5月10日” を正しく 2021 年 5 月 10 日に変換したことを確認しています。

## 手順 5: エッジケースと一般的なバリエーションの処理

### 複数の元号フォーマット
Aspose.Cells はいくつかの元号表記を認識します:

| 元号 (Japanese) | グレゴリオ暦 年範囲 |
|----------------|----------------------|
| 明治 (Meiji)   | 1868‑1912            |
| 大正 (Taishō)  | 1912‑1926            |
| 昭和 (Shōwa)   | 1926‑1989            |
| 平成 (Heisei)  | 1989‑2019            |
| 令和 (Reiwa)   | 2019‑present         |

ソース データに全角文字やスペースが混在していたり、漢字の “年”、 “月”、 “日” を使用していても、パーサは正常に動作します。例として、`"平成31年4月30日"` は `2019-04-30` に変換されます。

### 無効な文字列
文字列が解析できない場合（例: `"令和99年13月40日"`）、`DateTimeValue` は `DateTime.MinValue` を返します。この状態をチェックできます:

```csharp
if (parsedDate == DateTime.MinValue)
{
    Console.WriteLine("The cell does not contain a valid Japanese era date.");
}
```

### 機能の無効化
後で変換せずに元号文字列をそのまま保存したい場合は、フラグを `false` に戻します:

```csharp
workbook.Settings.UseJapaneseEraCalendar = false;
```

### パフォーマンスのヒント
元号カレンダーを有効にすると、文字列を含むすべての `PutValue` 呼び出しにわずかなオーバーヘッドが追加されます。数個のセルだけを解析する場合は、操作直前にフラグを有効にし、完了後に無効にすることで影響を最小限に抑えられます。

## 完全な実行可能サンプル

以下は、すぐにコピーして貼り付け、実行できる完全なプログラムです。

```csharp
using Aspose.Cells;
using System;

class ParseJapaneseEraDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Turn on Japanese era parsing
        workbook.Settings.UseJapaneseEraCalendar = true;

        // 3️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 4️⃣ Write an era date string into A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");

        // 5️⃣ Retrieve the parsed DateTime
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
        // Expected output: Parsed Gregorian date: 2021-05-10
    }
}
```

**期待される出力**

```
Parsed Gregorian date: 2021-05-10
```

このプログラムは、Aspose.Cells を使用した **Parse DateTime with Japanese Emperor Reign** のエンドツーエンドのフローを示しており、ワークブックの作成から利用可能な `DateTime` オブジェクトの取得までをカバーしています。

---

## 結論

これで、C# で **Parse DateTime with Japanese Emperor Reign** を行う方法が分かりました:

1. **Aspose.Cells** をインストールする。  
2. `Workbook.Settings` を使用して **Japanese era calendar** を有効にする。  
3. 元号ベースの文字列をセルに書き込む。  
4. 結果として得られる `DateTimeValue` を読み取る。  

このアプローチにより、手動の解析ロジックが不要になり、公式な元号の境界を尊重し、既存の .NET 日付処理コードとシームレスに統合できます。  

**次のステップ**  
- Hijri カレンダーやタイ仏教暦など、**C# date parsing** を含む Aspose.Cells の他の文化固有機能を探求する。  
- `CalcEngine` などの **Workbook Settings** と組み合わせて、元号日付を参照する数式を評価する。  
- 解析された `DateTime` をレポート、データベース保存、またはグレゴリオ暦の日付が必要な UI コンポーネントで使用する。  

さまざまな元号文字列で実験したり、無効な入力を処理したり、ソリューションを大規模なデータインポート パイプラインに統合したりしてみてください。コーディングを楽しんでください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法に基づく密接に関連したトピックをカバーしています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Excel で日本の元号日付を解析 – C# 開発者向け完全ガイド](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [C# で日本の日付を解析する方法 – 完全ガイド](/cells/english/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/)
- [Aspose.Cells を使用した .NET の日付検証実装方法 – 包括的ガイド](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}