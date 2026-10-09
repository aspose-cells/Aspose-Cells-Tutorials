---
category: general
date: 2026-06-08
description: C# と Aspose.Cells を使用して Excel の範囲を画像としてエクスポートします。簡単な手順で Excel ワークシートを画像として保存する方法を学びましょう。
draft: false
keywords:
- export excel range as image
- save excel worksheet as image
- Aspose.Cells image export
- C# Excel automation
- pivot table to image
language: ja
og_description: C#でExcelの範囲を画像としてエクスポートする。このチュートリアルでは、Excelのワークシートを画像として迅速かつ確実に保存する方法を示します。
og_title: Excelの範囲を画像としてエクスポート – 完全なC#ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Export Excel range as image using C# and Aspose.Cells. Learn how to
    save Excel worksheet as image in just a few simple steps.
  headline: Export Excel Range as Image – Complete C# Guide
  type: TechArticle
- description: Export Excel range as image using C# and Aspose.Cells. Learn how to
    save Excel worksheet as image in just a few simple steps.
  name: Export Excel Range as Image – Complete C# Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - Aspose.Cells
      for .NET ≥ 23.9 (you can grab a free trial from the Aspose website). - A basic
      understanding of C# and file I/O.'
  - name: What the code does
    text: '- `exportRange.ToImage` captures only the cells inside the range (pivot
      table or custom block). - `worksheet.ToImage` captures the *entire* visible
      area of the worksheet, effectively **save excel worksheet as image**.'
  - name: Multiple Pivot Tables
    text: 'If your workbook contains more than one pivot table, you can loop through
      them:'
  - name: Very Large Ranges
    text: 'Exporting a massive range (e.g., thousands of rows) can consume a lot of
      memory. Mitigate this by:'
  - name: Transparent Backgrounds
    text: 'If you need a transparent background (useful for overlaying on web pages),
      set the background color to `Color.Transparent` before export:'
  - name: File Permissions
    text: Make sure the target directory exists and your process has write permission.
      Otherwise `ToImage` throws an `IOException`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- ImageExport
title: Excelの範囲を画像としてエクスポート – 完全なC#ガイド
url: /ja/net/image-and-chart-operations/export-excel-range-as-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel 範囲を画像としてエクスポート – 完全 C# ガイド

Excel 範囲を画像としてエクスポートしたいと思ったことはありませんか？どの API 呼び出しを使えば良いか分からないこともあるでしょう。レポート用ダッシュボードを作成する場合や、PowerPoint スライド用にピボットテーブルのスナップショットが必要な場合など、セルブロックを PNG に変換するのは便利なテクニックです。

このガイドでは、**Excel 範囲を画像としてエクスポート** するだけでなく、シート全体を **Excel ワークシートを画像として保存** する方法も示す、自己完結型のサンプルを順を追って解説します。外部スクリプトは不要で、純粋な C# と Aspose.Cells だけなので、コードをコピー＆ペーストすればすぐに動作を確認できます。

## 学べること

- 既存のブックを読み込み、特定の範囲（ピボットテーブルまたは任意のセルブロック）を特定する。  
- 画像エクスポートオプション（形式、解像度、スケーリングなど）を設定する。  
- 単一の範囲を PNG、JPEG、または BMP にエクスポートする。  
- 同じロジックを使用して、**Excel ワークシートを画像として保存** をワンラインで実行する。  
- 複数のピボットテーブルや大きな範囲、一般的な落とし穴への対処法のヒント。

### 前提条件

- .NET 6.0 以降（コードは .NET Framework 4.7 以降でも動作します）。  
- Aspose.Cells for .NET ≥ 23.9（Aspose のウェブサイトから無料トライアルを取得できます）。  
- C# とファイル I/O の基本的な知識。  

これらが揃っていれば、さっそく始めましょう。

## 手順 1: プロジェクトのセットアップと名前空間のインポート

まず、新しいコンソール アプリを作成します（既存のプロジェクトにコードを統合しても構いません）。Aspose.Cells の NuGet パッケージを追加します：

```bash
dotnet add package Aspose.Cells
```

次に、必要な名前空間をインポートします：

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;   // For ImageOrPrintOptions
using System.Drawing.Imaging; // For ImageFormat enum
```

> **プロのコツ:** `using` 文はファイルの先頭にまとめておくと、コードが見やすくなります。特に後で Aspose の機能を追加する際に便利です。

## 手順 2: 対象範囲を含むブックをロードする

ディスク上にブックが必要です。`YOUR_DIRECTORY/input.xlsx` を実際のファイルパスに置き換えてください。

```csharp
// Step 2: Load the workbook containing the data you want to capture
Workbook workbook = new Workbook(@"YOUR_DIRECTORY/input.xlsx");

// Quick sanity check – make sure the file loaded correctly
if (workbook == null)
{
    Console.WriteLine("Failed to load workbook. Check the file path.");
    return;
}
```

この手順が重要な理由: `Workbook` オブジェクトはすべての Aspose.Cells 操作のエントリーポイントです。これがなければ、ワークシート、範囲、ピボットテーブルを参照できません。

## 手順 3: エクスポートする範囲を特定する

一般的なシナリオは 2 つあります：

1. **特定のピボットテーブル** – あなたが提示したコードは `PivotTables[0].PivotTableRange` を使用しています。  
2. **任意のセルブロック** – `worksheet.Cells.CreateRange("B2:D10")` を使用できます。  

以下では両方のケースを処理し、状況に合わせて選択できるようにしています。

```csharp
// Step 3a: Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Option A: Export the first pivot table's range
Range exportRange;
if (worksheet.PivotTables.Count > 0)
{
    exportRange = worksheet.PivotTables[0].PivotTableRange;
}
else
{
    // Option B: Fallback to a manual range (e.g., B2:D10)
    exportRange = worksheet.Cells.CreateRange("B2:D10");
}
```

> **ピボットテーブルを最初にチェックする理由:** 多くのレポートファイルは動的なピボットデータに依存しています。ピボットテーブルが存在しない場合は、フォールバックによりチュートリアルが正常に動作します。

## 手順 4: 画像エクスポートオプションの設定

Aspose.Cells は出力画像に対して細かい制御が可能です。最も一般的な設定は形式、解像度（DPI）、およびグリッドラインの有無です。

```csharp
// Step 4: Set up image export options
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG works well for lossless quality
    HorizontalResolution = 300,      // 300 DPI for crisp prints
    VerticalResolution = 300,
    // Optional: uncomment to hide gridlines
    // IsGridlinesVisible = false
};
```

`ImageFormat.Jpeg` や `ImageFormat.Bmp` に切り替えることもできます（下流システムがそれらの形式を好む場合）。DPI 設定は、画像を高解像度 PDF やスライド資料に埋め込む際に重要です。

## 手順 5: 範囲（またはシート全体）を画像としてエクスポートする

いよいよ本番です。`ToImage` メソッドは、範囲のビジュアル表現を直接ディスクに書き込みます。

```csharp
// Step 5a: Export the selected range to an image file
string rangeImagePath = @"YOUR_DIRECTORY/PivotRange.png";
exportRange.ToImage(rangeImagePath, imgOptions);
Console.WriteLine($"Range exported to: {rangeImagePath}");

// Step 5b: If you need to **save excel worksheet as image**, use the worksheet's ToImage overload
string sheetImagePath = @"YOUR_DIRECTORY/FullSheet.png";
worksheet.ToImage(sheetImagePath, imgOptions);
Console.WriteLine($"Worksheet exported to: {sheetImagePath}");
```

### コードの動作概要

- `exportRange.ToImage` は、範囲内（ピボットテーブルまたはカスタムブロック）のセルだけをキャプチャします。  
- `worksheet.ToImage` は、ワークシートの *全体* の表示領域をキャプチャし、実質的に **Excel ワークシートを画像として保存** します。  

どちらの呼び出しも先に設定したオプションを尊重するため、300 DPI の PNG ファイルが生成されます。

## エッジケースとよくある質問の対処

### 複数のピボットテーブル

ブックに複数のピボットテーブルがある場合は、ループで処理できます：

```csharp
for (int i = 0; i < worksheet.PivotTables.Count; i++)
{
    Range ptRange = worksheet.PivotTables[i].PivotTableRange;
    string outPath = $@"YOUR_DIRECTORY/Pivot_{i}.png";
    ptRange.ToImage(outPath, imgOptions);
    Console.WriteLine($"Pivot {i} saved to {outPath}");
}
```

### 非常に大きな範囲

膨大な範囲（例: 数千行）をエクスポートするとメモリを大量に消費します。以下の方法で対策できます：

- `HorizontalResolution` / `VerticalResolution` を下げる。  
- セクションごとにエクスポートする（範囲を小さなブロックに分割）。  

### 透明背景

透明な背景が必要な場合（Web ページ上に重ねる際に便利）、エクスポート前に背景色を `Color.Transparent` に設定します：

```csharp
imgOptions.BackgroundColor = System.Drawing.Color.Transparent;
```

### ファイル権限

対象ディレクトリが存在し、プロセスに書き込み権限があることを確認してください。権限がないと `ToImage` は `IOException` をスローします。

## 完全な動作例

以上をまとめると、すぐに実行できるコンソール プログラムは以下の通りです：

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing.Imaging;

namespace ExcelImageExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths for your environment
            string inputPath = @"YOUR_DIRECTORY/input.xlsx";
            string rangeImagePath = @"YOUR_DIRECTORY/PivotRange.png";
            string sheetImagePath = @"YOUR_DIRECTORY/FullSheet.png";

            // Load workbook
            Workbook workbook = new Workbook(inputPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // Determine which range to export
            Range exportRange;
            if (worksheet.PivotTables.Count > 0)
            {
                exportRange = worksheet.PivotTables[0].PivotTableRange;
            }
            else
            {
                exportRange = worksheet.Cells.CreateRange("B2:D10");
            }

            // Configure image options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // Export range as image
            exportRange.ToImage(rangeImagePath, imgOptions);
            Console.WriteLine($"Range exported to: {rangeImagePath}");

            // Export entire worksheet as image
            worksheet.ToImage(sheetImagePath, imgOptions);
            Console.WriteLine($"Worksheet exported to: {sheetImagePath}");
        }
    }
}
```

**期待される出力**（コンソール）:

```
Range exported to: YOUR_DIRECTORY/PivotRange.png
Worksheet exported to: YOUR_DIRECTORY/FullSheet.png
```

生成された PNG ファイルを開くと、選択した範囲とシート全体のピクセル単位で正確なスナップショットがそれぞれ確認できます。

## 結論

ここまでで、Aspose.Cells と C# を使用して **Excel 範囲を画像としてエクスポート** する方法と **Excel ワークシートを画像として保存** する方法のすべてを網羅しました。ブックのロードから画像オプションの微調整、複数ピボットの処理まで、手順はシンプルで再現性があります。

次にやってみると良いでしょう：

- `ImageFormat` のさまざまな値（JPEG、BMP）を試す。  
- `Document` クラスを使って画像を PDF と結合し、レポートを生成する。  
- フォルダー内の複数ファイルに対してプロセスを自動化する。  

このスニペットは、画像を Web API に渡す、メールに埋め込む、印刷用レポートを作成するなど、あらゆるワークフローに合わせて自由にカスタマイズしてください。コーディングを楽しんで、画像で Excel データを語らせましょう！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を応用した、密接に関連するトピックを取り上げています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [Aspose.Cells .NET を使用した Excel セルの画像エクスポート：ステップバイステップガイド](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)
- [Aspose.Cells for Java を使用した Excel ワークブックの画像エクスポート：ステップバイステップガイド](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Aspose Cells for Java を使用した Excel ワークブックの画像エクスポート](/cells/german/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}