---
category: general
date: 2026-11-22
description: Java を使用して、Excel の列を通貨として書式設定するカスタム数値形式の使い方を学びましょう。シンプルなスタイルで Excel の数値形式をすばやく設定できます。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format
- format column as currency
- set excel number format
- set currency format
- style first column
language: ja
lastmod: 2026-11-22
og_description: JavaでExcelにカスタム数値書式を適用する。このチュートリアルでは、Excelの数値書式を設定し、最初の列を通貨形式にスタイル設定する方法を示します。
og_image_alt: Java code snippet that applies a custom number format to an Excel column
og_title: JavaでExcelにカスタム数値書式を適用する – ステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use a custom number format to format a column as currency
    in Excel using Java. Set Excel number format quickly with a simple style.
  headline: How to apply a custom number format in Excel with Java
  type: TechArticle
tags:
- Java
- Excel
- Apache POI
- Spreadsheet Automation
title: JavaでExcelにカスタム数値書式を適用する方法
url: /ja/java/formatting/how-to-apply-a-custom-number-format-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JavaでExcelにカスタム数値書式を適用する方法

Excelのワークシートの列に**カスタム数値書式**を適用する必要がある場合、このガイドではJavaを使用して正確に行う方法を示します。財務レポートを作成したり会計データをエクスポートしたりする場合でも、最初の列を通貨として書式設定すれば、出力がすぐに読みやすくなります。

以下の例では**列を通貨として書式設定**し、スタイルを最初の列に適用した後、`DataTable`をワークシートにインポートします。同じアプローチは、表示したい任意の数値書式にも適用できます。

## 学べること

* Apache POI の `Style` オブジェクトを使用して **カスタム数値書式** を作成する方法。  
* 特定の列に対して **Excel の数値書式を設定** する方法（**通貨書式の設定** のケースを含む）。  
* `DataTable` をインポートしながら **最初の列にスタイルを適用** する方法。  
* ワークブックを保存し、書式設定が正しく反映されていることを確認する方法。

### 前提条件

* Java 17 以上。  
* Apache POI 5.x（`Workbook`、`Worksheet`、`Style` を提供するライブラリ）。  
* コードサンプルと同様にイテレート可能な `DataTable` 実装。  
* Java と Excel の基本的な概念に慣れていること。

---

## 手順 1: プロジェクトの設定とデータのインポート

まず、プロジェクトに Apache POI を追加します。Maven を使用している場合は、以下の依存関係を含めてください。

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

次に、ソースデータを `DataTable` として取得します。実際のシナリオでは、データベースクエリ、CSV ファイル、または API のレスポンスから取得することがあります。

```java
// Step 1: Obtain the source data as a DataTable
DataTable dataTable = getData();   // replace with your own data‑fetching logic
```

> **プロのコツ:** `DataTable` の列が正しい Java 型（`Integer`、`Double` など）であることを確認してください。数値書式は数値セルにのみ影響します。

---

## 手順 2: 最初の列のために **カスタム数値書式** を作成する

**カスタム数値書式** は、Excel が数値をどのように表示するかを指示します。値を通貨として表示するには組み込みの `CURRENCY` 書式を使用しますが、`"$#,##0.00"` のようなパターンを定義することもできます。

```java
// Step 2: Prepare a Style array – one entry per column in the DataTable
Style[] columnStyles = new Style[dataTable.getColumns().size()];

// Step 3: Create a style for the first column and set it to display values as currency
// wb – existing Workbook instance (e.g., XSSFWorkbook for .xlsx files)
Workbook wb = new XSSFWorkbook();
columnStyles[0] = wb.createCellStyle();               // style first column
columnStyles[0].setDataFormat(
        wb.createDataFormat().getFormat(Style.CustomNumberFormat.CURRENCY));
```

**このように機能する理由:**

* `createCellStyle()` は再利用可能なスタイルオブジェクトを返します。  
* `setDataFormat()` は **通貨書式の設定** をスタイルに付与し、Excel はこのスタイルを使用するすべてのセルに適用します。  
* `columnStyles[0]` にスタイルを保存することで、最初の列だけが通貨書式を受け取ることが保証されます。

---

## 手順 3: 列スタイルを適用しながら `DataTable` をインポートする

ここでデータをワークシートにインポートします。`importDataTable` メソッドはスタイル配列を受け取るため、**最初の列にスタイルを適用**し、残りの列はデフォルトの書式のままにできます。

```java
// Step 4: Import the DataTable into the worksheet, applying the column styles
// ws – existing Worksheet instance
Worksheet ws = wb.createSheet("Report");

// true  → import column headers
// 0,0   → start at cell A1
ws.getCells().importDataTable(dataTable, true, 0, 0, columnStyles);
```

上記の呼び出しは最初の列にのみ **Excel の数値書式を設定** します。他のすべての列はワークブックのデフォルトスタイルを継承するため、コードがシンプルかつ効率的です。

---

## 手順 4: ワークブックを保存し、結果を確認する

最後に、ワークブックをファイルに書き出し、Excel で開いて最初の列に通貨記号が表示されていることを確認します。

```java
// Step 5: Save the workbook to disk
try (FileOutputStream fileOut = new FileOutputStream("FormattedReport.xlsx")) {
    wb.write(fileOut);
}
System.out.println("Workbook saved as FormattedReport.xlsx");
```

**期待される出力:**

*FormattedReport.xlsx* を開くと、列 A の値が適切な通貨記号（例: `$1,234.00`）で表示されます。他の列は元の数値表現のままです。

---

## 一般的なバリエーションとエッジケース

| Situation | Adjustment |
|-----------|------------|
| **異なる通貨**（例: ユーロ） | `Style.CustomNumberFormat.CURRENCY` をカスタムパターンに置き換えます: <br>`wb.createDataFormat().getFormat("\"€\"#,##0.00")` |
| **複数の列にスタイルを適用** | `columnStyles[]` に追加のエントリを作成し、それぞれに `CellStyle` オブジェクトを設定します。 |
| **大規模データセット** | `importDataTable` をバッチで使用するか、行をストリーム処理して `OutOfMemoryError` を回避します。 |
| **ロケール固有の区切り文字** | `java.text.NumberFormat` を使用してロケール対応のパターンを生成し、`setDataFormat` に渡します。 |

> **注意点:** 多くの列で単一の `CellStyle` オブジェクトを再利用すると、Excel がブックごとに許容できるスタイル数に制限があるため、予期しない書式になることがあります。必要な各書式ごとに別々のスタイルを作成してください。

---

## 完全に実行可能なサンプル

以下は、データ作成から書式設定されたワークブックの保存まで、全体のワークフローを示す自己完結型プログラムです。

```java
import java.io.FileOutputStream;
import java.util.ArrayList;
import java.util.List;

import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

/* Mock DataTable implementation for demonstration purposes */
class DataTable {
    private final List<String> columns = List.of("Amount", "Description");
    private final List<Object[]> rows = new ArrayList<>();

    public DataTable() {
        rows.add(new Object[]{1234.5, "Consulting"});
        rows.add(new Object[]{5678.9, "Licensing"});
    }

    public List<String> getColumns() { return columns; }
    public List<Object[]> getRows() { return rows; }
}

/* Helper that mimics the importDataTable method used in the original snippet */
class WorksheetHelper {
    private final Sheet sheet;
    private final Workbook wb;

    public WorksheetHelper(Workbook wb, Sheet sheet) {
        this.wb = wb;
        this.sheet = sheet;
    }

    public void importDataTable(DataTable dt, boolean includeHeaders,
                                int startRow, int startCol, Style[] styles) {
        int rowIdx = startRow;
        if (includeHeaders) {
            Row header = sheet.createRow(rowIdx++);
            for (int c = 0; c < dt.getColumns().size(); c++) {
                Cell cell = header.createCell(startCol + c);
                cell.setCellValue(dt.getColumns().get(c));
            }
        }
        for (Object[] rowData : dt.getRows()) {
            Row row = sheet.createRow(rowIdx++);
            for (int c = 0; c < rowData.length; c++) {
                Cell cell = row.createCell(startCol + c);
                Object value = rowData[c];
                if (value instanceof Number) {
                    cell.setCellValue(((Number) value).doubleValue());
                } else {
                    cell.setCellValue(value.toString());
                }
                // Apply custom style if provided
                if (styles != null && c < styles.length && styles[c] != null) {
                    cell.setCellStyle((CellStyle) styles[c]);
                }
            }
        }
    }
}

/* Main class that puts everything together */
public class CustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Obtain the source data
        DataTable dataTable = new DataTable();

        // 2️⃣ Create a workbook and a sheet
        Workbook wb = new XSSFWorkbook();
        Sheet ws = wb.createSheet("Report");

        // 3️⃣ Prepare a style array – one entry per column
        Style[] columnStyles = new Style[dataTable.getColumns().size()];

        // 4️⃣ Create a style for the first column (currency)
        CellStyle currencyStyle = wb.createCellStyle();
        DataFormat fmt = wb.createDataFormat();
        currencyStyle.setDataFormat(fmt.getFormat("$#,##0.00"));
        columnStyles[0] = currencyStyle;   // style first column

        // 5️⃣ Import the DataTable, applying the column styles
        WorksheetHelper helper = new WorksheetHelper(wb, ws);
        helper.importDataTable(dataTable, true, 0, 0, columnStyles);

        // 6️⃣ Save the workbook
        try (FileOutputStream out = new FileOutputStream("FormattedReport.xlsx")) {
            wb.write(out);
        }
        System.out.println("Workbook written to FormattedReport.xlsx");
    }
}
```

プログラムを実行すると **FormattedReport.xlsx** が作成され、列 A（「Amount」列）がドル記号と小数点以下2桁を示す **カスタム数値書式** で表示されます。

---

## 結論

これで、Java から Excel ワークシートに **カスタム数値書式** を適用し、**列を通貨として書式設定**、データをインポートしながら **最初の列にスタイルを適用**する方法が分かりました。再利用可能な `CellStyle` を作成し `importDataTable` に渡すことで、各セルを手動でループせずに任意の列に **Excel の数値書式を設定** できます。

次に試すこと:

* `setDataFormat` をロケール固有のパターンで使用して **通貨書式を設定** する

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Set Number Format Excel in Java – Complete Guide](/cells/english/java/formatting/set-number-format-excel-in-java-complete-guide/)
- [Apply Number Format Excel in Java – Complete Aspose.Cells Guide](/cells/english/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/)
- [How to create excel workbook with currency format and bold font in Java](/cells/english/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}