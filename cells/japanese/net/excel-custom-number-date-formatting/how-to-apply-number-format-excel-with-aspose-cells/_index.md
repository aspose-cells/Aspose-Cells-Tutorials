---
category: general
date: 2026-10-10
description: DataTable をインポートし、日付と通貨の書式を設定し、ヘッダー行を保持したまま、Excel の数値書式を迅速に適用できるワンステップです。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- set date format excel
- format excel cells date
- set currency format excel
- preserve header row excel
language: ja
lastmod: 2026-10-10
og_description: Aspose.Cells を使用して C# で Excel の数値書式を適用する。Excel の日付書式の設定、通貨書式の設定、DataTable
  をインポートする際にヘッダー行を保持する方法を学びます。
og_image_alt: Excel worksheet showing currency and date columns formatted after import
og_title: C#でExcelの数値書式を適用する – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: apply number format excel quickly by importing a DataTable, setting
    date and currency formats, and preserving header row excel in a single step.
  headline: How to apply number format excel with Aspose.Cells
  type: TechArticle
tags:
- excel
- aspnet
- csharp
- excel-formatting
title: Aspose.CellsでExcelの数値書式を適用する方法
url: /ja/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cellsで数値書式（Excel）を適用する方法

DataTableからデータを読み込む際に **apply number format excel** を適用したい場合、このガイドで具体的な手順を示します。また、インポート時に **set date format excel**、**set currency format excel**、**preserve header row excel** を行う方法も学べるので、余分な後処理なしでプロフェッショナルなワークシートが作成できます。

ライブラリのインストールから、完全に実行可能なコードスニペットの作成までを網羅します。最終的には、任意の `DataTable` を Excel ワークブックにインポートし、数値列を自動的に書式設定し、ヘッダー行をそのまま保持できるようになります—C# の数行で完了します。

## Prerequisites

開始する前に、以下が揃っていることを確認してください。

* .NET 6.0 以降（コードは .NET Framework 4.6+ でも動作します）
* Visual Studio 2022（またはお好みの C# IDE）
* **Aspose.Cells for .NET** – NuGet でインストール:

```bash
dotnet add package Aspose.Cells
```

* `DataTable` ソース – 例ではサンプルデータを返すヘルパーメソッド `GetTable()` を使用しています。

> **Pro tip:** Aspose.Cells は商用ライブラリですが、30 日間ウォーターマークが無効になる無料評価モードが用意されています。

## Step 1: Create a workbook and access the first worksheet

ワークブックオブジェクトはすべての Excel 操作のエントリーポイントです。新しいワークブックを作成すると、インデックス 0 にデフォルトのワークシートが用意されます。

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook wb = new Workbook();

        // Obtain reference to the first worksheet
        Worksheet sheet = wb.Worksheets[0];
```

*このステップの目的は？*  
`Workbook` はファイル形式、計算エンジン、スタイルリポジトリを管理します。早い段階で `Worksheet` にアクセスしておくと、後でインポートメソッドに対象シートを渡すことが容易になります。

## Step 2: Retrieve the source data as a DataTable

実際のプロジェクトでは、データはデータベースクエリ、CSV パーサー、または API のレスポンスから取得されることが多いです。ここでは、**Product**、**Price**、**ReleaseDate** の 3 列を持つシンプルな `DataTable` を生成します。

```csharp
        // Step 2: Retrieve the source data as a DataTable
        DataTable sourceTable = GetTable();
```

```csharp
        // Helper method that builds a sample DataTable
        static DataTable GetTable()
        {
            DataTable dt = new DataTable();
            dt.Columns.Add("Product", typeof(string));
            dt.Columns.Add("Price", typeof(decimal));
            dt.Columns.Add("ReleaseDate", typeof(DateTime));

            dt.Rows.Add("Widget A", 12.99m, new DateTime(2023, 5, 1));
            dt.Rows.Add("Widget B", 23.50m, new DateTime(2023, 6, 15));
            dt.Rows.Add("Widget C", 7.75m, new DateTime(2023, 7, 30));
            return dt;
        }
```

*このステップの目的は？*  
`DataTable` はメモリ上の表形式データを提供し、Aspose.Cells が直接インポートできるため、列の順序やデータ型が保持されます。

## Step 3: Prepare a `Style` array – one style per column

Aspose.Cells では、インポート時に `Style` オブジェクトの配列を渡すことで、各列に個別のスタイルを適用できます。配列の長さはソーステーブルの列数と一致している必要があります。

```csharp
        // Step 3: Prepare an array of Style objects – one for each column
        Style[] columnStyles = new Style[sourceTable.Columns.Count];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            // Each entry must be instantiated before we can set properties
            columnStyles[i] = wb.CreateStyle();
        }
```

*このステップの目的は？*  
明示的に `CreateStyle()` でスタイルを作成しないと、`Number` を設定しようとした際に `NullReferenceException` が発生します。各 `Style` を初期化しておくことで、後続の代入が確実に成功します。

## Step 4: Assign number formats – currency and date

Excel は組み込みの数値書式を ID で識別します。  
* **14** – 通貨（例: `$1,234.00`）  
* **22** – 短い日付形式（`mm/dd/yyyy`）

```csharp
        // Step 4: Assign number formats to the desired columns
        // Column 0 – Product name (no format needed)
        // Column 1 – Currency format (Number format ID 14)
        columnStyles[1].Number = 14;   // set currency format excel

        // Column 2 – Date format (Number format ID 22)
        columnStyles[2].Number = 22;   // set date format excel
```

> **Note:** カスタム書式（例: `"¥#,##0.00"`）が必要な場合は、組み込み ID の代わりに `Style.Custom = "¥#,##0.00"` を使用してください。

*このステップの目的は？*  
インポート時に正しい **number format** を適用すれば、セルの書式を変更するために後からループで処理する必要がなくなります。また、**format excel cells date** と **set currency format excel** がすべての行で一貫して適用されます。

## Step 5: Import the DataTable while preserving the header row

`ImportDataTable` メソッドはデータをコピーし、最初の行をヘッダーとして保持し、先に用意した列スタイルを適用できます。

```csharp
        // Step 5: Import the DataTable into the worksheet
        // Parameters:
        //   sourceTable – the DataTable to import
        //   true        – preserve the header row (preserve header row excel)
        //   "A1"        – start cell
        //   columnStyles – array of styles for each column
        sheet.Cells.ImportDataTable(sourceTable, true, "A1", columnStyles);
```

```csharp
        // Save the workbook to disk
        wb.Save("FormattedReport.xlsx");
        Console.WriteLine("Workbook created successfully.");
    }
}
```

**Expected output** – `FormattedReport.xlsx` を開くと次のようになります:

| 製品 | 価格（通貨） | 発売日（日付） |
|------|--------------|----------------|
| Widget A | $12.99 | 05/01/2023 |
| Widget B | $23.50 | 06/15/2023 |
| Widget C | $7.75  | 07/30/2023 |

ヘッダー行はそのまま残り、**Price** 列には通貨記号が、**ReleaseDate** 列には短い日付形式が表示されます—追加のスタイリングコードは不要です。

### Handling common edge cases

| 状況 | 解決策 |
|------|--------|
| **スタイルより列が多い** | `columnStyles.Length` が `sourceTable.Columns.Count` と等しいことを確認してください。不足しているエントリはワークブックのデフォルトスタイルが使用されます。 |
| **数値列に null 値がある** | Excel は `null` を空セルとして扱います。後から値が入力された場合でも数値書式は適用されます。 |
| **ロケール固有の通貨** | `columnStyles[i].Custom = "\"€\"#,##0.00"` とし、`columnStyles[i].Number = -1` で組み込み ID を無効化します。 |
| **大規模テーブル（> 100 000 行）** | `ImportDataTable` のオーバーロードに `ImportTableOptions` を使用してストリーミングし、メモリ負荷を軽減してください。 |
| **複数列に同じスタイルを適用** | 配列内で同一の `Style` インスタンスを再利用します（例: `columnStyles[1] = columnStyles[2] = dateStyle;`）。 |

## Bonus: Using a custom format string

組み込み ID が要件に合わない場合は、カスタム数値書式を定義できます。

```csharp
// Example: display Euro currency with no decimal places
Style euroStyle = wb.CreateStyle();
euroStyle.Custom = "\"€\"#,##0";
columnStyles[1] = euroStyle;   // replace the built‑in currency style
```

この方法を使えば、**format excel cells date** や **set currency format excel** を事前定義された ID を超えて自由にコントロールできます。

## Conclusion

これで、Aspose.Cells を使用して `DataTable` をインポートする際に **apply number format excel** を効率的に適用する方法が分かりました。列ごとの `Style` 配列を作成し、組み込みまたはカスタムの数値 ID を割り当て、ヘッダー行を保持する `ImportDataTable` オーバーロードを利用すれば、ワンステップで公開可能なワークシートを生成できます。

### What’s next?

* カスタムパターン（例: `"dddd, mmmm dd, yyyy"`）で **set date format excel** を試す  
* **conditional formatting** と組み合わせて、範囲外の値をハイライト  
* ピボットテーブルやチャートで **format excel cells date** を使用し、動的レポートを作成  

さまざまな数値 ID やカスタム文字列を試して、組織のスタイルガイドに合わせてみてください。コーディングを楽しんでください！

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示したテクニックを基にした、密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、API の追加機能を習得したり、代替実装アプローチを自分のプロジェクトで試したりするのに役立ちます。

- [apply number format excel – 列の書式設定ステップバイステップガイド](/cells/english/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/)
- [Excel ワークブック作成 C# – 通貨書式を適用し DataTable をインポート](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [C# で Excel の日付書式を設定 – 完全インポート書式ガイド](/cells/english/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}