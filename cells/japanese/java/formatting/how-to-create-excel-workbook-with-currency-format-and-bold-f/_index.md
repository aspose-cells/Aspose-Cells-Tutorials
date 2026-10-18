---
category: general
date: 2026-08-20
description: JavaでAspose.Cellsを使用してExcelブックを作成し、通貨書式を設定し、太字フォントを追加し、スタイルされたセル用にスタイル配列をインポートする。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set currency format
- format cells currency
- how to import style
- add bold font
language: ja
lastmod: 2026-08-20
og_description: JavaでExcelブックを作成し、通貨形式を設定し、太字フォントを追加し、Aspose.Cellsを使用してスタイルのインポート方法を学びます。
og_image_alt: Screenshot of an excel workbook created with currency format and bold
  font using Aspose.Cells
og_title: Javaでスタイルが適用された通貨セルを持つExcelワークブックを作成
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  headline: How to create excel workbook with currency format and bold font in Java
  type: TechArticle
- description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  name: How to create excel workbook with currency format and bold font in Java
  steps:
  - name: Initialise the workbook and worksheet
    text: Creating a fresh workbook gives you a clean container for all subsequent
      formatting.
  - name: Build a DataTable with numeric data
    text: A `DataTable` mimics a database table, making it easy to import rows in
      bulk.
  - name: Define a style – currency format and bold font
    text: Here we **set currency format** and **add bold font** to a `Style` object.
  - name: Configure import options to use the style array
    text: Aspose.Cells lets you pass a `Style[]` via `ImportTableOptions`. This is
      the official **how to import style** method.
  - name: Import the DataTable into the worksheet
    text: Now we bring the data into the sheet at cell `A1`, applying the style array
      automatically.
  - name: Save the workbook to disk
    text: Finally, write the in‑memory workbook to a physical file.
  - name: Expected output
    text: 'When you open `DataTableWithStyleArray.xlsx` in Microsoft Excel, you should
      see:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Formatting
title: Javaで通貨形式と太字フォントを持つExcelブックを作成する方法
url: /ja/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Javaで通貨形式と太字フォントを持つExcelブックを作成する方法

プログラムで **create excel workbook** が必要な場合、このガイドで手順を正確に示します。ブックの作成、通貨形式の適用、太字フォントの追加、そして Aspose.Cells の **how to import style** 機能を使用して、インポートされたすべてのセルが一貫した外観になるように進めていきます。

最終的に、数値がドル表示され太字でハイライトされた `DataTableWithStyleArray.xlsx` ファイルがすぐに使用できる状態になります。Excelで手動で書式設定を行う必要はありません。

## 前提条件

- Java 17 以降がインストールされていること。
- Aspose.Cells for Java のライセンス（または無料評価キー）。
- `aspose-cells` 依存関係を管理するための Maven または Gradle。
- Java コレクションと `DataTable` の基本的な知識。

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

> **プロのヒント:** `LicenseException` が発生した場合は、ライセンスファイルをクラスパスに配置し、ブック作成前に `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` を呼び出してください。

## スタイル付き通貨セルで excel workbook を作成する方法

このセクションでは主要な手順を示します。各ステップは **why** が重要である理由を説明し、単に **what** を入力するだけではありません。

### 手順 1: ワークブックとワークシートの初期化

新しいワークブックを作成することで、以降のすべての書式設定のためのクリーンなコンテナが得られます。

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
Cells cells = worksheet.getCells();                     // shortcut to work with cells
```

> **なぜ:** `Workbook` オブジェクトは Excel ファイル全体を表します。最初の `Worksheet` にアクセスすることで、すぐにデータの入力を開始できます。

### 手順 2: 数値データで DataTable を構築する

`DataTable` はデータベーステーブルを模倣し、行を一括でインポートしやすくします。

```java
// Step 2: Build a DataTable with sample numeric data
DataTable dataTable = new DataTable();
dataTable.getColumns().add("Amount", DataType.DOUBLE); // column type DOUBLE ensures numeric handling
dataTable.getRows().add(new Object[]{1234.56});
dataTable.getRows().add(new Object[]{7890.12});
```

> **なぜ:** `DOUBLE` を使用することで、値の小数精度が保たれ、後で **format cells currency** を行う際に重要です。

### 手順 3: スタイルの定義 – 通貨形式と太字フォント

ここでは `Style` オブジェクトに **set currency format** と **add bold font** を設定します。

```java
// Step 3: Define a style (currency format and bold font) for the imported cells
Style currencyStyle = workbook.createStyle();                // create a reusable style instance
currencyStyle.getNumber().setFormat("$#,##0.00");            // set currency format (e.g., $1,234.56)
currencyStyle.getFont().setBold(true);                      // make the font bold
Style[] styleArray = new Style[] { currencyStyle };          // style array required by ImportTableOptions
```

> **なぜ:** `Number` の書式文字列 `$#,##0.00` は Excel にセルを通貨値として扱うよう指示し、`setBold(true)` は数値を目立たせます。スタイルを配列に入れることで、**how to import style** 手順の準備が整います。

### 手順 4: インポートオプションを設定してスタイル配列を使用する

Aspose.Cells では `ImportTableOptions` を介して `Style[]` を渡すことができ、これが公式の **how to import style** 手法です。

```java
// Step 4: Set up import options to use the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(styleArray); // tells the importer to apply our currencyStyle to every column
```

> **なぜ:** `ImportTableOptions` がないと、インポートされたセルはデフォルトのスタイルを継承し、定義した通貨書式と太字が失われます。

### 手順 5: DataTable をワークシートにインポートする

これでデータをシートのセル `A1` に持ち込み、スタイル配列が自動的に適用されます。

```java
// Step 5: Import the DataTable into the worksheet at A1, applying the style
cells.importDataTable(dataTable, true, "A1", importOptions);
```

- `true` は `DataTable` の最初の行が列ヘッダーであることを示します。
- `"A1"` はインポート開始位置の左上隅です。

> **なぜ:** スタイル配列でインポートすることで、各インポートされたセルが事前に用意した **format cells currency** スタイルを受け取ります。

### 手順 6: ワークブックをディスクに保存する

最後に、メモリ上のワークブックを実際のファイルに書き出します。

```java
// Step 6: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/DataTableWithStyleArray.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to: " + outputPath);
```

> **なぜ:** 保存することで書式設定が保持され、あなたや後続のプロセスが Excel で期待通りの外観でファイルを開くことができます。

## 完全なソースコード

以下は完全な、すぐに実行可能な Java クラスです。IDE にコピーし、`YOUR_DIRECTORY` を既存のフォルダーに置き換えて実行してください。

```java
import com.aspose.cells.*;

public class StyleArrayImportTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Build a DataTable with sample numeric data
        DataTable dataTable = new DataTable();
        dataTable.getColumns().add("Amount", DataType.DOUBLE);
        dataTable.getRows().add(new Object[]{1234.56});
        dataTable.getRows().add(new Object[]{7890.12});

        // Step 3: Define a style (currency format and bold font) for the imported cells
        Style currencyStyle = workbook.createStyle();
        currencyStyle.getNumber().setFormat("$#,##0.00");   // set currency format
        currencyStyle.getFont().setBold(true);             // add bold font
        Style[] styleArray = new Style[] { currencyStyle };

        // Step 4: Set up import options to use the style array
        ImportTableOptions importOptions = new ImportTableOptions();
        importOptions.setStyleArray(styleArray);           // how to import style

        // Step 5: Import the DataTable into the worksheet at A1, applying the style
        cells.importDataTable(dataTable, true, "A1", importOptions);

        // Step 6: Save the workbook to a file
        workbook.save("YOUR_DIRECTORY/DataTableWithStyleArray.xlsx");
        System.out.println("Workbook created successfully.");
    }
}
```

### 期待される出力

Microsoft Excel で `DataTableWithStyleArray.xlsx` を開くと、次のように表示されます。

| 金額 |
|------|
| **$1,234.56** |
| **$7,890.12** |

- 数値は **currency format**（`$` 記号、2 桁の小数）で表示されます。
- 両方のセルのフォントは **bold** で、目立つようになっています。

## 一般的なバリエーションとエッジケース

| シナリオ | 変更点 | 理由 |
|----------|----------------|--------|
| **異なる通貨** | `currencyStyle.getNumber().setFormat("€#,##0.00");` | ユーロ記号や任意のロケール固有の形式を使用します。 |
| **異なるスタイルの複数列** | Create multiple `Style` objects, populate `styleArray` in the same order as columns. | 各列は独自の数値形式、フォント、背景などを持つことができます。 |
| **大規模データセット** | Use `cells.importDataTable(dataTable, false, "A1", importOptions);` and set `importOptions.setImportDataOptions(ImportDataOptions.DATA_ONLY);` | ヘッダー行や不要なメタデータをスキップすることでパフォーマンスが向上します。 |
| **インポート後にスタイルを適用** | Call `cells.get("A2").setStyle(currencyStyle);` for individual cells. | 特定の行だけに特別な書式設定が必要な場合に便利です。 |

## 本番環境での使用時のヒント

- **License early**: ワークブック作成前に Aspose.Cells のライセンスを登録し、評価版の透かしを回避してください。
- **Thread safety**: `Workbook` インスタンスは **スレッドセーフではありません**。多数のファイルを同時に生成する場合は、スレッドごとに別々のインスタンスを作成してください。
- **Memory management**: 非常に大きなシートの場合、メモリ使用量を抑えるために `Workbook` のストリーミング API（`Workbook` → `WorkbookDesigner`）の使用を検討してください。
- **Testing**: 保存されたファイルを Apache POI で開き、セルスタイルの数値書式が `"$#,##0.00"` と一致することを検証するユニットテストを含めてください。

## 結論

これで、Java で **create excel workbook** を行い、**set currency format**、**add bold font** を設定し、Aspose.Cells の `ImportTableOptions` を使用して正しく **how to import style** を行う方法が分かりました。このエンドツーエンドのソリューションにより、手動の Excel 手順が不要になり、インポートされたすべてのセルが同じ **format cells currency** 書式に従うことが保証されます。

次のチャレンジに挑みますか？条件付き書式の追加、チャートの埋め込み、またはワークブックの PDF へのエクスポートなどを試してみてください—すべて同じ style‑array 手法を再利用できます。コーディングを楽しんでください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.Cells を使用した Java での Excel ワークブック作成：ステップバイステップガイド](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Aspose.Cells for Java を使用した Excel セルの作成と書式設定：ステップバイステップガイド](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Aspose.Cells for Java を使用した Excel セルのスタイル設定とハイパーリンクの追加](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}