---
category: general
date: 2026-09-24
description: Aspose.Cells を使用した C# で Excel の範囲を画像としてエクスポート – ワークシート領域を PNG または JPEG
  で保存するステップバイステップガイド
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- Aspose.Cells export range
- C# Excel to PNG
- ImageOrPrintOptions usage
- export pivot table as image
language: ja
lastmod: 2026-09-24
og_description: C# と Aspose.Cells で Excel の範囲を画像としてエクスポート。ピボットテーブルを含む任意のワークシート領域を数分で
  PNG または JPEG に変換する方法を学びましょう。
og_image_alt: Screenshot of a C# program exporting an Excel range to a PNG image
og_title: C#でExcel範囲を画像としてエクスポート – 完全なAspose.Cellsガイド
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  headline: How to export excel range as image with C# and Aspose.Cells
  type: TechArticle
- description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  name: How to export excel range as image with C# and Aspose.Cells
  steps:
  - name: '**Load** the workbook from disk.'
    text: '**Load** the workbook from disk.'
  - name: '**Define** the cell area that will become the image (the *print area*).'
    text: '**Define** the cell area that will become the image (the *print area*).'
  - name: '**Export** the area using `ImageOrPrintOptions` and write the file.'
    text: '**Export** the area using `ImageOrPrintOptions` and write the file.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Image export
title: C# と Aspose.Cells を使用して Excel の範囲を画像としてエクスポートする方法
url: /ja/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# と Aspose.Cells を使用して Excel の範囲を画像としてエクスポートする方法

.NET アプリケーションで **export excel range as image** をエクスポートする必要がある場合、本ガイドでは完全な実行可能ソリューションを示します。ダッシュボードを公開する場合や、ピボットテーブルをウェブページに埋め込む場合、レポートのサムネイルを生成する場合など、数行の C# コードだけで任意のワークシート領域を PNG（または JPEG）に変換できます。

このチュートリアルでは、次のことを学びます:

* 既存のブック（`Workbook` クラス）をロードする  
* キャプチャしたい正確なセル範囲を定義する（`PrintArea`）  
* `ImageOrPrintOptions` を使用して画像エクスポートオプションを設定する  
* 生成された画像をディスクに保存する  

すべての前提条件、エッジケース、一般的な落とし穴について解説しているので、コードを自分のプロジェクトに問題なく適用できます。

## 前提条件

| Requirement | Reason |
|-------------|--------|
| **Aspose.Cells for .NET** (latest version) | サンプルで使用されている `Workbook`、`Worksheet`、`ImageOrPrintOptions` API を提供します。 |
| **.NET 6.0 or later** | .NET 6 を対象としていますが、Aspose.Cells をサポートする任意の .NET Core/Framework バージョンでも動作します。 |
| **A valid Excel file** (e.g., `input.xlsx`) | 変換したいブックです。 |
| **Write permission to the output folder** | `Save` が成功するために必要です。 |

NuGet を使用して Aspose.Cells をインストールできます:

```bash
dotnet add package Aspose.Cells
```

## Excel の範囲を画像としてエクスポートする – プロセス概要

この操作は 3 つの論理フェーズで構成されます:

1. **Load** ワークブックをディスクからロードする。  
2. **Define** 画像になるセル領域（*印刷領域*）を定義する。  
3. **Export** `ImageOrPrintOptions` を使用して領域をエクスポートし、ファイルを書き出す。  

以下では、各フェーズを専用のステップに分解し、完全なソースコードと解説を示します。

## ステップ 1: ワークブックのロード

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Path to the source Excel file
string inputPath = @"YOUR_DIRECTORY\input.xlsx";

// Create a Workbook object – this reads the file into memory
Workbook workbook = new Workbook(inputPath);
```

**なぜ重要か:**  
`Workbook` はすべての Excel 操作のエントリーポイントです。ファイルを一度ロードするだけでメモリ使用量を抑え、後で任意のワークシートにアクセスできます。

## ステップ 2: 対象ワークシートへのアクセス

```csharp
// Get the first worksheet (index 0). Change the index or use the sheet name as needed.
Worksheet sheet = workbook.Worksheets[0];
```

**Tip:** 特定のシート名でアクセスしたい場合は、インデックスを `workbook.Worksheets["SheetName"]` に置き換えてください。これにより、ブックのレイアウトが変わってもエラーを防げます。

## ステップ 3: エクスポートしたい範囲の定義

```csharp
// Define the cell range that will be exported.
// Example: A1:G20 captures a typical pivot‑table area.
sheet.PageSetup.PrintArea = "A1:G20";
```

**なぜ `PrintArea` を設定するのか?**  
Aspose.Cells は画像作成時に *印刷領域* をレンダリングします。正確な範囲に限定することで余白を削減し、パフォーマンスが向上します。

### 代替案: シート全体をエクスポート

シート全体をエクスポートしたい場合は、`PrintArea` の設定を省略するだけです。デフォルトでシートの使用範囲が使用されます。

## ステップ 4: 画像エクスポートオプションの設定

```csharp
// Create an ImageOrPrintOptions object to control the output format.
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    // Choose PNG for lossless quality; change to Jpeg for smaller files.
    ImageFormat = ImageFormat.Png,

    // Optional: set the resolution (DPI). Higher DPI yields sharper images.
    HorizontalResolution = 300,
    VerticalResolution = 300,

    // Optional: set the page orientation if the range is wide.
    PageOrientation = PageOrientationType.Landscape
};
```

**主要プロパティの説明:**

* `ImageFormat` – ファイルタイプ（`Png`、`Jpeg`、`Bmp` など）を決定します。PNG はエッジが鮮明に保たれるため、チャートやテキストに最適です。  
* `HorizontalResolution` / `VerticalResolution` – ピクセル密度を制御します。ウェブ用サムネイルは 96 DPI で十分ですが、印刷用グラフィックは 300 DPI が推奨されます。  
* `PageOrientation` – 選択した範囲が横長の場合に役立ちます。  

## ステップ 5: 範囲を画像ファイルとしてエクスポート

```csharp
// Define the output path for the image
string outputPath = @"YOUR_DIRECTORY\range.png";

// Save the first picture on the worksheet as an image.
// The Pictures collection is automatically populated after setting PrintArea.
sheet.Pictures[0].Save(outputPath, imgOptions);
```

**内部での処理:**  
`PrintArea` が設定されると、Aspose.Cells はその領域を表す一時的な画像を生成します。`Pictures[0]` オブジェクトは、指定したオプションで保存されます。

### 画像がないワークシートの処理

ワークシートに画像がまだ含まれていない場合（例: 新規ファイル）、その場で画像を作成できます:

```csharp
// Create a picture from the defined range and add it to the sheet
Picture pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
pic.Save(outputPath, imgOptions);
```

## 完全な実行可能サンプル

すべてを組み合わせた、コピーして貼り付けて実行できる単体のコンソールアプリケーションは以下の通りです:

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // 2️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Define the range to export (e.g., a pivot table)
        sheet.PageSetup.PrintArea = "A1:G20";

        // 4️⃣ Set image export options (PNG, 300 DPI, landscape)
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300,
            PageOrientation = PageOrientationType.Landscape
        };

        // 5️⃣ Save the picture as an image file
        string outputPath = @"YOUR_DIRECTORY\range.png";

        // Ensure a picture exists; create one if necessary
        Picture pic;
        if (sheet.Pictures.Count == 0)
        {
            pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
        }
        else
        {
            pic = sheet.Pictures[0];
        }

        pic.Save(outputPath, imgOptions);

        System.Console.WriteLine($"Export completed: {outputPath}");
    }
}
```

**期待される出力:**  
`YOUR_DIRECTORY` に `range.png` という名前のファイルが作成されます。開くと **A1 から G20** のセルが鮮明な PNG 画像として表示されます。

## 一般的なバリエーションとエッジケースの処理

| Scenario | Adjustment |
|----------|------------|
| **Export to JPEG** | `ImageFormat = ImageFormat.Jpeg` に変更し、必要に応じて `Quality = 90`（範囲 0‑100）を設定します。 |
| **Multiple ranges** | 各範囲に対して `sheet.Pictures.Add` を呼び出し、異なるファイル名でそれぞれの画像を保存します。 |
| **Large worksheets** | 必要な範囲だけ `HorizontalResolution`/`VerticalResolution` を上げ、メモリ使用量の急増を防ぎます。 |
| **No picture generated** | `PrintArea` が正しくフォーマットされているか（`"A1:G20"`）を確認します。無効なアドレスは `Pictures` コレクションが空になる原因です。 |
| **Saving to a stream** | 画像をメモリ上に保持したい場合（例: ASP.NET のレスポンス）には `pic.Save(Stream, imgOptions)` を使用します。 |

## 信頼性の高い画像エクスポートのプロティップ

* **Validate the print area** – `CellArea` のパース（`CellArea area = CellArea.CreateCellArea("A1", "G20")`）を使用してプログラム的に範囲を構築し、タイプミスを防ぎます。  
* **Dispose of resources** – 多数のファイルを処理する場合は、`Workbook` を `using` ブロックで囲んでネイティブリソースを速やかに解放します。  
* **Batch processing** – 数十の範囲をエクスポートする際は、`ImageOrPrintOptions` のインスタンスを再利用してオブジェクト割り当てのオーバーヘッドを削減します。  
* **Thread safety** – Aspose.Cells のオブジェクトは **スレッドセーフではありません**。スレッドごとに別々の `Workbook` を作成するか、アクセスを同期してください。  

## 結論

これで、C# と Aspose.Cells を使用して **export excel range as image** を行う、完全で本番環境向けの手法が手に入りました。ワークブックのロード、印刷領域の設定、`ImageOrPrintOptions` の構成、画像の保存という手順は、“やり方” と “理由” の両方をカバーしており、ピボットテーブルやチャート、任意のセルブロックにもコードを適用できるようになります。

次に、以下を検討できます:

* **Export excel range as image** を他のフォーマット（SVG、BMP）でエクスポート – 試す価値のある別のサブキーワードです。  
* **Embedding the PNG in a PDF** を Aspose.PDF を使って行い、エンドツーエンドのレポート生成を実現します。  
* **Automating batch exports** を複数のブックに対してシンプルなコンソールループで自動化します。  

さまざまな解像度、向き、出力ディレクトリを試してみてください。コーディングを楽しんで！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックを取り上げています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.Cells .NET を使用した Excel セルの画像エクスポート：ステップバイステップガイド](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)
- [Aspose.Cells for Java を使用した Excel ワークブックの画像エクスポート](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Aspose.Cells Java を使用して Excel ワークシートを PNG にエクスポートする方法](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}