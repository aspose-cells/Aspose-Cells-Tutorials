---
category: general
date: 2026-09-27
description: Excelで印刷範囲を設定し、選択したセルをPNG画像としてエクスポートする方法を学びます。このガイドでは、範囲を画像として保存する方法や、ワークシートに画像を追加する方法も取り上げています。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- how to export png
- save range as image
- add picture to worksheet
- export selected cells image
language: ja
lastmod: 2026-09-27
og_description: Excelで印刷範囲を設定し、Aspose.CellsでPNGとしてエクスポートします。ステップバイステップのガイドに従って、範囲を画像として保存し、ワークシートに画像を追加しましょう。
og_image_alt: Screenshot showing set print area excel and exported PNG file
og_title: Excelで印刷範囲を設定 – C#でPNGをエクスポート
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Set print area in Excel and learn how to export PNG images of selected
    cells. This guide also covers saving range as image and adding picture to worksheet.
  headline: How to set print area in Excel and export PNG
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Excelで印刷範囲を設定し、PNGとしてエクスポートする方法
url: /ja/net/rendering-and-export/how-to-set-print-area-in-excel-and-export-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excelで印刷範囲を設定しPNGとしてエクスポートする方法

画像を作成する前に **set print area excel** が必要な場合、このガイドではその手順を正確に示します。また、特定の範囲から **how to export png** ファイルをエクスポートし、**save range as image**、**add picture to worksheet** を単一の繰り返し可能なワークフローで実行する方法も学べます。

プログラムから Excel を操作する場合、しばしばセルの一部（たとえばピボットテーブルやチャート）だけを画像にしたいことがあります。最初に印刷範囲を定義しておくことで、エクスポートされる PNG が期待通りのセルだけを含むことが保証され、余計な領域が含まれません。このチュートリアルでは、ブックの読み込みから最終 PNG ファイルの保存までのすべての手順を解説し、各設定がなぜ重要かを説明します。

## 前提条件

開始する前に、以下がインストールされていることを確認してください。

* .NET 6.0 以降
* Visual Studio 2022（または任意の C# IDE）
* **Aspose.Cells for .NET** NuGet パッケージ（`Install-Package Aspose.Cells`）
* 既知のディレクトリに配置された Excel ファイル（`input.xlsx`）

これらの要件により、追加設定なしでコードが実行できます。

## ステップ 1: 作業したいブックをロードする

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Load the workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

`Workbook` クラスは Excel ファイル全体を表します。最初にロードすることで、ワークシート、セル、ページ設定オプションへアクセスできるようになります。

## ステップ 2: 対象範囲の **set print area excel** を設定する

```csharp
// Define the range you want to capture
string printArea = "A1:G20";

// Apply the range as the print area on the first worksheet
workbook.Worksheets[0].PageSetup.PrintArea = printArea;
```

**印刷範囲** を設定すると、Excel（および Aspose.Cells）に対してどのセルが印刷可能ページに含まれるかを指示できます。後でシートを画像としてエクスポートするときは、この範囲だけが描画され、**export selected cells image** を実現するために必須です。

## ステップ 3: 画像エクスポートオプションを構成 – **how to export png**

```csharp
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG ensures lossless quality
    OnePagePerSheet = true           // Export the defined print area as a single page
};
```

`ImageOrPrintOptions` は出力形式を制御します。`ImageFormat.Png` を選択することで、高解像度かつ透過背景の画像が得られ、Web やデスクトップ環境での利用に適しています。

## ステップ 4: 定義した範囲から画像を作成し **add picture to worksheet** する

```csharp
// Create a picture object from the selected range
Picture picture = workbook.Worksheets[0].Pictures.Add(
    0,                                     // top‑left row index where the picture will be placed
    0,                                     // top‑left column index where the picture will be placed
    workbook.Worksheets[0].Cells.CreateRange(printArea));
```

`Pictures.Add` メソッドはワークシートに新しい画像を挿入します。ステップ 2 で作成した範囲を渡すことで、**save range as image** をシート上に直接配置でき、後で他のシートやブック内で画像を参照したい場合に便利です。

## ステップ 5: **Save the picture as an image file** – **export selected cells image** ワークフローの完了

```csharp
// Save the picture to disk as a PNG file
picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);
```

`Save` を呼び出すと、ステップ 3 で設定したオプションに従って画像がファイルシステムに書き込まれます。生成された `selected_range.png` には、**set print area excel** コマンドで指定したセルだけが含まれます。

## 完全な実行可能サンプル

すべてを組み合わせると、任意のコンソールアプリケーションに貼り付け可能なコンパクトなプログラムが完成します。

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

class ExportExcelRangeAsPng
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Set print area excel
        string printArea = "A1:G20";
        workbook.Worksheets[0].PageSetup.PrintArea = printArea;

        // 3️⃣ Configure how to export png
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            OnePagePerSheet = true
        };

        // 4️⃣ Add picture to worksheet (save range as image)
        Picture picture = workbook.Worksheets[0].Pictures.Add(
            0,
            0,
            workbook.Worksheets[0].Cells.CreateRange(printArea));

        // 5️⃣ Export selected cells image
        picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);

        Console.WriteLine("PNG exported successfully to YOUR_DIRECTORY\\selected_range.png");
    }
}
```

### 期待される出力

プログラムを実行すると次のように表示されます。

```
PNG exported successfully to YOUR_DIRECTORY\selected_range.png
```

そして、`selected_range.png` ファイルが作成され、`input.xlsx` の A1 から G20 までのセルだけが画像として保存されます。

## よくある落とし穴と回避策

| 問題 | 発生理由 | 対策 |
|------|----------|------|
| エクスポートされた画像にシート全体が含まれる | 印刷範囲が未設定 | 画像作成前に必ず **set print area excel** を設定 |
| PNG がぼやけて見える | デフォルト DPI が低い | `imageOptions.DpiX` と `imageOptions.DpiY` を高い値（例: 300）に設定 |
| ファイルが見つからないエラー | ディレクトリパスが間違っている | `Path.Combine` を使用するか、フォルダーの存在を再確認 |
| 画像がずれて表示される | 行・列インデックスが誤っている | `Pictures.Add` の最初の 2 パラメータは画像の左上セルを示すので、クリーンなエクスポートのために `0,0` のままにする |

## プロ tip: 1 回の実行で複数範囲をエクスポートする

複数の領域に対して **export selected cells image** が必要な場合、ステップ 2‑5 をループ内で繰り返し、各イテレーションで `printArea` を変更します。画像ごとにユニークなファイル名を付けないと、後の保存が前のファイルを上書きしてしまう点に注意してください。

## 結論

これで **set print area excel** の方法、**how to export png** の設定、**save range as image**、そして **add picture to worksheet** の手順がマスターできました。Aspose.Cells を使えば、数行の C# コードで任意のセルブロックを高品質な PNG に変換できます。

次に試してみると良いこと:

* エクスポートした PNG に枠線や透かしを追加する（*add picture to worksheet* にスタイリングを組み合わせて検索）
* 印刷可能なレポート用に直接 PDF へエクスポートする（*export selected cells image* → PDF ワークフロー）
* バッチジョブで複数ブックを自動処理する

さまざまな範囲、DPI 設定、画像形式を試して、プロジェクトの要件に合わせて最適化してください。コーディングを楽しんでください！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、ステップバイステップの説明と完全なコード例が含まれており、API の追加機能を習得したり、代替実装アプローチを探求したりするのに役立ちます。

- [Excelで印刷範囲を設定しPowerPointへエクスポート – ステップバイステップガイド](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Aspose.Cells Java で Excel の印刷範囲を HTML にエクスポート](/cells/english/java/workbook-operations/export-excel-print-area-html-aspose-cells-java/)
- [Aspose.Cells for .NET で Excel の印刷範囲を設定する方法](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}