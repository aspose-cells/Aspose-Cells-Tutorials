---
category: general
date: 2026-07-13
description: C# と ExportTableOptions を使用してセル範囲をテーブルとしてエクスポートする方法。ワークブックの設定、書式設定、テーブルエクスポートをステップバイステップで学びます。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export cell range as table
- ExportTableOptions usage
- Workbook and Worksheet handling
- cell value formatting C#
- scientific notation export
language: ja
lastmod: 2026-07-13
og_description: ExportTableOptions を使用して C# でセル範囲をテーブルとしてエクスポートする方法。このガイドに従ってセルの書式設定、ワークブックの作成、テーブルの簡単なエクスポートを行いましょう。
og_image_alt: Diagram illustrating a C# code snippet that exports a single cell range
  as a formatted table
og_title: セル範囲をテーブルとしてエクスポートする方法 – 完全なC#ウォークスルー
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to export cell range as table using C# and ExportTableOptions.
    Learn step‑by‑step workbook setup, formatting, and table export.
  headline: How to Export Cell Range as Table – Complete C# Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
- data export
title: セル範囲をテーブルとしてエクスポートする方法 – 完全なC#ガイド
url: /ja/net/excel-data-export-retrieval/how-to-export-cell-range-as-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# セル範囲をテーブルとしてエクスポートする方法 – 完全な C# ガイド

セル範囲を **テーブルとしてエクスポート** したいのに、書式設定の問題で頭を抱えていませんか？ あなただけではありません。データをレポート パイプラインに流し込む場合でも、手軽な CSV 風ダンプが必要な場合でも、エクスポート手順をマスターすれば、手作業のコピーペーストに費やす時間を何時間も節約できます。

このチュートリアルでは、数値セルに科学的表記を適用し、 **ExportTableOptions** を使ってテーブルとしてエクスポートする正確な手順を解説します。最後まで読めば、実行可能なコードスニペットが手に入り、各呼び出しの *理由* が理解でき、より大きな範囲や別の形式に合わせてコードを調整できるようになります。

## 前提条件

- .NET 6 以上（API は .NET Framework 4.7+ でも同様に動作します）
- Aspose.Cells for .NET がインストール済み（`Install-Package Aspose.Cells`）
- 基本的な C# 文法の理解；Excel の内部構造を深く知る必要はありません

これらが揃いましたか？ では、始めましょう。

## 手順 1: エクスポート オプションの設定 – セル範囲をテーブルとしてエクスポートする方法

最初に必要なのは、セルの内容をどのように扱うかをライブラリに指示する **ExportTableOptions** インスタンスです。これがないと、エクスポートは生の数値になるため、テキストを期待する下流のコンシューマで問題が発生します。

```csharp
// Step 1: Define export options – export the cell value as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Return the cell content as text
    CustomFormat = "0.00E+00"       // Apply scientific notation format
};
```

**重要なポイント:**  
- `ExportAsString = true` は、ライブラリにセルの表示テキストを書き出すよう指示し、内部の double 値ではなく文字列として出力します。  
- `CustomFormat` で **科学的表記のエクスポート** を指定でき、非常に大きな数値や非常に小さな数値を扱う際に便利です。

> **プロのコツ:** 日付や通貨形式が必要な場合は、`"0.00E+00"` をそれぞれ `"yyyy‑MM‑dd"` や `"$#,##0.00"` に置き換えてください。

## 手順 2: ワークブックを作成し、最初のワークシートを取得 – ワークブックとワークシートの操作

**Workbook** は Excel ファイル全体を表し、**Worksheet** は単一のタブを表します。シンプルなエクスポートでは、常に存在するインデックス 0 の最初のシートを使用します。

```csharp
// Step 2: Create a new workbook and access the first worksheet
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

**重要なポイント:**  
新しい `Workbook` を作成すると、隠れたスタイルや残存データがなく、クリーンな状態から始められます。`Worksheets[0]` でアクティブシートを取得するのが、シート名を意識せずに最速の方法です。

## 手順 3: 対象セルに値を設定 – C# におけるセル値の書式設定

ここで、セル **A1**（行 0、列 0）に数値を挿入します。選択する値は意図的に小数点以下が長く、科学的表記の効果を確認しやすくしています。

```csharp
// Step 3: Insert a numeric value into cell A1 (row 0, column 0)
sheet.Cells[0, 0].PutValue(12345.6789);
```

**重要なポイント:**  
`PutValue` を呼び出すとセルのデータ型が自動的に推測されます。後で文字列としてエクスポートするため、先に設定した書式が適用され、 `"1.23E+04"` のように整った出力が得られます。

## 手順 4: 定義したセル範囲をテーブルとしてエクスポート – セル範囲をテーブルとしてエクスポートする

オプションとデータの準備が整ったら、最後に Aspose.Cells に範囲を書き出すよう指示します。`ExportTable` メソッドは開始行/列、範囲のサイズ、そして先ほど作成したオプションオブジェクトを受け取ります。

```csharp
// Step 4: Export the defined cell range as a table using the options above
// Parameters: startRow, startColumn, totalRows, totalColumns, options
sheet.ExportTable(0, 0, 1, 1, exportOptions);
```

**重要なポイント:**  
- `totalRows = 1` と `totalColumns = 1` はエクスポート対象を単一セルに限定しますが、`5, 3` のように数値を変更すれば 5 行 × 3 列の範囲にも拡張できます。  
- このメソッドはデータを内部テーブル構造に書き込み、CSV、HTML、あるいはクライアントへの直接ストリームとして保存可能です。

### 結果の保存（オプション）

エクスポートしたテーブルをディスクに永続化したい場合は、CSV ファイルに書き出すことができます。

```csharp
// Optional: Save the exported table as CSV for verification
using (var stream = new MemoryStream())
{
    sheet.ExportTableToCSV(stream, exportOptions);
    File.WriteAllBytes("ExportedTable.csv", stream.ToArray());
}
```

上記を実行すると、次のようなファイルが生成されます。

```
1.23E+04
```

## エッジケースと一般的なバリエーション

| シチュエーション | 変更点 | 理由 |
|------------------|--------|------|
| **複数行をエクスポート** | `totalRows` を調整し、必要に応じて行をループ | `ExportTable` を繰り返し呼び出すことなく、一括エクスポートが可能 |
| **数式を保持** | `ExportAsString = false` を設定 | 表示値ではなく元の数式を保持 |
| **区切り文字を変更** | `ExportTableToCSV(..., ',', ...)` のオーバーロードを使用 | カンマ区切りからタブ区切りやパイプ区切りに切り替え |
| **大規模ワークシート** | ストリーミングエクスポートで `OutOfMemoryException` を回避 | 10 000 行以上のデータでも安定動作 |

## 完全動作サンプル

以下はコピー＆ペーストでそのまま使用できる完全版プログラムです。Aspose.Cells を参照した任意の .NET コンソール プロジェクトでコンパイルできます。

```csharp
using System;
using System.IO;
using Aspose.Cells;

class ExportCellRangeDemo
{
    static void Main()
    {
        // 1️⃣ Define export options – how to export cell range as table
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            CustomFormat = "0.00E+00"
        };

        // 2️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Put a numeric value into A1
        sheet.Cells[0, 0].PutValue(12345.6789);

        // 4️⃣ Export the single‑cell range as a table
        sheet.ExportTable(0, 0, 1, 1, exportOptions);

        // Optional: write to CSV to see the result
        using (var ms = new MemoryStream())
        {
            sheet.ExportTableToCSV(ms, exportOptions);
            File.WriteAllBytes("ExportedTable.csv", ms.ToArray());
        }

        Console.WriteLine("Export complete! Check ExportedTable.csv");
    }
}
```

**期待される出力:**  
`ExportedTable.csv` という名前のファイルが生成され、1 行だけが含まれます。

```
1.23E+04
```

CSV をテキストエディタで開くと、設定した通りの科学的表記が適用されていることが確認できます。

## 結論

ここまでで、**セル範囲をテーブルとしてエクスポート** する手順を最初から最後まで網羅しました：`ExportTableOptions` の設定、`Workbook` の作成、データの挿入、そして `ExportTable` の呼び出しです。各要素を理解すれば、より大きな範囲や別形式への拡張、さらには Excel 由来データをリアルタイムで提供する Web API への組み込みも容易になります。

今後の参考として、以下を試してみてください。

- **ExportTableToHTML** で Web 用プレビューを作成  
- **ExportTableToDataTable** で ADO.NET パイプラインに直接供給  
- 日付、通貨、パーセンテージ向けの高度な **カスタム書式**  

ぜひ挑戦してみてください。シンプルなセルエクスポートが汎用的なデータ配信エンジンに変わります。質問やユニークなユースケースがあれば、下のコメントで教えてください — Happy coding!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを基に、さらに関連するトピックを深掘りするものです。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、API の追加機能を習得したり、別の実装アプローチを自分のプロジェクトに取り入れたりするのに役立ちます。

- [Aspose.Cells for .NET を使用した可視 Excel 行のエクスポート方法：ステップバイステップ ガイド](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [Aspose.Cells を使用した .NET での Excel ファイルエクスポート方法：包括的ガイド](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [Aspose.Cells for .NET を使用した名前で Excel セルにアクセスする方法：ステップバイステップ ガイド](/cells/english/net/cell-operations/access-cell-by-name-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}