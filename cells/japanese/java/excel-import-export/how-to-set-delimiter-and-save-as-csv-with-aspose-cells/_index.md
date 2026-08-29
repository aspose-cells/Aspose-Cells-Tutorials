---
category: general
date: 2026-08-14
description: Aspose.Cells を使用して区切り文字を設定し CSV として保存する方法、桁数を制限する方法、CSV 文字列をエクスポートする方法、そして
  Java で数式を再計算する方法。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set delimiter
- save as csv
- recalculate formulas
- how to export csv
- how to limit digits
language: ja
lastmod: 2026-08-14
og_description: Aspose.Cellsで区切り文字を設定してCSVとして保存する方法、桁数を制限する方法、CSV文字列をエクスポートする方法、そしてJavaで数式を再計算する方法.
og_image_alt: Screenshot of Java code that sets a CSV delimiter and saves an Excel
  workbook as CSV using Aspose.Cells
og_title: 区切り文字の設定とCSVとして保存する方法 – Aspose.Cells ガイド
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  headline: How to set delimiter and save as CSV with Aspose.Cells
  type: TechArticle
- description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  name: How to set delimiter and save as CSV with Aspose.Cells
  steps:
  - name: Why this works
    text: "- `CsvSaveOptions.setDelimiter(char)` tells Aspose.Cells which character
      separates fields. By default it’s a comma, but any character (tab `'\t'`, pipe
      `'|'`, etc.) works. - `setSignificantDigits(int)` limits numeric precision,
      satisfying the **how to limit digits** requirement without manually form"
  - name: When to use this
    text: '- Returning CSV from a REST endpoint (`@RestController` in Spring) - Embedding
      CSV data into an email attachment without writing to disk - Performing quick
      sanity checks during unit tests'
  - name: Why recalculate?
    text: '- Formulas may reference external data or volatile functions (`NOW()`,
      `RAND()`) that need fresh values. - Dynamic‑array formulas (e.g., `=SORT(A1:A10)`)
      are evaluated automatically, but calling `calculateFormula()` guarantees consistency
      across all sheets.'
  - name: Verifying the result
    text: 1. Open `output.csv` in a text editor – you should see a semicolon (`;`)
      separating each column. 2. Confirm that numeric columns display at most five
      significant digits. 3. The console output will print the CSV string generated
      in step 4. 4. Open `japan_updated.xlsx` in Excel – any formulas that pre
  type: HowTo
tags:
- Aspose.Cells
- Java
- CSV export
- Excel automation
title: Aspose.Cellsで区切り文字を設定してCSVとして保存する方法
url: /ja/java/excel-import-export/how-to-set-delimiter-and-save-as-csv-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells を使用して区切り文字を設定し CSV として保存する方法

If you need to **区切り文字の設定方法** while exporting data from an Excel workbook, this guide shows you a complete, end‑to‑end solution using Aspose.Cells for Java. You’ll learn how to configure the CSV delimiter, limit the number of significant digits, export a CSV string, and refresh dynamic‑array formulas after loading a workbook.

The tutorial covers everything you need to run the code on your machine, including handling special calendars such as the Japanese Emperor reign. By the end, you’ll be able to generate accurate CSV files, control numeric precision, and ensure formulas are up‑to‑date.

## 前提条件

- Java 17 以降（コードは JDK 11+ でもコンパイル可能です）
- Aspose.Cells for Java 23.9 以降 – [Aspose のウェブサイト](https://products.aspose.com/cells/java/) からダウンロード
- Maven または Gradle を使用した依存関係管理の基本的な知識
- IDE（IntelliJ IDEA、Eclipse、VS Code）またはシンプルなテキストエディタとコマンドライン

> **プロのコツ:** `libs` フォルダーや Maven Central を使用して Aspose.Cells JAR をクラスパスに保持してください。以下の例は Maven プロジェクトを前提としています。

## 手順 1: Maven プロジェクトのセットアップ

Aspose.Cells の依存関係を含む `pom.xml` を作成します：

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>aspose-csv-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.9</version>
            <classifier>jdk17</classifier>
        </dependency>
    </dependencies>
</project>
```

`mvn clean compile` を実行してライブラリをダウンロードし、ビルドが成功することを確認します。

## 手順 2: 区切り文字を設定して CSV として保存する方法

主な目的は、Excel ワークブックを CSV として保存する際に、デフォルトのカンマ区切り文字をカスタム文字（例: セミコロン）に変更することです。そのために Aspose.Cells は `CsvSaveOptions` を提供しています。

```java
package com.example;

import com.aspose.cells.*;

public class CsvDelimiterDemo {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook (replace the path with your file)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Configure CSV save options
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        // Primary requirement: set a custom delimiter
        csvOptions.setDelimiter(';');               // <-- how to set delimiter
        // Optional: limit the number of significant digits
        csvOptions.setSignificantDigits(5);         // <-- how to limit digits

        // Save the workbook as CSV using the configured options
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);

        System.out.println("CSV file saved with ';' delimiter and 5‑digit precision.");
    }
}
```

### なぜこれが機能するのか

- `CsvSaveOptions.setDelimiter(char)` は、フィールドを区切る文字を Aspose.Cells に指示します。デフォルトはカンマですが、任意の文字（タブ `'\t'`、パイプ `'|'` など）でも使用できます。
- `setSignificantDigits(int)` は数値の精度を制限し、**桁数制限の方法** の要件を満たします。各セルを手動で書式設定する必要はありません。

#### 期待される出力

The file `output.csv` will contain rows like:

```
Name;Amount;Date
Alice;123.46;2024-01-15
Bob;78.90;2024-01-16
```

数値は有効数字5桁に丸められることに注意してください（例: `123.45678` → `123.46`）。

## 手順 3: CSV 保存時に桁数を制限する方法

数値書式設定をより厳密に制御したい場合は、`CsvSaveOptions` インスタンスを使用してカスタムの数値書式文字列を指定することもできます。

```java
CsvSaveOptions csvOptions = new CsvSaveOptions();
csvOptions.setDelimiter(',');                // standard comma delimiter
csvOptions.setNumberFormat("0.####");        // up to 4 decimal places
csvOptions.setSignificantDigits(6);          // overall significant digits
```

- `setNumberFormat` は .NET スタイルのパターンに従い、Aspose.Cells がそれを尊重します。
- `setNumberFormat` と `setSignificantDigits` の両方を組み合わせることで、異なるロケール間でも予測可能な丸めが実現します。

## 手順 4: カスタム区切り文字で CSV を文字列としてエクスポートする方法

場合によっては物理ファイルが不要で、CSV データをメモリ上に保持したいことがあります（例: HTTP 応答として送信する場合）。`ExportTableOptions` クラスを使用すると、範囲を文字列としてエクスポートできます。

```java
// Export a range (rows 0‑9, columns 0‑4) as a CSV string
ExportTableOptions exportOptions = new ExportTableOptions();
exportOptions.setExportAsString(true);   // return a string instead of a file
exportOptions.setDelimiter(',');         // <-- how to set delimiter for export
exportOptions.setIncludeColumnNames(true);

String csvData = workbook.getWorksheets()
                         .get(0)                     // first worksheet
                         .getCells()
                         .exportDataTableAsString(0, 0, 10, 5, exportOptions);

System.out.println("Exported CSV string:");
System.out.println(csvData);
```

### いつ使用するか

- REST エンドポイント（Spring の `@RestController`）から CSV を返す場合
- ディスクに書き込まずに CSV データをメール添付として埋め込む場合
- ユニットテスト中に簡易的な検証を行う場合

## 手順 5: ワークブック読み込み後に数式を再計算する方法

ワークブックに数式が含まれている場合、特に最近の Excel バージョンで導入された **dynamic‑array formulas** については、ファイル読み込み後に再計算する必要があります。Aspose.Cells は動的配列の結果を自動的に更新しますが、通常の数式については `calculateFormula()` を呼び出す必要があります。

```java
// Load a workbook that uses the Japanese Emperor calendar (optional step)
LoadOptions loadOptions = new LoadOptions();
loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

// Recalculate all formulas in the workbook
japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

// Save the refreshed workbook (preserves the original calendar)
japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
System.out.println("Formulas recalculated and workbook saved.");
```

### なぜ再計算が必要か

- 数式は外部データや揮発性関数（`NOW()`, `RAND()`）を参照している可能性があり、最新の値が必要です。
- 動的配列数式（例: `=SORT(A1:A10)`）は自動的に評価されますが、`calculateFormula()` を呼び出すことで全シート間の一貫性が保証されます。

## 手順 6: 完全なエンドツーエンド例

以下は、**区切り文字の設定方法**、**CSV として保存**、**桁数制限**、**CSV 文字列のエクスポート**、**特別な暦を持つワークブックの読み込み**、そして **数式の再計算** を示す単一クラスです。コードはそのままプロジェクトにコピーして使用できます。

```java
package com.example;

import com.aspose.cells.*;

public class AsposeCsvFullDemo {
    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // 1. Load an existing workbook
        // -----------------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // -----------------------------------------------------------------
        // 2. Configure CSV save options (delimiter + digit limit)
        // -----------------------------------------------------------------
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        csvOptions.setDelimiter(';');          // <-- how to set delimiter
        csvOptions.setSignificantDigits(5);    // <-- how to limit digits

        // -----------------------------------------------------------------
        // 3. Save the workbook as CSV
        // -----------------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);
        System.out.println("Saved CSV with ';' delimiter.");

        // -----------------------------------------------------------------
        // 4. Export a range as a CSV string (custom delimiter)
        // -----------------------------------------------------------------
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);
        exportOptions.setDelimiter(',');       // <-- how to set delimiter for export
        exportOptions.setIncludeColumnNames(true);

        String csvString = workbook.getWorksheets()
                                   .get(0)
                                   .getCells()
                                   .exportDataTableAsString(0, 0, 10, 5, exportOptions);
        System.out.println("CSV string exported:");
        System.out.println(csvString);

        // -----------------------------------------------------------------
        // 5. Load a workbook that uses the Japanese Emperor calendar
        // -----------------------------------------------------------------
        LoadOptions loadOptions = new LoadOptions();
        loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
        Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

        // -----------------------------------------------------------------
        // 6. Recalculate formulas (including dynamic‑array formulas)
        // -----------------------------------------------------------------
        japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

        // -----------------------------------------------------------------
        // 7. Save the refreshed workbook
        // -----------------------------------------------------------------
        japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
        System.out.println("Japanese workbook refreshed and saved.");
    }
}
```

### 結果の検証

1. テキストエディタで `output.csv` を開く – 各列がセミコロン (`;`) で区切られていることを確認してください。
2. 数値列が最大で有効数字5桁で表示されていることを確認します。
3. コンソール出力に手順 4 で生成された CSV 文字列が表示されます。
4. Excel で `japan_updated.xlsx` を開く – 以前 `#REF!` や古い値を表示していた数式が正しい結果に更新されていることを確認します。

## よくある落とし穴と回避方法

| Issue | Cause | Fix |
|-------|-------|-----|
| CSV に余分な引用符が表示される | セルにカンマが含まれているが、区切り文字もカンマになっている | `setDelimiter` で別の区切り文字（`;` または `\t`）を使用する |
| 数値が正しく丸められない | `setSignificantDigits` がカスタム数値書式の後に適用されている | `setNumberFormat` を **`setSignificantDigits` の前** に適用する |

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.Cells for Java を使用した Excel の CSV へのロードと保存: 包括的ガイド](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [Aspose.Cells for Java を使用した CSV ファイルのロード: 包括的ガイド](/cells/english/java/workbook-operations/load-csv-aspose-cells-java-tutorial/)
- [Aspose.Cells を使用した Java のカスタムパーサで CSV ファイルをロード](/cells/english/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}