---
category: general
date: 2026-10-26
description: C#でExcelのチャートをPowerPointにエクスポートする方法を学びましょう。形状の編集可能性を保持し、数行のコードでPPTXとして保存できます。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel charts to powerpoint
- Aspose.Cells export
- C# Excel to PowerPoint conversion
- preserve shape editability
- SaveFormat.Pptx
- Workbook.Save method
language: ja
lastmod: 2026-10-26
og_description: C#でExcelのチャートをPowerPointにエクスポートします。このガイドでは、形状を編集可能なままに保ち、Aspose.Cellsを使用してPPTXとして保存する方法を示します。
og_image_alt: Export Excel charts to PowerPoint example showing a chart transferred
  from Excel to a slide
og_title: C#でExcelのチャートをPowerPointにエクスポートする – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  headline: How to export Excel charts to PowerPoint using C#
  type: TechArticle
- description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  name: How to export Excel charts to PowerPoint using C#
  steps:
  - name: Load the Excel workbook
    text: '```csharp using Aspose.Cells;'
  - name: (Optional) Adjust workbook settings
    text: In most cases the default settings are sufficient for a clean export. However,
      if you need to change the calculation mode, page setup, or hide certain sheets,
      you can do it here.
  - name: Save the workbook as a PowerPoint file
    text: '```csharp // Export the workbook to PPTX while keeping chart shapes editable
      workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx); ```'
  - name: Verify the result
    text: 'Open `Shapes.pptx` in PowerPoint and:'
  - name: 'Edge case: Exporting multiple worksheets with separate charts'
    text: If your Excel file contains several worksheets, each with its own chart,
      Aspose.Cells creates a separate slide for each chart automatically. You can
      control slide order by rearranging worksheets before the save operation.
  - name: 'Performance tip: Stream the output instead of writing to disk'
    text: When generating PowerPoint files in a web API, avoid temporary files by
      writing to a `MemoryStream`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- PowerPoint
title: C# を使用して Excel のチャートを PowerPoint にエクスポートする方法
url: /ja/net/chart-rendering-and-conversion/how-to-export-excel-charts-to-powerpoint-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# を使用して Excel のチャートを PowerPoint にエクスポートする方法

Excel のチャートを **PowerPoint にエクスポート** する必要がある場合、このガイドでは、完全で実行可能なソリューションをステップバイステップで紹介します。レポート ダッシュボードを作成する場合でも、スライド デッキを自動化する場合でも、数行の C# コードで変換後もチャートの形状が完全に編集可能であることが確認できます。

このチュートリアルでは、以下を学びます：

* チャートを含む既存の Excel ワークブックを読み込む。  
* （オプション）変換前にワークブック設定を微調整する。  
* 形状の編集可能性を保持したまま、ワークブックを PowerPoint ファイルとして保存する。  

これらはすべて **Aspose.Cells for .NET** を使用して行います。このライブラリは、サーバー上で Microsoft Office を必要とせずに Excel から PowerPoint への変換を処理します。

## 必要なもの

| 要件 | 理由 |
|------|------|
| .NET 6.0 or later | フル機能の言語サポートを備えた最新のランタイム |
| Visual Studio 2022 (or any IDE) | 便利なエディタとデバッガ |
| **Aspose.Cells for .NET** NuGet package | `Workbook` クラスと `SaveFormat.Pptx` のサポートを提供 |
| An Excel file (`ChartAndShapes.xlsx`) that contains at least one chart | エクスポートしたいチャートのソース |

> **Pro tip:** コードをテストするには無料の **Aspose.Cells Evaluation** バージョンを使用してください。ライセンスキーを設定すれば評価版の透かしが削除されます。

```bash
dotnet add package Aspose.Cells
```

## Excel のチャートを PowerPoint にエクスポートする – 完全なワークフロー

以下は、**形状の編集可能性を保持**しながらエクスポートを実現するエンドツーエンドのコードです。各ステップについて詳細に説明します。

### 手順 1: Excel ワークブックをロードする

```csharp
using Aspose.Cells;

// Load the workbook that holds the charts you want to export
Workbook workbook = new Workbook(@"C:\Projects\ChartAndShapes.xlsx");
```

`Workbook` クラスは Excel ファイル全体を表します。ファイルをロードすると、すべてのワークシート、チャート、形状がメモリに読み込まれ、以降の操作に必要となります。

### 手順 2: （オプション）ワークブック設定の調整

ほとんどの場合、デフォルト設定でクリーンなエクスポートが可能です。ただし、計算モードやページ設定の変更、特定のシートの非表示などが必要な場合は、ここで行えます。

```csharp
// Example: ensure all formulas are calculated before export
workbook.CalculateFormula();

// Example: hide a sheet that you don’t want in the PowerPoint
workbook.Worksheets["SecretData"].IsVisible = false;
```

> **Why this matters:** 変換前に設定を調整することで、生成されるスライドが期待通りの状態を正確に反映します。特に、数式や非表示シートがチャートデータに影響を与える場合に重要です。

### 手順 3: ワークブックを PowerPoint ファイルとして保存する

```csharp
// Export the workbook to PPTX while keeping chart shapes editable
workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx);
```

`SaveFormat.Pptx` 定数は Aspose.Cells に PowerPoint プレゼンテーションを書き出すよう指示します。内部的に、ライブラリは各 Excel チャートを PowerPoint の形状に変換し、Microsoft PowerPoint で完全に編集可能なままにします。

### 手順 4: 結果の確認

`Shapes.pptx` を PowerPoint で開き、以下を実行します：

1. 任意のスライド上のチャートを選択します。  
2. 右クリック → **Edit Data**。  
3. チャートのデータテーブルが表示され、値を変更できることを確認します。

チャートが **Edit Data** ペインを開く場合、変換は成功しており、**形状の編集可能性** が保持されています。

![Export Excel charts to PowerPoint example](export-excel-charts-to-powerpoint.png){.img-fluid alt="Excel のチャートを PowerPoint にエクスポートする例"}

## よくある落とし穴と回避方法

| 問題点 | 原因 | 対策 |
|--------|------|------|
| チャートが静的画像として表示される | PPTX エクスポートをサポートしていない古い Aspose.Cells バージョンを使用している | 最新の Aspose.Cells 23.x 以降にアップグレードする |
| PowerPoint のチャートにデータが欠落している | エクスポート前にワークブックが完全に計算されていない | `Save` の前に `workbook.CalculateFormula()` を呼び出す |
| 形状が編集できない | `SaveFormat.Pptx` ではなく `SaveFormat.Xlsx` で保存している | `Workbook.Save` に `SaveFormat.Pptx` を渡すようにする |
| 実行時のライセンス例外 | 登録済みライセンスがない評価版を使用している | `License license = new License(); license.SetLicense("Aspose.Cells.lic");` でライセンスを登録する |

### エッジケース: 複数のワークシートに別々のチャートがある場合のエクスポート

Excel ファイルに複数のワークシートがあり、それぞれにチャートがある場合、Aspose.Cells は各チャートごとに自動的に別々のスライドを作成します。保存操作の前にワークシートの順序を入れ替えることで、スライドの順序を制御できます。

```csharp
// Move the worksheet that should appear first in the slide deck
workbook.Worksheets.MoveTo(2, 0); // move sheet index 2 to position 0
```

### パフォーマンスのヒント: ディスクに書き込む代わりに出力をストリームする

Web API で PowerPoint ファイルを生成する際は、`MemoryStream` に書き込むことで一時ファイルの作成を回避できます。

```csharp
using (MemoryStream pptStream = new MemoryStream())
{
    workbook.Save(pptStream, SaveFormat.Pptx);
    // Return the stream as a file download
    FileContentResult result = new FileContentResult(pptStream.ToArray(),
        "application/vnd.openxmlformats-officedocument.presentationml.presentation")
    {
        FileDownloadName = "Charts.pptx"
    };
    return result;
}
```

## 完全な実行可能サンプル

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1. Load the workbook containing charts
            string excelPath = @"C:\Projects\ChartAndShapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2. (Optional) Ensure formulas are up‑to‑date
            workbook.CalculateFormula();

            // 3. Export to PowerPoint while preserving shape editability
            string pptxPath = @"C:\Projects\Shapes.pptx";
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export complete. PowerPoint saved to: {pptxPath}");
        }
    }
}
```

**Expected output:** コンソールに確認メッセージが表示され、`Shapes.pptx` を PowerPoint で開くと各 Excel チャートが個別のスライドに表示されます。チャートを選択するとデータを編集でき、**形状の編集可能性** が保持されていることが確認できます。

## まとめと次のステップ

これで、C# を使用して **Excel のチャートを PowerPoint にエクスポート** し、チャートを完全に編集可能な状態で保持する方法が分かりました。ソリューションの核心は `Workbook.Save` メソッドに `SaveFormat.Pptx` を指定することで、**Aspose.Cells export** の機能により複雑な Open XML の処理を抽象化しています。

ここからは以下を検討できます：

* **Aspose.Slides** API を使用してカスタム スライド タイトルやノートを追加する。  
* チャートと共に他の Excel オブジェクト（テーブル、画像）を変換する。  
* バックグラウンド サービスで複数のワークブックをバッチ処理で自動化する。

上記のオプション設定を自由に試し、このパターンをレポート パイプラインに組み込んで、迅速かつ信頼性の高い PowerPoint 生成を実現してください。

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [C# で Excel チャートを PowerPoint にエクスポート – 完全な Aspose.Cells ガイド](/cells/english/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/)
- [C# で Excel を PowerPoint にエクスポートする方法 – 完全ガイド](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)
- [Excel から PowerPoint へシェイプをエクスポートする方法 – 完全ガイド](/cells/english/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}