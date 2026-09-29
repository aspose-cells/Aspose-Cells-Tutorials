---
category: general
date: 2026-01-14
description: Aspose.Cells を使用してピボットテーブルをコピーする方法と、Excel を PPTX に変換する方法、範囲を別のブックにコピーする方法、テキストボックスを編集可能な
  PPTX にする方法をひとつのチュートリアルで学ぶ。
draft: false
keywords:
- how to copy pivot table
- convert excel to pptx
- copy range to another workbook
- make textbox editable pptx
- save workbook as pptx
language: ja
og_description: ピボットテーブルをコピーし、ExcelをPPTXに変換し、範囲を別のブックにコピーし、テキストボックスを編集可能なPPTXにする方法—すべてAspose.Cellsで実現。
og_title: C#でピボットテーブルをコピーする方法 – 完全なExcelからPPTXへのガイド
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: C#でピボットテーブルをコピーする方法 – ExcelをPPTXに変換、範囲をコピーしてテキストボックスを編集可能にする
url: /ja/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# でピボットテーブルをコピーする方法 – 完全な Excel から PPTX ガイド

ワークブック間でピボットテーブルをコピーする方法は、Excel 主導のレポートを自動化する際によくある質問です。このチュートリアルでは、**Aspose.Cells for .NET** を使用した 3 つの実践シナリオを解説します：ピボットテーブル範囲のコピー、編集可能なテキストボックス付きのワークシートを PPTX ファイルにエクスポート、Smart Markers を使って JSON 配列を単一セルに埋め込む方法です。

また、**Excel を PPTX に変換**、**範囲を別のワークブックにコピー**、**テキストボックスを編集可能な PPTX にする** 方法も紹介し、書式を崩さずに実行可能なコードベースを最終的に取得できます。これを .NET プロジェクトにそのまま組み込めます。

> **プロのコツ:** すべての例は Aspose.Cells 23.12 を対象としていますが、同じ概念は以前のバージョンでも API の細かな変更で適用できます。

![ピボットテーブルのコピー、ワークシートの PPTX へのエクスポート、JSON 配列の挿入方法を示す図 – ピボットテーブルコピーのワークフロー](how-to-copy-pivot-table-diagram.png)

---

## 必要なもの

- Visual Studio 2022（または任意の C# IDE）
- .NET 6.0 以降のランタイム
- Aspose.Cells for .NET NuGet パッケージ  
  ```bash
  dotnet add package Aspose.Cells
  ```
- サンプル Excel ファイル 2 つ（`source.xlsx`、`chartWithTextbox.xlsx`）を、管理できるフォルダーに配置します（`YOUR_DIRECTORY` を実際のパスに置き換えてください）。

追加のライブラリは不要です。同じ `Aspose.Cells` アセンブリが Excel、PPTX、Smart Markers を処理します。

## ピボットテーブルをコピーしてデータを保持する方法

ピボットテーブルを含む範囲をコピーすると、デフォルトでは **値** のみが貼り付けられます。ピボットの定義をそのまま保持するには `CopyPivotTable` フラグを有効にする必要があります。

### 手順

1. ピボットテーブルを保持している **ソース ワークブックをロード** します。  
2. **空の宛先ワークブックを作成** します – ここにコピーした範囲が受け取られます。  
3. `CopyRange` を `CopyPivotTable = true` と共に使用し、ピボット定義をデータと共にコピーします。  
4. 必要な場所に **宛先ファイルを保存** します。

#### 完全なコード例

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Step 1: Load the source workbook and define the range to copy
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        // Assuming the pivot table lives inside A1:G20
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // Step 2: Create a destination workbook (blank)
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

        // Step 3: Copy the range, preserving the pivot table
        destinationSheet.Cells.CopyRange(
            sourceRange,
            "B2", // paste start cell
            new CopyOptions { CopyPivotTable = true });

        // Step 4: Save the result
        destinationWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

**なぜこれが機能するか:**  
`CopyOptions.CopyPivotTable` は、Aspose.Cells に対してレンダリングされた値だけでなく、基になる `PivotTable` オブジェクトをクローンするよう指示します。これにより、宛先ワークブックにはプログラムからリフレッシュや変更が可能な完全な機能を持つピボットが含まれます。

**エッジケース:** ソースワークブックが外部データ ソースを使用している場合、コピー後にデータを埋め込むか接続文字列を調整する必要があります。そうしないとピボットは “#REF!” を表示します。

## Excel を PPTX に変換し、テキストボックスを編集可能にする

ワークシートを PowerPoint にエクスポートすると、データから直接スライドデッキを作成でき便利です。デフォルトではエクスポートされたテキストボックスは静的なシェイプになりますが、`IsTextBoxEditable` を設定するとその動作が逆転します。

### 手順

1. エクスポートしたいチャートとテキストボックスを含む **ワークブックを開く**。  
2. `SaveFormat = SaveFormat.Pptx` を設定した **`ImageOrPrintOptions` を構成**。  
3. テキストボックスを含む **印刷領域を定義**。  
4. PPTX を開いた後にテキストを編集できるよう **`IsTextBoxEditable` を有効化**。  
5. **PPTX ファイルを保存**。

#### 完全なコード例

```csharp
using Aspose.Cells;

class ExcelToPptxDemo
{
    static void Main()
    {
        // Step 1: Load the workbook with chart and textbox
        Workbook chartWorkbook = new Workbook(@"YOUR_DIRECTORY\chartWithTextbox.xlsx");

        // Step 2: Set export options for PPTX
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Pptx
        };

        // Step 3: Define the print area that captures the textbox (A1:D20)
        chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:D20";

        // Step 4: Make the textbox editable in the exported PPTX
        chartWorkbook.Worksheets[0].PageSetup.IsTextBoxEditable = true;

        // Step 5: Export the worksheet to a PPTX file
        chartWorkbook.Save(@"YOUR_DIRECTORY\result.pptx", pptxOptions);
    }
}
```

**結果:** PowerPoint で `result.pptx` を開くと、Excel で配置したテキストボックスが通常のテキストボックスとして表示され、直接入力できます。手動で再作成する必要はありません。

**一般的な落とし穴:** 印刷領域と交差する結合セルがあると、スライドがずれることがあります。エクスポート前に印刷領域を調整するか、セルの結合を解除してください。

## Smart Markers を使用して別のワークブックに範囲をコピー（JSON → 単一セル）

場合によっては、JSON 配列を単一の Excel セルに埋め込む必要があります。たとえば、下流システムが JSON 文字列を期待する場合です。`ArrayAsSingle = true` を設定すると、Aspose.Cells の Smart Markers が配列を単一セルにシリアライズできます。

### 手順

1. Smart Marker プレースホルダー（例: `&=Items.Name`）を含む **テンプレート ワークブックをロード**。  
2. データオブジェクトを準備 – `Items` 配列を持つ匿名型。  
3. `SmartMarkerProcessor` を作成し、`ArrayAsSingle` を使用してデータを適用。  
4. **埋め込まれたワークブックを保存**。

#### 完全なコード例

```csharp
using Aspose.Cells;
using System;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Load the template workbook containing a smart marker like "&=Items.Name"
        Workbook templateWorkbook = new Workbook(@"YOUR_DIRECTORY\SmartMarkerTemplate.xlsx");

        // Step 2: Prepare the data object with an array of items
        var data = new
        {
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        };

        // Step 3: Apply the SmartMarkerProcessor with ArrayAsSingle option
        SmartMarkerProcessor processor = new SmartMarkerProcessor(templateWorkbook);
        processor.Apply(data, new SmartMarkerOptions { ArrayAsSingle = true });

        // Step 4: Save the result – the JSON array will appear in a single cell
        templateWorkbook.Save(@"YOUR_DIRECTORY\jsonSingleCell.xlsx");
    }
}
```

**説明:**  
`ArrayAsSingle` が true の場合、Aspose.Cells は `Items.Name` の各要素を JSON 形式の文字列（`["A","B"]`）に連結し、Smart Marker があったセルに書き込みます。これにより、要素ごとに別々の行を作成する必要がなくなります。

**使用例:** 設定テーブルや API ペイロードのエクスポート、または受取側がタブular なレイアウトではなくコンパクトな JSON 文字列を期待するシナリオに最適です。

## 追加のヒントとエッジケースの対処

| シナリオ | 注意点 | 推奨対策 |
|----------|-------------------|---------------|
| **大規模ピボットテーブル** | 巨大なピボットキャッシュをコピーするとメモリ使用量が急増する。 | ロード前に `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` を使用する。 |
| **画像付き PPTX エクスポート** | 画像が低 DPI でラスタライズされる可能性がある。 | `pptxOptions.ImageResolution = 300` を設定してスライドを高解像度にする。 |
| **Smart Marker JSON フォーマット** | 特殊文字（`"`、`\`）が JSON を壊す。 | 手動でエスケープするか、Smart Markers に渡す前に `JsonSerializer` で事前シリアライズする。 |
| **異なる Excel バージョン間で範囲をコピー** | 古い `.xls` ファイルは書式が失われる可能性がある。 | 宛先を `.xlsx` として保存し、最新機能を保持する。 |

## まとめ – ピボットテーブルのコピーとその他多くのこと

まず、**ピボットテーブルを機能を保持したままコピーする方法** に答え、次に **Excel を PPTX に変換**、**テキストボックスを編集可能な PPTX にする**、最後に Smart Markers を使用して JSON 配列を単一セルに埋め込む形で **別のワークブックに範囲をコピー** する方法を示しました。

3 つのコードスニペットはすべて自己完結しており、新しいコンソール アプリに貼り付け、ファイル パスを調整すればすぐに実行できます。

## 次にやること

- **他のエクスポート形式を探る** – Aspose.Cells は PDF、XPS、HTML もサポートしています。  
- コピー後に `PivotTable.RefreshData()` を使用して **プログラムからピボットテーブルをリフレッシュ**。  
- **Smart Markers とチャートを組み合わせ**、自動更新される動的ダッシュボードを生成。

**カスタムスライドレイアウトでワークブックを PPTX として保存** に興味がある場合は、`SlideOptions` に関する Aspose.Cells のドキュメントをご覧ください。

自由に試してみてください—印刷領域を変更したり、異なる `CopyOptions` を試したり、より複雑な JSON ペイロードを入力したり。API はほとんどのレポート パイプラインに十分柔軟です。

### よくある質問

**Q: `CopyPivotTable` はスライサーもコピーしますか？**  
A: 直接はコピーされません。スライサーは別個のオブジェクトなので、コピー後に `Worksheet.Shapes` コレクションを使って再作成またはコピーする必要があります。

**Q: 複数のワークシートを単一の PPTX デッキにエクスポートできますか？**  
A: はい。各ワークシートをループし、同じ `ImageOrPrintOptions` で `Save` を呼び出し、`pptxOptions.StartSlideNumber` を設定してスライド番号を連続させます。

**Q: JSON 配列にネストされたオブジェクトが含まれる場合はどうすればよいですか？**  
A: `ArrayAsSingle = false` に設定し、ネストされたオブジェクトを反復処理するカスタムテンプレートを使用します。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}