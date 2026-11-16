---
category: general
date: 2026-11-16
description: Aspose.Cells、動的配列関数、ラムダリデューサーを使用してExcelで配列を拡張する方法を学び、C#からExcelファイルを書き出す。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- create excel workbook
- how to use lambda
- dynamic array functions
- write excel file
language: ja
lastmod: 2026-11-16
og_description: Aspose.Cells、動的配列関数、ラムダリデューサーを使用してExcelで配列を拡張する方法。Excelファイルを書き込む完全なC#サンプルに従ってください。
og_image_alt: Diagram illustrating how to expand array in an Excel worksheet
og_title: Aspose.Cells を使用して Excel で配列を拡張する方法 – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to expand array in Excel using Aspose.Cells, dynamic array
    functions, and a lambda reducer, then write the Excel file from C#.
  headline: How to expand array in Excel with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. `EXPAND` pads missing columns with blank cells. The same works for
      rows.
    question: Can I expand to more columns than the source provides?
  - answer: '`EXPAND` will treat the source as a single row; you can still specify
      rows and columns to reshape it.'
    question: What if the source array is horizontal (`{1,2,3,4,5}`)?
  - answer: The lambda must return a value compatible with the accumulator type. For
      text concatenation you could use `LAMBDA(acc, val, acc & val)`.
    question: Does `REDUCE` work with non‑numeric data?
  - answer: Only when you need the computed values before saving. Excel will recalculate
      on open if you skip it.
    question: Do I need to call `CalculateFormula` for every change?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: Aspose.Cells を使用して Excel で配列を拡張する方法
url: /ja/net/calculation-engine/how-to-expand-array-in-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells を使用した Excel で配列を拡張する方法

C# から Excel ワークシートで **配列を拡張する方法** が必要な場合、本チュートリアルでは正確な手順を示します。Excel ブックを作成し、`EXPAND` や `REDUCE` といった動的配列関数を使用し、**lambda** アキュムレータを適用し、最後に **Excel ファイルを書き込む** 方法を紹介します。この手法は Aspose.Cells 23.10 以降で動作し、手動での Excel インストールは不要です。

本ガイドの最後までに、プログラム上で動的配列数式の威力を示す完全に機能する `ExpandReduceDemo.xlsx` が手に入ります。

## 必要なもの

- .NET 6.0（または Aspose.Cells がサポートする任意の .NET バージョン）
- Aspose.Cells for .NET パッケージ（`dotnet add package Aspose.Cells`）
- コードエディタまたは IDE（Visual Studio、VS Code、Rider など）

Aspose.Cells が内部でファイル形式を処理するため、追加の COM インタープロや Office のインストールは不要です。

## 手順 1: Excel ブックの作成

最初のタスクはメモリ上に **Excel ブックを作成** することです。Aspose.Cells は `Workbook` クラスを提供し、これは XLSX ファイル全体を表します。

```csharp
using System;
using Aspose.Cells;

class ExpandReduceDemo
{
    static void Main()
    {
        // Step 1: instantiate a new workbook and get the default worksheet
        Workbook workbook = new Workbook();              // creates an empty .xlsx structure
        Worksheet sheet = workbook.Worksheets[0];        // the first (and only) sheet by default
```

> **重要な理由:** `Workbook` をインスタンス化すると、クリーンなキャンバスが得られます。デフォルトのワークシートはすでに用意されているため、複数シートが必要でない限り手動で追加する必要はありません。

## 手順 2: 縦方向の配列定数を挿入

Excel の動的配列エンジンはリテラル配列定数を扱えます。縦方向の配列 `{1;2;3;4;5}` をセル **A1** に配置します。

```csharp
        // Step 2: put a vertical array constant into A1
        sheet.Cells["A1"].PutValue("{1;2;3;4;5}");
```

> **ヒント:** セミコロン (`;`) は定数内で行を区切り、カンマ (`,`) は列を区切ります。これは Excel の構文と同様です。

## 手順 3: 配列を行列に拡張

ここで核心の質問である **配列を拡張する方法** に `EXPAND` 関数を使って答えます。この数式は単一列の配列を 5 行 × 2 列の行列に拡張し、**B1** から開始します。

```csharp
        // Step 3: use EXPAND to create a 5‑row by 2‑column matrix
        sheet.Cells["B1"].Formula = "EXPAND(A1,5,2)";
```

> **なぜ EXPAND?** `EXPAND(source, rows, cols)` はソース範囲を指定したサイズに強制的に合わせ、必要に応じて空白で埋めます。単一配列から大きな行列を生成する最も読みやすい方法です。

## 手順 4: lambda アキュムレータで行列を縮小

`REDUCE` 関数は範囲を反復し、**lambda** 式を使用して値を集計します。ここでは各列の値を合計して単一列にし、結果を **D1** に配置します。

```csharp
        // Step 4: REDUCE the expanded matrix using a lambda accumulator
        sheet.Cells["D1"].Formula = "REDUCE(A1, B1:E5, LAMBDA(acc, val, acc+val))";
```

> **lambda の使い方:** `LAMBDA(acc, val, acc+val)` は現在のアキュムレータ (`acc`) と次のセル値 (`val`) を受け取り、新しいアキュムレータを返します。実質的に累積合計を実行します。これはコードから Excel 数式で **lambda の使用方法** を示す例です。

## 手順 5: 数式を計算して結果を表示

Aspose.Cells は数式を設定しただけでは自動的に評価しません。`CalculateFormula` を呼び出すことで、ブック内のすべての数式を計算させます。

```csharp
        // Step 5: recalculate all formulas so the results are materialized
        workbook.CalculateFormula();
```

> **注意:** 生成されたファイルを Excel で開くと、事前に計算されているため値がすでに表示されています。

## 手順 6: Excel ファイルをディスクに保存

最後に、`Save` メソッドを使用して **Excel ファイルを書き込む** ことができます。書き込み権限のあるフォルダーを選択してください。

```csharp
        // Step 6: save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\ExpandReduceDemo.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### 期待される結果

| A | B | C | D |
|---|---|---|---|
| {1;2;3;4;5} | 1 |  | 15 |
|            | 2 |  |    |
|            | 3 |  |    |
|            | 4 |  |    |
|            | 5 |  |    |

- **列 B** と **列 C** には `EXPAND` によって生成された 5 × 2 行列が含まれます。
- **セル D1** には `15` が表示されます。これは `REDUCE` と **lambda** 数式で計算された全数の合計です。

## よくある質問とエッジケース

- **ソースが提供する列数より多くの列に拡張できますか？**  
  はい。`EXPAND` は不足している列を空白セルで埋めます。行についても同様です。

- **ソース配列が横方向（`{1,2,3,4,5}`）の場合はどうなりますか？**  
  `EXPAND` はソースを単一行として扱い、行数と列数を指定して再形成できます。

- **`REDUCE` は数値以外のデータでも機能しますか？**  
  lambda はアキュムレータの型と互換性のある値を返す必要があります。テキスト結合の場合は `LAMBDA(acc, val, acc & val)` を使用できます。

- **すべての変更ごとに `CalculateFormula` を呼び出す必要がありますか？**  
  保存前に計算結果が必要なときだけ呼び出します。省略した場合、Excel は開いたときに再計算します。

## プロのコツ

- **パフォーマンス:** 大規模なブックでは、すべての数式を設定した後に一度だけ `workbook.CalculateFormula` を呼び出し、各セルごとに呼び出さないようにします。
- **バージョンの安全性:** `EXPAND` と `REDUCE` は Excel 365 以降で利用可能です。Aspose.Cells は計算エンジンが組み込まれているため、対象の Excel バージョンに関係なく実装しています。
- **数式のデバッグ:** `sheet.Cells["B1"].Formula` を使用して設定した正確な文字列を取得できます。動的に数式を構築する際に役立ちます。

## 結論

これで、Aspose.Cells を使用して Excel で **配列を拡張する方法** を理解し、**動的配列関数** を活用し、`REDUCE` とともに **lambda** を適用し、C# から **Excel ファイルを書き込む** 方法が分かりました。このエンドツーエンドの例は、行列の転置、累積合計、カスタム集計など、より複雑なデータ変換にも応用できます。

---

*次のステップ:*  
- `FILTER`、`SORT`、`UNIQUE` などの他の動的関数を調査する。  
- �数の `LAMBDA` 式を組み合わせて再利用可能なユーザー定義関数を作成する。  
- ワークブック生成を ASP.NET Core API に統合し、オンデマンドでレポートを作成する。

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、プロジェクトでの代替実装アプローチを探求するのに役立ちます。

- [How to create Excel workbook C# with a dynamic array formula](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/)
- [How to expand array in Excel and populate a template](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)
- [How to Expand Array in C# with Aspose.Cells – Step‑by‑Step Guide](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}