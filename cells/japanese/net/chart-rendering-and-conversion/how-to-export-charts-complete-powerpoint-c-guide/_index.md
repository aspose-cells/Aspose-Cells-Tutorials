---
category: general
date: 2026-06-05
description: C# を使用して PowerPoint からチャートをエクスポートする方法。OLE オブジェクトのエクスポートと、生成された PPTX でチャートを編集可能にする手順をステップバイステップで解説。
draft: false
keywords:
- how to export charts
- export ole objects
- how to export ole
- make charts editable
language: ja
og_description: C# を使用して PowerPoint からチャートをエクスポートする方法。OLE オブジェクトのエクスポートと、保存された PPTX
  でチャートを編集可能にする手順をステップバイステップで学びましょう。
og_title: チャートをエクスポートする方法 – 完全なPowerPoint C#ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  headline: How to Export Charts – Complete PowerPoint C# Guide
  type: TechArticle
- description: How to export charts from PowerPoint using C#. Includes export OLE
    objects and make charts editable in the resulting PPTX – step‑by‑step.
  name: How to Export Charts – Complete PowerPoint C# Guide
  steps:
  - name: Full Working Example
    text: Below is the complete, self‑contained program you can compile and run. It
      includes `using` statements, proper disposal, and comments that explain each
      line.
  - name: What if the source file has no charts?
    text: The code will still run; `ExportEditableCharts` simply has no effect because
      there’s nothing to convert. No error is thrown.
  - name: Can I export only specific charts?
    text: Yes. Instead of using the global `ExportEditableCharts` flag, you can iterate
      through `presentation.Slides` and set `Chart.IsEditable = true` on individual
      chart objects before saving. This gives you granular control.
  - name: Does enabling OLE export increase file size?
    text: A little. The binary OLE streams are stored verbatim, so the resulting PPTX
      can be a few kilobytes larger. In most business scenarios the trade‑off is worth
      it because you retain full editability.
  - name: Which PowerPoint versions can open the resulting file?
    text: Any version that supports the OOXML standard (PowerPoint 2007 and later).
      The editable chart feature relies on the native chart editor introduced in Office
      2007, so older binaries like `.ppt` won’t benefit.
  type: HowTo
tags:
- PowerPoint
- C#
- Aspose.Slides
- OLE
- Charts
title: チャートのエクスポート方法 – 完全なPowerPoint C#ガイド
url: /ja/net/chart-rendering-and-conversion/how-to-export-charts-complete-powerpoint-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# チャートのエクスポート方法 – 完全版 PowerPoint C# ガイド

PowerPoint のデッキから **チャートのエクスポート方法** を、後で編集できる状態を失わずに行いたいと思ったことはありませんか？ あなただけではありません。多くのレポートパイプラインでは、チャートデータが PPTX 内に保存されており、ファイルを渡した相手が値を微調整したりラベルを変更したりする必要があります。良いニュースは、数行の C# コードで編集可能性を保持でき、埋め込み OLE オブジェクトも同時にエクスポートできることです。

このチュートリアルでは、実用的でそのまま実行できるサンプルを通して、**チャートのエクスポート方法**、**OLE オブジェクトのエクスポート方法**、そして出力ファイルで **チャートを編集可能にする方法** を紹介します。最後まで読めば、Aspose.Slides ライブラリを使用する任意の .NET プロジェクトに組み込める再利用可能なスニペットが手に入ります。

> **Pro tip:** Aspose.Slides が初めての方は、NuGet パッケージ `Aspose.Slides.NET` をプロジェクトに追加してください。追加しないとコードがコンパイルできません。

## 必要なもの

| 要件 | 重要な理由 |
|------|------------|
| .NET 6+ (or .NET Framework 4.7+) | 最新のランタイムはパフォーマンスが向上し、パッケージ管理が容易になります。 |
| Aspose.Slides for .NET (latest version) | 本ライブラリが `Presentation` と `PptxSaveOptions` クラスを提供します。 |
| A sample PowerPoint file with at least one chart | 任意の `.pptx` でチャートが含まれていればデモは動作し、エクスポート後に編集可能か確認できます。 |
| An IDE (Visual Studio, Rider, or VS Code) | デバッグや生成ファイルの確認が手軽に行えます。 |

追加のサードパーティツールは不要です。すべて Aspose API が処理します。

## ステップ 1 – ソースプレゼンテーションの読み込み

まず、元の PPTX をメモリに読み込みます。これは Word で文書を開いて編集を始めるイメージです。

```csharp
using Aspose.Slides;

// Step 1: Load the source presentation
Presentation presentation = new Presentation(@"C:\MyProjects\input.pptx");
```

> **Why this matters:** `Presentation` オブジェクトは以降のすべての操作のエントリーポイントです。ファイルを解析し、スライド、シェイプ、チャート、OLE オブジェクトのオブジェクトモデルを構築し、可変状態で保持します。

## ステップ 2 – 保存オプションの作成と編集可能チャートの有効化

デフォルトでは `Save` を呼び出すとライブラリはチャートを静的画像にフラット化します。編集可能に保つには `ExportEditableCharts` フラグをオンにする必要があります。

```csharp
// Step 2: Create PPTX save options and enable editable charts
PptxSaveOptions saveOptions = new PptxSaveOptions
{
    // This tells Aspose to keep chart data in a format PowerPoint can edit.
    ExportEditableCharts = true
};
```

> **How it works:** `ExportEditableCharts` が `true` の場合、ライブラリはチャートの XML 定義 (`chart.xml`) を PPTX に書き込み、ラスタライズしません。PowerPoint はその XML を読み取り、ユーザーがチャートエディタを開けるようにします。

## ステップ 3 – 埋め込み OLE オブジェクトのエクスポートを有効化

多くのプレゼンテーションでは Excel シート、Visio 図、PDF ファイルなどが OLE オブジェクトとして埋め込まれています。これらを往復させたい場合は `ExportOLEObjects` を有効にします。

```csharp
// Step 3: Enable export of embedded OLE objects
saveOptions.ExportOLEObjects = true;
```

> **What “export OLE objects” really means:** OLE パッケージは PPTX 内にバイナリブロブとして保存されます。このフラグを設定すると元のバイナリが保持され、受取側はオブジェクトをダブルクリックしてネイティブアプリケーション（例: Excel）で開くことができます。設定しないと OLE オブジェクトは除去され、リンクが切れデータが失われます。

## ステップ 4 – 設定したオプションでプレゼンテーションを保存

オプションの準備ができたので、Aspose にファイルを書き出すよう指示します。

```csharp
// Step 4: Save the presentation with the configured options
presentation.Save(@"C:\MyProjects\editable.pptx", saveOptions);
```

> **Result:** `editable.pptx` は `input.pptx` と同じスライドを含みますが、任意のチャートを PowerPoint 上で直接編集でき、埋め込み OLE オブジェクトもそのまま残ります。

### 完全な動作例

以下はコンパイルして実行できる、完全に自己完結したプログラムです。`using` 文、適切な破棄処理、各行を説明するコメントが含まれています。

```csharp
using System;
using Aspose.Slides;

namespace ExportChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the source PPTX
            string sourcePath = @"C:\MyProjects\input.pptx";
            // Path where the edited PPTX will be saved
            string destPath = @"C:\MyProjects\editable.pptx";

            // Load the presentation
            using (Presentation presentation = new Presentation(sourcePath))
            {
                // Configure save options
                PptxSaveOptions options = new PptxSaveOptions
                {
                    ExportEditableCharts = true,   // make charts editable
                    ExportOLEObjects = true        // export OLE objects such as embedded Excel sheets
                };

                // Save the new file
                presentation.Save(destPath, options);
            }

            Console.WriteLine("Presentation saved with editable charts and OLE objects.");
        }
    }
}
```

**Expected output:** プログラム実行後、PowerPoint で `editable.pptx` を開きます。任意のチャートを右クリック → *Edit Data* → チャートエディタが開き、**チャートを編集可能にする** が成功したことが確認できます。埋め込みの Excel シートをダブルクリックすると Excel が起動し、**OLE オブジェクトのエクスポート** が機能したことが証明されます。

![チャートのエクスポート図](https://example.com/images/export-charts.png "チャートのエクスポート – エクスポート後の PowerPoint")

*(Alt text: チャートのエクスポート – 編集可能なチャートと OLE オブジェクトを含む PowerPoint のスクリーンショット)*

## よくある質問とエッジケース

### ソースファイルにチャートがない場合は？

コードは問題なく実行されます。`ExportEditableCharts` は変換対象がないため効果がなく、エラーは発生しません。

### 特定のチャートだけをエクスポートできますか？

可能です。グローバルな `ExportEditableCharts` フラグを使用する代わりに、`presentation.Slides` を走査し、保存前に個々のチャートオブジェクトの `Chart.IsEditable = true` を設定できます。これにより細かな制御が可能になります。

```csharp
foreach (ISlide slide in presentation.Slides)
{
    foreach (IChart chart in slide.Shapes.OfType<IChart>())
    {
        chart.IsEditable = true; // enable editability only for this chart
    }
}
```

### OLE エクスポートを有効にするとファイルサイズは増えますか？

多少増えます。OLE のバイナリストリームがそのまま保存されるため、生成される PPTX は数キロバイト大きくなることがあります。多くのビジネスシナリオでは、完全な編集可能性を保つ価値があると判断されます。

### どのバージョンの PowerPoint が生成されたファイルを開けますか？

OOXML 標準に対応しているバージョン（PowerPoint 2007 以降）であれば開くことができます。編集可能チャート機能は Office 2007 で導入されたネイティブチャートエディタに依存しているため、古い `.ppt` 形式のバイナリでは利用できません。

## 本番環境向けコードのヒント

| ヒント | 理由 |
|--------|------|
| `using` ブロック（上記参照）で `Presentation` オブジェクトを破棄する | バッチ処理で多数のファイルを扱う際のメモリリークを防止します。 |
| 読み込み前にファイルパスを検証する | `FileNotFoundException` によるバックグラウンドサービスのクラッシュを回避できます。 |
| `ExportEditableCharts` と `ExportOLEObjects` の設定をログに記録する | ユーザーが編集できないチャートを報告した際のトラブルシューティングに役立ちます。 |
| `Aspose.Slides.Exception` を個別に捕捉する | ライブラリ固有のエラーメッセージ（例: 未対応のチャート種別）を取得しやすくなります。 |
| ファイルサイズが問題になる場合は `PptxCompressionLevel` を検討する | 圧縮しながらも編集可能性を保持したまま出力できます。 |

## まとめ – 達成したこと

最初に掲げた質問は、**チャートのエクスポート方法** を PowerPoint ファイルから行い、編集可能な状態と埋め込み OLE オブジェクトを保持できるか、というものでした。`Presentation` を読み込み、`PptxSaveOptions`（`ExportEditableCharts = true` と `ExportOLEObjects = true`）を設定し、ファイルを保存することで、両方の要件を満たす PPTX が得られました。このパターンはバッチ変換、CI パイプライン、または自動化レポートツールでも再利用可能です。

## 次に探求すべきこと

- **Export charts as images** for static reports (`saveOptions.ExportEditableCharts = false`)。  
- **Convert PPTX to PDF** while preserving vector graphics (`PdfSaveOptions`)。  
- **Manipulate chart data programmatically** (e.g., update series values before export)。  
- **Integrate with Azure Functions** to provide an on‑demand chart‑export API。

実験してみて、遭遇したエッジケースをぜひ教えてください。コーディングを楽しみながら、すべてのチャートが編集可能であり続けることを願っています！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示した手法に基づく関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装を検討したりするのに役立ちます。

- [Aspose.Cells for .NET を使用した Excel チャートの PDF へのエクスポート方法 – ステップバイステップガイド](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Aspose.Cells for .NET を使用した Excel チャートの SVG 変換方法 – ステップバイステップガイド](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Aspose.Cells .NET で Excel チャートにテーマを適用する方法 – ステップバイステップガイド](/cells/english/net/charts-graphs/apply-themes-charts-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}