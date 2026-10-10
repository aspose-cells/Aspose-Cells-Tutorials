---
category: general
date: 2026-10-10
description: Aspose.Cells を使用した C# で Excel を PowerPoint に変換し、印刷領域を設定する方法 – Excel のエクスポート、印刷領域の設定、PPTX
  ファイルの生成を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- set print area excel
- how to export excel
- how to set print area
- convert excel to pptx
language: ja
lastmod: 2026-10-10
og_description: Aspose.Cells を使用して Excel を PowerPoint に変換します。このチュートリアルでは、印刷範囲の設定、Excel
  のエクスポート、C# での PPTX ファイルの作成方法を示します。
og_image_alt: Screenshot of code that converts Excel to PowerPoint while setting the
  print area
og_title: Excel を PowerPoint に変換 – C# 開発者向け完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert Excel to PowerPoint and set print area in C# with Aspose.Cells
    – learn how to export Excel, set print area, and generate a PPTX file.
  headline: Convert Excel to PowerPoint and set print area
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Excel を PowerPoint に変換し、印刷範囲を設定する
url: /ja/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel を PowerPoint に変換し、印刷範囲を設定する

**convert Excel to PowerPoint** が必要な場合、このガイドでは C# での具体的な手順を示します。最初に印刷範囲を定義することで、各スライドに表示されるセルを制御でき、最終的な PPTX ファイルはレイアウトの期待通りになります。このソリューションは “how to export Excel” と “how to set print area” にも同じコードベースで答えます。

このチュートリアルでは以下を行います：

* 既存のブックブックを読み込む。
* ワークシートの印刷範囲を設定する（**set print area excel** 手順）。
* PowerPoint 出力の変換オプションを構成する。
* 単一のメソッド呼び出しで **convert excel to pptx** ファイルを生成する。

必要なコードはすべて含まれているので、すぐにコピーして貼り付け、実行できます。

## 前提条件

開始する前に、以下が揃っていることを確認してください：

| Requirement | Why it matters |
|-------------|----------------|
| **.NET 6.0 or later** | このサンプルは .NET 6 以降を対象としていますが、C# 10 をサポートする任意の .NET バージョンでも動作します。 |
| **Aspose.Cells for .NET** | このライブラリは `Workbook`、`ImageOrPrintOptions`、および `ConvertToPdf`（PPTX 用に使用）メソッドを提供します。NuGet でインストールしてください: `dotnet add package Aspose.Cells` |
| **An input Excel file** | チュートリアルでは `input.xlsx` を使用します。コードから参照できるフォルダーに配置してください。 |
| **Write permission to the output folder** | プログラムは `output.pptx` を書き込みます。ディレクトリが存在し、書き込み可能であることを確認してください。 |

> **Pro tip:** 複数のワークシートを扱う場合、変換前に各シートで印刷範囲の設定を繰り返してください。

## 手順 1: 新しい C# コンソール プロジェクトを作成する

ターミナルまたは PowerShell ウィンドウを開き、次のコマンドを実行します：

```bash
dotnet new console -n ExcelToPowerPointDemo
cd ExcelToPowerPointDemo
dotnet add package Aspose.Cells
```

これにより **ExcelToPowerPointDemo** という新しいプロジェクトが作成され、Aspose.Cells パッケージが追加されます。これは **how to export Excel** を他の形式にエクスポートするための主要な依存関係です。

## 手順 2: 変換コードを書く

`Program.cs` の内容を以下の完全な例に置き換えます。このコードは **convert excel to powerpoint** を示し、**how to set print area** を表示し、**convert excel to pptx** ファイルを生成します。

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook (how to export Excel)
            // -----------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
            Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");

            // -----------------------------------------------------------------
            // 2️⃣ Define the print area for the first worksheet (set print area excel)
            // -----------------------------------------------------------------
            // The range "A1:G30" will be the only part visible on the slide.
            // Adjust the range to match the data you want to show.
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";
            Console.WriteLine($"Print area set to {sheet.PageSetup.PrintArea} on sheet \"{sheet.Name}\".");

            // -----------------------------------------------------------------
            // 3️⃣ Configure conversion options for PowerPoint output
            // -----------------------------------------------------------------
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                // SaveFormat.Pptx tells Aspose.Cells to generate a PowerPoint file.
                SaveFormat = SaveFormat.Pptx,
                // Optional: set the slide size or DPI if needed.
                // HorizontalResolution = 300,
                // VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 4️⃣ Convert the worksheet to a PowerPoint presentation (convert excel to powerpoint)
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);
            Console.WriteLine($"Successfully created PowerPoint file at: {outputPath}");
        }
    }
}
```

### 各部分が重要な理由

* **Loading the workbook** – これはすべての **how to export Excel** シナリオの最初のステップです。`Workbook` はファイルをメモリに読み込み、シート、セル、書式設定への完全なアクセスを提供します。
* **Setting the print area** – `PageSetup.PrintArea` を設定することで、Aspose.Cells にどのセルを描画するか指示します。これは **set print area excel** の核心です。これがないと、シート全体がエクスポートされ、巨大で読めないスライドになる可能性があります。
* **Choosing `SaveFormat.Pptx`** – `ImageOrPrintOptions` オブジェクトで出力形式を切り替えられます。`SaveFormat` を `Pptx` に設定すると、**convert excel to pptx** パイプラインが起動します。
* **Calling `ConvertToPdf`** – メソッド名は `ConvertToPdf` ですが、`SaveFormat` が `Pptx` の場合、ライブラリは PowerPoint ファイルを出力します。これは単一の呼び出しで **convert excel to powerpoint** を行う推奨方法です。

## 手順 3: プログラムを実行する

プロジェクトフォルダーから次のコマンドを実行します：

```bash
dotnet run
```

すべてが正しく設定されていれば、以下のようなコンソール出力が表示されます：

```
Loaded workbook with 1 worksheet(s).
Print area set to A1:G30 on sheet "Sheet1".
Successfully created PowerPoint file at: YOUR_DIRECTORY\output.pptx
```

`output.pptx` を Microsoft PowerPoint または互換性のあるビューアで開きます。各スライドはワークシートの印刷ページに対応し、定義した範囲に限定されます。

## 複数のワークシートの処理

ブックブックに複数のシートが含まれ、各シートを個別のスライドデッキにしたい場合は、コレクションをループ処理します：

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet ws = workbook.Worksheets[i];
    ws.PageSetup.PrintArea = "A1:G30"; // adjust per sheet if needed
    string slidePath = $@"YOUR_DIRECTORY\output_sheet{i + 1}.pptx";
    ws.ConvertToPdf(conversionOptions, slidePath);
    Console.WriteLine($"Created {slidePath}");
}
```

このパターンは **how to export Excel** データをシートごとにエクスポートしつつ、個別に **setting print area** を設定する方法を示しています。

## エッジケースとベストプラクティスのヒント

| Situation | Recommended approach |
|-----------|----------------------|
| **Very large worksheets** | 印刷範囲を縮小するか、`HorizontalResolution`/`VerticalResolution` を上げて PPTX のサイズを抑えます。 |
| **Different page orientations** | 変換前に `sheet.PageSetup.Orientation = PageOrientationType.Landscape;` を設定します。 |
| **Custom slide size** | `conversionOptions.OnePagePerSheet = false;` を使用し、`conversionOptions.Width` と `conversionOptions.Height` を調整します。 |
| **Missing input file** | ロードコードを `try { … } catch (FileNotFoundException)` ブロックで囲み、明確なエラーメッセージを提供します。 |
| **Non‑ASCII characters** | ブックブックが UTF‑8 エンコーディングで保存されていることを確認してください。Aspose.Cells は Unicode を自動的に処理します。 |

## 参照用の完全なソースコード

以下は `using` ディレクティブとコメントを含むプログラム全体です。**手順 1** で作成したプロジェクト内に `Program.cs` として保存してください。

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the Excel file you want to convert.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";

            // 1️⃣ Load the workbook (how to export Excel)
            Workbook workbook = new Workbook(inputPath);

            // Select the first worksheet – you can loop for multiple sheets.
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Set the print area (set print area excel)
            sheet.PageSetup.PrintArea = "A1:G30";

            // 3️⃣ Prepare conversion options for PowerPoint output.
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx   // This triggers convert excel to pptx
            };

            // 4️⃣ Convert the worksheet to PowerPoint (convert excel to powerpoint)
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);

            Console.WriteLine("Conversion complete.");
        }
    }
}
```

## 期待される出力

プログラムを実行すると、以下を含む PowerPoint ファイル（`output.pptx`）が生成されます：

* ワークシートの印刷ページごとに 1 スライド。
* 各スライドに **A1:G30** 内のセルのみが表示されます。
* Excel で表示されているフォント、色、罫線などの書式が保持されます。

PowerPoint でファイルを開き、レイアウトが定義した印刷範囲と一致していることを確認してください。

## 結論

これで、Aspose.Cells を使用して C# で **convert Excel to PowerPoint** を行い、正確に **set print area excel** を設定する方法が分かりました。このチュートリアルでは **how to export Excel** を取り上げ、**how to set print area** を実演し、完全な **convert excel to pptx** を示しました。

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックをカバーしています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area in Excel and Export to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}