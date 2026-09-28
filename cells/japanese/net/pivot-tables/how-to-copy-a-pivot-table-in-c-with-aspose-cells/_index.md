---
category: general
date: 2026-09-27
description: Aspose.Cells を使用して C# でピボットテーブルをコピーする方法を学びます。書式付きで行をコピーする、ピボットテーブルを別シートにコピーする、ピボットテーブルを新しいブックにエクスポートする、が含まれます。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy rows with formatting
- copy pivot table to another sheet
- how to copy excel rows
- export pivot table to new workbook
language: ja
lastmod: 2026-09-27
og_description: Aspose.Cells を使用して C# でピボットテーブルをコピーする方法。ステップバイステップのガイドに従って、書式付きで行をコピーし、ピボットテーブルを別のシートに移動し、新しいブックにエクスポートします。
og_image_alt: Excel sheet showing a copied pivot table after using Aspose.Cells
og_title: C#でピボットテーブルをコピーする方法 – 完全なAspose.Cellsガイド
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to copy a pivot table in C# using Aspose.Cells. Includes
    copy rows with formatting, copy pivot table to another sheet, and export pivot
    table to a new workbook.
  headline: How to copy a pivot table in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot table
title: C# と Aspose.Cells を使用してピボットテーブルをコピーする方法
url: /ja/net/pivot-tables/how-to-copy-a-pivot-table-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# と Aspose.Cells を使用してピボットテーブルをコピーする方法

ワークシート間で **ピボットテーブルをコピー** する必要がある場合、Aspose.Cells を使用した C# での **ピボットテーブルのコピー方法** を学ぶことで、手作業の時間を何時間も節約できます。この方法では **書式付きで行をコピー** でき、ピボットキャッシュをそのまま保持し、さらに **ピボットテーブルを新しいブックにエクスポート** して単体ファイルとして利用することも可能です。

このチュートリアルでは、以下の完全なワークフローを順に解説します：

* ワークブックを作成する、  
* 書式を保持したままピボットテーブル範囲をコピーする、  
* コピーしたデータを新しいシートに配置する、  
* 結果を別ファイルとして保存する。

組み込みの `CopyRows` メソッドが **ピボットテーブルを別シートにコピー** する最も信頼できる方法である理由を確認でき、非表示行や外部データソースなどのエッジケースへの対処法も紹介します。

## 前提条件

Before you start, make sure you have:

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 or later | Aspose.Cells は .NET 6+ をサポートしており、最高のパフォーマンスを提供します。 |
| Visual Studio 2022 (or any C# IDE) | NuGet パッケージを復元できるエディタが必要です。 |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | このライブラリはサンプルで使用する `CopyRows` API を提供します。 |
| A source Excel file (`source.xlsx`) that contains a pivot table in the range `A1:G20` | コードはこの特定の範囲をコピーします。ピボットテーブルが大きい場合は範囲を調整してください。 |

Install the library with the NuGet CLI or Package Manager Console:

```bash
dotnet add package Aspose.Cells
```

## 手順 1: ピボットテーブルを含むワークブックをロードする

最初の行で、Excel ファイル全体を表す `Workbook` オブジェクトを作成します。ファイルを一度ロードすれば、すべてのワークシートに対して読み書きが可能になります。

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **この手順が重要な理由** – ワークブックをロードしないと、以降の `CopyRows` 呼び出しはソースデータやピボットキャッシュを参照できません。

## 手順 2: ソースと宛先のワークシートを準備する

コピーしたピボットテーブルを配置する宛先シートが必要です。以下のコードは、元のピボットテーブルがある最初のワークシートを取得し、**Copy** という名前の新しいシートを追加します。

```csharp
// Get the source worksheet (index 0 = first sheet)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a new worksheet that will receive the copied rows
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
```

> **プロのコツ:** 宛先シートがすでに存在する場合は、重複した名前を防ぐために先に `Worksheets.RemoveAt(index)` を呼び出してください。

## 手順 3: ピボットテーブルを囲むセル領域を定義する

`CellArea` オブジェクトは、移動したい範囲の左上セルと右下セルを表します。この例ではピボットテーブルは `A1:G20` を占めています。テーブルが大きい場合は座標を調整してください。

```csharp
// Define the range that includes the pivot table (A1:G20)
CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");
```

## 手順 4: 書式付きで行をコピーし、ピボットキャッシュを保持する

`CopyRows` メソッドは、ソースシートから宛先シートへ **行** をコピーします。`CopyOptions.CopyAll` を指定することで、値、書式、チャート、埋め込みオブジェクト（すべてピボットテーブルの一部）を確実に転送できます。

```csharp
// Copy the rows from the source area to the destination sheet
sourceSheet.CopyRows(
    sourceArea.StartRow,          // start row in the source sheet
    destinationSheet,            // target worksheet
    0,                            // start row in the destination sheet
    sourceArea.RowCount,          // number of rows to copy
    CopyOptions.CopyAll);        // copy everything (values, formats, objects, etc.)
```

### ピボットテーブルで `CopyRows` が `Copy` より優れている理由

* `CopyRows` は内部のピボットキャッシュを尊重するため、コピーされたピボットテーブルは機能し続けます。
* 元シートと同じ **書式付きで行をコピー** した状態を正確に保持します。
* 単純な範囲の `Copy` とは異なり、非表示行や関連するスライサーも一緒にコピーします。

## 手順 5: コピーしたピボットテーブルを含むワークブックを保存する

最後に、変更したワークブックをディスクに書き込みます。新しいファイルには元のシートに加えて、元のピボットテーブルの完全に機能する複製を保持する **Copy** シートが含まれます。

```csharp
// Save the workbook to a new file
workbook.Save(@"YOUR_DIRECTORY\pivot_copied.xlsx");
```

### 期待される結果

`pivot_copied.xlsx` を開くと:

* シート **Sheet1** には元のデータとピボットテーブルがそのまま残っています。
* シート **Copy** には同一のレイアウト、フィルタ、書式を持つピボットテーブルが表示されます。
* ピボットキャッシュが行と共にコピーされたため、すべての数式とデータ接続が保持されます。

## 同一ブック内の別シートにピボットテーブルをコピーする方法

ピボットテーブルを別の既存シート（例: “Report”）にだけ配置したい場合は、宛先作成ステップを対象シートへの参照に置き換えます：

```csharp
Worksheet destinationSheet = workbook.Worksheets["Report"]; // existing sheet
sourceSheet.CopyRows(sourceArea.StartRow, destinationSheet, 0,
                     sourceArea.RowCount, CopyOptions.CopyAll);
```

このスニペットは、新しいワークシートを作成せずに **ピボットテーブルを別シートにコピー** する方法を示しています。

## ピボットテーブルを新しいブックにエクスポートする

ピボットテーブルを完全に別ファイルにしたい場合があります。コピー操作の後、コピーしたピボットテーブルがあるシート以外のすべてのワークシートを削除し、保存します：

```csharp
// Keep only the copied sheet
for (int i = workbook.Worksheets.Count - 1; i >= 0; i--)
{
    if (workbook.Worksheets[i].Name != "Copy")
        workbook.Worksheets.RemoveAt(i);
}

// Save as a new workbook containing only the pivot table
workbook.Save(@"YOUR_DIRECTORY\pivot_only.xlsx");
```

これで `pivot_only.xlsx` には、複製されたピボットテーブルを含む単一シートが残り、**ピボットテーブルを新しいブックにエクスポート** する要件が満たされます。

## 書式を失わずに Excel 行をコピーする方法

同じ `CopyRows` 呼び出しはピボットテーブルに限らず任意の範囲で機能します。条件付き書式、データ検証、結合セルを含む **Excel 行をコピー** したい場合は、同じメソッドを使用してください：

```csharp
// Example: copy rows 30‑40 from Sheet1 to Sheet2
sourceSheet.CopyRows(29, // zero‑based index for row 30
                     workbook.Worksheets["Sheet2"],
                     0,
                     11, // rows 30‑40 = 11 rows
                     CopyOptions.CopyAll);
```

`CopyOptions.CopyAll` がすべてを転送するため、宛先の行はソースの行とまったく同じ外観になります。

## よくある落とし穴と回避策

| Pitfall | Symptom | Fix |
|---------|---------|-----|
| ソース範囲がピボットテーブル全体を含んでいない | コピーされたピボットテーブルが切り取られたように見える | `CellArea` がピボットテーブルのすべての行/列をカバーしているか確認する。 |
| 宛先シートに既にデータが存在する | 上書きされた行によりデータが失われる | 新しいシートを使用するか、より上位の行インデックスからコピーを開始する。 |
| ピボットテーブルが外部データソースを使用している | コピー後に接続が失われる | コピー後に `pivotTable.RefreshData()` を呼び出してリンクを再確立する。 |
| 非表示行が除外される | コピーに一部の行が欠ける | `CopyRows` は自動的に非表示行もコピーするので、`CopyOptions.CopyValuesOnly` を使用していないことを確認する。 |

## 完全な実行可能サンプル

以下は新しいコンソールプロジェクトに貼り付けて実行できる、自己完結型のプログラムです。上記で説明したすべての手順を示しています。

```csharp
using System;
using Aspose.Cells;

namespace PivotTableCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains the pivot table
            string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2️⃣ Get source and destination worksheets
            Worksheet sourceSheet = workbook.Worksheets[0]; // first sheet
            Worksheet destinationSheet = workbook.Worksheets.Add("Copy");

            // 3️⃣ Define the cell area that holds the pivot table (A1:G20)
            CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");

            // 4️⃣ Copy rows with formatting and keep the pivot cache
            sourceSheet.CopyRows(
                sourceArea.StartRow,      // start row index (0‑based)
                destinationSheet,        // target sheet
                0,                        // start row in destination
                sourceArea.RowCount,      // number of rows to copy
                CopyOptions.CopyAll);    // copy everything

            // 5️⃣ Save the workbook with the copied pivot table
            string destPath = @"YOUR_DIRECTORY\pivot_copied.xlsx";
            workbook.Save(destPath);

            Console.WriteLine("Pivot table copied successfully to " + destPath);
        }
    }
}
```

**プログラムを実行**すると、元のピボットテーブルの複製が **Copy** という名前の新しいシートに作成された `pivot_copied.xlsx` が生成されます。

## 結論

これで C# で **ピボットテーブルをコピーする方法** が理解できました。

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、プロジェクトでの代替実装方法を検討するのに役立ちます。

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy Pivot Table in C# – Complete Step‑by‑Step Guide](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [How to copy range with pivot tables in C# – Complete Guide](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}