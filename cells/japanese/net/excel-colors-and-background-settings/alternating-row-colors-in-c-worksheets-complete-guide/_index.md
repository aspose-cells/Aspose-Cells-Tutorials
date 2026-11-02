---
category: general
date: 2026-05-30
description: C# のワークシートで交互に行の色を付ける方法、セルの背景を単色塗りつぶしで設定する方法、そしてワークシートのセルスタイルを簡単にカスタマイズする方法を学びましょう。
draft: false
keywords:
- alternating row colors
- set cell background
- solid fill pattern
- add background color
- worksheet cell style
language: ja
og_description: C# のワークシートで交互に行の色を付けるのが簡単に。セルの背景設定、単色塗りつぶしパターンの使用、そしてワークシートのセルスタイルをマスターしましょう。
og_title: C# ワークシートの交互行カラー – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  headline: Alternating Row Colors in C# Worksheets – Complete Guide
  type: TechArticle
- description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  name: Alternating Row Colors in C# Worksheets – Complete Guide
  steps:
  - name: Why Use a **Solid Fill Pattern**?
    text: The `Pattern` property tells the engine how to render the color. A `Solid`
      fill guarantees that the entire cell background is painted, eliminating any
      faint gridlines that might otherwise show through. This is the most common way
      to **set cell background** when you want a clean look.
  - name: Change the Colors
    text: 'If your brand uses different hues, just replace `Color.LightYellow` and
      `Color.LightCyan` with any `System.Drawing.Color` you prefer. For example:'
  - name: Use a Different **Background Type**
    text: While `BackgroundType.Solid` is the most common, you can experiment with
      `BackgroundType.Gray125`, `BackgroundType.Horizontal`, or any pattern that the
      library supports. This changes the visual texture while still **adding background
      color**.
  - name: Apply a **Worksheet Cell Style** to Specific Columns
    text: 'Sometimes you only want the alternating effect on data columns, leaving
      the first column (e.g., IDs) untouched. Create a separate style for that column
      and assign it after the import:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: C# ワークシートで交互に行の色を設定する完全ガイド
url: /ja/net/excel-colors-and-background-settings/alternating-row-colors-in-c-worksheets-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ワークシートで交互の行色 – 完全ガイド

Excel のエクスポートを **交互の行色** で洗練されたものにしたいと思ったことはありませんか？ あなたは一人ではありません—開発者は常に、何百万行ものコードを書かずに行に *背景色を追加* する方法を尋ねています。  

このチュートリアルでは、各行の **セルの背景を設定** し、**単色塗りつぶしパターン** を適用し、**ワークシートセルスタイル** を制御するシンプルな方法を順を追って解説します。結果は読みやすく、視覚的にも魅力的になります。

## 学べること

- `DataTable`（または任意の表形式データ）にデータを取得する。  
- 2 色を交互に使用する `Style` オブジェクトの配列を作成する。  
- それらのスタイルを適用しながら `DataTable` をワークシートにインポートする。  
- 出力を確認し、必要に応じて色やパターンを調整する。  

.NET 環境とスプレッドシートライブラリ（例では **Aspose.Cells** を使用）さえあれば、外部ツールは不要です。最後には、任意のレポートパイプラインに組み込める再利用可能なメソッドが手に入ります。

---

## ステップ 1: ソースデータを `DataTable` として取得する

まずはデータがなければスタイルを適用できません。以下はサンプル行で `DataTable` を構築する小さなヘルパーです。実際のプロジェクトでは、データベース呼び出しや CSV パーサーに置き換えてください。

```csharp
using System;
using System.Data;

static DataTable GetData()
{
    // Create a simple table with three columns
    DataTable table = new DataTable("Report");
    table.Columns.Add("ID", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with dummy rows
    for (int i = 1; i <= 10; i++)
    {
        table.Rows.Add(i, $"Item {i}", Math.Round(new Random().NextDouble() * 100, 2));
    }

    return table;
}
```

> **Why this matters:** `DataTable` にデータがあると、ワークシートエンジンが *インポート* を一度の呼び出しで行い、列名とデータ型を自動的に保持します。

## ステップ 2: **交互の行色** スタイルを作成する

ここでは `Style` オブジェクトの配列を生成します—行ごとに 1 つずつ—偶数行には淡い黄色、奇数行には柔らかなシアンを付けます。これが **交互の行色** テクニックの核心です。

```csharp
using Aspose.Cells;
using System.Drawing;

// Assume workbook and worksheet are already instantiated
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Retrieve data
DataTable dataTable = GetData();

// Prepare an array of styles – one for each row in the table
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style for the current row
    rowStyles[i] = workbook.CreateStyle();

    // **Add background color**: LightYellow for even rows, LightCyan for odd rows
    rowStyles[i].ForegroundColor = (i % 2 == 0)
        ? Color.LightYellow
        : Color.LightCyan;

    // **Set cell background** using a **solid fill pattern**
    rowStyles[i].Pattern = BackgroundType.Solid;

    // Optional: you could also set font color, borders, etc., here
}
```

### **Solid Fill Pattern** を使用する理由

`Pattern` プロパティはエンジンに色の描画方法を指示します。`Solid` 塗りつぶしはセル全体の背景を確実に塗り、薄いグリッドラインが透けて見えるのを防ぎます。クリーンな外観を求める際に **セルの背景を設定** する最も一般的な方法です。

## ステップ 3: 用意したスタイルで `DataTable` をインポートする

スタイル配列が準備できたら、インポート呼び出しはワンライナーになります。Aspose.Cells が各行に対応するスタイルを自動的に適用します。

```csharp
// Import the DataTable into the worksheet, applying the prepared styles
worksheet.Cells.ImportDataTable(
    dataTable,                     // source
    true,                          // include column names
    0,                             // start row (0‑based)
    0,                             // start column (0‑based)
    rowStyles);                    // array of styles
```

> **What happens under the hood?**  
> ライブラリは各行を走査し、値をセルにコピーした後、`rowStyles` から一致する `Style` を適用します。既に **単色塗りつぶしパターン** を定義しているため、行内のすべてのセルが同じ背景色を継承し、完璧な **交互の行色** が実現します。

## ステップ 4: ワークブックを保存して結果を確認する

簡単に保存すれば、Excel（または互換ビューア）でファイルを開き、効果を確認できます。

```csharp
// Save to disk – you can change the format to .xlsx, .xls, .csv, etc.
workbook.Save("AlternatingRowsReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved. Open 'AlternatingRowsReport.xlsx' to see the result.");
```

ファイルを開くと、行 1、 3、 5… が淡い黄色、行 2、 4、 6… が淡いシアンになります。列ヘッダーは白のままで、データが際立ちます。

![交互の行色を示すワークシート](/images/alternating-row-colors.png "交互の行色があるワークシートのスクリーンショット")

*画像の代替テキスト:* **alternating row colors** のスクリーンショットで、各行の背景が淡い黄色と淡いシアンで交互に変わります。

## ステップ 5: さらにカスタマイズ (オプション)

### 色を変更する

ブランドの配色が異なる場合は、`Color.LightYellow` と `Color.LightCyan` を任意の `System.Drawing.Color` に置き換えるだけです。例:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.FromArgb(255, 235, 205) // Peach
                                            : Color.FromArgb(205, 235, 255); // Soft blue
```

### 異なる **Background Type** を使用する

`BackgroundType.Solid` が最も一般的ですが、`BackgroundType.Gray125`、`BackgroundType.Horizontal`、またはライブラリがサポートする任意のパターンを試すことができます。これにより視覚的な質感が変わりますが、**背景色の追加** は引き続き可能です。

### 特定の列に **Worksheet Cell Style** を適用する

データ列だけに交互効果を適用し、最初の列（例: ID）をそのままにしたい場合があります。その列用に別のスタイルを作成し、インポート後に割り当てます:

```csharp
Style idStyle = workbook.CreateStyle();
idStyle.ForegroundColor = Color.White;
idStyle.Pattern = BackgroundType.Solid;

// Apply to the first column (A)
for (int row = 0; row < dataTable.Rows.Count + 1; row++) // +1 for header
{
    worksheet.Cells[row, 0].SetStyle(idStyle);
}
```

---

## 結論

これで C# ワークシートにおける **交互の行色** の完全で再利用可能なソリューションが手に入りました。`Style` オブジェクトの配列を構築し、**単色塗りつぶしパターン** で **セルの背景を設定**、`DataTable` を一度の呼び出しでインポートすれば、最小限のコードでプロフェッショナルなレポートが作成できます。  

ここからは次のような応用が考えられます：

- ヘッダー行に **背景色を追加** して強調する。  
- 条件付き書式と組み合わせて動的な視覚的ヒントを提供する。  
- フォント、罫線、数値書式など、他の **worksheet cell style** プロパティを探求する。

次回のエクスポート処理でぜひ試してみてください—ユーザーはよりクリーンで読みやすいスプレッドシートに感謝するでしょう。ハッピーコーディング！

## 次に学ぶべきこと

- [Worksheet の行高さを設定する (Aspose.Cells for .NET)](/cells/english/net/size-and-spacing-customization/setting-height-of-all-rows-in-worksheet/)
- [Aspose.Cells for .NET を使用して Excel セル名を行・列インデックスに変換する](/cells/english/net/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-dotnet/)
- [Aspose.Cells .NET で Excel のワークシートタブ色を設定する – 包括的ガイド](/cells/english/net/worksheet-management/set-worksheet-tab-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}