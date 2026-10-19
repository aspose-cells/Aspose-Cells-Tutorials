---
date: '2026-09-27'
description: Aspose.Cells を使用して Java で円グラフを作成する方法を学びます。Excel の円グラフをカスタマイズし、Maven 依存関係を設定し、プロフェッショナルなチャートを生成するステップバイステップガイドです。
keywords:
- create pie chart java
- customize excel pie chart
- maven dependency aspose cells
lastmod: '2026-09-27'
og_description: Aspose.Cells for Java を使用して円グラフを作成します。Excel の円グラフをカスタマイズし、Maven 依存関係を追加し、数分でプロフェッショナルなチャートを生成する方法を学びます。
og_image_alt: Java code generating a customized pie chart in Excel with Aspose.Cells
og_title: Aspose.Cells で Java の円グラフを作成 – 完全 Java ガイド
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to create pie chart java using Aspose.Cells. Step‑by‑step
    guide to customize Excel pie chart, set up Maven dependency, and generate professional
    charts.
  headline: How to create pie chart java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes, repeat the chart‑creation steps for each data range; each chart is
      independent.
    question: Can I generate multiple pie charts in the same workbook?
  - answer: It does; set the chart type to `ChartType.PIE_3D` when adding the chart.
    question: Does Aspose.Cells support 3‑D pie charts?
  - answer: Use the `Workbook.setDefaultTheme` method before creating any charts.
    question: How do I apply a custom theme to all charts?
  - answer: Over 30 formats, including XLSX, CSV, PDF, and HTML.
    question: What file formats can I export the workbook to?
  - answer: Yes, a valid license removes evaluation watermarks and unlocks full functionality.
    question: Is a license required for commercial deployment?
  type: FAQPage
tags:
- Aspose.Cells
- Java charting
- Excel automation
- data visualization
title: Aspose.Cells を使用した Java の円グラフ作成方法
url: /ja/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells を使用した Java の円グラフ作成方法

## はじめに
プログラムで **pie chart** を作成することは、特に色、凡例、タイトルを細かく制御する必要がある場合、パズルのように感じられることがあります。このガイドでは Aspose.Cells を使用して **create pie chart java** の方法を学び、Excel の円グラフをブランドやレポート様式に合わせてカスタマイズします。環境設定、データ入力、チャート生成、ビジュアル調整をすべて Java IDE から離れることなく順に解説します。

**学習内容**
- プロジェクトに **Maven dependency Aspose.Cells** を追加する。
- ワークブックを作成し、セルにデータを入力して円グラフを生成する。
- チャートにカスタムカラー、タイトル、凡例を適用する。
- ワークブックを共有用の XLSX ファイルとしてエクスポートする。

開始する前に、基本的な Java 文法に慣れており、Maven または Gradle がインストールされていることが必要です。

## クイック回答
- **Which library creates pie charts in Java?** Aspose.Cells for Java.
- **Do I need a license?** 開発には無料トライアルが使用でき、製品版には有料ライセンスが必要です。
- **What Maven coordinates are required?** `com.aspose:aspose-cells:24.10`.
- **Can I change slice colors?** はい、各シリーズの `setAreaColor` メソッドで変更できます。
- **Is the chart exportable to XLSX?** もちろんです—`workbook.save("output.xlsx")` を呼び出すだけです。

## Excel の円グラフとは何か？

円グラフは、単一のデータ系列を円の比例的なスライスとして視覚化し、全体の一部を比較しやすくします。各スライスの角度は、総計に対するその値に比例し、市場シェア、予算配分、人口統計のパーセンテージなどのカテゴリ別分布を迅速に把握できます。

## なぜ Aspose.Cells を使用して Java の円グラフを作成するのか？

Aspose.Cells は 50 種類以上のチャートタイプをサポートし、ファイル全体をメモリに読み込むことなく、最大 100 万行のワークシートを処理できます。このパフォーマンスの優位性により、低スペックのハードウェアでも大規模なレポートを生成でき、チャートの外観、データバインディング、エクスポート形式を細かく制御できるため、多くの open‑source ライブラリよりも優れた選択肢となります。

## 前提条件
- **Java Development Kit (JDK)** 8 以上。
- **IDE**（例：IntelliJ IDEA または Eclipse）。
- 依存関係管理のための **Maven** または **Gradle**。
- **trial or purchased Aspose.Cells license**。

### 必要なライブラリと依存関係
`pom.xml` に Aspose.Cells の Maven アーティファクトを追加します:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

または Gradle の等価設定:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### ライセンス取得手順
Aspose.Cells for Java は商用製品ですが、無料トライアルから始めることができます。テンポラリライセンスキーを取得するには、[purchase page](https://purchase.aspose.com/buy) をご覧ください。

## Aspose.Cells for Java の設定
まず、ライブラリがクラスパスにあることを確認してください。依存関係を追加したら、以下のように API を初期化できます。

```java
import com.aspose.cells.Workbook;

// Initialize a new workbook instance
Workbook workbook = new Workbook();
```

## 実装ガイド

### ワークブックの作成と構成
`Workbook` クラスは、メモリ上の Excel ファイル全体を表します。

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### Step 1: ワークブックをインスタンス化する
```java
// Creates an empty workbook instance to work with.
Workbook workbook = new Workbook();
```  
これは新しい空のワークブックを作成し、すぐにデータを入力し始めることができます。

### ワークシートのセルへのアクセスまたは変更
`Worksheet` はワークブック内の単一シートを表し、セル、行、列を含みます。  
円グラフのデータとなる情報をワークシートに書き込みます。

#### Step 2: 最初のワークシートとそのセルを取得する
```java
// Access the first worksheet in the workbook.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Put sample values used for a pie chart into specific cells.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Put percentage values for a pie chart into specific cells.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```  
セルにカテゴリ名と値を入力し、チャートが使用できるようにします。

### 円グラフの作成
`Chart` オブジェクトはワークシート内のデータを可視化し、円、棒、折れ線などさまざまなタイプをサポートします。

#### Step 3: ワークシートに円グラフを追加する
```java
// Create a pie chart in the worksheet.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```  

### 円グラフのシリーズとデータの構成
`Series` はチャートのデータ範囲と書式設定を定義し、ワークシートのセルとビジュアル要素を結びつけます。

#### Step 4: チャートのシリーズを設定する
```java
// Configure the series data range for the chart.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Link the pie chart title to a cell containing the title text.
pie.getTitle().setLinkedSource("D2");
```  

### チャートの凡例とタイトルの外観設定
チャートの `Legend` はシリーズ名とカラーを表示し、各スライスを識別しやすくします。

#### Step 5: チャートの凡例とタイトルをカスタマイズする
```java
// Set legend position at bottom of the chart.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Set font properties for the chart title.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```  

### チャートシリーズの色をカスタマイズする
`setAreaColor` は RGB 値を使用してチャートシリーズのスライスの塗りつぶし色を設定します。

#### Step 6: 円グラフのセグメント色を変更する
```java
import com.aspose.cells.Color;

// Access and customize colors of individual pie chart segments.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```  

### 列の自動調整とワークブックの保存
`autoFitColumns` はセルの内容に合わせて列幅を自動的に調整します。

#### Step 7: 列幅を調整し、ファイルを保存する
```java
// Autofit all columns.
worksheet.autoFitColumns();

// Define output directory placeholder path for saving the workbook.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Save the modified workbook to an Excel file in the specified directory.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```  

## 一般的な使用例
- **Demographic analysis:** 地域別の人口分布を示す。
- **Market‑share reporting:** 各競合他社のシェアを一目で可視化する。
- **Budget allocation:** 部門別の予算配分をハイライトする。

## パフォーマンス上の考慮点
- 必要なくなったオブジェクトは (`workbook.dispose()`) を呼び出して解放し、ネイティブメモリを確保します。
- 大規模データセットの場合、`WorkbookDesigner` を使用してデータをストリーミングし、すべてを一度にロードしないようにします。
- Java Flight Recorder でプロファイルし、チャート生成時のボトルネックを特定します。

## よくある質問

**Q: Can I generate multiple pie charts in the same workbook?**  
A: はい、各データ範囲に対してチャート作成手順を繰り返すことで、複数の円グラフを同一ワークブックに生成できます。各チャートは独立しています。

**Q: Does Aspose.Cells support 3‑D pie charts?**  
A: 対応しています。チャートを追加する際にチャートタイプを `ChartType.PIE_3D` に設定してください。

**Q: How do I apply a custom theme to all charts?**  
A: チャートを作成する前に `Workbook.setDefaultTheme` メソッドを使用してカスタムテーマを適用します。

**Q: What file formats can I export the workbook to?**  
A: XLSX、CSV、PDF、HTML など、30 以上の形式にエクスポートできます。

**Q: Is a license required for commercial deployment?**  
A: はい、有効なライセンスが評価用の透かしを除去し、すべての機能を利用可能にします。

## 結論
Aspose.Cells を使用した **create pie chart java** の完全な手順が揃いました。上記の手順に従うことで、洗練された Excel の円グラフを生成し、色やタイトルをカスタマイズして、任意のレポートパイプラインに組み込むことができます。他のチャートタイプ（棒、折れ線、レーダー）も試して、データ可視化ツールキットを拡充しましょう。

---

**最終更新日:** 2026-09-27  
**テスト環境:** Aspose.Cells 24.10 for Java  
**作者:** Aspose

## 関連チュートリアル

- [Aspose.Cells for Java を使用した Excel チャート データ ラベルのカスタマイズ&#58; ステップバイステップ ガイド](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Aspose.Cells Java で動的 Excel チャートを作成する&#58; 開発者向け包括的ガイド](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Aspose.Cells Java を使用した Excel ワークブックの作成とカスタマイズ&#58; ステップバイステップ ガイド](/cells/java/workbook-operations/create-customize-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}