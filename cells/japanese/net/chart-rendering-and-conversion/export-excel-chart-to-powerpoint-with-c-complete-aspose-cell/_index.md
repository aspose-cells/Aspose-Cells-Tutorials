---
category: general
date: 2026-08-04
description: C#でAspose.Cellsを使用してExcelのチャートをPowerPointにエクスポートします。ステップバイステップのExcelからPowerPointへの変換ガイドに従い、シェイプを編集可能なままに保ちます。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel chart to powerpoint
- Aspose.Cells PPTX export
- editable shapes in PowerPoint
- Excel to PowerPoint conversion
- C# chart export
language: ja
lastmod: 2026-08-04
og_description: C#でAspose.Cellsを使用してExcelのチャートをPowerPointにエクスポートします。編集可能なPPTXの作成方法、チャートデータの保持、ExcelからPowerPointへの変換を自動化する方法を学びましょう。
og_image_alt: Screenshot of an Excel chart rendered as an editable PowerPoint slide
og_title: C#でExcelチャートをPowerPointにエクスポート – 完全なAspose.Cellsチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  headline: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  type: TechArticle
- description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  name: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  steps:
  - name: Expected output
    text: '| File name | Content on slide | |--------------------------|------------------------------------------|
      | `ShapesExport.pptx` | The chart from `Shapes.xlsx` rendered as an editable
      PowerPoint chart, with axis labels, legends, and data series intact. |'
  - name: Exporting multiple worksheets
    text: If you need a slide for each worksheet, loop through `workbook.Worksheets`
      and call `Save` with a unique file name for each iteration.
  - name: Controlling slide layout
    text: Aspose.Slides lets you add a custom slide layout after the export. Create
      a new presentation, import the generated slide, and then apply a master theme.
  - name: Handling charts with external data sources
    text: If a chart references a data range outside the defined print area, extend
      the `PrintArea` to include those cells. Otherwise the chart may lose data series
      during export.
  - name: Licensing considerations
    text: 'Aspose libraries work in evaluation mode with a watermark. To remove the
      watermark, set the license before any API call:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- PowerPoint
title: C#でExcelチャートをPowerPointにエクスポート – 完全なAspose.Cellsガイド
url: /ja/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Excel チャートを PowerPoint にエクスポート – 完全な Aspose.Cells ガイド

**Excel チャートを PowerPoint にエクスポート** が必要な場合、このチュートリアルでは C# で Aspose.Cells と Aspose.Slides を使用してその方法を示します。チャートデータとシェイプを保持した完全に編集可能な PPTX が取得でき、変換後すぐにデザイン作業を続けられます。

Excel から PowerPoint へのチャートのエクスポートは、レポート自動化パイプライン、営業資料、トレーニング教材を作成する際の一般的な要件です。このガイドでは、すべてのチャート要素が編集可能な **Excel から PowerPoint への変換** を実行する正確な手順を学びます。手動のコピー＆ペーストは不要で、コードは .NET 6+ と従来の .NET Framework の両方で動作します。

## 前提条件

- 有効な Aspose.Cells ライセンス（または無料評価キー）  
- プロジェクトに追加された Aspose.Slides for .NET（ライブラリは PPTX 出力を処理します）  
- .NET 6 SDK 以降がインストールされていること  
- 少なくとも 1 つのチャートを含む Excel ワークブック（この例では `Shapes.xlsx` を使用）  

以下のコマンドで NuGet パッケージをインストールできます。

```bash
dotnet add package Aspose.Cells
dotnet add package Aspose.Slides
```

## 手順 1: Excel ワークブックをロードする

最初の操作は、エクスポートしたいチャートを含むワークブックを開くことです。`Workbook` クラスは Excel ファイル全体を表します。

```csharp
using Aspose.Cells;
using Aspose.Slides;   // required for PPTX output

// Load the Excel workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

**この重要性:** ワークブックをロードすると、ワークシート、チャート、書式設定にアクセスできます。Aspose.Cells は Microsoft Office のインストールを必要とせずにファイルを読み取るため、ソリューションが軽量でサーバーフレンドリーになります。

## 手順 2: ワークシートを選択し、印刷領域を定義する

ワークシートには多数のチャートが含まれることがありますが、通常は特定の領域だけをエクスポートします。`PrintArea` を設定することで、Aspose.Cells にどのセル（チャートを含む）をレンダリングすべきか指示できます。

```csharp
// Choose the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Define the area that contains the chart and any supporting data
worksheet.PageSetup.PrintArea = "A1:G30";
```

**この重要性:** 定義された印刷領域にエクスポートを限定することで、不要な空白スライドを防ぎ、PPTX ファイルサイズを小さく保ちます。領域はチャートの正確な範囲に合わせて調整可能です。

## 手順 3: 編集可能な PPTX 用にエクスポートオプションを設定する

Aspose.Cells は `ImageOrPrintOptions` クラスを使用して出力形式と編集可能性を制御します。`ImageFormat` を `ImageFormat.Pptx` に設定すると PowerPoint ファイルが作成され、`ExportEditableShapes = true` にするとチャートオブジェクトが編集可能なシェイプとして保持されます。

```csharp
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Pptx,   // Target format
    ExportEditableShapes = true       // Keep shapes/textboxes editable
};

// Attach the options to the worksheet's print settings
worksheet.PageSetup.PrintOptions = exportOptions;
```

**この重要性:** `ExportEditableShapes` フラグは **PowerPoint で編集可能なシェイプ** を得るための鍵です。これが無いと、チャートは画像としてラスタライズされ、後でデータポイントやスタイルを変更することができなくなります。

## 手順 4: ワークシートを PowerPoint プレゼンテーションとして保存する

最後に、`Workbook` オブジェクトの `Save` メソッドを呼び出します。`SaveFormat.Pptx` 列挙体は Aspose.Cells に PowerPoint ファイルを生成するよう指示します。

```csharp
// Export the selected worksheet to a PPTX file
workbook.Save("YOUR_DIRECTORY/ShapesExport.pptx", SaveFormat.Pptx);
```

コードの実行が完了したら、PowerPoint で `ShapesExport.pptx` を開きます。元の Excel チャートがネイティブな PowerPoint チャートオブジェクトとしてスライドに表示されます。チャートをダブルクリックするとデータを編集したり、色を変更したり、アニメーションを追加したりできます—まるで PowerPoint で直接チャートを作成したかのようです。

### 期待される出力

| ファイル名                | スライド上の内容                         |
|--------------------------|------------------------------------------|
| `ShapesExport.pptx`      | `Shapes.xlsx` のチャートが編集可能な PowerPoint チャートとして描画され、軸ラベル、凡例、データ系列がそのまま保持されています。 |

## 完全な実行可能サンプル

以下はコピー、貼り付け、実行できる完全なプログラムです。必要な `using` 文、エラーハンドリング、コメントがすべて含まれています。

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;   // Required for PPTX output

class ExcelToPowerPoint
{
    static void Main()
    {
        // Path to the source Excel file – adjust as needed
        const string excelPath = "YOUR_DIRECTORY/Shapes.xlsx";
        // Path for the generated PowerPoint file
        const string pptxPath = "YOUR_DIRECTORY/ShapesExport.pptx";

        try
        {
            // Load the workbook
            Workbook workbook = new Workbook(excelPath);

            // Use the first worksheet (you can change the index or name)
            Worksheet worksheet = workbook.Worksheets[0];

            // Define the area that contains the chart
            worksheet.PageSetup.PrintArea = "A1:G30";

            // Set export options for PPTX with editable shapes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Pptx,
                ExportEditableShapes = true
            };
            worksheet.PageSetup.PrintOptions = exportOptions;

            // Save as PPTX
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export successful. PPTX saved to: {pptxPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**各ブロックの説明**

| ブロック | 目的 |
|----------|------|
| `using` directives | Aspose.Cells と Aspose.Slides の名前空間をインポートします。 |
| `Workbook workbook = new Workbook(excelPath);` | Office がインストールされていなくても Excel ファイルをロードします。 |
| `worksheet.PageSetup.PrintArea = "A1:G30";` | チャートが含まれる領域にエクスポートを限定します。 |
| `ImageOrPrintOptions` | PPTX 出力を設定し、編集可能なシェイプを伴う **Aspose.Cells PPTX エクスポート** を有効にします。 |
| `workbook.Save(pptxPath, SaveFormat.Pptx);` | PowerPoint ファイルをディスクに書き込みます。 |
| `try / catch` | ファイルが見つからない場合やライセンス問題の基本的なエラーハンドリングを提供します。 |

このプログラムを実行すると、Microsoft PowerPoint、Google Slides（変換後）、または任意の互換ビューアで開ける PowerPoint スライドが生成されます。

## 一般的なバリエーションとエッジケース

### 複数ワークシートのエクスポート

各ワークシートごとにスライドが必要な場合、`workbook.Worksheets` をループし、各イテレーションで固有のファイル名を指定して `Save` を呼び出します。

```csharp
int index = 1;
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.PageSetup.PrintOptions = exportOptions;
    string fileName = $"Slide{index++}.pptx";
    workbook.Save(fileName, SaveFormat.Pptx);
}
```

### スライドレイアウトの制御

Aspose.Slides を使用すると、エクスポート後にカスタムスライドレイアウトを追加できます。新しいプレゼンテーションを作成し、生成されたスライドをインポートしてからマスターテーマを適用します。

```csharp
using Aspose.Slides.Export;

// Load the PPTX created by Aspose.Cells
Presentation pres = new Presentation(pptxPath);

// Apply a built‑in layout (e.g., Title and Content)
pres.Slides[0].LayoutSlide = pres.LayoutSlides[(int)SlideLayoutType.TitleAndContent];

// Save the final presentation
pres.Save("FinalPresentation.pptx", SaveFormat.Pptx);
```

### 外部データソースを使用するチャートの処理

チャートが定義された印刷領域外のデータ範囲を参照している場合、`PrintArea` を拡張してそのセルを含めてください。そうしないと、エクスポート時にデータ系列が失われる可能性があります。

### ライセンスに関する考慮事項

Aspose ライブラリは評価モードでは透かしが表示されます。透かしを除去するには、任意の API 呼び出しの前にライセンスを設定します：

```csharp
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

高度な機能を使用する場合は、Aspose.Slides についても同様にライセンスを設定してください。

## プロのコツ

- **Reuse export options:** 単一の `ImageOrPrintOptions` インスタンスを作成し、各ワークシートに割り当ててコードの重複を防ぎます。  
- **Batch processing:** 大規模なレポート作成の場合、このエクスポートロジックをバックグラウンドワーカーや Azure Function と組み合わせて、オンデマンドで PPTX ファイルを生成します。  
- **Performance:** `ExportEditableShapes = false` に設定すると、チャート画像のみが必要な場合にメモリ使用量が減り、変換が高速化します。  
- **Testing:** 生成された PPTX を Windows と macOS の PowerPoint 両方で確認し、プラットフォーム間で異なるレンダリングの問題がないかテストします。  

## 結論

これで C# を使用した **Excel チャートを PowerPoint にエクスポート** の完全なエンドツーエンドソリューションが手に入りました。このチュートリアルでは、ワークブックのロード、印刷領域の選択、**PowerPoint で編集可能なシェイプ** を伴う **Aspose.Cells PPTX エクスポート** の設定、そして完全に編集可能な PPTX ファイルとしての保存について説明しました。

ここからは、バッチエクスポート、カスタムスライドレイアウト、またはプロセスを Web API に統合するなど、追加の **Excel から PowerPoint への変換** シナリオを検討できます。さまざまなチャートタイプを試したり、画像を追加したり、複数のワークシートを単一のプレゼンテーションに結合して、ビジネスニーズに合わせた出力を作成してください。

レポートワークフローを自動化する準備はできましたか？ソースファイルを差し替え、印刷領域を調整し、コードを既存の .NET サービスに統合してみてください。コーディングを楽しんで！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.Cells for .NET を使用して Excel を PowerPoint に変換する方法：完全ガイド](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Aspose.Cells for .NET を使用して Excel チャートを PDF にエクスポートする方法：ステップバイステップガイド](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Aspose.Cells .NET を使用して Excel セルを画像にエクスポートする方法：ステップバイステップガイド](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}