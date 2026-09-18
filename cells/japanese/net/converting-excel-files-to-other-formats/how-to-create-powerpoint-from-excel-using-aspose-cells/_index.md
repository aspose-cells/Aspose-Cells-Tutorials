---
category: general
date: 2026-09-18
description: Aspose.Cells を使用して Excel から PowerPoint を作成 – ピボットテーブルをコピーし、範囲をエクスポートし、数行の
  C# コードで PPTX として保存します。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create powerpoint from excel
- how to copy pivot table
- copy range between workbooks
- how to export excel to pptx
- save workbook as pptx
language: ja
lastmod: 2026-09-18
og_description: Excel から PowerPoint をすばやく作成。ピボットテーブルのコピー、範囲のエクスポート、そして Aspose.Cells
  を使用してブックを PPTX として保存する方法を学びましょう。
og_image_alt: Screenshot of a PowerPoint slide generated from Excel data
og_title: Aspose.CellsでExcelからPowerPointを作成する – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  headline: How to create PowerPoint from Excel using Aspose.Cells
  type: TechArticle
- description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  name: How to create PowerPoint from Excel using Aspose.Cells
  steps:
  - name: Load the source workbook and define the range
    text: You must load the workbook that holds the source data and the pivot table.
      Selecting a precise range ensures that only the needed cells are transferred,
      which keeps the resulting slide lightweight.
  - name: Prepare the destination workbook
    text: Aspose.Cells treats a PowerPoint slide as a workbook when you save it in
      PPTX format. Creating a fresh workbook gives you a clean canvas for the copied
      range.
  - name: Copy the range while preserving the pivot table
    text: The `CopyRange` method accepts a `PasteOptions` object. Setting `CopyPivotTables
      = true` tells Aspose.Cells to keep the pivot table structure intact, not just
      the rendered values.
  - name: Save the workbook as a PowerPoint file
    text: Finally, export the workbook to PPTX format. The `SaveFormat.Pptx` flag
      tells Aspose.Cells to write the worksheet as a PowerPoint slide.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel to PowerPoint
title: Aspose.Cells を使用して Excel から PowerPoint を作成する方法
url: /ja/net/converting-excel-files-to-other-formats/how-to-create-powerpoint-from-excel-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel から PowerPoint を作成する方法（Aspose.Cells 使用）

Excel から PowerPoint を作成する必要がある場合、このガイドでは簡潔なエンドツーエンドのソリューションを示します。ピボットテーブルのコピー、選択範囲のエクスポート、数行の C# コードだけで PPTX ファイルとして保存する方法が分かります。

スプレッドシート データから直接スライド デッキを生成すれば、レポート作成ワークフローで時間がかかる手動のコピー＆ペースト作業を省くことができます。このチュートリアルでは、プロジェクトのセットアップから最終的な PPTX ファイルの作成まで、必要なすべてをカバーし、最新の Aspose.Cells for .NET でも動作します。

## 前提条件

開始する前に、以下が揃っていることを確認してください。

* **Aspose.Cells for .NET**（バージョン 23.12 以降）。NuGet でインストールします：`Install-Package Aspose.Cells`。
* **.NET 6 以上**の開発環境（Visual Studio 2022 または VS Code が使用可能）。
* データと再利用したいピボットテーブルを含む Excel ブック（`Source.xlsx`）。
* 出力フォルダーへの書き込み権限。

追加のサードパーティ ライブラリは不要です。

## Excel から PowerPoint を作成する手順

このプロセスは、後述のコード例に直接対応する 4 つの論理ステップで構成されています。

### 手順 1: ソース ブックを読み込み、範囲を定義する

ピボットテーブルが含まれるソース データを保持しているブックを読み込む必要があります。正確な範囲を選択することで、必要なセルだけが転送され、結果として生成されるスライドが軽量になります。

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// Select the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that contains the pivot table and surrounding data
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

**重要ポイント:**  
`CreateRange` は `Range` オブジェクトを作成し、まとめてコピーできるようにします。範囲を `A1:G20` に限定することで、関係のないセルが PowerPoint に取り込まれ、ファイルが肥大化するのを防げます。

### 手順 2: 宛先ブックを準備する

Aspose.Cells は PPTX 形式で保存するとき、PowerPoint スライドをブックとして扱います。新しいブックを作成すると、コピーした範囲用のクリーンなキャンバスが得られます。

```csharp
// Create a new empty workbook that will become the PowerPoint slide
Workbook destinationWorkbook = new Workbook();

// Use the first worksheet of the new workbook
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

**ヒント:** 複数のスライドが必要な場合は、追加のワークシートを作成し、後でそれぞれを個別の PPTX ファイルとして保存できます。

### 手順 3: ピボットテーブルを保持しながら範囲をコピーする

`CopyRange` メソッドは `PasteOptions` オブジェクトを受け取ります。`CopyPivotTables = true` を設定すると、Aspose.Cells はピボットテーブルの構造を保持し、単なる表示値だけでなく完全なピボットテーブルをコピーします。

```csharp
// Copy the defined range, preserving the pivot table definition
destinationSheet.Cells.CopyRange(
    sourceRange,
    new PasteOptions { CopyPivotTables = true });
```

**動作概要:**  
`CopyPivotTables` が true の場合、宛先シートはソース データとピボット キャッシュの両方を受け取ります。これにより、ピボットテーブルは完全に機能し、ソース データが変更されたときに PowerPoint 内で更新できるようになります。

### 手順 4: ブックを PowerPoint ファイルとして保存する

最後に、ブックを PPTX 形式でエクスポートします。`SaveFormat.Pptx` フラグは、Aspose.Cells に対してワークシートを PowerPoint スライドとして書き出すよう指示します。

```csharp
// Save the destination workbook as a PowerPoint presentation
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);
```

**結果:**  
`CopyWithPivot.pptx` を Microsoft PowerPoint（または互換ビューア）で開くと、コピーされた範囲とライブ ピボットテーブルが表示された単一スライドが表示されます。PowerPoint 上でピボットテーブルを操作できます。

## 完全に実行可能なサンプル

以下は新しいコンソール プロジェクトに貼り付けてすぐに実行できる、完全なプログラムです。

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook and select the range containing the pivot table
            Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
            Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
            Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

            // 2️⃣ Create a fresh workbook that will become the PowerPoint slide
            Workbook destinationWorkbook = new Workbook();
            Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

            // 3️⃣ Copy the range, preserving the pivot table definition
            destinationSheet.Cells.CopyRange(
                sourceRange,
                new PasteOptions { CopyPivotTables = true });

            // 4️⃣ Export the workbook as a PPTX file
            destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);

            Console.WriteLine("PowerPoint file created successfully.");
        }
    }
}
```

**期待される出力:**  
プログラムを実行すると “PowerPoint file created successfully.” と表示され、`CopyWithPivot.pptx` という名前のファイルが生成されます。PowerPoint でファイルを開くと、コピーされた Excel 範囲がソース ワークシートと同じ見た目で単一スライドに表示され、PowerPoint 内からピボットテーブルを更新できる状態になっています。

## よくあるバリエーションとエッジケース

| 状況 | 変更点 |
|-----------|----------------|
| **複数のピボットテーブル** | 各テーブル用に個別の `Range` オブジェクトを定義し、`CopyRange` をそれぞれ呼び出すか、同じデータ ソースを共有している場合はシート全体をコピーします。 |
| **大規模データセット** | 範囲を拡大（例: `"A1:Z5000"`）します。`PasteOptions.CompressData = true` を有効にすると PPTX のサイズを削減できます。 |
| **異なるスライド レイアウト** | PPTX として保存した後、PowerPoint でカスタム レイアウトやテーマを適用します。データは引き続き編集可能です。 |
| **ストリームへの保存** | Web API で PPTX を返す必要がある場合は、`destinationWorkbook.Save(stream, SaveFormat.Pptx)` を使用します。 |
| **セル書式の保持** | `PasteOptions.PasteType = PasteType.All` を設定すると、フォント、色、罫線などが保持されます。 |

**プロのコツ:** `Save` を呼び出す前に、宛先フォルダーが存在することを必ず確認してください。フォルダーがない場合、`Save` は `DirectoryNotFoundException` をスローします。

## 結論

これで、Excel から PowerPoint を作成し、ピボットテーブルをコピーして PPTX ファイルとしてエクスポートする方法が分かりました。ソース ブックの読み込み、範囲の定義、`CopyPivotTables` を使用したコピー、PPTX 形式での保存という手順は、信頼性が高く本番環境でも使えるワークフローを網羅しています。

次は **複数シートの Excel を PPTX にエクスポート** する方法や、**複数ソースからデータをマージしてスライド デッキを生成** する際の **ブック間での範囲コピー** を学んでみましょう。どちらも同じ API をベースにしており、複雑なレポート パイプラインの自動化に活用できます。

Happy coding, and enjoy turning your spreadsheets into polished presentations!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを基にした関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、API の追加機能を習得したり、代替実装アプローチを自分のプロジェクトに取り入れたりするのに役立ちます。

- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [How to Create and Save Excel Files with Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}