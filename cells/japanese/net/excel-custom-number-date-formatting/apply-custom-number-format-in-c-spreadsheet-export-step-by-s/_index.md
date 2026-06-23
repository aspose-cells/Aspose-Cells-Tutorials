---
category: general
date: 2026-04-07
description: スプレッドシートのセルにカスタム数値書式を適用し、C#でセルの値をエクスポートしながら数値をフォーマットする方法を学びましょう。迅速かつ完全なガイドです。
draft: false
keywords:
- apply custom number format
- format number in spreadsheet
- how to format numeric cell
- how to export cell value
language: ja
og_description: スプレッドシートのセルにカスタム数値書式を適用し、フォーマットされた文字列としてエクスポートします。スプレッドシートで数値をフォーマットし、セルの値をエクスポートする方法を学びましょう。
og_title: カスタム数値フォーマットの適用 – 完全なC#エクスポートチュートリアル
tags:
- C#
- Spreadsheet
- Number Formatting
title: C# スプレッドシートエクスポートでカスタム数値書式を適用する – ステップバイステップガイド
url: /ja/net/excel-custom-number-date-formatting/apply-custom-number-format-in-c-spreadsheet-export-step-by-s/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# スプレッドシートエクスポートでカスタム数値書式を適用する – 完全チュートリアル

セルに **カスタム数値書式** を適用し、その書式化された文字列をスプレッドシートから取得したことがありますか？ あなただけではありません。多くの開発者が、生の数値が返ってきて、期待していた見栄えの良いロケール対応の文字列が得られない壁にぶつかります。このガイドでは、スプレッドシートのセルで数値を書式設定する方法と、人気のある C# スプレッドシートライブラリを使ってセルの値を書式化された文字列としてエクスポートする方法を正確に示します。

このハンズオンが終わる頃には、任意の数値セルに **カスタム数値書式** を適用し、`ExportTable` で結果をエクスポートし、UI やレポートに表示したい正確な出力を確認できるようになります。外部ドキュメントは不要です—すべてここにあります。

## 前提条件

- .NET 6.0 以降（コードは .NET Framework 4.7+ でも動作します）
- `Workbook`、`Worksheet`、`ExportTableOptions` を提供するスプレッドシートライブラリへの参照（例: **Aspose.Cells** または **GemBox.Spreadsheet**；ここで示す API は Aspose.Cells に合わせています）
- 基本的な C# の知識—`Console.WriteLine` が書ければ問題ありません

> **プロのコツ:** 別のライブラリを使用している場合、プロパティ名は概ね同じです（`NumberFormat`、`ExportAsString` など）。それに合わせてマッピングしてください。

## チュートリアルで扱う内容

1. ワークブックを作成し、最初のワークシートを取得する。  
2. セルに数値を挿入する。  
3. `ExportTableOptions` を設定して **カスタム数値書式** を適用し、文字列として返すようにする。  
4. セルをエクスポートし、書式化された結果を出力する。  
5. エッジケースの処理 – セルに数式や null 値が入っている場合は？

さあ、始めましょう。

![カスタム数値書式の例](https://example.com/image.png "カスタム数値書式")

## 手順 1 – ワークブックを作成し、最初のワークシートを取得

最初に必要なのはワークブックオブジェクトです。これは Office アプリで開く Excel ファイルと考えてください。取得したら最初のシートを取得します—多くのチュートリアルがそこから始めるのは、例を簡潔に保つためです。

```csharp
// Step 1: Initialize the workbook and fetch the first worksheet
Workbook workbook = new Workbook();                 // creates an in‑memory workbook
Worksheet worksheet = workbook.Worksheets[0];      // first sheet (index 0)
```

**なぜ重要か:** 新しいワークブックはクリーンな状態から始められるため、後でカスタム数値書式が正しく適用されるよう、隠れた書式設定が干渉する心配がありません。

## 手順 2 – セル B2 に数値を入力（エクスポート対象のセル）

次に書式設定する対象が必要です。セル **B2** は参照しやすく、デフォルトの A1 から離れているため、誤って上書きされるリスクが低い便利な場所です。

```csharp
// Step 2: Insert a raw numeric value
worksheet.Cells["B2"].Value = 1234.56;   // raw double, no formatting yet
```

**数式が入っている場合は？**  
後で生の値を数式（例: `=SUM(A1:A10)`）に置き換えても、次の手順で設定した数値書式はセルに付随しているため、エクスポート時に正しく適用されます。

## 手順 3 – エクスポートオプションを設定し、書式化された文字列として取得

ここがチュートリアルの核心です。ライブラリに **カスタム数値書式** を適用しながらエクスポートするよう指示します。`NumberFormat` 文字列は Excel の「ユーザー定義」カテゴリで使用するパターンと同じです。

```csharp
// Step 3: Set up options for exporting as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,                         // forces string output
    NumberFormat = "#,##0.00;(#,##0.00)"           // custom format: 1,234.56 or (1,234.56) for negatives
};
```

- `ExportAsString = true` は、メソッドが生の double ではなく `string` を返すことを保証します。  
- `NumberFormat = "#,##0.00;(#,##0.00)"` は Excel のパターンを模倣しています：千位区切りにカンマ、少数第2位まで、負の数は丸括弧で囲む。

> **カスタム書式を使う理由:** 文化圏（米国 vs. ヨーロッパ）の違いに関係なく一貫した表示が保証され、会計用の丸括弧などビジネス固有のスタイリングも埋め込めます。

## 手順 4 – 設定したオプションでセルをエクスポート

ここで実際にワークシートから値を取得し、先ほど定義した書式をライブラリに適用させます。

```csharp
// Step 4: Export the formatted value from B2
string formattedResult = worksheet.Cells.ExportTable(
    worksheet.Cells["B2"],   // the source cell
    exportOptions);         // our custom options
```

**エッジケース – 空セル:** `B2` が空の場合、`formattedResult` は `null` になります。出力前にシンプルな null チェックでガードできます。

## 手順 5 – 書式化された文字列を表示

最後に結果をコンソールに出力します。実際のアプリでは、この文字列を PDF、メール、または UI ラベルに渡すことになるでしょう。

```csharp
// Step 5: Show the result
Console.WriteLine(formattedResult);   // Expected output: 1,234.56
```

**期待される出力**

```
1,234.56
```

生の値を `-9876.54` に変更すると、同じ書式で `(9,876.54)` が得られます—多くの会計レポートが求める形式です。

## 完全に実行可能なサンプル

以下は新しいコンソールプロジェクトにコピペできる完全プログラムです。適切な NuGet パッケージ（スプレッドシートライブラリ）を追加すれば、そのままコンパイル・実行できます。

```csharp
using System;
using Aspose.Cells;   // Replace with your library’s namespace if different

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Insert numeric value into B2
        worksheet.Cells["B2"].Value = 1234.56;

        // 3️⃣ Set export options – apply custom number format
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00;(#,##0.00)"   // custom format
        };

        // 4️⃣ Export the cell as a formatted string
        string formattedResult = worksheet.Cells.ExportTable(
            worksheet.Cells["B2"], exportOptions);

        // 5️⃣ Output the result
        Console.WriteLine(formattedResult);   // → 1,234.56
    }
}
```

### 簡易チェックリスト

- **コンパイルできますか？** はい—`Aspose.Cells`（または同等）の DLL が参照されていることを確認してください。  
- **他のカルチャでも動作しますか？** 書式文字列はカルチャ非依存です。ライブラリは指定されたパターンをそのまま使用します。ロケール固有の区切り文字が必要な場合は、エクスポート前に `CultureInfo` の処理を前置できます。

## よくある質問とバリエーション

### 別のパターンで **スプレッドシート内の数値を書式設定** するには？

`NumberFormat` 文字列を置き換えます。たとえば、1 桁の小数点を持つパーセンテージ表示にしたい場合:

```csharp
NumberFormat = "0.0%";
```

### **セルの値を HTML としてエクスポート** したい場合は？

多くのライブラリはエクスポートタイプを受け取るオーバーロードを提供しています。`ExportAsString = true` に加えて `ExportHtml = true`（または同等）を設定します。原則は同じで、書式を定義した後に出力形式を選択します。

### 1 つのセルだけでなく、範囲全体に書式を適用できるか？

もちろん可能です。`Style` オブジェクトに `NumberFormat` を設定し、そのスタイルを `Range` に適用します。エクスポート呼び出しは変更不要で、スタイルが自動的に反映されます。

```csharp
Style style = workbook.CreateStyle();
style.Custom = "#,##0.00;(#,##0.00)";
Range range = worksheet.Cells.CreateRange("A1:C10");
range.ApplyStyle(style, new StyleFlag { NumberFormat = true });
```

### セルに数式が入っている場合はどうなる？

エクスポート処理はまず数式を評価し、得られた数値に対して書式を適用します。自動計算をオフにしている場合は、`Calculate` を呼び出すだけで問題ありません。

```csharp
worksheet.Cells["B2"].Formula = "=SUM(A1:A5)";
worksheet.Calculate();   // forces evaluation
```

## 結論

これで **カスタム数値書式** をスプレッドシートのセルに適用し、**スプレッドシート内の数値を書式設定** し、**セルの値をエクスポート** して表示可能な文字列に変換する方法がマスターできました。上記のコンパクトなコードサンプルは、ワークブック作成から最終出力までのすべてのステップを網羅しているので、すぐに本番プロジェクトに組み込めます。

次のチャレンジは？ **日付や通貨記号、条件付き書式** 用の数値書式を組み合わせてみましょう。また、複数セルを CSV としてエクスポートしつつ、各セルのカスタム書式を保持する方法も探ってみてください。可能性は無限大です。この基礎があれば、どんな要件にも対応できるはずです。

コーディングを楽しんで、書式文字列を少しだけ変えてみる実験も忘れずに！最高の答えは、ちょっとした調整から生まれることが多いです。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}