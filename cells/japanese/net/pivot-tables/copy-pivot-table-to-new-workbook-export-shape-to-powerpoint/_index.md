---
category: general
date: 2026-10-20
description: Aspose.Cells を使用してピボットテーブルを新しいブックにコピーし、1つのガイドで編集可能なシェイプを PowerPoint にエクスポートする方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table to new workbook
- copy rows between worksheets
- Aspose.Cells copy rows
- export shape to PowerPoint
- editable textbox in PowerPoint
language: ja
lastmod: 2026-10-20
og_description: Aspose.Cells を使用してピボットテーブルを新しいブックにコピーし、編集可能なシェイプを PowerPoint にエクスポートする—今日すぐに実行できるステップバイステップのコード。
og_image_alt: Screenshot showing copy pivot table to new workbook using Aspose.Cells
og_title: ピボットテーブルを新しいブックにコピーし、シェイプをPowerPointにエクスポート
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  headline: Copy pivot table to new workbook, export shape to PowerPoint
  type: TechArticle
- description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  name: Copy pivot table to new workbook, export shape to PowerPoint
  steps:
  - name: – Load the source workbook and select the first worksheet
    text: '```csharp // Load the workbook that already contains the pivot table Workbook
      srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");'
  - name: – Define the cell area that includes the pivot table
    text: '```csharp // CellArea(startRow, startColumn, endRow, endColumn) // Here
      we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table CellArea
      sourceArea = new CellArea(0, 0, 20, 10); ```'
  - name: – Create the destination workbook and get its first worksheet
    text: '```csharp // Create an empty workbook that will receive the copied range
      Workbook destWorkbook = new Workbook();'
  - name: – Copy the rows from the source area to the destination sheet
    text: '```csharp // CopyRows(startRow, endRow, destinationCells, destinationStartRow)
      srcWorksheet.Cells.CopyRows( sourceArea.StartRow, sourceArea.EndRow, destWorksheet.Cells,
      0); // start at row 0 in the destination sheet ```'
  - name: – Save the new workbook
    text: '```csharp destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx"); ```'
  - name: – Create a new workbook and access its first worksheet
    text: '```csharp Workbook workbook = new Workbook(); // Empty workbook Worksheet
      worksheet = workbook.Worksheets[0]; // First (and only) sheet ```'
  - name: – Add a textbox shape to the worksheet
    text: '```csharp // AddTextBox(startRow, startColumn, width, height, text) int
      shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
      ```'
  - name: – Retrieve the shape and modify its text
    text: '```csharp Shape textShape = worksheet.Shapes[shapeIndex]; textShape.Text
      = "Change me in PowerPoint"; ```'
  - name: – Save the workbook as a PowerPoint presentation
    text: '```csharp workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
      ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Pivot Table
- PowerPoint Export
title: ピボットテーブルを新しいブックにコピーし、シェイプをPowerPointにエクスポート
url: /ja/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ピボットテーブルを新しいブックにコピーし、シェイプを PowerPoint にエクスポート

機能を保持したまま **copy pivot table to new workbook** が必要な場合、このガイドでは Aspose.Cells を使用して正確に実行する方法を示します。また、**export an editable shape to PowerPoint** の最速の方法も紹介し、変換後もテキストボックスが編集可能なままになることを確認できます。

多くの開発者は、ピボットテーブルを含む範囲をコピーするとピボットロジックが失われる、またはシェイプが PPTX として保存すると静的画像になると想定しています。このチュートリアルはそれらの誤解を払拭し、信頼できる本番環境向けのソリューションを提供します。

以下のセクションで行うこと:

* ソースブックを読み込み、ピボットテーブルを含む範囲をコピーする。
* 同じピボットテーブルを含む宛先ブックを作成する。
* テキストボックスシェイプを追加しテキストを変更し、テキストボックスが編集可能なまま PowerPoint プレゼンテーションとしてブックを保存する。
* 各 API 呼び出しが必要な理由と、一般的な落とし穴を回避する方法を理解する。

**Prerequisites**

* .NET 6.0 以降（コードは .NET Framework 4.7+ でも動作します）。
* Aspose.Cells for .NET がインストール済み（`Install-Package Aspose.Cells`）。
* C# と Visual Studio（またはお好みの IDE）に関する基本的な知識。

---

## Copy pivot table to new workbook

このステップバイステップのセクションでは、ピボットテーブルを含む範囲をコピーし、新しいファイルでピボット定義を保持する方法を示します。

### Step 1 – Load the source workbook and select the first worksheet

```csharp
// Load the workbook that already contains the pivot table
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// The first worksheet (index 0) holds the pivot table we want to copy
Worksheet srcWorksheet = srcWorkbook.Worksheets[0];
```

*Why?*  
`Workbook` は Aspose.Cells におけるすべての Excel 操作のエントリーポイントです。正しいワークシートを選択することで、対象のピボットテーブルの位置で作業できることが保証されます。

### Step 2 – Define the cell area that includes the pivot table

```csharp
// CellArea(startRow, startColumn, endRow, endColumn)
// Here we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table
CellArea sourceArea = new CellArea(0, 0, 20, 10);
```

*Why?*  
ピボットテーブルは特定のセルブロック内に存在します。ピボット全体を包含する `CellArea` を指定することで、Aspose.Cells は基になるピボットキャッシュもコピー対象と認識します。

### Step 3 – Create the destination workbook and get its first worksheet

```csharp
// Create an empty workbook that will receive the copied range
Workbook destWorkbook = new Workbook();

// Destination worksheet (also index 0)
Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Why?*  
新規ブックを作成することで、名前付き範囲や既存のピボットと競合することがなく、コピー操作をクリーンに実行できます。

### Step 4 – Copy the rows from the source area to the destination sheet

```csharp
// CopyRows(startRow, endRow, destinationCells, destinationStartRow)
srcWorksheet.Cells.CopyRows(
    sourceArea.StartRow,
    sourceArea.EndRow,
    destWorksheet.Cells,
    0); // start at row 0 in the destination sheet
```

*Why?*  
`CopyRows` は **Aspose.Cells copy rows** API の一部です。セルの値だけでなく非表示のピボットキャッシュもコピーするため、移行後もピボットテーブルは機能し続けます。

### Step 5 – Save the new workbook

```csharp
destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Result*  
Excel で `CopyWithPivot.xlsx` を開きます。ピボットテーブルはソースファイルと全く同じ状態で表示され、通常通りリフレッシュや編集が可能です。

---

## Export editable shape to PowerPoint

ここではテキストボックスシェイプを追加し、内容を変更したうえでブックを PPTX ファイルとして保存します。PowerPoint で開いたときにシェイプは完全に編集可能なままです。

### Step 1 – Create a new workbook and access its first worksheet

```csharp
Workbook workbook = new Workbook();          // Empty workbook
Worksheet worksheet = workbook.Worksheets[0]; // First (and only) sheet
```

### Step 2 – Add a textbox shape to the worksheet

```csharp
// AddTextBox(startRow, startColumn, width, height, text)
int shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
```

*Why?*  
`AddTextBox` は **editable textbox in PowerPoint** 互換のシェイプを作成します。座標はポイント単位で指定されるため、レイアウトに合わせて調整してください。

### Step 3 – Retrieve the shape and modify its text

```csharp
Shape textShape = worksheet.Shapes[shapeIndex];
textShape.Text = "Change me in PowerPoint";
```

*Why?*  
`Shape` オブジェクトに直接アクセスすることで、`Text`、`Font`、`Fill` などのプロパティを変更できます。この手順はプログラムから初期コンテンツを設定する方法を示しています。

### Step 4 – Save the workbook as a PowerPoint presentation

```csharp
workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
```

*Result*  
Microsoft PowerPoint で `Presentation.pptx` を開きます。テキストボックスが最初のスライドに表示され、ダブルクリックすると任意のテキストを編集できる、ネイティブな PowerPoint シェイプと同様に扱えます。

---

## Expected output

| File | What you’ll see |
|------|-----------------|
| `CopyWithPivot.xlsx` | 元のピボットテーブルを含むワークシートが表示され、完全に機能します（リフレッシュが可能）。 |
| `Presentation.pptx` | 1 枚のスライドに「Change me in PowerPoint」と表示された編集可能なテキストボックスが配置されています。 |

---

## Common pitfalls and best‑practice tips

* **Pivot cache loss** – `CopyRows` に `PasteOptions` フラグで `PasteValues` を指定してセルの値だけをコピーすると、ピボットキャッシュが省かれテーブルが静的になります。必ず上記のようにデフォルトの `CopyRows` オーバーロードを使用してください。
* **Shape positioning** – `AddTextBox` はポイント単位で座標を指定し、Excel のセルインデックスではありません。スライド外に配置されないよう、サンプルファイルで座標をテストしましょう。
* **File format mismatch** – `SaveFormat.Pptx` でブックを PPTX として保存すると、サポートされているすべてのシェイプが自動的に変換されます。`Pdf` で保存しようとするとシェイプがラスタライズされ、編集できなくなります。

---

## Conclusion

これで **copy pivot table to new workbook** と **export an editable shape to PowerPoint** を Aspose.Cells for .NET を使って実現する方法が分かりました。完全な実行可能コード例は必要なすべての API 呼び出しを網羅し、各ステップの意図を解説し、期待される結果を示しています。

次に検討できるトピック:

* **Working with charts** – ピボットテーブルと一緒にチャートをコピーする方法（`Aspose.Cells copy rows between worksheets`）。

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示した手法を基にした関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、プロジェクトで代替実装を検討したりするのに役立ちます。

- [新しいブックの作成 – ピボットテーブル付きワークシートのコピー方法](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [ピボットテーブルをコピーして Excel を PPTX にエクスポートする (Aspose.Cells)](/cells/english/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/)
- [C# で新しいブックを作成 – ピボットテーブルのコピー](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}