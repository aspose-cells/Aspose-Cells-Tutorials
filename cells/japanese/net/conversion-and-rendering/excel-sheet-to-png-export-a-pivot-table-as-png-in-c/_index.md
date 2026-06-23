---
category: general
date: 2026-03-18
description: Aspose.Cells を使用して、ピボットテーブルをエクスポートし、印刷領域を設定し、Excel の範囲画像をエクスポートする方法を示す
  Excel シートから PNG へのチュートリアル。
draft: false
keywords:
- excel sheet to png
- how to export pivot
- set print area pivot
- export excel range image
- export worksheet to image
language: ja
og_description: ExcelシートをPNGに変換するチュートリアル：ピボットテーブルのエクスポート方法、印刷範囲のピボット設定、C#でExcel範囲の画像をエクスポートする手順を解説。
og_title: ExcelシートをPNGに変換 – ピボットテーブルのエクスポート完全ガイド
tags:
- Aspose.Cells
- C#
- Excel automation
title: ExcelシートをPNGに変換 – C#でピボットテーブルをPNGとしてエクスポート
url: /ja/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# excelシートをpngへ – C#でピボットテーブルをPNGとしてエクスポート

Ever needed to turn an **excel sheet to png** but weren’t sure how to capture just the pivot table? You’re not alone. In many reporting pipelines the visual of a pivot is the star, and exporting it as a PNG lets you embed it in emails, dashboards, or documentation without pulling the whole workbook along.

このガイドでは、**how to export pivot** データ、**set print area pivot**、そして最終的に **export excel range image** を示し、クリーンな **export worksheet to image** ファイルを作成する方法を紹介します。外部ドキュメントへの不明瞭なリンクはありません—完全な実行可能スニペットと各行の背後にある理由だけです。

## 必要なもの

- **Aspose.Cells for .NET**（NuGet パッケージ `Aspose.Cells` – バージョン 23.12 以上）。  
- .NET 開発環境（Visual Studio、Rider、または `dotnet` CLI）。  
- ピボットテーブルが少なくとも1つ含まれる Excel ファイル（`input.xlsx`）。

以上です。これらが揃っていれば、さっそく始めましょう。

## Step 1 – ワークブックをロードして最初のワークシートを取得

ピボットに触れる前に、ワークブックをメモリ上にロードする必要があります。

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

namespace PivotToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"C:\Data\input.xlsx");

            // Get the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];
```

*Why this matters:* ファイルをロードすることで、すべてのオブジェクト（テーブル、チャート、ピボット）にアクセスできます。最初のワークシートを使用するのはシンプルなデフォルトで、必要に応じて `0` を実際のシートインデックスや名前に置き換えることができます。

## Step 2 – ピボットテーブルの範囲を取得

ピボットテーブルはセルブロック内に存在します。そのブロックが必要なのは、Excel に印刷範囲を指示できるようにするためです。

```csharp
            // Assume the first pivot table on the sheet
            PivotTable pivot = worksheet.PivotTables[0];

            // The range that the pivot occupies (e.g., A1:D20)
            CellArea pivotRange = pivot.PivotTableRange;
```

*Why we do this:* `PivotTableRange` は開始行/列と終了行/列の正確な位置を教えてくれます。これがなければ、エクスポートはシート全体を含んでしまい、**set print area pivot** の目的が失われます。

## Step 3 – ピボットだけがレンダリングされるように印刷領域を定義

Excel の印刷エンジンは `PrintArea` プロパティを尊重します。これをピボットに絞ることで、余計なデータや空白セルを回避できます。

```csharp
            // Build the address string: "StartRow,StartColumn:EndRow,EndColumn"
            string printArea = $"{pivotRange.StartRow},{pivotRange.StartColumn}:" +
                               $"{pivotRange.EndRow},{pivotRange.EndColumn}";

            worksheet.PageSetup.PrintArea = printArea;
```

*Pro tip:* 同じシートに複数のピボットがある場合、カンマ区切りリスト（`"0,0:10,5,12,0:22,5"`）で範囲を結合できます。これが複数ブロックに対する **export excel range image** のテクニックです。

## Step 4 – 画像エクスポートオプションを設定（PNG形式）

Aspose.Cells を使うと出力を細かく調整できます。PNG はロスレスで、鮮明なピボットビジュアルに最適です。

```csharp
            // Configure image export options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: increase resolution for sharper output
                HorizontalResolution = 300,
                VerticalResolution = 300
            };
```

*Why PNG?* JPEG とは異なり、PNG はテキストの鮮明さと透過背景を保持するため、**excel sheet to png** のシナリオで最適です。

## Step 5 – ワークシート（ピボット領域）を PNG ファイルにエクスポート

いよいよマジックが起きます—定義した印刷領域を画像としてレンダリングします。

```csharp
            // Export the first page (index 0) of the worksheet to an image
            // The page corresponds to the print area we set earlier
            worksheet.ToImage(0, imgOptions).Save(@"C:\Data\pivot.png");

            // Inform the user
            System.Console.WriteLine("Pivot exported to PNG successfully!");
        }
    }
}
```

*What you’ll see:* ピボットテーブルだけが含まれた `pivot.png` ファイルが生成されます。余分な行や列はありません。任意の画像ビューアで開くと、すぐに共有できるビジュアルが得られます。

---

## よくある質問とエッジケース

### ワークブックに **multiple pivot tables** がある場合は？

各ピボットの `PivotTableRange` を取得し、範囲を結合して、結合した文字列を `PrintArea` に割り当てます。例:

```csharp
string combinedArea = "";
foreach (PivotTable pt in worksheet.PivotTables)
{
    CellArea ca = pt.PivotTableRange;
    combinedArea += $"{ca.StartRow},{ca.StartColumn}:{ca.EndRow},{ca.EndColumn},";
}
combinedArea = combinedArea.TrimEnd(','); // Remove trailing comma
worksheet.PageSetup.PrintArea = combinedArea;
```

### **other image formats** にエクスポートできますか？

もちろんです。`imgOptions.ImageFormat = ImageFormat.Jpeg;`（または `Bmp`, `Gif`, `Tiff`）に変更します。ただし JPEG は圧縮アーティファクトを生むため、テキストが多いピボットには通常適していません。

### 多ページにまたがる **large pivots** の扱い方は？

`imgOptions.OnePagePerSheet = false;` に設定してマルチページレンダリングを許可し、ページごとにループします。

```csharp
int pageCount = worksheet.PageCount;
for (int i = 0; i < pageCount; i++)
{
    worksheet.ToImage(i, imgOptions).Save($@"C:\Data\pivot_page{i + 1}.png");
}
```

### **hidden rows/columns** はどうですか？

Aspose はワークシートの表示設定を尊重します。非表示要素を無視したい場合は、エクスポート前に一時的に表示に戻すか、`PrintArea` を手動で調整してください。

## 完全動作例（コピー＆ペースト可能）

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

namespace PivotToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook & select sheet
            Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Get the first pivot table's range
            PivotTable pivot = worksheet.PivotTables[0];
            CellArea pivotRange = pivot.PivotTableRange;

            // 3️⃣ Set print area to the pivot only
            string printArea = $"{pivotRange.StartRow},{pivotRange.StartColumn}:" +
                               $"{pivotRange.EndRow},{pivotRange.EndColumn}";
            worksheet.PageSetup.PrintArea = printArea;

            // 4️⃣ Prepare PNG export options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // 5️⃣ Export to PNG
            worksheet.ToImage(0, imgOptions).Save(@"C:\Data\pivot.png");

            System.Console.WriteLine("✅ Pivot exported to PNG at C:\\Data\\pivot.png");
        }
    }
}
```

プログラムを実行すると、指定した場所に `pivot.png` が生成されます。ファイルを開くと、ピボットテーブルだけが鮮明にレンダリングされていることが確認でき、他のものは含まれていません。

## 結論

これで、**excel sheet to png** をピボットテーブルに限定して変換する **完全なエンドツーエンドソリューション** が手に入りました。**setting the print area pivot** を行い、**image export options** を設定し、Aspose.Cells の `ToImage` メソッドを使用することで、レポート生成の自動化、ウェブページへのビジュアル埋め込み、または分析スナップショットのアーカイブが可能になります。

次は何をしますか？ PNG を高解像度 PDF（`ImageFormat.Pdf`）に置き換えてみたり、1枚のシートに複数のピボットを試したり、チャートエクスポートと組み合わせてフル機能のダッシュボードエクスポートパイプラインを構築してみてください。

何か独自の工夫がありますか？ コメントを残すか、次回のチュートリアルで **export worksheet to image** を使ったシート全体のスナップショット（チャートや条件付き書式を含む）を探求しましょう。コーディングを楽しんでください！  

<img src="pivot.png" alt="excel sheet to png example of pivot table export">

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}