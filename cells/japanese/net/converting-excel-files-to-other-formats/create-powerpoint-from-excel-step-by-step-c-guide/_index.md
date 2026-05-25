---
category: general
date: 2026-03-30
description: Aspose.Cells と Aspose.Slides を使用して、Excel から PowerPoint を素早く作成します。ワークシートを画像としてエクスポートし、C#
  でプレゼンテーションを PPTX として保存する方法を学びましょう。
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export worksheet as image
- save presentation as pptx
- export excel chart as picture
language: ja
og_description: Aspose を使用して C# で Excel から PowerPoint を作成します。ワークシートを画像としてエクスポートし、シェイプは編集可能なままにして、結果を
  PPTX として保存します。
og_title: ExcelからPowerPointを作成 – 完全C#チュートリアル
tags:
- Aspose
- C#
- Office Automation
title: Excel から PowerPoint を作成する – ステップバイステップ C# ガイド
url: /ja/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel から PowerPoint を作成 – 完全 C# チュートリアル

Excel から PowerPoint を作成する必要があったが、どのライブラリがチャートを編集可能なままにできるか分からなかったことはありませんか？ あなたは一人ではありません。多くのレポートシナリオでは、スプレッドシートをスライドデッキに変換し、後でテキストボックスを調整できる機能を失いたくありません。このガイドでは、Aspose.Cells と Aspose.Slides を使用して **Excel を PowerPoint に変換** を正確に行う方法を示し、さらに **ワークシートを画像としてエクスポート** と最終的に **プレゼンテーションを PPTX として保存** についてもカバーします。

コードの各行を順に解説し、各設定がなぜ重要かを説明します。また、ワークブックに複雑なチャートが含まれていて、画像としてエクスポートしたい場合の対処法も議論します。最後までに、`ShapesDemo.xlsx` を受け取り `Result.pptx` を出力する、すぐに実行できる C# コンソールアプリが手に入ります – すべて編集可能なテキストボックスと鮮明な画像が保持されます。

## 必要なもの

- .NET 6.0 以降 (API は .NET Framework でも動作しますが、.NET 6 が最適です)。  
- **Aspose.Cells** と **Aspose.Slides** の NuGet パッケージ (無料トライアル ライセンスでテスト可能)。  
- C# の構文に基本的に慣れていること – `Console.WriteLine` が書ければ問題ありません。  

追加の COM インタープロ、サーバーに Office をインストールする必要はなく、画像の手動コピー＆ペーストも不要です。すべてプログラムで処理されます。

---

## Excel から PowerPoint を作成 – ワークブックの読み込みとエクスポートオプションの設定

最初に行うのは Excel ファイルを開き、Aspose.Cells にシートの描画方法を指示することです。`ImageOrPrintOptions` オブジェクトが魔法の場所で、`ExportShapes` と `ExportEditableTextBoxes` を有効にすることで、すべてのシェイプ（チャートを含む）がスライドの一部となり、変換後も編集可能なままになります。

```csharp
using Aspose.Cells;
using Aspose.Slides;

// 1️⃣ Load the Excel workbook
string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
Workbook workbook = new Workbook(excelPath);
Worksheet worksheet = workbook.Worksheets[0];   // Grab the first sheet

// 2️⃣ Configure image export – keep shapes editable
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    OnePagePerSheet = true,          // Export the whole sheet as one slide
    ExportShapes = true,             // Include shapes (charts, drawings)
    ExportEditableTextBoxes = true   // Make text boxes editable in PPTX
};
```

**これらのフラグの理由は？**  
- `OnePagePerSheet` はシートが複数のスライドに分割されるのを防ぎ、単一のフルサイズ画像を取得します。  
- `ExportShapes` は Aspose.Cells にチャートとベクターシェイプをラスタライズさせ、外観を保持します。  
- `ExportEditableTextBoxes` は、PowerPoint でテキストボックスをダブルクリックして、Excel を再度開かずにテキストを編集できる秘密の要素です。  

> **プロのコツ:** チャートの静的画像だけが必要な場合は `ExportShapes = false` に設定し、後で `ExportExcelChartAsPicture` メソッドを使用してください（最終セクション参照）。

---

## Excel を PowerPoint に変換 – ワークシートから画像を生成

オプションが準備できたら、ワークシートを `System.Drawing.Image` に変換します。`WorksheetToImageConverter` が重い処理を担当し、先ほど定義した設定を適用します。

```csharp
// 3️⃣ Convert the worksheet to an image using the options above
WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
System.Drawing.Image sheetImage = converter.ConvertToImage(0, imageOptions);
```

`0` 引数は最初のページを示します（`OnePagePerSheet` のためページは1枚だけです）。結果として得られる `sheetImage` は元の DPI を保持するので、高解像度ディスプレイでもスライドがピクセル化しません。

---

## プレゼンテーションを PPTX として保存 – スライドに画像を挿入

ここで新しい PowerPoint ファイルを作成し、スライドを追加してビットマップを貼り付けます。Aspose.Slides は画像を *ピクチャーフレーム* シェイプとして扱うため、後で任意の PowerPoint オブジェクトと同様にサイズ変更や移動が可能です。

```csharp
// 4️⃣ Create a new PowerPoint presentation
Presentation presentation = new Presentation();
ISlide slide = presentation.Slides[0];   // The default blank slide

// Add the Excel‑derived image as a picture frame
slide.Shapes.AddPictureFrame(
    ShapeType.Rectangle,                 // Simple rectangle container
    0, 0,                                // Top‑left corner (0,0)
    sheetImage.Width,                    // Width of the picture
    sheetImage.Height,                   // Height of the picture
    sheetImage);                         // The bitmap we generated
```

> **画像がスライドサイズより大きい場合は？**  
> PowerPoint はスライドの寸法を超える部分を自動的にクリップします。簡単な対策は、挿入前に画像をスケーリングすることです：

```csharp
float scale = Math.Min(presentation.SlideSize.Size.Width / (float)sheetImage.Width,
                       presentation.SlideSize.Size.Height / (float)sheetImage.Height);
int newWidth  = (int)(sheetImage.Width * scale);
int newHeight = (int)(sheetImage.Height * scale);
```

その後、`newWidth` と `newHeight` を `AddPictureFrame` に渡すことができます。

---

## ワークシートを画像としてエクスポート – PPTX ファイルを保存

最後にプレゼンテーションをディスクに保存します。`SaveFormat.Pptx` フラグは最新の OpenXML 形式を保証し、すべての最近の PowerPoint バージョンで動作します。

```csharp
// 5️⃣ Save the presentation as a PPTX file
string pptxPath = "YOUR_DIRECTORY/Result.pptx";
presentation.Save(pptxPath, SaveFormat.Pptx);
```

`Result.pptx` を開くと、Excel シートと全く同じ外観の単一スライドが表示されますが、任意のテキストボックスをクリックして PowerPoint 上で直接内容を編集できます。

---

## Excel のチャートを画像としてエクスポート – ラスタ画像が好まれる場合

場合によっては編集可能なシェイプは不要で、チャートの高品質 PNG だけで十分なことがあります。Aspose.Cells はシート全体を変換せずに特定のチャートを画像としてエクスポートできます：

```csharp
// Example: Export the first chart on the sheet as a PNG
int chartIndex = 0; // Adjust if you have multiple charts
Chart chart = worksheet.Charts[chartIndex];
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    OnePagePerSheet = false
};
chart.ToImage("chart.png", chartOptions);
```

その後、`chart.png` を `sheetImage` を追加したのと同様にスライドに埋め込むことができます。この方法は PPTX ファイルサイズを削減し、スライドに周囲のデータが不要な場合に有用です。

---

## よくある落とし穴と回避策

| 問題 | 発生理由 | 対策 |
|------|----------|------|
| **テキストがぼやける** | 低 DPI（デフォルト 96）でエクスポートされたため。 | `imageOptions.Dpi = 300;` を変換前に設定します。 |
| **シェイプが消える** | `ExportShapes` が `false` のままになっているため。 | 編集可能なグラフィックが必要な場合は `ExportShapes = true` にしてください。 |
| **スライドサイズの不一致** | 画像がスライドの寸法より大きい。 | 画像をスケーリング（コードスニペット参照）するか、`presentation.SlideSize` でスライドサイズを変更します。 |
| **ライセンス例外** | 適切にアクティベートされていないトライアル版を使用しているため。 | `Main` の冒頭で `License license = new License(); license.SetLicense("Aspose.Total.lic");` を呼び出します。 |

---

## 完全動作例（コピー＆ペースト可能）

以下は全プログラムです。新しいコンソールプロジェクトに貼り付けてすぐに使用できます。`YOUR_DIRECTORY` を Excel ファイルが格納されているフォルダーに置き換えてください。

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;
using System.Drawing;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook
            // -----------------------------------------------------------------
            string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
            Workbook workbook = new Workbook(excelPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -----------------------------------------------------------------
            // 2️⃣ Set up export options – keep shapes editable
            // -----------------------------------------------------------------
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                OnePagePerSheet = true,
                ExportShapes = true,
                ExportEditableTextBoxes = true,
                Dpi = 300                 // High‑resolution output
            };

            // -----------------------------------------------------------------
            // 3️⃣ Convert worksheet to an image
            // -----------------------------------------------------------------
            WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
            Image sheetImage = converter.ConvertToImage(0, imageOptions);

            // -----------------------------------------------------------------
            // 4️⃣ Create PowerPoint and add the image as a slide
            // -----------------------------------------------------------------
            Presentation presentation = new Presentation();
            ISlide slide = presentation.Slides[0];
            slide.Shapes.AddPictureFrame(
                ShapeType.Rectangle,
                0, 0,
                sheetImage.Width,
                sheetImage.Height,
                sheetImage);

            // -----------------------------------------------------------------
            // 5️⃣ Save the PPTX file
            // -----------------------------------------------------------------
            string pptxPath = "YOUR_DIRECTORY/Result.pptx";
            presentation.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine("✅ PowerPoint created successfully at: " + pptxPath);
        }
    }
}
```

**期待される出力:**  
プログラムを実行すると `✅ PowerPoint created successfully at: YOUR_DIRECTORY/Result.pptx` が表示されます。PPTX を開くと、元の Excel シートを鏡像した単一スライドが表示され、テキストボックスは編集可能です。

---

## まとめと次のステップ

これで、Aspose の強力な API を使用して **Excel から PowerPoint を作成** する方法、**ワークシートを画像としてエクスポート** する方法、そして **プレゼンテーションを PPTX として保存** しながら編集可能性を保持する方法が分かりました。同じパターンは複数シートのブックでも機能します – `workbook.Worksheets` をループし、各シートごとに新しいスライドを追加するだけです。

**次に探求すべきことは？**  

- **バッチ変換:** フォルダー内の Excel ファイルをループし、ファイルごとにスライドデッキを生成します。  
- **動的レイアウト:** `slide.LayoutSlide` を使用して事前にデザインされた PowerPoint テンプレートを適用します。  
- **チャートのみエクスポート:** “Export Excel chart as picture” スニペットとスライドプレースホルダーを組み合わせて、より軽量なデッキを作ります。  
- **高度なスタイリング:** Aspose.Slides を使ってカスタムスライド背景、トランジション、アニメーションを適用します。  

自由に試してみてください—DPI を変更したり、`ShapeType.Ellipse` を円形のピクチャーフレームに置き換えたり、スライドに複数の画像を埋め込んだりできます。プログラムで制御できる限り、可能性は無限です。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}