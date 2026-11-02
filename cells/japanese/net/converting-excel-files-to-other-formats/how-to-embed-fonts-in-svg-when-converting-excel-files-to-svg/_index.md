---
category: general
date: 2026-09-15
description: SVGにフォントを埋め込む方法と、ExcelのチャートをPowerPointにエクスポートする方法を学びます。XLSXをSVGに変換する方法とXLSXをPPTXに変換する方法を、完全なコード例とともに解説します。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in SVG
- export excel chart to powerpoint
- convert xlsx to svg
- convert xlsx to pptx
- save workbook as svg
language: ja
lastmod: 2026-09-15
og_description: SVGにフォントを埋め込み、Excel のチャートを PowerPoint にエクスポートするステップバイステップの C# コード。XLSX
  を SVG に、XLSX を PPTX に迅速かつ確実に変換。
og_image_alt: Screenshot showing an Excel chart exported to PowerPoint with embedded
  fonts in the resulting SVG file
og_title: SVGにフォントを埋め込み、ExcelのチャートをPowerPointにエクスポートする完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  headline: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  type: TechArticle
- description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  name: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  steps:
  - name: Open `EditableChart.pptx` in PowerPoint.
    text: Open `EditableChart.pptx` in PowerPoint.
  - name: Locate the slide containing the chart.
    text: Locate the slide containing the chart.
  - name: Choose **Chart Tools → Design → Edit Data**.
    text: Choose **Chart Tools → Design → Edit Data**.
  - name: Confirm that the Excel‑style data grid appears and that you can change values.
    text: Confirm that the Excel‑style data grid appears and that you can change values.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Excel ファイルを SVG および PowerPoint に変換する際の、SVG へのフォント埋め込み方法
url: /ja/net/converting-excel-files-to-other-formats/how-to-embed-fonts-in-svg-when-converting-excel-files-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel ファイルを SVG および PowerPoint に変換する際の SVG へのフォント埋め込み方法  

If you need to **embed fonts in SVG** while converting an Excel workbook, this guide shows you exactly how to do it. You’ll also learn how to **export Excel chart to PowerPoint**, and how to **convert XLSX to SVG** and **convert XLSX to PPTX** with editable charts.  

Excel ワークブックを変換する際に **SVG にフォントを埋め込む** 必要がある場合、このガイドでその手順を正確に示します。また、**Excel のチャートを PowerPoint にエクスポートする方法**、**XLSX を SVG に変換する方法**、そして **XLSX を PPTX に変換して編集可能なチャートを保持する方法** も学べます。  

Working with Excel data programmatically often means you have to move the same visual content between different file formats. Manually recreating a chart in PowerPoint or re‑applying fonts in an SVG is error‑prone and time‑consuming. By the end of this tutorial you will have a single, reusable C# snippet that:

Excel データをプログラムで扱う場合、同じビジュアルコンテンツを異なるファイル形式間で移動させる必要があることがよくあります。PowerPoint でチャートを手動で再作成したり、SVG でフォントを再適用したりするのはミスが起きやすく、時間がかかります。このチュートリアルの最後までに、単一で再利用可能な C# スニペットを手に入れることができます。

* フォントとフォントバリエーションセレクタが埋め込まれた SVG ファイルとしてワークブックを保存します。  
* 同じワークブックを PPTX ファイルにエクスポートし、チャートが編集可能な状態を保持します。  

The only prerequisite is a recent version of **Aspose.Cells for .NET** (2024‑x or later) and a .NET development environment such as Visual Studio 2022.

必要条件は、最新バージョンの **Aspose.Cells for .NET**（2024‑x 以降）と、Visual Studio 2022 などの .NET 開発環境だけです。

---

## 必要なもの  

* .NET 6.0 以降（コードは .NET Framework 4.8 でも動作します）。  
* Aspose.Cells for .NET NuGet パッケージ（`Install-Package Aspose.Cells`）。  
* 少なくとも 1 つのチャートを含む Excel ファイル（`input.xlsx`）。  
* 出力ディレクトリへの書き込み権限。  

## XLSX を SVG に変換する際の SVG へのフォント埋め込み  

Embedding fonts ensures that the SVG renders correctly on any device, even if the target system lacks the original typefaces. The `SvgSaveOptions` class provides two flags that make this possible: `EmbedFonts` and `FontVariationSelectors`.

フォントを埋め込むことで、対象システムに元のフォントがなくても、SVG がどのデバイスでも正しく表示されます。`SvgSaveOptions` クラスは、この機能を実現するための 2 つのフラグ `EmbedFonts` と `FontVariationSelectors` を提供します。

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// OPTIONAL: Use WRAPCOLS to reshape data before export (demonstrates a formula)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)"; // 2 columns per wrap
sheet.Calculate(); // Force calculation so the formula result appears

// Configure SVG options to embed fonts
SvgSaveOptions svgOptions = new SvgSaveOptions
{
    EmbedFonts = true,                // embed fonts in the SVG
    FontVariationSelectors = true    // include variation selectors for better Unicode handling
};

// Save the workbook as an SVG file
string svgPath = @"YOUR_DIRECTORY\WithFonts.svg";
workbook.Save(svgPath, svgOptions);
```

**この動作の理由:**  
* `EmbedFonts = true` はフォントファイルを SVG の `<defs>` セクションにコピーし、外部依存を排除します。  
* `FontVariationSelectors = true` は OpenType 機能をサポートするフォント用の必要なセレクタを追加し、合字などのグリフバリエーションを保持します。  

**期待される結果:** 任意の最新ブラウザで `WithFonts.svg` を開くと、チャートやセル内のテキストが Excel で使用されたフォントと同一の書体で表示され、フォントがインストールされていないマシンでも同様に表示されます。  

## 編集可能なチャートとして Excel のチャートを PowerPoint にエクスポート  

When you need to embed a chart into a PowerPoint slide but still allow the recipient to edit the chart data, Aspose.Cells’ `PptxSaveOptions` offers the `ExportEditableChart` flag.

チャートを PowerPoint のスライドに埋め込みつつ、受取側がチャートデータを編集できるようにしたい場合、Aspose.Cells の `PptxSaveOptions` が `ExportEditableChart` フラグを提供します。

```csharp
// Configure PPTX options to keep charts editable after export
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableChart = true   // allow chart editing in PowerPoint
};

// Save the same workbook as a PPTX file
string pptxPath = @"YOUR_DIRECTORY\EditableChart.pptx";
workbook.Save(pptxPath, pptxOptions);
```

**この重要性:**  
`ExportEditableChart` を `true` に設定すると、チャートは静的画像ではなく Office Open XML のチャートオブジェクトとして保存されます。PowerPoint で `EditableChart.pptx` を開くと、チャートを右クリック → **Edit Data** で、ネイティブの PowerPoint チャートと同様に系列を編集できます。

**検証手順:**  

1. PowerPoint で `EditableChart.pptx` を開く。  
2. チャートが含まれるスライドを探す。  
3. **Chart Tools → Design → Edit Data** を選択する。  
4. Excel 形式のデータグリッドが表示され、値を変更できることを確認する。  

## XLSX を SVG に変換 – フルワークフローのまとめ  

Below is a compact version that combines loading, optional data manipulation, and saving as SVG. Use this when you only need the SVG output.

以下は、ロード、オプションのデータ操作、SVG への保存を組み合わせたコンパクトなバージョンです。SVG 出力だけが必要な場合に使用してください。

```csharp
public void ConvertXlsxToSvg(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Example: apply a formula to demonstrate cell calculations
    Worksheet ws = wb.Worksheets[0];
    ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
    ws.Calculate();

    SvgSaveOptions opts = new SvgSaveOptions
    {
        EmbedFonts = true,
        FontVariationSelectors = true
    };

    wb.Save(outputPath, opts);
}
```

メソッドは次のように呼び出します:

```csharp
ConvertXlsxToSvg(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.svg");
```

**エッジケースのヒント:** ワークブックにサーバーにインストールされていないカスタムフォントが含まれている場合、`Save` を呼び出す前に手動で埋め込んでください。`FontInfoCollection` を使用してフォントファイルを `SvgSaveOptions` の `CustomFonts` プロパティに追加します（新しい Aspose.Cells リリースで利用可能）。  

## XLSX を PPTX に変換 – チャートの編集可能性を保持  

The following helper method demonstrates the **convert XLSX to PPTX** path while ensuring the chart remains editable.

以下のヘルパーメソッドは、**XLSX を PPTX に変換** する際にチャートが編集可能なままになることを示しています。

```csharp
public void ConvertXlsxToPptx(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Ensure any chart you want to keep editable is on the first worksheet
    // (Aspose.Cells exports only the first worksheet by default for PPTX)
    PptxSaveOptions opts = new PptxSaveOptions
    {
        ExportEditableChart = true
    };

    wb.Save(outputPath, opts);
}
```

使用方法:

```csharp
ConvertXlsxToPptx(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.pptx");
```

**よくある質問:** *ワークブックに複数のワークシートがあり、各シートにチャートがある場合はどうすればよいですか？*  
**回答:** Aspose.Cells はデフォルトで最初のワークシートのみをエクスポートします。追加のシートを含めるには、`workbook.Worksheets` を反復処理し、各チャートを新しいスライドにコピーし、Aspose.Slides の `Presentation` オブジェクトを使用して各スライドを個別に保存します。この高度なシナリオは、基本的な「ワークブックを SVG として保存」および「Excel チャートを PowerPoint にエクスポート」フローを超えますが、コアフラグは同じままです。  

## 実用的なヒントと落とし穴  

* **Performance:** フォントを埋め込むと SVG ファイルサイズが増加します。サイズが問題になる場合は `EmbedFonts = false` に設定し、ウェブセーフフォントに依存してください。  
* **Font licensing:** 使用するフォントを埋め込む権利があることを確認してください。商用フォントの中には埋め込みを制限するものがあります。  
* **Chart compatibility:** 編集可能なチャートは PPTX 内の `chart.xml` パーツとして保存されます。非常に複雑なチャート（例：3D チャートやコンボチャート）は、PowerPoint で編集すると一部のスタイルが失われる可能性があります。必要な主要なチャートタイプでテストしてください。  
* **Version mismatches:** `ExportEditableChart` フラグは Aspose.Cells 20.10 以降が必要です。古いバージョンを使用すると、静止画像に自動的にフォールバックします。  
* **Thread safety:** Workbook オブジェクトはスレッドセーフではありません。Web サービスシナリオではリクエストごとに新しい `Workbook` インスタンスを作成してください。  

## 完全なエンドツーエンド例  

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class ExcelExportDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputFile = @"YOUR_DIRECTORY\input.xlsx";
        string svgFile   = @"YOUR_DIRECTORY\WithFonts.svg";
        string pptxFile  = @"YOUR_DIRECTORY\EditableChart.pptx";

        // 1. Load workbook
        Workbook workbook = new Workbook(inputFile);

        // 2. Optional: reshape data using WRAPCOLS
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
        sheet.Calculate();

        // 3. Save as SVG with embedded fonts
        SvgSaveOptions svgOpts = new SvgSaveOptions
        {
            EmbedFonts = true,
            FontVariationSelectors = true
        };
        workbook.Save(svgFile, svgOpts);
        Console.WriteLine($"SVG saved with embedded fonts to: {svgFile}");

        // 4. Save as PPTX with editable chart
        PptxSaveOptions pptxOpts = new PptxSaveOptions
        {
            ExportEditableChart = true
        };
        workbook.Save(pptxFile, pptxOpts);
        Console.WriteLine($"PPTX saved with editable chart to: {pptxFile}");
    }
}
```

このプログラムを実行すると、次の 2 つのファイルが生成されます:

* **WithFonts.svg** – Excel の表示と同様に正確にレンダリングされ、フォントが埋め込まれた SVG。  
* **EditableChart.pptx** – チャートを直接編集できる PowerPoint プレゼンテーション。  

## 結論  

You now know how to **embed fonts in SVG** when you **convert XLSX to SVG**, and how to **export Excel chart to PowerPoint** while keeping the chart editable. The same code also demonstrates a clean way to **save workbook as SVG** and **convert XLSX to PPTX** with minimal effort.  

これで、**XLSX を SVG に変換する際に SVG にフォントを埋め込む** 方法と、**Excel のチャートを PowerPoint にエクスポートし、チャートを編集可能なままに保つ** 方法が分かりました。同じコードは、**ワークブックを SVG として保存** し、**XLSX を PPTX に変換** して最小限の手間でチャートの編集可能性を保持するクリーンな方法も示しています。  

ここからは、以下のようなトピックをさらに探求できます:

* プログラムでカスタムフォントを追加する (`svgOptions.CustomFonts`)。  
* バックグラウンドサービスで複数のワークブックをバッチ処理する。  
* Aspose.Slides を使用して、複数の Excel チャートを組み合わせたマルチスライド PPTX ファイルを作成する。  

オプションを試し、スニペットをプロジェクトに合わせて調整し、手動の後処理なしで信頼性の高い Excel から SVG/PPTX への変換を楽しんでください。コーディングを楽しんで！

## 次に学ぶべきことは？

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックをカバーしています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.Cells for .NET を使用した Excel チャートの SVG 変換方法（ステップバイステップガイド）](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Excel チャートを SVG に変換する Aspose Cells .NET](/cells/german/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Excel チャートを SVG に変換する Aspose Cells .NET](/cells/french/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}