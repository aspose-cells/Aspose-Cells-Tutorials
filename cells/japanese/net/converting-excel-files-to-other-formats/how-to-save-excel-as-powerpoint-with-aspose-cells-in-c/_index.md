---
category: general
date: 2026-11-16
description: Excel を PowerPoint として保存する方法や、プログラムで Excel を PowerPoint に変換する方法を学びましょう。このステップバイステップガイドでは、Excel
  を PPTX にエクスポートする方法や、ブックを PPTX として保存する方法も取り上げています。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- export excel to pptx
- how to convert excel slide
- save workbook as pptx
language: ja
lastmod: 2026-11-16
og_description: Aspose.Cells を使用して Excel を PowerPoint に保存します。このガイドに従って Excel を PowerPoint
  に変換し、Excel を PPTX にエクスポートし、数分でブックを PPTX として保存できます。
og_image_alt: Screenshot showing the result of saving Excel as PowerPoint with editable
  shapes
og_title: Excel を PowerPoint として保存 – 完全な C# ガイド
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to save Excel as PowerPoint and convert Excel to PowerPoint
    programmatically. This step‑by‑step guide also covers export Excel to PPTX and
    saving a workbook as PPTX.
  headline: How to save Excel as PowerPoint with Aspose.Cells in C#
  type: TechArticle
tags:
- Excel
- PowerPoint
- Aspose.Cells
- C#
- Export
title: C#でAspose.Cellsを使用してExcelをPowerPointとして保存する方法
url: /ja/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-with-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells を使用した C# で Excel を PowerPoint に保存する方法

プログラムで **Excel を PowerPoint に保存** する必要がある場合、このチュートリアルは完全な、すぐに実行できるソリューションを提供します。レポートエンジンや自動スライドジェネレータを構築しているかどうかにかかわらず、以下の手順で Excel ワークシートを編集可能な PPTX スライドに数行のコードで変換できます。

**Excel を PowerPoint に変換** する方法、シートを PPTX ファイルにエクスポートする方法、テキストボックスや図形を編集可能なままに保つ方法を、.NET 環境から離れることなく学べます。

## 前提条件

* .NET 6.0 以降（コードは .NET Framework 4.7.2+ でも動作します）
* 有効な Aspose.Cells ライセンス（評価用に無料トライアルが利用可能です）
* Visual Studio 2022（または任意の C# IDE）
* エクスポートしたいデータと図形が含まれる Excel ワークブック

## 手順 1: Aspose.Cells のインストール

プロジェクトに Aspose.Cells NuGet パッケージを追加します：

```bash
dotnet add package Aspose.Cells
```

> **プロのコツ:** `-v` フラグを使用して特定のバージョンを指定します。例: `Aspose.Cells.24.5`.

## 手順 2: エクスポートしたいワークブックをロードする

**Excel を PowerPoint に保存** ワークフローの最初の操作は、ソースワークブックをロードすることです。

```csharp
using Aspose.Cells;
using System;

// Load the workbook that contains the shapes
Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");
```

*重要な理由:* ワークブックをロードすると、ワークシート、ページ設定、そして PowerPoint の編集可能な図形になる描画オブジェクトにアクセスできます。

## 手順 3: 編集可能な PPTX スライド用にエクスポートオプションを設定する

編集可能性を保持したまま **Excel を PowerPoint に変換** するには、`ImageOrPrintOptions` のいくつかのプロパティを設定する必要があります。

```csharp
// Prepare export options to generate an editable PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // Export format
    ExportEditableText = true,        // Keep text boxes editable
    ExportEditableShapes = true       // Keep shapes editable
};
```

*説明:*  
* `SaveFormat = SaveFormat.Pptx` は Aspose.Cells に PowerPoint ファイルを生成させることを指示します。  
* `ExportEditableText` と `ExportEditableShapes` は、生成されたスライドがネイティブな PowerPoint スライドのように動作することを保証します。テキストボックスや図形をクリックして、PowerPoint で直接編集できます。

## 手順 4: エクスポート領域を定義し、単一スライドにフィットさせる

**Excel を PPTX にエクスポート** する際、通常は特定の範囲をスライドに表示させたいです。印刷領域とフィットオプションを設定することで、クリーンな単一スライド出力が保証されます。

```csharp
// Define the area of the first worksheet to export
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G30";

// Fit the exported content to a single slide
sheet.PageSetup.FitToPagesTall = 1;
sheet.PageSetup.FitToPagesWide = 1;
```

*重要な理由:* `PrintArea` はエクスポートをセル A1 から G30 に限定し、`FitToPagesTall` と `FitToPagesWide` はすべてを1枚のスライドに圧縮し、不要な余分なページが生成されるのを防ぎます。

## 手順 5: ワークシートを編集可能な PPTX ファイルとして保存する

これで最終的に **ワークブックを PPTX として保存** でき、**Excel を PowerPoint に保存** プロセスが完了します。

```csharp
// Save the worksheet as an editable PPTX file
workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
Console.WriteLine("Export completed: EditableShapes.pptx");
```

プログラムを実行した後、Microsoft PowerPoint で `EditableShapes.pptx` を開きます。選択した Excel 範囲を反映したスライドが表示され、すべてのテキストボックスと図形が完全に編集可能です。

### 期待される出力

* `C:\Output\` に作成される `EditableShapes.pptx` という名前のファイル。
* 範囲 A1:G30 を含む PowerPoint スライドが1枚。
* テキストボックス、チャート、図形はダブルクリックで PowerPoint 上で直接編集できます。

## 完全なソースコード（コピーしてすぐに使用可能）

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the shapes
            Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");

            // Step 2: Prepare export options to generate an editable PPTX slide
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportEditableText = true,   // keep text boxes editable
                ExportEditableShapes = true  // keep shapes editable
            };

            // Step 3: Define the area of the first worksheet to export
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";

            // Step 4: Fit the exported content to a single slide
            sheet.PageSetup.FitToPagesTall = 1;
            sheet.PageSetup.FitToPagesWide = 1;

            // Step 5: Save the worksheet as an editable PPTX file
            workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
            Console.WriteLine("Export completed: EditableShapes.pptx");
        }
    }
}
```

## よくある質問とエッジケースの対処法

| Question | Answer |
|----------|--------|
| **複数のワークシートがある場合はどうすればよいですか？** | `workbook.Worksheets` をループし、各シートに対して手順 3‑5 を繰り返し、出力ファイル名を変更します（例: `Sheet1.pptx`, `Sheet2.pptx`）。 |
| **ワークブック全体を単一の PowerPoint デッキにエクスポートできますか？** | はい。`ImageOrPrintOptions` の `ExportAllSheets = true` を設定します。各ワークシートが別々のスライドになります。 |
| **図形が画像として表示され、編集可能なオブジェクトになりません。** | `ExportEditableShapes = true` を設定し、Aspose.Cells 24.5 以降を使用していることを確認してください（以前のバージョンにはこの機能がありません）。 |
| **生成された PPTX が大きすぎます。** | 印刷領域を縮小するか、`exportOptions.ImageResolution` で画像解像度を下げてください。 |
| **本番環境でライセンスが必要ですか？** | 有料ライセンスは評価用の透かしを除去し、フルパフォーマンスを解放します。無料トライアルはテストに使用できます。 |

## 安定した本番コードのためのヒント

* `Workbook` や `Save` を呼び出す前に **ファイルパスを検証** して、`FileNotFoundException` を回避します。  
* **try/catch** ブロックでエクスポートをラップし、ライセンスエラー（`Aspose.Cells.LicenseException`）を処理します。  
* 使用後は **ワークブックを破棄**（`workbook.Dispose()`）して、アンマネージドリソースを解放します。  
* Web サービスで多数の大きなシートをエクスポートする場合は、**非同期 I/O**（`FileStream` と `await`）を使用します。

## 次のステップ

これで **Excel を PowerPoint に保存** する方法が分かったので、関連トピックを探求できます：

* **カスタムスライドレイアウトで Excel を PPTX にエクスポート** – `SlideSize` を調整し、マスタースライドを追加します。  
* **Excel スライドを PDF に変換** – 印刷用バージョンとして `SaveFormat.Pdf` を使用します。  
* **フォルダー内のワークブックを一括変換** – 上記のループと `Directory.GetFiles` を組み合わせます。  

さまざまな印刷領域、スケーリングオプション、PowerPoint テーマを試して、組織のブランディングに合わせた出力を作成してください。

---

*コーディングを楽しんでください！このガイドが **Excel を PowerPoint に変換** するのに役立った場合は、チームメンバーと共有するか、さらなるサポートが必要な場合は Aspose.Cells の GitHub リポジトリで issue を開いてください。*

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックをカバーしています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [C# と Aspose.Cells を使用して Excel を PowerPoint に保存する方法](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/)
- [Excel から PPTX を保存する方法 – Excel シートを PowerPoint にエクスポートする完全ガイド](/cells/english/java/integration-interoperability/how-to-save-pptx-from-excel-complete-guide-to-export-excel-s/)
- [Excel を PowerPoint に変換する方法 – 完全ステップバイステップガイド](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-full-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}