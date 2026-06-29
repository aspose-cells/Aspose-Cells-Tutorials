---
category: general
date: 2026-06-27
description: C#でExcelをエクスポートする方法—ExcelをPowerPointに変換する方法、ExcelからPowerPointを作成する方法、そして数分でC#でExcelブックを読み込む方法を学びましょう。
draft: false
keywords:
- how to export excel
- convert excel to powerpoint
- create powerpoint from excel
- load excel workbook c#
- export excel chart powerpoint
language: ja
og_description: C#でExcelをエクスポートする方法は簡単です。このステップバイステップのチュートリアルに従って、ExcelをPowerPointに変換し、ExcelからPowerPointを作成し、C#でExcelブックを読み込みましょう。
og_title: Excel を PowerPoint にエクスポートする方法 – 完全 C# ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to export Excel using C#—learn to convert Excel to PowerPoint,
    create PowerPoint from Excel, and load Excel workbook C# in minutes.
  headline: How to Export Excel to PowerPoint – Complete C# Guide
  type: TechArticle
- description: How to export Excel using C#—learn to convert Excel to PowerPoint,
    create PowerPoint from Excel, and load Excel workbook C# in minutes.
  name: How to Export Excel to PowerPoint – Complete C# Guide
  steps:
  - name: '**Load Excel workbook** – We read the `.xlsx` file into memory.'
    text: '**Load Excel workbook** – We read the `.xlsx` file into memory.'
  - name: '**Convert workbook to a PowerPoint presentation** – Aspose converts each
      worksheet (or selected chart) into a slide.'
    text: '**Convert workbook to a PowerPoint presentation** – Aspose converts each
      worksheet (or selected chart) into a slide.'
  - name: '**Save the generated presentation** – The final PPTX can be opened in PowerPoint,
      edited, or sent to stakeholders.'
    text: '**Save the generated presentation** – The final PPTX can be opened in PowerPoint,
      edited, or sent to stakeholders.'
  type: HowTo
- questions:
  - answer: Yes. Use `Workbook.Worksheets["Sheet1"]` to isolate a sheet, then call
      `SaveToPresentation` on that worksheet alone.
    question: Can I export only a single worksheet instead of the whole workbook?
  - answer: Macros are not transferred to PowerPoint—only visual objects (charts,
      tables) are exported. If you need macro functionality, consider generating the
      slides first, then adding VBA manually.
    question: What about preserving macros?
  - answer: Absolutely. Aspose.Cells supports legacy formats; just change the file
      extension in `excelPath`.
    question: Does this work with `.xls` files?
  - answer: 'After creating the `Presentation` object, set: ```csharp presentation.SlideSize.Size
      = SlideSizeType.Widescreen; ```'
    question: How do I change the slide size to widescreen (16:9)?
  - answer: 'Open‑source libraries like EPPlus can read Excel, but they don’t provide
      direct Excel‑to‑PowerPoint conversion. You’d need to manually render charts
      to images and insert them, which is far more code. ## Tips & Best Practices
      - **Batch processing:** If you have dozens of workbooks, wrap the conversio'
    question: Is there a free alternative?
  type: FAQPage
tags:
- C#
- Excel
- PowerPoint
- Aspose
title: Excel を PowerPoint にエクスポートする方法 – 完全 C# ガイド
url: /ja/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel を PowerPoint にエクスポートする方法 – 完全な C# ガイド

**Excel のデータ**を書式を失わずに直接 PowerPoint のスライドにエクスポートしたいと思ったことはありませんか？ あなただけではありません。多くのレポートパイプラインで、ボトルネックは Excel のブックからチャートやテーブルを洗練されたスライドデッキへ移すことです。良いニュースは、数行の C# コードさえ書けば **Excel を PowerPoint に変換**し、完全に編集可能な PPTX を生成し、チャートの忠実度さえも保持できるということです。

このチュートリアルでは、C# で Excel ブックを読み込み、その内容を PowerPoint プレゼンテーションに変換し、結果を保存する手順を解説します。最後まで読めば、手動でコピー＆ペーストすることなく **Excel から PowerPoint を自動作成**できるようになります。重い UI 操作は不要、コードだけです。

> **必要なもの**  
> * .NET 6+（または .NET Framework 4.7.2+）  
> * Aspose.Cells と Aspose.Slides の NuGet パッケージ（重い処理を担当）  
> * 少なくとも 1 つのチャートを含むサンプル Excel ファイル（`chartOle.xlsx` と呼びます）  

これらが揃ったら、さっそく始めましょう。

![C# を使用して Excel を PowerPoint にエクスポートする方法を示す図](https://example.com/images/export-excel-to-pptx.png "Excel を PowerPoint にエクスポートする方法の図")

## C# で Excel を PowerPoint にエクスポートする概要

コードを書く前に、3 つのステップの流れを把握しておきましょう。

1. **Excel ブックをロード** – `.xlsx` ファイルをメモリに読み込みます。  
2. **ブックを PowerPoint プレゼンテーションに変換** – Aspose が各ワークシート（または選択したチャート）をスライドに変換します。  
3. **生成されたプレゼンテーションを保存** – 完成した PPTX は PowerPoint で開いたり、編集したり、ステークホルダーに配布したりできます。

各ステップは意図的に分離されているので、後でカスタムロジック（特定シートの選択、スライドテーマの適用など）を差し込むことが容易です。では、詳細を見ていきましょう。

## Step 1 – Load Excel Workbook C# Style

最初にやるべきことは、Excel ファイルをアプリケーションに取り込むことです。Aspose.Cells を使うとコードはシンプルです。

```csharp
using Aspose.Cells;   // Handles Excel files
using Aspose.Slides;  // Handles PowerPoint files
using System;

// Step 1: Load the Excel workbook
string excelPath = @"YOUR_DIRECTORY\chartOle.xlsx";

if (!System.IO.File.Exists(excelPath))
{
    throw new FileNotFoundException($"Excel file not found at {excelPath}");
}

// The Workbook class reads the .xlsx file into memory
Workbook workbook = new Workbook(excelPath);
```

**この処理が重要な理由:**  
`Workbook` はスプレッドシート全体を抽象化し、ワークシート、セル、そして何より埋め込みチャートへのアクセスを提供します。存在チェックを省くと、後で曖昧な `FileNotFoundException` が発生し、運用環境でのデバッグが大変になります。

**プロのコツ:** 特定のシートだけが必要な場合は、`LoadOptions` オブジェクトを渡してメモリ使用量を抑えることができます。

```csharp
LoadOptions options = new LoadOptions(LoadFormat.Xlsx) { LoadDataOnly = true };
Workbook workbook = new Workbook(excelPath, options);
```

この小さな調整だけで、大規模ブックの読み込み速度が劇的に向上します。

## Step 2 – Convert Excel to PowerPoint (Export Excel Chart PowerPoint)

いよいよマジックです。ブックを PPTX に変換します。Aspose.Slides が 1 つのメソッドで重い処理を担います。

```csharp
// Step 2: Convert the workbook to a PowerPoint presentation (PPTX format)
Presentation presentation = workbook.SaveToPresentation(ExportToPresentationFormat.Pptx);
```

**内部で何が起きているか:**  
`SaveToPresentation` は各ワークシートを走査し、チャートオブジェクトを抽出してチャートごとにスライドを作成します。元のチャートのスタイル（色、フォント、データラベル）をそのまま保持します。ブックに単なるテーブルが含まれている場合は、スライド上にテキストボックスとして描画されます。

**エッジケース – 複数チャート:**  
1 つのワークシートに複数のチャートがあると、Aspose はそれらを同一スライドに縦に並べます。別々のスライドにしたい場合は、チャートを手動でループ処理してください。

```csharp
Presentation presentation = new Presentation();

foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (Chart chart in sheet.Charts)
    {
        // Export each chart as an individual slide
        ISlide slide = presentation.Slides.AddEmptySlide(presentation.SlideSize.Size);
        chart.ExportToSlide(presentation, slide);
    }
}
```

このスニペットで細かい制御が可能になり、洗練されたデッキを作成できます。

## Step 3 – Save the Generated Presentation (Create PowerPoint from Excel)

最後のステップは、PPTX ファイルをディスクに保存することです。とてもシンプルです。

```csharp
// Step 3: Save the generated presentation to a file
string pptxPath = @"YOUR_DIRECTORY\editable.pptx";
presentation.Save(pptxPath, Aspose.Slides.Export.SaveFormat.Pptx);

Console.WriteLine($"Presentation saved successfully to {pptxPath}");
```

**出力を検証すべき理由:**  
保存後に `editable.pptx` を PowerPoint で開くと、チャートごとに 1 スライドが作成され、すべて編集可能（色変更やオブジェクト移動が可能）であることが確認できます。もしチャートの見た目が崩れている場合は、元の Excel チャートが標準フォントを使用しているか確認してください。カスタムフォントは正しく埋め込まれないことがあります。

**よくある落とし穴:**  
ネットワーク共有先に保存する際、権限が不足していると `UnauthorizedAccessException` がスローされます。実行アカウントが `YOUR_DIRECTORY` への書き込み権限を持っていることを確認してください。

## Full Working Example – All Steps Together

以下は、すべての手順をまとめた完全な実行可能プログラムです。新しいコンソールアプリプロジェクトに貼り付け、NuGet パッケージを復元して **F5** を押すだけです。

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Paths – adjust to your environment
            string excelPath = @"YOUR_DIRECTORY\chartOle.xlsx";
            string pptxPath = @"YOUR_DIRECTORY\editable.pptx";

            // -------------------------------------------------
            // Step 1: Load the Excel workbook (load excel workbook c#)
            // -------------------------------------------------
            if (!System.IO.File.Exists(excelPath))
            {
                Console.WriteLine($"Error: File not found -> {excelPath}");
                return;
            }

            Workbook workbook = new Workbook(excelPath);
            Console.WriteLine("Excel workbook loaded successfully.");

            // -------------------------------------------------
            // Step 2: Convert Excel to PowerPoint (export excel chart powerpoint)
            // -------------------------------------------------
            Presentation presentation = workbook.SaveToPresentation(ExportToPresentationFormat.Pptx);
            Console.WriteLine("Workbook converted to PowerPoint.");

            // -------------------------------------------------
            // Step 3: Save the generated presentation (create powerpoint from excel)
            // -------------------------------------------------
            presentation.Save(pptxPath, Aspose.Slides.Export.SaveFormat.Pptx);
            Console.WriteLine($"Presentation saved at: {pptxPath}");
        }
    }
}
```

**期待されるコンソール出力:**

```
Excel workbook loaded successfully.
Workbook converted to PowerPoint.
Presentation saved at: YOUR_DIRECTORY\editable.pptx
```

`editable.pptx` を開くと、各チャートに対応したスライドが表示され、さらに調整が可能です。

## Frequently Asked Questions (FAQs)

**Q: ワークブック全体ではなく、単一のワークシートだけをエクスポートできますか？**  
A: はい。`Workbook.Worksheets["Sheet1"]` でシートを限定し、そのシートに対して `SaveToPresentation` を呼び出すだけです。

**Q: マクロはどうなりますか？**  
A: マクロは PowerPoint へは転送されません。転送されるのは視覚オブジェクト（チャート、テーブル）のみです。マクロ機能が必要な場合は、スライドを生成した後に手動で VBA を追加してください。

**Q: `.xls` ファイルでも動作しますか？**  
A: 完全に対応しています。Aspose.Cells はレガシーフォーマットをサポートしているので、`excelPath` の拡張子を変更するだけで OK です。

**Q: スライドサイズをワイドスクリーン（16:9）に変更するには？**  
A: `Presentation` オブジェクト作成後に次のコードを設定します。

```csharp
presentation.SlideSize.Size = SlideSizeType.Widescreen;
```

**Q: 無料の代替手段はありますか？**  
A: EPPlus などのオープンソースライブラリは Excel の読み取りは可能ですが、直接 Excel から PowerPoint への変換機能は提供していません。チャートを画像として手動でレンダリングし、挿入する必要があり、コード量が大幅に増えます。

## Tips & Best Practices

- **バッチ処理:** 数十個のブックを処理する場合は、`Parallel.ForEach` ループで変換をラップすると高速化できます。ただし、Aspose オブジェクトはスレッドセーフでない点に注意してください。  
- **メモリ管理:** 大きなファイルを扱う際は、`presentation.Dispose()` と `workbook.Dispose()` を呼び出してネイティブリソースを速やかに解放しましょう。  
- **スライドのスタイリング:** 変換後に `presentation.SlideMaster` を使ってマスタースライドテーマを適用すれば、全スライドの外観を統一できます。  
- **テスト:** 既知のブックをロードし、変換を実行し、生成された PPTX に期待通りのスライド数が含まれるかをアサートする簡易ユニットテストを自動化すると安心です。

## Conclusion

本稿では **Excel のデータを C# で PowerPoint デッキにエクスポートする方法** を示しました。ブックをロードし、Aspose で変換し、PPTX を保存するだけで、**Excel を PowerPoint に変換**し、**Excel から PowerPoint を作成**し、**C# スタイルで Excel ブックをロード**する再利用可能なプログラムが完成します。コードは自己完結型で、最新の .NET ランタイム上で動作し、複雑なレポートパイプラインにも拡張可能です。

次のステップに挑戦してみませんか？スライド 1 枚に複数チャートを埋め込んだり、カスタムレイアウトを適用したり、スピーカーノートを自動生成したりすると、さらに高度な自動化が実現できます。Excel の自動化と PowerPoint の生成を組み合わせれば、可能性は無限です。

質問や面白いユースケースがあればコメントで教えてください。ハッピーコーディング！

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれているので、API の追加機能を習得したり、代替実装アプローチを探求したりするのに役立ちます。

- [Aspose.Cells for .NET を使用した Excel から PowerPoint への変換: 完全ガイド](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Aspose.Cells for .NET を使用した Excel チャートの PDF エクスポート: ステップバイステップガイド](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Aspose.Cells for .NET を使用した Excel の HTML エクスポート（グリッドライン付き）](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}