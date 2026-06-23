---
category: general
date: 2026-06-17
description: C#でExcelの日付形式を設定し、セルの背景色や文字色を適用し、インポート時にExcel列に色を付ける方法をステップバイステップで学ぶ。
draft: false
keywords:
- set date format
- set cell background
- apply foreground color
- color excel column
- excel import formatting
language: ja
og_description: C#でセルの背景色を設定し、前景色を適用し、インポート時にExcel列に色を付けながら、Excelの日時形式を設定する。完全チュートリアル。
og_title: C#でExcelの日付形式を設定する – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  headline: Set date format in Excel with C# – Full Import Formatting Guide
  type: TechArticle
- description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  name: Set date format in Excel with C# – Full Import Formatting Guide
  steps:
  - name: 2.1 Set Date Format for the First Column
    text: The first column (`OrderDate`) should display as “MM/dd/yyyy”. Aspose uses
      the built‑in number format index 14 for the short date, but you can also supply
      a custom format string if you prefer.
  - name: 2.2 Set Cell Background for the Second Column
    text: Let’s give the `CustomerName` column a light blue background. This is where
      **set cell background** comes into play.
  - name: 2.3 Apply Foreground (Text) Color – Optional Extra
    text: 'If you also want the text itself to be a contrasting color, you can tweak
      the same style:'
  - name: 3.1 Save the Workbook
    text: '```csharp // Save to a file – change path as needed wb.Save("FormattedReport.xlsx",
      SaveFormat.Xlsx); Console.WriteLine("Excel file created with date format and
      colors."); ```'
  - name: What if I have more than two columns?
    text: Just expand the `columnStyles` array and assign a `Style` to each index
      you care about. Unassigned indexes will fall back to the default style, which
      is perfectly fine.
  - name: How do I format a column as currency?
    text: '```csharp columnStyles[3] = wb.CreateStyle(); columnStyles[3].Number =
      164; // Built‑in currency format (e.g., $#,##0.00) ```'
  - name: Can I change the header row style separately?
    text: 'Yes. After the import, you can grab the first row and apply a distinct
      style:'
  - name: What if the DataTable contains null dates?
    text: 'Aspose will leave those cells blank. If you prefer a placeholder like “N/A”,
      you can preprocess the table:'
  type: HowTo
tags:
- excel
- csharp
- aspnet
- data-import
title: C#でExcelの日付形式を設定する – 完全インポート書式ガイド
url: /ja/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Excel の日付形式を設定 – 完全インポート書式ガイド

C# のコードから生成した Excel シートで **日付形式を設定** したい、さらに列にカスタムの背景色や文字色を付けたい、という経験はありませんか？ あなただけではありません。多くのレポート作成シナリオでは、データベースから `DataTable` を取得し、ワークシートに貼り付けた後、日付を正しく表示させ、列を適切な色で目立たせようと奮闘します。  

このチュートリアルでは、**日付形式を設定**、**セルの背景を設定**、**前景色を適用**、さらには **Excel の列全体に色を付ける** という一連の手順を、クリーンでエンドツーエンドな解決策として解説します。最後まで読めば、**excel import formatting** を試行錯誤なしで実現できる再利用可能なパターンが手に入ります。

> **必要なもの**  
> * .NET 6+（または .NET Framework 4.7+）  
> * Aspose.Cells for .NET（無料トライアルでテスト可）  
> * `DataTable` ソース – 任意の ADO.NET クエリで取得できれば OK  
> * Visual Studio もしくはお好みの IDE  

さあ、始めましょう。

---

## ソリューションの概要

問題を次の 3 つの論理的なパートに分割します。

1. **ソースデータの取得** – エクスポートしたい行が入った `DataTable`。  
2. **列ごとのスタイル作成** – 日付列用のスタイル、テキスト列用のスタイル、その他必要なスタイルを用意。  
3. **スタイル付きでテーブルをインポート** – `Worksheet.Cells.ImportDataTable` を使用し、各列が事前に用意したスタイルを継承するようにインポート。

なぜこのアプローチかというと、Aspose.Cells では `ImportDataTable` 呼び出し時に `Style` 配列を直接渡せるため、二度手間で書式を再適用する必要がなくなります。高速でエラーが少なく、コードもすっきりします。

---

## 手順 1: エクスポートするデータを取得

まずは `DataTable` が必要です。実際のプロジェクトではストアドプロシージャを呼び出したり Entity Framework で取得したりしますが、ここでは日付列とテキスト列だけを持つシンプルなテーブルをモックします。

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("OrderDate", typeof(DateTime));
    table.Columns.Add("CustomerName", typeof(string));

    // Sample rows – replace with your DB call
    table.Rows.Add(DateTime.Today.AddDays(-2), "Acme Corp");
    table.Rows.Add(DateTime.Today.AddDays(-1), "Globex Inc");
    table.Rows.Add(DateTime.Today, "Soylent Co");

    return table;
}
```

> **プロのコツ:** ソースが nullable な日付を含む場合、列の型を `typeof(DateTime?)` にしておくと、後で割り当てる書式が正しく適用されます。

---

## 手順 2: 列ごとのスタイル配列を作成

次に、`DataTable` の列数と同じ長さの `Style[]` を作成します。各要素に対応する列の書式を設定します。

```csharp
// Create a new workbook and get the first worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Pull the data
DataTable dataTable = GetData();

// Allocate the style array
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

### 2.1 最初の列の日時書式を設定

最初の列（`OrderDate`）は “MM/dd/yyyy” 形式で表示させます。Aspose では組み込みの数値書式インデックス 14 がショート日付に相当しますが、カスタム書式文字列を指定しても構いません。

```csharp
// Style for the date column (index 0)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Built‑in short date format
// Or a custom pattern:
// columnStyles[0].Custom = "mm/dd/yyyy";
```

**重要ポイント:** Excel は日付をシリアル番号として保存します。数値書式を割り当てることで、シリアル番号を人が読める日付として表示させることができます。

### 2.2 2 番目の列にセル背景を設定

`CustomerName` 列に薄い青色の背景を付けてみましょう。ここが **set cell background** の出番です。

```csharp
// Style for the text column (index 1)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightBlue;
columnStyles[1].Pattern = BackgroundType.Solid; // Needed to show the color
```

> **注記:** `Pattern` を `Solid` にしないと前景色が表示されません。デフォルトのパターンは “None” です。

### 2.3 前景（テキスト）色を適用 – 任意の追加設定

テキスト自体をコントラストのある色にしたい場合は、同じスタイルで調整できます。

```csharp
columnStyles[1].Font.Color = System.Drawing.Color.DarkBlue; // apply foreground color
```

これで **apply foreground color** の要件を満たしつつ、列の背景はそのまま保持できます。

---

## 手順 3: 定義したスタイルで DataTable をインポート

スタイルが準備できたら、データをインポートしつつ列ごとに書式を適用するワンライナーを実行します。

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// includeColumnNames = true to add a header row
ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**動作概要:** Aspose は `columnStyles` 配列を読み取り、各 `Style` を対応する列インデックスにマッピングします。ヘッダー行は別途スタイルを指定しない限りデフォルトの書式を継承します。

### 3.1 ワークブックを保存

```csharp
// Save to a file – change path as needed
wb.Save("FormattedReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Excel file created with date format and colors.");
```

プログラムを実行し、*FormattedReport.xlsx* を開くと以下が確認できます。

- **OrderDate** 列が日付として表示（例: `06/15/2026`）。  
- **CustomerName** 列が薄い青色の塗りつぶしと濃い青色の文字。  

これで 30 行程度の C# で **excel import formatting** の全工程が完了です。

---

## 手順ごとのまとめ（なぜ必要か）

| 手順 | やること | 重要性 |
|------|----------|--------|
| **データ取得** | `GetData()` を呼び出して `DataTable` を作成 | Aspose が直接取り込める構造化データを提供 |
| **スタイル配列作成** | 列数に合わせて `Style[]` を確保 | 1 回のインポート呼び出しで列ごとの書式を適用 |
| **日付書式設定** | `columnStyles[0].Number = 14;` | Excel 上で日付が正しく表示される |
| **背景色設定** | `ForegroundColor = LightBlue; Pattern = Solid;` | 列を目立たせ、**set cell background** を実現 |
| **前景色設定** | `Font.Color = DarkBlue;` | 可読性向上と **apply foreground color** の要件達成 |
| **スタイル付きインポート** | `ImportDataTable(..., columnStyles);` | 書式を保持したまま一括インポート |
| **ワークブック保存** | `wb.Save(...);` | 結果を永続化し、 downstream ユーザーに提供 |

---

## エッジケースとよくある質問

### 列が 2 つ以上ある場合は？

`columnStyles` 配列を拡張し、必要なインデックスに `Style` を割り当てるだけです。割り当てていないインデックスはデフォルトスタイルが使用されます。

```csharp
columnStyles[2] = wb.CreateStyle();
columnStyles[2].Number = 0; // General format for numeric columns
```

### 通貨形式にしたい列は？

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 164; // Built‑in currency format (e.g., $#,##0.00)
```

### ヘッダー行の書式を別にしたい？

インポート後に先頭行を取得して別スタイルを適用できます。

```csharp
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = System.Drawing.Color.Gold;
headerStyle.Pattern = BackgroundType.Solid;

ws.Cells.Rows[0].ApplyStyle(headerStyle, new StyleFlag { All = true });
```

### DataTable に null 日付が含まれる場合は？

Aspose はそれらのセルを空白のままにします。プレースホルダーとして “N/A” を表示したい場合は、テーブルを前処理します。

```csharp
foreach (DataRow row in dataTable.Rows)
{
    if (row.IsNull("OrderDate"))
        row["OrderDate"] = DateTime.MinValue; // or any sentinel
}
```

その後、カスタム書式で “N/A” を表示させる設定を行います。

---

## 完全動作サンプル

以下はコピー＆ペーストで動作する完全版プログラムです。コンソールアプリとして実行すれば、整形された Excel ファイルが生成されます。

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelExportDemo
{
    static void Main()
    {
        // 1️⃣ データ取得
        DataTable dataTable = GetData();

        // 2️⃣ ワークブックとスタイル配列作成
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 2a️⃣ 日付列 – 書式設定
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // 短い日付 (MM/dd/yyyy)

        // 2b️⃣ テキスト列 – 背景色と前景色設定
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].ForegroundColor = Color.LightBlue;
        columnStyles[1].Pattern = BackgroundType.Solid;
        columnStyles[1].Font.Color = Color.DarkBlue; // 前景色適用

        // 3️⃣ 書式付きでインポート
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // 任意: ヘッダー行のスタイル
        Style headerStyle = wb.CreateStyle();
        headerStyle.Font.IsBold = true;
        headerStyle.ForegroundColor = Color.Gold;
        headerStyle.Pattern = BackgroundType.Solid;
        ws.Cells


## 次に学ぶべきこと


以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれているので、API の追加機能を習得したり、別の実装アプローチを自分のプロジェクトに取り入れたりする際に役立ちます。

- [Set Font Color in Excel Cells using Aspose.Cells for .NET](/cells/english/net/formatting/setting-font-color/)
- [Set Font Color in .NET Excel with Aspose.Cells](/cells/english/net/formatting/set-font-color-net-excel-aspose-cells/)
- [Set Excel Column Widths in Pixels Using Aspose.Cells for .NET | Step-by-Step Guide](/cells/english/net/formatting/set-excel-column-width-pixels-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}