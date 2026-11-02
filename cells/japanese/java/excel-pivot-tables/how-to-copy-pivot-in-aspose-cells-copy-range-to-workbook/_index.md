---
category: general
date: 2026-08-08
description: Aspose.Cellsでピボットテーブルをコピーし、Javaを使用して範囲をワークブックにコピーする方法。CopyOptions を使ってピボットテーブルを複製する正確な手順を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range to workbook
- aspose.cells copy range
language: ja
lastmod: 2026-08-08
og_description: Aspose.Cellsでピボットテーブルをコピーし、Javaで範囲をワークブックにコピーする方法。CopyOptionsを使用してピボットテーブルを複製する完全ガイドをご覧ください。
og_image_alt: Diagram showing how to copy pivot in Aspose.Cells
og_title: Aspose.Cellsでピボットテーブルをコピーする方法 – 範囲をワークブックにコピー
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  headline: How to copy pivot in Aspose.Cells – copy range to workbook
  type: TechArticle
- description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  name: How to copy pivot in Aspose.Cells – copy range to workbook
  steps:
  - name: Add Aspose.Cells to your project
    text: 'If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Configure copy options to include the pivot table
    text: '```java // Define copy options to include the pivot table in the copied
      range CopyOptions copyOptions = new CopyOptions() .setCopyPivotTable(true);
      ```'
  - name: Copy the desired range with the pivot table
    text: '```java // Copy the range A1:H20, preserving the pivot table workbook.getWorksheets().get(0).getCells()
      .copyRange("A1:H20", copyOptions); ```'
  - name: Save the modified workbook
    text: '```java // Save the workbook with the copied pivot table workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected result
    text: '* `output.xlsx` contains the same data as `input.xlsx`. * The pivot table
      that originally occupied the source range appears in the destination cells,
      fully functional (filters, refresh capability, etc.). * All cell formatting,
      formulas, and column widths are preserved because `copyRange` copies the '
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- CopyRange
title: Aspose.Cellsでピボットをコピーする方法 – 範囲をワークブックにコピー
url: /ja/java/excel-pivot-tables/how-to-copy-pivot-in-aspose-cells-copy-range-to-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cellsでピボットをコピーする方法 – 範囲をブックにコピー

Aspose.Cellsを使用してExcelファイルで**ピボットをコピーする方法**が必要な場合、このガイドでは正確な手順を示します。チュートリアルの最後までに、**範囲をブックにコピー**し、ピボットテーブルの定義を保持できるようになります。

この例はJavaを使用していますが、同じ概念はAspose.Cellsで動作する任意の.NET言語にも適用できます。外部ツールは不要で、Aspose.Cells for Javaライブラリと基本的な開発環境だけで十分です。

## 前提条件

* Java Development Kit (JDK) 8 以上。
* Maven または Gradle を使用して依存関係を管理（例では Maven を使用）。
* Aspose.Cells for Java 23.9（または最新バージョン）をプロジェクトに追加。
* 最初のワークシートに少なくとも1つのピボットテーブルが含まれる入力ブック (`input.xlsx`)。

これらの項目を準備しておくことで、コードがブックにアクセスする際のランタイムエラーを防止できます。

## Aspose.Cellsでピボットをコピーする方法

このセクションでは、シートのある部分から別の部分へ**ピボットをコピーする方法**を、`CopyOptions` クラスを使用してステップごとに説明します。

### 手順 1: プロジェクトに Aspose.Cells を追加

Maven を使用している場合、以下の依存関係を `pom.xml` に追加してください。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust JDK version as needed -->
</dependency>
```

*このステップが重要な理由*: ライブラリは **aspose.cells copy range** 操作に必要な `Workbook`、`CopyOptions` などのクラスを提供します。依存関係がなければ、コンパイラはこれらの型を解決できません。

### 手順 2: ソースブックをロード

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

ファイルをロードすると、スプレッドシートのメモリ内表現が作成されます。`Workbook` オブジェクトを使用してワークシート、セル、ピボットテーブルにアクセスできます。

### 手順 3: ピボットテーブルを含めるようにコピーオプションを設定

```java
        // Define copy options to include the pivot table in the copied range
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);
```

`CopyOptions.setCopyPivotTable(true)` は、操作がピボットテーブルのメタデータを保持すべきであることを Aspose.Cells に指示します。このフラグを省略すると、ピボットテーブルは静的データに変換され、インタラクティブ性が失われます。

### 手順 4: ピボットテーブルを含む対象範囲をコピー

```java
        // Copy the range A1:H20, preserving the pivot table
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);
```

`copyRange` メソッドはセルと書式をコピーし、前のステップで設定したオプションにより、範囲と交差するすべてのピボットテーブルもコピーします。これが **copy range to workbook** 機能の核心です。

### 手順 5: 変更されたブックを保存

```java
        // Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

保存すると、変更が新しいファイル (`output.xlsx`) に書き込まれます。これで Excel でファイルを開くと、範囲がコピーされた場所にピボットテーブルが正確に複製されていることが確認できます。

## 完全な実行可能サンプル

すべての要素を組み合わせた、コンパイルして実行できる完全なプログラムは以下の通りです。

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Define copy options to include the pivot table
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);

        // 3. Copy the range A1:H20 with the specified options
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);

        // 4. Save the modified workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### 期待される結果

* `output.xlsx` は `input.xlsx` と同じデータを含みます。
* 元のソース範囲にあったピボットテーブルが、宛先セルに出現し、完全に機能します（フィルター、更新機能など）。
* `copyRange` がセルブロック全体をコピーするため、すべてのセル書式、数式、列幅が保持されます。

## よくある質問とエッジケース

**宛先範囲が既存のピボットテーブルと重なる場合はどうなりますか？**  
Aspose.Cells は対象セルを上書きします。データ損失を防ぐため、宛先領域が空であることを確認するか、事前に既存のピボットテーブルを移動してください。

**ワークシート間でピボットテーブルをコピーできますか？**  
はい。`targetSheetIndex` が宛先シートを指すように、`workbook.getWorksheets().get(targetSheetIndex).getCells().copyRange(sourceRange, copyOptions);` を使用します。

**`setCopyPivotTable(true)` は基になるデータソースもコピーしますか？**  
このメソッドはピボットキャッシュの参照のみをコピーします。ソースデータが同じブック内にある場合、宛先ピボットは同じキャッシュを指します。キャッシュを複製するには、手動で新しいピボットキャッシュを作成する必要があります。

**大きな範囲を効率的にコピーするには？**  
非常に大きな範囲をコピーする場合、必要に応じて `CopyOptions.setCopyFormula(true)` や `setCopyDataValidation(true)` を使用することを検討してください。オプションの数を減らすことでパフォーマンスが向上します。

## 信頼性の高い **aspose.cells copy range** の使用に関するヒント

* **プロのコツ:** 範囲にピボットキャッシュに依存する数式が含まれる場合、コピー後は必ず `workbook.calculateFormula()` を呼び出してください。
* **注意点:** 非表示のワークシート。`copyRange` は非表示シートを除き、表示シートでのみ動作します。非表示シートを使用する場合はインデックスで明示的に参照してください。
* **バージョン確認:** `setCopyPivotTable` フラグは Aspose.Cells 20.9 以降で利用可能です。使用しているライブラリのバージョンが対応していることを確認してください。

## 結論

これで、Aspose.Cells で **ピボットをコピーする方法** と、完全なピボット機能を保持したまま **範囲をブックにコピー** する方法が分かりました。ライブラリの追加、ブックのロード、`CopyOptions` の設定、コピーの実行、保存という手順は、他のコピー＆ペーストシナリオにも応用できる再利用可能なパターンです。

次に、チャート、条件付き書式、データ検証向けの **aspose.cells copy range** などの関連トピックを探求してください。異なるファイル形式間（XLSX → XLS）でのコピーを試して、Automation の可能性を広げましょう。コーディングを楽しんでください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説付きの完全なコード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.Cells for Java を使用した Excel でのピボットテーブル作成方法：包括的ガイド](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Aspose.Cells for Java を使用した Excel ピボットテーブル ソースの更新方法：包括的ガイド](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Aspose.Cells for Java を使用したピボットテーブルのスライサー実装方法：包括的ガイド](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}