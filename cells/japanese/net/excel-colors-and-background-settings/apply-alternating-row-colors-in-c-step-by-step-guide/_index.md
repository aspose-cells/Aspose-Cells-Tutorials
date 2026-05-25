---
category: general
date: 2026-03-18
description: C# を使用してワークシートに交互に行の色を適用する方法を学びます。行の背景色の設定、薄い黄色の背景の追加、そして行を交互に色付けすることが含まれます。
draft: false
keywords:
- apply alternating row colors
- set row background color
- add light yellow background
- set alternating row shading
- color rows alternately
language: ja
og_description: C#で交互に行の色を適用して可読性を向上させます。このガイドでは、行の背景色の設定、薄い黄色の背景の追加、そして行を交互に色付けする方法を示します。
og_title: C#で交互の行の色を設定する – 完全チュートリアル
tags:
- C#
- DataTable
- Spreadsheet styling
- UI design
title: C#で交互に行の色を適用する – ステップバイステップガイド
url: /ja/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で交互に行の色を適用する – 完全チュートリアル

データ駆動のワークシートに **apply alternating row colors** を適用したいと思ったことはありませんか？どこから始めればいいか分からないこともあるでしょう。あなただけではありません — 多くの開発者がテーブルを少し見やすくしようとしたときにこの壁にぶつかります。良いニュースは、数行の C# で **set row background color** ができ、**add light yellow background** を加えるだけで、すぐに可読性が向上する洗練されたグリッドが完成します。

このチュートリアルでは、`DataTable` をメモリに取り込むところから、微妙な黄白ストライプで各行をスタイリングするまでの全プロセスを順に解説します。最後まで読めば、**color rows alternately** を自信を持って実装できるようになり、異なる色合いや動的テーマが必要な場合の便利なバリエーションも紹介します。

## 必要なもの

- .NET 6 以降を対象とした .NET プロジェクト（コードは .NET Framework 4.7+ でも動作します）。  
- スタイルオブジェクトをサポートするスプレッドシートライブラリ – 例では **Aspose.Cells**、**GemBox.Spreadsheet**、または **ClosedXML** のような API を模した汎用 `Workbook`/`Worksheet` を使用しています。  
- `DataTable` ソース – データベースクエリ、CSV インポート、または任意のインメモリコレクションから取得できます。  

スプレッドシートライブラリ以外に追加の NuGet パッケージは不要です。Aspose.Cells を使用する場合は名前空間が `Aspose.Cells`、ClosedXML の場合は `ClosedXML.Excel` です。`CreateStyle` と `ImportDataTable` の呼び出しはそれぞれのライブラリに合わせて置き換えてください。

## ステップ 1: ソースデータを DataTable として取得する

まず最初に、表示したいデータを取得します。実際のアプリでは通常データベースにアクセスしますが、ここでは `GetData()` というヘルパーメソッドをスタブとして用意し、充実した `DataTable` を返すものとします。

```csharp
// Step 1: Retrieve the source data as a DataTable
DataTable dataTable = GetData();   // Replace with your actual data retrieval logic
```

> **Why this matters:** `DataTable` は後で交互のシェーディングを適用する行と列を定義します。テーブルが空の場合はスタイルを適用する対象がないため、必ず `Rows.Count` > 0 であることを確認してから処理を進めてください。

### プロ・チップ
Entity Framework からデータを取得する場合は、`SqlCommand` を実行した後に `DataTable.Load(reader)` を使用できます。これによりコードがすっきりし、手動で列定義を行う手間が省けます。

## ステップ 2: 各行のスタイルを保持する配列を割り当てる

次に、行数と同じサイズのコンテナが必要です。ほとんどのスプレッドシート API はインポートメソッドにスタイル配列を渡すことができるので、行数に正確に合わせた `Style[]` を作成します。

```csharp
// Step 2: Allocate an array to hold a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];
```

> **Explanation:** 配列を事前に確保しておくことで、各イテレーションで新しいスタイルオブジェクトを再割り当てする必要がなくなり、数千行を扱う際のパフォーマンス向上につながります。

## ステップ 3: 交互に行の色を適用する（ライトイエロー / ホワイト）

いよいよ本題です： **apply alternating row colors** を実装します。各行をループし、ワークブックから新しいスタイルインスタンスを作成し、行インデックスに基づいて背景色を設定します。偶数行はライトイエローで塗り、奇数行はホワイトのままにします。

```csharp
// Step 3: Create alternating background colors (light yellow / white) for the rows
for (int rowIndex = 0; rowIndex < dataTable.Rows.Count; rowIndex++)
{
    // Create a new style instance from the workbook
    rowStyles[rowIndex] = wb.CreateStyle();

    // Apply a light yellow background to even rows, white to odd rows
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow   // add light yellow background
        : Color.White;        // set row background color to white

    rowStyles[rowIndex].Pattern = BackgroundType.Solid; // set alternating row shading
}
```

### なぜこれが機能するのか
- **`rowIndex % 2 == 0`** は行が偶数かどうかを判定します。  
- **`Color.LightYellow`** はデータテーブルに最適な、控えめで目障りしない色合いを提供します。  
- **`BackgroundType.Solid`** により塗りつぶしがセル全体を覆い、**set row background color** の効果を実現します。  

`Color.LightYellow` は `Color.LightCyan` など他の色に置き換えても構いません。同じロジックを使えば、ステータスフラグなど別の条件に基づいて **color rows alternately** することも可能です。

## ステップ 4: 用意したスタイルで DataTable をワークシートにインポートする

最後に、すべてをワークシートに書き込みます。多くのライブラリはスタイル配列を受け取る `ImportDataTable` のオーバーロードを提供しています。`true` フラグは列ヘッダーを書き込むことを指示し、`0, 0` の座標は左上セルから開始することを意味します。

```csharp
// Step 4: Import the DataTable into the worksheet, applying the prepared row styles
ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

> **Result:** ワークシートは **alternating row shading** パターンでデータを表示します—偶数行はライトイエロー、奇数行はホワイトです。ユーザーは目を行き来させることなくグリッドをスムーズに閲覧できます。

### 期待される出力
結果のスプレッドシートを開くと、以下のように表示されます：

| ID | Name      | Quantity |
|----|-----------|----------|
| **1** | Apple      | 50       |
| **2** | Banana     | 30       |
| **3** | Cherry     | 20       |
| **4** | Date       | 15       |

行 1、 3、 5… は **light yellow background**、行 2、 4、 6… は **white** のままです。ヘッダー行（行 0）はデフォルトスタイルを継承しますが、別途カスタマイズすることも可能です。

## オプションのバリエーションとエッジケース

### 1. 別のカラーパレットを使用する
ライトイエローがブランドと合わない場合は、`Color.LightYellow` を別の `System.Drawing.Color` に置き換えるだけです。ブルーグレーのテーマにしたい場合は次のようにします：

```csharp
rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
    ? Color.FromArgb(220, 235, 247) // soft blue
    : Color.White;
```

### 2. データに基づく動的シェーディング
条件を満たす行（例：在庫が少ない）をハイライトしたいことがあります。その場合は、モジュロチェックにカスタムテストを組み合わせます：

```csharp
int quantity = Convert.ToInt32(dataTable.Rows[rowIndex]["Quantity"]);
if (quantity < 20)
{
    rowStyles[rowIndex].ForegroundColor = Color.Salmon; // urgent low‑stock color
}
else
{
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow
        : Color.White;
}
```

### 3. 特定の列だけにスタイルを適用する
特定の列だけに **set row background color** を適用したい場合は、列ごとに別々のスタイルを作成し、インポート後にワークシートのセル範囲 API を使って割り当てます。

```csharp
// Example for column B only
var colBStyle = wb.CreateStyle();
colBStyle.ForegroundColor = Color.LightYellow;
colBStyle.Pattern = BackgroundType.Solid;

// Apply after import
ws.Cells[$"B2:B{dataTable.Rows.Count + 1}"].SetStyle(colBStyle);
```

### 4. 大規模テーブル向けのパフォーマンス・ヒント
10,000 行を超える場合は、色ごとに 1 つのスタイルオブジェクトを再利用し、行ごとに新しいオブジェクトを作成しないようにします。配列は 2 つの共有スタイルへの参照だけを保持するため、メモリ使用量が大幅に削減されます。

```csharp
Style yellowStyle = wb.CreateStyle();
yellowStyle.ForegroundColor = Color.LightYellow;
yellowStyle.Pattern = BackgroundType.Solid;

Style whiteStyle = wb.CreateStyle();
whiteStyle.ForegroundColor = Color.White;
whiteStyle.Pattern = BackgroundType.Solid;

for (int i = 0; i < dataTable.Rows.Count; i++)
    rowStyles[i] = (i % 2 == 0) ? yellowStyle : whiteStyle;
```

## 完全な動作例

以下はコンソールアプリに貼り付けて実行できる、自己完結型のプログラムです。架空の `Workbook`/`Worksheet` API を使用していますので、使用しているライブラリの型に置き換えてください。

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using YourSpreadsheetLib;     // Replace with actual namespace

class Program
{
    static void Main()
    {
        // Initialize workbook & worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Step 1: Retrieve data
        DataTable dataTable = GetData();

        // Step 2: Allocate style array
        Style[] rowStyles = new Style[dataTable.Rows.Count];

        // Step 3: Apply alternating row colors
        for (int i = 0; i < dataTable.Rows.Count; i++)
        {
            rowStyles[i] = wb.CreateStyle();
            rowStyles[i].ForegroundColor = (i % 2 == 0)
                ? Color.LightYellow   // add light yellow background
                : Color.White;        // set row background color
            rowStyles[i].Pattern = BackgroundType.Solid; // set alternating row shading
        }

        // Step 4: Import with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // Save to file
        wb.Save("AlternatingRows.xlsx");
        Console.WriteLine("Workbook saved with alternating row colors.");
    }

    // Sample data generator
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(1, "Apple", 50);
        dt.Rows.Add(2, "Banana", 30);
        dt.Rows.Add(3, "Cherry", 20);
        dt.Rows.Add(4, "Date", 15);
        dt.Rows.Add(5, "Elderberry", 5);
        return dt;
    }
}
```

**Output:** `AlternatingRows.xlsx` という名前のファイルが生成され、各行がライトイエローの塗りつぶしとホワイトを交互に繰り返すため、表が目に優しくなります。

## よくある質問

**Q: Does this approach work with Excel‑style conditional formatting?**  
A: はい。ライブラリが条件付きルールをサポートしている場合、同じロジックを `MOD(ROW(),2)=0` をチェックするルールに変換できます。ここで示したコードベースの手法は、組み込みの条件付き書式がないライブラリでもより汎用的に利用できます。

**Q: What if I need to **color rows alternately** in a PDF table instead of an Excel sheet?**  
A: 多くの PDF テーブルジェネレータ（例：iTextSharp、PdfSharp）では、行ごとに `BackgroundColor` を設定できます。同じモジュロ計算を適用すれば、PDF テーブルでも交互に行の色を付けることが可能です。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}