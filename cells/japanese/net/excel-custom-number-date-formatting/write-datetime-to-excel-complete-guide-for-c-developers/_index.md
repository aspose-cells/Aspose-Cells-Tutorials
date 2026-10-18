---
category: general
date: 2026-04-07
description: C#で日時をExcelに書き込む。ワークシートへの日付の挿入方法、Excelセルの日付値の扱い方、そして日本の元号カレンダーの日付への変換を数ステップで学びましょう。
draft: false
keywords:
- write datetime to excel
- excel cell date value
- insert date into worksheet
- convert japanese calendar date
language: ja
og_description: 日時をExcelに素早く書き込む。このガイドでは、ワークシートへの日付の挿入方法、Excelセルの日付値の管理方法、そしてC#で和暦日付を変換する方法を紹介します。
og_title: Excelに日時を書き込む – ステップバイステップ C# チュートリアル
tags:
- C#
- Excel automation
- Aspose.Cells
title: Excelへ日時を書き込む – C#開発者のための完全ガイド
url: /ja/net/excel-custom-number-date-formatting/write-datetime-to-excel-complete-guide-for-c-developers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel に日時を書き込む – C# 開発者向け完全ガイド

Excel に **日時を書き込む** 必要があったけれど、どの API 呼び出しが正しい Excel の日付として保存されるのか分からなかったことはありませんか？ あなただけではありません。多くの社内ツールでは C# の `DateTime` をスプレッドシートに投入する必要があり、その結果は本物の Excel 日付のようにソート可能で、フィルタリングでき、ピボットテーブルでも使用できる必要があります。  

このチュートリアルでは、Aspose.Cells を使用して *insert date into worksheet* の正確な手順を解説し、カルチャー設定が重要な理由を説明し、さらに **convert Japanese calendar date** を通常の `DateTime` に変換して書き込む方法も示します。最後まで読むと、任意の .NET プロジェクトにコピー＆ペーストできる自己完結型のスニペットが手に入ります。

## 必要なもの

- **.NET 6+** (または最近の .NET バージョン; コードは .NET Framework でも動作します)  
- **Aspose.Cells for .NET** – Office がインストールされていなくても Excel ファイルを操作できる NuGet パッケージです。  
- C# の `DateTime` とカルチャーに関する基本的な理解。  

余計なライブラリは不要で、COM インタープロや Excel のインストールも必要ありません。すでにワークシートインスタンス (`ws`) を持っている場合は、そのまま進められます。

## 手順 1: 日本のカルチャーを設定する (Convert Japanese Calendar Date)

`"R02/05/01"`（令和2年5月1日）のような日付を受け取ったとき、.NET に元号記号の解釈方法を指示する必要があります。日本のカレンダーはデフォルトのグレゴリオ暦ではないため、`JapaneseCalendar` にカレンダーを置き換える `CultureInfo` を作成します。

```csharp
using System;
using System.Globalization;
using Aspose.Cells;   // Make sure Aspose.Cells is referenced

// Assume you already have a worksheet instance named "ws"
Worksheet ws = /* your worksheet instance */;

// 1️⃣ Configure a Japanese culture that uses the Japanese calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

**これが重要な理由:**  
デフォルトのカルチャーで文字列を解析すると、`R`（令和）を年にマッピングできないため .NET はフォーマット例外をスローします。`JapaneseCalendar` に置き換えることで、パーサーは元号記号を理解し、正しいグレゴリオ年に変換できるようになります。

## 手順 2: 元号ベースの文字列を `DateTime` に解析する

カルチャーの準備ができたので、`DateTime.ParseExact` を安全に呼び出せます。フォーマット文字列 `"ggyy/MM/dd"` はパーサーに次のことを指示します：

- `gg` – 元号指定子（例: 令和は `R`）  
- `yy` – 元号内の2桁の年  
- `MM/dd` – 月と日。

```csharp
// 2️⃣ Parse a date string in the Japanese era format (ggyy/MM/dd)
string japaneseDate = "R02/05/01";          // Reiwa 2, May 1st
DateTime parsedDate = DateTime.ParseExact(
    japaneseDate,
    "ggyy/MM/dd",
    japaneseCulture,
    DateTimeStyles.None
);
```

**プロ・チップ:** 他の形式（例: `"Heisei 30/12/31"`）の日付が来る可能性がある場合は、解析を `try/catch` で囲み、`DateTime.TryParseExact` にフォールバックさせます。これにより、1 行の不正なデータでインポート全体がクラッシュするのを防げます。

## 手順 3: `DateTime` を Excel のセルに書き込む (Excel Cell Date Value)

Aspose.Cells は `PutValue` を使用すると、.NET の `DateTime` をネイティブな Excel 日付として扱います。ライブラリは自動的にティック数を Excel のシリアル番号（1900‑01‑00 からの日数）に変換します。これにより、セルは正しい **excel cell date value** を表示し、後で Excel の組み込み日付スタイルで書式設定できます。

```csharp
// 3️⃣ Write the resulting DateTime value into cell C1 of the worksheet
Cell targetCell = ws.Cells["C1"];
targetCell.PutValue(parsedDate);

// Optional: apply a standard date format so users see "yyyy-MM-dd"
targetCell.Style.Number = 14;   // built‑in Excel format ID for "m/d/yy"
```

**Excel での表示例:**  
セル C1 にはシリアル番号 `44796` が格納され、Excel はこれを `2020‑05‑01`（または設定した書式）として表示します。基になる値は文字列ではなく実際の日付なので、ソートが期待通りに機能します。

## 手順 4: ワークブックを保存する (Wrap‑Up)

まだワークブックを保存していない場合は、今すぐ保存してください。このステップは日時の書き込みそのものとは直接関係ありませんが、ワークフローを完了させます。

```csharp
// Save the workbook to a file (or a MemoryStream if you need it in‑memory)
Workbook workbook = ws.Workbook;   // get the parent workbook
workbook.Save("Output.xlsx", SaveFormat.Xlsx);
```

以上です—4 つの簡潔な手順で、**write datetime to Excel** に成功し、途中で日本の元号日付も処理できました。

![Excel に日時を書き込む例](/images/write-datetime-to-excel.png "C# プロジェクトが DateTime を Excel のセル C1 に書き込む様子を示すスクリーンショット")

*上の画像は、セル C1 に日付が正しく表示された最終的な Excel ファイルを示しています。*

## よくある質問とエッジケース

### ワークシート変数がまだ用意できていない場合は？

その場で新しいワークブックを作成できます：

```csharp
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];   // default first sheet
```

### シートに元の日本の元号文字列を保持するには？

元の文字列と解析した日付の両方が必要な場合は、隣接するセルに書き込んでください：

```csharp
ws.Cells["B1"].PutValue(japaneseDate);   // original text
ws.Cells["C1"].PutValue(parsedDate);     // parsed DateTime
```

### 古い .NET バージョンでも動作しますか？

はい。`JapaneseCalendar` は .NET 2.0 以降に存在し、Aspose.Cells は .NET Framework 4.5+ をサポートしています。正しいアセンブリを参照していることを確認してください。

### タイムゾーンはどう扱いますか？

`DateTime.ParseExact` は **Kind** が `Unspecified` の `DateTime` を返します。ソースの日付が UTC の場合は、先に変換してください：

```csharp
DateTime utcDate = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
DateTime localDate = utcDate.ToLocalTime();
targetCell.PutValue(localDate);
```

### カスタム日付書式（例: “yyyy年MM月dd日”）を設定できますか？

もちろんです。`Style.Custom` プロパティを使用します：

```csharp
targetCell.Style.Custom = "yyyy\"年\"mm\"月\"dd\"日\"";
```

これで Excel は `2020年05月01日` と表示しつつ、実際の日付値はそのまま保持されます。

## まとめ

C# から **write datetime to Excel** するために必要なすべてをカバーしました：

1. **Configure** `JapaneseCalendar` を使用した日本のカルチャーを設定し、**convert Japanese calendar date** 文字列を変換します。  
2. **Parse** `DateTime.ParseExact` を使用して元号ベースの文字列を解析します。  
3. **Insert** 生成された `DateTime` をセルに挿入し、適切な **excel cell date value** を確保します。  
4. **Save** ワークブックを保存してデータを永続化します。  

これらの4つの手順で、ソース形式に関係なく安全に **insert date into worksheet** できます。コードは完全に実行可能で、Aspose.Cells だけが必要で、最新の .NET ランタイム上で動作します。

## 次にやることは？

- **Bulk import:** CSV の行をループし、各日本の日付を解析して連続したセルに書き込む。  
- **Styling:** 期限切れの日付をハイライトする条件付き書式を適用する。  
- **Performance:** 数千行を処理する際は `WorkbookDesigner` または `CellStyle` のキャッシュを使用する。  

自由に試してみてください—日本の元号をグレゴリオ暦に置き換えたり、対象セルを変更したり、別のファイル形式（CSV、ODS）に出力したりできます。基本的な考え方は変わりません：解析、変換、そして **write datetime to Excel** を自信を持って行うことです。

コーディングを楽しんで、スプレッドシートが常に正しくソートされますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}