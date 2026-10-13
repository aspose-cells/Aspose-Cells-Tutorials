---
category: general
date: 2026-03-22
description: Excelから日付を抽出し、datetime を ISO 形式にフォーマットし、Aspose.Cells を使用して C# で ISO 日付を表示する方法を学びましょう。
draft: false
keywords:
- format datetime to iso
- extract date from excel
- display iso date
- Aspose.Cells date parsing
- Japanese era dates
language: ja
og_description: 日付時刻をISO形式に変換するのが簡単です。このガイドでは、Excelから日付を抽出し、Aspose.CellsでISO日付を表示する方法を示します。
og_title: C#で日時をISO形式にフォーマットする – ステップバイステップチュートリアル
tags:
- C#
- Aspose.Cells
- DateTime
- Excel
- ISO 8601
title: C#で日時をISO形式にフォーマットする – 完全ガイド
url: /ja/net/number-and-display-formats-in-excel/format-datetime-to-iso-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でdatetimeをISO形式にフォーマットする – 完全ガイド

Excelブック内にデータがある状態で **format datetime to iso** が必要になったことはありませんか？セルに「令和3年5月1日」のような和暦が入っていて、これをきれいな `2021‑05‑01` 文字列に変換する方法に頭を抱えているかもしれません。あなたは一人ではありません。このチュートリアルでは **extract date from excel** を行い、和暦をパースし、そしてコンソールに **display iso date** を表示します—すべて数行の C# と Aspose.Cells で実現します。

必要なものすべてを順に解説します：必要な NuGet パッケージ、コピー＆ペーストできる正確なコード、各行が重要な理由、そしていくつかのエッジケースに関するヒント。最後には、元の Excel の値がどんなに変則的でも datetime を ISO にフォーマットできる再利用可能なスニペットが手に入ります。

## 必要なもの

- .NET 6.0 以降（コードは .NET Framework 4.6+ でもコンパイル可能です）
- Visual Studio 2022（またはお好みのエディタ）
- **Aspose.Cells for .NET** NuGet パッケージ – `Install-Package Aspose.Cells`
- 和暦形式の日付が入っている Excel ファイル（または新規ブック）

以上です。余計なライブラリや COM インタープ、ただ 1 つの十分にドキュメント化されたメソッドだけです。

## ステップ 1: ワークブックを作成し、和暦日付を書き込む  

最初に操作対象となるワークブックが必要です。既に Excel ファイルがある場合は `new Workbook("path")` で読み込めます。この例ではメモリ上に新しいブックを作成し、セル **A1** に和暦文字列を投入します。

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

> **Why we do this:** Aspose.Cells はセルの値をデフォルトで文字列として扱います。生の和暦テキストを挿入することで、和暦で日付を入力した日本のクライアントが実際に使うシナリオをシミュレートしています。

## ステップ 2: 和暦パースを有効にして日付を抽出する  

Aspose.Cells は日本の和暦文字列を .NET の `DateTime` オブジェクトに自動変換できます—ただしその旨を指示する必要があります。`DateTimeParseOptions.EnableJapaneseEra` フラグがその重い作業を担います。

```csharp
        // 3️⃣ Retrieve the cell value while enabling Japanese era parsing
        CellValue parsed = sheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

> **Pro tip:** `EnableJapaneseEra` オプションを忘れると、ライブラリは元の文字列を返し、続く変換が失敗します。混在コンテンツを扱う場合は必ず `parsed.Type` を確認してください。

## ステップ 3: パースした DateTime を ISO 8601 に変換する  

適切な `DateTime` が手に入ったら、ISO 形式の文字列への変換は楽々です。`"yyyy-MM-dd"` パターンは ISO 8601 の日付部分に準拠しており、ほとんどの API が期待する形式です。

```csharp
        // 4️⃣ Convert to ISO 8601 (yyyy‑MM‑dd) and display it
        string isoDate = parsed.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

プログラムを実行すると次が出力されます：

```
ISO date: 2021-05-01
```

それが求めていた **display iso date** です。

## 完全な実行可能サンプル  

以下はコンソールプロジェクトにそのまま貼り付けられる完全なコードブロックです。隠れた依存関係や余計な設定はありません。

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

> **Expected output:** `ISO date: 2021-05-01`

## ステップバイステップの内訳（各部分が重要な理由）

| Step | What Happens | Why It’s Important |
|------|--------------|--------------------|
| **Create workbook** | インメモリの Excel コンテナを初期化します。 | ファイルシステムに触れずにテストできるサンドボックスを提供します。 |
| **PutValue** | 生の和暦文字列を **A1** に格納します。 | 実際のデータ入力を模倣し、パーサが正確なテキストを取得できるようにします。 |
| **GetValue with `EnableJapaneseEra`** | 和暦文字列を .NET の `DateTime` に変換します。 | カレンダー変換を自動で処理し、手作業の変換表は不要です。 |
| **`ToString("yyyy-MM-dd")`** | `DateTime` を ISO 8601 形式にフォーマットします。 | 文化に依存しない、ソート可能な日付文字列を REST API やデータベースで確実に使用できます。 |
| **Console.WriteLine** | 最終的な ISO 日付を表示します。 | パイプライン全体がエンドツーエンドで機能していることを確認できます。 |

## 一般的なバリエーションの取り扱い  

### 1. 異なるセル位置  

日付が **B2** や名前付き範囲にある場合は、単に `"A1"` を適切なアドレスに置き換えるだけです：

```csharp
worksheet.Cells["B2"].PutValue("令和2年12月31日");
var value = worksheet.Cells["B2"]
    .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

### 2. 列内の複数日付  

多数の行で **extract date from excel** が必要なときは、使用範囲をループします：

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

### 3. 和暦以外の日付のフォールバック  

セルにすでに標準的な日付文字列が入っている場合でもパーサは動作しますが、安全策を設けると良いでしょう：

```csharp
CellValue cv = cell.GetValue(CellValueType.DateTime,
    DateTimeParseOptions.EnableJapaneseEra | DateTimeParseOptions.TryParse);
```

`TryParse` フラグは例外を防ぎ、変換に失敗した場合は元の値を返します。

### 4. 時間コンポーネント  

時間まで必要な場合は `"yyyy-MM-ddTHH:mm:ss"` を使用します：

```csharp
string isoDateTime = parsedValue.DateTimeValue.ToString("yyyy-MM-ddTHH:mm:ss");
```

これにより完全な ISO 8601 タイムスタンプ（`2021-05-01T00:00:00`）が得られます。

## ビジュアルエイド  

![format datetime to iso example](image.png "An example of formatting datetime to iso in C#")

*代替テキスト:* *コンソール出力を示す format datetime to iso の例*

## よくある質問  

- **Can I use this with .xls files?**  
  はい。Aspose.Cells は `.xls`, `.xlsx`, `.csv` など多数のフォーマットを標準でサポートしています。

- **What if the workbook is password‑protected?**  
  `new Workbook("file.xlsx", new LoadOptions { Password = "secret" })` で読み込みます。

- **Is the ISO format locale‑dependent?**  
  いいえ。`"yyyy-MM-dd"` パターンは文化に依存せず、どのマシンでも同じ文字列が保証されます。

- **Does this work on .NET Core?**  
  完全に対応しています—Aspose.Cells は .NET Standard 2.0 に準拠しています。

## まとめ  

**format datetime to iso** を **extract date from excel** で取得し、和暦文字列をパースし、最終的にコンソールに **display iso date** を表示する方法を解説しました。コアステップ—ワークブック作成、和暦テキストの書き込みまたは読み込み、和暦パースの有効化、`ToString("yyyy-MM-dd")` でのフォーマット—はほとんどのシナリオで必要なすべてです。

次にやってみたいこと：

- ISO 日付を別の列に書き戻して下流処理に利用する。
- 変換したブックを CSV にエクスポートして一括インポートに備える。
- Excel アップロードを受け取り JSON‑encoded の ISO 日付を返す Web API と組み合わせる。

さまざまな日付形式、タイムゾーン、あるいは独自カレンダーで実験してみてください。Aspose.Cells の柔軟性のおかげで壁にぶつかることはほとんどありません。

Happy coding, and may all your dates be perfectly ISO‑compliant!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}