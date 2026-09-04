---
category: general
date: 2026-02-21
description: Excel から PowerPoint を素早く作成します。数行の C# コードで Aspose.Cells を使用し、編集可能なテキストとチャートを含む
  Excel から PowerPoint へのエクスポート方法を学びましょう。
draft: false
keywords:
- create powerpoint from excel
- export excel to powerpoint
- export editable text
- export excel chart powerpoint
- convert excel chart powerpoint
language: ja
og_description: 編集可能なテキストとチャートを含むExcelからPowerPointを作成します。Aspose.Cells を使用して Excel
  を PowerPoint にエクスポートする詳細ガイドをご覧ください。
og_title: ExcelからPowerPointを作成する – ステップバイステップ C# ガイド
tags:
- C#
- Aspose.Cells
- PowerPoint
- Excel Automation
title: ExcelからPowerPointを作成する – 完全C#チュートリアル
url: /ja/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-complete-c-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel から PowerPoint を作成 – 完全 C# チュートリアル

**Excel から PowerPoint を作成**したいけど、どの API を使えばいいか分からないことはありませんか？ 同じ悩みを抱える開発者は多いです。データが豊富なワークシートを洗練されたスライドデッキに変換したいとき、特に変換後もテキストボックスを編集可能にしたい場合は壁にぶつかりがちです。

このガイドでは、**Excel を PowerPoint にエクスポート**し、テキストの編集可能性、チャートの忠実度、レイアウトをすべて保持しながら、数行の C# で実現する方法を紹介します。最後には、手動で作成したスライドと同様に PowerPoint で調整できる PPTX ファイルが手に入ります。

## 学べること

- チャートやシェイプを含む Excel ワークブックの読み込み方法  
- テキストボックスを編集可能に保つための `PresentationExportOptions` の設定方法（`export editable text`）  
- 実際に **Excel chart PowerPoint** をエクスポートしてクリーンなスライドデッキを取得する手順  
- ページ設定や複数シートに対応した **convert Excel chart PowerPoint** の小さなバリエーション  

### 前提条件

- .NET 開発環境（Visual Studio 2022 以降）  
- Aspose.Cells for .NET（無料トライアルまたはライセンス版）  
- 少なくとも 1 つのチャートと、編集可能にしたいシェイプを含む Excel ファイル（`ChartWithShape.xlsx`）  

これらが揃っていれば、余計な説明は省き、実用的で実行可能なソリューションにすぐ取り掛かれます。

## Excel から PowerPoint を作成 – 手順別ガイド

各ステップの下に簡潔なコードスニペットを掲載し、**なぜ**その処理が必要かを解説します。ページ下部の完全サンプルもそのままコピーして使用できます。

### 手順 1: Excel ワークブックを読み込む

まず、ソースとなるワークブックをメモリにロードします。Aspose.Cells がファイルを読み取り、操作可能なリッチなオブジェクトモデルを構築します。

```csharp
// Step 1: Load the Excel workbook that contains the chart and shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");

// Quick sanity check – make sure the workbook actually loaded
if (workbook.Worksheets.Count == 0)
    throw new InvalidOperationException("The workbook appears to be empty.");
```

**重要ポイント:**  
ワークブックの読み込みは土台です。ファイルパスが間違っている、またはブックが破損していると、以降の `export excel to powerpoint` 手順はすべて失敗します。早期にエラーを検出できるサニティチェックは、後で「ファイルが見つかりません」などの曖昧なエラーになるのを防ぎます。

### 手順 2: エクスポートオプションを準備する

Aspose.Cells では `PresentationExportOptions` オブジェクトで PPTX の外観を制御できます。ここでテキストを編集可能にしたいかどうかを決めます。

```csharp
// Step 2: Create export options for PowerPoint conversion
PresentationExportOptions exportOptions = new PresentationExportOptions();

// Optional: tweak the slide size (default is 10in x 7.5in)
exportOptions.SlideSize = new SizeF(10, 7.5f);
```

**重要ポイント:**  
`PresentationExportOptions` を設定しないと、ライブラリは既定値を使用します。既定値は社内スライドテンプレートと合わないことがあるため、スライドサイズを事前に調整しておくと、後から手動でリサイズする手間が省けます。

### 手順 3: 編集可能なテキストボックスを有効化する

フラグ `ExportEditableTextBoxes` をオンにすると、Aspose.Cells はテキストシェイプを PowerPoint のテキストボックスとして保持し、画像化しません。

```csharp
// Step 3: Enable editability of text boxes in the resulting presentation
exportOptions.ExportEditableTextBoxes = true;
```

**重要ポイント:**  
この行を省略すると、生成された PPTX はテキストがラスタ画像化され、PowerPoint 上でラベルやキャプションを編集できなくなります。`export editable text` を設定することが、再利用可能なスライドデッキを作る鍵です。

### 手順 4: ワークシートを PPTX にエクスポートする

いよいよ PPTX ファイルを書き出します。任意のワークシートを選択できますが、ここでは最初のシート（`Worksheets[0]`）を使用します。

```csharp
// Step 4: Export the first worksheet's page setup to a PPTX file
workbook.Worksheets[0].PageSetup.SaveToPptx("YOUR_DIRECTORY/Result.pptx", exportOptions);
```

**重要ポイント:**  
`SaveToPptx` は Excel で設定したページ設定（余白、向き）を尊重するため、スライドは既にデザインしたレイアウトと一致します。これが **export excel chart powerpoint** の核心です。

### 手順 5: 出力結果を確認する（任意だが推奨）

変換後、生成された `Result.pptx` を PowerPoint で開き、次の点をチェックします。

1. チャートが鮮明でデータ系列が保持されているか  
2. テキストボックスが選択可能で編集できるか  
3. スライドサイズが期待通りか  

問題がある場合は `exportOptions` を見直します。たとえば、名前付き印刷領域を尊重したい場合は `exportOptions.IncludePrintArea = true` を設定します。

```csharp
// Optional: open the PPTX automatically (requires System.Diagnostics)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/Result.pptx",
    UseShellExecute = true
});
```

### 手順 6: 応用バリエーション（複数シートのエクスポート）

複数のワークシートを一括で **convert excel chart powerpoint** したいことがよくあります。コレクションをループし、各スライドに固有の名前を付けます。

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outputPath = $"YOUR_DIRECTORY/Result_Sheet{i + 1}.pptx";
    workbook.Worksheets[i].PageSetup.SaveToPptx(outputPath, exportOptions);
}
```

**プロのコツ:** すべてのシートを *単一* の PPTX にまとめたい場合は、新しい `Presentation` オブジェクトを作成し、各スライドをインポートしてから一度だけ保存します。手間は増えますが、ファイル管理が楽になります。

## 完全動作サンプル

以下はコンソールアプリに貼り付けてすぐに実行できる、全体プログラムです。

```csharp
using System;
using System.Drawing;
using Aspose.Cells;
using Aspose.Cells.Export;

class Program
{
    static void Main()
    {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");
        if (workbook.Worksheets.Count == 0)
        {
            Console.WriteLine("Workbook is empty – aborting.");
            return;
        }

        // 2️⃣ Set up export options
        PresentationExportOptions exportOptions = new PresentationExportOptions
        {
            SlideSize = new SizeF(10, 7.5f),          // optional custom size
            ExportEditableTextBoxes = true           // <‑‑ keep text boxes editable
        };

        // 3️⃣ Export first worksheet
        string outputPath = "YOUR_DIRECTORY/Result.pptx";
        workbook.Worksheets[0].PageSetup.SaveToPptx(outputPath, exportOptions);
        Console.WriteLine($"PowerPoint created at: {outputPath}");

        // 4️⃣ Open the result automatically (Windows only)
        try
        {
            System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
            {
                FileName = outputPath,
                UseShellExecute = true
            });
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Could not open PPTX automatically: {ex.Message}");
        }
    }
}
```

**期待される結果:**  
`Result.pptx` を開くと、Excel ワークシートのレイアウトをそのまま映したスライドが表示されます。Excel に配置したチャートはネイティブな PowerPoint チャートとして、シェイプとして追加したキャプションは完全に編集可能なテキストボックスになります。

## よくある質問とエッジケース

- **マクロ有効ブック（`.xlsm`）でも動作しますか？**  
  はい。Aspose.Cells はマクロを読み取りますが実行はしません。変換プロセスは VBA を無視するため、ビジュアルコンテンツは取得できます。

- **ワークシートに複数のチャートがある場合は？**  
  すべての表示チャートが同一スライドに転送されます。チャートごとに別スライドが必要な場合は、シートを分割するか、手順 6 のループを活用してください。

- **カスタム PowerPoint テーマを保持できますか？**  
  エクスポート時に直接は保持できません。変換後に PowerPoint でテーマを適用するか、Aspose.Slides を使ってプログラム的に適用してください。

- **特定の範囲だけをエクスポートしたい場合は？**  
  Excel で名前付き印刷領域を設定（`ページレイアウト → 印刷範囲`）し、`exportOptions.IncludePrintArea = true` を有効にします。

## まとめ

Aspose.Cells を使って **Excel から PowerPoint を作成**する方法と、編集可能テキスト、チャートの忠実度、スライドサイズをフルコントロールする手順を習得しました。提示した短いコードスニペットは最も一般的なシナリオに対応し、追加のヒントで **export excel to powerpoint** を複数シートやカスタムレイアウトに拡張できます。

次のステップに挑戦したいですか？この手法と **Aspose.Slides** を組み合わせて、トランジションやスピーカーノートの自動追加、あるいは生成したスライドを大規模プレゼンテーションに埋め込むことも可能です。あるいは、ワークブック全体をマルチスライドデッキに変換して、レポート自動化パイプラインに活用してみてください。

質問や便利なカスタマイズ方法があれば、下のコメント欄でシェアしてください。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}