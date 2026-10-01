---
category: general
date: 2026-10-01
description: Aspose.Cells を使用して Excel を HTML に変換する際に、HTML にフォントを埋め込む方法を学びましょう。数ステップでフォントが埋め込まれた
  HTML として Excel をエクスポートできます。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- convert excel to html
- embed fonts in html
- how to export excel
- export excel as html
language: ja
lastmod: 2026-10-01
og_description: Excelファイルをエクスポートする際にHTMLにフォントを埋め込む方法。ステップバイステップのガイドに従って、フォントが埋め込まれたHTMLへExcelを変換しましょう。
og_image_alt: Screenshot of Aspose.Cells code embedding fonts in exported HTML
og_title: ExcelからHTMLへフォントを埋め込む方法 – Aspose.Cells ガイド
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  headline: How to embed fonts when converting Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  name: How to embed fonts when converting Excel to HTML with Aspose.Cells
  steps:
  - name: 'Edge case: unsupported fonts'
    text: If the workbook uses a font that is not installed on the server, Aspose.Cells
      falls back to a default system font. To avoid this, install the required fonts
      on the server or embed them manually after export.
  - name: Converting multiple worksheets
    text: If you need to **convert Excel to HTML** for all worksheets, set `ExportActiveWorksheetOnly
      = false` (the default). Aspose.Cells will create a separate HTML file for each
      sheet.
  - name: Controlling CSS output
    text: 'You can reduce the HTML size by disabling inline CSS:'
  - name: Using a stream instead of a file
    text: 'When integrating into a web API, write the HTML to a `MemoryStream` and
      return it directly:'
  type: HowTo
tags:
- Aspose.Cells
- .NET
- Excel conversion
title: Aspose.CellsでExcelをHTMLに変換する際にフォントを埋め込む方法
url: /ja/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-converting-excel-to-html-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells を使用して Excel を HTML に変換する際にフォントを埋め込む方法

Excel ワークブックを HTML に変換する際にフォントを埋め込むことは、ブラウザ間で元の外観を保つために重要です。カスタムフォントを保持したまま Excel を HTML に変換したい場合、本ガイドではその完全な手順を示します。また、Excel を HTML としてエクスポートする方法と、HTML にフォントを埋め込むことが一貫したレンダリングにとってなぜ重要かも解説します。

このチュートリアルでは、必要なライブラリ、コード設定、生成された HTML ファイルの検証方法をすべて網羅しています。最後まで読めば、数行の C# コードでフォントが埋め込まれた HTML として Excel をエクスポートできるようになります。

## 必要なもの

開始する前に、以下をご用意ください。

* **.NET 6.0 以降** – コードは .NET 6 を対象としていますが、Aspose.Cells がサポートする任意の .NET バージョンで動作します。  
* **Aspose.Cells for .NET** – ライセンスを取得するか、Aspose のウェブサイトから無料評価版を使用してください。  
* **C# 開発環境**（Visual Studio、Rider、または VS Code） – .NET プロジェクトをコンパイルできる IDE があれば OK です。  
* カスタムフォントが使用されている Excel ワークブック（`Styled.xlsx`）  

## 手順 1: .NET プロジェクトに Aspose.Cells を設定する

まず、プロジェクトに Aspose.Cells NuGet パッケージを追加します。

```bash
dotnet add package Aspose.Cells
```

次に、C# ファイルの先頭で名前空間をインポートします。

```csharp
using Aspose.Cells;
```

パッケージを追加することで、`Workbook`、`HtmlSaveOptions`、および関連クラスが利用可能になります。

## 手順 2: Excel ワークブックを読み込む

ワークブックの読み込みは、**Excel データをエクスポートする方法** の最初の具体的なステップです。`Workbook` コンストラクタはディスク上のファイルを読み取ります。

```csharp
// Step 1: Load the Excel workbook
var workbook = new Workbook("YOUR_DIRECTORY/Styled.xlsx");
```

*重要ポイント:* Aspose.Cells はワークブックを解析し、セルのスタイル、数式、フォント情報を取得します。ファイルが見つからない場合は例外がスローされるため、パスが正しいことを確認してください。

## 手順 3: フォント埋め込み用に HTML 保存オプションを構成する

**HTML にフォントを埋め込む** コアは `HtmlSaveOptions` クラスです。`EmbedFonts` を `true` に設定すると、ワークブックで使用されたすべてのフォントが Base64 エンコードされた `@font-face` ルールとして HTML 出力に書き込まれます。

```csharp
// Step 2: Set HTML save options to embed fonts in the output
var htmlOptions = new HtmlSaveOptions
{
    EmbedFonts = true,
    // Optional: keep the original worksheet name as the HTML file name
    ExportActiveWorksheetOnly = true
};
```

*重要ポイント:* デフォルトでは Aspose.Cells は外部フォントファイルへの参照を出力しますが、クライアントマシンにそのフォントが無い場合は正しく表示されません。`EmbedFonts` を有効にすると、閲覧者の環境に依存せず、元の Excel シートと同一の外観で HTML がレンダリングされます。

### エッジケース: サポートされていないフォント

サーバーにインストールされていないフォントがワークブックで使用されている場合、Aspose.Cells はデフォルトのシステムフォントにフォールバックします。この問題を回避するには、サーバーに必要なフォントをインストールするか、エクスポート後に手動で埋め込んでください。

## 手順 4: 設定したオプションでワークブックを HTML として保存する

`Save` メソッドに出力パスと `HtmlSaveOptions` インスタンスを渡すだけで、HTML ファイルを書き出せます。

```csharp
// Step 3: Save the workbook as an HTML file using the configured options
workbook.Save("YOUR_DIRECTORY/Styled.html", htmlOptions);
```

実行後、`Styled.html` にはスプレッドシートデータと、各カスタムフォント用の Base64 エンコードされた `@font-face` 定義が `<style>` ブロックとして含まれます。

## 手順 5: 埋め込まれたフォントを検証する

ブラウザで `Styled.html` を開き、`<head>` セクションを確認してください。以下のような記述が見えるはずです。

```html
<style>
@font-face {
    font-family: 'Calibri';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
}
...
</style>
```

テーブルが正しくフォントで表示されていれば埋め込みは成功です。文字が欠けている場合は、変換を実行したマシンに元フォントがインストールされているか再確認してください。

## よくあるバリエーションと追加オプション

### 複数シートの変換

すべてのシートを **Excel を HTML に変換** したい場合は、`ExportActiveWorksheetOnly = false`（デフォルト）を設定します。Aspose.Cells はシートごとに別々の HTML ファイルを作成します。

```csharp
htmlOptions.ExportActiveWorksheetOnly = false;
workbook.Save("YOUR_DIRECTORY/AllSheets.html", htmlOptions);
```

### CSS 出力の制御

インライン CSS を無効にすると HTML のサイズを削減できます。

```csharp
htmlOptions.ExportCssSeparately = true; // Generates a .css file alongside the .html
```

### ファイルではなくストリームを使用する

Web API に組み込む場合は、`MemoryStream` に HTML を書き込み、直接返却します。

```csharp
using var stream = new MemoryStream();
workbook.Save(stream, htmlOptions);
stream.Position = 0; // Reset for reading
// Return stream as a file download in ASP.NET Core
```

## プロのコツ: 評価版の透かしを除去するにはライセンスを適用する

評価版を使用していると、生成された HTML に透かしコメントが入ることがあります。ワークブックを読み込む前に Aspose.Cells のライセンスを適用すれば、透かしのないクリーンな出力が得られます。

```csharp
var license = new License();
license.SetLicense("Aspose.Total.lic");
```

## 完全動作サンプル

以下は **フォントを埋め込む方法**、**Excel を HTML に変換**、**Excel を HTML としてエクスポート** を一度に実演する、完結した実行可能プログラムです。

```csharp
using System;
using Aspose.Cells;

class ExcelToHtmlWithEmbeddedFonts
{
    static void Main()
    {
        // Apply license if you have one (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Total.lic");

        // 1️⃣ Load the Excel workbook
        var workbookPath = @"YOUR_DIRECTORY/Styled.xlsx";
        var workbook = new Workbook(workbookPath);

        // 2️⃣ Configure HTML save options to embed fonts
        var htmlOptions = new HtmlSaveOptions
        {
            EmbedFonts = true,
            ExportActiveWorksheetOnly = true, // Export only the first sheet
            ExportCssSeparately = false        // Keep CSS inline for a single file
        };

        // 3️⃣ Save as HTML
        var htmlPath = @"YOUR_DIRECTORY/Styled.html";
        workbook.Save(htmlPath, htmlOptions);

        Console.WriteLine($"Excel workbook '{workbookPath}' has been exported to HTML with embedded fonts at '{htmlPath}'.");
    }
}
```

**期待される出力:** プログラム実行後、`Styled.html` が `YOUR_DIRECTORY` に作成されます。モダンブラウザでファイルを開くと、元の Excel ファイルと同じフォントでスプレッドシートが表示され、フォントがインストールされていない環境でも同一の見た目が保たれます。

## 結論

これで、Aspose.Cells を使用して **Excel を HTML に変換** する際に **フォントを埋め込む方法** が分かりました。ワークブックの読み込みから埋め込みフォントの検証までのフローを一通り体験したので、生成された HTML の視覚的忠実度が保たれ、ウェブレポートやメールニュースレター、カスタムタイポグラフィが必要なあらゆるシナリオに最適です。

次は、**Excel を PDF にエクスポート**、**カスタム CSS で HTML 出力をスタイリング**、または **複数ワークブックのバッチ処理** などの関連トピックを探求してください。これらはすべて同じ `HtmlSaveOptions` パターンを基盤としているため、コードを最小限の変更で再利用できます。

Happy coding!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法を基にした関連トピックを扱っています。各リソースには、ステップバイステップの説明と完全なコード例が含まれており、API の追加機能を習得したり、独自プロジェクトで代替実装を検討したりするのに役立ちます。

- [How to Export Excel to HTML – Step‑by‑Step Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-step-by-step-guide/)
- [How to Embed Fonts in HTML – Complete C# Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/)
- [How to embed fonts when converting Excel to PDF – Step‑by‑Step Guide](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}