---
category: general
date: 2026-07-03
description: C# を使用して DataTable を Excel にインポートする際に、交互に行の色を適用します。C# の DataTable を Excel
  にエクスポートする方法、スタイル付きテーブル Excel を保存する方法、そしてブックの書式設定を保持する方法を学びましょう。
draft: false
keywords:
- apply alternating row colors
- import datatable to excel
- export c# datatable to excel
- save styled table excel
- save workbook with formatting
language: ja
og_description: C# を使用して Excel で交互の行色を適用する。このチュートリアルでは、DataTable を Excel にインポートし、C#
  の DataTable を Excel にエクスポートし、書式設定されたブックを保存する方法を示します。
og_title: C#でExcelの交互行の色を設定する – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  headline: Apply Alternating Row Colors in Excel with C# – Complete Guide
  type: TechArticle
- description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  name: Apply Alternating Row Colors in Excel with C# – Complete Guide
  steps:
  - name: Expected Output
    text: '| ID | Name | Department | HireDate | |----|---------|------------|------------|
      | 1 | Alice | Finance | 15‑01‑2020 | | 2 | Bob | HR | 23‑06‑2019 | | 3 | Charlie
      | IT | 10‑03‑2021 | | 4 | Diana | Marketing | 05‑11‑2018 |'
  - name: What if my DataTable has thousands of rows?
    text: The `ImportDataTable` method streams data efficiently, but you might hit
      memory limits on very large tables. In such cases, consider splitting the export
      into multiple worksheets or using the `ImportDataTable` overload that lets you
      specify a start row and column.
  - name: Can I use custom colors instead of the built‑in ones?
    text: Absolutely. Just replace the `ForegroundColor` assignments in `styleWhite`
      and `styleGray` with any `System.Drawing.Color` you prefer—think pastel blues
      or corporate brand colors.
  - name: How do I ensure the alternating style works when the user adds rows later?
    text: If users edit the file manually, the original style array won’t automatically
      extend. A quick workaround is to convert the range into an Excel Table (`ListObject`)
      after import; Excel then repeats the pattern for new rows.
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataExport
title: C#でExcelの交互行カラーを適用する – 完全ガイド
url: /ja/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel で交互行カラーを C# で適用する – 完全ガイド

C# の `DataTable` を Excel にエクスポートするときに **交互行カラーを適用** したいことはありませんか？ 同じ悩みを持つ開発者は多く、手作業で Excel を整形せずにスプレッドシートをきれいに見せる方法が求められています。 良いニュースは、数行のコードでプログラム的に実現できることです。

このチュートリアルでは **import datatable to excel** の手順を追いながら、**export c# datatable to excel** でスタイル付きテーブルを作成し、最終的に **save styled table excel** して書式を保持する方法を紹介します。 終了時には **save workbook with formatting** がクライアント向けの資料としてすぐに使える状態になります。

## 前提条件

- .NET 6.0 以降（サンプルは .NET 6 を使用していますが、最近のバージョンであればどれでも可）
- Aspose.Cells for .NET（無料トライアルまたはライセンス版） – このライブラリがスタイリングを簡単にします
- `DataTable` ソース（データベース、CSV、またはインメモリコレクションから取得可能）

> **プロのコツ:** Aspose.Cells がまだ無い場合は、`dotnet add package Aspose.Cells` で NuGet から取得できます。

## 手順 1: プロジェクトを作成しデータをロードする

まずコンソールアプリ（または任意の C# プロジェクト）を作成し、必要な `using` 文を追加します。続いてデータを `DataTable` に取り込みます。ここでは簡易的にテーブルをその場で生成します。

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Retrieve the source data as a DataTable
        DataTable sourceTable = GetSampleData();

        // The rest of the steps follow...
    }

    // Helper that creates a dummy DataTable
    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

**ポイント:** `DataTable` が用意できれば、**import datatable to excel** をワンコールで実行でき、セル単位で手動入力する手間が省けます。

## 手順 2: ワークブックを作成し交互行スタイルを定義する

次に新しい `Workbook` をインスタンス化します。**apply alternating row colors** のコツは `ImportTableOptions.StyleArray` にあります。ここでは組み込みの 2 つのスタイル（通常は白と薄いグレー）を使用しますが、後でカスタマイズ可能です。

```csharp
// Step 2: Create a new workbook
Workbook workbook = new Workbook();

// Define two simple styles: white (default) and light gray
Style styleWhite = workbook.Styles[workbook.Styles.Add()];
styleWhite.ForegroundColor = System.Drawing.Color.White;
styleWhite.Pattern = BackgroundType.Solid;

Style styleGray = workbook.Styles[workbook.Styles.Add()];
styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242); // light gray
styleGray.Pattern = BackgroundType.Solid;

// Step 3: Set up ImportTableOptions with the alternating styles
ImportTableOptions importOptions = new ImportTableOptions
{
    // The array alternates between the two styles for each row
    StyleArray = new Style[] { styleWhite, styleGray }
};
```

**解説:** `ImportTableOptions` は Aspose.Cells に対しインポート時の行処理方法を指示します。2 要素の `StyleArray` を渡すことで、ライブラリは奇数行に最初のスタイル、偶数行に 2 番目のスタイルを自動的に適用し、**apply alternating row colors** を実現します。

## 手順 3: DataTable をワークシートへインポート（ヘッダー含む）

ワークブックとスタイルの準備ができたら、**import datatable to excel** を実行します。`ImportDataTable` メソッドが主要な処理を行い、列ヘッダーを書き込み、スタイル配列を尊重し、データをセル A1 から配置します。

```csharp
// Step 4: Import the DataTable into the first worksheet (include column headers)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells.ImportDataTable(sourceTable, true, importOptions);
```

**`true` を第2引数に指定する理由:** このフラグにより列名が最初の行に書き込まれ、プロフェッショナルなレポートに必須のヘッダーが自動的に生成されます。

## 手順 4: テーブルを微調整（任意だが便利）

列幅を自動調整したりフィルタ行を追加したりしたい場合は、以下の数行でテーブルをさらに見栄え良くできます。

```csharp
// Auto‑fit all columns for readability
sheet.AutoFitColumns();

// Add a filter to the header row
sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";
```

これらの調整は交互カラーには影響しませんが、**save styled table excel** ファイル全体のユーザー体験を向上させます。

## 手順 5: 書式を保持したままワークブックを保存

最後にファイルをディスクに書き出します。`Save` メソッドは設定したすべてのスタイルを保持し、交互行の色がそのまま残ります。

```csharp
// Step 5: Save the workbook with the styled table
string outputPath = @"C:\Temp\StyledEmployees.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

`StyledEmployees.xlsx` を開くと、白と薄いグレーが交互に並んだクリーンなテーブルが表示されます。これは多くのユーザーが可読性向上のために頼る視覚的手がかりです。

### 期待される出力

| ID | Name    | Department | HireDate   |
|----|---------|------------|------------|
| 1  | Alice   | Finance    | 15‑01‑2020 |
| 2  | Bob     | HR         | 23‑06‑2019 |
| 3  | Charlie | IT         | 10‑03‑2021 |
| 4  | Diana   | Marketing  | 05‑11‑2018 |

- 行 1, 3 … → 白背景  
- 行 2, 4 … → 薄いグレー背景  

これが **save workbook with formatting** の全工程です。

## よくある質問とエッジケース

### DataTable が数千行ある場合はどうすれば？

`ImportDataTable` はデータを効率的にストリームしますが、非常に大きなテーブルではメモリ制限に達することがあります。その場合はエクスポート先を複数シートに分割するか、開始行・開始列を指定できるオーバーロードを利用してください。

### 組み込みスタイルではなくカスタムカラーを使いたい？

もちろん可能です。`styleWhite` と `styleGray` の `ForegroundColor` 設定を任意の `System.Drawing.Color` に置き換えるだけです。パステルブルーや社内ブランドカラーなど自由に選べます。

```csharp
styleWhite.ForegroundColor = System.Drawing.Color.LightBlue;
styleGray.ForegroundColor = System.Drawing.Color.LightCyan;
```

### ユーザーが後から行を追加したときに交互スタイルを維持するには？

手動でファイルを編集した場合、元のスタイル配列は自動的に拡張されません。対策としてインポート後に範囲を Excel テーブル（`ListObject`）に変換すると、Excel が新しい行にもパターンを適用します。

```csharp
int lastRow = sheet.Cells.MaxDataRow;
int lastCol = sheet.Cells.MaxDataColumn;
string tableRange = $"A1:{CellsHelper.ColumnIndexToName(lastCol)}{lastRow + 1}";
ListObject table = sheet.ListObjects[sheet.ListObjects.Add(tableRange, true)];
```

これで新規行も交互カラーを継承します。

## 完全動作サンプル（全手順を一括で実装）

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve source data
        DataTable sourceTable = GetSampleData();

        // 2️⃣ Create workbook and define alternating styles
        Workbook workbook = new Workbook();

        Style styleWhite = workbook.Styles[workbook.Styles.Add()];
        styleWhite.ForegroundColor = System.Drawing.Color.White;
        styleWhite.Pattern = BackgroundType.Solid;

        Style styleGray = workbook.Styles[workbook.Styles.Add()];
        styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242);
        styleGray.Pattern = BackgroundType.Solid;

        ImportTableOptions importOptions = new ImportTableOptions
        {
            StyleArray = new Style[] { styleWhite, styleGray }
        };

        // 3️⃣ Import DataTable (including headers)
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(sourceTable, true, importOptions);

        // 4️⃣ Optional polish
        sheet.AutoFitColumns();
        sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";

        // 5️⃣ Save the styled workbook
        string outputPath = @"C:\Temp\StyledEmployees.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

プログラムを実行し、生成されたファイルを開くと、手動で書式設定する必要なしに交互行カラーが適用された状態がすぐに確認できます。

## まとめ

本稿では C# で **import datatable to excel** する際に **apply alternating row colors** を実装する方法を示しました。これにより **export c# datatable to excel**、**save styled table excel**、そして **save workbook with formatting** がワンステップで完了し、プロフェッショナルな見た目のファイルが自動的に生成されます。

次のステップは？ 2 つのスタイルを入れ替えてカスタムテーマにしたり、範囲を Excel テーブルに変換してユーザーが並べ替えやフィルタを利用できるようにしたりしてください。さらに `ConditionalFormattingCollection` を活用すれば、より動的な視覚効果も実装可能です。

ご質問や独自の実装例があればぜひ共有してください。

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで扱ったテクニックを応用した関連トピックを網羅しています。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能習得や代替実装アプローチの探求に役立ちます。

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Apply Colors & Backgrounds in Excel using Aspose.Cells for .NET](/cells/english/net/formatting/colors-and-background/)
- [Automate Excel Theme Colors Using Aspose.Cells .NET for Efficient Formatting](/cells/english/net/formatting/automate-excel-theme-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}