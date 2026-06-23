---
category: general
date: 2026-03-30
description: C#で通貨書式設定されたExcelブックを作成します。DataTableのインポート方法、Excelへの数値書式の追加、そして数分で通貨書式の列を適用する方法を学びましょう。
draft: false
keywords:
- create excel workbook c#
- format cells currency
- import datatable to excel
- add number format excel
- apply currency format column
language: ja
og_description: C#でExcelブックを作成し、セルを即座に通貨形式にフォーマットします。このステップバイステップのチュートリアルでは、DataTableをExcelにインポートし、列に数値書式（通貨）を追加する方法を示します。
og_title: C#でExcelブックを作成 – 通貨書式設定ガイド
tags:
- Aspose.Cells
- C#
- Excel automation
title: C#でExcelブックを作成 – 通貨形式を適用し、DataTableをインポート
url: /ja/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel ワークブック C# の作成 – 通貨形式を適用し DataTable をインポート

すでに完成されたレポートのような **Excel ワークブック C#** を作成したことがありますか？たとえばデータベースから売上数字を取得し、価格列を手動で Excel を操作せずにドル表記にしたい、というケースです。心当たりはありませんか？同じ問題に直面する開発者は多いです――Excel エクスポートを自動化し始めたときにこの壁にぶつかります。

このガイドでは、**Excel ワークブック C# を作成し**、`DataTable` をインポートし、**価格列を通貨形式にフォーマット**する、すぐに実行できる完全なソリューションを順を追って解説します。最後には `StyledTable.xlsx` というファイルが生成され、開いたときにきれいにフォーマットされた数値が表示されます。追加のポストプロセスは不要です。

> **学べること**
> - .NET プロジェクトで Aspose.Cells を設定する方法  
> - **import datatable to excel** をスタイル配列と共に実装する方法  
> - 特定の列に対して **add number format excel** を適用する方法  
> - 複数列や異なるロケールに対応する際のポイント  

> **前提条件**  
> - .NET 6+（または .NET Framework 4.6+）がインストール済み  
> - Aspose.Cells for .NET NuGet パッケージ (`Install-Package Aspose.Cells`)  
> - C# と DataTable の基本的な知識  

---

## Step 1: Prepare the DataTable (import datatable to excel)

まずはサンプルデータを用意します。実際のアプリでは DB クエリからこのテーブルにデータを詰め込むことが多いですが、ここではハードコーディングした例でシンプルに示します。

```csharp
using System.Data;

// Create a DataTable with two columns: Product (string) and Price (double)
DataTable dataTable = new DataTable();
dataTable.Columns.Add("Product", typeof(string));
dataTable.Columns.Add("Price", typeof(double));

// Add a few rows – you can add as many as you like
dataTable.Rows.Add("Apple", 1.23);
dataTable.Rows.Add("Banana", 0.78);
dataTable.Rows.Add("Cherry", 2.50);
```

*なぜ重要か*: `DataTable` はビジネスデータと Excel ファイルをつなぐ橋渡しです。Aspose.Cells はこれを直接インポートでき、列名やデータ型を保持します。

---

## Step 2: Spin Up a New Workbook (create excel workbook c#)

次に実際の Excel ファイルオブジェクトを作成します。これは、描き始めるための白紙のキャンバスと考えてください。

```csharp
using Aspose.Cells;

// Instantiate a fresh workbook – this is the core of create excel workbook c#
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0). You could also add more sheets later.
Worksheet worksheet = workbook.Worksheets[0];
```

> **プロのコツ**: 複数シートが必要な場合は `workbook.Worksheets.Add()` を呼び出し、シートごとに意味のある名前を付けましょう。

---

## Step 3: Define a Currency Style (format cells currency)

Aspose.Cells では、セルの見た目を定義する `Style` オブジェクトを作成できます。通貨用には組み込みの数値形式 ID 164（`"$#,##0.00"`）を使用します。

```csharp
// Create a new style object for the price column
Style priceStyle = workbook.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format "$#,##0.00"
```

*なぜ文字列だけでなく ID を使うのか*? 組み込み ID を使用すると、Excel のバージョン間での互換性が保たれ、ロケール固有の問題を回避できます。

---

## Step 4: Build the Style Array (apply currency format column)

`DataTable` をインポートする際、列ごとに `Style` オブジェクトの配列を渡すことができます。`null` は「デフォルトスタイルを使用」の意味です。ここでは 2 番目の列（価格列）だけに `priceStyle` を適用します。

```csharp
// Column 0 (Product) gets the default style, Column 1 (Price) gets the currency style
Style[] columnStyles = { null, priceStyle };
```

後で列を増やす場合は、配列を同様に拡張すれば OK です。`columnStyles` の長さはインポートする列数と一致している必要があり、そうでないと Aspose が例外をスローします。

---

## Step 5: Import the DataTable with Styles (import datatable to excel)

ここで魔法が起きます――`DataTable` がワークシートに配置され、価格列は即座に通貨形式で表示されます。

```csharp
// Parameters:
//  - dataTable: source data
//  - true: include column headers
//  - startRow: 0 (top of sheet)
//  - startColumn: 0 (first column)
//  - columnStyles: style array defined above
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

*列が 2 つ以上ある場合は?* `columnStyles` を拡張して各列に適切なスタイル（またはデフォルトの `null`）を設定してください。これが **add number format excel** を選択的に適用する最もクリーンな方法です。

---

## Step 6: Save the Workbook (create excel workbook c#)

最後にファイルをディスクに書き出します。書き込み権限のあるフォルダーを選んでください。

```csharp
// Save the workbook as an XLSX file
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

`StyledTable.xlsx` を Excel で開くと以下のように表示されます:

| Product | Price |
|---------|-------|
| Apple   | $1.23 |
| Banana  | $0.78 |
| Cherry  | $2.50 |

**Price** 列はすでに通貨形式にフォーマットされており、追加の手順は不要です。

---

## Edge Cases & Variations

### More Columns, Different Formats

複数列（例: Cost, Tax, Total）に **format cells currency** を適用したい場合は、列ごとに別々の `Style` を作成し、`columnStyles` に設定します:

```csharp
Style costStyle = workbook.CreateStyle();
costStyle.Number = 164; // currency

Style taxStyle = workbook.CreateStyle();
taxStyle.Number = 164;

// Assuming columns: Product, Cost, Tax, Total
Style[] styles = { null, costStyle, taxStyle, priceStyle };
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, styles);
```

### Locale‑Specific Currency

ユーロやポンドなど別の通貨を使用する場合は、別の組み込み ID（例: `€#,##0.00` 用の 165）を使います。あるいはカスタム書式文字列を設定します:

```csharp
priceStyle.Custom = "€#,##0.00";
```

### Large Data Sets

Aspose.Cells は数百万行まで処理可能ですが、スタイルオブジェクトが増えるとメモリ使用量も増えます。通貨列が複数ある場合は、同一の `Style` インスタンスを再利用してフットプリントを抑えましょう。

### Missing Styles

`columnStyles` が列数より短い場合、残りの列にはデフォルトスタイルが適用されます。特定の列だけを対象にしたいときに便利です。

---

## Full Working Example (All Steps Combined)

以下はコンソールアプリにコピペできる完全なプログラムです。これまで説明したすべての要素と、いくつかの便利なコメントが含まれています。

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Build sample DataTable (import datatable to excel)
        // -------------------------------------------------
        DataTable dataTable = new DataTable();
        dataTable.Columns.Add("Product", typeof(string));
        dataTable.Columns.Add("Price", typeof(double));
        dataTable.Rows.Add("Apple", 1.23);
        dataTable.Rows.Add("Banana", 0.78);
        dataTable.Rows.Add("Cherry", 2.50);
        // You can add as many rows as you like here.

        // -------------------------------------------------
        // Step 2: Create a new workbook (create excel workbook c#)
        // -------------------------------------------------
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // -------------------------------------------------
        // Step 3: Define a currency style (format cells currency)
        // -------------------------------------------------
        Style priceStyle = workbook.CreateStyle();
        priceStyle.Number = 164; // "$#,##0.00" – built‑in currency format

        // -------------------------------------------------
        // Step 4: Build the style array (apply currency format column)
        // -------------------------------------------------
        // First column gets default style (null), second column uses priceStyle.
        Style[] columnStyles = { null, priceStyle };

        // -------------------------------------------------
        // Step 5: Import the DataTable with the style array
        // -------------------------------------------------
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // -------------------------------------------------
        // Step 6: Save the workbook to disk
        // -------------------------------------------------
        string outputPath = @"YOUR_DIRECTORY\StyledTable.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**期待される結果**: `StyledTable.xlsx` を開くと `Price` 列がドル記号と小数点以下 2 桁で表示され、**format cells currency** の指示通りにフォーマットされています。

---

## Frequently Asked Questions

**Q: Does this work with .NET Core?**  
A: Absolutely. Aspose.Cells is .NET‑standard compliant, so you can target .NET 5, .NET 6, or later without changes.

**Q: What if my DataTable has 10 columns but I only want to format column 5?**  
A: Create a `Style[]` of length 10, fill positions 0‑4 and 6‑9 with `null`, and put your custom style at index 4 (zero‑based). Aspose will respect each entry.

**Q: Can I hide the header row?**  
A: After import, set `worksheet.Cells.Rows[0].Hidden = true;` or simply pass `false` for the `includeColumnNames` parameter in `ImportDataTable`.

---

## Conclusion

私たちは **Excel ワークブック C# を作成し**、`DataTable` をインポートし、Aspose.Cells を使って **通貨形式の列を適用**しました。データ準備、スタイル定義、スタイル配列作成、`ImportDataTable` によるインポート、保存という主要ステップは、ほとんどの Excel 自動化タスクの核となります。

ここからさらに踏み込むなら:

- **add number format excel** を日付やパーセンテージに応用  
- 1 ファイルに複数シートをエクスポート  
- ロケール固有のシンボルで **format cells currency** を使用  
- 同じデータを元にしたチャート自動生成  

ぜひ試してみて、チーム内の Excel レポート作成の頼りになる存在になってください。独自の工夫や質問があればコメントでシェアしてください—Happy coding!

![create excel workbook c# screenshot](image.png "create excel workbook c#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}