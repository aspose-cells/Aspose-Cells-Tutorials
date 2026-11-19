---
category: general
date: 2026-11-19
description: C#でExcelの通貨形式を設定 – Excelワークシートのインポート時に、数値形式と列のスタイルを設定する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set currency format
- how to set number format
- assign number format
- excel worksheet import
- style excel columns
language: ja
lastmod: 2026-11-19
og_description: C#でExcelの通貨形式を設定し、数値形式の設定、数値形式の割り当て、Excelシートのインポート時に列のスタイルを適用する方法を学びましょう。
og_image_alt: Screenshot showing Excel cells formatted as currency after import
og_title: C#でExcelの通貨形式を設定する – 完全ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  headline: Set currency format while importing data into Excel using C#
  type: TechArticle
- description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  name: Set currency format while importing data into Excel using C#
  steps:
  - name: Expected result
    text: 'When you open **FinancialReport.xlsx**, you’ll see:'
  - name: Assign number format to date columns
    text: '```csharp // Suppose column 2 contains dates and you want "dd-MMM-yyyy"
      columnStyles[2].Number = 14; // 14 = built‑in short date ```'
  - name: Use custom number formats for percentages
    text: '```csharp columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00% ```'
  - name: Styling beyond number formats
    text: 'You can also set font, background color, or alignment on the same `Style`
      object:'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
- Formatting
title: C# を使用してデータを Excel にインポートする際に通貨形式を設定する
url: /ja/net/excel-custom-number-date-formatting/set-currency-format-while-importing-data-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# でデータを Excel にインポートする際に通貨書式を設定する方法

Excel ワークシートで **通貨書式を設定** したい場合、このガイドでは **数値書式を設定** し、列にスタイルを適用しながら **Excel ワークシートのインポート** を行う方法を示します。`DataTable` の各列に正しい数値書式を割り当て、希望通りのスタイリングでデータをインポートする完全な実行可能サンプルが確認できます。

C# から Excel を操作する際は、単に生データを出力するだけでなく、数値の表示方法も制御する必要があります。請求書や財務レポート、ダッシュボードを作成する場合、通貨・パーセンテージ・日付を正しく書式設定することで、出力がすぐに読みやすくなります。

## 前提条件

開始する前に以下を確認してください。

* .NET 6.0（またはそれ以降）がインストールされていること。
* **Aspose.Cells for .NET**（または `Style` クラスに `Number` プロパティを持つ任意のライブラリ）への参照があること。  
  *NuGet*: `Install-Package Aspose.Cells`。
* `DataTable` と C# コレクションの基本的な知識。
* Visual Studio 2022 または VS Code などの IDE。

## 手順 1: ワークシートに書き込むデータを取得する

まず、エクスポートしたい生データを保持した `DataTable` を取得します。実際のプロジェクトでは、データベースクエリ、API 呼び出し、CSV パーサーなどから取得することが多いでしょう。

```csharp
using System.Data;

/// <summary>
/// Returns a sample DataTable with three columns:
/// Id (int), Amount (decimal), and Description (string).
/// </summary>
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Amount", typeof(decimal));
    table.Columns.Add("Description", typeof(string));

    // Sample rows
    table.Rows.Add(1, 1234.56m, "Office supplies");
    table.Rows.Add(2, 98765.43m, "Consulting fees");
    table.Rows.Add(3, 0.99m, "Miscellaneous");

    return table;
}

// Retrieve the data
DataTable dataTable = GetData();
```

> **重要ポイント:** 完全にデータが入った `DataTable` をインポートすることで、データ取得ロジックと Excel 生成ロジックを分離でき、テスト容易性と保守性が向上します。

## 手順 2: スタイル配列を作成 – DataTable の列数分だけ用意する

Aspose.Cells は、インポートする列数と同じ長さの `Style[]` を期待します。各要素には特定の数値書式を保持させます。

```csharp
// Allocate a Style object for each column
Style[] columnStyles = new Style[dataTable.Columns.Count];

// Initialize each Style instance (required before assigning properties)
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = ws.Workbook.CreateStyle();
}
```

> **プロのコツ:** 書式が必要な列が一部だけでも、すべての列に対して `Style` インスタンスを作成しなければなりません。作成しないとインポート時に `NullReferenceException` が発生します。

## 手順 3: 必要な列に数値書式を割り当てる

組み込みのスタイル番号はライブラリごとに異なります。Aspose.Cells の場合:

* `0` → General（整数）  
* `2` → Currency（例: `$#,##0.00`）  
* `3` → Date など

ここでは **数値書式を割り当て** る例として、最初の列（Id）は整数のまま、2 番目の列（Amount）に通貨書式を設定します。

```csharp
// Column 0 → integer format (style number 0)
columnStyles[0].Number = 0;

// Column 1 → currency format (style number 2)
columnStyles[1].Number = 2;

// If you need a custom format, you can also use a format string:
// columnStyles[1].Custom = "$#,##0.00";
```

> **数値書式の設定方法:** `Number` プロパティを使用すると、組み込み書式を手早く指定できます。ロケール固有の通貨を扱う場合は、適切な通貨記号を含むカスタム書式文字列を使用してください。

## 手順 4: DataTable をワークシートにインポートし、列スタイルを適用する

スタイル配列の準備ができたら、データをインポートします。`ImportDataTable` メソッドは渡したスタイルを尊重します。

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];

// Import the DataTable, starting at cell A1 (row 0, column 0)
// The third argument (true) tells the method to write column headers.
ws.Cells.ImportDataTable(
    dataTable,
    /* includeColumnNames */ true,
    /* startRow */ 0,
    /* startColumn */ 0,
    columnStyles);

// Save the workbook
workbook.Save("FinancialReport.xlsx", SaveFormat.Xlsx);
```

### 期待される結果

**FinancialReport.xlsx** を開くと、以下のように表示されます。

| Id | 金額          | 説明               |
|----|--------------|-------------------|
| 1  | $1,234.56    | 事務用品           |
| 2  | $98,765.43   | コンサルティング費用 |
| 3  | $0.99        | 雑費               |

***金額** 列は設定した通貨書式で表示され、**Id** 列は整数のままです。*

## 追加シナリオ向けの数値書式設定方法

### 日付列に数値書式を割り当てる

```csharp
// Suppose column 2 contains dates and you want "dd-MMM-yyyy"
columnStyles[2].Number = 14; // 14 = built‑in short date
```

### パーセンテージ用にカスタム数値書式を使用する

```csharp
columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00%
```

### 数値書式以外のスタイリング

同じ `Style` オブジェクトでフォント、背景色、配置なども設定できます。

```csharp
columnStyles[1].Font.IsBold = true;
columnStyles[1].ForegroundColor = Color.LightYellow;
columnStyles[1].HorizontalAlignment = TextAlignmentType.Center;
```

> **なぜ機能するのか:** `Style` オブジェクトはセルの視覚プロパティをすべて集約します。配列を `ImportDataTable` に渡すと、各セルは自動的に定義されたスタイルを継承します。

## よくある落とし穴と回避策

| 落とし穴 | 症状 | 対策 |
|---------|------|------|
| 各 `Style` をインスタンス化し忘れる | インポート時に `NullReferenceException` が発生 | 配列をループし、プロパティ設定前に `CreateStyle()` を呼び出す |
| 組み込み数値インデックスを間違える | 書式が誤る（例: 日付が整数として表示） | ライブラリのドキュメントで正しい `Number` 定数を確認 |
| ワークブックを保存し忘れる | 出力ファイルが生成されない、または空ファイルになる | インポート完了後に必ず `workbook.Save(...)` を呼び出す |
| 通貨記号のロケール不一致 | 米国以外でも `$` が表示される | 適切なシンボルを含むカスタム書式文字列（例: `"€#,##0.00"`）を使用 |

## 完全な実行可能サンプル



## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、API の追加機能を習得したり、独自プロジェクトで代替実装を検討したりする際に役立ちます。

- [Create excel file c# – style cells and set currency format](/cells/english/net/excel-formatting-and-styling/create-excel-file-c-style-cells-and-set-currency-format/)
- [How to Format Excel Columns in C# – Complete Guide](/cells/english/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/)
- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}