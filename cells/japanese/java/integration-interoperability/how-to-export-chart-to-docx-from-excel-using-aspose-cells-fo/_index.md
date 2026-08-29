---
category: general
date: 2026-08-20
description: Aspose.Cells for Java を使用して、チャートを DOCX にエクスポートし、Excel ワークブックを DOCX に変換する方法を学びましょう。完全なコード付きのステップバイステップガイドです。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export chart to docx
- convert excel workbook to docx
- Aspose.Cells Java
- editable chart DOCX
- Excel to Word conversion
language: ja
lastmod: 2026-08-20
og_description: Aspose.Cells for Java を使用して、チャートを DOCX にエクスポートし、Excel ワークブックを DOCX
  に変換します。この完全な実行可能チュートリアルに従ってください。
og_image_alt: Screenshot showing a Java code editor exporting an Excel chart to a
  DOCX file
og_title: Aspose.Cells を使ってチャートを docx にエクスポートする – Java ガイド
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to export chart to docx and convert Excel workbook to docx
    with Aspose.Cells in Java. Step‑by‑step guide with complete code.
  headline: How to export chart to docx from Excel using Aspose.Cells for Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- DOCX
- Excel
title: Aspose.Cells for Java を使用して Excel からチャートを docx にエクスポートする方法
url: /ja/java/integration-interoperability/how-to-export-chart-to-docx-from-excel-using-aspose-cells-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java を使用して Excel ワークブックからチャートを DOCX にエクスポートする

Excel ファイルから直接 **export chart to docx** する必要がある場合、このチュートリアルではすぐに実行できるソリューションを示します。ガイドの最後までに、**convert Excel workbook to docx** も、編集可能なチャートを保持したまま行う方法が分かります。その結果得られる Word 文書は、忠実度を失うことなく編集できます。

スプレッドシートの計算とリッチな Word レイアウトを組み合わせたレポートを作成する際、チャートのエクスポートは一般的です。Aspose.Cells for Java は変換をシンプルにし、API によりチャートを編集可能なまま保持できます—静的画像は不要です。

## このチュートリアルでカバーする内容

* チャートを含む既存のワークブックをロードする。  
* `ImageOrPrintOptions` を設定して DOCX フォーマットを対象にする。  
* `ExportEditableCharts` フラグを有効にする（バージョン 25.10 以降で利用可能）。  
* 編集可能なチャートを保持したままワークブックを DOCX ファイルとして保存する。  

Aspose.Cells JAR 以外に外部ツールは必要ありません。コードは Java 8+ と最新の Aspose.Cells バージョンで動作します。

## 前提条件

| Requirement | Why it matters |
|-------------|----------------|
| **Aspose.Cells for Java** (v25.10 or later) | このリリースで `setExportEditableCharts` 機能が導入されました。 |
| **Java Development Kit (JDK) 8 or newer** | サンプルのコンパイルと実行に必要なランタイムを提供します。 |
| **An Excel workbook (`.xlsx`) that contains at least one chart** | チャートは DOCX にエクスポートされる対象オブジェクトです。 |
| **A Java IDE or build tool (e.g., Maven, Gradle)** | 依存関係の管理と実行を簡素化します。 |

最新の Aspose.Cells JAR は [Aspose website](https://products.aspose.com/cells/java/) からダウンロードできます。

## 手順 1: プロジェクトを設定し Aspose.Cells の依存関係を追加する

Maven を使用する場合、以下の依存関係を `pom.xml` に追加してください。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version> <!-- use the latest version -->
</dependency>
```

Gradle を使用する場合、以下を追加してください。

```gradle
implementation 'com.aspose:aspose-cells:25.10'
```

> **Pro tip:** `ExportEditableCharts` を導入した正確なバージョン（25.10）またはそれ以降のリリースを使用してください。古いバージョンではフラグが無視され、代わりに静的画像が生成されます。

## 手順 2: チャートを含むワークブックをロードする

`Workbook` クラスは Excel ファイル全体を表します。ロードは 1 行の操作です。

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Load the workbook with the chart you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");
```

> **Why this matters:** エクスポートオプションを適用する前に、ワークブックは完全にロードされている必要があります。ファイルパスが間違っていると、Aspose.Cells は `FileNotFoundException` をスローします。

## 手順 3: DOCX 出力のための image/print オプションを設定する

`ImageOrPrintOptions` はワークブックのレンダリング方法を制御します。保存形式を `DOCX` に設定すると、Aspose.Cells は画像ではなく Word 文書を生成します。

```java
        // Create options and specify DOCX as the target format
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);
```

ここでページサイズ、DPI、画像品質なども調整できますが、チャートのエクスポートには必須ではありません。

## 手順 4: 編集可能なチャートのエクスポートを有効にする

バージョン 25.10 以降、Aspose.Cells はチャートをネイティブな Word チャートオブジェクトとして埋め込むことができます。これにより、Microsoft Word で完全に編集可能になります。

```java
        // Turn on the editable chart export flag
        options.setExportEditableCharts(true);
```

> **Edge case:** このフラグを `false` に設定する（または省略する）と、チャートは静的画像としてレンダリングされます。変換後にチャートを編集する必要がある対象者がいる場合のみ `true` を使用してください。

## 手順 5: ワークブックを DOCX ファイルとして保存する

最後に、設定したオプションで `Workbook.save` を呼び出します。

```java
        // Save the workbook as a DOCX document that contains an editable chart
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

プログラムが終了したら、Microsoft Word で `ChartEditable.docx` を開きます。元のチャートが表示され、右クリックすると **Edit Data** オプションが利用可能になっているはずです—これによりチャートが実際に編集可能であることが確認できます。

## 完全な実行可能サンプル

以下が完全なソースファイルです。IDE にコピーし、`YOUR_DIRECTORY` を絶対パスまたは相対パスに置き換えて実行してください。

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");

        // Step 2: Create image/print options and set the target format to DOCX
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);

        // Step 3: Enable exporting of editable charts (available from version 25.10)
        options.setExportEditableCharts(true);

        // Step 4: Save the workbook as a DOCX document with the configured options
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

**期待される出力**

- 指定ディレクトリに `ChartEditable.docx` という名前のファイルが作成されます。  
- Word でファイルを開くと、Excel に表示されていたチャートがそのまま表示され、チャートをダブルクリックするとデータ系列を編集できます。

## よくある落とし穴と回避方法

| 症状 | 原因 | 対策 |
|------|------|------|
| Word が編集可能なチャートではなく **静的画像** を表示する | `setExportEditableCharts` が呼び出されていない、またはバージョンが 25.10 未満 | フラグが `true` に設定されていること、かつ Aspose.Cells 25.10 以降を使用していることを確認してください。 |
| 生成された DOCX が **空白** になる | ソースワークブックのファイルパスが間違っている、または権限が不足している | ワークブックのパスと、アプリケーションが読み書き権限を持っているか確認してください。 |
| チャートのレイアウトが **歪んで** 見える | Excel のページ設定（例: 非表示行/列）が Word のデフォルトと異なる | `ImageOrPrintOptions` を調整（例: `setOnePagePerSheet(true)`）してスケーリングを制御してください。 |
| 大規模なワークブックで **パフォーマンス** が低下する | 多数のチャートや大規模データセットをエクスポートしている | 必要なシートだけをエクスポートするか、`setSheetIndex` を使用して処理を制限してください。 |

## ソリューションの拡張

- **Multiple charts:** すべてのワークシートを反復し、`worksheet.getCharts()` を呼び出して各チャートを個別にエクスポートします。  
- **Custom DOCX styling:** 保存後、Aspose.Words を使用して生成されたドキュメントにヘッダー、フッター、スタイルを適用します。  
- **Batch conversion:** `.xlsx` ファイルのディレクトリを処理するループでコードをラップし、各ファイルに対して DOCX を生成します。  

## 結論

これで、チャートの完全な編集可能性を保持したまま **export chart to docx** および **convert Excel workbook to docx** を行う信頼できる方法が手に入りました。重要な手順は、ワークブックのロード、DOCX 用の `ImageOrPrintOptions` 設定、`ExportEditableCharts` の有効化、そして結果の保存です。

ページ余白の設定やワークブックの数式埋め込みなど、追加オプションを試して出力をレポート作成フローに合わせて調整してください。Excel データからプログラムで Word レポートを生成する必要がある場合、このアプローチはクリーンで保守しやすいソリューションを提供します。

--- 

*試してみませんか？サンプルをクローンし、ファイルパスを更新してプログラムを実行してください。問題が発生した場合は、Aspose.Cells for Java のドキュメントを参照するか、以下の関連トピックをご覧ください。*  

### 次に探求できる関連トピック

- **convert excel workbook to pdf** – 同じワークブックから PDF レポートを生成します。  
- **Aspose.Cells chart formatting** – エクスポート前に色、マーカー、軸をカスタマイズします。  
- **Embedding images in DOCX with Aspose.Words** – チャートを他の Word コンテンツと組み合わせます。  

コーディングを楽しんでください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックをカバーしています。各リソースには、ステップバイステップの解説付きの完全なコード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.Cells for Java を使用してトレンドライン付き Excel チャートを作成し、画像にエクスポートする方法](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Aspose.Cells Java を使用して Excel チャートへのアクセスを自動化するステップバイステップガイド](/cells/english/java/charts-graphs/excel-charts-access-aspose-cells-java/)
- [Aspose.Cells for Java を使用して Excel チャートのデータラベルをカスタマイズするステップバイステップガイド](/cells/english/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}