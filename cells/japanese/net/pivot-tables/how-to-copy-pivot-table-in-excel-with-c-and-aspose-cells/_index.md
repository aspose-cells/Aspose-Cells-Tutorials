---
category: general
date: 2026-10-04
description: C# を使用して、あるブックから別のブックへピボットテーブルをコピーする方法を学びます。このガイドでは、行のコピー、ピボットテーブルの複製、Excel
  の範囲を効率的にコピーする方法もカバーしています。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- how to copy rows
- duplicate pivot table
language: ja
lastmod: 2026-10-04
og_description: C# を使用して Excel のピボットテーブルをコピーする。Aspose.Cells を使ったピボットテーブルの複製、行のコピー、Excel
  範囲のコピーの完全チュートリアルをご覧ください。
og_image_alt: Screenshot showing a duplicated pivot table in an Excel worksheet after
  using C# code
og_title: C#でExcelのピボットテーブルをコピーする – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to copy pivot table from one workbook to another using C#.
    This guide also covers how to copy rows, duplicate pivot table, and copy Excel
    range efficiently.
  headline: How to copy pivot table in Excel with C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: C# と Aspose.Cells を使用して Excel のピボットテーブルをコピーする方法
url: /ja/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# と Aspose.Cells を使用して Excel でピボットテーブルをコピーする方法

ワークブック間で **ピボットテーブルをコピー** する必要がある場合、このチュートリアルでは完全な実行可能なソリューションを示します。ソースファイルの読み込み、ピボットが含まれる範囲の定義、行（ピボット定義を含む）のコピー、結果の保存方法を正確に確認できます。レポートパイプラインの自動化やマイグレーションツールの構築など、以下の手順で数行の C# コードだけでピボットテーブルを複製できます。

ピボットテーブルのコピーはセルの値だけをコピーする以上の作業で、基になるキャッシュとフィールド設定も一緒に移動させる必要があります。この例では **Aspose.Cells** ライブラリを使用しています。ピボットのメタデータを自動的に処理してくれるため、キャッシュを手動で再構築する必要はありません。このガイドの最後までに、**ピボットのコピー方法**、**Excel 範囲のコピー**、そして **行のコピー方法** を安全に実行できるようになります。

## 前提条件

- .NET 6.0 以降がインストールされていること（コードは .NET Framework 4.7+ でも動作します）。
- 有効な Aspose.Cells for .NET ライセンス、または一時的な評価ライセンス。
- `Source.xlsx`（複製したいピボットテーブルが含まれる）と、`CopyWithPivot.xlsx` を書き込む空のフォルダーの、2 つの Excel ファイル。
- Visual Studio 2022（または C# をサポートする任意の IDE）。

## 手順 1: プロジェクトを設定し Aspose.Cells を追加する

新しいコンソールプロジェクトを作成し、Aspose.Cells の NuGet パッケージを追加します。

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
dotnet add package Aspose.Cells
```

このパッケージは、以下のコードで使用する `Workbook`、`Worksheet`、`CellArea` クラスを提供します。

## 手順 2: ピボットテーブルを含むソースブックを読み込む

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the source workbook that holds the pivot you want to duplicate
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");
```

> **なぜ重要か:** ブックを読み込むことで、すべてのワークシート（非表示のピボットキャッシュを含む）のメモリ上の表現が作成されます。ファイルを読み込まなければ、ピボットの範囲を参照できません。

## 手順 3: ピボットテーブルをカバーするセル領域を定義する

Aspose.Cells に対し、どの行と列がピボットに属するかを指示する必要があります。`CellArea` 構造体を使用すると、矩形のブロックを指定できます。

```csharp
        // Define the rectangle that encloses the pivot table (adjust as needed)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,      // first row (zero‑based)
            StartColumn = 0,   // first column
            EndRow = 30,       // last row of the pivot
            EndColumn = 10     // last column of the pivot
        };
```

> **ヒント:** 正確なサイズが分からない場合は、Excel でソースファイルを開き、ピボットを選択して、名前ボックスに表示される範囲（例: `A1:K31`）を確認してください。Excel の座標をコード用の 0 基準インデックスに変換します。

## 手順 4: 新しい宛先ブックを作成し、最初のワークシートを取得する

```csharp
        // Create an empty workbook that will receive the copied pivot
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

> **この手順が必要な理由:** 行をコピーする前に、宛先ブックが存在している必要があります。Aspose.Cells はデフォルトのワークシートを自動的に作成するので、これをターゲットとして使用します。

## 手順 5: ソースから宛先へ行（ピボットテーブルを含む）をコピーする

`CopyRows` メソッドはセルの値と基になるピボットキャッシュの両方をコピーします。

```csharp
        // Copy rows from source to destination, preserving the pivot definition
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,      // source cells
            sourceRange.StartRow,                 // first row to copy
            sourceRange.EndRow - sourceRange.StartRow + 1, // number of rows
            destWorksheet.Cells,                  // target cells
            sourceRange.StartRow);                // target start row
```

> **動作概要:**  
> - `CopyRows` はソースワークシート、開始行、コピーする行数を受け取ります。  
> - また、宛先ワークシートとコピー開始行も指定します。  
> - ソース範囲にピボットテーブルが含まれているため、メソッドはピボットのキャッシュ、フィールドリスト、レイアウトをそのまま転送します。これが機能を失わずに **ピボットのコピー方法** の核心です。

### エッジケース: 複数シートにまたがるピボットのコピー

ピボットの元データがピボット自体とは別のシートにある場合でも、Aspose.Cells はキャッシュをシートではなくブック全体に保存するため、コピー時にキャッシュは引き継がれます。ただし、宛先ブックに同じ元データ範囲が存在することを確認しなければなりません。そうでないとピボットは `#REF!` エラーを表示します。そのような場合は、まず元データ範囲をコピーし、次にピボット行をコピーしてください。

## 手順 6: コピーされたピボットテーブルを含むブックを保存する

```csharp
        // Persist the destination workbook to disk
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

プログラムを実行すると、元のピボットテーブルと全く同じコピー（スライサー、フィルター、計算フィールドを含む）を持つ `CopyWithPivot.xlsx` が生成されます。

### 期待される出力

`CopyWithPivot.xlsx` を開くと:

- ピボットテーブルは `Source.xlsx` と同じ位置（例: A1:K31）に表示されます。
- すべての行・列ラベル、合計、書式設定が保持されています。
- ピボットを更新すると、元データと同じデータが表示され、キャッシュが正しくコピーされたことが確認できます。

## ピボットなしで行をコピーする方法（Excel 範囲のコピー）

ピボットデータが不要で **Excel 範囲をコピー** したい場合は、同じ `CopyRows` メソッドを使用し、ピボットを含まない範囲を指定すればできます。例:

```csharp
// Copy a simple data table from rows 5‑15, columns A‑D
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    4,            // start at row 5 (zero‑based)
    11,           // copy 11 rows (5‑15 inclusive)
    destWorksheet.Cells,
    0);           // paste at the top of the destination sheet
```

これは、汎用データに対して **行のコピー方法** を示すもので、同一 API の汎用性を強調しています。

## 同一ブック内でピボットテーブルを複製する（代替アプローチ）

新しいファイルを作成せず、同じブック内で **ピボットテーブルを複製** したい場合があります。その場合は、行を別の場所にコピーすることで実現できます。

```csharp
// Duplicate pivot table to start at row 40 in the same worksheet
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    sourceRange.StartRow,
    sourceRange.EndRow - sourceRange.StartRow + 1,
    destWorksheet.Cells,
    40); // destination start row (zero‑based)
```

保存後、ブックには同一のピボットが2つ含まれます。これは並列比較やバックアップコピーの作成に便利です。

## よくある落とし穴と回避方法

| 落とし穴 | 発生理由 | 対策 |
|---------|----------------|-----|
| コピー後にピボットが `#REF!` を表示 | 宛先ブックに元データ範囲が存在しない | まず元データ範囲をコピーするか、ピボットをコピーする前に元データシートで `CopyRows` を使用する |
| 書式が失われる | 値だけがコピーされた（例: `CopyRows` ではなく `Copy` を使用） | 常に `CopyRows` を使用し、スタイル、書式、ピボットメタデータを保持する |
| 予期しない行オフセット | 宛先の開始行がソースの開始行と一致していない | `destWorksheet.Cells` の開始行が意図した位置と合っているか確認する |
| 大規模ブックでメモリ圧迫が発生 | `CopyRows` がシート全体をメモリに読み込む | コピーをチャンク単位で処理するか、100,000 行超の場合はストリーミング API を使用する |

## 完全な実行可能サンプル

以下は `Program.cs` に貼り付けてすぐに実行できる完全なプログラムです（`YOUR_DIRECTORY` を実際のパスに置き換えてください）。

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook containing the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");

        // 2️⃣ Define the area that encloses the pivot (adjust to your sheet)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 30,
            EndColumn = 10
        };

        // 3️⃣ Create the destination workbook (empty) and get its first sheet
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // 4️⃣ Copy rows—including the pivot cache—into the destination
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,
            sourceRange.StartRow,
            sourceRange.EndRow - sourceRange.StartRow + 1,
            destWorksheet.Cells,
            sourceRange.StartRow);

        // 5️⃣ Save the result
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

`dotnet run` でプログラムを実行します。実行後、`CopyWithPivot.xlsx` を開き、ピボットテーブルがソースファイルと全く同じであることを確認してください。

## 結論

これで C# と Aspose.Cells を使用して、ある Excel ブックから別のブックへ **ピボットテーブルをコピー** する方法が分かりました。本ガイドでは、ソースファイルの読み込み、ピボットのセル領域の定義、行のコピー、宛先ブックの保存という一連の手順を網羅しました。また、**行のコピー方法**、**Excel 範囲のコピー**、同一ファイル内での **ピボットテーブルの複製** も学び、一般的な落とし穴とベストプラクティスのヒントも紹介しました。

次のステップに進みませんか？コピーしたピボットをプログラムでリフレッシュするコードを追加したり、Aspose.Cells でピボットを PDF にエクスポートする方法を試したりしてください。さまざまなソース範囲で実験すれば、.NET における Excel 自動化をすぐにマスターできるでしょう。

---

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を応用した密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説付きの完全なコード例が含まれており、追加の API 機能を習得し、プロジェクトで代替実装方法を検討するのに役立ちます。

- [C# でピボットテーブルをコピー – 完全ステップバイステップガイド](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [新しい Excel ブックの作成 – ピボットテーブルのコピーと複製](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Excel 行のコピー – 行を複製しながらピボットテーブルを保持](/cells/english/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}