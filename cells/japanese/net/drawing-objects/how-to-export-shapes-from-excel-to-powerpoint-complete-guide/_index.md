---
category: general
date: 2026-07-26
description: Excel のワークシートから PowerPoint へシェイプを数ステップでエクスポートする方法 – 開発者向けの簡単な Excel から
  PPTX へのエクスポートチュートリアル
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export shapes
- convert worksheet to powerpoint
- export excel to pptx
- excel to powerpoint tutorial
- export excel workbook powerpoint
language: ja
lastmod: 2026-07-26
og_description: Excel のシェイプを PowerPoint にエクスポートする手順をステップバイステップで解説。エクスポート Excel から
  PPTX へのチュートリアルに従い、ワークシートが編集可能なスライドに変わる様子をご覧ください。
og_image_alt: Screenshot showing how to export shapes from Excel to PowerPoint using
  Aspose.Cells
og_title: ExcelからPowerPointへ図形をエクスポートする方法 – 簡単・高速
schemas:
- author: Aspose
  dateModified: '2026-07-26'
  description: How to export shapes from an Excel worksheet to PowerPoint in just
    a few steps – a quick export excel to pptx tutorial for developers.
  headline: How to Export Shapes from Excel to PowerPoint – Complete Guide
  type: TechArticle
- description: How to export shapes from an Excel worksheet to PowerPoint in just
    a few steps – a quick export excel to pptx tutorial for developers.
  name: How to Export Shapes from Excel to PowerPoint – Complete Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - A valid
      license for **Aspose.Cells for .NET** (the free trial works for testing). -
      An Excel workbook (e.g., `ShapesDemo.xlsx`) that contains at least one text
      box or shape. - A development environment—Visual Studio, Rider, or VS Co'
  - name: Multiple Worksheets
    text: If you need to export several sheets into a single PPTX, loop through `workbook.Worksheets`
      and call `worksheet.Save` with the same `pptxOptions`. Aspose.Cells will automatically
      add a new slide for each sheet.
  - name: Custom Slide Layouts
    text: You can specify `pptxOptions.SlideSize` (e.g., `SlideSizeType.Widescreen`)
      to match your corporate deck dimensions.
  - name: Missing Files or Permissions
    text: 'Wrap the whole `Main` method in a `try` block:'
  type: HowTo
- questions:
  - answer: Yes. `Workbook` can open `.xls`, `.xlsx`, and even CSV files. The shape
      export works the same way.
    question: Does this work with older Excel formats (.xls)?
  - answer: Charts are already exported as native PowerPoint charts; you don’t need
      extra flags.
    question: What if I need to keep charts editable?
  - answer: Absolutely—just replace `SaveFormat.Pptx` with `SaveFormat.Pdf` and omit
      the `PptxSaveOptions`.
    question: Can I export to PDF instead of PPTX?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Office Automation
title: ExcelからPowerPointへ図形をエクスポートする方法 – 完全ガイド
url: /ja/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel から PowerPoint へシェイプをエクスポートする方法 – 完全ガイド

Excel ファイルから **シェイプをエクスポート** し、PowerPoint のスライドで編集可能なままにしたいと考えたことはありませんか？ あなただけではありません。レポート パイプラインを構築している場合でも、スプレッドシートをプレゼンテーションに素早く変換したいだけの場合でも、**worksheet を PowerPoint に変換** してシェイプの編集可能性を失わないことは、手作業の時間を何時間も節約できます。

この **excel to powerpoint tutorial** では、ワークブックを読み込み、適切なエクスポート オプションを設定し、テキスト ボックスやその他の描画オブジェクトが編集可能なまま PPTX ファイルに書き出す完全に動作する C# のサンプルを順を追って解説します。曖昧な説明はありません—そのままコピーして貼り付け、すぐに実行できるコードだけをご紹介します。

## 学べること

- **excel を pptx にエクスポート** しながらシェイプの編集可能性を保持する正確な手順。  
- `Aspose.Cells` ライブラリの `PptxSaveOptions` がエクスポート動作をどのように制御するか。  
- 複数シートの取り扱い、ファイルが見つからない場合、カスタム シェイプ設定のコツ。  
- 任意の .NET プロジェクトに組み込める、完全に実行可能なプログラム。

### 前提条件

- .NET 6.0 以降（コードは .NET Framework 4.7+ でも動作します）。  
- **Aspose.Cells for .NET** の有効なライセンス（無料トライアルでテスト可能）。  
- 少なくとも 1 つのテキスト ボックスまたはシェイプが含まれる Excel ワークブック（例: `ShapesDemo.xlsx`）。  
- 開発環境—Visual Studio、Rider、または VS Code のいずれか。

これらが揃ったら、さっそく始めましょう。

## 手順 1: ワークブックの読み込み – シェイプをエクスポートするための出発点  

まず、編集可能にしたいシェイプが入っている Excel ファイルを開く必要があります。

```csharp
using Aspose.Cells;
using System;

class ExportEditableShapes
{
    static void Main()
    {
        // Load the Excel workbook that contains text boxes and other shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesDemo.xlsx");
        Worksheet worksheet = workbook.Worksheets[0];
```

**重要ポイント:**  
`Workbook` オブジェクトは、ファイル内のすべてのセル、チャート、描画オブジェクトへのゲートウェイです。最初のワークシート（`Worksheets[0]`）を取得することで既知のシートで作業できますが、特定のタブが必要な場合はインデックスの代わりに名前（`workbook.Worksheets["Sheet2"]`）を指定しても構いません。

> **プロのコツ:** 読み込み呼び出しを `try / catch` ブロックでラップし、ファイル パスが間違っている場合にフレンドリーなエラーメッセージを表示させましょう。

## 手順 2: PPTX エクスポート オプションの設定 – シェイプをエクスポートするコア  

次に、Aspose.Cells に対して結果の PPTX でシェイプを編集可能にするよう指示します。

```csharp
        // Configure PPTX export options to keep shapes editable
        var pptxOptions = new Aspose.Cells.Export.PptxSaveOptions
        {
            ExportEditableTextBoxes = true, // makes text boxes editable in the PPTX
            ExportEditableShapes = true     // makes other shapes editable in the PPTX
        };
```

**これらのフラグの意味は？**  
- `ExportEditableTextBoxes` は Excel のテキスト ボックスを PowerPoint のテキスト プレースホルダーに変換し、ダブルクリックで編集可能にします。  
- `ExportEditableShapes` は矢印、矩形、SmartArt などのシェイプにも同様の処理を行います。これらのフラグが無いと、オブジェクトは静的画像になり、**worksheet を PowerPoint に変換** する目的が失われます。

`PptxSaveOptions` ではスライドサイズ、テーマ、フォント埋め込みの有無なども調整でき、企業のブランディングに合わせたプレゼンテーション作成に便利です。

## 手順 3: ワークシートを PPTX として保存 – Excel ワークブックを PowerPoint にエクスポートする最終ステップ  

オプション設定が完了したら、保存はシンプルです。

```csharp
        // Save the worksheet as a PPTX file with the editable shapes option
        worksheet.Save("YOUR_DIRECTORY/ShapesEditable.pptx", SaveFormat.Pptx, pptxOptions);
```

**内部で何が起きているか:**  
Aspose.Cells はシート上のすべての描画オブジェクトを走査し、対応する PowerPoint のシェイプ クラスにマッピングして XML を生成します。編集可能フラグを有効にしているため、XML は各シェイプを `Picture` ではなく `Shape` としてマークし、PowerPoint はそれをライブ オブジェクトとして扱います。

## 手順 4: エクスポートの確認 – ユーザーへの簡易フィードバック  

小さなコンソール メッセージで処理が成功したことを知らせます。

```csharp
        // Inform the user that the export is complete
        Console.WriteLine("Exported worksheet with editable shapes.");
    }
}
```

プログラムを実行してメッセージが表示されたら、`ShapesEditable.pptx` を PowerPoint で開きます。テキスト ボックスをクリックすると直接テキストを編集でき、シェイプをドラッグするとネイティブの PowerPoint オブジェクトと同様に移動します。

## 手順 5: 実務でのシナリオ対応  

以下は **excel to powerpoint tutorial** 作成時に遭遇しやすいバリエーションです。

### 複数シートのエクスポート

複数のシートを 1 つの PPTX にエクスポートしたい場合は、`workbook.Worksheets` をループし、同じ `pptxOptions` を使って `worksheet.Save` を呼び出します。Aspose.Cells は自動的にシートごとに新しいスライドを追加します。

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.Save($"YOUR_DIRECTORY/{ws.Name}.pptx", SaveFormat.Pptx, pptxOptions);
}
```

### カスタム スライド レイアウト

`pptxOptions.SlideSize`（例: `SlideSizeType.Widescreen`）を指定して、企業のデッキサイズに合わせることができます。

```csharp
pptxOptions.SlideSize = SlideSizeType.Widescreen;
```

### ファイルが見つからない、または権限がない場合

`Main` メソッド全体を `try` ブロックでラップします:

```csharp
try
{
    // ... existing code ...
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error: {ex.Message}");
}
```

これにより、**export excel workbook powerpoint** プロセスが本番パイプラインでも堅牢になります。

## 完全動作サンプル

以下が今すぐコンパイルできる完全プログラムです。`ExportEditableShapes.cs` として保存し、ファイル パスを調整した上で `dotnet run` を実行してください。

```csharp
using Aspose.Cells;
using System;

class ExportEditableShapes
{
    static void Main()
    {
        try
        {
            // Step 1: Load the Excel workbook that contains text boxes and other shapes
            Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesDemo.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 2: Configure PPTX export options to keep shapes editable
            var pptxOptions = new Aspose.Cells.Export.PptxSaveOptions
            {
                ExportEditableTextBoxes = true, // makes text boxes editable in the PPTX
                ExportEditableShapes = true,    // makes other shapes editable in the PPTX
                SlideSize = SlideSizeType.Widescreen // optional: set slide size
            };

            // Step 3: Save the worksheet as a PPTX file with the editable shapes option
            worksheet.Save("YOUR_DIRECTORY/ShapesEditable.pptx", SaveFormat.Pptx, pptxOptions);

            // Step 4: Inform the user that the export is complete
            Console.WriteLine("Exported worksheet with editable shapes.");
        }
        catch (Exception ex)
        {
            // Step 5: Handle errors gracefully
            Console.Error.WriteLine($"Export failed: {ex.Message}");
        }
    }
}
```

**プログラム実行時の期待出力:**

```
Exported worksheet with editable shapes.
```

生成された `ShapesEditable.pptx` を開くと、Excel の各シェイプが完全に編集可能な PowerPoint オブジェクトとして表示されます—**how to export shapes** を検索したときに期待した通りの結果です。

## よくある質問

- **古い Excel 形式（.xls）でも動作しますか？**  
  はい。`Workbook` は `.xls`、`.xlsx`、さらには CSV ファイルも開くことができ、シェイプのエクスポートは同様に機能します。

- **チャートも編集可能にしたい場合は？**  
  チャートはすでにネイティブの PowerPoint チャートとしてエクスポートされるため、追加のフラグは不要です。

- **PPTX ではなく PDF にエクスポートしたい場合は？**  
  簡単です—`SaveFormat.Pptx` を `SaveFormat.Pdf` に置き換え、`PptxSaveOptions` を省略すれば完了です。

## 結論

これで **how to export shapes** を使って Excel から編集可能な PowerPoint デッキへシェイプをエクスポートする、エンドツーエンドの解決策が手に入りました。`Aspose.Cells` の `PptxSaveOptions` を活用すれば、すべてのテキスト ボックスと描画オブジェクトを保持したまま、静的なスプレッドシートを動的なプレゼンテーションに変換できます。

次のステップに挑戦してみませんか？ カスタム スライド マスターの追加、プログラムでの画像挿入、あるいは CI/CD パイプラインに組み込んで週次の売上デッキを自動生成するなど、**export excel workbook powerpoint** の世界は無限に広がっています—ぜひ探検してみてください！

--- 

*この **excel to powerpoint tutorial** が役に立ったら、GitHub でスターを付けるか、スプレッドシートをスライドにコピペしている同僚と共有してください。ハッピーコーディング！*

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックをカバーしています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、API の追加機能をマスターしたり、別の実装アプローチを自分のプロジェクトで試したりするのに役立ちます。

- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [How to Export Excel Cells as Images Using Aspose.Cells for Java](/cells/english/java/import-export/export-excel-cells-as-image-aspose-cells-java/)
- [How to Export Excel Charts as SVG Using Aspose.Cells Java for Scalable Vector Graphics](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}