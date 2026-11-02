---
category: general
date: 2026-08-11
description: C# と Aspose.Cells を使用して JSON を Excel にインポートします。JSON を DataSet にロードし、スマートマーカーを処理して、数分で
  xlsx として保存します。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- import json to excel
- convert json to xlsx
- export json data excel
- load json into dataset
- save workbook c#
language: ja
lastmod: 2026-08-11
og_description: C# と Aspose.Cells を使用して JSON を Excel にインポートします。このガイドでは、JSON を DataSet
  にロードし、スマートマーカーを処理し、ブックを xlsx ファイルとして保存する方法を示し、シームレスなデータエクスポートを実現します。
og_image_alt: Screenshot of C# code importing JSON into an Excel workbook using Aspose.Cells
og_title: C#でJSONをExcelにインポートする – 完全ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Import json to excel using C# and Aspose.Cells. Load JSON into a DataSet,
    process smart markers, and save as xlsx in minutes.
  headline: Import json to excel in C# – step‑by‑step guide
  type: TechArticle
- questions:
  - answer: '`ReadJson` still creates an empty `DataTable`. The smart marker will
      produce only the header row, which is often the desired outcome for reporting
      templates.'
    question: What if the JSON array is empty?
  - answer: Yes. Load each array into its own `DataTable` within the same `DataSet`,
      then call `ProcessSmartMarkers` on each worksheet, referencing the appropriate
      table name in the marker (e.g., `&=Table(Orders)`).
    question: Can I import multiple JSON arrays into different sheets?
  - answer: After `ReadJson`, reorder columns by manipulating `dataSet.Tables[0].Columns`
      before processing the smart marker.
    question: How do I control column order?
  - answer: 'If you need the raw JSON string in a cell, skip the `DataSet` step and
      assign it directly: `worksheet.Cells["A1"].PutValue(jsonData);`'
    question: Is it possible to write JSON directly to a single cell as a string?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- JSON
- Excel automation
title: C#でJSONをExcelにインポートする – ステップバイステップガイド
url: /ja/net/smart-markers-dynamic-data/import-json-to-excel-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で JSON を Excel にインポートする – ステップバイステップガイド

C# で JSON を Excel にインポートする必要がある場合、このチュートリアルが全工程を案内します。JSON を DataSet に読み込み、スマートマーカーを適用し、結果を xlsx ファイルとして保存する方法を学べます。同じ手法で、レポートパイプラインやデータ移行スクリプト向けに JSON を xlsx に変換することも可能です。

本ガイドでは必要なコード行をすべて解説し、各ステップの重要性とよくある落とし穴を紹介します。最終的にカスタムパーサーを書かずに JSON データを Excel にエクスポートでき、実稼働環境向けに workbook を C# で保存する方法が理解できるようになります。Aspose.Cells 以外の外部ツールは不要です。

## 前提条件

開始する前に、以下がインストールされていることを確認してください。

- .NET 6.0 以降  
- Visual Studio 2022（または .NET をサポートする任意の IDE）  
- Aspose.Cells for .NET NuGet パッケージ（`Install-Package Aspose.Cells`）  
- スマートマーカーを含む Excel テンプレートファイル（例: `Template.xlsx`）  

テンプレートには、`&=Table(Data)` というスマートマーカーが入った単一セルが必要です。`Data` は後で渡す DataTable の名前と一致させます。

## JSON を Excel にインポート – プロジェクトのセットアップ

新しいコンソール アプリケーションを作成し、Aspose.Cells の参照を追加します。

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // The complete workflow is demonstrated in the following steps.
        }
    }
}
```

上部に `using` ディレクティブを追加すると、コンパイラが `DataSet`、`Workbook`、関連型を認識できるようになります。この基盤は以降のすべての操作に必須です。

## JSON を xlsx に変換 – JSON を DataSet に読み込む

最初の機能的ステップは、JSON 文字列を `DataSet` に変換することです。Aspose.Cells は配列オブジェクトを直接テーブルに変換する便利な `ReadJson` 拡張メソッドを提供します。

```csharp
// Step 1: Define the JSON source
string jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

// Step 2: Load the JSON into a DataSet
DataSet dataSet = new DataSet();
dataSet.ReadJson(jsonData);
```

**重要なポイント:**  
`ReadJson` は自動的に `Table`（またはルート要素名）という名前の `DataTable` を作成し、JSON のキーに基づいて列を生成します。これにより手動でループ処理を書く必要がなくなり、データ型も正しく推測されます。JSON に入れ子オブジェクトが含まれる場合、Aspose.Cells はそれらを別々のテーブルにフラット化し、後で参照できます。

**ヒント:** JSON ペイロードが大きい場合は、`StringReader` を使ってストリーミングし、文字列全体をメモリにロードしないようにすると良いでしょう。

## JSON データを Excel にエクスポート – スマートマーカー付きテンプレートを開く

次に、スマートマーカーを含むワークブックを開きます。スマートマーカーは、`DataSet` からデータを挿入すべき場所を Aspose.Cells に指示します。

```csharp
// Step 3: Open the Excel template that contains a smart marker
Workbook workbook = new Workbook("YOUR_DIRECTORY/Template.xlsx");
```

**重要なポイント:**  
テンプレートは書式設定とコードを分離します。Excel 上で最終的な見た目（フォント、罫線、条件付き書式など）をデザインし、ライブラリにデータ挿入を任せられます。スマートマーカー構文 `&=Table(Data)` は、マーカーがあるセルに `DataTable` 全体を書き込むようエンジンに指示します。

## JSON データを Excel にエクスポート – スマートマーカーを処理する

作成した `DataTable` を渡して、スマートマーカーを処理します。

```csharp
// Step 4: Process the smart marker, writing the entire array into a single cell
workbook.Worksheets[0].ProcessSmartMarkers(dataSet.Tables[0]);
```

**重要なポイント:**  
`ProcessSmartMarkers` はマーカーを読み取り、テーブルを縦方向に展開し、元のセル書式を保持します。また、列幅や数値書式も基になる .NET 型に基づいて自動的に適用されます。

**エッジケース:** 対象セルに既にデータがある場合、メソッドは上書きします。既存の内容を残したい場合は、テンプレート内の専用領域にマーカーを配置してください。

## workbook を C# で保存 – 最終ファイルを書き出す

最後に、ワークブックを `.xlsx` ファイルとして保存します。アプリケーションが書き込み可能な任意の場所を指定できます。

```csharp
// Step 5: Save the resulting workbook
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx", SaveFormat.Xlsx);
```

**重要なポイント:**  
`SaveFormat.Xlsx` を指定すると、出力が Open XML 標準に準拠し、最新の表計算ソフトで読み取れるようになります。レガシーな `.xls` が必要な場合は、`SaveFormat.Xlsx` を `SaveFormat.Excel97To2003` に置き換えてください。

**プロのコツ:** 大容量ファイル向けに圧縮レベルを制御したい場合は `SaveOptions` を使用します。例: `var opts = new XlsSaveOptions { CompressionLevel = CompressionLevel.Maximum }; workbook.Save("out.xls", opts);`

## 完全なソースコード

すべての手順をまとめると、以下のような実行可能プログラムになります。

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace JsonToExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Define the JSON source
            string jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

            // Load the JSON into a DataSet
            DataSet dataSet = new DataSet();
            dataSet.ReadJson(jsonData);

            // Open the Excel template that contains a smart marker
            Workbook workbook = new Workbook("YOUR_DIRECTORY/Template.xlsx");

            // Process the smart marker, writing the entire array into a single cell
            workbook.Worksheets[0].ProcessSmartMarkers(dataSet.Tables[0]);

            // Save the resulting workbook
            workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx", SaveFormat.Xlsx);

            Console.WriteLine("JSON has been imported to Excel successfully.");
        }
    }
}
```

**期待される出力:**  
プログラムを実行すると `JsonSingleCell.xlsx` が作成されます。ファイルを開くと、スマートマーカーセルの下に 2 行（`John`, `30` と `Anna`, `25`）が配置され、`Template.xlsx` で定義したヘッダー書式が保持されていることが確認できます。

![Import json to excel code example](image.png "Import json to excel code example")

## よくある質問と対処法

- **JSON 配列が空の場合はどうなる？**  
  `ReadJson` は空の `DataTable` を作成します。スマートマーカーはヘッダー行だけを出力し、レポートテンプレートで期待される動作です。

- **複数の JSON 配列を別々のシートにインポートできるか？**  
  はい。各配列を同一 `DataSet` 内の別々の `DataTable` にロードし、各ワークシートで `ProcessSmartMarkers` を呼び出し、マーカーで適切なテーブル名（例: `&=Table(Orders)`）を指定します。

- **列の順序はどう制御する？**  
  `ReadJson` 後に `dataSet.Tables[0].Columns` を操作して列順を入れ替えてから、スマートマーカーを処理します。

- **JSON を文字列として単一セルに書き込むことは可能か？**  
  生の JSON 文字列をセルに入れたい場合は、`DataSet` のステップを省略し、直接 `worksheet.Cells["A1"].PutValue(jsonData);` と代入します。

## 結論

これで Aspose.Cells を使用した C# における JSON → Excel のインポート手順がマスターできました。JSON を DataSet に読み込み、スマートマーカーを処理し、workbook を C# で保存するまでのエンドツーエンドソリューションにより、JSON を xlsx に素早く変換し、JSON データをエクスポートできます。

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [Effortlessly Import JSON into Excel using Aspose.Cells for .NET](/cells/english/net/import-export/import-json-excel-aspose-cells-net/)
- [Import JSON Data into Excel Using Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Efficiently Import JSON to Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/import-export/import-json-to-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}