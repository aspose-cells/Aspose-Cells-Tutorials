---
category: general
date: 2026-09-15
description: Aspose.Cells を使用して C# でピボットテーブルのコピー、ピボット付きワークシートのコピー、ブックを PPTX として保存する方法を学びましょう。ステップバイステップの完全ガイド。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy worksheet with pivot
- save workbook as pptx
language: ja
lastmod: 2026-09-15
og_description: Aspose.Cells を使用してピボットテーブルをコピーし、ピボット付きワークシートをコピーし、ブックを PPTX として保存する方法。完全な実行可能な
  C# サンプルをご覧ください。
og_image_alt: Screenshot showing how to copy pivot table in a C# code editor
og_title: ピボットテーブルのコピーとワークシートのエクスポート方法 – 完全C#ガイド
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  headline: How to copy pivot table while preserving worksheets
  type: TechArticle
- description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  name: How to copy pivot table while preserving worksheets
  steps:
  - name: – Load the source workbook that holds the pivot table
    text: '```csharp // Load the workbook that contains the pivot table you want to
      copy Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx"); ```'
  - name: – Create an empty destination workbook
    text: '```csharp // Create a new, empty workbook that will receive the copied
      data Workbook destinationWorkbook = new Workbook(); ```'
  - name: – Copy the rows that include the pivot table
    text: '```csharp // Copy rows 0‑19 (A1:G20) from the first worksheet of the source
      sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20); ```'
  - name: – Copy the columns that contain the pivot table
    text: '```csharp // Copy columns 0‑6 (A‑G) from the same worksheet sourceWorkbook.Worksheets[0].Cells.CopyColumns(0,
      0, 7); ```'
  - name: – Transfer the prepared sheet into the destination workbook
    text: '```csharp // Move the fully prepared worksheet into the destination workbook
      sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]); ```'
  - name: – Save the result – the pivot table remains intact
    text: '```csharp // Save the destination workbook; the pivot table works exactly
      like the original destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
      ```'
  - name: – Load the workbook that includes the textbox
    text: '```csharp // Load the Excel file that contains an editable textbox shape
      Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
      ```'
  - name: – Configure PPTX save options
    text: '```csharp // Create PPTX save options and enable the editable textbox feature
      (available from v25.11) PptxSaveOptions pptxOptions = new PptxSaveOptions {
      ExportEditableTextBox = true }; ```'
  - name: – Save the workbook as PPTX
    text: '```csharp // Export the workbook to a PPTX file; the textbox stays editable
      in PowerPoint workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
      ```'
  - name: – Prepare the SmartMarkerProcessor
    text: '```csharp // Initialise the processor that will fill Smart Markers SmartMarkerProcessor
      smartMarkerProcessor = new SmartMarkerProcessor(); ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: ワークシートを保持しながらピボットテーブルをコピーする方法
url: /ja/net/pivot-tables/how-to-copy-pivot-table-while-preserving-worksheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ピボットテーブルをコピーしながらワークシートを保持する方法

ワークブック間で **ピボットテーブルをコピーする方法** を、基になるピボットキャッシュを失わずに実行したい場合は、このガイドのソリューションをご利用ください。また、 **ピボット付きワークシートをコピーする方法** や、 **編集可能なテキストボックスを保持したままワークブックを pptx として保存する方法** も紹介します。すべての例は最新の Aspose.Cells for .NET を使用しているので、コードを任意の C# プロジェクトに貼り付けるだけで即座に結果を確認できます。

Excel ファイルをプログラムで操作する際は、ワークブック間でデータを移動したり、プレゼンテーションにエクスポートしたり、複雑な Smart Marker を挿入したりするケースが頻繁にあります。以下の 3 つのコードスニペットは、そうした一般的なシナリオをカバーし、各ステップの重要性を解説します。

## 前提条件

開始する前に、以下を確認してください。

* .NET 6.0 以降がインストールされていること  
* Aspose.Cells for .NET（バージョン 25.11 以降）がプロジェクトに参照されていること  
* サンプルファイルの読み書きに使用する `YOUR_DIRECTORY` という名前のフォルダーが存在すること  

追加の NuGet パッケージは不要です。

---

## Aspose.Cells でピボットテーブルをコピーする方法

ピボットテーブルを含む範囲をコピーし、ピボットキャッシュを保持する必要が頻繁にあります。以下の手順で正確なシーケンスを示します。

### 手順 1 – ピボットテーブルが含まれるソース ワークブックを読み込む

```csharp
// Load the workbook that contains the pivot table you want to copy
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
```

*理由*: Aspose.Cells はワークブックをメモリに読み込み、ワークシート、セル、ピボットテーブルへのアクセスを可能にします。

### 手順 2 – 空の宛先ワークブックを作成する

```csharp
// Create a new, empty workbook that will receive the copied data
Workbook destinationWorkbook = new Workbook();
```

*理由*: 空のワークブックから開始することで、隠れたスタイルや名前付き範囲がコピー操作に干渉するのを防げます。

### 手順 3 – ピボットテーブルを含む行をコピーする

```csharp
// Copy rows 0‑19 (A1:G20) from the first worksheet of the source
sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20);
```

*理由*: `CopyRows` はセルの生データ、書式、基になるピボットキャッシュ参照をコピーします。範囲はピボットテーブル全体を含む必要があります。

### 手順 4 – ピボットテーブルを含む列をコピーする

```csharp
// Copy columns 0‑6 (A‑G) from the same worksheet
sourceWorkbook.Worksheets[0].Cells.CopyColumns(0, 0, 7);
```

*理由*: ピボットテーブルは行と列の両方にまたがるため、列をコピーすることでテーブル全体のレイアウトが保持されます。

### 手順 5 – 用意したシートを宛先ワークブックに転送する

```csharp
// Move the fully prepared worksheet into the destination workbook
sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]);
```

*理由*: `Copy` メソッドはワークシート全体をクローンし、ピボットキャッシュも含めてコピーするため、宛先ワークブックに同一のピボットテーブルが表示されます。

### 手順 6 – 結果を保存する – ピボットテーブルはそのまま保持される

```csharp
// Save the destination workbook; the pivot table works exactly like the original
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*理由*: ワークブックを永続化することで内部構造がすべて書き込まれ、後でピボットをリフレッシュできることが保証されます。

**プロのコツ**: コピー後に `destinationWorkbook.Worksheets[0].PivotTables[0].Refresh()` を呼び出すと、元データが変更された場合にピボットを更新できます。

---

## ピボット付きワークシートをコピーする – 簡潔な代替手段

ピボットテーブルを含むワークシート全体を単純に複製したい場合は、行/列コピーの手順を省略し、ワークシートレベルの `Copy` メソッドを直接使用できます。

```csharp
// Load source workbook
Workbook src = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

// Create destination workbook
Workbook dst = new Workbook();

// Copy the first worksheet (including its pivot table) to the destination
src.Worksheets[0].Copy(dst.Worksheets[0]);

// Save the new file
dst.Save("YOUR_DIRECTORY/WorksheetCopy.xlsx");
```

この方法は、ワークシートにピボット領域外の余分なデータがない場合に便利です。 **ピボット付きワークシートのコピー** 操作は、すべての書式、名前付き範囲、ピボットキャッシュを自動的に保持します。

---

## 編集可能なテキストボックス付きでワークブックを PPTX として保存する

編集可能なテキストボックスを含む Excel シートを PowerPoint にエクスポートする必要があるケース（レポート ダッシュボード等）があります。以下のコードは、 **ワークブックを pptx として保存** しつつテキストボックスを編集可能なままにする方法を示します。

### 手順 1 – テキストボックスを含むワークブックを読み込む

```csharp
// Load the Excel file that contains an editable textbox shape
Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
```

### 手順 2 – PPTX 保存オプションを設定する

```csharp
// Create PPTX save options and enable the editable textbox feature (available from v25.11)
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableTextBox = true
};
```

*理由*: `ExportEditableTextBox` を設定すると、Aspose.Cells は Excel のテキストボックスを PowerPoint の形状に変換し、エクスポート後も編集可能にします。

### 手順 3 – ワークブックを PPTX として保存する

```csharp
// Export the workbook to a PPTX file; the textbox stays editable in PowerPoint
workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
```

**期待される結果**: PowerPoint で `Result.pptx` を開き、テキストボックスを選択して内容を任意に編集できることを確認してください。

**よくある質問**: *テキストボックスをロックしたままにしたい場合は？*  
`pptxOptions.ExportEditableTextBox = false` と設定すると、形状は静的な画像に変換されます。

---

## JSON 配列を単一セル値として含む Smart Marker をエクスポートする

Smart Marker を使用すると、複雑なデータ構造を Excel テンプレートに埋め込めます。以下は **ピボットテーブルのコピー** と同様のデータ処理を行いながら、JSON 配列を単一セルに挿入する完全な例です。

### 手順 1 – SmartMarkerProcessor を準備する

```csharp
// Initialise the processor that will fill Smart Markers
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
```

### 手順 2 – セル A1 に Smart Marker を挿入する

```csharp
// The marker ${Orders:ArrayAsSingle} tells the processor to write the whole array into one cell
Workbook workbook = new Workbook();
workbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
```

### 手順 3 – JSON 形式の配列でデータ ソースを定義する

```csharp
// Anonymous object that mimics a JSON array
var dataModel = new { Orders = new[] { "A", "B", "C" } };
```

### 手順 4 – ワークブックを処理する

```csharp
// Fill the Smart Marker with the array data; the array becomes a comma‑separated string
smartMarkerProcessor.Process(workbook, dataModel);
```

### 手順 5 – 結果のワークブックを保存する

```csharp
// Persist the workbook; cell A1 now contains "A,B,C"
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
```

**結果の検証**: `JsonSingleCell.xlsx` を開き、セル A1 に `A,B,C` と表示されていることを確認してください。これは、コレクションを単一セル値として扱う方法を示すもので、下流システム向けにデータをエクスポートする際に頻繁に必要となります。

---

## 完全動作サンプル

以下は 3 つのシナリオを組み合わせた単一プログラムです。コードをコンソール アプリに貼り付け、ファイル パスを調整して実行すれば、すべての出力を確認できます。

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1. How to copy pivot table (preserve pivot cache)
        // -------------------------------------------------
        Workbook srcPivot = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Workbook dstPivot = new Workbook();
        srcPivot.Worksheets[0].Cells.CopyRows(0, 0, 20);
        srcPivot.Worksheets[0].Cells.CopyColumns(0, 0, 7);
        srcPivot.Worksheets[0].Copy(dstPivot.Worksheets[0]);
        dstPivot.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");

        // -------------------------------------------------
        // 2. Save workbook as PPTX with editable textbox
        // -------------------------------------------------
        Workbook txtWorkbook = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
        PptxSaveOptions pptxOpts = new PptxSaveOptions { ExportEditableTextBox = true };
        txtWorkbook.Save("YOUR_DIRECTORY/Result.pptx", pptxOpts);

        // -------------------------------------------------
        // 3. Export Smart Marker containing a JSON array
        // -------------------------------------------------
        SmartMarkerProcessor smProcessor = new SmartMarkerProcessor();
        Workbook smWorkbook = new Workbook();
        smWorkbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
        var model = new { Orders = new[] { "A", "B", "C" } };
        smProcessor.Process(smWorkbook, model);
        smWorkbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
    }
}
```

このプログラムを実行すると次のファイルが生成されます。

* `CopyWithPivot.xlsx` – 元のピボットテーブルを完全にコピーしたもの。  
* `Result.pptx` – 編集可能なテキストボックスを含む PowerPoint スライド。  
* `JsonSingleCell.xlsx` – JSON 配列が単一セルに表示されたシート。

---

## まとめ

これで **ピボットテーブルを安全にコピーする方法**、**ピボット付きワークシートを一括でコピーする方法**、そして **編集可能なテキストボックスを保持したままワークブックを pptx として保存する方法** が分かりました。これらのパターンは、エンタープライズ自動化プロジェクトで頻繁に遭遇する Excel‑to‑PowerPoint および Excel‑to‑JSON ワークフローの最も一般的なケースを網羅しています。

次に検討すべき項目:

* コピーしたピボットテーブルをプログラムでリフレッシュする (`PivotTable.Refresh()`)  
* PDF や HTML など他の形式へのエクスポート (`PdfSaveOptions`, `HtmlSaveOptions`)  
* カスタム関数や条件付き書式など高度な Smart Marker オプションの活用  

さまざまな範囲、複数シート、より大きな JSON 構造で実験してみてください。Aspose.Cells API は細かな制御を提供するため、これらの例を実際のシナリオに合わせて自由にカスタマイズできます。コーディングを楽しんでください！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを基にした関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、API の追加機能を習得したり、代替実装アプローチを探求したりするのに役立ちます。

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step‑By‑Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}