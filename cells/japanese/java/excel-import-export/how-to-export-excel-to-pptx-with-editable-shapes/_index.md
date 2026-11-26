---
category: general
date: 2026-11-25
description: 編集可能なシェイプを含むExcelをPPTXにエクスポートする方法を学びましょう。このガイドでは、印刷範囲の設定方法と、プレゼンテーション用にExcelチャートを変換する方法も紹介しています。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel
- set print area
- how to convert xlsx
- set print area excel
- convert excel chart
language: ja
lastmod: 2026-11-25
og_description: Aspose.Cells を使用して、編集可能なシェイプ付きで Excel を PPTX にエクスポートする方法、印刷範囲の設定やプレゼンテーション用に
  Excel グラフを変換するヒントも紹介。
og_image_alt: Screenshot showing how to export Excel to PPTX with editable shapes
og_title: Excelを編集可能なシェイプ付きでPPTXにエクスポートする方法
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to export Excel to PPTX with editable shapes. This guide
    also shows how to set print area and convert Excel chart for presentations.
  headline: How to export Excel to PPTX with editable shapes
  type: TechArticle
- description: Learn how to export Excel to PPTX with editable shapes. This guide
    also shows how to set print area and convert Excel chart for presentations.
  name: How to export Excel to PPTX with editable shapes
  steps:
  - name: '**Dependency** – Aspose.Cells provides the `ImageOrPrintOptions` class
      that can render worksheets as PPTX slides. Adding it via Maven ensures the library
      is on the classpath.'
    text: '**Dependency** – Aspose.Cells provides the `ImageOrPrintOptions` class
      that can render worksheets as PPTX slides. Adding it via Maven ensures the library
      is on the classpath.'
  - name: '**Imports** – Importing the right classes keeps the code clean and avoids
      fully‑qualified names.'
    text: '**Imports** – Importing the right classes keeps the code clean and avoids
      fully‑qualified names.'
  - name: '**Loading the workbook** – You must point to the exact file that contains
      the objects you want to export. The path can be absolute or relative to the
      project root.'
    text: '**Loading the workbook** – You must point to the exact file that contains
      the objects you want to export. The path can be absolute or relative to the
      project root.'
  - name: '**Export options** – Setting `setEditable(true)` is the key to **how to
      export Excel** so that the resulting PowerPoint shapes remain editable. Without
      this flag, text boxes become static images.'
    text: '**Export options** – Setting `setEditable(true)` is the key to **how to
      export Excel** so that the resulting PowerPoint shapes remain editable. Without
      this flag, text boxes become static images.'
  - name: '**Print area** – The `setPrintArea` call limits the export to the region
      you care about, which reduces file size and removes unwanted rows/columns. This
      directly addresses the **set print area excel** requirement.'
    text: '**Print area** – The `setPrintArea` call limits the export to the region
      you care about, which reduces file size and removes unwanted rows/columns. This
      directly addresses the **set print area excel** requirement.'
  - name: '**Saving** – The `SaveFormat.PPTX` constant tells Aspose.Cells to generate
      a PowerPoint file rather than an image or PDF.'
    text: '**Saving** – The `SaveFormat.PPTX` constant tells Aspose.Cells to generate
      a PowerPoint file rather than an image or PDF.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Excel を PPTX に、編集可能な図形付きでエクスポートする方法
url: /ja/java/excel-import-export/how-to-export-excel-to-pptx-with-editable-shapes/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel を編集可能なシェイプ付きで PPTX にエクスポートする方法

PowerPoint にエクスポートする際に、編集可能なテキストボックスやシェイプを保持したまま **how to export Excel** ファイルを変換したい場合、本ガイドではその全手順を解説します。また、スライドを絞り込むための **set print area** の設定方法や、エクスポート後も完全に編集可能なままにする **convert Excel chart** オブジェクトの変換方法も学べます。

データ駆動型レポートからプレゼンテーション資料を作成する際、Excel を PPTX にエクスポートすることは一般的です。Aspose.Cells for Java を使用すれば、手動でのコピー＆ペーストを回避し、書式をそのまま保持しつつ、出力をプログラムで制御できます。

## 学習内容

* テキストボックスまたはチャートを含む既存の XLSX ワークブックを読み込む。  
* エクスポートオプションを設定し、生成される PPTX ファイルに **editable shapes** が含まれるようにする。  
* **Set the print area** を使用して、エクスポート範囲を必要なセルに限定する。  
* ワークシートを PPTX ファイルとして保存し、PowerPoint でテキストボックスやチャートが編集可能であることを確認する。  

**前提条件**

* Java 17 以降がインストールされていること。  
* 依存関係管理に Maven または Gradle を使用できること。  
* Excel ワークブックと Java プログラミングの基本的な理解があること。

---

## 編集可能なシェイプ付きで Excel を PPTX にエクスポートする方法

このセクションでは、エクスポートを実行するコアコードを示します。例では執筆時点での最新バージョンである Aspose.Cells 23.9 を使用し、必要な手順をすべて実演します。

```java
// ------------------------------------------------------------
// 1. Add Aspose.Cells dependency (Maven example)
// ------------------------------------------------------------
/*
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
*/

// ------------------------------------------------------------
// 2. Import required classes
// ------------------------------------------------------------
import com.aspose.cells.*;

public class ExcelToPptxExporter {

    public static void main(String[] args) throws Exception {
        // --------------------------------------------------------
        // 3. Load the workbook that contains a text box or chart
        // --------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/WithTextBox.xlsx");

        // --------------------------------------------------------
        // 4. Set up export options for PPTX and enable shape editing
        // --------------------------------------------------------
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setFormat(ImageFormat.PPTX);          // output format
        exportOptions.setExportType(ExportType.PPTX);      // explicit PPTX export
        exportOptions.setEditable(true);                   // makes text boxes/shapes editable

        // --------------------------------------------------------
        // 5. Define the print area to limit the exported range
        // --------------------------------------------------------
        // This is the **set print area** step. Adjust the range as needed.
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:H30");

        // --------------------------------------------------------
        // 6. Save the first worksheet as an editable PPTX file
        // --------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/EditableShapes.pptx", SaveFormat.PPTX);

        System.out.println("Export completed: EditableShapes.pptx");
    }
}
```

### 各行が重要な理由

1. **Dependency** – Aspose.Cells はワークシートを PPTX スライドとしてレンダリングできる `ImageOrPrintOptions` クラスを提供します。Maven で追加すれば、ライブラリがクラスパスに含まれます。  
2. **Imports** – 正しいクラスをインポートすることでコードがすっきりし、完全修飾名の使用を回避できます。  
3. **Loading the workbook** – エクスポートしたいオブジェクトが含まれる正確なファイルを指定する必要があります。パスは絶対パスでもプロジェクトルートからの相対パスでも構いません。  
4. **Export options** – `setEditable(true)` を設定することが **how to export Excel** の鍵であり、生成された PowerPoint のシェイプが編集可能なままになります。このフラグがないと、テキストボックスは静的画像になります。  
5. **Print area** – `setPrintArea` 呼び出しにより、エクスポート対象を関心のある領域に限定でき、ファイルサイズが削減され、不要な行・列が除外されます。これは **set print area excel** の要件に直接対応します。  
6. **Saving** – `SaveFormat.PPTX` 定数は、Aspose.Cells に画像や PDF ではなく PowerPoint ファイルを生成するよう指示します。  

#### 期待される出力

プログラムを実行したら、PowerPoint で `EditableShapes.pptx` を開きます。選択した Excel 範囲を反映したスライドが表示され、テキストボックスやチャートの凡例はダブルクリックでネイティブの PowerPoint オブジェクトと同様に編集可能です。

---

## Excel で印刷範囲を設定する

ワークシートの一部だけが必要な場合、**print area** を定義することでパフォーマンスと視覚的な明瞭さが向上します。

```java
// Example: set print area to the first 10 rows and columns A‑J
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.getPageSetup().setPrintArea("A1:J10");
```

*Tip:* 後でデータ範囲を変更した場合は、エクスポート前に再度 `setPrintArea` を呼び出してください。エクスポートは最新の設定を尊重します。

---

## XLSX のチャートを編集可能な PowerPoint チャートに変換する

Aspose.Cells はチャートを描画オブジェクトとして扱います。`setEditable(true)` を有効にすると、チャートはネイティブの PowerPoint チャートに変換され、シリーズや軸タイトルの変更などが可能になります。

```java
// No extra code needed – the same exportOptions handle chart conversion.
// Just ensure the workbook contains a chart object.
```

複数のチャートを含む **how to convert xlsx** ファイルが必要な場合は、各ワークシートごとにエクスポートを繰り返すか、アクティブシートを調整した後に `Workbook.save` と `SaveFormat.PPTX` を使用してください。

---

## プログラムで XLSX を変換する方法（ボーナス）

PPTX 以外にも、ワークブックを PDF や PNG など別の形式に変換したい場合があります。同じ `ImageOrPrintOptions` クラスがそれらのターゲットでも機能します。

```java
exportOptions.setFormat(ImageFormat.PDF);   // for PDF output
workbook.save("Converted.pdf", SaveFormat.PDF);
```

これは Aspose.Cells の幅広い **how to convert xlsx** 機能を示しています。

---

## よくある落とし穴とベストプラクティスのヒント

| 問題 | 発生理由 | 対策 |
|------|----------|------|
| シェイプが画像になる | `setEditable(false)` (default) | `exportOptions.setEditable(true)` を呼び出す |
| エクスポートされたスライドが空白になる | 印刷範囲にデータが含まれていない | `setPrintArea` に渡す範囲文字列を確認する |
| チャートの書式が失われる | 古いバージョンの Aspose.Cells を使用している | 最新のライブラリ (≥ 23.9) にアップグレードする |
| ファイルサイズが大きくなる | ワークシート全体をエクスポートしている | 印刷範囲を限定するか、未使用の行・列を非表示にする |

---

## 結論

これで、**how to export Excel** のワークブックを完全に編集可能なシェイプとチャート付きで PPTX にエクスポートする方法、出力を絞り込むための **set print area** の設定方法、そしてプレゼンテーション編集をシームレスに行えるように **convert Excel chart** オブジェクトを変換する方法が分かりました。上記の完全な実行可能な Java サンプルは、Aspose.Cells を既に使用しているプロジェクトにそのまま組み込むことができます。

**次のステップ**

* PowerPoint の **convert excel chart** オプションを調査する（例：チャートタイプの変更）。  
* このエクスポートと **set print area excel** の自動化を組み合わせて、1 つのワークブックから複数のスライドを生成する。  
* 同じ `ImageOrPrintOptions` パターンを使用して、他の形式（PDF、PNG）へのエクスポートを試す。

さまざまな範囲や複数のワークシート、カスタムスライドレイアウトで自由に試してみてください。コーディングを楽しんで！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [How to set print area excel and export to PowerPoint](/cells/english/java/excel-import-export/how-to-set-print-area-excel-and-export-to-powerpoint/)
- [Convert Excel to PowerPoint and set print area](/cells/english/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/)
- [Set Print Area in Excel and Export to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}