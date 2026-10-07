---
category: general
date: 2026-10-07
description: Aspose.Cells を使用して JSON を Excel にロードし、JSON から XLSX を生成する方法を学びます。このステップバイステップガイドでは、JSON
  から Excel にデータを入力し、ブックを XLSX として保存する方法も示しています。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- load json into excel
- generate xlsx from json
- populate excel from json
- save workbook as xlsx
- create workbook from json
language: ja
lastmod: 2026-10-07
og_description: JSON を Excel に読み込み、Aspose.Cells for Java を使用して JSON から XLSX を生成します。このガイドに従って
  JSON から Excel を作成し、ブックを XLSX として保存してください。
og_image_alt: Screenshot of an Excel workbook that was loaded with JSON data using
  Aspose.Cells
og_title: Aspose.CellsでJSONをExcelにロードする – 完全なJavaガイド
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to load JSON into Excel and generate XLSX from JSON using
    Aspose.Cells. This step‑by‑step guide also shows how to populate Excel from JSON
    and save workbook as XLSX.
  headline: How to load JSON into Excel with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to load JSON into Excel and generate XLSX from JSON using
    Aspose.Cells. This step‑by‑step guide also shows how to populate Excel from JSON
    and save workbook as XLSX.
  name: How to load JSON into Excel with Aspose.Cells for Java
  steps:
  - name: 'Compile the program:'
    text: 'Compile the program:'
  - name: 'Run it:'
    text: 'Run it:'
  - name: Verify that `JsonSingleCell.xlsx` appears in the working directory and opens
      without errors.
    text: Verify that `JsonSingleCell.xlsx` appears in the working directory and opens
      without errors.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Aspose.Cells for Java を使用して JSON を Excel にロードする方法
url: /ja/java/excel-import-export/how-to-load-json-into-excel-with-aspose-cells-for-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java 用 Aspose.Cells で JSON を Excel にロードする

Excel に **JSON をロード** する必要がある場合、このチュートリアルでは Aspose.Cells for Java を使用した信頼できる方法を示します。JSON から XLSX を生成し、JSON から Excel を入力し、最後に **ワークブックを XLSX として保存** する方法を、単一の自己完結型プログラムで確認できます。

Web サービス、API、または NoSQL ストアからデータをエクスポートする際に、スプレッドシートで JSON を扱うことは一般的です。このガイドの最後までに、JSON からワークブックを作成し、結果をディスク上のファイルに書き込む、すぐに実行可能な Java クラスが手に入ります。

## 前提条件

* Java 8 以上がインストールされていること（コードは標準の Java 機能を使用します）。
* Aspose.Cells for Java ライブラリ（バージョン 23.10 以降）。[Aspose のウェブサイト](https://downloads.aspose.com/cells/java) または Maven Central から入手できます。
* IDE またはシンプルなテキストエディタと、Java コードをコンパイル・実行するためのターミナル。
* JSON 構文と Excel の概念に関する基本的な知識。

> **プロのコツ:** Maven を使用している場合、手動で JAR を管理しないように `pom.xml` に次の依存関係を追加してください：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
</dependency>
```

## 手順 1: プロジェクトを設定し、必要なクラスをインポートする

`JsonToExcelDemo` という名前の新しい Java クラスを作成します。ワークブック作成、ワークシート操作、Smart Marker 処理に必要な Aspose.Cells クラスをインポートします。

```java
package com.example.exceljson;

import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerProcessor;
import com.aspose.cells.SaveFormat;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // The full implementation starts in the next step.
    }
}
```

*この手順が重要な理由:* 正しいクラスをインポートすることで、コンパイラが Aspose.Cells API を見つけられるようになります。`Workbook` クラスは Excel ファイルを表し、`SmartMarkerProcessor` が JSON から Excel への変換を実行します。

## 手順 2: Excel にロードする JSON ソースを定義する

この例では、2 つのオブジェクトを含む小さな JSON 配列を使用します。実際のシナリオでは、JSON をファイル、REST エンドポイント、またはデータベースから読み取ることができます。

```java
// Step 2: Define the JSON data that will be used as the smart‑marker source
String jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";
```

*この手順が重要な理由:* JSON 文字列は **JSON から Excel を入力** 操作のデータソースです。JSON を `String` 変数に保持することで、`SmartMarkerProcessor` に簡単に渡せます。

## 手順 3: 新しいワークブックを作成し、最初のワークシートを取得する

新しいワークブックはクリーンな状態を提供します。最初のワークシート（インデックス 0）は、Smart Marker を挿入する場所です。

```java
// Step 3: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty XLSX workbook
Worksheet worksheet = workbook.getWorksheets().get(0);
```

*この手順が重要な理由:* Aspose.Cells は後で XLSX ファイルとして保存できる `Workbook` オブジェクトで動作します。最初の `Worksheet` にアクセスすることで、既知のセルアドレスにマーカーを配置できます。

## 手順 4: Aspose.Cells に JSON の扱い方を指示する Smart Marker を挿入する

Smart Markers は、ソースからのデータで置き換えられるプレースホルダーです。マーカー `&=JSONData.ArrayAsSingle` は、ライブラリに JSON 配列全体を単一セルの値として扱うよう指示します。

```java
// Step 4: Insert a smart‑marker that tells Aspose.Cells to treat the JSON array as a single cell
worksheet.getCells().putValue(0, 0, "&=JSONData.ArrayAsSingle");
```

*この手順が重要な理由:* `ArrayAsSingle` を使用すると、各配列要素が別々の行に展開されるデフォルト動作を回避できます。セル内に JSON テキストをそのまま表示したい場合や、後で数式で分割する予定がある場合に便利です。

## 手順 5: JSON データソースで SmartMarkerProcessor を構成する

JSON 文字列を論理名 `JSONData` にバインドします。プロセッサはマーカーを実際のデータに置き換えます。

```java
// Step 5: Configure the SmartMarkerProcessor with the JSON data source
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
processor.setDataSource("JSONData", jsonData);
processor.process();   // expands the marker and writes JSON into the worksheet
```

*この手順が重要な理由:* `setDataSource` はマーカーで使用される名前（`JSONData`）と実際の JSON ペイロードを結び付けます。`process()` は重い処理を実行し、JSON の解析、マーカーロジックの適用、結果のワークシートへの書き込みを行います。

## 手順 6: 結果のワークブックを XLSX ファイルとして保存する

最後に、ワークブックをディスクに書き出します。`SaveFormat.XLSX` 定数は正しい Office Open XML 形式であることを保証します。

```java
// Step 6: Save the resulting workbook
String outputPath = "JsonSingleCell.xlsx";   // adjust the path as needed
workbook.save(outputPath, SaveFormat.XLSX);
System.out.println("Workbook saved to " + outputPath);
```

*この手順が重要な理由:* ファイルの保存により **JSON から XLSX を生成** ワークフローが完了します。生成されたファイルは Excel、LibreOffice、または XLSX をサポートする任意のスプレッドシートプログラムで開くことができます。

### 完全なソースコード

すべての要素を組み合わせた、**JSON からワークブックを作成**、**JSON から Excel を入力**、そして **ワークブックを XLSX として保存** する完全で実行可能なプログラムを以下に示します。

```java
package com.example.exceljson;

import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerProcessor;
import com.aspose.cells.SaveFormat;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // 1. JSON source – replace with your own data if needed
        String jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

        // 2. Create a fresh workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3. Place a smart‑marker that treats the JSON array as a single cell
        worksheet.getCells().putValue(0, 0, "&=JSONData.ArrayAsSingle");

        // 4. Bind the JSON string to the marker name and process it
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
        processor.setDataSource("JSONData", jsonData);
        processor.process();

        // 5. Save the workbook as an XLSX file
        String outputPath = "JsonSingleCell.xlsx";
        workbook.save(outputPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

### 期待される結果

`JsonSingleCell.xlsx` を開くと、JSON 配列がセル **A1** に元の文字列とまったく同じ形で表示されます：

```
[{"Name":"John","Age":30},{"Name":"Anna","Age":25}]
```

各オブジェクトを別々の行にしたい場合は、マーカーを `&=JSONData`（`.ArrayAsSingle` なし）に置き換えてください。プロセッサは配列を個別の行に展開し、別の **JSON から Excel を入力** 手法を実演します。

## 一般的なバリエーションとエッジケース

| 状況 | 調整 |
|-----------|------------|
| **大きな JSON ペイロード ( > 10 MB )** | JVM のヒープサイズを (`-Xmx2g`) に増やし、`OutOfMemoryError` を回避するために JSON のストリーミングを検討してください。 |
| **入れ子オブジェクト** | テーブル内で `&=JSONData.Name` や `&=JSONData.Age` のような階層マーカーを使用して、各プロパティを列にマッピングします。 |
| **文字列ではなく JSON ファイル** | `java.nio.file.Files.readString(Path.of("data.json"))` を使用してファイルを `String` に読み込み、`setDataSource` に渡します。 |
| **元の JSON 形式を保持する必要がある** | `.ArrayAsSingle` サフィックスを保持するか、後で JSON を解析する Excel の数式を使用する予定がある場合は JSON を CDATA でラップしてください。 |
| **複数のワークシート** | 追加のワークシートを作成し（`workbook.getWorksheets().add("Sheet2")`）、各シートでマーカーの挿入を繰り返します。 |

> **警告:** Smart Markers は大文字小文字を区別します。マーカーと `setDataSource` の間で論理名（`JSONData`）が完全に一致していることを確認してください。

## ソリューションのテスト

1. プログラムをコンパイルする：

   ```bash
   javac -cp ".:aspose-cells-23.10.jar" com/example/exceljson/JsonToExcelDemo.java
   ```

2. 実行する：

   ```bash
   java -cp ".:aspose-cells-23.10.jar" com.example.exceljson.JsonToExcelDemo
   ```

3. 作業ディレクトリに `JsonSingleCell.xlsx` が生成され、エラーなく開けることを確認します。

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックをカバーしています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [JSON から Excel ワークブックを作成 – 完全な Aspose.Cells ガイド](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Excel ワークブック C# 作成 – JSON を挿入して XLSX として保存](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)
- [JSON から Excel ワークブックを保存 – 完全ガイド](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}