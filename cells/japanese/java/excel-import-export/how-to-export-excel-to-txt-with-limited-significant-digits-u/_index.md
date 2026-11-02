---
category: general
date: 2026-08-17
description: 有効数字を制限しながらExcelをTXTにエクスポート – 桁数の設定方法と、JavaでExcelをテキストに変換する完全なAspose.Cellsサンプルを学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set digits
- convert excel to text
- how to limit decimals
- limit significant digits
language: ja
lastmod: 2026-08-17
og_description: 有効数字を制限してExcelをTXTにエクスポートします。このチュートリアルでは、桁数を設定し、Aspose.Cells for Java
  を使用してExcelをテキストに変換する方法を示します。
og_image_alt: Java code exporting Excel to TXT with 4 significant digits
og_title: ExcelからTXTへ、有効桁数を制限してエクスポート – Javaガイド
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  headline: How to export Excel to TXT with limited significant digits using Java
  type: TechArticle
- description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  name: How to export Excel to TXT with limited significant digits using Java
  steps:
  - name: Prerequisites
    text: '- Java 17 or later (the code compiles with Java 8 as well). - Aspose.Cells
      for Java 25.10 or newer. Download the JAR from the [Aspose website](https://products.aspose.com/cells/java)
      and add it to your project’s classpath. - An IDE or a simple text editor and
      command‑line build tool (Maven/Gradle).'
  - name: How the setting differs from “limit decimals”
    text: '- **limit decimals** (`setDecimalPlaces`) trims digits *after* the decimal
      point, regardless of the integer part. - **significant digits** (`setSignificantDigits`)
      counts digits from the first non‑zero digit, which is useful when numbers vary
      in magnitude.'
  - name: Expected output
    text: '| Cell | Original value | Exported (4 significant digits) | |------|----------------|---------------------------------|
      | A1 | 123.456789 | 123.5 |'
  - name: Exporting a whole range
    text: 'If you want to export more than one cell, simply fill the range before
      saving:'
  - name: Handling locale‑specific decimal separators
    text: 'Aspose.Cells respects the system locale when writing text. To force a dot
      (`.`) as the decimal separator, set the `TxtSaveOptions` culture:'
  - name: Overwriting existing files
    text: 'The `save` method overwrites the target file by default. If you need to
      avoid accidental data loss, check for file existence first:'
  - name: Large workbooks and memory usage
    text: 'When exporting very large worksheets, consider streaming the output:'
  - name: Next steps
    text: "- Explore other `TxtSaveOptions` properties such as `setDelimiter('\t')`
      to customize column separators. - Combine the exporter with `CsvSaveOptions`
      if you need comma‑separated values instead of plain text. - Integrate the routine
      into a web service that accepts uploaded Excel files and returns tri"
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel export
- TXT conversion
title: JavaでExcelを有効数字を制限してTXTにエクスポートする方法
url: /ja/java/excel-import-export/how-to-export-excel-to-txt-with-limited-significant-digits-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java を使用して有効数字を制限して Excel を TXT にエクスポートする

Excel を **TXT にエクスポート** しながら有効数字の桁数を制御したい場合、本ガイドがすぐに実行できるソリューションを提供します。桁数の設定方法、Excel からテキストへの変換方法、そして 1 つの設定変更だけで出力をすっきりさせる方法を確認できます。

サンプルは Aspose.Cells for Java 25.10 を使用しています。このバージョンで `setSignificantDigits` オプションが導入されました。チュートリアルの最後までに、余計な丸め処理コードを書かずに、必要な桁数だけを含む TXT ファイルを生成できるようになります。

## 実現できること

- プログラムからワークブックを作成する  
- セルに数値を挿入する  
- TXT 保存オプションで有効数字を制限する  
- ワークブックをプレーンテキストファイルとして保存する  
- `significantDigits` 設定の仕組みを理解し、他のシナリオに応用できるようになる  

### 前提条件

- Java 17 以降（コードは Java 8 でもコンパイル可能）  
- Aspose.Cells for Java 25.10 以上。JAR は [Aspose のウェブサイト](https://products.aspose.com/cells/java) からダウンロードし、プロジェクトのクラスパスに追加してください。  
- IDE あるいはシンプルなテキストエディタとコマンドラインビルドツール（Maven/Gradle）  

## Step 1: Set up the project and import Aspose.Cells

新しい Java プロジェクトを作成し、Aspose.Cells JAR をビルドパスに追加します。Maven を使用する場合は、`pom.xml` に以下の依存関係を追加してください。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Pro tip:** 最新の Java ランタイム用に `jdk17` classifier を使用すると、互換性警告のリスクが低減します。

## Step 2: Create a workbook and write a value

ワークブックはメモリ上の Excel ファイルを表します。`putValue` メソッドを使って任意のセルにデータを追加できます。

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Put a numeric value into cell A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue(123.456789);
```

数値 `123.456789` が TXT エクスポートの元データになります。デフォルトでは Aspose.Cells はすべての小数位を書き出すため、テキストファイルが騒がしくなることがあります。

## Step 3: Configure TXT save options to limit significant digits

Aspose.Cells はプレーンテキスト出力を細かく制御できる `TxtSaveOptions` を提供します。`setSignificantDigits` メソッドは、小数点以下だけでなく **全体** の桁数を指定します。

```java
        // Configure TXT save options to keep only 4 significant digits
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4); // new option in 25.10
```

`significantDigits` を `4` に設定すると、エクスポーターは `123.456789` を `123.5` に丸めます。この動作は有効数字の数学的定義に合致しており、最初の 4 桁の有効数字が保持されます。

### 「小数位を制限する」設定との違い

- **小数位を制限** (`setDecimalPlaces`) は整数部に関係なく小数点以下の桁数だけを切り詰めます。  
- **有効数字** (`setSignificantDigits`) は最初の非ゼロ桁から数えて桁数をカウントするため、桁数が大きく異なる数値でも一貫した精度が得られます。

小数位だけを固定したい場合は、上記の行を次のように置き換えてください。

```java
saveOptions.setDecimalPlaces(2); // keeps two digits after the decimal point
```

## Step 4: Save the workbook as a TXT file

設定したオプションを使って、ワークブックをディスクに書き出します。

```java
        // Save the workbook as a TXT file using the configured options
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

プログラムを実行すると、作業ディレクトリに `significant_digits.txt` が作成されます。ファイルの内容は 1 行だけです。

```
123.5
```

### 期待される出力

| Cell | Original value | Exported (4 significant digits) |
|------|----------------|---------------------------------|
| A1   | 123.456789     | 123.5                           |

`setSignificantDigits(4)` を `6` に変更すると、出力は `123.457` になります。さまざまな値で丸めがどのように変化するか試してみてください。

## Step 5: Common variations and edge cases

### Exporting a whole range

複数セルをエクスポートしたい場合は、保存前に範囲にデータを入力するだけです。

```java
worksheet.getCells().get("B1").putValue(0.0012345);
worksheet.getCells().get("C1").putValue(98765.4321);
```

同じ `significantDigits` 設定がすべての数値セルに適用され、ファイル全体で一貫した精度が保たれます。

### Handling locale‑specific decimal separators

Aspose.Cells はテキスト書き込み時にシステムロケールを尊重します。小数点記号を必ず `.` にしたい場合は、`TxtSaveOptions` のカルチャを設定します。

```java
saveOptions.setCultureInfo(java.util.Locale.US);
```

CSV パーサーなど、ドットのみを受け付けるアプリケーションに出力を渡す際に便利です。

### Overwriting existing files

`save` メソッドは既定で対象ファイルを上書きします。誤ってデータを失うのを防ぎたい場合は、事前にファイルの有無を確認してください。

```java
java.io.File outFile = new java.io.File("significant_digits.txt");
if (outFile.exists()) {
    throw new IllegalStateException("File already exists. Choose a different name or delete the existing file.");
}
workbook.save(outFile.getPath(), saveOptions);
```

### Large workbooks and memory usage

非常に大きなシートをエクスポートする場合は、ストリーミング出力を検討してください。

```java
saveOptions.setEnableMemorySaving(true);
```

このオプションは行を順次書き出すことでヒープ使用量を削減します。

## Full working example

以下に、すぐにコピー＆ペーストして実行できる完全なプログラムを示します。

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 2: Put numeric values into cells
        worksheet.getCells().get("A1").putValue(123.456789);
        worksheet.getCells().get("B1").putValue(0.0012345);
        worksheet.getCells().get("C1").putValue(98765.4321);

        // Step 3: Configure TXT save options
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4);          // limit to 4 significant digits
        saveOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator
        saveOptions.setEnableMemorySaving(true);      // optional for large files

        // Step 4: Save the workbook as a TXT file
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

このコードを実行すると、タブ区切りの列で構成された `significant_digits.txt` が生成されます。

```
123.5	0.001235	98770
```

各数値は **4 有効数字** ルールに従って出力され、異なる桁数の数でも設定が正しく機能することが確認できます。

## Conclusion

これで **Excel を TXT にエクスポート** しながら有効数字の桁数を制御する方法が分かりました。`TxtSaveOptions.setSignificantDigits` を使用すれば、**桁数の設定方法**、**小数位の制限方法**、**有効数字の制限方法** を 1 行の保守しやすいコードで実現できます。この手法は単一セル、範囲全体、そして大規模ワークブックでも有効です。

### Next steps

- `setDelimiter('\t')` など、`TxtSaveOptions` の他のプロパティを調べて列区切り文字をカスタマイズする。  
- プレーンテキストの代わりにカンマ区切りが必要な場合は、`CsvSaveOptions` と組み合わせて使用する。  
- アップロードされた Excel ファイルを受け取り、リアルタイムでトリミングされた TXT を返す Web サービスにこのルーチンを組み込む。

さまざまな桁数やロケールで実験してみてください。組み込みオプションだけでは対応できない特殊要件が出た場合は、標準的な Java I/O ユーティリティで生成された TXT を後処理すれば対応可能です。

Happy coding!


## What Should You Learn Next?


以下のチュートリアルは、本ガイドで示したテクニックを基にした関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれているため、API の追加機能を習得したり、代替実装アプローチを自分のプロジェクトに取り入れたりするのに役立ちます。

- [How to Convert Text to Numbers in Excel Using Aspose.Cells for Java](/cells/english/java/cell-operations/convert-text-to-numbers-excel-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Export Custom Excel Properties to PDF Using Aspose.Cells for Java](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}