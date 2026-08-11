---
category: general
date: 2026-08-11
description: JavaでAsposeを使用して新しいワークブックを作成し、Excelのカスタムプロパティを追加してから、ステップバイステップの完全な例でワークブックをXLSB形式で保存する。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook aspose
- save workbook as xlsb
- add custom property excel
- Aspose.Cells Java
- custom properties Excel
- workbook serialization
language: ja
lastmod: 2026-08-11
og_description: JavaでAsposeを使用して新しいワークブックを作成し、Excelのカスタムプロパティを追加して、完全な実行可能サンプルとともにワークブックをXLSBとして保存する。
og_image_alt: Java code screenshot that creates a new workbook Aspose, adds a custom
  Excel property, and saves it as an XLSB file
og_title: 新しいワークブックを作成 – AsposeでExcelにカスタムプロパティを追加
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  headline: Create new workbook Aspose – add custom property Excel and save as XLSB
  type: TechArticle
- description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  name: Create new workbook Aspose – add custom property Excel and save as XLSB
  steps:
  - name: What if I need to store a string property?
    text: '```java worksheet.getCustomProperties().add("Owner", "Alice"); ```'
  - name: Can I add multiple custom properties at once?
    text: Yes. Call `add` repeatedly for each name/value pair. Aspose.Cells does not
      limit the number of custom properties, but keep the total size reasonable to
      avoid bloating the file.
  - name: How does the binary format affect performance?
    text: XLSB files load faster because they avoid XML parsing. This is especially
      noticeable for workbooks with many rows, formulas, or embedded images.
  - name: What if I need to work with an existing XLSX file?
    text: Replace the `new Workbook()` constructor with `new Workbook("ExistingFile.xlsx")`.
      The rest of the steps (adding properties, saving as XLSB) remain identical.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- XLSB
- Custom Properties
title: Asposeで新しいワークブックを作成 – カスタムプロパティをExcelに追加してXLSBとして保存
url: /ja/java/spreadsheet-automation/create-new-workbook-aspose-add-custom-property-excel-and-sav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 新しいワークブック Aspose を作成 – カスタム プロパティ Excel を追加して XLSB として保存

If you need to **create new workbook Aspose** in a Java application, this guide shows you exactly how to do it. You will learn to **add custom property Excel**, retrieve the value, and **save workbook as XLSB** without losing any metadata.

このガイドでは、Java アプリケーションで **create new workbook Aspose** が必要な場合の手順を正確に示します。**add custom property Excel** の方法を学び、値を取得し、**save workbook as XLSB** でメタデータを失わずに保存する方法を学びます。

The tutorial covers everything from project setup to verification of the saved file. No external documentation is required; just follow the steps and run the code.

このチュートリアルでは、プロジェクトのセットアップから保存されたファイルの検証まで、すべてをカバーしています。外部ドキュメントは必要ありません。手順に従ってコードを実行するだけです。

## 前提条件

- Java Development Kit (JDK) 8 以上がインストールされていること。
- 依存関係管理のための Maven または Gradle（例では Maven を使用）。
- 有効な Aspose.Cells for Java ライセンス（またはテスト用に無料評価モードを使用）。

## 手順 1: Aspose.Cells をプロジェクトに追加

Add the Aspose.Cells Maven artifact to your `pom.xml`. This dependency provides the classes needed to **create new workbook Aspose** objects.

`pom.xml` に Aspose.Cells の Maven アーティファクトを追加します。この依存関係は **create new workbook Aspose** オブジェクトに必要なクラスを提供します。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

> **プロのコツ:** Gradle を使用したい場合は、Maven のスニペットを同等の `implementation "com.aspose:aspose-cells:23.12"` 行に置き換えてください。

## 手順 2: 新しい workbook Aspose を作成

The first functional step is to instantiate a `Workbook` object. This object represents an Excel file in memory and is the entry point for all further operations.

最初の機能的なステップは `Workbook` オブジェクトをインスタンス化することです。このオブジェクトはメモリ上の Excel ファイルを表し、以降のすべての操作のエントリーポイントとなります。

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {

    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();               // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0); // Default first sheet
```

新しい workbook Aspose を作成すると、デフォルトのワークシートが含まれたクリーンなブックが得られ、カスタマイズの準備が整います。

## 手順 3: カスタム プロパティ Excel を追加

Custom properties let you store arbitrary metadata inside an Excel file. Here we **add custom property Excel** named `ProjectId` with a numeric value.

カスタム プロパティを使用すると、Excel ファイル内に任意のメタデータを保存できます。ここでは数値の値を持つ `ProjectId` という名前の **add custom property Excel** を追加します。

```java
        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);
```

`add` メソッドはプロパティ名と、サポートされている任意の型（文字列、数値、日付など）の値を受け取ります。このメタデータはファイルをコピーした先でも一緒に保持されます。

## 手順 4: カスタム プロパティを取得して表示

Reading back the property verifies that it was stored correctly. You can also use the retrieved value in your business logic.

プロパティを読み戻すことで、正しく保存されたことを確認できます。取得した値はビジネスロジックでも使用できます。

```java
        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);
```

数値を保存したため `int` へのキャストが機能します。文字列を保存した場合は `(String)` を使用してください。

## 手順 5: workbook を XLSB として保存

Now you **save workbook as XLSB**. The XLSB format stores the workbook in a binary representation, which is faster to open and smaller on disk. All custom properties are preserved automatically.

ここで **save workbook as XLSB** を実行します。XLSB 形式はブックをバイナリ表現で保存するため、開く速度が速く、ディスク上のサイズも小さくなります。すべてのカスタム プロパティは自動的に保持されます。

```java
        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

特定のディレクトリに保存したい場合は、`"WithCustomProps.xlsb"` を絶対パスに置き換えてください。`SaveFormat.XLSB` 列挙体は Aspose.Cells にバイナリ形式で書き込むよう指示します。

## 手順 6: 出力を検証

Run the program from your IDE or command line:

```bash
mvn compile exec:java -Dexec.mainClass=CustomPropertiesXlsb
```

You should see:

```
ProjectId = 12345
```

Open `WithCustomProps.xlsb` in Excel. Navigate to **File → Info → Properties → Advanced Properties → Custom**. The `ProjectId` entry with value `12345` will be listed, confirming that the **add custom property excel** step succeeded and the **save workbook as xlsb** operation retained the metadata.

`WithCustomProps.xlsb` を Excel で開きます。**File → Info → Properties → Advanced Properties → Custom** の順に進みます。値が `12345` の `ProjectId` エントリが表示され、**add custom property excel** 手順が成功し、**save workbook as xlsb** 操作でメタデータが保持されたことが確認できます。

## よくある質問とエッジケース

### 文字列プロパティを保存したい場合は？

```java
worksheet.getCustomProperties().add("Owner", "Alice");
```

Retrieve it with:

```java
String owner = (String) worksheet.getCustomProperties().get("Owner").getValue();
```

### 複数のカスタム プロパティを一度に追加できますか？

はい。各名前/値のペアごとに `add` を繰り返し呼び出します。Aspose.Cells はカスタム プロパティの数に制限を設けていませんが、ファイルが肥大化しないよう総サイズは適切に保ってください。

### バイナリ形式はパフォーマンスにどのように影響しますか？

XLSB ファイルは XML パースを回避するため、読み込みが速くなります。特に行数や数式、埋め込み画像が多数あるブックで顕著です。

### 既存の XLSX ファイルで作業したい場合は？

`new Workbook()` コンストラクタを `new Workbook("ExistingFile.xlsx")` に置き換えます。残りの手順（プロパティの追加、XLSB として保存）は同じです。

## 完全なソースコード

Below is the complete, ready‑to‑run example. Copy it into a file named `CustomPropertiesXlsb.java` inside your `src/main/java` folder.

以下は完全な実行可能サンプルです。`src/main/java` フォルダー内に `CustomPropertiesXlsb.java` という名前でコピーしてください。

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();                       // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // Default first sheet

        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);

        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);

        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

Running this class produces an XLSB file that contains the custom property and can be opened in any modern version of Microsoft Excel.

このクラスを実行すると、カスタム プロパティを含む XLSB ファイルが生成され、最新の Microsoft Excel で開くことができます。

## 結論

You now know how to **create new workbook Aspose**, **add custom property Excel**, and **save workbook as XLSB** using Java. The example demonstrates the full lifecycle: initialization, metadata injection, verification, and binary serialization.

これで Java を使用して **create new workbook Aspose**、**add custom property Excel**、そして **save workbook as XLSB** を行う方法が分かりました。この例は、初期化、メタデータ注入、検証、バイナリシリアライズというフルライフサイクルを示しています。

Next, explore related topics such as **setting document properties**, **working with Excel formulas**, or **converting between XLSX and XLSB**. Each of these builds on the same Aspose.Cells API you just used, so you can extend the solution without learning new libraries.

次に、**setting document properties**、**working with Excel formulas**、**converting between XLSX and XLSB** などの関連トピックを探求してください。これらはすべて、先ほど使用した Aspose.Cells API を基にしているため、新しいライブラリを学ぶことなくソリューションを拡張できます。

Feel free to experiment with different data types, multiple worksheets, or password protection—Aspose.Cells supports all of those scenarios out of the box. Happy coding!

さまざまなデータ型、複数のワークシート、パスワード保護などを自由に試してみてください。Aspose.Cells はこれらすべてのシナリオを標準でサポートしています。コーディングを楽しんでください！

## 次に学ぶべきことは？

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックをカバーしています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose Cells Java で Excel ワークブックを作成・保存](/cells/english/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Aspose.Cells for Java を使用して Excel ワークブックを SVG として作成・保存する方法](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Aspose.Cells for Java で Excel ワークブックを作成しラベルを追加](/cells/english/java/advanced-excel-charts/data-labeling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}