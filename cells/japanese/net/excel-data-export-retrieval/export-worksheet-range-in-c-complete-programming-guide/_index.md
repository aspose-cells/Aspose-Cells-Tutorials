---
category: general
date: 2026-05-04
description: C# を使用してカスタム書式でワークシートの範囲をエクスポートします。Excel の範囲のエクスポート方法と、セルのエクスポートをカスタマイズする方法を、簡単な手順で学びましょう。
draft: false
keywords:
- export worksheet range
- how to export excel range
- how to customize cell export
- C# Excel export
- worksheet export options
language: ja
og_description: C#でワークシートの範囲をエクスポートする。このガイドでは、Excel の範囲をエクスポートし、セルのエクスポートを迅速かつ確実にカスタマイズする方法を示します。
og_title: C#でワークシートの範囲をエクスポートする – 完全プログラミングガイド
tags:
- C#
- Excel
- Data Export
title: C#でワークシートの範囲をエクスポート – 完全プログラミングガイド
url: /ja/net/excel-data-export-retrieval/export-worksheet-range-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# でワークシート範囲をエクスポートする – 完全プログラミングガイド

デフォルトの出力が期待通りでない、**export worksheet range** が必要になったことはありませんか？ あなただけではありません—多くの開発者がセルのブロックを CSV や JSON ファイルに書き出そうとしたときに同じ壁にぶつかります。 良いニュースは、数行の C# で **export excel range** ができるだけでなく、**customize cell export** で下流フォーマットに合わせてセルの書き出しをカスタマイズできることです。

このチュートリアルでは、実際のシナリオとして Excel ワークブックから *A1:D10* のセルを取得し、すべての値を角括弧で囲んだ文字列に変換してファイルに書き出す手順を解説します。 最後まで読むと、各セルの表現を完全にコントロールしながら **how to export worksheet range** ができるようになり、後で遭遇するかもしれないエッジケースへのヒントもいくつか得られます。

## 必要なもの

- .NET 6 以上（コードは .NET Framework 4.7+ でも動作します）  
- **GemBox.Spreadsheet** NuGet パッケージ（または `ExportTableOptions` を提供する任意のライブラリ；ここで示す API は GemBox のものです）  
- C# の基本的な構文理解 – 特別なことは不要、通常の `using` 文やオブジェクト生成ができれば OK  

これらが揃っていれば、すぐに始められます。

## 手順 1: エクスポートオプションの設定 – 主な制御ポイント  

最初に行うのは `ExportTableOptions` のインスタンスを作成し、すべてのセルを文字列として扱うよう指示することです。 これが **how to export excel range** の基礎となり、データ型の一貫性を保ちます。

```csharp
using GemBox.Spreadsheet;

public class WorksheetExporter
{
    public void ExportRange(string sourcePath, string destinationPath)
    {
        // Load the workbook.
        var workbook = ExcelFile.Load(sourcePath);
        var worksheet = workbook.Worksheets[0]; // assume first sheet

        // Step 1: Create export options and enable string export.
        var exportOptions = new ExportTableOptions
        {
            ExportAsString = true // forces every cell to be exported as text
        };
```

*なぜ文字列エクスポートを強制するのか？*  
後で各セルをカスタマイズするときに、角括弧やその他の記号を挿入します。 すべてを文字列として保持することで、型変換による予期せぬ動作（例: 日付がシリアル番号になる）を防げます。

## 手順 2: CellExport イベントにフックする – 各セルのカスタマイズ  

いよいよ楽しいパートです: **how to customize cell export**。 GemBox は書き出し直前の各セルに対して `CellExport` イベントを発生させます。 このハンドラで値を角括弧で囲んだり、プレフィックスを付加したり、場合によってはセル自体をスキップしたりできます。

```csharp
        // Step 2: Customize each cell's exported value.
        exportOptions.CellExport += (sender, e) =>
        {
            // e.Value holds the original cell content.
            // We'll wrap it in square brackets.
            e.Value = $"[{e.Value}]";
        };
```

*Pro tip:* 数値セルだけを変更したい場合は、角括弧を付加する前に `e.Value.GetType()` をチェックしてください。 この小さなガードで、ヘッダー文字列を誤って壊すリスクを回避できます。

## 手順 3: 目的の範囲をエクスポート – コアアクション  

オプションが整ったら `ExportTable` を呼び出します。 このメソッドはロードしたワークブック、エクスポートしたい範囲のアドレス、そして先ほど設定したオプションを受け取ります。

```csharp
        // Step 3: Export the range A1:D10 using the configured options.
        worksheet.ExportTable(workbook, "A1:D10", exportOptions, destinationPath);
    }
}
```

使用したオーバーロードは直接ファイルに書き出します（デフォルトは CSV）。 メモリ上の文字列が欲しい場合は、最後の引数を `StringWriter` に置き換えて実行後に結果を取得してください。

### 完全動作例

以下は新規プロジェクトに貼り付けてすぐに実行できる、自己完結型のコンソールアプリです（ファイルパスだけ置き換えてください）。

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License key (free version works with limited rows/columns).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        var exporter = new WorksheetExporter();
        exporter.ExportRange(
            sourcePath: @"C:\Temp\Sample.xlsx",
            destinationPath: @"C:\Temp\ExportedRange.csv");

        Console.WriteLine("Export completed. Check C:\\Temp\\ExportedRange.csv");
    }
}
```

**期待される出力（CSV の抜粋）：**

```
[Header1],[Header2],[Header3],[Header4]
[123],[456],[789],[012]
[ABC],[DEF],[GHI],[JKL]
...
```

*A1* から *D10* までのすべてのセルが角括弧で囲まれ、`CellExport` ハンドラで定義した通りになっています。

## 一般的なエッジケースの処理  

### 1. 空セル  

セルが空の場合、`e.Value` は `null` になります。 文字列補間でフォーマットしようとすると例外がスローされます。 事前にチェックして回避しましょう:

```csharp
exportOptions.CellExport += (s, e) =>
{
    var raw = e.Value?.ToString() ?? string.Empty;
    e.Value = $"[{raw}]";
};
```

### 2. 大規模範囲  

数百万行をエクスポートするとメモリ制限に達することがあります。 そのような場合は、ワークブック全体をメモリに読み込むのではなく、出力をストリームで書き出してください:

```csharp
using (var writer = new StreamWriter(destinationPath))
{
    worksheet.ExportTable(workbook, "A1:D1000000", exportOptions, writer);
}
```

### 3. 異なる区切り文字  

CSV だけが必要なわけではありません。 `ExportTableOptions.CsvSeparator` を変更すれば、任意の区切り文字に切り替えられます:

```csharp
exportOptions.CsvSeparator = '\t'; // Tab‑delimited
```

## よくある質問  

**Q: Excel 365 で作成された .xlsx ファイルでも動作しますか？**  
はい。 GemBox は追加設定なしで最新の OpenXML 形式を読み取ります。

**Q: 複数の非連続範囲を一度にエクスポートできますか？**  
単一の `ExportTable` 呼び出しでは直接できません。 各範囲文字列（例: `"A1:D10"`, `"F1:H5"`）をループしてエクスポートし、結果を自分で結合してください。

**Q: 列ごとに異なる書式を適用したい場合は？**  
`CellExport` ハンドラ内で `e.ColumnIndex` が取得できます。 `switch` 文などで列固有のロジックを実装してください。

## まとめ  

**how to export worksheet range** を完全にコントロールしながらセルの外観をカスタマイズする方法、`ExportTableOptions` を使った **how to export excel range** の実装、そして `CellExport` イベントによる **how to customize cell export** の手順を解説しました。 完全なソリューションは数十行の C# で実現でき、実務レベルのシナリオにも十分対応可能です。

次のステップは、角括弧ラッパーを JSON 向けの形式に置き換えてみる、または非表示行をスキップする条件ロジックを試すことです。 Web API のレスポンス用に `MemoryStream` へ直接エクスポートすれば、一時ファイルを作成する必要もありません。

この手順に従っていただければ、任意のワークシート範囲を必要な形でエクスポートする堅牢で再利用可能なパターンが手に入ります。 コーディングを楽しんで、問題があれば遠慮なくコメントを残してください！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}