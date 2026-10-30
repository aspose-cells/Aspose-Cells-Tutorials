---
category: general
date: 2026-09-11
description: Aspose.Cells を使用してピボットテーブルをコピーし、Excel を PPTX にエクスポートします。C# で編集可能な PPTX
  を生成し、ブックを PPTX として保存する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- export excel to pptx
- generate editable pptx
- save workbook as pptx
- export excel sheet pptx
language: ja
lastmod: 2026-09-11
og_description: Aspose.Cells を使用して C# でピボットテーブルをコピーし、Excel を PPTX にエクスポートします。数行のコードで編集可能な
  PPTX を生成し、ブックを PPTX として保存します。
og_image_alt: Screenshot of copy pivot table code and generated editable PPTX slide
og_title: ピボットテーブルをコピーしてExcelをPPTXにエクスポート – 完全なC#ガイド
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Copy pivot table and export Excel to PPTX using Aspose.Cells. Learn
    to generate editable PPTX and save workbook as PPTX in C#.
  headline: Copy pivot table and export Excel to PPTX with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel
- PPTX
- Pivot Table
title: Aspose.Cellsでピボットテーブルをコピーし、ExcelをPPTXにエクスポートする
url: /ja/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ピボットテーブルをコピーして Excel を PPTX にエクスポートする方法（Aspose.Cells 使用）

1 つのワークシートから別のワークシートへピボットテーブルをコピーし、その後 Excel ファイルを PowerPoint プレゼンテーションにエクスポートしたい場合、本ガイドで手順を示します。Aspose.Cells を使用すれば、数行の C# コードで編集可能な PPTX を生成し、ブックを PPTX として保存できます。

このチュートリアルでは、ピボットテーブルの移動、機能保持、そしてチャートや図形が編集可能なまま PPTX ファイルを作成するために必要なすべての手順をカバーします。外部ツールは不要で、Aspose.Cells ライブラリと .NET 開発環境だけで完了します。

## 達成できること

* **ピボットテーブルのコピー**：データ接続をすべて保持したまま、ソースシートから宛先シートへコピーします。  
* **Excel から PPTX へのエクスポート**：生成されたスライドを PowerPoint で編集可能にします。  
* **編集可能な PPTX の生成**：チャート、テーブル、図形が画像にフラット化されず、ネイティブな PowerPoint オブジェクトとして保持されます。  
* **ブックを PPTX として保存**：同じ Aspose.Cells API 呼び出しで実現します。  

### 前提条件

* .NET 6.0 以降（コードは .NET Framework 4.6+ でも動作します）。  
* Aspose.Cells for .NET（NuGet パッケージ `Aspose.Cells`）。  
* C# コンソールアプリケーションの基本的な知識。  

> **プロのヒント:** CLI を使用して NuGet パッケージをインストールし、最新バージョンを確実に取得してください:  
> ```bash
> dotnet add package Aspose.Cells
> ```

## ワークシート間でピボットテーブルをコピーする方法

最初の操作は、ピボットテーブルの定義を保持したまま移動することです。Aspose.Cells は `CopyRange` メソッドと `CopyOptions` オブジェクトを提供しており、`CopyPivotTable` フラグを設定できます。

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Load the workbook that contains the source and destination worksheets.
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Identify the worksheets by name.
Worksheet sourceSheet = workbook.Worksheets["Source"];
Worksheet destinationSheet = workbook.Worksheets["Destination"];

// Define the range that encloses the pivot table on the source sheet.
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

// Copy the range to the destination sheet, preserving the pivot table.
destinationSheet.Cells.CopyRange(
    sourceRange,
    0,                     // destination row index
    0,                     // destination column index
    new CopyOptions { CopyPivotTable = true });
```

**動作理由:**  
`CopyRange` はセルデータ、書式設定、そして `CopyPivotTable` が true の場合はピボットテーブルのキャッシュとメタデータもコピーします。宛先範囲はセル `A1`（行 0、列 0）から開始しますが、オフセットを変更して別の場所に配置することも可能です。

**一般的なエッジケース:** 宛先シートに同名のピボットテーブルが既に存在する場合、Aspose.Cells は自動的に新しいテーブルの名前を変更し、名前衝突を防止します。

## Excel を PPTX にエクスポートし、編集可能な PPTX を生成する

ピボットテーブルが配置されたら、ブック全体を PPTX ファイルにエクスポートできます。`ImageOrPrintOptions` クラスで `ExportImageFormat = ImageFormat.Pptx` を指定すると、Aspose.Cells は出力をラスタ画像ではなく PowerPoint プレゼンテーションとして扱います。

```csharp
// Configure export options to produce an editable PPTX.
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ExportImageFormat = ImageFormat.Pptx
};

// Save the workbook as an editable PPTX file.
workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);
```

**動作理由:**  
`ExportImageFormat` を `Pptx` に設定すると、Aspose.Cells は各ワークシートをスライドに変換します。図形、チャート、ピボットテーブルはネイティブな PowerPoint オブジェクトとして書き出されるため、PowerPoint でダブルクリックすると基になるデータを編集できます。

**大規模ブック向けのヒント:** エクスポートしたくないシートがある場合は、`Save` を呼び出す前に `workbook.Worksheets.RemoveAt(index)` で不要なシートを削除してください。これにより PPTX のファイルサイズが削減されます。

## 完全な実行可能サンプル

以下は、前述の手順をすべて結びつけた完全なプログラムです。`YOUR_DIRECTORY` を実際のパスに置き換えて使用してください。

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Export;

class Example
{
    static void Main()
    {
        // 1. Load the workbook that contains the source and destination worksheets.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Identify the source and destination worksheets.
        Worksheet sourceSheet = workbook.Worksheets["Source"];
        Worksheet destinationSheet = workbook.Worksheets["Destination"];

        // 3. Define the range that holds the pivot table.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // 4. Copy the range, preserving the pivot table.
        destinationSheet.Cells.CopyRange(
            sourceRange,
            0,
            0,
            new CopyOptions { CopyPivotTable = true });

        // 5. Set up export options to generate an editable PPTX.
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
        {
            ExportImageFormat = ImageFormat.Pptx
        };

        // 6. Save the workbook as a PPTX document.
        workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);

        Console.WriteLine("Pivot table copied and workbook exported to PPTX successfully.");
    }
}
```

### 期待される出力

プログラムを実行すると次のように表示されます:

```
Pivot table copied and workbook exported to PPTX successfully.
```

`output.pptx` を Microsoft PowerPoint で開くと、コピーされたピボットテーブルが編集可能なチャートとしてスライドに表示されます。チャートをダブルクリックすると PowerPoint のチャートエディタが起動し、シリーズや軸、データラベルを Excel に戻すことなく変更できます。

## 典型的な落とし穴と対処法

| 問題 | 原因 | 対策 |
|-------|-------|-----|
| ピボットテーブルが静的画像として表示される | `CopyPivotTable` フラグが省略されている、または `ExportImageFormat` が `Png` に設定されている | `CopyPivotTable = true` と `ExportImageFormat = ImageFormat.Pptx` を確実に設定する。 |
| 宛先シートが空白になる | ソース範囲がピボットテーブル全体をカバーしていない | 範囲（例: `"A1:H30"`）を拡大してすべてのピボットフィールドを含める。 |
| エクスポートされた PPTX が巨大になる | 不要なワークシートが含まれている | `Save` 前に不要なシートを削除する。 |
| PowerPoint でチャートが編集できない | PPTX 対応がない古いバージョンの Aspose.Cells を使用している | 最新の Aspose.Cells バージョンにアップグレードする（リリースノートを確認）。 |

## 次のステップと関連トピック

* **カスタムスライドレイアウトで Excel シートを PPTX にエクスポート** – `WorksheetToPdfConverter` を活用してスライド外観を細かく制御します。  
* **Excel を PDF にエクスポート** – `ImageFormat.Pptx` を `ImageFormat.Pdf` に置き換えて PDF を生成します。  
* **エクスポート後に PPTX をプログラムで操作** – `Aspose.Slides` ライブラリを使用してアニメーションやスピーカーノートを追加します。  

**copy pivot table**、**export excel to pptx**、**generate editable pptx** をマスターすれば、スプレッドシートからプレゼンテーションデッキへデータを直接移行し、編集可能性を失わないエンドツーエンドのレポートパイプラインを構築できます。

---


## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法に密接に関連するトピックを扱っており、ステップバイステップのコード例と解説が含まれています。これらを活用して、API の追加機能を習得し、独自プロジェクトで代替実装アプローチを検討してください。

- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Create a Pivot Table in Excel Using Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}