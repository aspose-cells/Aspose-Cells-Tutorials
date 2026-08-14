---
category: general
date: 2026-08-14
description: Aspose.Cells を使用して Excel を PowerPoint にエクスポートし、コードで Excel の数式を計算する方法を学びます。ステップバイステップの
  C# サンプルと完全なソースコード。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- calculate excel formulas in code
- Aspose.Cells copy pivot table
- export editable objects pptx
- dynamic array EXPAND function
- C# workbook automation
language: ja
lastmod: 2026-08-14
og_description: Aspose.Cells を使用して Excel を PowerPoint にエクスポートし、コード内で Excel の数式を計算します。ワークブックから編集可能な
  PPTX ファイルを生成する完全ガイドをご覧ください。
og_image_alt: Screenshot showing an Excel sheet being exported to a PowerPoint slide
  with editable textboxes
og_title: Aspose.Cells を使用した Excel から PowerPoint へのエクスポート – 完全 C# チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  headline: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  type: TechArticle
- description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  name: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  steps:
  - name: Why this works
    text: '* **`Workbook`** loads the entire Excel file into memory, giving you full
      API access. * **`CopyRange`** with `CopyPivotTable = true` ensures the pivot
      table’s data source, cache, and layout are duplicated exactly—something older
      versions of Aspose.Cells could not do. * Adding a new worksheet (`Copy`'
  - name: Explanation
    text: '* **`WorkbookDesigner`** is a high‑level helper that prepares the workbook
      for export, handling Smart Markers, named ranges, and layout adjustments. *
      Setting `ExportEditableObjects = true` tells Aspose.Cells to translate Excel
      drawings into PowerPoint shapes rather than flattening them into images.'
  - name: Why you might use this
    text: '* **Uniform data type:** Exporting as strings avoids type‑mismatch errors
      when the consumer expects text. * **Custom formatting:** Replace `value.ToString()`
      with any custom formatter (e.g., `value.ToString("yyyy-MM-dd")` for dates).'
  - name: How the calculation engine works
    text: '* The `Formula` property stores the expression exactly as you would type
      it in Excel. * `CalculateFormula()` triggers a full workbook recalculation,
      respecting dependencies between cells. * The `EXPAND` function (available in
      Excel 365) returns a spill range based on the source cell (`B1`) and the s'
  - name: What to verify
    text: '* Open `result.xlsx` in Excel to confirm the pivot table copy, the `EXPAND`
      formula result, and any custom‑exported strings. * Open `output.pptx` in PowerPoint;
      you should see a slide that mirrors the Excel layout, and all charts/textboxes
      should be editable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
- Office 365 functions
title: Aspose.Cells を使用した Excel から PowerPoint へのエクスポート – 完全プログラミングガイド
url: /ja/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-aspose-cells-complete-progra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells を使用した Excel から PowerPoint へのエクスポート – 完全プログラミングガイド

プログラムで **Excel を PowerPoint にエクスポート** する必要がある場合、このガイドでは Aspose.Cells for .NET を使用してその方法を詳しく解説します。また、**コード内で Excel の数式を計算** する方法、ピボットテーブルを定義を失わずにコピーする方法、そして動的配列用の新しい Office‑365 EXPAND 関数の使用方法も学べます。

以下のセクションでは、実際の C# サンプルを順に解説し、各行が重要な理由を説明するとともに、一般的な落とし穴についても取り上げます。これにより、皆さんのプロジェクトに合わせてソリューションを適用できるようになります。

## 本チュートリアルでカバーする内容

* 既存のブック (`input.xlsx`) をロードする  
* ピボットテーブルを含む範囲を定義を保持したままコピーする  
* ブックを PowerPoint (`.pptx`) ファイルにエクスポートし、テキストボックスやシェイプを編集可能にする  
* カスタムロジックを使用してセル範囲を文字列としてエクスポートする  
* Excel の数式をコード内で計算する（Office‑365 EXPAND 関数を含む）  
* すべての変更を適用した最終ブックを保存する  

**前提条件**  
* .NET 6.0 以降（コードは .NET Framework 4.7.2+ でも動作します）  
* Aspose.Cells for .NET v25.11 以降（`CopyPivotTable` オプションは v25.11 で導入されました）  
* C# と、範囲、ピボットテーブル、数式などの Excel の概念に関する基本的な理解  

> **プロのコツ:** NuGet (`Install-Package Aspose.Cells`) で Aspose.Cells をインストールすると、プロジェクトを最新機能に保つことができます。

## Aspose.Cells を使用した Excel から PowerPoint へのエクスポート

最初の重要なタスクは、ブックを PowerPoint プレゼンテーションに変換し、すべてのビジュアル要素を編集可能なまま保持することです。これは、財務レポートやダッシュボードからスライドデッキを自動的に生成したい場合に不可欠です。

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;      // ExportTableOptions, ExportOptions, etc.
using Aspose.Cells.Pivot;      // Pivot‑table APIs
using Aspose.Cells.Drawing;    // Shapes, textboxes, etc.

// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Step 2: Copy a range that contains a pivot table (preserves the definition)
Worksheet sourceSheet = workbook.Worksheets["Source"];
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");   // includes a pivot table
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
destinationSheet.Cells.CopyRange(sourceRange, destinationSheet.Cells, new CopyOptions
{
    CopyPivotTable = true   // new option in v25.11
});
```

### これが機能する理由

* **`Workbook`** は Excel ファイル全体をメモリに読み込み、フル API アクセスを提供します。  
* `CopyRange` に `CopyPivotTable = true` を設定すると、ピボットテーブルのデータソース、キャッシュ、レイアウトが正確に複製されます。これは旧バージョンの Aspose.Cells では実現できませんでした。  
* 新しいワークシート（`Copy`）を追加することで、元のシートを変更せずに保持でき、監査トレイルに役立ちます。  

## 編集可能なオブジェクト付きでブックを PowerPoint にエクスポート

ここではブックを PowerPoint ファイルに変換します。`ExportEditableObjects` を有効にすると、すべてのチャート、シェイプ、テキストボックスがネイティブな PowerPoint オブジェクトとなり、エクスポート後にユーザーが直接編集できるようになります。

```csharp
// Step 3: Export the workbook to PowerPoint with editable textboxes/shapes
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.Process();   // processes Smart Markers if present
designer.ExportToPptx("YOUR_DIRECTORY/output.pptx", new ExportOptions
{
    ExportEditableObjects = true   // makes objects editable in the PPTX
});
```

### 説明

* **`WorkbookDesigner`** は、エクスポートのためにブックを準備する高レベルヘルパーで、スマートマーカー、名前付き範囲、レイアウト調整を処理します。  
* `ExportEditableObjects = true` を設定すると、Aspose.Cells は Excel の描画を画像にフラット化せず、PowerPoint のシェイプに変換します。これにより、**完全に編集可能**なスライドデッキが得られます。  

> **エッジケース:** ブックに外部データ接続から作成された複雑なチャートが含まれる場合、`ExportToPptx` を呼び出す前にその接続が解決されていることを確認してください。そうしないと、チャートが空白で表示される可能性があります。

## カスタムロジックを使用して範囲を文字列としてエクスポート

下流処理（例: CSV パーサーへの入力）で生の文字列値が必要になることがあります。`ExportTableOptions` クラスを使用すると、各セルの変換方法を制御できます。

```csharp
// Step 4: Export a range as strings using custom logic
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true,
    CustomExport = (cell, value) => value.ToString()   // simple conversion for each cell
};
workbook.Worksheets[0].Cells.ExportTableAsString(tableOptions, "A1:D10");
```

### これを使用する理由

* **統一されたデータ型:** 文字列としてエクスポートすることで、受取側がテキストを期待している場合の型不一致エラーを回避できます。  
* **カスタム書式設定:** `value.ToString()` を任意のカスタムフォーマッタに置き換えられます（例: 日付の場合は `value.ToString("yyyy-MM-dd")`）。  

## コード内で Excel の数式を計算

頻繁に求められる要件として、Excel を開かずに **コード内で Excel の数式を計算** することがあります。Aspose.Cells はオフラインで動作し、最新の Office‑365 関数（`EXPAND` を含む）をサポートする組み込み計算エンジンを提供します。

```csharp
// Step 5: Use the new Office‑365 EXPAND function to create a dynamic array
Worksheet firstSheet = workbook.Worksheets[0];
firstSheet.Cells["A1"].Formula = "EXPAND(B1,5,3)";   // expands array starting at B1
workbook.CalculateFormula();   // forces recalculation of the formula
```

### 計算エンジンの仕組み

* `Formula` プロパティは、Excel で入力するのと同じ式をそのまま保持します。  
* `CalculateFormula()` はブック全体の再計算をトリガーし、セル間の依存関係を考慮します。  
* `EXPAND` 関数（Excel 365 で利用可能）は、ソースセル (`B1`) と指定された行数 (`5`) および列数 (`3`) に基づいてスピル範囲を返します。  

> **ヒント:** ブックの一部だけを計算したい場合は、`Worksheet.CalculateFormula()` を使用して範囲を限定し、パフォーマンスを向上させてください。

## すべての変更を適用した状態でブックを保存

最後に、変更されたブックをディスクに書き戻します。ファイル拡張子を変更することで、サポートされている任意の形式（`.xlsx`、`.xls`、`.csv` など）で保存できます。

```csharp
// Step 6: Save the workbook with all changes applied
workbook.Save("YOUR_DIRECTORY/result.xlsx");
```

### 確認すべき点

* `result.xlsx` を Excel で開き、ピボットテーブルのコピー、`EXPAND` 数式の結果、カスタムエクスポートされた文字列が正しいことを確認します。  
* `output.pptx` を PowerPoint で開きます。Excel のレイアウトを反映したスライドが表示され、すべてのチャート/テキストボックスが編集可能であることを確認してください。  

## よくある質問とトラブルシューティング

| 質問 | 回答 |
|----------|--------|
| **Aspose.Cells の使用にライセンスは必要ですか？** | はい。評価用にトライアルは使用できますが、フルライセンスを取得すると評価用の透かしが除去され、`CopyPivotTable` 機能が有効になります。 |
| **エクスポートされた PPTX が空白のシェイプになる場合はどうすればよいですか？** | `Workbook` の描画オブジェクトが非表示になっていないか (`Visible = true`) を確認し、エクスポート前に外部画像リンクが埋め込まれていることを確認してください。 |
| **複数のワークシートを別々の PPTX スライドにエクスポートできますか？** | `WorkbookDesigner.ExportToPptx` をループで使用し、各ワークシートごとに異なる `ExportOptions` を指定するか、Aspose.Slides を使用して手動でスライドを追加し、単一のプレゼンテーションに結合します。 |
| **`CalculateFormula` はスレッドセーフですか？** | いいえ。計算は単一スレッドで実行するか、スレッドごとにブックをクローンしてレースコンディションを回避してください。 |

## 結論

これで、Aspose.Cells を使用した **Excel から PowerPoint へのエクスポートの完全なエンドツーエンドソリューション** が手に入り、**コード内で Excel の数式を計算**する方法（最新の `EXPAND` 関数を含む）も理解できました。本チュートリアルでは、ブックのロード、ピボットテーブルのコピー、編集可能な PowerPoint へのエクスポート、カスタム文字列エクスポート、数式計算、最終保存について解説しました。

ここからは以下のように拡張できます：

* ワークシートごとに複数のスライドを含めるようにエクスポートを拡張する（副キーワード: *calculate Excel formulas in code* はチャートデータ生成時に再利用できます）。  
* Aspose.Slides を統合して、アニメーションやマスタースライドレイアウトを追加する。  
* シンプルな `CustomExport` デリゲートを、国際プロジェクト向けにロケール対応の書式設定に置き換える。  

さまざまな範囲で実験したり、他の Office‑365 関数（例: `FILTER`、`SORT`）を試したり、このワークフローを自動メール配信と組み合わせて、完全にハンドオフされたレポートパイプラインを構築してみてください。

---

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説付きの完全な動作コード例が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.Cells for .NET を使用した Excel データエクスポートの自動化&#58; ステップバイステップガイド](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)
- [Aspose.Cells for .NET を使用した Excel チャートの PDF へのエクスポート&#58; ステップバイステップガイド](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Aspose.Cells .NET を使用した Excel セルの画像へのエクスポート&#58; ステップバイステップガイド](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}