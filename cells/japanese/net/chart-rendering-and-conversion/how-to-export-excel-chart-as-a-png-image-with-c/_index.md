---
category: general
date: 2026-11-19
description: Aspose.Cells を使用して Excel のチャートを PNG 画像としてエクスポートする方法。数ステップで Excel チャート画像を保存し、画像形式を
  PNG に設定する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel chart
- save excel chart image
- set image format png
- save excel picture file
language: ja
lastmod: 2026-11-19
og_description: Aspose.Cells を使用して Excel のチャートを PNG 画像としてエクスポートする方法。ステップバイステップのガイドに従って、Excel
  のチャート画像を保存し、画像形式を PNG に効率的に設定しましょう。
og_image_alt: How to export Excel chart as a PNG image
og_title: Excel のチャートを PNG 画像としてエクスポートする方法 – 簡単 C# ガイド
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to export Excel chart as a PNG image using Aspose.Cells. Learn
    to save Excel chart image and set image format PNG in just a few steps.
  headline: How to export Excel chart as a PNG image with C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Chart export
title: C#でExcelチャートをPNG画像としてエクスポートする方法
url: /ja/net/chart-rendering-and-conversion/how-to-export-excel-chart-as-a-png-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でExcelチャートをPNG画像としてエクスポートする方法

ポータブル画像として **how to export Excel chart** が必要な場合、このガイドでは完全で実行可能なソリューションを示します。Aspose.Cells を使用すると、たった3行のコードで **save Excel chart image** を PNG 形式で保存でき、チュートリアルでは **set image format png** と **save Excel picture file** の方法も安全に解説します。

この記事を読み終えると、ワークブックを読み込み、最初のチャートをレンダリングし、`pivot.png` ファイルをディスクに書き出す実行可能なプログラムが完成します。追加ツールや手動のコピー＆ペーストは不要で、任意の .NET プロジェクトにそのまま組み込めるクリーンな C# コードです。

## 前提条件

* .NET 6.0 SDK 以降（コードは .NET Framework 4.6 以降でも動作します）
* Visual Studio 2022 または任意の C# エディタ
* Aspose.Cells for .NET のライセンス（または一時評価キー）
* 最初のワークシートに少なくとも1つのチャートが含まれる Excel ファイル（`pivot.xlsx`）

これらが唯一の外部依存項目であり、チュートリアルはマシンに Office がインストールされている必要はありません。

## 手順 1: Aspose.Cells をインストール

プロジェクトフォルダーでターミナルを開き、次のコマンドを実行します：

```bash
dotnet add package Aspose.Cells
```

このパッケージは `Aspose.Cells` 名前空間を追加し、`Workbook`、`ImageOrPrintOptions` など、**save Excel chart image** に必要なクラスを提供します。

## 手順 2: 最小限のコンソールプログラムを作成

`dotnet new console -n ExportChartDemo` で新しいコンソールアプリを作成し、自動生成された `Program.cs` を以下のコードに置き換えます。このプログラムは **how to export Excel chart** を示し、各決定を説明するコメントが含まれています。

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for ImageOrPrintOptions
using System.Drawing.Imaging;  // Provides ImageFormat enum

namespace ExportChartDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook that contains the pivot chart
            // -----------------------------------------------------------------
            // Replace the path with the actual location of your Excel file.
            string workbookPath = @"YOUR_DIRECTORY\pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -----------------------------------------------------------------
            // 2️⃣ Set up image export options (PNG format)
            // -----------------------------------------------------------------
            // This is where we **set image format png** for the exported picture.
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: control the resolution (DPI) of the output image.
                // Higher DPI yields larger files but sharper charts.
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 3️⃣ Render the first picture (the chart) on the first worksheet
            // -----------------------------------------------------------------
            // Aspose.Cells stores charts as Picture objects inside the worksheet.
            // The index [0] refers to the first chart; adjust if you have multiple.
            Worksheet sheet = workbook.Worksheets[0];
            if (sheet.Pictures.Count == 0)
            {
                Console.WriteLine("No pictures found on the first worksheet.");
                return;
            }

            // Render the picture to a PNG file.
            string outputPath = @"YOUR_DIRECTORY\pivot.png";
            sheet.Pictures[0].RenderToImage(imageOptions, outputPath);

            Console.WriteLine($"Chart exported successfully to: {outputPath}");
        }
    }
}
```

### 各部分が重要な理由

* **Loading the workbook** – `Workbook` は Microsoft Excel がインストールされていなくても `.xlsx` ファイルを解析します。
* **ImageOrPrintOptions** – このオブジェクトは出力形式を制御します。`ImageFormat = ImageFormat.Png` を設定すると **sets image format png** となり、ロスレスで広くサポートされています。
* **RenderToImage** – `RenderToImage` メソッドはチャート（`Picture` オブジェクト）を画像ファイルに変換します。このメソッドはスケーリング、DPI、透過性も自動的に処理します。
* **Error handling** – `sheet.Pictures.Count == 0` のチェックにより、ワークシートにチャートがない場合のランタイム例外を防ぎます。これはユーザーが誤ったシートを指定したときに頻出するケースです。

## 手順 3: プログラムを実行し結果を確認

1. プロジェクトをビルド: `dotnet build`。
2. 実行: `dotnet run --project ExportChartDemo`。

すべてが正しく設定されていれば、次のように表示されます：

```
Chart exported successfully to: YOUR_DIRECTORY\pivot.png
```

`pivot.png` を任意の画像ビューアで開きます。Excel チャートと同一のビジュアルが表示され、**saved Excel picture file** に成功したことが確認できます。

### 期待される出力

以下はエクスポートされた PNG のサンプルです（実際のチャートは元ファイルに依存します）。

![エクスポートされたExcelチャート（PNG画像）](images/exported-chart.png){: .center alt="ExcelチャートをPNG画像としてエクスポートする方法"}

## 手順 4: 高度なオプション – 複数チャートのエクスポート

ワークブックに複数のチャートが含まれる場合、`Pictures` コレクションをループ処理できます：

```csharp
for (int i = 0; i < sheet.Pictures.Count; i++)
{
    string chartPath = $@"YOUR_DIRECTORY\chart_{i + 1}.png";
    sheet.Pictures[i].RenderToImage(imageOptions, chartPath);
    Console.WriteLine($"Chart {i + 1} saved to {chartPath}");
}
```

このパターンにより、シート上のすべてのチャートに対して **save Excel chart image** が可能になり、レポートパイプラインで便利です。

## よくある落とし穴と回避方法

| 症状 | 考えられる原因 | 対策 |
|------|----------------|------|
| `Pictures[0]` に対する `ArgumentOutOfRangeException` | ワークシートにチャートがない、または別のシートにチャートがある。 | シートインデックス（`Worksheets[0]`）を確認し、チャートが存在することを確認する。必要に応じて `Worksheets["SheetName"]` を使用する。 |
| エクスポートされた画像がぼやける | DPI が低すぎる（デフォルト 96）。 | `ImageOrPrintOptions` の `HorizontalResolution` と `VerticalResolution` を増やす。 |
| PNG ファイルが空または破損している | ライセンスがないため評価制限がかかっている。 | ワークブックをロードする前に有効な Aspose.Cells ライセンスを適用する（`License license = new License(); license.SetLicense("Aspose.Total.lic");`）。 |
| ファイルパスエラー（`FileNotFoundException`） | `YOUR_DIRECTORY` プレースホルダーが正しくない。 | 絶対パスを使用するか、`Path.Combine(Environment.CurrentDirectory, "pivot.xlsx")` を使用する。 |

これらの問題に対処することで、スムーズな **save excel picture file** 体験が得られます。

## プロのコツ: メモリストリームへ直接エクスポート

画像をディスクに書き込む代わりに、メモリ上で扱う必要がある場合（例: Web API へアップロード）があります：

```csharp
using (var ms = new MemoryStream())
{
    sheet.Pictures[0].RenderToImage(imageOptions, ms);
    // ms now contains the PNG bytes – you can send them over HTTP, store in DB, etc.
}
```

同じ **set image format png** ロジックが適用され、ファイルパスの代わりにストリームを使用します。

## 結論

これで Aspose.Cells for .NET を使用して **how to export Excel chart** を PNG ファイルとしてエクスポートする方法が分かりました。チュートリアルでは以下をカバーしました：

* ライブラリのインストール
* ワークブックの読み込み
* **Setting image format png**
* **Saving Excel chart image** をディスクに保存
* 複数チャートの処理と一般的なエラーへの対処

この基盤があれば、チャートエクスポートを自動レポート、Web サービス、デスクトップユーティリティに組み込むことができます。次に、**save excel picture file** を JPEG（`ImageFormat.Jpeg`）として保存したり、チャートを PDF に変換して印刷用レポートにするなど、関連トピックを探求してください。

コーディングを楽しんでください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法に基づく密接に関連したトピックをカバーしています。各リソースには、ステップバイステップの解説付きの完全なコード例が含まれ、追加の API 機能を習得し、プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Convert Excel Pie Chart to Image Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)
- [Export Chart as PNG – Complete Guide to Convert Excel to HTML with Aspose.Cells](/cells/english/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/)
- [Export Excel Cells to Image Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}