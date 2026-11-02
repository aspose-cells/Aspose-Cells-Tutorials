---
category: general
date: 2026-10-10
description: C#でAspose.Cellsを使用してExcelを素早くPNGに変換します。Excelの範囲をエクスポートし、ExcelをPNGとして保存し、ワークシートを画像に変換する方法を数分で学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to png
- export excel range
- save excel as png
- how to export excel
- convert worksheet to image
language: ja
lastmod: 2026-10-10
og_description: Aspose.CellsでExcelを即座にPNGに変換。このチュートリアルでは、Excelの範囲をエクスポートし、ExcelをPNGとして保存し、ワークシートを画像に変換する方法を示します。
og_image_alt: Screenshot of C# code that converts an Excel worksheet to a PNG image
og_title: C#でExcelをPNGに変換する – 完全プログラミングガイド
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: convert excel to png quickly using Aspose.Cells in C#. Learn to export
    excel range, save excel as png, and convert worksheet to image in minutes.
  headline: How to convert Excel to PNG with C# – step‑by‑step guide
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Image export
- Automation
title: C#でExcelをPNGに変換する方法 – ステップバイステップガイド
url: /ja/net/converting-excel-files-to-other-formats/how-to-convert-excel-to-png-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Excel を PNG に変換する方法 – ステップバイステップガイド

プログラムで **Excel を PNG に変換** する必要がある場合、このガイドでは Aspose.Cells for .NET を使用して具体的な手順を示します。レポートサービスや自動ダッシュボードを構築している場合でも、Excel の範囲をエクスポートし、結果を PNG ファイルとして保存し、一般的なエッジケースを処理する方法を学べます。

NuGet パッケージの追加から特定のワークシート領域のレンダリングまで、必要な手順をすべて順に説明しますので、追加のリソースを探さずに任意の C# プロジェクトにソリューションを組み込むことができます。

## 前提条件

* .NET 6.0 SDK 以降（コードは .NET Framework 4.6+ でも動作します）
* Visual Studio 2022（または C# をサポートする任意の IDE）
* 有効な Aspose.Cells for .NET ライセンス（無料トライアルは評価に使用できます）
* **Pivot.xlsx** という名前の Excel ファイルを、参照可能なフォルダーに配置します（チュートリアルでは `YOUR_DIRECTORY` をプレースホルダーとして使用しています）

> **プロのコツ:** NuGet パッケージ マネージャ コンソールから Aspose.Cells パッケージをインストールします:  
> `Install-Package Aspose.Cells`

## Excel を PNG に変換 – 完全コード解説

以下の完全なプログラムは、ブックを読み込み、画像オプションを設定し、指定したセル範囲を PNG ファイルにレンダリングします。必要な `using` ディレクティブはすべて含まれているので、コードを新しいコンソール プロジェクトにコピーしてすぐに実行できます。

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

namespace ExcelToPngDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Load the workbook (convert excel to png starts here)
            // -------------------------------------------------
            string workbookPath = @"YOUR_DIRECTORY\Pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -------------------------------------------------
            // Step 2: Configure image options (PNG format)
            // -------------------------------------------------
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                // Export format – PNG ensures lossless quality
                ImageFormat = ImageFormat.Png,

                // Optional: set resolution (default is 96 DPI)
                // HorizontalResolution = 150,
                // VerticalResolution = 150
            };

            // -------------------------------------------------
            // Step 3: Define the range you want to export
            // -------------------------------------------------
            // Example range A1:H30 – you can change this to any valid Excel range
            string range = "A1:H30";

            // -------------------------------------------------
            // Step 4: Render the range to an image file
            // -------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\Pivot.png";
            workbook.Worksheets[0].RenderRangeToImage(range, outputPath, imgOptions);

            Console.WriteLine($"Excel range {range} has been exported to PNG at: {outputPath}");
        }
    }
}
```

### コードの動作概要

* **Loading the workbook** – `Workbook` は `.xlsx` ファイルをメモリに読み込み、すべてのワークシートへのアクセスを可能にします。
* **ImageOrPrintOptions** – このオブジェクトは Aspose.Cells に PNG（`ImageFormat.Png`）を生成させます。必要に応じて DPI、スケーリング、背景色も調整できます。
* **RenderRangeToImage** – メソッド `RenderRangeToImage` は 3 つの引数を受け取ります：セル範囲（`"A1:H30"`）、出力ファイルパス、画像オプション。これが **export excel range** を PNG 画像にエクスポートする核心の操作です。
* **Result** – 実行後、指定したフォルダーに `Pivot.png` が作成され、選択したセルの正確なビジュアル表現が含まれます。

## Excel 範囲を PNG にエクスポート – 出力のカスタマイズ

`A1:H30` 以外の **export excel range** が必要な場合は、`range` 変数を変更するだけです。このメソッドは、名前付き範囲を含む任意の Excel 形式のアドレスを受け付けます：

```csharp
// Export a named range called "ReportArea"
string range = "ReportArea";
```

`"A1:Z1000"`（またはそれ以上のアドレス）を使用するか、範囲パラメータなしで `RenderToImage` を呼び出すことで、ワークシート全体をエクスポートすることもできます。

## 追加設定で Excel を PNG として保存

印刷やウェブ用に特定の解像度に合わせた PNG が必要な場合があります。そのようなときは、`ImageOrPrintOptions` を以下のように調整します：

```csharp
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    HorizontalResolution = 300,   // 300 DPI for high‑quality print
    VerticalResolution = 300,
    Transparent = true           // Makes the background transparent
};
```

これらの設定は、カスタム DPI と透過性を使用して **save excel as png** する方法を示しており、最終画像の品質を完全にコントロールできます。

## Excel をエクスポートする方法 – 複数シートの処理

この例は最初のワークシート（`Worksheets[0]`）を対象としています。別のシートを **convert worksheet to image** したい場合は、インデックスまたは名前で参照してください：

```csharp
// By index (second sheet)
Worksheet sheet = workbook.Worksheets[1];

// By name
Worksheet sheet = workbook.Worksheets["DataSheet"];
sheet.RenderRangeToImage(range, outputPath, imgOptions);
```

ループで各シートを処理するのは簡単です：

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string sheetPath = $@"YOUR_DIRECTORY\Sheet{i + 1}.png";
    workbook.Worksheets[i].RenderRangeToImage(range, sheetPath, imgOptions);
    Console.WriteLine($"Sheet {i + 1} exported to {sheetPath}");
}
```

## エッジケースとトラブルシューティング

| Situation | Recommended approach |
|-----------|----------------------|
| **非常に大きな範囲**（例：ブック全体） | `OutOfMemoryException` を回避するために、`HorizontalResolution`/`VerticalResolution` を徐々に上げます。シートごとに別々にエクスポートすることも検討してください。 |
| **結合セル** | Aspose.Cells は結合セルのビジュアルを自動的に保持しますが、正確な列幅に依存する場合は出力を確認してください。 |
| **外部ファイルを参照する数式** | ワークブックを読み込む前にそれらのファイルがアクセス可能であることを確認してください。そうしないと、レンダリングされた画像に古い値が表示される可能性があります。 |
| **ライセンスがない** | 試用版は透かしが追加されます。レンダリング前に有効なライセンスを適用してください（`License license = new License(); license.SetLicense("Aspose.Cells.lic");`）ことで、透かしのない PNG を生成できます。 |

## 完全な動作例

以下はコンパイルして実行できる自己完結型プログラムです。`YOUR_DIRECTORY` を実際のフォルダー パスに置き換えてください。

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

namespace ExcelToPngDemo
{
    class Program
    {
        static void Main()
        {
            // Load workbook
            var workbook = new Workbook(@"C:\Temp\Pivot.xlsx");

            // Set PNG options
            var options = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 150,
                VerticalResolution = 150
            };

            // Define range and output file
            string range = "A1:H30";
            string output = @"C:\Temp\Pivot.png";

            // Export the range as a PNG image
            workbook.Worksheets[0].RenderRangeToImage(range, output, options);

            Console.WriteLine($"Successfully converted Excel to PNG: {output}");
        }
    }
}
```

**期待される出力**

```
Successfully converted Excel to PNG: C:\Temp\Pivot.png
```

`Pivot.png` を任意の画像ビューアで開くと、セル A1 から H30 までの正確なビジュアルレイアウト（書式設定、色、罫線を含む）が表示されます。

## 結論

C# を使用して **convert Excel to PNG** する信頼できる方法が手に入りました。このチュートリアルでは、**export excel range**、**save excel as png**、**convert worksheet to image** の方法を、カスタマイズ可能なオプションとベストプラクティスのヒントとともに解説しました。  

ここからは次のことが可能です：

* コードを Web API に組み込み、オンデマンドで画像を生成する。  
* PNG 出力を PDF 生成と組み合わせ、マルチフォーマットレポートを作成する。  
* `ImageFormat` プロパティを変更して、他の画像形式（`ImageFormat.Jpeg`、`ImageFormat.Bmp`）を試す。

さまざまな範囲、解像度、ワークシートの選択を試して、特定の自動化シナリオに合わせてください。

---

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説付きの完全な動作コード例が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.Cells Java を使用して Excel ワークシートを PNG にエクスポートする方法](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Aspose.Cells を使用して Java で Excel を PNG、TIFF、PDF に変換する](/cells/english/java/workbook-operations/render-excel-as-png-tiff-pdf-aspose-cells-java/)
- [Aspose.Cells Java のマスタリング：カスタム ストリーム プロバイダーで Excel を PNG に変換する](/cells/english/java/advanced-features/aspose-cells-java-custom-stream-provider/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}