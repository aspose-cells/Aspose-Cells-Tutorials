---
category: general
date: 2026-10-01
description: 数分で Aspose を使って Word にチャートを追加。Excel のチャートを Word に埋め込む方法、Excel から Word
  へのチャートのエクスポート、Aspose で Word 文書を作成、そしてチャートを Word 文書に保存する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add chart to word
- embed excel chart word
- export chart excel word
- create word document aspose
- save chart word document
language: ja
lastmod: 2026-10-01
og_description: 数分でAsposeを使用してWordにチャートを追加できます。このガイドでは、ExcelのチャートをWordに埋め込む方法、チャートをExcelからWordへエクスポートする方法、AsposeでWord文書を作成する方法、そしてチャートをWord文書に保存する方法を示します。
og_image_alt: Screenshot illustrating how to add chart to Word using Aspose
og_title: AsposeでWordにチャートを追加 – Excelチャートを埋め込む
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  headline: How to add chart to Word with Aspose – embed Excel chart
  type: TechArticle
- description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  name: How to add chart to Word with Aspose – embed Excel chart
  steps:
  - name: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
    text: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
  - name: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
    text: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
  - name: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
    text: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
  - name: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
    text: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
  - name: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
    text: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
  type: HowTo
tags:
- Aspose
- C#
- Word automation
title: AsposeでWordにチャートを追加する方法 – Excelチャートを埋め込む
url: /ja/net/chart-rendering-and-conversion/how-to-add-chart-to-word-with-aspose-embed-excel-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose を使用して Word にチャートを追加する – Excel チャートの埋め込み

**Word にチャートを追加**したい場合、このチュートリアルはすぐに実行できる完全なソリューションを提供します。Excel のチャートを Word ファイルに埋め込み、Excel から Word へチャートをエクスポートし、数行の C# コードだけで **チャート付き Word ドキュメントを保存**する方法を紹介します。

レポート、請求書、ダッシュボードなどをプログラムで生成する際、チャートの埋め込みは一般的な要件です。このガイドを終える頃には、手動でコピー＆ペーストすることなく、Excel ワークブック内の任意のチャートを含む **Word ドキュメント Aspose** を作成できるようになります。

## 前提条件

- .NET 6.0 以降（コードは .NET Framework 4.7+ でも動作します）
- Aspose.Cells と Aspose.Words の NuGet パッケージ（`dotnet add package Aspose.Cells` と `dotnet add package Aspose.Words` でインストール）
- 少なくとも 1 つのチャートが含まれる既存の Excel ファイル（`Chart.xlsx`）
- Visual Studio 2022 または VS Code などの開発環境

## Aspose で Word にチャートを追加する

以下は完全な単体プログラムです。新しいコンソールプロジェクトにコピーし、パッケージを復元して実行してください。プログラムは Excel ワークブックを読み込み、Word ドキュメントを作成し、最初のチャートを挿入して結果を保存します。

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

namespace AddChartToWordDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the Excel workbook that contains the chart
            var workbookPath = @"YOUR_DIRECTORY\Chart.xlsx";
            var workbook = new Workbook(workbookPath);

            // Step 2: Create a new Word document that will receive the chart
            var wordDoc = new Document();

            // Step 3: Initialise a DocumentBuilder for the Word document
            var builder = new DocumentBuilder(wordDoc);

            // Step 4: Insert the first chart from the first worksheet into the Word document
            // This uses Aspose.Words' InsertChart overload that accepts an Aspose.Cells chart object
            builder.InsertChart(workbook.Worksheets[0].Charts[0]);

            // Step 5: Save the resulting Word document
            var outputPath = @"YOUR_DIRECTORY\Chart.docx";
            wordDoc.Save(outputPath);

            Console.WriteLine($"Chart successfully added and saved to '{outputPath}'.");
        }
    }
}
```

### 各行の重要ポイント

1. **ワークブックの読み込み** – `Workbook` は Excel ファイルを解析し、ワークシートやチャートへのプログラム的アクセスを提供します。  
2. **Word ドキュメントの作成** – `Document` は Aspose.Words のあらゆる Word 処理タスクのエントリーポイントです。  
3. **DocumentBuilder** – このヘルパークラスは現在のカーソル位置にテキスト、画像、チャートなどのコンテンツを挿入できます。  
4. **InsertChart** – `Aspose.Cells.Chart` オブジェクトを受け取るオーバーロードは、チャートのデータ、書式設定、系列を直接 Word ファイルにコピーします。中間の画像変換は不要で、ベクター品質が保持されます。  
5. **Save** – `Save` は .docx パッケージをディスクに書き込み、**チャート付き Word ドキュメントの保存**ステップを完了します。

#### 期待される出力

プログラム実行後に `Chart.docx` を開くと、`Chart.xlsx` に保存されていた正確なチャートがドキュメントの先頭に配置されていることが確認できます。チャートは Word 内で完全に編集可能で、サイズ変更や色変更、データソースの修正が行えます。

## Excel のチャートを Word に埋め込む

複数のチャートを埋め込む必要がある場合は、各チャートオブジェクトに対して `InsertChart` 呼び出しを繰り返します。たとえば、最初のワークシートにあるすべてのチャートを埋め込む例は次の通りです。

```csharp
var sheet = workbook.Worksheets[0];
foreach (Chart chart in sheet.Charts)
{
    builder.InsertChart(chart);
    builder.Writeln(); // add a line break between charts
}
```

**プロのコツ:** `builder.Writeln()` を使用して段落改行を挿入すれば、各チャートが新しい行から開始されます。

## Excel → Word でチャートをエクスポート – 複数シートの処理

チャートが複数のワークシートに分散している場合は、ワークブックの `Worksheets` コレクションを走査します。

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    foreach (Chart chart in ws.Charts)
    {
        builder.InsertChart(chart);
        builder.Writeln();
    }
}
```

この手法は **Excel → Word でチャートをエクスポート** するあらゆるレイアウトに対応し、複雑なレポートでも堅牢に動作します。

## Aspose で Word ドキュメントを作成 – 外観のカスタマイズ

`InsertChart` が返す `Shape` を変更することで、挿入した各チャートのサイズや位置を制御できます。

```csharp
Shape chartShape = builder.InsertChart(chart);
chartShape.Width = 500;   // width in points
chartShape.Height = 300;  // height in points
chartShape.WrapType = WrapType.Inline; // make the chart flow with text
```

`WrapType` を `Inline` に設定すると、チャートは通常の段落と同様に扱われます。自動化された文書生成ではこの設定が好まれることが多いです。

## チャート付き Word ドキュメントの保存 – ベストプラクティス

- **分かりやすいファイル名を使用**（例: `Report_Q1_2026.docx`）してバージョン管理を容易にします。  
- **オブジェクトは必ず破棄** しましょう。特に大量バッチ処理では以下のように `using` を活用します。

```csharp
wordDoc.Dispose();
workbook.Dispose();
```

- **結果をプログラムで検証** することで、多数のファイルを生成する際の信頼性を高めます。

```csharp
if (System.IO.File.Exists(outputPath))
{
    Console.WriteLine("File saved successfully.");
}
else
{
    Console.Error.WriteLine("Failed to save the document.");
}
```

## よくある質問とエッジケース

| 質問 | 回答 |
|----------|--------|
| *シート上で最初のチャート以外を挿入できますか？* | はい。インデックスでアクセスできます：`sheet.Charts[2]` は 3 番目のチャートです。 |
| *Excel のチャートがワークブックに存在しないデータソースを使用している場合は？* | Aspose.Cells はデータをチャートオブジェクトに直接埋め込むため、元の範囲が削除されてもチャートは機能し続けます。 |
| *Aspose のライセンスは必要ですか？* | 無料評価版でも動作しますが、評価透かしが除去され、すべての機能が解放されるのはライセンス版です。 |
| *挿入後に Word でチャートを編集できますか？* | はい。ネイティブな Word チャートとして挿入されるため、シリーズやタイトル、スタイルを Word の UI で編集可能です。 |
| *ネイティブチャートではなく画像として挿入したい場合は？* | `builder.InsertImage(chart.ToImage())` を使用してラスタ画像として埋め込めます。Word レベルでの編集は不要で、見た目を完全に固定したいときに便利です。 |

## 完全動作サンプル（コピー＆ペースト）

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

class AddChartToWord
{
    static void Main()
    {
        // Load Excel workbook
        var wb = new Workbook(@"C:\Data\Chart.xlsx");

        // Create Word document
        var doc = new Document();
        var builder = new DocumentBuilder(doc);

        // Insert every chart from every worksheet
        foreach (Worksheet ws in wb.Worksheets)
        {
            foreach (Chart ch in ws.Charts)
            {
                Shape shape = builder.InsertChart(ch);
                shape.Width = 500;
                shape.Height = 300;
                builder.Writeln(); // separate charts
            }
        }

        // Save the document
        var outPath = @"C:\Data\ReportWithCharts.docx";
        doc.Save(outPath);
        Console.WriteLine($"Document saved to {outPath}");
    }
}
```

コードを実行すると、ソースワークブック内のすべてのチャートに対する **Word にチャートを追加** の結果が含まれた Word ファイル（`ReportWithCharts.docx`）が生成されます。

## まとめ

これで **Aspose.Cells と Aspose.Words を使用して Word にチャートを追加**する方法、**Excel チャートを Word に埋め込む**、**Excel → Word でチャートをエクスポート**、**Aspose で Word ドキュメントを作成**、そして最終的に **チャート付き Word ドキュメントを保存**する手順が分かりました。このアプローチは単一チャートのシナリオだけでなく、複数シートにまたがる多数のチャートを含む複雑なワークブックにも対応します。

次に試してみると良いでしょう：

- `Chart` API を使って挿入チャートのカスタムスタイリング（色、フォント）を適用する。  
- テキスト生成と組み合わせて、完全に自動化されたレポートを作成する。  
- 必要に応じて Aspose.Slides を利用する  

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示したテクニックを基にした関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、API の追加機能を習得したり、独自プロジェクトで代替実装を検討したりするのに役立ちます。

- [How to Save DOCX from Excel – Complete Guide to Export Charts to Word](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-docx-from-excel-complete-guide-to-export-charts/)
- [Create Excel Workbook with Pie Chart Using Aspose.Cells .NET - Comprehensive Guide](/cells/english/net/charts-graphs/create-excel-workbook-pie-chart-aspose-cells-net/)
- [Create a Bubble Chart in Excel Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/charts-graphs/create-bubble-chart-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}