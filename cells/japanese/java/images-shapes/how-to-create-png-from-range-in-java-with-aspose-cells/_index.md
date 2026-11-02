---
category: general
date: 2026-10-07
description: Javaで範囲からPNGを作成し、データをPNGとしてエクスポートする方法を学びます。このガイドでは、Aspose.Cells を使用して
  Excel の範囲画像を保存する手順を示します。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from range
- export data as png
- save excel range image
- convert worksheet to png
- save cells as png
language: ja
lastmod: 2026-10-07
og_description: Javaで範囲からPNGを作成し、Aspose.CellsでデータをPNGとしてエクスポートします。この完全なチュートリアルに従って、Excelの範囲画像を即座に保存しましょう。
og_image_alt: Screenshot of Java code that creates a PNG from an Excel range
og_title: Javaで範囲からPNGを作成 – ステップバイステップ Aspose.Cells ガイド
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  headline: How to create PNG from range in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  name: How to create PNG from range in Java with Aspose.Cells
  steps:
  - name: Maven dependency
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-cells</artifactId>
      <version>23.12</version> </dependency> ```'
  - name: Expected output
    text: '* A file named `PivotImage.png` located in `YOUR_DIRECTORY`. * The image
      shows the exact layout, fonts, colors, and borders from the selected range.
      * If the source range contains a pivot table, the rendered image includes the
      same styling and calculated values as displayed in Excel.'
  - name: Exporting a non‑contiguous range
    text: Aspose.Cells does not render disjoint ranges in a single image. To export
      multiple areas, create separate images for each range and combine them later
      with an image‑processing library (e.g., ImageIO).
  - name: Saving a large worksheet as PNG
    text: 'Rendering an entire sheet that spans thousands of rows can consume significant
      memory. Mitigate this by:'
  - name: Preserving cell formulas
    text: A PNG image is a raster format; formulas are not retained. If downstream
      consumers need the raw data, also export the range as CSV or JSON using `Range.exportDataTable()`.
  - name: Next steps
    text: '* Experiment with different `Resolution` values to balance quality and
      file size. * Use `ImageOrPrintOptions.setTransparent(true)` if you need a PNG
      with a transparent background. * Combine multiple range images into a single
      PDF using `PdfSaveOptions` for multi‑page reports. * Explore exporting to '
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Aspose.Cells を使用して Java で範囲から PNG を作成する方法
url: /ja/java/images-shapes/how-to-create-png-from-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java と Aspose.Cells を使用して範囲から PNG を作成する方法

Excel ワークブック内の **範囲から PNG を作成** したい場合、本チュートリアルで手順を詳しく解説します。ガイドを最後まで読むと、**データを PNG としてエクスポート** し、Excel の範囲画像を保存してレポートや Web ページで再利用できるようになります。

ワークブックを読み込み、目的のセルを選択し、PNG としてレンダリングし、ディスクに保存する完全な実行可能 Java プログラムを示します。外部ツールは不要で、Aspose.Cells がすべて内部で処理します。

## 本チュートリアルでカバーする内容

* Aspose.Cells の前提条件と Maven 設定
* ピボットテーブルまたは任意のデータ範囲を含むワークブックの読み込み
* 変換したい正確なセル範囲の定義
* PNG 出力用の画像オプション設定
* 範囲をレンダリングして PNG ファイルとして保存
* 高品質画像作成のための一般的な落とし穴とヒント

これらの手順を完了すれば、**ワークシートを PNG に変換** できるようになり、シンプルなテーブルから複雑なピボットチャートまで、任意の範囲を画像化できます。

## 前提条件

* Java 17 以降（コードは JDK 11+ でもコンパイル可能）
* Maven 3.6+（または好みで Gradle）
* Aspose.Cells for Java 23.12 以上 – 以下の依存関係を追加してください
* 取得したい範囲を含む既存の Excel ファイル（`PivotWithStyle.xlsx`）

> **Pro tip:** ライセンスをお持ちでない場合は、Aspose から一時的な評価キーをリクエストできます。評価モードでも追加設定なしでライブラリは動作します。

### Maven 依存関係

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

## 手順 1: 対象範囲を保持するワークブックをロード

最初の操作は Excel ファイルを開くことです。Aspose.Cells は Microsoft Office を必要とせずにファイルをメモリに読み込みます。

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the data you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");
```

*重要ポイント*: ワークブックをロードすると、レンダリングに必要なワークシート、セル、ページ設定プロパティへアクセスできるようになります。

## 手順 2: 範囲を含むワークシートにアクセス

ほとんどのワークブックはインデックス 0 にデフォルトシートがありますが、シート名を使用することも可能です。

```java
        // Retrieve the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

別シートにデータがある場合は、`0` を該当インデックスに置き換えるか、`workbook.getWorksheets().get("SheetName")` を使用してください。

## 手順 3: 変換したいセル範囲を定義

A1 形式で任意の矩形領域を指定できます。この例では `A1:D15` を取得します。ピボットテーブルでも通常のデータブロックでも構いません。

```java
        // Create a range object for cells A1:D15
        Range pivotRange = worksheet.getCells().createRange("A1:D15");
```

*エッジケース*: 範囲に結合セルが含まれる場合、Aspose.Cells は自動的に結合領域全体を画像に拡張します。

## 手順 4: PNG 画像オプションを準備

`ImageOrPrintOptions` でフォーマット、解像度、その他のレンダリング詳細を制御できます。保存形式を PNG に設定するとロスレス品質が保証されます。

```java
        // Configure image options – we want a PNG file
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        // Optional: increase DPI for sharper output (default is 96)
        imageOptions.setImageFormat(ImageFormat.getPng());
        imageOptions.setResolution(150); // 150 DPI for clearer text
```

フォントが小さい、または詳細なチャートが含まれる場合は DPI を上げると見栄えが向上します。

## 手順 5: レンダー領域を選択した範囲に限定

レンダリング領域を印刷領域として設定することで、Aspose.Cells はそのセルだけを描画し、シートの残りは無視します。

```java
        // Set the print area so only the defined range is rendered
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());
```

この手順を省略すると、シート全体がラスタライズされ、メモリ消費が増大し、画像サイズも大きくなります。

## 手順 6: 範囲をレンダリングし、ワークシートに画像を追加（オプション）

生成した PNG をワークブックに埋め込み（プレビュー目的など）たい場合は、画像としてシートに追加できます。このステップは純粋なエクスポートシナリオでは任意です。

```java
        // Add the rendered image back to the worksheet at cell (0,0) – optional
        worksheet.getPictures().add(0, 0, imageOptions);
```

*なぜ行うか*: 配布前に画像をワークブックに組み込む必要があるワークフロー（例: ネイティブセルと画像を混在させた印刷レポート作成）があります。

## 手順 7: PNG ファイルをディスクに保存

最後に画像をファイルへ書き出します。`save` メソッドは `imageOptions` で指定したフォーマットを尊重します。

```java
        // Save the rendered PNG image to the specified path
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

プログラムが終了すると、`PivotImage.png` にセル `A1:D15` のピクセルパーフェクトなスナップショットが保存されます。

### 期待される出力

* `YOUR_DIRECTORY` 配下に作成される `PivotImage.png` ファイル
* 画像は選択範囲のレイアウト、フォント、色、罫線を正確に再現
* ソース範囲がピボットテーブルの場合、レンダリング画像は Excel 上のスタイリングと計算結果を同様に表示

## 一般的なシナリオの取り扱い

### 連続しない範囲のエクスポート

Aspose.Cells は単一画像で不連続範囲をレンダリングできません。複数領域をエクスポートする場合は、各範囲ごとに別画像を作成し、後で ImageIO などの画像処理ライブラリで結合してください。

```java
Range first = worksheet.getCells().createRange("A1:B10");
Range second = worksheet.getCells().createRange("D1:E10");
// Render each range individually using the same ImageOrPrintOptions
```

### 大規模シートを PNG として保存

数千行にわたるシート全体をレンダリングするとメモリ消費が大きくなります。対策として:

* DPI を下げる（例: `imageOptions.setResolution(72)`）ことでファイルサイズを縮小
* `setPageCount` でレンダリングページ数を制限
* `worksheet.getPageSetup().setPrintArea(...)` を使用し、1 ページずつ印刷領域を設定してエクスポート

### セル数式の保持

PNG はラスタ形式のため、数式は保持されません。下流で生データが必要な場合は、`Range.exportDataTable()` などで CSV や JSON としてもエクスポートしてください。

## 完全な実行可能サンプル

以下は IDE にコピペできる完全な Java クラスです。`YOUR_DIRECTORY` を環境に合わせた絶対パスまたは相対パスに置き換えてください。

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the workbook containing the data
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");

        // 2️⃣ Access the first worksheet (adjust index or name as needed)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Define the exact cell range you want to convert (A1:D15 in this case)
        Range pivotRange = worksheet.getCells().createRange("A1:D15");

        // 4️⃣ Prepare PNG image options – set format and optional resolution
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        imageOptions.setResolution(150); // sharper output

        // 5️⃣ Restrict rendering to the selected range
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());

        // 6️⃣ (Optional) Add the rendered image back to the worksheet for preview
        worksheet.getPictures().add(0, 0, imageOptions);

        // 7️⃣ Save the PNG file – this creates the final image on disk
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

`mvn compile exec:java`（またはお好みのビルドツール）でプログラムを実行し、完了後に `PivotImage.png` を開いて結果を確認してください。

## 結論

これで **Java と Aspose.Cells を使用して範囲から PNG を作成** する方法が習得できました。**データを PNG としてエクスポート** し、**Excel 範囲画像を保存** する一連の手順（ワークブックのロード、範囲の定義、画像オプションの設定、印刷領域の指定、ファイル保存）により、**ワークシートを PNG に変換** し **セルを PNG として保存** するフローが完成します。

### 次のステップ

* 品質とファイルサイズのバランスを取るために、さまざまな `Resolution` 値を試す
* 背景を透明にした PNG が必要な場合は `ImageOrPrintOptions.setTransparent(true)` を使用
* 複数の範囲画像を `PdfSaveOptions` で単一 PDF に結合し、マルチページレポートを作成
* `setSaveFormat` を変更すれば JPEG、BMP など他のラスタ形式へのエクスポートも可能

このパターンをチャート、テーブル、あるいはシート全体にも応用してみてください。Happy coding!

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックをカバーしています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、API の追加機能習得や代替実装アプローチの探索に役立ちます。

- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Convert Excel to PNG Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/workbook-operations/convert-excel-to-png-aspose-cells-java/)
- [Create Union Range in Excel using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/range-management/create-union-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}