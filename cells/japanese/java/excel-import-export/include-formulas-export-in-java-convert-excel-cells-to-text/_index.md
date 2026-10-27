---
category: general
date: 2026-07-03
description: Aspose.Cells を使用して、Java で Excel のセルをテキストに変換する際に数式のエクスポートを含めます。Excel の範囲を印刷し、セルの値文字列を効率的に取得する方法をご紹介します。
draft: false
keywords:
- include formulas export
- convert excel cells text
- print excel range
- export table options
- get cell values string
language: ja
og_description: Javaで数式をエクスポートし、Excelセルをテキストに変換する方法を含む。Excelの範囲を印刷し、セルの値を文字列として取得する手順をステップバイステップで解説。
og_title: Javaで数式エクスポートを含める – Excelセルをテキストに変換
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  headline: Include Formulas Export in Java – Convert Excel Cells to Text
  type: TechArticle
- description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  name: Include Formulas Export in Java – Convert Excel Cells to Text
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles with older versions but we’ll stick
      to the latest LTS). - Aspose.Cells for Java 23.10 (or any recent release)—you
      can grab it from Maven Central. - A sample `input.xlsx` placed in a folder you
      control (the path is hard‑coded in the example for clarity).'
  - name: Optional Tweaks
    text: '- `eto.setExportHiddenRows(true);` – include rows hidden in Excel. - `eto.setExportHiddenColumns(true);`
      – same for columns. - `eto.setExportAsHTML(true);` – get HTML instead of plain
      text.'
  - name: Expected Output (sample)
    text: '``` =SUM(A2:A3) 42 Hello =IF(B1>10,"Yes","No") =AVERAGE(C1:C3) =VLOOKUP(A1,Sheet2!A:B,2,FALSE)
      ```'
  - name: What if the range contains merged cells?
    text: Merged cells are treated as the value of the top‑left cell. The rest of
      the merged area will appear as empty strings. If you need the merged region’s
      address, query `Cell.getMergedRange()` before export.
  - name: Can I export a massive sheet (hundreds of thousands of rows)?
    text: Yes, but beware of memory consumption. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to let Aspose.Cells stream data to disk. Also, consider exporting in chunks
      (e.g., 10 000 rows at a time) to keep the string manageable.
  - name: How do I change the column delimiter?
    text: '`ExportTableOptions` exposes `setSeparator(char separator)`. For CSV‑style
      output, set it to `'',''`:'
  - name: Do formulas respect external references?
    text: If a formula points to another workbook, Aspose.Cells will keep the reference
      text (`='[Other.xlsx]Sheet1'!A1`). It won’t evaluate the external value unless
      you load that workbook as well.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Export
title: Javaで数式を含むエクスポート – Excelセルをテキストに変換
url: /ja/java/excel-import-export/include-formulas-export-in-java-convert-excel-cells-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Javaで数式エクスポートを含める – Excelセルをテキストに変換

Excelブックからデータを取得するときに **include formulas export** が必要になったことはありませんか？元の数式を保持しつつ、整ったテキストブロブを提供しなければならないレポーティングサービスを構築しているかもしれません。その場合は正しい場所に来ています。このガイドでは、Aspose.Cells for Java を使用して、Excelセルをプレーンテキストに変換する方法—*埋め込まれた数式も含めて*—を説明します。

**print Excel range** の方法や **export table options** の調整、最終的に **get cell values string** を取得してログに記録したり API 経由で送信したりデータベースに保存したりできるようになるまでをカバーします。最後まで読めば、完全に実行可能なコードスニペットと、各呼び出しの背後にある理由をしっかり理解できるようになります。

## 本ガイドで得られるもの

- `.xlsx` ファイルを読み取り、範囲を選択し、フォーマット済み文字列としてエクスポートする、コピー＆ペースト可能な完全な Java プログラム。
- `ExportTableOptions` クラスの役割と、`setExportAsString` と `setIncludeFormula` を切り替える意味。
- 大規模シートの扱い方、さまざまなデータ型への対処、出力フォーマットのカスタマイズに関するヒント。
- よくある落とし穴（結合セル、非表示行、ロケール固有の数値書式など）に対するチェックリスト。

### 前提条件

- Java 17 以上（コードは古いバージョンでもコンパイル可能ですが、最新の LTS を使用します）。
- Aspose.Cells for Java 23.10（またはそれ以降のリリース）— Maven Central から取得できます。
- サンプルの `input.xlsx` を任意のフォルダーに配置（例示のためパスはハードコードされています）。

上記が揃っていれば、さっそく始めましょう。

## 手順 1: プロジェクトを作成し依存関係を追加

まず Maven プロジェクト（または好みで Gradle）を作成し、`pom.xml` に Aspose.Cells の依存関係を追加します。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Pro tip:** 社内プロキシを使用している場合は、リポジトリにアクセスできることを確認してください。アクセスできないと “Could not resolve dependencies” エラーでビルドが失敗します。

Maven が依存関係のダウンロードを終えたら、Java の記述に進めます。

## 手順 2: ワークブックを読み込み目的のシートを取得

コード例の最初の行は、既存のワークブックを開く方法を示しています。

```java
// Step 1: Load the workbook
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`YOUR_DIRECTORY` をファイルの絶対パスまたは相対パスに置き換えてください。`Workbook` コンストラクタはファイル形式（XLS、XLSX、CSV など）を自動判別するため、明示的に指定する必要はありません。

次に、最初のシートを取得します。

```java
// Step 2: Get the first worksheet
Worksheet ws = wb.getWorksheets().get(0);
```

なぜ最初のシートかというと、多くのテンプレートではデータが最初のタブに配置されているからです。任意のインデックスを指定したり、名前で取得したい場合は `get("SheetName")` を使用できます。

## 手順 3: エクスポートしたい範囲を定義

ここからが **convert excel cells text** の核心です。`Range` オブジェクトを作成して、Aspose.Cells に取得対象のセルを指示します。

```java
// Step 3: Create a range covering cells A1 to C3
Range rng = ws.getCells().createRange("A1:C3");
```

文字列 `"A1:C3"` は典型的な A1 形式のアドレスです。プログラムで組み立てることも可能です。

```java
int firstRow = 0, firstCol = 0, totalRows = 3, totalCols = 3;
Range rng = ws.getCells().createRange(firstRow, firstCol, totalRows, totalCols);
```

この柔軟性は、たとえば `ws.getCells().getMaxDataRow()` で取得した最終行を基に動的に範囲サイズを決める場合に便利です。

## 手順 4: 数式を含めるために ExportTableOptions を設定

ここが **include formulas export** の魔法が宿る場所です。デフォルトでは Aspose.Cells は「表示されている」値を返します。セルに `=SUM(A1:A3)` が入っている場合、計算結果の数値が取得され、数式テキストは得られません。これを変更するには `ExportTableOptions` を設定します。

```java
// Step 4: Set up export options to return the range as a string and include formulas
ExportTableOptions eto = new ExportTableOptions();
eto.setExportAsString(true);      // Forces the result to be a single string
eto.setIncludeFormula(true);      // Includes the underlying formula instead of the evaluated value
```

なぜ両方のフラグが必要かというと、`setExportAsString(true)` は列区切り文字（デフォルトはタブ）と行区切り文字（デフォルトは改行）でセルを連結する指示です。`setIncludeFormula(true)` は「表示値」から「生の数式」へソースを切り替えます。値だけが欲しい場合は `false` のままで構いません。

### オプション設定例

- `eto.setExportHiddenRows(true);` – Excel で非表示になっている行も含める。
- `eto.setExportHiddenColumns(true);` – 非表示列も同様に含める。
- `eto.setExportAsHTML(true);` – プレーンテキストの代わりに HTML を取得。

好きなように試してみてください。`ExportTableOptions` は **export table options** の遊び場です。

## 手順 5: 範囲をフォーマット済み文字列として取得

実際にデータを取得します。

```java
// Step 5: Retrieve the range values as a formatted string using the options
String txt = rng.getValueAsString(eto);
```

返ってくる `txt` は次のような形式になります（A1:C3 に値と数式が混在していると仮定）。

```
=SUM(A2:A3)	42	"Hello"
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

列はタブ（`\t`）で、行は改行（`\n`）で区切られています。後で 2 次元配列に分割したい場合は以下のように処理できます。

```java
String[] rows = txt.split("\n");
for (String row : rows) {
    String[] cells = row.split("\t");
    // Process each cell...
}
```

## 手順 6: 結果を出力 – “Print Excel Range” をシンプルに

最後に、文字列をコンソールに出力します。

```java
// Step 6: Print the resulting string
System.out.println(txt);
```

プログラムを実行すると、上記と同じ出力がコンソールに表示されます。ここからは、文字列をログファイルに書き込んだり、HTTP で送信したり、NoSQL ドキュメントに保存したりと自由に活用できます。

## 完全に実行可能なサンプル

すべてをまとめた完全版プログラムです。コピーして貼り付け、**Run** をクリックすれば動作します（インポート漏れはありません）。

```java
import com.aspose.cells.*;

public class ExportFormulaRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // Define the range A1:C3 (adjust as needed)
        Range rng = ws.getCells().createRange("A1:C3");

        // Configure export options: string output + include formulas
        ExportTableOptions eto = new ExportTableOptions();
        eto.setExportAsString(true);
        eto.setIncludeFormula(true);

        // Get the string representation of the range
        String txt = rng.getValueAsString(eto);

        // Print the resulting text
        System.out.println(txt);
    }
}
```

### 期待される出力（サンプル）

```
=SUM(A2:A3)	42	Hello
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

ワークブックに日付形式の数値が含まれている場合、ロケール固有の書式（例: `2026‑07‑03`）で表示されます。ISO 形式の日付に統一したい場合は、`ExportTableOptions` にカスタム `NumberFormat` を設定してください。

## エッジケースとよくある質問への対処

### 範囲に結合セルが含まれている場合は？

結合セルは左上のセルの値として扱われます。結合領域の残りは空文字列になります。結合領域のアドレスが必要な場合は、エクスポート前に `Cell.getMergedRange()` を問い合わせてください。

### 数十万行の巨大シートをエクスポートできるか？

可能ですが、メモリ消費に注意が必要です。`Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` を使用して Aspose.Cells にディスクストリーミングを許可してください。また、文字列サイズを抑えるために 10 000 行ずつなどのチャンクに分割してエクスポートすることも検討してください。

### 列区切り文字を変更したい場合は？

`ExportTableOptions` の `setSeparator(char separator)` を使用します。CSV 形式にしたい場合は次のようにカンマを指定します。

```java
eto.setSeparator(',');
```

### 数式は外部参照を保持するか？

数式が別ブックを参照している場合、Aspose.Cells は参照テキスト（例: `='[Other.xlsx]Sheet1'!A1`）をそのまま保持します。外部ブックをロードしない限り、外部値は評価されません。

## 本番環境向けコードのプロティップ

- **Cache the workbook** if you’re reading the

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれているので、API の追加機能をマスターしたり、独自プロジェクトで代替実装を試したりする際に役立ちます。

- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Convert Excel to PDF in Java Using Aspose.Cells&#58; A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}