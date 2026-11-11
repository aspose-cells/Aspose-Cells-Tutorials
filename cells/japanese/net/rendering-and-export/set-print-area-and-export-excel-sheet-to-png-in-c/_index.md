---
category: general
date: 2026-10-26
description: C#で印刷範囲を設定し、ExcelシートをPNGにエクスポートします。画像エクスポートのオプションを学び、PNGのエクスポート方法を理解し、ブックから印刷可能な画像を取得します。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area
- excel sheet to png
- how to export png
- export excel image
- image export options
language: ja
lastmod: 2026-10-26
og_description: C#で印刷範囲を設定し、ExcelシートをPNGにエクスポートする方法。このステップバイステップのチュートリアルでは、画像エクスポートオプションとブックからPNGをエクスポートする手順を解説します。
og_image_alt: Screenshot showing an Excel worksheet with the print area set and exported
  as a PNG image
og_title: 印刷範囲を設定してExcelシートをPNGにエクスポートする – C# ガイド
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Set print area and export an Excel sheet to PNG in C#. Learn image
    export options, how to export PNG, and get a printable image from a workbook.
  headline: Set print area and export Excel sheet to PNG in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: C#で印刷範囲を設定し、ExcelシートをPNGにエクスポートする
url: /ja/net/rendering-and-export/set-print-area-and-export-excel-sheet-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 印刷範囲を設定して Excel シートを PNG にエクスポートする（C#）

Excel シートを PNG にエクスポートする前に **印刷範囲を設定** する必要がある場合、このガイドで手順を示します。画像エクスポートオプションを設定し、ワークシートの印刷範囲を調整し、結果を画像として保存する完全な C# の例が確認できます。

Excel シートを PNG にエクスポートすることは、レポートやメール、ウェブページにワークシートのスナップショットを埋め込みたいときに一般的な要件です。以下のコードはピボットテーブルを含む任意のブックで動作しますが、通常のデータ範囲にも同様に適用できます。外部ツールは不要で、Aspose.Cells for .NET ライブラリだけで実現できます。

## 前提条件

- .NET 6.0 以降（サンプルは .NET 6 を対象としていますが、最近の .NET バージョンであればどれでも動作します）
- Aspose.Cells for .NET（NuGet でインストール: `Install-Package Aspose.Cells`）
- C# と Excel の概念（ワークシートや印刷範囲など）に関する基本的な知識

## 手順 1: 画像エクスポートオプションの設定

最初に `ImageOrPrintOptions` インスタンスを作成します。このオブジェクトは Aspose.Cells にシートを画像としてどのようにレンダリングするかを指示します。

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

// Define image export options (PNG format)
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    // Export quality settings can be adjusted here
    ImageFormat = ImageFormat.Png,
    // Optional: set resolution (DPI) for higher‑quality PNGs
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**Why this matters:** `ImageOrPrintOptions` は出力形式、解像度、その他のレンダリング詳細を制御します。PNG を使用することでロスレスな品質が保たれ、テキストやグラフィックが鮮明に必要なレポートに最適です。

## 手順 2: ワークブックを読み込み、対象のワークシートにアクセスする

```csharp
// Load an existing workbook (replace with your file path)
Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

// Access the first worksheet in the workbook
Worksheet worksheet = wb.Worksheets[0];
```

**Why this matters:** 印刷範囲はワークシート単位の設定なので、特定の `Worksheet` オブジェクトを操作する必要があります。

## 手順 3: 印刷したい範囲を特定する

多くの場合、対象データはピボットテーブル内にあります。以下のコードはシート上の最初のピボットテーブルのデータ範囲を取得します。

```csharp
// Get the data range of the first pivot table on the worksheet
CellArea pivotDataRange = worksheet.PivotTables[0].PivotDataRange;
```

ワークシートにピボットテーブルが存在しない場合は、`pivotDataRange` を手動で作成した任意の `CellArea` に置き換えることができます。例:

```csharp
CellArea customRange = new CellArea(0, 0, 20, 10); // A1:K21
```

## 手順 4: 選択した範囲に合わせて **印刷範囲を設定**

```csharp
// Set the worksheet's print area to match the pivot table's data range
worksheet.PageSetup.PrintArea = pivotDataRange.RefersTo;
```

**Why this matters:** 印刷範囲は Excel（および Aspose.Cells）に対して、画像に含めるセルを指示します。印刷範囲をピボットデータ範囲と一致させることで、余白がなくなり、エクスポートされた PNG に必要なデータだけが含まれます。

## 手順 5: ワークシートを PNG 画像としてエクスポート

```csharp
// Export the worksheet to an image using the defined options
// and assign the resulting image to the first picture shape on the sheet
worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);

// Optionally, save the image to a file for external use
worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);
```

**Why this matters:** `worksheet.ToImage` は事前に設定した印刷範囲を尊重するため、PNG ファイルには定義したセルだけが正確に含まれます。画像をピクチャーシェイプに割り当てればブックに再埋め込みでき、ディスクに保存すれば単体ファイルとして利用できます。

## 完全な動作例

すべての手順を組み合わせると、すぐに実行可能な自己完結型プログラムが完成します。

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

class ExportExcelToPng
{
    static void Main()
    {
        // 1️⃣ Configure image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 2️⃣ Load the workbook
        Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

        // 3️⃣ Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // 4️⃣ Get the data range of the first pivot table (or define your own)
        CellArea dataRange = worksheet.PivotTables[0].PivotDataRange;

        // 5️⃣ **Set print area** to the data range
        worksheet.PageSetup.PrintArea = dataRange.RefersTo;

        // 6️⃣ Export the worksheet as PNG
        worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);
        worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);

        Console.WriteLine("Export complete: WorksheetExport.png created.");
    }
}
```

### 期待される出力

プログラムを実行すると `C:\Temp\WorksheetExport.png` が作成されます。ファイルを開くと、**印刷範囲を設定** したセル（この例ではピボットテーブルのデータ）だけが含まれた鮮明な PNG 画像が表示されます。この画像は Word 文書、PowerPoint スライド、ウェブページに追加の変換作業なしで挿入可能です。

## 複数のワークシートやピボットテーブルの処理

- **Multiple worksheets:** `wb.Worksheets` をループし、エクスポートが必要な各シートに対して手順 3‑5 を繰り返します。
- **Multiple pivot tables:** 適切な `PivotTables[index]` を選択するか、`worksheet.PivotTables` を列挙して各テーブルを個別にエクスポートします。
- **No pivot table:** 手順 3 のコメントを参照し、`CellArea` を手動で作成して `PrintArea` に割り当てます。

## 実践的なヒント (E‑E‑A‑T)

- **Pro tip:** 印刷品質の PNG 用に `HorizontalResolution` と `VerticalResolution` を 300 DPI に設定します。ウェブ用にファイルサイズを小さくしたい場合は、解像度を下げても構いません。
- **Watch out for empty picture shapes:** ワークシートにピクチャーシェイプが無い場合は、画像を割り当てる前に 1 つ追加してください:

```csharp
if (worksheet.Pictures.Count == 0)
{
    worksheet.Pictures.Add(0, 0, 0, 0);
}
```

- **Performance:** 複数シートで同じ `ImageOrPrintOptions` インスタンスを再利用すると、不要なメモリ割り当てを回避できます。
- **Compatibility:** Aspose.Cells 23.9 以降は .NET 6 以降を完全にサポートしています。以前のバージョンでは API 名の調整が必要になる場合があります。

## 結論

これで **印刷範囲を設定** し、Excel を PNG にエクスポートする方法が分かりました。

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを検討したりするのに役立ちます。

- [Excel を PNG にエクスポートする方法 – 完全ステップバイステップガイド](/cells/english/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/)
- [C# と Aspose.Cells を使用して Excel 範囲を画像としてエクスポートする方法](/cells/english/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/)
- [Excel シートを PNG に – C# でピボットテーブルを PNG としてエクスポートする方法](/cells/english/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}