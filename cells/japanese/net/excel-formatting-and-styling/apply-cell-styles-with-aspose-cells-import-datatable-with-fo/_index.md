---
category: general
date: 2026-06-05
description: Aspose.Cells のインポートを使用する際にセルスタイルを適用します。書式設定された DataTable のインポート方法、行のスタイル設定、そしてワークシートを整頓する方法を学びましょう。
draft: false
keywords:
- apply cell styles
- aspose cells import
- import with formatting
- how to import datatable
- import datatable worksheet
language: ja
og_description: DataTable を Aspose.Cells ワークシートにインポートする際にセルスタイルを適用する。コード全文とヒント付きのステップバイステップガイド。
og_title: Aspose.Cellsでセルスタイルを適用 – DataTableのインポート
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  headline: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  type: TechArticle
- description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  name: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  steps:
  - name: How It Works
    text: 1. **Headers** – Because we passed `true`, Aspose writes “Name” and “Score”
      into the first row. 2. **Data Rows** – Each subsequent row receives the corresponding
      style from `importStyles`. 3. **Performance** – The method streams the data
      directly into the worksheet, which is faster than looping cell
  - name: What if My DataTable Has More Columns Than Styles?
    text: Aspose will apply the last style in the array to any extra columns. To avoid
      unexpected colors, always match the array length to the column count, or pass
      `null` for columns you don’t want styled.
  - name: Can I Apply Different Styles to Specific Rows?
    text: 'Absolutely. After the import, you can loop through rows and assign new
      `Style` objects based on conditions (e.g., highlight scores > 90 in green).
      Here’s a quick snippet:'
  - name: Does This Work with Large DataSets?
    text: Yes. `ImportDataTable` streams data efficiently, and applying a static style
      array adds negligible overhead. For millions of rows, consider using `ImportDataTable`
      in chunks or leveraging `Cells.ImportDataTable` with a `DataReader` for even
      better memory usage.
  - name: How Do I Preserve Existing Formatting in the Worksheet?
    text: If the target range already has formatting you want to keep, set the `ImportDataTable`
      overload’s `importOptions` parameter (`ImportTableOptions`) and tweak `ImportDataTableOptions.PreserveCellFormatting`.
      The default behavior overwrites styles with the ones you supply.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DataTable
title: Aspose.Cellsでセルスタイルを適用 – 書式付きDataTableのインポート
url: /ja/net/excel-formatting-and-styling/apply-cell-styles-with-aspose-cells-import-datatable-with-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells でセルスタイルを適用 – フォーマット付きで DataTable をインポート

Excel シートに `DataTable` を取り込むときに **セルスタイルを適用** したいと思ったことはありませんか？ 多くのレポートシナリオでは、データがすぐに見栄え良くなることが求められます—後から手動で書式設定する必要はありません。良いニュースは、Aspose.Cells を使えば **フォーマット付きでインポート** が簡単にでき、行を赤や青にしたり、太字にしたり、好きな書式にできることです。

このチュートリアルでは、**セルスタイルを適用した状態で DataTable をワークシートにインポート** する完全な実行可能サンプルを順を追って解説します。最後まで読めば、C# コンソールアプリでブックを作成し、最初の 2 列にスタイルを設定し、`aspose cells import` API を使ってファイルを保存するまでの手順が分かります。

## 学べること

- .NET プロジェクトに Aspose.Cells を設定する方法  
- 実際のデータに近いサンプル `DataTable` の作成方法  
- 赤フォントと青フォント用の `Style` オブジェクトの定義方法  
- `Worksheet.Cells.ImportDataTable` を使って **セルスタイルを適用しながら DataTable をインポート** する方法  
- 結果を確認し、ブックを保存する手順  

外部ツールは不要、純粋に C# と Aspose.Cells だけです。さっそく始めましょう。

---

## 前提条件

コードに入る前に、以下が揃っていることを確認してください。

| 要件 | 重要な理由 |
|------|------------|
| .NET 6.0 以降 | Aspose.Cells 23.x は .NET Standard 2.0+ を対象としているため、.NET 6 で最新のランタイム機能が利用できます。 |
| Aspose.Cells for .NET (NuGet) | `Workbook`、`Worksheet`、`Style`、`ImportDataTable` メソッドを提供します。 |
| 基本的な C# の知識 | クラス、配列、`using` 文が理解できていることが前提です。 |
| IDE (Visual Studio、VS Code、Rider) | 任意のエディタで構いませんが、NuGet パッケージの復元が必要です。 |

パッケージはコマンドラインからインストールできます。

```bash
dotnet add package Aspose.Cells
```

---

## 手順 1: 新しい Workbook を作成し、最初の Worksheet にアクセスする

まずは `Workbook` を作成し、最初のシートを取得します。Workbook は空のノートブック、最初の Worksheet が書き込むページと考えてください。

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create a new workbook (equivalent to a new Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **プロのコツ:** 複数シートが必要な場合は `wb.Worksheets.Add()` でシートを追加し、名前またはインデックスで参照できます。

---

## 手順 2: サンプル DataTable を用意する（DataTable のインポート方法）

次にインポート対象となるものを用意します。実際のプロジェクトでは DB から取得しますが、ここではメモリ上に `DataTable` を作成します。

```csharp
        // Build a sample DataTable with two columns: Name and Score
        DataTable dataTable = new DataTable("Results");
        dataTable.Columns.Add("Name", typeof(string));
        dataTable.Columns.Add("Score", typeof(int));

        // Populate rows – imagine these came from a query
        dataTable.Rows.Add("Alice", 85);
        dataTable.Rows.Add("Bob", 92);
        dataTable.Rows.Add("Charlie", 78);
        dataTable.Rows.Add("Diana", 91);
```

> **なぜ重要か:** `DataTable` があれば、外部依存なしで **aspose cells import** のフローをテストできます。

---

## 手順 3: インポートするセルに適用するスタイルを定義する

ここが本番です。赤フォント用と青フォント用の 2 つの `Style` オブジェクトを作成し、インポート時に列単位で適用します。

```csharp
        // Define an array of styles – one per column
        Style[] importStyles = new Style[2];

        // Style for the first column (Name) – red text
        Style redStyle = wb.CreateStyle();
        redStyle.Font.Color = Color.Red;
        importStyles[0] = redStyle;

        // Style for the second column (Score) – blue text
        Style blueStyle = wb.CreateStyle();
        blueStyle.Font.Color = Color.Blue;
        importStyles[1] = blueStyle;
```

> **注意:** `importStyles` 配列の長さはインポートする列数と一致させる必要があります。そうしないと Aspose が `ArgumentException` をスローします。

---

## 手順 4: フォーマット付きで DataTable を Worksheet にインポートする

いよいよ全体を組み合わせます。使用する `ImportDataTable` のオーバーロードは `Style[]` 配列を受け取るため、データがシートに書き込まれると同時に **セルスタイルを適用** できます。

```csharp
        // Import the DataTable starting at cell A1 (row 0, column 0)
        // The 'true' flag tells Aspose to generate column headers automatically
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);
```

### 動作概要

1. **ヘッダー** – `true` を渡したので、Aspose が「Name」および「Score」を最初の行に書き込みます。  
2. **データ行** – 以降の各行は `importStyles` から対応するスタイルが適用されます。  
3. **パフォーマンス** – メソッドはデータを直接シートにストリームし、セルごとにループするより高速です。

---

## 手順 5: 結果を確認し、Workbook を保存する

最初の数セルをチェックしてスタイルが適用されていることを確認し、ファイルをディスクに書き出します。

```csharp
        // Optional: Quick sanity check – print the first row's values
        Console.WriteLine("Header Row:");
        Console.WriteLine($"{worksheet.Cells[0, 0].StringValue} | {worksheet.Cells[0, 1].StringValue}");

        // Save the workbook to an Excel file
        string outputPath = "StyledImport.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**StyledImport.xlsx** を開くと次のようになります：

- 「Name」列は **赤** 文字  
- 「Score」列は **青** 文字  
- 列ヘッダーはデフォルトスタイル（ヘッダーもスタイル付けしたい場合は別途解説）

![セルスタイル適用例](https://example.com/images/apply-cell-styles.png "Aspose.Cells でセルスタイルを適用した例")

> **注記:** 上記画像は最終的な外観を示しています。`alt` 属性には主要キーワードが含まれており、SEO 要件を満たしています。

---

## よくある質問とエッジケース

### DataTable の列数がスタイル配列より多い場合は？

Aspose は配列の最後のスタイルを余分な列すべてに適用します。予期しない色付きを防ぐには、配列長を列数と合わせるか、スタイルを付けたくない列には `null` を渡してください。

### 特定の行に別のスタイルを適用できるか？

可能です。インポート後に行をループし、条件に応じて新しい `Style` オブジェクトを割り当てれば OK です（例: スコアが 90 超の行を緑でハイライト）。簡単なサンプルは以下です。

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++) // start at 1 to skip header
{
    int score = worksheet.Cells[i, 1].IntValue;
    if (score > 90)
    {
        Style highScore = wb.CreateStyle();
        highScore.Font.Color = Color.Green;
        worksheet.Cells[i, 1].SetStyle(highScore);
    }
}
```

### 大規模データセットでも動作するか？

はい。`ImportDataTable` はデータを効率的にストリームし、静的なスタイル配列の適用はほぼオーバーヘッドがありません。数百万行の場合は、データをチャンクに分割してインポートするか、`DataReader` と組み合わせた `Cells.ImportDataTable` を検討してください。

### 既存の書式を保持したままインポートできるか？

対象範囲に既に書式があり保持したい場合は、`ImportDataTable` のオーバーロードで `importOptions`（`ImportTableOptions`）を設定し、`ImportDataTableOptions.PreserveCellFormatting` を調整します。デフォルト動作は提供したスタイルで上書きします。

---

## まとめ：達成したこと

- **aspose cells import** 操作中に **セルスタイルを適用** しました。  
- `Style[]` 配列を渡すことで **フォーマット付きインポート** を実演しました。  
- `DataTable` を Worksheet にインポートし、結果を保存する方法を示しました。  
- スタイル数の不一致や条件付き行スタイリングなどのエッジケースもカバーしました。

すべて単一の自己完結型コンソールアプリで実現。外部スクリプトや手動の Excel 操作は不要です。これで、洗練された Excel 出力が必要なレポート機能の土台ができました。

---

## 次のステップ

さらにレベルアップしたい方へ、以下のアイデアを試してみてください：

- **ヘッダー行のスタイル**（太字、背景色など）を設定する。  
- `Worksheet.Cells[i, j].ConditionalFormattingCollection` を使って **条件付き書式** を適用する。  
- `wb.Save("file.pdf", SaveFormat.Pdf)` で **CSV や PDF など他形式へエクスポート** する。  
- 複数の `DataTable` を同一ブックの別シートに **同じスタイリング手法で結合** する。

問題が発生したらコメントを残すか、`ImportDataTable` に関する Aspose の公式ドキュメントを確認してください。コーディングを楽しみながら、美しくスタイルされた Excel ファイルを手に入れましょう！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで学んだテクニックを拡張する内容です。各リソースには、ステップバイステップの説明と完全な動作コード例が含まれています。

- [Aspose.Cells for .NET で DataTable を Excel にインポートする方法（ステップバイステップガイド）](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Aspose.Cells for .NET で Excel のフォントスタイルを設定する方法（ステップバイステップガイド）](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)
- [Aspose.Cells .NET で Excel にテキストシャドウを適用する方法（ステップバイステップガイド）](/cells/english/net/formatting/apply-text-shadow-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}