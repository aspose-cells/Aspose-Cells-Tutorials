---
category: general
date: 2026-03-01
description: C# を使用して書式付きデータを Excel にインポートします。DataTable を Excel に取り込み、セルに背景色を付ける方法を数ステップで学びましょう。
draft: false
keywords:
- import data with formatting
- how to import datatable into excel
- add background color to excel cells
language: ja
og_description: C# を使用して書式付きデータを Excel にインポートする。DataTable をインポートし、セルに背景色を付ける方法をステップバイステップで解説したガイド。
og_title: 書式設定されたデータをExcelにインポート – C#ガイド
tags:
- C#
- Excel
- DataTable
- Formatting
title: C# を使用して書式付きデータを Excel にインポートする
url: /ja/net/excel-data-import-export/import-data-with-formatting-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で書式付きデータを Excel にインポートする

**書式付きデータ**を Excel ブックにインポートしたいのに、平坦で退屈なシートになってしまうことはありませんか？ あなたは一人ではありません。多くの開発者が、デフォルトのインポートがソースデータで設定した色やスタイルをすべて削除してしまう壁にぶつかります。

このチュートリアルでは、**DataTable を Excel にインポート**し、同時に **Excel のセルに背景色を付与**する、完全に実行可能なソリューションを順を追って解説します。追加のポストプロセッシングは不要です—スプレッドシートは箱から出した瞬間から希望通りの見た目になります。

## 学べること

- `DataTable` にデータを取得する方法  
- 背景色を保持する `Style` オブジェクト配列の定義方法  
- そのスタイルを使って `ImportDataTable` を呼び出し、書式付きインポートを実現する方法  
- コンソールアプリにそのまま貼り付けてすぐに結果を確認できる、完全な実行例  
- 実務で役立つヒント、落とし穴、バリエーション

### 前提条件

- .NET 6.0 以降（コードは .NET Framework 4.6+ でも動作します）  
- **GemBox.Spreadsheet** ライブラリ（デモには無料版で十分です）  
- C# と Excel の基本的な知識

*なぜ GemBox か？* それは、書式付きデータをインポートするために必要な `ImportDataTable` メソッドが、スタイル配列を受け取るシングルラインで提供されているからです。

---

## 手順 1: プロジェクトを作成し GemBox.Spreadsheet を追加

まずは新しいコンソールアプリを作成します：

```bash
dotnet new console -n ExcelImportDemo
cd ExcelImportDemo
dotnet add package GemBox.Spreadsheet
```

> **プロのコツ:** 無料版はシートあたり 150 k セルまで使用可能です。デモには十分な上限です。上限に達した場合はアップグレードするか EPPlus に切り替えてください。ただし API が若干異なります。

## 手順 2: `DataTable` としてソースデータを取得

最初に必要なのは、通常はデータベースから取得するような `DataTable` です。以下はメモリ上で作成する小さなヘルパーです：

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register the free license (remove for paid version).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve the source data as a DataTable.
        DataTable dataTable = GetSampleData();

        // Remaining steps will follow...
    }

    /// <summary>
    /// Generates a sample DataTable with three columns and five rows.
    /// In a real app you’d replace this with a DB call.
    /// </summary>
    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

**重要ポイント:** データ取得を独立したメソッドに分離することで、SQL、CSV、Web サービスなど任意のソースに差し替えてもインポートロジックを触る必要がありません。これによりコードがすっきりし、チュートリアルの **how to import datatable into excel** が再利用可能になります。

## 手順 3: 適用したいスタイルを定義

ここからが楽しいパートです。`Style` オブジェクトの配列を作成し、各オブジェクトに固有の `ForegroundColor` を設定します。GemBox では `BackgroundPatternColor`（セルの塗りつぶし）と `ForegroundColor`（文字色）を設定できます。このデモでは最初の 2 列に異なる色を付けます。

```csharp
        // 2️⃣ Define the styles to apply to the imported cells.
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // Column 0 – Light blue fill
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Column 1 – Light green fill
            // No style for column 2 – it will keep the default look.
        };
```

**解説:**  
- `Style` オブジェクトは軽量なコンテナです。セルごとに新しいインスタンスを作る必要はありません。  
- 配列の順序を列の順序と合わせるだけで、GemBox がインポート時に自動的に対応するスタイルを適用します。  
- これが **import data with formatting** の鍵です—書式はデータと一緒に転送され、後から付与されるわけではありません。

## 手順 4: スタイル付きで `DataTable` をワークシートにインポート

データとスタイルが揃ったら、ワークブックを作成し、最初のワークシートを取得して `ImportDataTable` を呼び出します。メソッドシグネチャは次の通りです：

```csharp
public void ImportDataTable(
    DataTable dataTable,
    bool includeColumnNames,
    int startRow,
    int startColumn,
    Style[] columnStyles = null);
```

実際の使用例は以下です：

```csharp
        // 3️⃣ Create a new workbook and import the DataTable.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        // Import, include column headers, start at A1 (0,0), apply our styles.
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the file to disk.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Excel file 'Report.xlsx' created with formatted data.");
```

**内部で何が起きているか:**  
- `true` は列名を最初の行に書き込む指示です。  
- `0, 0` はインポート開始位置をセル A1 に設定します。  
- `importStyles` が各列に対して先ほど定義した色を紐付けます。

*Report.xlsx* を開くと、**ID** 列が薄い青、**Name** 列が薄い緑、**Score** 列はそのままという結果が確認できます。これが **import data with formatting** をワンコールで実現した例です。

## 手順 5: 結果を確認（期待出力）

生成された `Report.xlsx` を開くと、次のようになっているはずです：

| ID (light blue) | Name (light green) | Score |
|-----------------|--------------------|-------|
| 1               | Alice              | 93.5 |
| 2               | Bob                | 78.0 |
| 3               | Charlie            | 85.2 |
| 4               | Diana              | 91.3 |
| 5               | Ethan              | 67.8 |

- **ID** 列のセルは薄い青色の背景です。  
- **Name** 列のセルは薄い緑色の背景です。  
- **Score** 列はデフォルトの白背景のままです。

この視覚的なヒントにより、レポートは瞬時にスキャンしやすくなり、ユーザー体験が大幅に向上します。

![Excel sheet showing import data with formatting – ID column light blue, Name column light green](excel-screenshot.png "import data with formatting example")

*画像の alt テキストは SEO 用の主要キーワードを含んでいます。*

---

## よくある質問とエッジケース

### 背景色以外の書式も適用できますか？

もちろんです。`Style` ではフォント、罫線、数値書式、さらには条件付き書式も設定できます。例えば、90 点以上のスコアを太字かつ赤色にしたい場合は次のようにします：

```csharp
Style highScoreStyle = new Style()
{
    FontColor = Color.Red,
    FontBold = true
};
worksheet.Cells["C2:C6"].ConditionalFormatting.Add(
    ConditionalFormattingCondition.GreaterThan, "90", highScoreStyle);
```

### DataTable の列数がスタイル配列より多い場合は？

GemBox は配列に対応するエントリがある列にだけスタイルを適用し、余剰の列はデフォルトスタイルのままになります。エラーは発生しません。

### 大規模データセットでも動作しますか？

はい。ただし無料版のセル上限（150 k セル）に注意してください。非常に大きなレポートの場合は有料ライセンスを検討するか、`worksheet.Cells[row, col].Value = …` で行ごとにストリーミングする方法もあります—ただしワンライナーの便利さは失われます。

### 既存の Excel テンプレートから書式付きでインポートしたい場合は？

まずテンプレートワークブックをロードします：

```csharp
var template = ExcelFile.Load("Template.xlsx");
var targetSheet = template.Worksheets[0];
targetSheet.Cells.ImportDataTable(dataTable, true, 5, 2, importStyles);
template.Save("FilledReport.xlsx");
```

これによりヘッダーのロゴやフッター、既存の書式を保持しつつ、動的部分だけ **import data with formatting** できます。

---

## 完全動作サンプル（コピー＆ペースト可能）

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register free license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Get the source data.
        DataTable dataTable = GetSampleData();

        // 2️⃣ Define column styles (background colors).
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // ID column
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Name column
            // Score column gets default style.
        };

        // 3️⃣ Create workbook and import with styles.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the result.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Report.xlsx created – import data with formatting complete.");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

プログラムを実行（`dotnet run`）し、生成された *Report.xlsx* を開くと、色が即座に適用されているのが確認できます。

---

## 結論

これで、書式付きデータを Excel にインポートするための堅牢な手法を習得しました。  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}