---
category: general
date: 2026-09-27
description: JavaでExcelブックを作成し、SQLデータをインポートし、列の数値書式を設定し、Aspose.Cellsを使用してXLSXとして保存する。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- import sql data excel
- add number format excel
- set number format column
language: ja
lastmod: 2026-09-27
og_description: JavaでExcelブックを作成し、SQLデータをインポート、数値書式の列を設定し、完全に動作するJavaのサンプルでXLSXとして保存する。
og_image_alt: Screenshot of a Java program creating an Excel workbook with styled
  numeric columns
og_title: JavaでExcelブックを作成 – SQLデータをインポートし、列の数値形式を設定
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Create Excel workbook java, import SQL data, set number format column,
    and save workbook as XLSX using Aspose.Cells in Java.
  headline: Create Excel workbook java and apply column number formats
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Data import
title: JavaでExcelワークブックを作成し、列の数値フォーマットを適用する
url: /ja/java/formatting/create-excel-workbook-java-and-apply-column-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel ワークブックを Java で作成し、列の数値書式を適用する

**Excel ワークブックを Java で作成**し、数値列に書式を設定したい場合、本ガイドで手順をすべて解説します。SQL データを Excel にインポートし、各列に数値書式を設定し、**Aspose.Cells ライブラリ**を使用して **XLSX としてワークブックを保存**する方法を学べます。

Java からスプレッドシートを操作する際、開発者はコードをコピペしたり、数値の書式設定を忘れたり、CSV ファイルになってしまったりと断片的になりがちです。このチュートリアルは、任意の Java プロジェクトに組み込める、単一のエンドツーエンド ソリューションを提供し、こうした摩擦を取り除きます。

この記事を読み終えると、以下ができるようになります。

* データベースに接続し、`DataTable`（または `ResultSet`）を取得  
* Aspose.Cells で新しいワークブックを作成  
* すべての列に一貫した **add number format excel** スタイルを適用  
* 任意の場所に **XLSX としてワークブックを保存**  

前提条件は、Java 開発環境（JDK 8 以上推奨）と、クラスパスに Aspose.Cells for Java の JAR があることだけです。

---

## 前提条件

| Requirement | Why it matters |
|-------------|----------------|
| JDK 8 以上 | サンプルで使用している言語機能を提供します。 |
| Aspose.Cells for Java（最新バージョン） | Office がインストールされていなくても Excel の作成・書式設定・保存を処理します。 |
| JDBC 対応データベース（例: MySQL、PostgreSQL） | インポートする SQL データを供給します。 |
| Maven または Gradle（任意） | 依存関係の管理を簡素化します。 |

Maven の `pom.xml` に Aspose.Cells を追加します:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- use the latest stable version -->
</dependency>
```

または Aspose のウェブサイトから JAR を直接ダウンロードし、プロジェクトのクラスパスに追加してください。

---

## 手順 1: Excel ワークブックを Java で作成

最初の論理ブロックは新しい `Workbook` をインスタンス化することです。このオブジェクトはメモリ上の Excel ファイル全体を表し、ワークシート、セル、スタイルへのアクセスを提供します。

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

ワークブックを先に作成しておくことで、後で **set number format column** に必要となる `Style` ファクトリを取得できます。

---

## 手順 2: SQL からデータを取得（import sql data excel）

以下では JDBC 接続を開き、シンプルな `SELECT` 文を実行し、結果セットを Aspose の `DataTable` にロードします。`DataTable` クラスは .NET の `DataTable` を模倣しており、`importDataTable` メソッドとシームレスに連携します。

```java
// Step 2: Pull data from a database and fill a DataTable
private static DataTable getDataTableFromDb() throws SQLException {
    // Replace with your actual connection string, user, and password
    String url = "jdbc:mysql://localhost:3306/yourdb";
    String user = "your_user";
    String password = "your_password";

    try (Connection conn = DriverManager.getConnection(url, user, password);
         Statement stmt = conn.createStatement();
         ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

        // Aspose.Cells provides a utility to convert ResultSet → DataTable
        return CellsHelper.getDataTableFromResultSet(rs);
    }
}
```

> **Tip:** 既に別のソース（例: CSV パース）から `DataTable` を取得している場合は、JDBC のコードを省略してそのテーブルを直接返すことができます。

---

## 手順 3: 再利用可能なスタイルを作成（add number format excel）

数値列すべてに対して「小数点以下 2 桁・千位区切り」の表示にしたいとします。各セルに個別に書式を設定するのではなく、列ごとに `Style` オブジェクトを一度作成し、インポート時に再利用します。これが **add number format excel** を実現する最も効率的な方法です。

```java
// Step 3: Build a style array – one style per column
private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
    Style[] styles = new Style[columnCount];
    for (int i = 0; i < columnCount; i++) {
        styles[i] = workbook.createStyle();
        // "0.00" = two decimal places; "#,##0.00" adds thousands separator
        styles[i].setNumber("#,##0.00");
    }
    return styles;
}
```

書式文字列（`"#,##0.00"`）は必要に応じて任意の Excel 数値書式に変更できます。日付の場合は `styles[i].setCustom("mm-dd-yyyy")` などとしてください。

---

## 手順 4: DataTable をインポートし、列スタイルを適用

ここで全体を統合します。`importDataTable` のオーバーロードを使用すると、`DataTable` を渡し、最初の行を列ヘッダーとして扱うかどうかを指定し、スタイル配列を提供できます。これにより、対応する列の各セルに自動的に **set number format column** が適用されます。

```java
// Step 4: Import data with styles into the first worksheet
private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
    // Build a style for each column based on the number of columns in the DataTable
    Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());

    // Import the DataTable starting at cell A1 (row 0, column 0)
    workbook.getWorksheets().get(0).getCells()
            .importDataTable(dataTable, true, 0, 0, columnStyles);
}
```

`importColumnNames` フラグに `true` を渡したため、ワークシートの最初の行には `DataTable` の列名が配置されます。その後の行は、定義したスタイルに従ってフォーマットされたデータが入ります。

---

## 手順 5: XLSX としてワークブックを保存

最後のステップは、メモリ上のワークブックを実際のファイルに永続化することです。Aspose.Cells は多数の形式をサポートしていますが、ここでは現代的な XLSX 形式を使用します。これはほとんどのアプリケーションが現在期待している形式です。

```java
// Step 5: Save the workbook to an .xlsx file
private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
    workbook.save(filePath, com.aspose.cells.SaveFormat.XLSX);
}
```

`filePath` をシステム上の任意の有効な場所に変更できます。ディレクトリが存在しない、または書き込み権限がない場合は `IOException` がスローされます。

---

## 完全な実行可能サンプル

すべての部品を組み合わせると、すぐにコンパイルして実行できる自己完結型プログラムが完成します。

```java
import com.aspose.cells.*;
import java.sql.*;

public class CreateExcelWorkbookJava {
    public static void main(String[] args) {
        try {
            // 1️⃣ Obtain data from the database
            DataTable dataTable = getDataTableFromDb();

            // 2️⃣ Create a new workbook that will hold the imported data
            Workbook workbook = new Workbook();

            // 3️⃣ Import the DataTable with a numeric style per column
            importDataWithStyles(workbook, dataTable);

            // 4️⃣ Save the workbook as XLSX
            String outputPath = "DataTableWithNumberFormat.xlsx";
            saveWorkbook(workbook, outputPath);

            System.out.println("Workbook created successfully at: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    // ---- Helper methods (see earlier sections) ----
    private static DataTable getDataTableFromDb() throws SQLException {
        String url = "jdbc:mysql://localhost:3306/yourdb";
        String user = "your_user";
        String password = "your_password";

        try (Connection conn = DriverManager.getConnection(url, user, password);
             Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

            return CellsHelper.getDataTableFromResultSet(rs);
        }
    }

    private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
        Style[] styles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++) {
            styles[i] = workbook.createStyle();
            styles[i].setNumber("#,##0.00"); // two decimals with thousands separator
        }
        return styles;
    }

    private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
        Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());
        workbook.getWorksheets().get(0).getCells()
                .importDataTable(dataTable, true, 0, 0, columnStyles);
    }

    private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
        workbook.save(filePath, SaveFormat.XLSX);
    }
}
```

### 期待される結果

プログラムを実行すると、作業ディレクトリに **DataTableWithNumberFormat.xlsx** という名前のファイルが作成されます。Microsoft Excel、LibreOffice Calc、または任意の XLSX 対応ビューアで開くと、以下のように表示されます。

| Id | Amount | CreatedDate |
|----|--------|-------------|
| 1  | 1,234.56 | 2023‑01‑15 |
| 2  | 78,900.00 | 2023‑02‑20 |
| …  | … | … |

***Amount** 列は **add number format excel** スタイルにより、小数点以下 2 桁・千位区切りで数値が表示されます。*

---

## よくある質問とエッジケースの対処

| Question | Answer |
|----------|--------|
| **クエリが行を返さない場合はどうなりますか？** | `DataTable` は空になりますが、列定義は保持されます。ワークブックにはヘッダー行だけが残り、下流プロセスで十分なことが多いです。 |
| **列ごとに異なる書式を適用したい場合は？** | `buildColumnStyles` を修正し、列名やデータ型をチェックしてカスタム書式（例: 日付、パーセンテージ）を割り当てます。 |
| **`ByteArrayOutputStream` へ直接書き込むことはできますか？** | はい。`workbook.save(filePath, SaveFormat.XLSX);` を `workbook.save(outputStream, SaveFormat.XLSX);` に置き換えるだけです。 |

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれているため、API の追加機能を習得したり、独自の実装アプローチを探求したりする際に役立ちます。

- [Aspose.Cells for Java を使用して Excel ワークブックを SVG として作成および保存する方法](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Aspose.Cells for Java で Excel ワークブックを作成・保存する（ヒンディー語）](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Aspose.Cells for Java で Excel ワークブックを作成・保存する（ドイツ語）](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}