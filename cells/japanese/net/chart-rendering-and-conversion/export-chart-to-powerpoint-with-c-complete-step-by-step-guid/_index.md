---
category: general
date: 2026-02-26
description: C# を使用して Excel から PowerPoint にチャートをエクスポートする。Excel を PowerPoint に変換する方法、Excel
  を PowerPoint として保存する方法、そして図形を編集可能なままに保つ方法を学びましょう。
draft: false
keywords:
- export chart to powerpoint
- convert excel to powerpoint
- save excel as powerpoint
- how to convert excel to ppt
- save workbook as pptx
language: ja
og_description: C# を使用して Excel から PowerPoint へチャートをエクスポートします。このガイドでは、Excel を PowerPoint
  に変換し、ブックを PPTX として保存し、図形を編集可能なままにする方法を示します。
og_title: C#でチャートをPowerPointにエクスポート – 完全プログラミングチュートリアル
tags:
- Aspose.Cells
- C#
- Office Automation
title: C#でチャートをPowerPointにエクスポートする – 完全ステップバイステップガイド
url: /ja/net/chart-rendering-and-conversion/export-chart-to-powerpoint-with-c-complete-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Chart to PowerPoint – Complete Programming Tutorial

**PowerPoint にチャートをエクスポート** しても編集可能な状態を保ちたいと思ったことはありませんか？多くのレポートシナリオでは、スライドデッキ内にライブチャートが必要ですが、手動でコピー＆ペーストするのは手間です。実は、C# の数行でプログラム的に実現できます。

このガイドでは、チャートとテキストボックスを含む Excel ワークブックの読み込み、テキストボックスやシェイプを編集可能なままエクスポートする設定、そして最終的に **PowerPoint** ファイルとして保存するまでの全工程を解説します。最後まで読むと、**Excel を PowerPoint に変換**、**Excel を PowerPoint として保存**、さらにはエッジケース向けのオプション調整方法もマスターできます。

## What You’ll Need

- **Aspose.Cells for .NET**（バージョン 23.10 以降）。変換をシンプルにしてくれるライブラリです。
- **.NET 6+** ランタイム – 最近の SDK であればどれでも可。
- シンプルな Excel ファイル（`ChartWithTextbox.xlsx`） – 少なくとも 1 つのチャートとテキストボックスが含まれていること。
- Visual Studio もしくはお好みの IDE。

追加の NuGet パッケージは Aspose.Cells 以外不要ですが、C# の基本構文が分かっているとスムーズです。

## Export Chart to PowerPoint – Step‑by‑Step

以下では、解決策を段階的に分解して説明します。各ステップには必要なコードと、なぜそのコードが必要かを説明する短い「why」パラグラフを添えています。

### Step 1: Load the Excel Workbook That Holds the Chart

まず、ソースファイルをメモリに読み込みます。Aspose.Cells の `Workbook` を使うと、チャート、画像、埋め込みオブジェクトをすべて含めてスプレッドシート全体を読み取れます。

```csharp
using Aspose.Cells;

// Step 1: Load the Excel workbook that contains the chart with a textbox
Workbook workbook = new Workbook(@"C:\Samples\ChartWithTextbox.xlsx");

// Verify that the workbook actually contains a chart
if (workbook.Worksheets[0].Charts.Count == 0)
{
    throw new InvalidOperationException("No chart found in the first worksheet.");
}
```

*Why this matters:* パスを正しく指定せずにワークブックを開くと `FileNotFoundException` が発生します。簡単なサニティチェックを入れることで、後で空のスライドをエクスポートしてしまうミスを防げます。

### Step 2: Prepare Presentation Options to Keep Shapes Editable

Aspose.Cells では、エクスポート後にテキストボックス、シェイプ、さらにはチャート自体を **編集可能** に保つかどうかを設定できます。`ExportTextBoxes` と `ExportShapes` を `true` にすると、これらのオブジェクトが静的画像ではなく PowerPoint のネイティブ要素として保持されます。

```csharp
using Aspose.Cells.Drawing;

// Step 2: Set up presentation options to keep textboxes and shapes editable in the output
PresentationOptions presentationOptions = new PresentationOptions
{
    ExportTextBoxes = true, // Preserve editable textboxes
    ExportShapes    = true  // Preserve shapes such as the chart itself
};
```

*Why this matters:* これらのフラグをデフォルト（`false`）のままにすると、結果のスライドはチャートのビットマップ画像になり、シリーズの編集やキャプションの変更が不可能になります。両方のオプションを有効にすれば、手動で作成したものと同等の本物の PowerPoint チャートが得られます。

### Step 3: Convert Excel to PowerPoint and Save the File

ここで `Save` メソッドを呼び出し、`SaveFormat.Pptx` 列挙体と先ほど設定したオプションを渡します。ライブラリが Excel のチャートオブジェクトを PowerPoint のチャートシェイプへ変換してくれます。

```csharp
// Step 3: Save the workbook as a PowerPoint presentation using the configured options
workbook.Save(@"C:\Samples\Result.pptx", SaveFormat.Pptx, presentationOptions);
```

*Why this matters:* `Save` 呼び出しがすべての重い処理を担います—Excel のシリーズを PowerPoint のシリーズにマッピングし、軸の書式を保持し、リンクされたテキストボックスもコピーします。この行が実行されると、Microsoft PowerPoint で開ける完全に編集可能な `.pptx` ファイルが生成されます。

### Verify the Result

PowerPoint で `Result.pptx` を開きます。スライドには以下が表示されるはずです：

- 元のチャートがデータにリンクされたまま（ダブルクリックでシリーズを編集可能）。
- Excel シートにあったテキストボックスが、PowerPoint のネイティブテキストボックスとして表示。
- スライドレイアウトは自動的に選択されます（通常は空白スライド）。

要素が欠けている場合は、元のワークブックに可視オブジェクトが存在したか、`ExportTextBoxes` / `ExportShapes` が `true` に設定されているかを再確認してください。

### Convert Excel to PowerPoint: Handling Multiple Worksheets

ワークブックに複数のシートがあり、それぞれにチャートがあるケースがよくあります。デフォルトでは Aspose.Cells が **すべてのシートのすべてのチャート** を個別のスライドにエクスポートします。特定のチャートだけが必要な場合は、保存前にフィルタリングできます。

```csharp
// Example: Export only charts from the first worksheet
Worksheet firstSheet = workbook.Worksheets[0];
foreach (Chart chart in firstSheet.Charts)
{
    chart.IsVisible = true; // Ensure visibility
}

// Hide charts from other sheets
for (int i = 1; i < workbook.Worksheets.Count; i++)
{
    foreach (Chart chart in workbook.Worksheets[i].Charts)
    {
        chart.IsVisible = false;
    }
}
```

*Pro tip:* `chart.IsVisible = false` に設定すると、チャートを完全に削除するよりもコストが低く、ソースファイルを変更せずに含めるか除外するかを切り替えられます。

### Save Excel as PowerPoint – Customizing Slide Size

PowerPoint のデフォルトスライドサイズは 10 インチ × 5.63 インチです。チャートが窮屈に見える場合は、`PresentationOptions` オブジェクトでスライド寸法を変更できます。

```csharp
presentationOptions.SlideSize = new SizeF(13.33f, 7.5f); // 16:9 widescreen
```

これでエクスポートされたチャートに余裕ができ、テキストボックスも元のレイアウトを保持したまま表示されます。

### How to Convert Excel to PPT: Dealing with Hidden Objects

非表示の行・列・シェイプがエクスポートに混入することがあります。保存前に簡単なクリーンアップを実行して除去しましょう。

```csharp
// Remove hidden rows/columns that might affect chart layout
foreach (Worksheet sheet in workbook.Worksheets)
{
    sheet.Cells.HideRows = false;
    sheet.Cells.HideColumns = false;
}
```

このステップは必須ではありませんが、最終的なスライドデッキに予期せぬ空白ができるのを防げます。

### Save Workbook as PPTX – Full Working Example

すべてをまとめた、実行可能なコンソールプログラムの例を示します。

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing; // For SizeF

class ExportChartDemo
{
    static void Main()
    {
        // Load workbook (Step 1)
        string sourcePath = @"C:\Samples\ChartWithTextbox.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // Verify chart existence
        if (workbook.Worksheets[0].Charts.Count == 0)
        {
            Console.WriteLine("No chart found. Exiting.");
            return;
        }

        // Configure presentation options (Step 2)
        PresentationOptions options = new PresentationOptions
        {
            ExportTextBoxes = true,
            ExportShapes    = true,
            SlideSize       = new SizeF(13.33f, 7.5f) // optional widescreen
        };

        // Optional: export only first worksheet charts
        for (int i = 1; i < workbook.Worksheets.Count; i++)
        {
            foreach (Chart c in workbook.Worksheets[i].Charts)
                c.IsVisible = false;
        }

        // Save as PowerPoint (Step 3)
        string targetPath = @"C:\Samples\Result.pptx";
        workbook.Save(targetPath, SaveFormat.Pptx, options);

        Console.WriteLine($"Export complete! File saved to {targetPath}");
    }
}
```

このプログラムを実行すると、編集可能なチャートとテキストボックスを含む `Result.pptx` が作成されます。手動で **workbook を pptx として保存** したときと同じ結果です。

![Export chart to PowerPoint example](/images/export-chart-to-powerpoint.png "Export chart to PowerPoint – editable slide")

## Common Questions & Edge Cases

**What if the Excel file contains a chart with a linked external data source?**  
Aspose.Cells は *現在の* データ値を PowerPoint のチャートにコピーします。外部データソースへのリンクは保持されません。PowerPoint では Excel のデータ接続を同様に参照できないためです。ライブ更新が必要な場合は、元の Excel ファイルを OLE オブジェクトとして PPTX に埋め込むことを検討してください。

**Can I export a chart that uses a custom theme?**  
はい。ライブラリは Excel のテーマカラーを PowerPoint のテーマスロットにマッピングしようとします。非常にカスタムなパレットの場合は、エクスポート後に PowerPoint の API（例：Aspose.Slides）で色を調整する必要があるかもしれません。

**Is there a limit on the number of charts?**  
実質的な制限はありません。Aspose.Cells はデータをストリーミングするため、数十個のチャートがあってもエクスポート可能です。ただし PPTX のファイルサイズは線形に増加します。

**Do I need a license for Aspose.Cells?**  
評価版でも動作しますが、最初のスライドに透かしが入ります。製品環境で使用する場合は、透かしを除去しパフォーマンスを最大化するために正規ライセンスを取得してください。

## Recap

C# を使って **チャートを PowerPoint にエクスポート** する方法を解説しました。Excel ワークブックの読み込み、テキストボックスやシェイプを編集可能に保つ `PresentationOptions` の設定、そして `.pptx` として保存するまでのコードを具体的に示しました。また、**Excel を PowerPoint に変換**、**Excel を PowerPoint として保存**、さらには「**Excel を ppt に変換する方法**」という質問への完全な実装例も提供しました。

## What’s Next?

- **Save workbook as PPTX** with multiple slides: 各ワークシートをループし、`PresentationOptions` を使って `Save` を呼び出す。
- 生成された PPTX をさらにプログラムで加工したい場合は **Aspose.Slides** を検討（トランジションやスピーカーノートの追加など）。
- **ピボットチャート** や **3‑D チャート** のエクスポートにも同様のオプションが適用できますが、軸書式の微調整が必要になることがあります。

問題が発生したらコメントを残すか、公式の Aspose.Cells ドキュメントで最新 API 変更点を確認してください。コーディングを楽しみながら、数行の C# で Excel のチャートを洗練された PowerPoint プレゼンテーションに変換しましょう！

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}