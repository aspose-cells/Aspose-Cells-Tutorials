---
category: general
date: 2026-08-17
description: C#でExcelをPowerPointとして保存 – XLSXファイルを変換し、テキストボックスを編集可能にし、PPTX出力を生成するステップバイステップガイド
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- how to convert xlsx
- make textbox editable
- how to edit textboxes
language: ja
lastmod: 2026-08-17
og_description: C#でExcelをPowerPointとして保存する完全コード例。XLSXの変換方法、テキストボックスを編集可能にする方法、そしてPPTXへのエクスポートを学びましょう。
og_image_alt: Screenshot showing Excel data saved as a PowerPoint slide
og_title: C#でExcelをPowerPointに保存する – 完全変換ガイド
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Save Excel as PowerPoint with C# – step‑by‑step guide to convert XLSX
    files, make textboxes editable, and generate PPTX output.
  headline: How to save Excel as PowerPoint using C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel-to-PowerPoint
title: C# と Aspose.Cells を使用して Excel を PowerPoint に保存する方法
url: /ja/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# と Aspose.Cells を使用して Excel を PowerPoint に保存する方法

.NET プロジェクトで **Excel を PowerPoint に保存** する必要がある場合、このガイドでは完全で実行可能なソリューションを示します。XLSX ワークブックの読み込み、シート上のすべてのテキストボックスを編集可能にする方法、そして結果を PPTX ファイルにエクスポートする方法を、C# の数行だけで実現できます。

Excel を PowerPoint に変換することは、レポート ダッシュボード、スライド デック、または自動プレゼンテーション生成のための一般的な要件です。このチュートリアルでは **テキストボックスをプログラムで編集する方法** もカバーしているので、保存前にスライド内容をカスタマイズできます。

## 前提条件

* .NET 6.0（またはそれ以降）SDK がインストールされていること  
* Visual Studio 2022 や VS Code などの開発環境  
* Aspose.Cells for .NET のライセンス（または無料評価キー） – [Aspose website](https://products.aspose.com/cells/net/) からダウンロード  
* 変換したい `input.xlsx` ファイル  

> **プロのコツ:** 無料評価版を使用すると、出力される PPTX に透かしが入ります。ライセンス版を使用すれば透かしは除去されます。

## 手順 1: Aspose.Cells NuGet パッケージをインストールする

プロジェクトフォルダーでターミナルを開き、次のコマンドを実行します:

```bash
dotnet add package Aspose.Cells
```

これにより、変換に必要な `Workbook`、`Worksheet`、`Shape` クラスを提供する `Aspose.Cells` アセンブリが追加されます。

## 手順 2: コンソール アプリケーションの雛形を作成する

新しいコンソール プロジェクトを作成します（まだ持っていない場合）:

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
```

生成された `Program.cs` を次の手順で示すコードに置き換えます。

## 手順 3: ワークブックを読み込み、最初のワークシートを選択する

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Load the workbook from a file – adjust the path to your environment
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**なぜ重要か:**  
`Workbook` は Excel ファイルをメモリに読み込み、`Worksheet` はシートのセル、チャート、シェイプにアクセスできるようにします。最初のワークシートは、提示したいデフォルトのレポートであることが多いです。

## 手順 4: シート上のすべてのテキストボックスを編集可能にする

```csharp
        // Iterate through all shapes on the worksheet
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            // Check if the shape is a textbox (ShapeType.TextBox)
            if (shapeItem.Type == ShapeType.TextBox)
            {
                // The IsEditable property was added in Aspose.Cells 25.11
                shapeItem.TextBox.IsEditable = true;
            }
        }
```

**なぜ必要か:**  
デフォルトでは、Excel からインポートされたテキストボックスは PowerPoint で表示されるときに読み取り専用になります。`IsEditable = true` を設定すると、スライド上で直接テキストを変更できるようになります（後の PowerPoint ユーザーも同様です）。

## 手順 5: ワークブックを PowerPoint プレゼンテーションとして保存する

```csharp
        // Define the output path for the PPTX file
        string outputPath = @"YOUR_DIRECTORY\output.pptx";

        // Save the workbook as a PowerPoint presentation
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

**内部で何が起きているか:**  
`Workbook.Save` は `SaveFormat.Pptx` 列挙値を検出し、Excel シートのレイアウト（行、列、チャート、そして編集可能にしたテキストボックス）を PowerPoint のスライド オブジェクトに変換します。

## 完全なソースコード（実行可能）

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from a file
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Step 2: Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Make every textbox on the sheet editable (property added in version 25.11)
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            if (shapeItem.Type == ShapeType.TextBox)
            {
                shapeItem.TextBox.IsEditable = true;
            }
        }

        // Step 4: Save the workbook as a PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\output.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

### 期待される出力

プログラムを実行すると（`dotnet run`）、次のような出力が表示されます:

```
Conversion complete. PPTX saved to: YOUR_DIRECTORY\output.pptx
```

Microsoft PowerPoint で `output.pptx` を開くと、元の Excel シートを鏡像したスライドが表示されます。すべてのテキストボックスはダブルクリックで直接編集可能です。

## よくある質問とエッジケース

| 質問 | 回答 |
|----------|--------|
| **最初のシートではなく、特定のシートを変換できますか？** | はい。`workbook.Worksheets[0]` を `workbook.Worksheets["SheetName"]` または必要なインデックスに置き換えてください。 |
| **ワークブックに複数のシートがある場合はどうすればよいですか？** | `workbook.Save` をシートごとに一度ずつ呼び出し、各シートに対して別々の PPTX ファイル名を指定するか、Aspose.Slides の `Presentation` オブジェクトを使用して単一のプレゼンテーションに結合します。 |
| **チャートは保持されますか？** | Aspose.Cells は Excel のチャートを PowerPoint のチャートオブジェクトに自動的に変換します。追加のコードは不要です。 |
| **スライドサイズを変更するには？** | `workbook.Save` 後に、生成された PPTX を Aspose.Slides で読み込み、`Presentation.SlideSize` を調整できます。 |
| **保存前にテキストボックスのテキストを編集したい場合は？** | ループ内で `shapeItem.TextBox.Text` にアクセスし、変更した後に `IsEditable = true` を設定します。例: `shapeItem.TextBox.Text = "New title";` |

## トラブルシューティングのヒント

* **“ShapeType.TextBox” が見つからない** – Aspose.Cells バージョン 25.11 以降を使用していることを確認してください。古いバージョンには `IsEditable` プロパティがありません。  
* **ファイルが見つからないエラー** – `YOUR_DIRECTORY` が絶対パスであるか、相対パスが正しい場所を指しているか確認してください。  
* **ライセンスが適用されていない** – ワークブックを読み込む前に `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` を呼び出して、評価版の透かしを除去します。

## 結論

これで、C# で XLSX ワークブックを読み込み、すべてのテキストボックスを編集可能にし、PPTX にエクスポートすることで **Excel を PowerPoint に保存** する方法が分かりました。この方法はチャート、画像、セル書式設定を自動的に処理し、すぐにプレゼンテーションできるスライド デックを提供します。

次に、**Aspose.Slides を使用した Excel から PowerPoint への変換**、**変換後にテキストボックスをプログラムで編集する方法**、または **複数のワークブックをバッチ処理する方法** などの関連トピックを探求してください。これらは本ガイドのコア手順を基にしており、レポート ワークフローをさらに自動化できます。

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックをカバーしています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得したり、プロジェクトで代替実装アプローチを検討したりするのに役立ちます。

- [Aspose.Cells for .NET を使用して Excel を PowerPoint に変換する完全ガイド](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [C# でピボットテーブルをコピーする方法 – Excel を PPTX に変換、範囲コピー、テキストボックス作成](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Aspose.Cells .NET を使用して Excel ファイルを複数形式で保存する方法（2023 ガイド）](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}