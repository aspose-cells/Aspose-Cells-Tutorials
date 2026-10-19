---
category: general
date: 2026-09-15
description: C#でExcelブックを作成し、EXPAND関数を使って動的配列をスピルさせながらブックをPDFとして保存する方法を学ぶ。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save workbook as pdf
- spill dynamic array
- use expand function
- how to create dynamic array in excel
language: ja
lastmod: 2026-09-15
og_description: C#でExcelブックを作成し、EXPAND関数で動的配列をスピルさせながら、ブックをPDFとしてすばやく保存する。
og_image_alt: Create Excel workbook screenshot showing dynamic array and PDF output
og_title: 動的配列を使用してExcelブックを作成し、PDFとして保存
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Create Excel workbook in C# and learn how to save workbook as PDF while
    spilling dynamic arrays using the EXPAND function.
  headline: Create Excel workbook and save as PDF with dynamic arrays
  type: TechArticle
tags:
- excel
- csharp
- aspose-cells
- pdf
- dynamic-array
title: Excelブックを作成し、動的配列でPDFとして保存
url: /ja/net/conversion-to-pdf/create-excel-workbook-and-save-as-pdf-with-dynamic-arrays/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel ワークブックを作成し、動的配列で PDF に保存する

プログラムで **Excel ワークブックを作成**し、さらに **ワークブックを PDF として保存**したい場合、このガイドでは C# による完全なエンドツーエンドのソリューションを示します。また、**EXPAND 関数**を使用して **動的配列をスピル**させる方法も紹介します。これは VBA を使わずに配列を生成する最新の方法です。

レポートサービスの構築、ERP システムのエクスポート機能、あるいはデータ駆動型ダッシュボードの作成など、どのようなシナリオでも、以下の手順でワークブックを生成し、スマートマーカー データで埋め込み、先進的なフォント機能を保持した PDF を作成できます。

## 前提条件

* .NET 6.0 以降（コードは .NET Framework 4.8 でも動作します）
* 最新バージョンの **Aspose.Cells for .NET**（v25.8 以降）— `Workbook`、`PdfSaveOptions`、`SmartMarkerProcessor` を提供します。
* Visual Studio 2022 などの IDE（C# をコンパイルできるエディタであれば何でも可）。

Add the NuGet package to your project:

```bash
dotnet add package Aspose.Cells --version 25.8
```

## 手順 1: Excel ワークブックを作成し、最初のワークシートを設定する

最初のタスクは **Excel ワークブックを作成**し、デフォルトのワークシートへの参照を取得することです。このワークシートは動的配列と Smart Marker テンプレートのホストになります。

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook in memory
        Workbook wb = new Workbook();

        // Get the first (default) worksheet
        Worksheet ws = wb.Worksheets[0];
```

*重要な理由*: `Workbook` をインスタンス化すると内部のブック構造が確保され、`Worksheets[0]` にアクセスすると手動でシートを追加することなく、すぐに使用できるシートが取得できます。

## 手順 2: EXPAND 関数を使用して動的配列をスピルする

Excel の **EXPAND 関数**は、静的な配列リテラルを任意のサイズのスピル範囲に変換できます。ここでは `{1,2,3}` を `A1` から始まる 5 行 × 1 列の範囲に展開するよう Excel に指示しています。

```csharp
        // Write the EXPAND formula into A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // Force calculation so the spill occurs immediately
        ws.Calculate();
```

*重要な理由*: `EXPAND` を使用すると C# で手動ループを書く必要がなくなります。エンジンがスピル範囲を計算し、値を直接ワークシートに格納するため、後で PDF にも反映されます。

## 手順 3: フォントバリエーションセレクタを保持しながらワークブックを PDF として保存する

**ワークブックを PDF として保存**する必要がある場合、フォントバリエーションセレクタなどの高度な組版機能（Aspose.Cells v25.8 以降で利用可能）を有効にすることもできます。これにより、PDF が複雑な文字体系を正しくレンダリングします。

```csharp
        // Configure PDF options
        PdfSaveOptions pdfOpts = new PdfSaveOptions
        {
            FontVariationSelectors = true   // keeps variation selectors for OpenType fonts
        };

        // Save the current workbook (with the spilled array) as PDF
        wb.Save(@"YOUR_DIRECTORY\VarSelector.pdf", pdfOpts);
```

*重要な理由*: `FontVariationSelectors` を `true` に設定することは、文字形状のバリエーションに依存する言語（例: 中国語、日本語、絵文字）にとって不可欠です。生成された PDF は画面上の Excel 表示と同一になります。

## 手順 4: ネストされたデータソースを参照する Smart Marker テンプレートを挿入する

Smart Marker を使用すると、プレースホルダーをワークシートに直接埋め込むことができます。以下のテンプレートは注文とそのアイテムのリストを生成します。

```csharp
        // Define a Smart Marker template in cell A1
        string template = "${Orders.OrderId}\n${Orders.Items:ItemName}\n";
        ws.Cells["A1"].PutValue(template);
```

*重要な理由*: `A1` にテンプレートを配置することで、Aspose.Cells にデータの展開開始位置を指示します。`:` 構文（`Items:ItemName`）は、ネストされたコレクションを反復処理することをプロセッサに指示します。

## 手順 5: ネストされたデータソース（注文とそのアイテム）を定義する

各注文が独自のアイテムオブジェクトコレクションを持つ匿名配列を作成します。これは典型的なマスタ‑詳細シナリオを模倣しています。

```csharp
        // Sample nested data source
        var orders = new[]
        {
            new
            {
                OrderId = 1,
                Items = new[]
                {
                    new { ItemName = "Apple" },
                    new { ItemName = "Banana" }
                }
            },
            new
            {
                OrderId = 2,
                Items = new[]
                {
                    new { ItemName = "Carrot" }
                }
            }
        };
```

*重要な理由*: ネスト構造は、VBA や手動セルループを書かずに Smart Markers を通じて **Excel で動的配列を作成**する方法を示しています。

## 手順 6: Smart Marker を処理し、最終的な Excel ファイルを保存する

ここでワークブックとデータソースを `SmartMarkerProcessor` に渡します。処理後、プレースホルダーは実際の行に置き換えられ、結果を通常の `.xlsx` ファイルとして保存します。

```csharp
        // Process the Smart Markers
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Process(wb, orders);

        // Save the populated workbook
        wb.Save(@"YOUR_DIRECTORY\NestedSmartMarker.xlsx");
    }
}
```

*重要な理由*: `SmartMarkerProcessor` はテンプレートを自動的に展開し、必要な行を作成してデータで埋めます。最終的なワークブックは Excel で開き、各注文とそのアイテムが正しく表示されていることを確認できます。

## 期待される出力

* **VarSelector.pdf** – 1‑3 の数字が 5 行にわたってスピルし、設定した任意の OpenType フォントバリエーションでレンダリングされた PDF ファイル。
* **NestedSmartMarker.xlsx** – 以下の行が `A1` から始まる Excel ファイル：

| OrderId | ItemName |
|---------|----------|
| 1       | Apple    |
| 1       | Banana   |
| 2       | Carrot   |

PDF バージョンは、Smart Marker の処理前にワークシートの状態が保存されたため、同じ数値スピルを保持します。最終データを PDF にしたい場合は、処理後に再度 PDF を保存することも可能です。

## プロのコツと一般的な落とし穴

| ヒント | 説明 |
|-----|-------------|
| **同じ `PdfSaveOptions` を再利用する** | オプション オブジェクトを一度作成して再利用すると、レンダリングの微妙な差異（例: バリエーションセレクタが欠落するなど）を防げます。 |
| **`ws.Calculate()` を数式設定後に呼び出す** | 明示的な計算を行わないと、プログラムでワークブックを検査したときにスピル範囲が空のままになることがあります。 |
| **Smart Marker テンプレートはクリーンなシートに配置する** | 既存データとテンプレートを混在させると、予期しない行挿入が発生する可能性があります。可能であれば専用シートを使用してください。 |
| **ファイルパスに注意する** | `Path.Combine(Environment.CurrentDirectory, "output.pdf")` を使用して、マシン間でハードコーディングされたディレクトリを回避します。 |
| **バージョンチェック** | `FontVariationSelectors` はバージョン 25.8 以降でのみ利用可能です。古いバージョンではプロパティが無視され、例外はスローされません。 |

## 次のステップ

**Excel ワークブックを作成**、**動的配列をスピル**、そして **ワークブックを PDF として保存**する方法が分かったので、以下を検討できます。

* PDF 変換前にチャートや画像を追加する。
* `Save` のオーバーロードを使用して、同じワークブックを他の形式（例: HTML、CSV）にエクスポートする。
* **Smart Marker 式**（`${Orders.Total:SUM(Items.Price)}`）を使用して、集計をリアルタイムで計算する。
* このコードを ASP.NET Core API に統合し、ユーザーが Web エンドポイントから生成された PDF を直接ダウンロードできるようにする。

---

**Summary** – このチュートリアルでは、**Excel ワークブックを作成**し、**EXPAND 関数**を使用して **動的配列をスピル**させ、ネストされたデータソースと連携する **Smart Marker** を埋め込み、最終的に **ワークブックを PDF として保存**し、先進的なフォント機能を保持する方法を示しました。完全な実行可能サンプルは任意の C# プロジェクトにコピーして、独自のデータ構造に合わせて調整できます。ハッピーコーディング！

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックをカバーしています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得したり、プロジェクトで代替実装アプローチを検討したりするのに役立ちます。

- [Aspose.Cells を使用して ASP.NET で Excel ワークブックを PDF として作成・保存する](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Aspose.Cells for .NET を使用して Excel ワークブックを ODS として作成・保存する方法](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Aspose.Cells for Java を使用して Excel ワークブックを SVG として作成・保存する方法](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}