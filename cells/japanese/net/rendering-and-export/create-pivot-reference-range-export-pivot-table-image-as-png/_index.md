---
category: general
date: 2026-02-09
description: C#でピボット参照範囲を作成し、ピボットテーブルの画像をエクスポートします。Aspose.Cells を使用して Excel の範囲を PNG
  として保存する方法を学びましょう — 簡単で完全なガイド。
draft: false
keywords:
- create pivot reference range
- export pivot table image
- save excel range as png
- Aspose.Cells C#
- Excel automation C#
language: ja
og_description: C#でピボット参照範囲を作成し、ピボットテーブルの画像をPNGにエクスポートします。Excel の範囲を PNG として保存する完全なステップバイステップ
  ガイド。
og_title: ピボット参照範囲を作成 – ピボットテーブル画像をPNGでエクスポート
tags:
- Aspose.Cells
- C#
- Excel
title: ピボット参照範囲の作成 – ピボットテーブル画像をPNGでエクスポート
url: /ja/net/rendering-and-export/create-pivot-reference-range-export-pivot-table-image-as-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ピボット参照範囲の作成 – ピボットテーブル画像を PNG としてエクスポート

C# で Excel ワークブックの **ピボット参照範囲を作成** したいですか？数行のコードだけで **ピボットテーブル画像をエクスポート** し、**Excel の範囲を PNG として保存** できます。実務では、ライブのピボットを静的画像に変換することで、レポートやメール、ダッシュボードに分析結果を埋め込む際に、ワークブック全体を持ち込む必要がなくなります。

このチュートリアルでは、必要なライブラリ、正確なコード、各呼び出しが重要な理由、そして遭遇しやすい落とし穴をすべて解説します。最後まで読めば、任意のピボットテーブルの PNG ファイルを自信を持って生成でき、複数シートやカスタム画像形式へのパターン適用方法も理解できます。

## 前提条件

始める前に以下を確認してください：

- **Aspose.Cells for .NET**（無料トライアルでテスト可能）。  
- **.NET 6.0** 以上 – 使用する API は .NET Standard 2.0+ と完全互換なので、古いフレームワークでもコンパイルできます。  
- 基本的な C# プロジェクト（コンソールアプリ、WinForms、または ASP.NET など、NuGet パッケージを参照できるもの）。  

まだ Aspose.Cells をインストールしていない場合は、以下を実行してください：

```bash
dotnet add package Aspose.Cells
```

これだけです – COM インターロップやサーバー上に Excel をインストールする必要はありません。

## 手順 1: ワークブックを開き、最初のワークシートにアクセス

最初に行うのは、ワークブックファイルをロードし、ピボットテーブルが配置されているワークシートを取得することです。デモファイルの多くはピボットが **最初のシート** (`Worksheets[0]`) にあるためここではそのシートを選択していますが、インデックスの代わりにシート名を指定しても構いません。

```csharp
using Aspose.Cells;
using System;

// Load an existing Excel file (replace with your own path)
Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Access the first worksheet – this is where our pivot lives
Worksheet worksheet = wb.Worksheets[0];
```

*なぜ重要か:* `Worksheet` はすべての範囲ベース操作のエントリーポイントです。間違ったシートを指すと、続く `PivotTables[0]` 呼び出しで `IndexOutOfRangeException` がスローされます。

## 手順 2: ピボット参照範囲を作成

次にピボットテーブル自体に **参照範囲** を取得させます。この範囲はピボットを構成するセル（ヘッダー、データ行、合計行）すべてを表します。`CreateReferenceRange()` メソッドが内部でマージセルや非表示行を処理してくれます。

```csharp
// Grab the first pivot table on the worksheet
PivotTable pivot = worksheet.PivotTables[0];

// Build a reference range that covers the whole pivot
Range pivotReferenceRange = pivot.CreateReferenceRange();
```

> **プロのコツ:** ワークブックに複数のピボットがある場合は、`worksheet.PivotTables` を列挙し、`Name` プロパティで目的のピボットを選択してください。

## 手順 3: 参照範囲を画像としてレンダリング

Aspose.Cells は任意の `Range` を画像に変換できます。返されるオブジェクトはラスタ形式（PNG、JPEG）とベクタ形式（SVG）の両方に対応しています。ここではデフォルトのラスタ画像、すなわち `System.Drawing.Image` 互換オブジェクトを取得します。

```csharp
// Convert the pivot reference range into an image object
ImageOrVector pivotImage = pivotReferenceRange.ToImage();
```

*内部で何が起きているか？* API は範囲のビジュアルレイアウトをスナップショットし、セルのスタイル、フォント、条件付き書式を尊重します。実質的にはスクリーンショットをプログラム的に取得したものですが、UI は不要です。

## 手順 4: 生成した画像をファイルに保存

最後に画像を永続化します。`Save` メソッドは拡張子が “.png” の場合自動的に PNG 形式を選択します。DPI 制御や別形式が必要な場合は `SaveOptions` オブジェクトを渡すこともできます。

```csharp
// Save the image as PNG – the extension drives the format
pivotImage.Save("YOUR_DIRECTORY/pivot.png");
```

この行が実行された後、`pivot.png` を開くとピボットテーブルのピクセルパーフェクトなスナップショットが表示され、任意の場所に埋め込めます。

## 完全動作サンプル

すべてをまとめた、コピー＆ペーストで実行できるコンソールプログラムは以下の通りです：

```csharp
using Aspose.Cells;
using System;

namespace PivotExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

            // 2️⃣ Access first worksheet
            Worksheet worksheet = wb.Worksheets[0];

            // 3️⃣ Get first pivot table
            if (worksheet.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found on the first sheet.");
                return;
            }
            PivotTable pivot = worksheet.PivotTables[0];

            // 4️⃣ Create a reference range that covers the whole pivot
            Range pivotReferenceRange = pivot.CreateReferenceRange();

            // 5️⃣ Render the range to an image
            ImageOrVector pivotImage = pivotReferenceRange.ToImage();

            // 6️⃣ Save as PNG
            string outputPath = "YOUR_DIRECTORY/pivot.png";
            pivotImage.Save(outputPath);

            Console.WriteLine($"Pivot table image saved to {outputPath}");
        }
    }
}
```

**期待される出力:** `YOUR_DIRECTORY` 配下に `pivot.png` という名前のファイルが作成されます。任意の画像ビューアで開くと、元のピボットと同一のレイアウト（列ヘッダー、データ行、総計）が確認できます。

## ピボットテーブル画像のエクスポート – サイズと DPI のカスタマイズ

デフォルト画像がプレゼンテーションスライドに対して小さすぎることがあります。`ImageOrVectorSaveOptions` オブジェクトを渡すことで解像度を調整できます：

```csharp
using Aspose.Cells.Drawing;

// Define PNG options – 300 DPI for high‑quality print
ImageOrVectorSaveOptions options = new ImageOrVectorSaveOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300 // DPI
};

pivotImage.Save("YOUR_DIRECTORY/pivot_highres.png", options);
```

*なぜ DPI を調整するのか？* DPI を上げると、特に PNG を PowerPoint や PDF で拡大表示する際にエッジがより鮮明になります。

## Excel の範囲を PNG として保存 – 複数シートの処理

複数シートからピボットをエクスポートしたい場合は、`Workbook.Worksheets` をループして同じ手順を繰り返します。簡潔なスニペットは次の通りです：

```csharp
foreach (Worksheet ws in wb.Worksheets)
{
    foreach (PivotTable pt in ws.PivotTables)
    {
        Range refRange = pt.CreateReferenceRange();
        ImageOrVector img = refRange.ToImage();
        string fileName = $"pivot_{ws.Name}_{pt.Name}.png";
        img.Save($"YOUR_DIRECTORY/{fileName}");
        Console.WriteLine($"Saved {fileName}");
    }
}
```

このパターンはワークブック内のすべてのピボットに対して **ピボットテーブル画像をエクスポート** し、各ファイルはシート名とピボット名で命名されるため、バッチ処理に最適です。

## よくある落とし穴と回避策

| 問題 | 発生原因 | 対策 |
|------|----------|------|
| `IndexOutOfRangeException` が `PivotTables[0]` で発生 | ワークシートにピボットテーブルが存在しない | アクセス前に `worksheet.PivotTables.Count` を確認 |
| 画像が空白になる | ピボットがすべての行を非表示にフィルタリングしている | ピボットに表示データがあることを確認、または `pivot.RefreshData();` を呼び出す |
| PNG の解像度が低い | デフォルト DPI が 96 | 上記のように `ImageOrVectorSaveOptions.Resolution` を使用 |
| ファイルパスエラー | `YOUR_DIRECTORY` に無効な文字が含まれる | `Path.Combine` と `Path.GetInvalidPathChars()` でサニタイズ |

## 検証 – クイックテスト

完全サンプルを実行した後は以下を確認してください：

1. Windows Photo Viewer で `pivot.png` を開く。  
2. 列ヘッダー、データ行、合計行が Excel の表示と一致しているか確認。  
3. 行が欠落している場合は、`CreateReferenceRange()` の前にピボットの **RefreshData** メソッドが呼び出されているか再確認。

## ボーナス: PNG を Word 文書に埋め込む

画像が PNG 形式なので、Aspose.Words にそのまま渡すことができます：

```csharp
using Aspose.Words;
Document doc = new Document();
DocumentBuilder builder = new DocumentBuilder(doc);
builder.InsertImage("YOUR_DIRECTORY/pivot.png");
doc.Save("YOUR_DIRECTORY/report.docx");
```

これで、ピボットのスナップショットを含む Word レポートが自動的に作成され、手動でコピー＆ペーストする手間が省けます。

## 結論

Aspose.Cells を使って C# で **ピボット参照範囲を作成**、**ピボットテーブル画像をエクスポート**、そして **Excel の範囲を PNG として保存** する方法を学びました。重要なポイントは次の通りです：

- `PivotTable.CreateReferenceRange()` でピボットの可視領域を切り出す。  
- `Range.ToImage()` でその範囲を画像に変換する。  
- PNG として保存し、必要に応じて DPI を調整して印刷品質を向上させる。  

ここからはバッチエクスポート、別画像形式（SVG、JPEG）への変換、あるいは PNG を PDF や Word に埋め込むといった応用が可能です。ピボットを静的グラフィックとしてキャプチャすれば、可能性は無限に広がります。

質問や難しいシナリオがあれば下のコメント欄にどうぞ。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}