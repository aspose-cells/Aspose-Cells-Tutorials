---
category: general
date: 2026-02-09
description: 数分でExcelからPowerPointを作成 – 簡単なC#コード例でExcelをPowerPointに変換し、ExcelをPPTにエクスポートする方法を学びましょう。
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export excel to ppt
- generate ppt from excel
- how to convert excel to pptx
language: ja
og_description: ExcelからPowerPointを素早く作成します。このガイドでは、ExcelをPowerPointに変換する方法、ExcelをPPTにエクスポートする方法、そしてC#を使用してExcelからPPTを生成する方法を紹介します。
og_title: ExcelからPowerPointを作成する – 完全プログラミングガイド
tags:
- C#
- Aspose.Cells
- PowerPoint automation
- Office interop
title: ExcelからPowerPointを作成する – ステップバイステップガイド
url: /ja/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel から PowerPoint を作成 – 完全プログラミングガイド

Excel から **PowerPoint を作成** したいと思ったことはありますか、でもどの API を呼び出せばよいか分からなかったことはありませんか？ あなたは一人ではありません。多くの開発者が、スプレッドシートを手動でコピー＆ペーストせずにスライドデッキに変換しようとすると壁にぶつかります。  

良いニュースです：数行の C# コードで **Excel を PowerPoint に変換** でき、シートの図形をエクスポートし、すぐにプレゼンテーションできる PPTX ファイルを作成できます。このチュートリアルでは、全工程を順に解説し、各ステップの重要性を説明し、最も一般的な落とし穴への対処方法を示します。

## 学べること

- チャート、画像、または SmartArt を含む Excel ワークブックの読み込み方法  
- Aspose.Cells ライブラリを使用した **Excel を PPT にエクスポート** する正確な呼び出し方  
- 生成されたプレゼンテーションの保存方法と結果の検証方法  
- 図形がないワークブックの処理、スライドサイズの調整、バージョン不一致のトラブルシューティングのコツ  

外部ツール不要、COM 相互運用も不要、.NET Core または .NET 5+ がサポートされている環境ならどこでも動作する純粋な .NET コードです。

---

## 前提条件

始める前に以下を用意してください：

1. **Aspose.Cells for .NET**（`SaveToPresentation` を提供するライブラリ）。NuGet から取得できます：  

   ```bash
   dotnet add package Aspose.Cells
   ```
2. 最近の .NET SDK（6.0 以降推奨）。  
3. 少なくとも 1 つの図形、チャート、または画像が含まれた Excel ファイル（`shapes.xlsx`）。

以上です—Office のインストールは不要、デモ目的のライセンス問題もなし（無料評価版で問題なく動作します）。

---

## Step 1: Load the Excel Workbook (Create PowerPoint from Excel)

最初に必要なのは、ソースファイルを指す `Workbook` オブジェクトです。このオブジェクトは、すべてのワークシート、チャート、埋め込みオブジェクトを含む Excel ドキュメント全体を表します。

```csharp
using Aspose.Cells;
using Aspose.Slides;

// Step 1: Load the Excel workbook containing the shapes
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\shapes.xlsx");

// Why this matters:
// - `Workbook` abstracts the file format, so you don’t have to worry about .xls vs .xlsx.
// - Loading the file early lets you inspect its contents (e.g., count of worksheets) before conversion.
```

> **Pro tip:** ファイルの存在が不確かの場合は、コンストラクタを `try/catch` でラップし、わかりやすいエラーメッセージを提供しましょう。後で暗号的な `FileNotFoundException` に悩まされることを防げます。

---

## Step 2: Convert the Workbook to a PowerPoint Presentation (Export Excel to PPT)

Aspose.Cells には、ワークブック全体または選択したシートだけを PowerPoint プレゼンテーションに変換する組み込みエクスポーターが同梱されています。`SaveToPresentation` メソッドがその重い処理を担います。

```csharp
// Step 2: Convert the workbook to a PowerPoint presentation (PPTX format)
Presentation presentation = workbook.SaveToPresentation(ExportTo.Pptx);

// How it works:
// - Each worksheet becomes a separate slide.
// - Shapes, charts, and images are rasterized and placed on the slide preserving their layout.
// - You can later tweak the `Presentation` object (e.g., add a title slide) before saving.
```

サブセットのシートだけで **generate ppt from excel** が必要な場合は、`SheetOptions` コレクションを受け取るオーバーロードを使用できます。ほとんどのシナリオではデフォルトの変換で十分です。

---

## Step 3: Save the Generated Presentation (How to Convert Excel to PPTX)

`Presentation` インスタンスが手に入ったら、ディスクへの保存はとても簡単です。出力は標準的な `.pptx` ファイルとなり、最新バージョンの PowerPoint で開くことができます。

```csharp
// Step 3: Save the generated presentation to a file
presentation.Save(@"C:\MyProjects\ExcelToPpt\shapes.pptx");

// Verification:
// Open the file in PowerPoint or use Aspose.Slides to programmatically inspect slide count.
```

> **What if the workbook has no shapes?**  
> エクスポーターは依然としてスライドを作成しますが、内容は空になります。変換前に `workbook.Worksheets[i].Shapes.Count` をチェックし、そのシートをスキップするかどうか判断できます。

---

## Optional: Fine‑Tuning the Output (Advanced Export Excel to PPT)

デフォルトのスライドサイズ（標準 4:3）がワイドスクリーン向きでないことがあります。保存前にスライドの寸法を調整できます：

```csharp
// Set slide size to widescreen (16:9)
presentation.SlideSize.SetSize(SlideSizeType.Widescreen, SlideSizeScaleType.DoNotScale);

// Add a custom title slide (optional)
ISlide titleSlide = presentation.Slides.InsertEmptySlide(0, presentation.LayoutSlides[0]);
titleSlide.Shapes.AddAutoShape(ShapeType.Rectangle, 50, 50, 600, 100)
          .TextFrame.Text = "Quarterly Report – Exported from Excel";
```

これらの調整により、**Excel を PowerPoint に変換** した結果が単なるデータのダンプではなく、プロフェッショナルな見た目になります。

---

## Full Working Example (All Steps Combined)

以下は完全に動作するサンプルプログラムです。コンソールアプリにコピーペーストし、ファイルパスを調整して **F5** を押すだけです。

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string excelPath = @"C:\MyProjects\ExcelToPpt\shapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2️⃣ Convert to PPTX
            Presentation presentation = workbook.SaveToPresentation(ExportTo.Pptx);

            // Optional: set widescreen layout
            presentation.SlideSize.SetSize(SlideSizeType.Widescreen, SlideSizeScaleType.DoNotScale);

            // Optional: add a title slide
            ISlide titleSlide = presentation.Slides.InsertEmptySlide(0, presentation.LayoutSlides[0]);
            titleSlide.Shapes.AddAutoShape(ShapeType.Rectangle, 50, 50, 600, 100)
                      .TextFrame.Text = "Quarterly Report – Exported from Excel";

            // 3️⃣ Save the PPTX file
            string pptxPath = @"C:\MyProjects\ExcelToPpt\shapes.pptx";
            presentation.Save(pptxPath);

            Console.WriteLine($"✅ Successfully created PowerPoint from Excel! File saved at: {pptxPath}");
        }
    }
}
```

**Expected outcome:** PowerPoint で `shapes.pptx` を開きます。各ワークシートごとに 1 枚のスライドが作成され、元のチャート、画像、その他の図形が保持されています。オプションのタイトルスライドが最初に挿入され、デッキに洗練された導入部が加わります。

---

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| *単一シートだけが必要な場合は？* | `Workbook.Worksheets[0]` を使用し、`SheetOptions` 経由でそのシートに対して `SaveToPresentation` を呼び出します。 |
| *Excel の数式を保持できますか？* | できません—数式はスライド上で静的な値として描画されます。リアルタイムデータが必要な場合は、後で PPTX を Excel にリンクすることを検討してください。 |
| *Linux/macOS でも動作しますか？* | はい。Aspose.Cells はプラットフォームに依存せず、.NET ランタイムさえインストールすれば動作します。 |
| *パスワード保護されたワークブックは？* | `LoadOptions` にパスワードを設定してロードし、その後 `SaveToPresentation` を呼び出します。 |
| *空白スライドが生成されるのはなぜですか？* | ワークブックに図形が存在しない場合（`Shapes.Count > 0` でない）でもスライドは作成されます。空のシートに対しては空白スライドが生成されます。 |

---

## Conclusion

これで C# を使用した **Excel から PowerPoint を作成** のエンドツーエンドソリューションが明確になりました。ワークブックを読み込み、`SaveToPresentation` を呼び出し、結果を保存するだけで、**Excel を PowerPoint に変換**、**Excel を PPT にエクスポート**、そして **Excel から PPT を生成** できます。  

ここからさらに以下を検討できます：

- Aspose.Slides を使って生成スライドにアニメーションを追加する。  
- パイプライン全体を自動化（例：フォルダー内のファイルを読み込み、一括変換）。  
- コードを ASP.NET Core API に統合し、ユーザーが Excel ファイルをアップロードして即座に PPTX を受け取れるようにする。

ぜひ試してみて、スライドサイズを調整したりカスタムタイトルを加えたりして、出力を自分色に仕上げてください。質問や問題があれば下のコメント欄にどうぞ。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}