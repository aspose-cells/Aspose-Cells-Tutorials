---
category: general
date: 2026-11-19
description: Aspose.Cells の CopyOptions を使用して範囲をコピーする方法を学び、書式やピボットテーブルを保持しながら、書式付き
  Excel 範囲をコピーします。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range using copyoptions
- copy excel range with formatting
- Aspose.Cells copy range
- preserve pivot tables Aspose
- Excel automation C#
language: ja
lastmod: 2026-11-19
og_description: Aspose.Cells の CopyOptions を使用して範囲をコピーすると、完全な書式設定とピボットテーブルを保持したまま
  Excel データを複製でき、信頼性の高いブック操作が可能になります。
og_image_alt: Screenshot of C# code that copies an Excel range using Aspose.Cells
  CopyOptions
og_title: Aspose.CellsでCopyOptionsを使用して範囲をコピーする – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  headline: How to copy range using CopyOptions in Aspose.Cells
  type: TechArticle
- description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  name: How to copy range using CopyOptions in Aspose.Cells
  steps:
  - name: Why `CopyOptions` matters
    text: '* **Performance** – The library performs a single internal operation rather
      than copying cells one‑by‑one. * **Accuracy** – All visual aspects (fonts, colors,
      borders) survive the move, which eliminates visual drift in generated reports.
      * **Reliability** – Pivot tables remain functional because the'
  - name: What if the destination area overlaps the source?
    text: 'Aspose.Cells throws an `ArgumentException`. To avoid this, calculate a
      destination that does not intersect the source, or copy to a different worksheet:'
  - name: How to copy between different workbooks?
    text: 'Create a second `Workbook` instance for the target file and use the same
      `CopyOptions` object:'
  - name: Does `CopyOptions` also copy merged cells?
    text: Yes. The `CopyStyle` flag includes merged‑cell information. If you need
      finer control, set `options.CopyMergedCells = true` (available in newer versions).
  - name: What about large ranges (thousands of rows)?
    text: The operation is memory‑efficient, but you may want to increase the `WorkbookSettings`
      `MemorySetting` to `MemorySetting.MemoryPreference` for very large files.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Aspose.CellsでCopyOptionsを使用して範囲をコピーする方法
url: /ja/net/range-management/how-to-copy-range-using-copyoptions-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells で CopyOptions を使用して範囲をコピーする方法

Aspose.Cells で **CopyOptions を使用して範囲をコピー** する必要がある場合、このガイドではセルのブロックを複製し、すべての書式設定や埋め込みピボットテーブルをそのまま保持する方法を正確に示します。ワークシート間でデータを移動する際に書式を保持するのに苦労する開発者が多く、`CopyOptions` クラスは余分な手作業なしでこの問題を解決します。

このチュートリアルで学べること:

* Excel ブック内でソース領域と宛先領域を定義する方法。  
* `CopyOptions` を使用してセルの書式、列幅、ピボットテーブルを保持する方法。  
* 結果を新しいファイルに保存し、下流処理に備える方法。

この例は任意の `.xlsx` ファイルで動作し、必要なのは Aspose.Cells for .NET ライブラリだけです。

## Prerequisites

開始する前に、以下がインストールされていることを確認してください:

* .NET 6.0 以降  
* 有効な Aspose.Cells for .NET ライセンス（または無料評価キー）  
* Visual Studio 2022 またはお好みの C# IDE  

`Aspose.Cells` 以外に追加の NuGet パッケージは必要ありません。

## Step 1: Set up the project and import namespaces

新しいコンソール アプリケーションを作成し、Aspose.Cells への参照を追加します:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Your code will go here
        }
    }
}
```

`using Aspose.Cells;` ディレクティブにより、`Workbook`、`CellArea`、`CopyOptions` にアクセスできるようになります。

## Step 2: Load the workbook you want to modify

```csharp
// Step 2: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`Workbook` は Excel ファイル全体を表します。`YOUR_DIRECTORY` を、ソース ファイルが格納されているフォルダーに置き換えてください。

## Step 3: Define the source and destination ranges

```csharp
// Step 3: Define the source range (A1:H30)
CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");

// Step 3b: Define the destination range (A35:H64)
CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");
```

`CellArea.CreateCellArea` は、左上セルと右下セルのアドレスに基づいて矩形領域を作成します。コピーしたいブロックのサイズに合わせて座標を調整してください。

## Step 4: Copy the range while preserving formatting and pivot tables

```csharp
// Step 4: Copy the range using CopyOptions
CopyOptions options = new CopyOptions
{
    // Preserve all cell styles, number formats, and column widths
    CopyStyle = true,
    // Keep formulas unchanged (they will still reference the original sheet)
    CopyFormula = true,
    // Preserve any pivot tables that intersect the copied area
    CopyPivotTables = true,
    // Retain data validation and conditional formatting
    CopyDataValidation = true,
    CopyConditionalFormatting = true
};

workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
```

`CopyOptions` オブジェクトは Aspose.Cells に保持すべき項目を正確に指示します。`CopyPivotTables = true` を設定することが、ソースにピボットテーブルが含まれる場合に **CopyOptions を使用して範囲をコピー** する鍵となります。他のフラグにより **書式付き Excel 範囲のコピー** が自動的に実現され、コピー後にスタイルを再適用する余分なコードは不要です。

### Why `CopyOptions` matters

* **Performance（パフォーマンス）** – ライブラリはセルを一つずつコピーするのではなく、単一の内部操作で処理します。  
* **Accuracy（正確性）** – フォント、色、罫線などの視覚的要素がすべて保持され、生成レポートでの見た目のずれがなくなります。  
* **Reliability（信頼性）** – ピボットテーブルはキャッシュとソース参照が複製されるため、機能し続けます。

## Step 5: Save the modified workbook

```csharp
// Step 5: Save the workbook with the copied range
workbook.Save("YOUR_DIRECTORY/output.xlsx");
Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
```

`Save` を呼び出した後、`output.xlsx` には元のデータに加えて、宛先位置に複製されたブロックが書式とピボットテーブルを保持したまま保存されます。

## Full source code for reference

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // Define source and destination ranges
            CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");
            CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");

            // Configure copy options to preserve everything
            CopyOptions options = new CopyOptions
            {
                CopyStyle = true,
                CopyFormula = true,
                CopyPivotTables = true,
                CopyDataValidation = true,
                CopyConditionalFormatting = true
            };

            // Perform the copy operation
            workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);

            // Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");
            Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
        }
    }
}
```

このプログラムを実行すると次のように出力されます:

```
Range copied successfully. Output saved to output.xlsx
```

Excel で `output.xlsx` を開くと、A1:H30 のブロックが A35:H64 に複製され、すべてのセルの色、罫線、数値書式、ピボットテーブルがそのまま残っていることが確認できます。

## Common questions and edge‑case handling

### What if the destination area overlaps the source?

Aspose.Cells は `ArgumentException` をスローします。これを回避するには、ソースと交差しない宛先を計算するか、別のワークシートへコピーしてください:

```csharp
Worksheet destSheet = workbook.Worksheets.Add("CopySheet");
destSheet.Cells.CopyRange(sourceRange, CellArea.CreateCellArea("A1", "H30"), options);
```

### How to copy between different workbooks?

ターゲット ファイル用に 2 番目の `Workbook` インスタンスを作成し、同じ `CopyOptions` オブジェクトを使用します:

```csharp
Workbook target = new Workbook();
target.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
target.Save("target.xlsx");
```

### Does `CopyOptions` also copy merged cells?

はい。`CopyStyle` フラグには結合セル情報も含まれます。より細かい制御が必要な場合は、`options.CopyMergedCells = true`（新しいバージョンで利用可能）を設定してください。

### What about large ranges (thousands of rows)?

この操作はメモリ効率が高いですが、非常に大きなファイルの場合は `WorkbookSettings` の `MemorySetting` を `MemorySetting.MemoryPreference` に変更するとよいでしょう。

## Pro tips

* **同じ `CopyOptions` インスタンスを複数のコピー操作で再利用** – オブジェクト割り当てのオーバーヘッドを削減できます。  
* **コピー前に範囲を検証** – `if (!CellArea.IsValid(sourceRange) || !CellArea.IsValid(destinationRange))` を使用すると、タイプミスによるエラーを早期に検出できます。  
* **大規模データのコピー中は計算をオフにする** (`workbook.Settings.CalcMode = CalculationMode.Manual`) と処理速度が向上します。コピー後に結果が必要な場合は `workbook.CalculateFormula()` を呼び出してください。

## Conclusion

これで Aspose.Cells で **CopyOptions を使用して範囲をコピー** する方法が分かり、**書式付き Excel 範囲のコピー** を実現しながらピボットテーブルやその他高度な機能を保持できるようになりました。このアプローチにより手動でのスタイル再適用が不要となり、Excel 自動化の堅牢性と保守性が向上します。

次に試すべきステップ:

* `CopyOptions` を使用してシート全体を複製する。  
* `WorksheetCollection.AddCopy` と組み合わせてテンプレートベースのレポート生成を行う。  
* コードを ASP.NET Core API に統合し、オンデマンドで Excel 変換を提供する。

さまざまなソース/宛先座標で実験し、結果をコメントで共有してください！

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [Excel Aspose Cells .NET 範囲コピー](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells .NET 範囲コピー](/cells/french/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells .NET 範囲コピー](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}