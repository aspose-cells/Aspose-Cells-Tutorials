---
category: general
date: 2026-10-01
description: C# で Aspose.Cells を使用して Excel から PowerPoint を作成します。Excel を PowerPoint
  にエクスポートし、XLSX を PPTX に迅速に変換する完全なコード例を提供します。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create PowerPoint from Excel
- export Excel to PowerPoint
- convert Excel to PPTX
- convert XLSX to PPTX
- generate PowerPoint from Excel
language: ja
lastmod: 2026-10-01
og_description: C# で Aspose.Cells を使用して Excel から PowerPoint を作成します。数行のコードで Excel を
  PowerPoint にエクスポートし、XLSX を PPTX に変換する方法を学びましょう。
og_image_alt: Screenshot of a PowerPoint slide generated from Excel using Aspose.Cells
og_title: Aspose.CellsでExcelからPowerPointを作成する – クイックガイド
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create PowerPoint from Excel using Aspose.Cells in C#. Export Excel
    to PowerPoint and convert XLSX to PPTX quickly with a complete code example.
  headline: Create PowerPoint from Excel with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Office automation
title: Aspose.Cells を使用して Excel から PowerPoint を作成する – ステップバイステップガイド
url: /ja/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel から PowerPoint を作成する – Aspose.Cells を使ったステップバイステップガイド

Excel から **PowerPoint を作成** したい場合は、このチュートリアルで Aspose.Cells for .NET を使用した方法をご紹介します。**Excel を PowerPoint にエクスポート** し、XLSX ワークブックを PPTX プレゼンテーションに変換し、C# プロジェクト内でスライドをカスタマイズする方法を学びます。

本ガイドでは、.NET 6 以降でコードを実行するために必要なすべて（プロジェクトのセットアップ、必要な NuGet パッケージ、完全に実行可能なサンプル）を網羅しています。最後には、元の Excel のチャートがそのままスライドに表示された PowerPoint ファイルが手に入ります。

## 必要なもの

| 前提条件 | 理由 |
|---|---|
| .NET 6 SDK 以上 | C# コンソール アプリのランタイムを提供 |
| Visual Studio 2022（または任意の IDE） | プロジェクト作成とデバッグが容易 |
| Aspose.Cells for .NET NuGet パッケージ | `Workbook` クラスとエクスポート API を提供 |
| 少なくとも 1 つのチャートを含む Excel ファイル（`.xlsx`） | PowerPoint スライドの元データ |

> **プロのコツ:** Aspose.Cells は Windows、Linux、macOS で動作するため、Docker コンテナや CI パイプラインでも同じコードを実行できます。

## 手順 1: 新しいコンソール プロジェクトを作成し Aspose.Cells を追加

ターミナル（または Visual Studio のパッケージ マネージャ コンソール）で次を実行します。

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
dotnet add package Aspose.Cells
```

`dotnet add package` コマンドは、後で使用する `ExportPptx` メソッドを含む **Aspose.Cells** の最新安定版をダウンロードします。

## 手順 2: ソースとなる Excel ワークブックを追加

変換したい Excel ファイルをプロジェクト フォルダーに配置します。このチュートリアルでは、最初のワークシートに 1 つのチャートが含まれる `ChartOle.xlsx` を使用します。

```
/ExcelToPptxDemo
│   Program.cs
│   ChartOle.xlsx   ← your source workbook
```

## 手順 3: **Excel から PowerPoint を作成** するコードを書く

`Program.cs` を開き、内容を以下のコードに置き換えます。サンプルは **コア エクスポート** 操作を示すと同時に、ファイルが見つからない場合やサポート外のチャート種別などの一般的なエッジケースの処理方法も示しています。

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelToPptxDemo
{
    class Program
    {
        static void Main()
        {
            // Define input and output paths
            string inputPath = Path.Combine(AppContext.BaseDirectory, "ChartOle.xlsx");
            string outputPath = Path.Combine(AppContext.BaseDirectory, "Exported.pptx");

            // Verify that the source workbook exists
            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: The file '{inputPath}' was not found.");
                return;
            }

            try
            {
                // Load the Excel workbook that contains the chart
                var workbook = new Workbook(inputPath);

                // Export the first worksheet as a PowerPoint presentation
                // This call performs the **convert Excel to PPTX** operation.
                workbook.Worksheets[0].ExportPptx(outputPath);

                Console.WriteLine($"Success: PowerPoint file created at '{outputPath}'.");
            }
            catch (Exception ex)
            {
                // Catch any errors thrown by Aspose.Cells (e.g., unsupported chart)
                Console.WriteLine($"Export failed: {ex.Message}");
            }
        }
    }
}
```

### これが機能する理由

* `Workbook` は埋め込みチャート、テーブル、書式設定を含む Excel ファイル全体を読み取ります。  
* `ExportPptx` はアクティブなワークシートを PPTX スライド デッキに変換します。このメソッドは Excel のチャートを自動的に PowerPoint のシェイプに変換し、視覚的忠実度を保持します。  
* `try/catch` ブロックで処理をラップし、破損したファイルによる **convert XLSX to PPTX** 失敗などのエラーを表面化します。

## 手順 4: プログラムを実行し出力を確認

アプリケーションを実行します。

```bash
dotnet run
```

コンソールに次のメッセージが表示されるはずです。

```
Success: PowerPoint file created at '.../Exported.pptx'.
```

`Exported.pptx` を Microsoft PowerPoint または互換ビューアで開きます。最初のスライドに `ChartOle.xlsx` と同じ外観のチャートが表示されます。これで **Excel から PowerPoint を生成** できたことが確認できます。

## 手順 5: 応用 – 複数シートのエクスポートやカスタム スライド レイアウト

基本例は最初のシートだけをエクスポートしますが、実務では次のような要件が出てくることがあります。

* **複数シート** を個別のスライドにエクスポート  
* **スライドサイズ** を制御したりタイトル プレースホルダーを追加  
* **非表示シート** も変換に含める  

以下は、すべてのワークシートを走査し、各シートを別々のスライドとして追加する簡潔なスニペットです。

```csharp
// Export each worksheet as a separate slide
var pptxPath = Path.Combine(AppContext.BaseDirectory, "FullExport.pptx");
var presentation = new Presentation(); // Aspose.Slides.Presentation, if you have the Slides library

foreach (Worksheet ws in workbook.Worksheets)
{
    // Convert worksheet to an image first (optional for custom layout)
    var imgStream = new MemoryStream();
    ws.PageSetup.PrintArea = ws.Cells.MaxDisplayRange; // ensure full content
    ws.Pictures[0].ToImage(imgStream, ImageFormat.Png);

    // Add a new slide and insert the image
    var slide = presentation.Slides.AddEmptySlide(presentation.SlideSize.Size);
    slide.Shapes.AddPictureFrame(ShapeType.Rectangle, 0, 0, presentation.SlideSize.Size.Width, presentation.SlideSize.Size.Height, imgStream);
}

// Save the final presentation
presentation.Save(pptxPath, SaveFormat.Pptx);
```

> **注意:** 上級スニペットは **Aspose.Slides for .NET** ライブラリが必要です。シンプルな 1 シート変換だけで良ければ、前述の `ExportPptx` 呼び出しで十分です。

## よくある落とし穴と回避策

| 問題 | 原因 | 対策 |
|---|---|---|
| エクスポート後に空白スライドができる | ワークシートに可視オブジェクトがない | `ExportPptx` を呼び出す前に、少なくとも 1 つのチャート、テーブル、シェイプが存在することを確認 |
| PowerPoint のフォントが欠落している | PPTX を開くマシンにフォントがインストールされていない | 必要なフォントを Excel ワークブックに埋め込むか、対象システムにインストール |
| 予期しないスケーリング | 大きなチャートがスライドサイズを超えている | エクスポート前にワークシートの `PageSetup.Zoom` プロパティでサイズ調整 |
| `convert XLSX to PPTX` が `NotSupportedException` を投げる | Aspose.Cells がサポートしないチャート種別（例: 3‑D マップ） | サポート対象のチャートに置き換えるか、シートを画像としてエクスポートしてから貼り付ける |

これらのエッジケースに対処すれば、実運用環境でも信頼性の高い **Excel から PowerPoint へのエクスポート** ワークフローが実現できます。

## 結論

Aspose.Cells for .NET を使って **Excel から PowerPoint を作成** する方法が分かりました。本チュートリアルで取り上げた内容は以下の通りです。

* プロジェクトのセットアップと NuGet のインストール  
* Excel ワークブックの読み込みと `ExportPptx` の呼び出し  
* コード実行と生成された PPTX の確認  
* 複数シートやカスタム レイアウトへの拡張方法  
* 一般的な変換問題を回避する実践的なヒント  

この知識を活用すれば、レポート自動生成やプレゼンテーション パイプラインの構築、任意の C# アプリケーションへの Excel‑to‑PowerPoint 変換統合が可能です。さまざまなチャート種別を試したり、スライドタイトルを追加したり、Aspose.Slides と組み合わせてフル機能のプレゼンテーション作成に挑戦してみてください。

--- 

*もっと学びたいですか？ **Excel を PDF に変換**、**Excel データを Word に埋め込む**、または **Aspose.Slides で PPTX をプログラム的に編集** などの関連トピックもチェックしてください。*

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法を基に、さらに関連するトピックを深く掘り下げたものです。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれています。

- [Excel を PowerPoint に変換 (Aspose Cells .NET)](/cells/german/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Excel を PowerPoint に変換 (Aspose Cells .NET)](/cells/french/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Excel を PowerPoint に変換 (Aspose Cells .NET)]( /cells/spanish/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}