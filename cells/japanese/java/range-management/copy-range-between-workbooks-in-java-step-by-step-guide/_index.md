---
category: general
date: 2026-08-14
description: Aspose.Cells を使用した Java でブック間の範囲をコピーします。ピボットテーブルのブックをコピーし、画像を PowerPoint
  にエクスポートし、Excel テーブルから AutoFilter を削除する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range between workbooks
- copy pivot table workbook
- export picture to powerpoint
- copy excel range to new workbook
- remove autofilter from excel table
language: ja
lastmod: 2026-08-14
og_description: Javaでブック間の範囲をコピーする。このガイドでは、ピボットテーブルのブックをコピーし、画像をPowerPointにエクスポートし、ExcelテーブルからAutoFilterを削除する方法を示します。
og_image_alt: Screenshot of Java code copying range between workbooks with Aspose.Cells
og_title: Javaでワークブック間の範囲をコピー – 完全なAspose.Cellsチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Copy range between workbooks with Java using Aspose.Cells. Learn to
    copy pivot table workbook, export picture to PowerPoint and remove AutoFilter
    from Excel table.
  headline: Copy range between workbooks in Java – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Javaでブック間の範囲をコピーする – ステップバイステップガイド
url: /ja/java/range-management/copy-range-between-workbooks-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Javaでブック間の範囲をコピーする – ステップバイステップガイド

Javaで **ブック間の範囲をコピー** する必要がある場合、Aspose.Cells はピボットテーブルや画像などの複雑なオブジェクトを処理できるシンプルな API を提供します。このチュートリアルでは、**ピボットテーブルのブックをコピー**、**画像を PowerPoint にエクスポート**、そして **Excel テーブルから AutoFilter を削除** する方法を示しながら、コードを読みやすく保守しやすくします。

以下を学びます:

* ソースブックをロードし、ソース範囲を定義する。  
* 宛先ブックを作成し、範囲をコピーしてピボットテーブルをそのまま保持する。  
* シート上の最初の画像を編集可能な PowerPoint オブジェクトとしてエクスポートする。  
* 最初の Excel テーブルから AutoFilter を削除する。  
* `SmartMarkerOptions` を使用してブックをロードし、JSON 配列を単一セルの値として扱う。

この例は Aspose.Cells 23.10 for Java を使用していますが、概念は以前のバージョンでも適用できます。

---

## 前提条件

| 要件 | 重要な理由 |
|------|------------|
| Java 17 以降 | 最新の Aspose.Cells ランタイムで必要です。 |
| Aspose.Cells for Java (Maven artifact `com.aspose:aspose-cells`) | `Workbook`、`Worksheet`、`Range` など、コードで使用されるクラスを提供します。 |
| ピボットテーブル、画像、AutoFilter が設定されたテーブルを含むソース Excel ファイル (`src.xlsx`) | このチュートリアルではこれらのオブジェクトを操作して各機能を示します。 |

`pom.xml` に Maven 依存関係を追加します:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## ブック間で範囲をコピー – ソースと宛先のロード

最初のステップは、ソースブックを開き、コピーしたいデータが含まれる範囲を選択し、空の宛先ブックを作成することです。

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table, picture, and table.
        Workbook sourceWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceWs = sourceWb.getWorksheets().get(0);

        // Define the range that includes the pivot table (A1:G20 in this example).
        Range sourceRange = sourceWs.getCells().createRange("A1:G20");

        // Create a new workbook that will receive the copied range.
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
        Range destRange = destWs.getCells().createRange("A1");
```

> **なぜ重要か:** `Range.copy` を使用すると、Aspose.Cells は生のセル値だけでなく、基になるピボットキャッシュもコピーし、宛先ブックでピボットテーブルが機能し続けます。

---

## 範囲をコピーしながらピボットテーブルブックをコピー

次に、ソースブックから宛先ブックへ定義した範囲をコピーします。範囲にピボットキャッシュが含まれているため、ピボットテーブルは自動的に保持されます。

```java
        // Copy the source range to the destination range.
        destRange.copy(sourceRange);

        // Save the intermediate workbook to verify that the pivot table was copied.
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
```

> **結果:** `destination.xlsx` を開くと、`src.xlsx` と同じピボットテーブルのレイアウトが表示されます。ピボットキャッシュを再構築するための追加コードは不要です。

---

## 画像を PowerPoint にエクスポート

Aspose.Cells は画像を編集可能な PowerPoint オブジェクトとしてエクスポートするようマークできます。以下のコードは、宛先シート上の最初の画像を選択し、エクスポートフラグを設定します。

```java
        // Retrieve the first picture on the destination sheet.
        Shape picture = destWs.getPictures().get(0);

        // Instruct Aspose.Cells to export this picture as a PowerPoint object.
        picture.getPictureFormat().setExportToPptx(true);

        // Optionally, save the workbook as PPTX to see the result.
        destWb.save("YOUR_DIRECTORY/destination.pptx");
```

> **表示結果:** PowerPoint で `destination.pptx` を開くと、画像がネイティブなシェイプとして表示され、編集、サイズ変更、アニメーション付与が可能です。

---

## Excel テーブルから AutoFilter を削除

ソースシートに AutoFilter が設定されたテーブルがある場合、コピー後にそれをクリアしたくなることがあります。以下のコードは最初のテーブルにアクセスし、フィルターを削除します。

```java
        // Access the first table on the destination sheet.
        Table table = destWs.getTables().get(0);

        // Remove the AutoFilter by assigning null.
        table.setAutoFilter(null);

        // Save the final workbook.
        destWb.save("YOUR_DIRECTORY/final_output.xlsx");
```

> **効果:** テーブルはブック内に残りますが、ドロップダウンのフィルター矢印が消え、データがすっきりと表示されます。

---

## SmartMarker オプションでブックをロード – JSON 配列を単一セルとして扱う

JSON からレポートを生成する際、Aspose.Cells は配列全体を単一セルの値として扱うことができます。これにより、JSON 文字列をテンプレートに埋め込んでも、複数セルに展開されません。

```java
        // Configure LoadOptions to enable SmartMarker array handling.
        LoadOptions loadOptions = new LoadOptions();
        SmartMarkerOptions smOptions = new SmartMarkerOptions();
        smOptions.setArrayAsSingle(true);
        loadOptions.setSmartMarkerOptions(smOptions);

        // Load a template workbook using the configured options.
        Workbook smartMarkerWb = new Workbook("YOUR_DIRECTORY/template.xlsx", loadOptions);

        // Continue processing (e.g., populate markers) as needed.
        // ...

        // Save the processed workbook.
        smartMarkerWb.save("YOUR_DIRECTORY/template_filled.xlsx");
    }
}
```

> **使用例:** JSON ペイロードに単一セルに JSON 文字列として表示すべき配列が含まれる場合、`setArrayAsSingle(true)` を設定すると、Aspose.Cells が配列を別々の行や列に展開するのを防ぎます。

![Javaでブック間の範囲をコピー – Aspose.Cells コード例](copy-range-workbooks.png)

*Image alt text:* **Javaでブック間の範囲をコピー – Aspose.Cells コード例** (matches the primary keyword).

---

## 期待される出力

| ファイル名                | 内容 |
|--------------------------|------|
| `destination.xlsx`       | 機能するピボットテーブルを含むコピーされた範囲。 |
| `destination.pptx`       | 編集可能な PowerPoint シェイプとしてエクスポートされた画像。 |
| `final_output.xlsx`      | AutoFilter の矢印がないテーブル。 |
| `template_filled.xlsx`   | 単一セルの値として保存された JSON 配列。 |

各ファイルを適切なアプリケーション（Excel または PowerPoint）で開き、操作が成功したことを確認してください。

---

## 結論

これで、Aspose.Cells を使用して Java で **ブック間の範囲をコピー** する方法を理解できました。ピボットテーブルを保持し、画像を PowerPoint にエクスポートし、Excel テーブルから AutoFilter を削除することができます。同じパターンを応用すれば、任意の Excel 範囲を新しいブックにコピーしたり、SmartMarker の JSON 配列を処理したり、さらに変換を連鎖させることも可能です。

次に検討できるステップ:

* **Excel の範囲を新しいブックにコピー**（複数シート対応）。  
* バッチ画像抽出のために **export picture to PowerPoint** を使用します。  
* 大規模なレポートパイプラインで **remove autofilter from excel table** を適用します。  
* これらの手法を Aspose.Slides と組み合わせて、Excel から PowerPoint への完全な自動化を実現します。

さまざまな範囲アドレス、複数のピボットテーブル、カスタム画像形式で自由に試してみてください。Aspose.Cells API はプログラム的な柔軟性を念頭に設計されているため、ここで示したパターンを任意のエンタープライズ Excel 自動化シナリオに合わせて適用できます。

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.Cells for Java を使用した Excel のシート間で画像をコピーする完全ガイド](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Aspose.Cells Java を使用した Excel のワークシート間でページ設定をコピー](/cells/english/java/headers-footers/copy-page-setup-excel-aspose-cells-java/)
- [Excel のブック間でワークシートをコピー](/cells/english/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}