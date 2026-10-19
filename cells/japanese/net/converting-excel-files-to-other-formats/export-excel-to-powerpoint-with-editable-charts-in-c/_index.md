---
category: general
date: 2026-09-21
description: Aspose.Cells を使用して、編集可能なチャート付きの Excel を PowerPoint にエクスポートします。チャートを編集可能なまま、ワークシートを
  PPTX に変換するステップバイステップガイドをご覧ください。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- worksheet to powerpoint
- export excel chart pptx
- editable charts pptx
language: ja
lastmod: 2026-09-21
og_description: Aspose.Cells を使用して、編集可能なチャート付きで Excel を PowerPoint にエクスポートします。チャートの完全な編集可能性を保ったまま、ワークシートを
  PPTX に変換する方法を学びましょう。
og_image_alt: Screenshot of a PowerPoint slide showing an editable Excel chart after
  export
og_title: 編集可能なチャート付きでExcelをPowerPointにエクスポート – C#チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  headline: Export Excel to PowerPoint with editable charts in C#
  type: TechArticle
- description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  name: Export Excel to PowerPoint with editable charts in C#
  steps:
  - name: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
    text: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
  - name: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
    text: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
  - name: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
    text: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
  - name: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
    text: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel‑to‑PowerPoint
- PPTX export
title: C#で編集可能なチャートを含むExcelをPowerPointにエクスポート
url: /ja/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-editable-charts-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で編集可能なチャート付き Excel を PowerPoint にエクスポート

Excel のスプレッドシートのビジュアルをプレゼンテーションで再利用する必要がある場合、**Excel を PowerPoint にエクスポート**し、チャートの編集可能性を保持することは一般的な要件です。このガイドでは、Aspose.Cells for .NET を使用して **Excel を PowerPoint にエクスポート**しながら、チャートの編集可能性を維持する方法を示します。

学べること:

* チャートやテキスト ボックスを含む既存のブックを読み込む方法。  
* PPTX エクスポート オプションを構成し、チャートや図形を編集可能なままにする方法。  
* 特定のワークシートを PowerPoint ファイルに変換し、Microsoft PowerPoint で開いて編集できるようにする方法。

このチュートリアルは、基本的な C# の知識と .NET の最新バージョン（≥ .NET 6）を前提としています。Aspose.Cells の事前経験は不要です。

---

## Excel を PowerPoint にエクスポート – 概要

**Excel を PowerPoint にエクスポート** の基本的な考え方は、各ワークシートを画像ソースとして扱い、PPTX スライドにレンダリングすることです。`ExportChartAsEditableText` と `ExportShapeAsEditableText` フラグを切り替えることで、Aspose.Cells はフラットなビットマップではなく、PowerPoint の描画オブジェクトとして基になるチャート データを書き込みます。これにより、結果のスライドは完全に編集可能になり、PowerPoint で直接作成したチャートと同様に扱えます。

> **なぜ編集可能なチャートを使用するのか？**  
> 編集可能なチャートを使用すると、プレゼンターは元の Excel ファイルに戻ることなくデータや色、ラベルを調整でき、最終段階の変更が迅速に行えるため、プレゼンテーションのワークフローがスムーズになります。

---

## ワークシートを PowerPoint に変換（worksheet to PowerPoint）

以下は、**worksheet to PowerPoint** 変換を実演する完全な実行可能サンプルです。

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the chart and textbox
            // Replace YOUR_DIRECTORY with the actual folder path on your machine.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Configure PPTX export options to keep charts and shapes editable
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,               // Target format: PPTX
                ExportChartAsEditableText = true,           // Enable editable charts
                ExportShapeAsEditableText = true            // Enable editable shapes/textboxes
            };

            // Step 3: Export the first worksheet (index 0) to a PowerPoint file
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";
            workbook.Worksheets[0].ConvertToImage(exportOptions, outputPath);

            Console.WriteLine($"Worksheet successfully exported to {outputPath}");
        }
    }
}
```

### 各ステップの説明

| Step | コードの動作 | **export excel chart pptx** における重要性 |
|------|--------------|--------------------------------------------|
| 1️⃣   | `input.xlsx` を `Aspose.Cells.Workbook` オブジェクトに読み込みます。 | ワークブックはエクスポートしたいチャートへのアクセスを提供します。 |
| 2️⃣   | `ExportType` を `Pptx` に設定し、`ExportChartAsEditableText` と `ExportShapeAsEditableText` を有効にします。 | これらのフラグが **editable charts pptx** の鍵となり、ライブラリにチャートのジオメトリをラスタ画像ではなく PowerPoint の描画オブジェクトとして書き込むよう指示します。 |
| 3️⃣   | 最初のワークシートで `ConvertToImage` を呼び出し、`Worksheet.pptx` を生成します。 | このメソッドが **export excel to powerpoint** 操作を実行し、PowerPoint で直接開ける PPTX ファイルを書き出します。 |

> **プロのコツ:** 複数のワークシートをエクスポートする必要がある場合は、`workbook.Worksheets` をループし、各シートで `ConvertToImage` を呼び出します。出力ファイルは `Sheet1.pptx`、`Sheet2.pptx` などと命名すると便利です。

---

## PPTX で編集可能なチャートを有効化（export excel chart pptx）

`ExportChartAsEditableText` を `true` に設定すると、Aspose.Cells は各チャートを PPTX XML 内の `<a:graphic>` 要素のコレクションとして書き込みます。PowerPoint はこれらの要素をネイティブなチャート オブジェクトとして扱い、ダブルクリックでチャート エディタを開くことができます。

**よくある落とし穴**

* **Aspose.Cells のライセンスがない** – ライセンスがないと出力に透かしが入ります。プログラムの冒頭でライセンスを登録してください（`License license = new License(); license.SetLicense("Aspose.Cells.lic");`）。  
* **サポートされていないチャート タイプ** – ほとんどの 2‑D チャート（棒、折れ線、円）は完全に編集可能ですが、複雑な 3‑D やコンボ チャートは画像にフォールバックすることがあります。完全な編集可能性が必要な場合は、対象のチャート タイプを事前にテストしてください。  
* **大規模なワークシート** – 非常に大きなワークシートをエクスポートするとメモリ消費が増大します。`ImageOrPrintOptions` の `ExportMaxRows` または `ExportMaxColumns` を使用して、変換対象領域を制限することを検討してください。

---

## チャートを編集可能に保つためのヒント（editable charts pptx）

1. **チャート データ範囲を保持** – エクスポート対象のワークシート内にチャートのデータ ソースがあることを確認してください。シート間参照は PPTX では静的な値に変換されます。  
2. **最新の Aspose.Cells バージョンを使用** – 新しいリリースは追加のチャート機能サポートや PPTX エクスポートに関するエッジケースのバグ修正が含まれます。  
3. **出力を検証** – 変換後、PowerPoint で生成された PPTX を開き、チャート タイトル、系列、軸ラベルが編集可能か確認してください。要素が画像として表示された場合は、`ExportChartAsEditableText` が有効かつチャート タイプがサポート対象か再確認してください。  
4. **バッチ処理** – 多数の Excel レポートからスライド デッキを生成する自動化シナリオでは、`Workbook`、`int worksheetIndex`、`string outputPath` を受け取るメソッドに変換ロジックをラップすると便利です。これにより **export excel to powerpoint** ワークフローが分離され、再利用可能になります。

---

## 完全動作サンプルのまとめ

すべてを組み合わせた最小限のプログラムを以下に示します。新しい .NET コンソール プロジェクトにコピー＆ペーストして使用できます。

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Register license (optional but removes evaluation watermark)
            // var license = new License();
            // license.SetLicense("Aspose.Cells.lic");

            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";

            Workbook workbook = new Workbook(inputPath);

            ImageOrPrintOptions options = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,
                ExportChartAsEditableText = true,
                ExportShapeAsEditableText = true
            };

            workbook.Worksheets[0].ConvertToImage(options, outputPath);

            Console.WriteLine($"Export complete: {outputPath}");
        }
    }
}
```

**期待される結果**

* `Worksheet.pptx` という名前のファイルが `YOUR_DIRECTORY` に作成されます。  
* Microsoft PowerPoint でファイルを開くと、元のチャートとテキスト ボックスを含むスライドが表示されます。  
* チャートをダブルクリックすると PowerPoint のチャート エディタが開き、系列の値、色、軸タイトルなどを変更でき、**editable charts pptx** 機能が正しく動作していることが確認できます。

---

## 結論

これで **Excel を PowerPoint にエクスポート** し、チャートを編集可能に保つ完全なソリューションが手に入りました。`ImageOrPrintOptions` に `ExportChartAsEditableText` と `ExportShapeAsEditableText` を設定することで、変換プロセスは PowerPoint で直接作成したチャートと同様に動作するネイティブ PPTX ファイルを生成します。  

ここからは次のように活用できます:

* 複数のワークシートに対応するコードを拡張（各シートごとに **worksheet to PowerPoint**）。  
* スライド タイトルの追加や画像挿入など、他の Aspose.Cells 機能と組み合わせる。  
* カスタム テーマを適用した **export Excel chart PPTX** や、スライド デッキ全体の自動生成パイプラインの構築など、関連トピックを探求する。

さまざまなチャート タイプを試したり、データ ラベルを追加したり、このワークフローを大規模なレポーティング システムに統合したりして、自由に実験してみてください。Happy coding!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを基にした、密接に関連するトピックをカバーしています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、API の追加機能を習得したり、代替実装アプローチを自分のプロジェクトで試したりするのに役立ちます。

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}