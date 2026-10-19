---
category: general
date: 2026-10-10
description: Aspose.Cells を使用して Java で Excel の範囲を画像としてエクスポートする方法を学びます。このガイドでは、選択したセルを画像としてエクスポートする方法や、Excel
  ワークシートを画像として保存する方法もカバーしています。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- export selected cells as image
- save excel worksheet as picture
language: ja
lastmod: 2026-10-10
og_description: JavaでExcelの範囲を画像としてエクスポートするステップバイステップのソリューション。選択したセルを画像としてエクスポートし、Excelワークシートを画像として保存する機能を含む。
og_image_alt: Diagram showing export Excel range as image using Java and Aspose.Cells
og_title: JavaでExcelの範囲を画像としてエクスポート – 完全なAspose.Cellsガイド
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to export Excel range as image in Java using Aspose.Cells.
    The guide also covers export selected cells as image and save Excel worksheet
    as picture.
  headline: How to export Excel range as image in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to export Excel range as image in Java using Aspose.Cells.
    The guide also covers export selected cells as image and save Excel worksheet
    as picture.
  name: How to export Excel range as image in Java with Aspose.Cells
  steps:
  - name: Why this method matters
    text: '* **Separation of concerns:** Loading, option configuration, and exporting
      are clearly divided. * **Flexibility:** You can change the image format or DPI
      without touching the core logic. * **Error handling:** Throwing `Exception`
      lets the caller decide whether to log, retry, or abort.'
  - name: 1. Merged cells
    text: Aspose.Cells automatically preserves merged cell appearance, but if you
      need to control the rendering, set `options.setOnePagePerSheet(true)` to force
      the whole sheet onto a single page before exporting.
  - name: 2. Hidden rows or columns
    text: 'By default, hidden rows/columns are not rendered. To include them, enable:'
  - name: 3. Large ranges and memory consumption
    text: 'Exporting very large ranges can consume significant memory. If you encounter
      `OutOfMemoryError`, consider:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- Image export
title: Aspose.Cells を使用して Java で Excel の範囲を画像としてエクスポートする方法
url: /ja/java/images-shapes/how-to-export-excel-range-as-image-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java と Aspose.Cells を使用して Excel の範囲を画像としてエクスポートする方法

Excel の範囲を画像として **エクスポート**する必要がある場合、このチュートリアルでは Aspose.Cells ライブラリを使用した完全な Java ソリューションをご案内します。また、**選択したセルを画像としてエクスポート**する方法や、**Excel ワークシートを画像として保存**する方法も学べます。

ワークブックの一部を画像にエクスポートすれば、サードパーティ製のスクリーンショットツールが不要になり、ピクセル単位で完璧な結果が保証されます。本ガイドの最後までに、PNG（またはサポートされている任意の形式）を直接ディスクに書き込む再利用可能なメソッドを手に入れ、PDF、メール、Web ページへの組み込みがすぐにできるようになります。

## 前提条件

開始する前に、以下が揃っていることを確認してください。

* Java 17 以上がインストールされていること。
* Maven 3.8 以上（または Maven 依存関係を扱える他のビルドツール）。
* Aspose.Cells for Java のライセンス（無料評価版でも動作しますが透かしが入ります）。
* 既知のディレクトリに配置したサンプル Excel ファイル（`input.xlsx`）。

以下のセクションでは、基本的な Java 開発と Maven プロジェクトの設定に慣れていることを前提としています。

## 手順 1: プロジェクトに Aspose.Cells を追加する

`pom.xml` に Aspose.Cells の Maven 依存関係を追加します。このライブラリは、コード例で使用する `Workbook`、`Worksheet`、`ImageOrPrintOptions` クラスを提供します。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** バージョン番号は常に最新に保ちましょう。新しいリリースではフォーマットのサポートやパフォーマンスが向上しています。

## 手順 2: 範囲をエクスポートするユーティリティ メソッドを作成する

エクスポートロジックをメソッドにカプセル化すれば、プロジェクト間で簡単に再利用でき、結合セルや非表示行といったエッジケースも扱いやすくなります。

```java
import com.aspose.cells.*;

import java.io.File;

/**
 * Exports a specific cell range from an Excel worksheet to an image file.
 *
 * @param workbookPath   Full path to the source .xlsx file.
 * @param sheetIndex     Zero‑based index of the worksheet (0 = first sheet).
 * @param range          A‑style range string, e.g. "A1:G20".
 * @param outputPath     Full path where the image will be saved.
 * @param imageFormat    Desired image format (PNG, JPEG, BMP, etc.).
 * @throws Exception if the file cannot be read or written.
 */
public static void exportRangeAsImage(
        String workbookPath,
        int sheetIndex,
        String range,
        String outputPath,
        ImageFormat imageFormat) throws Exception {

    // Load the workbook
    Workbook wb = new Workbook(workbookPath);

    // Obtain the requested worksheet
    Worksheet ws = wb.getWorksheets().get(sheetIndex);

    // Configure image export options
    ImageOrPrintOptions options = new ImageOrPrintOptions();
    options.setImageFormat(imageFormat);
    // Optional: increase DPI for higher‑resolution output
    options.setHorizontalResolution(300);
    options.setVerticalResolution(300);

    // Export the defined range as an image file
    ws.getCells().exportRangeAsImage(range, outputPath, options);
}
```

### このメソッドが重要な理由

* **Separation of concerns:** 読み込み、オプション設定、エクスポートが明確に分離されています。
* **Flexibility:** 画像形式や DPI をコアロジックに手を加えずに変更できます。
* **Error handling:** `Exception` をスローすることで、呼び出し側がログ記録、再試行、または中止を自由に判断できます。

## 手順 3: 実際のパラメータでメソッドを呼び出す

以下は最小限の `main` メソッドです。**選択したセルを画像としてエクスポート**する方法と、シート全体の範囲を使用して **Excel ワークシートを画像として保存**する方法の両方を示しています。

```java
public class ExcelImageExporter {
    public static void main(String[] args) {
        try {
            String inputFile   = "C:/Data/input.xlsx";
            String outputFile1 = "C:/Data/range.png";
            String outputFile2 = "C:/Data/full_sheet.png";

            // Export a specific range (A1:G20)
            exportRangeAsImage(
                    inputFile,
                    0,                  // first worksheet
                    "A1:G20",
                    outputFile1,
                    ImageFormat.PNG);   // primary format for lossless quality

            // Export the entire first worksheet – effectively saving the worksheet as picture
            exportRangeAsImage(
                    inputFile,
                    0,
                    "A1:" + getLastCellAddress(inputFile, 0), // compute last used cell
                    outputFile2,
                    ImageFormat.PNG);

            System.out.println("Images generated successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    /**
     * Helper that returns the address of the last used cell in a worksheet.
     */
    private static String getLastCellAddress(String workbookPath, int sheetIdx) throws Exception {
        Workbook wb = new Workbook(workbookPath);
        Worksheet ws = wb.getWorksheets().get(sheetIdx);
        // Find the maximum row and column that contain data
        int maxRow = ws.getCells().getMaxDataRow();
        int maxCol = ws.getCells().getMaxDataColumn();
        // Convert column index to A‑style letter (0 -> A)
        String colLetter = CellReference.convertNumToColString(maxCol);
        return colLetter + (maxRow + 1);
    }
}
```

#### 期待される出力

プログラムを実行すると、2 つの PNG ファイルが作成されます。

* `range.png` – **A1:G20** のセルだけを含む画像。
* `full_sheet.png` – 最初のワークシートの使用領域全体を画像化したもので、実質的に **Excel ワークシートを画像として保存**した結果です。

任意の画像ビューアでファイルを開き、セルの枠線、色、結合セルなどが Excel の表示と一致していることを確認できます。

## 手順 4: 一般的なエッジケースを処理する

### 1. 結合セル

Aspose.Cells は結合セルの外観を自動的に保持しますが、レンダリングを制御したい場合は `options.setOnePagePerSheet(true)` を設定して、エクスポート前にシート全体を 1 ページに強制してください。

### 2. 非表示の行または列

デフォルトでは、非表示の行・列は描画されません。これらも含めたい場合は、以下を有効にします。

```java
options.setSkipEmptyRows(false);
options.setSkipEmptyColumns(false);
```

### 3. 大きな範囲とメモリ消費

非常に大きな範囲をエクスポートすると、メモリ使用量が大幅に増加します。`OutOfMemoryError` が発生した場合は、次の対策を検討してください。

* DPI を下げる（`options.setHorizontalResolution(150)`）。
* 範囲を小さなチャンクに分割してエクスポートし、グラフィックライブラリで画像を結合する。

## 手順 5: プログラムで結果を検証する（オプション）

下流プロセスで画像が正しく生成されたか確認する必要がある場合、`javax.imageio.ImageIO` で PNG を読み込み、寸法をチェックできます。

```java
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;

BufferedImage img = ImageIO.read(new File(outputFile1));
System.out.println("Image width: " + img.getWidth() + " px");
System.out.println("Image height: " + img.getHeight() + " px");
```

幅と高さが 0 でなければ、エクスポートは成功しています。

## 結論

これで、Java で **Excel の範囲を画像としてエクスポート**する方法、**選択したセルを画像としてエクスポート**する方法、そして Aspose.Cells を使用して **Excel ワークシートを画像として保存**する方法が分かりました。再利用可能な `exportRangeAsImage` メソッドは複雑さを抽象化し、画像品質を制御でき、任意のワークシートインデックスやセル範囲に対応します。

次に検討できるステップ:

* Aspose.PDF を使って PNG を PDF に変換し、レポート作成に利用する。
* ディレクトリ内の複数ワークブックをバッチ処理する。
* 画像エクスポート機能を Spring Boot の REST エンドポイントに統合し、クライアントがオンデマンドで画像を取得できるようにする。

`ImageFormat.JPEG`、`ImageFormat.BMP` などの異なる画像形式や DPI 設定を試して、プロジェクトのビジュアル要件に合わせてください。コーディングを楽しんでください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックをカバーしています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [Export Excel Workbook as Image Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Export Excel Cells to Image Using Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}