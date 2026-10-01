---
category: general
date: 2026-10-01
description: C#でExcelの交互列カラーを設定 – DataTableからExcelファイルを作成し、セルの背景色を設定し、スタイル付き列でDataTableをExcelにインポートする方法を学ぶ。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- alternating column colors excel
- set cell background color c#
- create excel file from datatable c#
- import datatable to excel
language: ja
lastmod: 2026-10-01
og_description: 交互に列の色を設定できるExcelが簡単に作れます。このガイドに従って DataTable から Excel ファイルを作成し、C#
  でセルの背景色を設定し、スタイル付き列で DataTable を Excel にインポートしましょう。
og_image_alt: Screenshot of an Excel sheet showing alternating column colors applied
  by C# code
og_title: C#でExcelの列に交互の色を付ける – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: alternating column colors excel using C# – learn to create an Excel
    file from a DataTable, set cell background color c#, and import datatable to excel
    with styled columns.
  headline: How to add alternating column colors in Excel using C#
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: C# を使って Excel の列に交互に色を付ける方法
url: /ja/net/excel-colors-and-background-settings/how-to-add-alternating-column-colors-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# を使用して Excel で交互に列の色を付ける方法

アプリケーションから生成されるレポートで **alternating column colors excel** が必要な場合、このガイドでは完全なソリューションを示します。`DataTable` から Excel ファイルを作成し、C# スタイルでセルの背景色を設定し、各列に異なるスタイルを適用しながら **import datatable to excel** を行う方法が分かります。

このチュートリアルでは、必要な NuGet パッケージ、実行可能な完全サンプルコード、各ステップが重要な理由の解説をすべて網羅しています。最後まで実行すれば、Microsoft Excel で直接開くことができるスタイル付きワークブックが手に入ります。

## 前提条件

開始する前に、以下がインストールされていることを確認してください。

* .NET 6.0（またはそれ以降）SDK がインストール済み  
* Visual Studio 2022（または C# 対応の任意の IDE）  
* **Aspose.Cells for .NET** ライブラリ – 以下でインストール  

```bash
dotnet add package Aspose.Cells
```

Aspose.Cells は、サンプルで使用する `Workbook`、`Worksheet`、`Style`、`BackgroundType` クラスを提供します。

## ステップ 1: ソースデータを `DataTable` として取得する

最初のタスクは、エクスポートしたいデータを取得することです。実際のプロジェクトでは、データベースクエリ、API 呼び出し、または任意のインメモリコレクションから `DataTable` を作成することが多いでしょう。

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetData()
{
    // Create a sample DataTable with three columns and five rows
    DataTable table = new DataTable("Sample");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    for (int i = 1; i <= 5; i++)
    {
        table.Rows.Add(i, $"Student {i}", 60 + i * 5);
    }
    return table;
}
```

**なぜ重要か:**  
`DataTable` は Excel のワークシートにきれいにマッピングできる汎用コンテナです。`DataTable` を使用することで、**create excel file from datatable c#** をカスタムループを書かずに実現できます。

## ステップ 2: 新しいワークブックを作成し、最初のワークシートを取得する

```csharp
// Initialize a new workbook – this represents the Excel file
Workbook workbook = new Workbook();

// The first worksheet is created by default
Worksheet worksheet = workbook.Worksheets[0];
```

**説明:**  
`Workbook` がルートオブジェクトで、`Worksheets[0]` がデータを配置するデフォルトシートを指します。

## ステップ 3: 各列に固有のスタイルを準備する（交互の背景色）

**alternating column colors excel** を実現するため、各列ごとに `Style` を生成し、2 つの色のうちどちらかをライトな背景色として割り当てます。

```csharp
// Determine how many columns we have
int columnCount = dataTable.Columns.Count;
Style[] columnStyles = new Style[columnCount];

// Create a style for each column
for (int i = 0; i < columnCount; i++)
{
    // Create a fresh style instance
    Style style = workbook.CreateStyle();

    // Alternate between LightYellow and LightCyan
    style.ForegroundColor = (i % 2 == 0)
        ? System.Drawing.Color.LightYellow
        : System.Drawing.Color.LightCyan;

    // Use a solid fill pattern
    style.Pattern = BackgroundType.Solid;

    columnStyles[i] = style;
}
```

**ループを使用する理由:**  
ループを使うことで、**set cell background color c#** が列数の増減に関係なく一貫して適用されます。これにより、動的レポートでも堅牢な解決策となります。

## ステップ 4: `DataTable` をワークシートにインポートし、列スタイルを適用する

Aspose.Cells は `DataTable` を直接インポートでき、スタイル配列を渡すことで各列に色を付けられます。

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// The second argument (true) tells the API to add column headers
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**内部で何が起きているか:**  
`ImportDataTable` はヘッダー行を書き込み、その後データ行を順に書き込みます。`columnStyles` を渡したため、対象列のすべてのセルが対応するスタイルを受け取り、交互の色が実現されます。

## ステップ 5: スタイル付きワークブックをファイルに保存する

```csharp
// Choose an output path – adjust as needed for your environment
string outputPath = @"C:\Temp\StyledTable.xlsx";
workbook.Save(outputPath);

Console.WriteLine($"Workbook saved to {outputPath}");
```

*StyledTable.xlsx* を Excel で開くと、各列が交互にシェーディングされ、テーブルが見やすくなります。

## 完全な実行可能サンプル

以下に、コピーして貼り付け、すぐに実行できる自己完結型プログラムを示します。

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Get the source data
        DataTable dataTable = GetData();

        // Step 2: Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Build alternating column styles
        int columnCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++)
        {
            Style style = workbook.CreateStyle();
            style.ForegroundColor = (i % 2 == 0)
                ? System.Drawing.Color.LightYellow
                : System.Drawing.Color.LightCyan;
            style.Pattern = BackgroundType.Solid;
            columnStyles[i] = style;
        }

        // Step 4: Import DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // Step 5: Save the file
        string outputPath = @"C:\Temp\StyledTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetData()
    {
        DataTable table = new DataTable("Students");
        table.Columns.Add("Id", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        for (int i = 1; i <= 5; i++)
        {
            table.Rows.Add(i, $"Student {i}", 60 + i * 5);
        }
        return table;
    }
}
```

### 期待される出力

* `C:\Temp\` に **StyledTable.xlsx** という名前のファイルが作成されます。  
* ワークシートには 3 列（`Id`、`Name`、`Score`）が交互の背景色で表示されます：列 1 と 3 が *LightYellow*、列 2 が *LightCyan*。  
* `DataTable` のすべての行がヘッダー行の下に表示されます。

## よくある質問とエッジケース

| Question | Answer |
|----------|--------|
| *Can I use other colors?* | Yes. Replace `System.Drawing.Color.LightYellow` and `LightCyan` with any `System.Drawing.Color` value. |
| *What if the DataTable has many columns?* | The loop automatically creates a style for each column, so the pattern scales without code changes. |
| *Do I need to dispose of the workbook?* | Aspose.Cells implements `IDisposable`. If you wrap the `Workbook` in a `using` block, resources are released promptly. |
| *How to apply the same alternating colors to rows instead of columns?* | Create a `Style[]` for rows and call `worksheet.Cells.ImportDataTable(..., rowStyles)` – Aspose.Cells overloads support both. |
| *Can I write the file directly to a stream (e.g., for a web API)?* | Yes. Use `workbook.Save(stream, SaveFormat.Xlsx);` instead of a file path. |

## 現場からのヒント

* **Pro tip:** Cache the style objects if you generate many worksheets in a single run – creating a style is relatively cheap, but reusing them reduces memory churn.  
* **Watch out for:** When using `System.Drawing.Color` on non‑Windows platforms, add the `System.Drawing.Common` NuGet package and ensure the runtime supports GDI+.

## 結論

これで **alternating column colors excel** を実現する方法が分かりました。`DataTable` から Excel ファイルを作成し、Aspose.Cells でセルの背景色を設定し、**import datatable to excel** と同時に列ごとのスタイル配列を適用する手順です。このアプローチは高速で保守性が高く、データ量に関係なく機能します。

### 次のステップ

* **set cell background color c#** を使った条件付き書式（例: 低スコアのハイライト）を調査。  
* この手法と **create excel file from datatable c#** を組み合わせて、マルチシートレポートを生成。  
* 同じワークブックに視覚的サマリーを追加するため、Aspose.Cells のチャート API を検討。

色、ファイル形式、データソースはプロジェクトの要件に合わせて自由にカスタマイズしてください。Happy coding!

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示したテクニックを基にした、密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得したり、代替実装アプローチを自分のプロジェクトで試したりするのに役立ちます。

- [Set Column Background in Excel with C# – Complete Guide](/cells/english/net/excel-colors-and-background-settings/set-column-background-in-excel-with-c-complete-guide/)
- [Add background color excel – Alternating Row Styles in C#](/cells/english/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/)
- [Create Workbook C# – Import DataTable to Excel with Styles](/cells/english/net/excel-data-import-export/create-workbook-c-import-datatable-to-excel-with-styles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}