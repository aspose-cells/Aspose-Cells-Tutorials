---
category: general
date: 2026-03-22
description: Excelで印刷範囲を設定し、編集可能なシェイプ付きでExcelをPowerPointに変換します。タイトル行を繰り返す方法、ExcelからPowerPointを作成する方法、Excelをpptxにエクスポートする方法を学びましょう。
draft: false
keywords:
- set print area
- convert excel to powerpoint
- repeat title row
- create powerpoint from excel
- export excel to pptx
language: ja
og_description: Excelで印刷範囲を設定し、編集可能なシェイプを含むPowerPointスライドに変換します。タイトル行を繰り返し、ExcelをPPTXにエクスポートする完全ガイドをご覧ください。
og_title: Excelで印刷範囲を設定 – PowerPointへのエクスポートチュートリアル
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint generation
title: Excelで印刷範囲を設定し、PowerPointへエクスポートする – ステップバイステップガイド
url: /ja/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excelで印刷範囲を設定しPowerPointへエクスポート – 完全プログラミングチュートリアル

Excelのワークシートで **印刷範囲を設定** し、そのスライスをPowerPointのスライドに変換したことがありますか？ あなただけではありません。多くのレポートパイプラインでは、きれいに印刷できるデータをプレゼンテーションにも表示する必要があり、しばしば最初の行をタイトルとして繰り返すことが求められます。良いニュースは、数行のC#コードで **excel を powerpoint に変換** でき、すべてのテキストボックスを編集可能に保ち、さらに **タイトル行を自動で繰り返す** ことができるということです。

このガイドでは、印刷範囲の設定からPowerPoint（PPTX）ファイルの作成まで、必要なすべての手順を解説します。最後まで読めば、 **excel から powerpoint を作成** し、 **excel を pptx にエクスポート** でき、任意の .NET プロジェクトで同じコードを再利用できるようになります。マジックはなく、明確な手順と完全に実行可能なサンプルが揃っています。

## 必要なもの

本題に入る前に、以下をご用意ください。

- **.NET 6.0** 以上（APIは .NET Framework でも動作します）
- **Aspose.Cells for .NET**（`Workbook`、`ImageOrPrintOptions` などを提供するライブラリ）
- 基本的な C# IDE（Visual Studio、Rider、または C# 拡張機能付き VS Code）
- エクスポートしたいデータが入った Excel ファイル（`input.xlsx`）

以上だけです—Aspose.Cells 以外に追加の NuGet パッケージは不要です。まだライブラリを追加していない場合は、次のコマンドを実行してください。

```bash
dotnet add package Aspose.Cells
```

これで準備完了です。

## 手順 1: ワークブックの読み込み – エクスポートの出発点

最初に行うべきことは、スライドに変換したいシートが含まれるワークブックを読み込むことです。ワークブックはソースドキュメントと考えてください。これがなければ、以降の操作はすべて意味を成しません。

```csharp
using Aspose.Cells;

// Load the workbook that contains the shapes and data
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\input.xlsx");
```

**重要ポイント:** ワークブックを読み込むことで、ワークシートコレクションやページ設定オプション、エクスポートエンジンにアクセスできます。このステップを省略すると **印刷範囲** を設定したり、行を繰り返したりできません。

> **プロのコツ:** テスト時は絶対パスを使用し、実運用では相対パスまたは設定ベースのパスに切り替えましょう。

## 手順 2: エクスポートオプションの構成 – テキストボックスとシェイプを編集可能に保つ

PowerPoint にエクスポートする際、スライドを編集可能にしたいことが多いでしょう。Aspose.Cells では `ImageOrPrintOptions` でそれを制御できます。`ExportTextBoxes` と `ExportShapeObjects` を `true` に設定すると、これらのオブジェクトが画像にフラット化されず、PowerPoint のネイティブ要素として保持されます。

```csharp
// Configure export options for a PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // The target format – crucial for PowerPoint
    ExportTextBoxes = true,            // Keep text boxes editable
    ExportShapeObjects = true          // Keep shape objects editable
};
```

**重要ポイント:** **excel を powerpoint に変換** した後にスライドを手動で調整したい場合、この設定によりテキストボックスを一から作り直す手間が省けます。また、矢印やチャートなどのシェイプもベクターオブジェクトとして残り、サイズ変更が可能です。

## 手順 3: 印刷範囲の設定とタイトル行の繰り返し

ここがチュートリアルの核心です： **印刷範囲を設定** し、最初の行をすべての印刷ページ（今回の場合はエクスポートスライド）で繰り返します。印刷範囲は、Excel が印刷（またはエクスポート）対象とするセルを指定します。

```csharp
// Define the area of the sheet to export (A1:G20)
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G20";

// Repeat the first row as a title on each printed page
sheet.PageSetup.PrintTitleRows = "$1:$1";
```

**重要ポイント:** エクスポート範囲を `A1:G20` に限定することで、不要な空白領域の読み込みを防ぎ、変換速度が向上し、スライドがすっきりします。`PrintTitleRows` 行は、最初の行をヘッダーとして扱うようにし、プレゼンテーションで **タイトル行を繰り返す** 際に理想的です。

> **エッジケース:** データが 2 行目から始まる場合は、範囲を適宜調整してください（例: `PrintTitleRows = "$2:$2"`）。

## 手順 4: ワークシートを PowerPoint ファイルとして保存

最後に、スライドをディスクに書き出します。`Save` メソッドは保存先ファイル名と、前述のオプションを受け取ります。結果として、編集可能なテキストボックスとシェイプを含む PPTX ファイルが生成され、PowerPoint で開くことができます。

```csharp
// Save the selected sheet as a PPTX file using the configured options
string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
workbook.Save(outputPath, exportOptions);
```

**期待される結果:** `SheetWithEditableShapes.pptx` を PowerPoint で開くと、最初の行がタイトルとして表示され、`A1:G20` のすべてのセルが描画され、Excel で追加したシェイプは依然として移動・編集可能です。ラスタ画像ではなく、ネイティブの PowerPoint オブジェクトです。

## 完全動作サンプル – すべての手順を統合

以下はコピー＆ペーストで実行できる完全版プログラムです。コンソールアプリとして実行するか、任意のソリューションに組み込んで使用してください。

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the workbook
            string inputPath = @"C:\MyProjects\ExcelToPpt\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Set export options for editable PPTX
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportTextBoxes = true,
                ExportShapeObjects = true
            };

            // Step 3: Define print area and repeat title row
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G20";
            sheet.PageSetup.PrintTitleRows = "$1:$1";

            // Step 4: Save as PowerPoint
            string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
            workbook.Save(outputPath, exportOptions);

            Console.WriteLine($"Successfully exported to {outputPath}");
        }
    }
}
```

**期待出力:** プログラム実行後、コンソールに成功メッセージが表示され、指定した場所に PPTX ファイルが生成されます。ファイルを開くと、選択した範囲だけが表示された単一スライドが現れ、テキストボックスや元のシェイプがすべて編集可能です。

## よくある質問 & 注意点

| Question | Answer |
|----------|--------|
| **Does this work with multiple worksheets?** | Yes. Loop through `workbook.Worksheets` and repeat the same steps for each sheet, changing the output filename each time. |
| **What if I need to export more than one slide?** | Call `workbook.Save` multiple times with different `ImageOrPrintOptions` objects, each configured with a different `PageSetup` if needed. |
| **Can I change the slide size?** | Use `exportOptions.ImageFormat` to set DPI, or adjust `sheet.PageSetup.PaperSize` before saving. |
| **Is Aspose.Cells free?** | It offers a free evaluation with watermarks. For production, a license is required. |
| **What about Excel formulas?** | The exported values are the **calculated results** at the time of export. If you need live formulas in PowerPoint, you’ll need a different approach. |

## スムーズなワークフローのためのヒント

- **プロのコツ:** エクスポート前に `Workbook.Settings.CalcMode = CalculationModeType.Automatic` を設定し、すべての数式が最新の状態であることを保証しましょう。 |
- **注意点:** 非常に大きな範囲はメモリ圧迫の原因となります。印刷範囲は必要最小限に絞ってください。 |
- **パフォーマンスのコツ:** 多数のシートをエクスポートする場合は、`ImageOrPrintOptions` のインスタンスを再利用すると、毎回新規作成するオーバーヘッドを削減できます。 |
- **バージョン情報:** 上記コードは Aspose.Cells 23.10（2023年11月リリース）を対象としています。以降のバージョンでも API は基本的に同じですが、破壊的変更がないかリリースノートを必ず確認してください。 |

## 結論

Excel ワークシートで **印刷範囲を設定** し、最初の行をタイトルとして繰り返し、 **excel を pptx にエクスポート** すると同時にテキストボックスやシェイプを編集可能に保つ方法を解説しました。要するに、数行の C# で **excel を powerpoint に変換**、 **タイトル行を繰り返す**、そして **excel から powerpoint を作成** できる信頼性の高い手法を習得したことになります。

次のステップに進みませんか？数十件のレポートをバッチ変換したり、エクスポート後に PowerPoint SDK を使ってカスタムスライドレイアウトを追加したりしてみましょう。可能性は無限大です—実験し、試行錯誤し、プログラムによる文書生成の力を存分に楽しんでください。

このチュートリアルが役に立ったら、シェアしたり、独自の工夫をコメントで共有したり、 **excel を pptx にエクスポート** や関連自動化トピックに関する他のガイドもぜひご覧ください。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}