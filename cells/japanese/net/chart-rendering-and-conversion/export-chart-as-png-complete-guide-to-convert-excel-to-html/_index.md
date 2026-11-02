---
category: general
date: 2026-06-30
description: Aspose.Cells を使用して Excel を HTML に変換する際に、チャートを PNG としてエクスポートします。画像を Base64
  で埋め込む方法と、数分でブックを HTML として保存する方法を学びましょう。
draft: false
keywords:
- export chart as png
- convert excel to html
- embed images as base64
- save workbook as html
- export excel chart to png
language: ja
og_description: Excel を HTML に変換する際に、チャートを PNG としてエクスポートし、画像を Base64 で埋め込みます。ステップバイステップの
  C# チュートリアルに従って、ブックを簡単に HTML として保存しましょう。
og_title: チャートをPNGとしてエクスポート – Aspose.CellsでExcelをHTMLに変換
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Export chart as PNG while you convert Excel to HTML using Aspose.Cells.
    Learn to embed images as Base64 and save workbook as HTML in minutes.
  headline: Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Export chart as PNG while you convert Excel to HTML using Aspose.Cells.
    Learn to embed images as Base64 and save workbook as HTML in minutes.
  name: Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells
  steps:
  - name: Open Visual Studio and create a new **Console App** (`dotnet new console`).
    text: Open Visual Studio and create a new **Console App** (`dotnet new console`).
  - name: 'Add the Aspose.Cells NuGet package:'
    text: 'Add the Aspose.Cells NuGet package:'
  - name: '(Optional) If you have a license file, place it in the project root and
      activate it at runtime:'
    text: '(Optional) If you have a license file, place it in the project root and
      activate it at runtime:'
  - name: Open the generated HTML in Chrome. Right‑click the chart image and select
      **Open image in new tab**. The URL will still start with `data:image/png;base64,`.
    text: Open the generated HTML in Chrome. Right‑click the chart image and select
      **Open image in new tab**. The URL will still start with `data:image/png;base64,`.
  - name: 'If the image appears blurry, consider increasing the chart’s resolution
      before saving:'
    text: 'If the image appears blurry, consider increasing the chart’s resolution
      before saving:'
  - name: 'For charts that rely on external data sources, make sure the workbook is
      fully refreshed before saving:'
    text: 'For charts that rely on external data sources, make sure the workbook is
      fully refreshed before saving:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: チャートをPNGでエクスポート – Aspose.CellsでExcelをHTMLに変換する完全ガイド
url: /ja/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# チャートをPNGとしてエクスポート – Aspose.CellsでExcelをHTMLに変換する完全ガイド

Excelブックから **チャートをPNGとしてエクスポート** しながら、シート全体をきれいでレスポンシブなHTMLに変換したいと考えたことはありませんか？ あなただけではありません。多くの開発者が、画像ファイルを別々に管理せずにチャートを表示できるウェブ対応レポートを作成しようとして壁にぶつかります。良いニュースは、Aspose.Cells を使えばこの作業がとても簡単になることです。

このチュートリアルでは、**ExcelをHTMLに変換**し、**画像をBase64で埋め込み**、最終的に **ワークブックをHTMLとして保存** する手順を詳しく解説します。すべてのチャートがPNG画像として保存されます。最後には、任意のウェブページに貼り付けられる単一のHTMLファイルが完成し、追加のアセットは不要です。

## 学べること

- 既にチャートが含まれている既存のワークブックの読み込み方法  
- 画像エクスポート、チャート形式、レスポンシブ対応を制御する `HtmlSaveOptions` のフラグ  
- **チャートをPNGとしてエクスポート** し、PNGをBase64文字列として埋め込むための正確なコード  
- **ワークブックをHTMLとして保存** するシンプルなメソッド呼び出し  
- チャート画像が欠落したり、Base64文字列が大きすぎるといった一般的な落とし穴の対処法  

**前提条件:**  
- .NET 6+（または .NET Framework 4.6+）がインストールされていること  
- 有効な Aspose.Cells ライセンス（または一時評価キー）  
- C# と Visual Studio（またはお好みのIDE）の基本的な知識  

これらに心当たりがない場合は、一度立ち止まって環境を整えてください。以降の手順はそれらが準備できていることを前提としています。

---

## 手順 1: プロジェクトをセットアップし Aspose.Cells をインストール

**チャートをPNGとしてエクスポート** する前に、Aspose.Cells ライブラリを参照する C# プロジェクトが必要です。

1. Visual Studio を開き、**コンソール アプリ**（`dotnet new console`）を新規作成します。  
2. Aspose.Cells の NuGet パッケージを追加します:

```bash
dotnet add package Aspose.Cells
```

3. （オプション）ライセンス ファイルがある場合は、プロジェクトのルートに配置し、実行時に有効化します:

```csharp
// Activate license – skip this line if you’re using the trial version
Aspose.Cells.License license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

> **プロのコツ:** ライセンス ファイルはソース管理に含めないでください。本番環境では環境変数や安全なシークレットストアを使用しましょう。

---

## 手順 2: チャートが含まれるワークブックを読み込む

次に、**チャートをPNGとしてエクスポート** したい Excel ファイルを読み込みます。

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;   // Needed for ImageFormat enum

// Path to the source workbook – change this to your actual file location
string sourcePath = @"C:\Reports\ReportWithChart.xlsx";

// Load the workbook
Workbook workbook = new Workbook(sourcePath);
```

> **なぜ重要か:** ワークブックを早めに読み込むことで、すべてのワークシート、チャート、埋め込みオブジェクトにアクセスできます。読み込みに失敗すると、以降の **チャートをPNGにエクスポート** 手順は実行されません。

---

## 手順 3: HTML 保存オプションを構成

ソリューションの核心は `HtmlSaveOptions` にあります。いくつかのプロパティを切り替えるだけで次のことが可能です:

- **ExportChartImageFormat = ImageFormat.Png** → すべてのチャートが PNG になることを保証  
- **ExportImagesAsBase64 = true** → PNG データを HTML に直接埋め込み、外部ファイルを不要に  
- **IsResponsive = true** → 生成されたテーブルがモバイル画面に適応  
- **ExportPrintingHeadersFooters = false** → 不要な印刷メタデータを除去  

完全な設定は以下の通りです:

```csharp
// Create HTML save options and fine‑tune them
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // 1️⃣ Embed PNG/JPEG images directly as Base64 strings
    ExportImagesAsBase64 = true,

    // 2️⃣ Force chart images to be saved as PNG files
    ExportChartImageFormat = ImageFormat.Png,

    // 3️⃣ Omit printing headers/footers for a cleaner web view
    ExportPrintingHeadersFooters = false,

    // 4️⃣ Generate responsive tables for mobile friendliness
    IsResponsive = true,

    // 5️⃣ Target modern browsers with HTML5
    HtmlVersion = HtmlVersion.Html5
};
```

### なぜこれらの設定か？

- **ExportChartImageFormat = ImageFormat.Png** は、ロスレスでウェブ対応のチャート画像を保証する唯一の方法です。  
- **ExportImagesAsBase64 = true** にすると、**画像をBase64で埋め込む** ことができ、メールレポートや単一ファイル配布に最適です。  
- **IsResponsive = true** は、スマートフォンでテーブルがはみ出すという一般的な不満を解消します。  
- **ExportPrintingHeadersFooters = false** により、HTML が軽量化され、ウェブ上で使われない隠れた印刷情報が除去されます。

---

## 手順 4: ワークブックを HTML として保存

オプション設定が完了したら、以下の 1 行で **Excel を HTML に変換** し、裏で **チャートをPNGとしてエクスポート** が行われます。

```csharp
// Destination HTML file – adjust the folder as needed
string outputPath = @"C:\Reports\Report.html";

// Save the workbook using the configured options
workbook.Save(outputPath, htmlOptions);
```

この行が完了すると、`Report.html` というファイルが生成されます。任意のブラウザで開くと、次のように表示されます:

- ワークシートのデータがきれいな HTML テーブルとしてレンダリング  
- すべてのチャートがインライン PNG 画像として表示（Base64 埋め込みのおかげ）  
- HTML の隣に余分な画像ファイルは存在しません  

### 期待される出力

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Report</title>
    <style>
        /* Aspose.Cells generated responsive CSS */
    </style>
</head>
<body>
    <table class="aspose">
        <!-- Table rows here -->
    </table>

    <!-- Example of an embedded chart image -->
    <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAA..." alt="Chart 1" />
</body>
</html>
```

`src="data:image/png;base64,..."` 属性に注目してください。これが **画像をBase64で埋め込む** マジックです。ディスク上に別個の `.png` ファイルは作成されません。

---

## 手順 5: PNG エクスポートを確認し、必要に応じて調整

カスタムフォントや複雑なグラデーションを使用している場合、変換後にチャートが若干ずれることがあります。以下の手順で確認してください:

1. Chrome で生成された HTML を開き、チャート画像を右クリックして **新しいタブで画像を開く** を選択します。URL は依然として `data:image/png;base64,` で始まります。  
2. 画像がぼやけている場合は、保存前にチャートの解像度を上げてみてください:

```csharp
htmlOptions.ImageResolution = 300; // DPI – higher values = sharper PNGs
```

3. 外部データ ソースに依存するチャートの場合、保存前にワークブックを完全にリフレッシュしてください:

```csharp
workbook.CalculateFormula(); // Force recalculation
```

これらの調整により、**Excel のチャートを PNG にエクスポート** するステップで、鮮明で本番環境向けのグラフィックが得られます。

---

## 手順 6: HTML を任意の場所にデプロイ

すべての画像が埋め込まれているため、次のことが可能です:

- HTML を単一の添付ファイルとしてメール送信  
- 生コードを受け付ける CMS に貼り付け  
- 静的サイトにホストし、PNG ファイルが欠ける心配なし  

別途 PNG ファイルが必要な場合（例: 後で PDF に変換したい場合）は、`ExportImagesAsBase64` を `false` に変更し、`HtmlSaveOptions` で画像出力フォルダーを指定してください。

```csharp
htmlOptions.ExportImagesAsBase64 = false;
htmlOptions.ImageFolder = @"C:\Reports\Images";
```

これで HTML は外部 PNG ファイルを参照するようになり、**チャートをPNGとしてエクスポート** はそのままに、他の用途向けに個別画像を取得できます。

---

## よくある落とし穴と回避策

| 症状 | 考えられる原因 | 対処法 |
|------|----------------|--------|
| HTML にチャートが表示されない | `ExportChartImageFormat` がデフォルト（`Jpeg`）のままで、ブラウザが混在コンテンツをブロック | `ExportChartImageFormat = ImageFormat.Png` を設定 |
| HTML ファイルが巨大（数 MB） | 多数の高解像度画像が Base64 で埋め込まれている | `htmlOptions.ImageResolution` を下げるか、Excel 側でチャートを圧縮 |
| モバイルでテーブルがはみ出す | `IsResponsive` が有効になっていない | `HtmlSaveOptions` で `IsResponsive = true` を確認 |
| Base64 文字列に改行が入る | 古い .NET バージョンが長い文字列を折り返す | .NET 6+ にアップグレード、または `htmlOptions.ExportBase64StringInOneLine = true` を設定 |

---

## ボーナス: 再利用可能なメソッドにまとめる

この変換を頻繁に行う場合は、ロジックをメソッド化すると便利です:

```csharp
public static void ConvertExcelToHtmlWithPngCharts(string excelPath, string htmlPath)
{
    // Load workbook
    Workbook wb = new Workbook(excelPath);

    // Prepare options
    HtmlSaveOptions opts = new HtmlSaveOptions
    {
        ExportImagesAsBase64 = true,
        ExportChartImageFormat = ImageFormat.Png,
        ExportPrintingHeadersFooters = false,
        IsResponsive = true,
        HtmlVersion = HtmlVersion.Html5,
        ImageResolution = 150 // reasonable default DPI
    };

    // Force recalculation for up‑to‑date charts
    wb.CalculateFormula();

    // Save as HTML
    wb.Save(htmlPath, opts);
}
```

これで `ConvertExcelToHtmlWithPngCharts(@"C:\Reports\MyFile.xlsx", @"C:\Reports\MyFile.html");` をコードベースのどこからでも呼び出せます。

---

## 結論

**チャートをPNGとしてエクスポート** しながら **Excel を HTML に変換**、**画像を Base64 で埋め込み**、そして **ワークブックを HTML として保存** する方法をマスターしました。ポイントは、適切に設定された数個の `HtmlSaveOptions` により、単一の自己完結型 HTML ファイルが作成でき、デバイスを問わず動作することです。余計な PNG ファイルやフォルダー構造は不要です。

次のステップに挑戦してみませんか？この手法を **PDF 生成用の Excel チャートエクスポート** と組み合わせたり、カスタム CSS でテーブルの見た目をさらに調整したりしてみましょう。データとプレゼンテーションをプログラムで自在にコントロールすれば、可能性は無限です。

質問や問題があればコメントで教えてください。また、このパターンを自分のプロジェクトでどのように活用したかシェアしていただけると嬉しいです。Happy coding!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、完全なコード例とステップバイステップの解説が含まれており、API の追加機能を習得したり、別の実装アプローチを探求したりするのに役立ちます。

- [Export Excel to HTML Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/export-excel-html-aspose-cells-net/)
- [Export Excel to HTML Without Frame Scripts Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-to-html-aspose-cells-net/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}