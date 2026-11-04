---
category: general
date: 2026-10-20
description: Aspose.Cellsでwrapcolsの使い方を学び、HTMLにフォントを埋め込み、完全なC#サンプルでExcelをHTMLとして保存する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- embed fonts in html
- save excel as html
- convert workbook to html
- use wrapcols function
language: ja
lastmod: 2026-10-20
og_description: Aspose.Cellsでwrapcolsを使用し、HTMLにフォントを埋め込み、ワークブックをHTMLに変換する方法を、開発者向けにC#でわかりやすく解説。
og_image_alt: Screenshot of an Excel workbook saved as HTML with embedded fonts using
  Aspose.Cells
og_title: ExcelをHTMLにエクスポートする際のwrapcolsの使い方とフォント埋め込み
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to use wrapcols in Aspose.Cells, embed fonts in HTML, and
    save Excel as HTML with a complete C# example.
  headline: How to use wrapcols and embed fonts saving Excel to HTML
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel to HTML
- Smart Markers
title: ExcelをHTMLに保存する際のwrapcolsの使い方とフォント埋め込み
url: /ja/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# wrapcols の使用方法とフォント埋め込みで Excel を HTML に保存する方法

Aspose.Cells の数式で **wrapcols の使用方法** が必要な場合、このガイドでは正確な手順を示します。また、**HTML にフォントを埋め込む** 方法と **Excel を HTML として保存する** 方法も学び、出力がブラウザ間で同一に表示されるようにします。  

このチュートリアルでは、`WRAPCOLS` 関数の使用、埋め込みフォント付きのワークブックのエクスポート、Smart Markers を使用したマスタ‑ディテイル レポートの生成という 3 つの実用シナリオを取り上げます。最後まで実行すれば、これらすべての機能を示す単一の実行可能な C# プログラムが手に入ります。

## 前提条件

開始する前に、以下が揃っていることを確認してください。

* .NET 6.0（またはそれ以降）がインストールされていること。
* プロジェクトに Aspose.Cells for .NET を追加する（`dotnet add package Aspose.Cells`）。
* C# と Excel の数式に関する基本的な知識があること。

追加のサードパーティ ライブラリは不要です。Aspose.Cells が HTML 変換とフォント埋め込みを内部で処理します。

## 手順 1: 数式で **wrapcols の使用方法** をデモする

`WRAPCOLS` 関数は一次元の範囲を二次元配列に分割し、列方向に先に埋めていきます。レポートやチャート用にデータの形状を変換したいときに便利です。

```csharp
using Aspose.Cells;
using System;

class WrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Populate a vertical range A1:A3
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // Apply WRAPCOLS(A1:A3, 2) – this creates a 2‑column array {1,2}
        sheet.Cells["B1"].Formula = "=WRAPCOLS(A1:A3, 2)";

        // Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // Output the result to verify the function works
        Console.WriteLine("Result of WRAPCOLS: " + sheet.Cells["B1"].Value);
        // Expected output: Result of WRAPCOLS: 1
    }
}
```

**この動作の理由:**  
`WRAPCOLS` は 2 つの引数（ソース範囲と列数）を受け取ります。関数は列単位で配列を埋め、余分な値（例の `3`）は破棄されます。結果はターゲット範囲の左上セル（`B1`）に表示され、必要に応じて手動で範囲を拡張すれば配列全体を取得できます。

> **プロのコツ:** 数式を設定した後は `workbook.CalculateFormula()` を呼び出し、セルの値を読み取る前に結果が最新であることを確認してください。

## 手順 2: **ワークブックを HTML に変換** し **HTML にフォントを埋め込む**

Excel ファイルを HTML にエクスポートすると、フォントがブラウザのデフォルトに置き換わり、レイアウトが崩れることがあります。Aspose.Cells を使用すれば、ワークブックで使用されているフォントをそのまま HTML に埋め込むことができます。

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for HtmlSaveOptions
using System;

class HtmlExportDemo
{
    static void Main()
    {
        // Re‑use the workbook from the previous step
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue("Hello");
        sheet.Cells["A2"].PutValue("World");

        // Configure HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Embedding fonts ensures the output looks the same on any device
            EmbedFonts = true,
            // Optional: specify a folder for supporting files (images, CSS)
            ExportEmbeddedImages = true
        };

        // Save the workbook as an HTML file with embedded fonts
        string outputPath = @"C:\Temp\WorkbookWithFonts.html";
        workbook.Save(outputPath, htmlOptions);

        Console.WriteLine($"Workbook saved to HTML with embedded fonts at: {outputPath}");
    }
}
```

**フォント埋め込みが重要な理由:**  
`EmbedFonts` が `true` の場合、Aspose.Cells は使用された TrueType/OpenType フォントを Base64 エンコードされた `@font-face` ルールに変換し、生成された HTML に埋め込みます。これにより、クライアント側に同じフォントがインストールされていなくても、ピクセル単位で正確な描画が保証されます。

> **エッジケース:** ソース ワークブックがサーバーにインストールされていないフォントを参照している場合、Aspose.Cells はデフォルト フォントにフォールバックし、警告を出します。必要なフォントがサーバー上にあることを事前に確認してください。

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを検討したりするのに役立ちます。

- [C# で WRAPCOLS を使用する方法 – ラップ関数で Excel ワークブックを作成](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [HTML にフォントを埋め込む方法 – C# で Excel を HTML に変換](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/)
- [Aspose.Cells for .NET を使用して Excel ファイルを HTML に変換する方法 – 重なったコンテンツを非表示にする](/cells/english/net/workbook-operations/excel-to-html-hide-overlaid-content-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}