---
date: 2026-09-02
description: Aspose.Cells for Java を使用して、チャートを PNG にエクスポートし、データシリーズを追加し、line column
  chart を結合し、ワークブックを XLSX として保存し、legend chart を追加する方法を学びます。
keywords:
- export chart to png
- combine line and column chart
- save workbook as xlsx
- generate chart image java
lastmod: 2026-09-02
linktitle: チャートを PNG にエクスポートし、結合チャート用にデータシリーズを追加
og_description: Aspose.Cells for Java を使用して、チャートを PNG にエクスポートし、line and column chart
  を結合し、データシリーズを追加し、ワークブックを XLSX として保存する単一チュートリアルです。
og_image_alt: Developer guide showing combined line‑column chart export to PNG using
  Aspose.Cells for Java
og_title: チャートを PNG にエクスポートし、結合チャート用にデータシリーズを追加
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  headline: Export chart to PNG and add data series for combined chart
  type: TechArticle
- description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  name: Export chart to PNG and add data series for combined chart
  steps:
  - name: import aspose.cells classes
    text: '`Workbook` is Aspose.Cells’ core object that represents an entire Excel
      file in memory.'
  - name: create a new workbook
    text: '`Worksheet` represents a single sheet inside a `Workbook` and provides
      access to cells, rows, and charts.'
  - name: access the first worksheet
    text: '`Chart` is the object that holds all chart‑related settings, series, and
      rendering options.'
  - name: add a combined chart object to the worksheet
    text: We’ll start with a line chart and later add a column series to achieve a
      **combined line column chart** effect.
  - name: define the data ranges and add data series
    text: '`NSeries` is the collection that stores each data series for a chart. Adding
      a series links a range of cells to the chart. > **Pro tip:** The first parameter
      (`"A1:A5"`) is the range for the first series, and the second (`"B1:B5"`) creates
      a second series that will be combined with the first.'
  - name: set the category (X‑axis) data
    text: '`CategoryAxis` represents the horizontal axis of the chart, controlling
      the labels displayed along the X‑axis.'
  - name: set chart axis labels and title
    text: '`Title` sets the main title of the chart, and `Axis` objects represent
      the X and Y axes.'
  - name: add legend chart and adjust its position
    text: '`Legend` controls the placement and appearance of the series legend in
      the chart.'
  - name: save the workbook as an Excel file (XLSX)
    text: '`Workbook.save` writes the in‑memory workbook to a file in the specified
      format.'
  - name: export chart to PNG
    text: '`Chart.toImage` renders the chart as an image file in the chosen format.
      > The `chart.toImage` method **generates Excel chart** images that can be used
      in web pages, reports, or emails.'
  type: HowTo
- questions:
  - answer: 'Download the JAR from the official site and add it to your project’s
      classpath. The download link is: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).'
    question: How do I install Aspose.Cells for Java?
  - answer: Yes, Aspose.Cells supports bar, pie, scatter, area, and many more chart
      types. Refer to the API documentation for the full list.
    question: Can I create other chart types besides line and column?
  - answer: A valid Aspose.Cells license is required for production deployments. A
      free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Use `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (or similar)
      after adding the series.
    question: How can I change the colors of each series?
  - answer: 'Comprehensive documentation and additional samples are available at the
      Aspose reference site: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more code examples?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart to png
- Aspose.Cells
- Java Excel charts
title: チャートを PNG にエクスポートし、結合チャート用にデータシリーズを追加
url: /ja/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNGにチャートをエクスポートし、結合チャート用にデータ系列を追加する

このチュートリアルでは、Excelブックに**データ系列を追加**し、**折れ線グラフと縦棒グラフを結合**し、Aspose.Cells for Java を使用して**チャートを PNG にエクスポート**する方法を学びます。ワークブックの設定、ワークシートへのチャート追加、凡例のカスタマイズ、**ワークブックを XLSX として保存**し、チャートの PNG 画像を生成するまでのすべての手順を順に説明します。最後まで実行すれば、レポートやダッシュボードに埋め込める、すぐに使用できる結合チャートが完成します。

## クイック回答
- **どのライブラリが結合チャートを作成しますか？** Aspose.Cells for Java.  
- **データ系列はどうやって追加しますか？** 適切な範囲を指定して `chart.getNSeries().add(...)` を呼び出します。  
- **チャートを PNG にエクスポートするには？** `chart.toImage("chart.png", ImageFormat.getPng())` を使用します。  
- **ワークブックはどのファイル形式で保存できますか？** 標準の `.xlsx`（ワークブックを XLSX として保存）。  
- **本番環境でライセンスは必要ですか？** はい – 本番展開には有効な Aspose.Cells ライセンスが必要です。

## Aspose.Cells におけるチャートの PNG エクスポートとは？

チャートを PNG にエクスポートすると、Excel のチャートをラスタ画像として生成でき、Excel アプリケーションを必要とせずにウェブページ、レポート、メールなどで表示できます。この方法は、正確なビジュアルレイアウト、色、データマーカーをそのままキャプチャし、ポータブルな画像ファイルを作成します。

## なぜ折れ線と縦棒の結合チャートを作成するのか？

結合折れ線・縦棒チャートを使用すると、異なるデータセットをそれぞれ異なるビジュアル表現（例：縦棒系列の上に折れ線系列）で単一のビューに表示できます。この手法は、トレンドと合計を比較したり、相関関係を強調したり、視覚的なフットプリントを小さく保ちながらより豊かな洞察を提供するのに最適です。

## 前提条件
- Java Development Kit (JDK) 8 以上  
- Aspose.Cells for Java ライブラリ（以下のリンクからダウンロード）  
- Java の構文と Excel の概念に関する基本的な知識  

## はじめに

まず、公式サイトから Aspose.Cells for Java ライブラリをダウンロードします。

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

JAR をプロジェクトのクラスパスに追加したら、チャートの作成を開始できます。

### 手順 1: aspose.cells クラスをインポート
`Workbook` は、メモリ内の Excel ファイル全体を表す Aspose.Cells のコアオブジェクトです。  
```java
import com.aspose.cells.*;
```

### 手順 2: 新しいワークブックを作成
`Worksheet` は `Workbook` 内の単一シートを表し、セル、行、チャートへのアクセスを提供します。  
```java
Workbook workbook = new Workbook();
```

### 手順 3: 最初のワークシートにアクセス
`Chart` は、チャートに関するすべての設定、系列、レンダリングオプションを保持するオブジェクトです。  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### 手順 4: ワークシートに結合チャートオブジェクトを追加  
まず折れ線チャートを作成し、後で縦棒系列を追加して **結合折れ線・縦棒チャート** の効果を実現します。  
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## チャートへのデータ追加

チャートコンテナが作成されたので、データを供給する必要があります。

### 手順 5: データ範囲を定義し、データ系列を追加
`NSeries` はチャートの各データ系列を格納するコレクションです。系列を追加すると、セル範囲がチャートにリンクされます。  
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **プロのコツ:** 最初のパラメータ (`"A1:A5"`) は最初の系列の範囲で、2 番目のパラメータ (`"B1:B5"`) は最初の系列と結合される第2系列を作成します。

### 手順 6: カテゴリ (X 軸) データを設定
`CategoryAxis` はチャートの水平軸を表し、X 軸に表示されるラベルを制御します。  
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## チャートのカスタマイズ

優れたチャートはストーリーを伝えます。タイトル、軸ラベル、明確な凡例を付けましょう。

### 手順 7: チャートの軸ラベルとタイトルを設定
`Title` はチャートのメインタイトルを設定し、`Axis` オブジェクトは X 軸と Y 軸を表します。  
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### 手順 8: 凡例を追加し、その位置を調整
`Legend` はチャート内の系列凡例の配置と外観を制御します。  
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## チャートの保存とエクスポート

カスタマイズ後は、**ワークブックを XLSX として保存**し、画像も生成したいでしょう。

### 手順 9: ワークブックを Excel ファイル (XLSX) として保存
`Workbook.save` はメモリ内のワークブックを指定された形式のファイルに書き込みます。  
```java
workbook.save("CombinedChart.xlsx");
```

### 手順 10: チャートを PNG にエクスポート
`Chart.toImage` は選択した形式でチャートを画像ファイルとしてレンダリングします。  
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> `chart.toImage` メソッドは **Excel チャート** 画像を生成し、ウェブページ、レポート、メールで使用できます。

## よくある問題とトラブルシューティング

| 問題 | 解決策 |
|-------|----------|
| **データが表示されません** | セル範囲 (`A1:A5`, `B1:B5`, `C1:C5`) に実際にデータが含まれているか、チャート作成前に確認してください。 |
| **凡例がチャートと重なる** | `chart.getLegend().setOverlay(false)` を設定するか、凡例を別の位置（例: `RIGHT`）に移動します。 |
| **画像ファイルが空白** | チャートに少なくとも1つの系列があり、すべてのカスタマイズ後に `chart.toImage` が呼び出されていることを確認してください。 |
| **保存時に例外が発生** | 対象ディレクトリへの書き込み権限があるか、ファイルが Excel で開かれていないかを確認してください。 |

## よくある質問

**Q: Aspose.Cells for Java のインストール方法は？**  
A: 公式サイトから JAR をダウンロードし、プロジェクトのクラスパスに追加します。ダウンロードリンク: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: 折れ線と縦棒以外のチャートタイプも作成できますか？**  
A: はい、Aspose.Cells は棒グラフ、円グラフ、散布図、エリアチャートなど多数のチャートタイプをサポートしています。完全な一覧は API ドキュメントをご参照ください。

**Q: 本番環境でライセンスは必要ですか？**  
A: 本番展開には有効な Aspose.Cells ライセンスが必要です。評価用に無料トライアルが利用可能です。

**Q: 各系列の色を変更するには？**  
A: 系列を追加した後、`chart.getNSeries().get(i).setAreaColor(Color.getRed())`（または類似のメソッド）を使用します。

**Q: さらにコード例はどこで見つかりますか？**  
A: 詳細なドキュメントと追加サンプルは Aspose 参照サイトで入手できます: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).

---

**最終更新日:** 2026-09-02  
**テスト環境:** Aspose.Cells for Java 最新バージョン  
**作者:** Aspose

## 関連チュートリアル

- [Aspose.Cells for Java を使用して Excel チャートにラベルを追加する方法](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)
- [Aspose.Cells for Java を使用してトレンドライン付き Excel チャートを作成し画像にエクスポートする方法](/cells/java/advanced-excel-charts/trendline-analysis/)
- [Aspose.Cells for Java を使用して Excel チャートを PDF にエクスポート: カスタムページサイズガイド](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}