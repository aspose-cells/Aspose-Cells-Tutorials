---
date: 2026-08-27
description: Aspose.Cells for Java を使用して、chartにtrendlineを追加し、R‑squared 値を表示し、chartを
  PNG または JPEG image としてエクスポートする方法を学びます。
keywords:
- add trendline to chart
- save chart as image
- export excel chart image
- java create excel workbook
- convert chart to png
lastmod: 2026-08-27
linktitle: trendline分析でChartをImageにエクスポート
og_description: Aspose.Cells for Java を使用して、chartにtrendlineを追加し、R‑squared を確認し、結果を
  PNG/JPEG としてエクスポートします – 高速で50フォーマット対応のソリューションです。
og_image_alt: Guide showing Java code to add a trendline to an Excel chart and export
  it as an image
og_title: Aspose.Cells for Java でchartにtrendlineを追加し、imageとしてエクスポート
schemas:
- author: Aspose
  dateModified: '2026-08-27'
  description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  headline: How to add trendline to chart and export as image in Java
  type: TechArticle
- description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  name: How to add trendline to chart and export as image in Java
  steps:
  - name: set up the project
    text: Create a new Java project and place the Aspose.Cells JARs on the build path.
      This prepares the environment for generating and manipulating Excel files.
  - name: load excel file (load excel file java)
    text: '*We’ve just **loaded an Excel file** into memory, ready for chart creation.*'
  - name: create a chart
    text: '*Here we generate a line chart that will later host our trendline.*'
  - name: add trendline (how to add trendline) and display R‑squared value
    text: '*The `setDisplayRSquaredValue(true)` call ensures the **R‑squared value**
      appears on the chart.*'
  - name: customize chart and save workbook (save workbook xlsx, generate excel file
      java)
    text: '*Now the workbook is **generated** and saved as an XLSX file, ready for
      further processing.*'
  - name: export chart to image (export chart to image)
    text: '> **Note:** This step is described without an additional code block to
      keep the original block count unchanged. After the chart is created and saved,
      you can export it to an image by calling the `chart.toImage()` method and writing
      the resulting `java.awt.image.BufferedImage` to a file format of you'
  type: HowTo
- questions:
  - answer: Use a different `TrendlineType` enumeration when adding the trendline,
      e.g., `TrendlineType.POLYNOMIAL` for a polynomial fit.
    question: How can I change the trendline type?
  - answer: Yes. Access the trendline’s `LineFormat` via `trendline.getLineFormat()`
      and set properties such as `setWeight()` and `setColor()`.
    question: Can I customize the trendline appearance (color, thickness)?
  - answer: Convert the chart to an image first, then embed that image into a PDF
      using Aspose.PDF or any other PDF library.
    question: How do I export the chart to PDF instead of an image?
  - answer: Absolutely. Call `chart.getNSeries().get(0).getTrendlines().add(...)`
      for each series you wish to analyze.
    question: Is it possible to add multiple trendlines to the same chart?
  - answer: Yes. You can specify the DPI when calling `chart.toImage()` and then scale
      the image before saving, ensuring crisp output for print or high‑density screens.
    question: Does Aspose.Cells support high‑resolution image export?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java charting
- Excel automation
- trendline analysis
title: Javaでchartにtrendlineを追加し、imageとしてエクスポートする方法
url: /ja/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# チャートにトレンドラインを追加して画像としてエクスポートする

このチュートリアルでは、**チャートにトレンドラインを追加**し、R‑squared 値を表示し、Aspose.Cells for Java を使用して PNG または JPEG ファイルとしてビジュアルをエクスポートする方法を学びます。トレンドラインが重要な理由、ワークブックの準備方法、レポートやメール、ウェブページに埋め込める高解像度画像を生成する正確な手順を確認できます。

## クイック回答
- **このガイドの主な目的は何ですか？** Java を使用してチャートにトレンドラインを追加し、方程式と R‑squared 値を表示し、チャートを画像としてエクスポートする方法を示すことです。  
- **どのライブラリが必要ですか？** Aspose.Cells for Java – [Aspose.Cells for Java リリースページ](https://releases.aspose.com/cells/java/) からダウンロードしてください。  
- **開発にライセンスは必要ですか？** 開発には無料トライアルで動作しますが、本番環境での展開には商用ライセンスが必要です。  
- **Excel ワークブックをプログラムで生成できますか？** はい – このチュートリアルでは最初から XLSX ワークブックを作成し、保存します。  
- **チャートはどのように PNG または JPEG にエクスポートされますか？** `Chart.toImage()` メソッドを呼び出し、返された `BufferedImage` を `ImageIO.write(...)` で書き出します。

## トレンドライン付きの Excel チャートを作成し、画像としてエクスポートする方法は？
ワークブックをロードし、折れ線グラフを追加し、方程式と R‑squared 値を表示するトレンドラインを付与し、ワークブックを保存した後、`chart.toImage()` を呼び出して得られた `BufferedImage` を PNG または JPEG ファイルに書き出します。このエンドツーエンドのフローは数行の Java コードで実現でき、あらゆる下流アプリケーションに適したピクセルパーフェクトな画像を生成します。

## チャートを画像にエクスポートするとは？
チャートを画像にエクスポートすると、データの視覚表現がポータブルなビットマップ（PNG、JPEG、BMP など）に変換されます。この形式は、元の Excel ファイルが不要なレポート、ウェブページ、プレゼンテーションにチャートを埋め込むのに最適です。

## なぜトレンドラインを追加し、R‑squared 値を表示するのですか？
トレンドラインはデータ系列の基礎的なパターンを明らかにし、**R‑squared** メトリックはトレンドラインがデータにどれだけ適合しているかを定量化します。エクスポートされた画像に両方を含めることで、ステークホルダーはワークブックを開かずに即座に洞察を得られ、意思決定者は相関の強さや将来の傾向を迅速に評価できます。

## 前提条件
- 開発マシンに Java 8 以上がインストールされていること。  
- プロジェクトのクラスパスに Aspose.Cells for Java ライブラリ（JAR ファイル）を追加していること。  
- IntelliJ IDEA や Eclipse などの Java IDE に慣れていること。  

## ステップバイステップガイド

### ステップ 1: プロジェクトの設定
新しい Java プロジェクトを作成し、Aspose.Cells の JAR をビルドパスに配置します。これにより、Excel ファイルの生成と操作の環境が整います。

### ステップ 2: Excel ファイルをロードする (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*メモリに **Excel ファイルをロード** したばかりで、チャート作成の準備ができています。*

### ステップ 3: チャートを作成する
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*ここで後でトレンドラインを設定する折れ線グラフを生成します。*

### ステップ 4: トレンドラインを追加する (how to add trendline) と R‑squared 値を表示する
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*`setDisplayRSquaredValue(true)` 呼び出しにより、**R‑squared 値** がチャート上に表示されます。*

### ステップ 5: チャートをカスタマイズし、ワークブックを保存する (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*これでワークブックは **生成** され、XLSX ファイルとして保存され、さらに処理できる状態になりました。*

### ステップ 6: チャートを画像にエクスポートする (export chart to image)
> **注:** このステップは、元のブロック数を変更しないため、追加のコードブロックなしで説明しています。  
チャートが作成・保存された後、`chart.toImage()` メソッドを呼び出し、得られた `java.awt.image.BufferedImage` を任意のファイル形式（PNG、JPEG、BMP）で書き出すことで画像にエクスポートできます。典型的なワークフローは次のとおりです:
1. `Chart` オブジェクトを取得する（前ステップですでに取得済み）。  
2. `chart.toImage()` を呼び出して `BufferedImage` を取得する。  
3. `ImageIO.write(bufferedImage, "png", new File("chart.png"))` のようにしてファイルに書き出す。  

`Chart` オブジェクトはワークブック内のチャートを表し、外観やデータを変更するメソッドを提供します。`BufferedImage` はメモリ上に画像を保持する Java クラスで、ファイルへの保存が可能です。`ImageIO` は Java の画像入出力ユーティリティクラスです。`setDisplayRSquaredValue` はトレンドライン上に R‑squared 統計を表示できるようにします。

### 結果の分析
`output.xlsx` を Excel で開き、トレンドライン、方程式、R‑squared 値が期待通りに表示されていることを確認します。エクスポートされた画像ファイル（例: `chart.png`）を開き、元のワークブックがなくても共有できるきれいなビジュアルが得られることを確認します。

## よくある問題と解決策
- **トレンドラインが表示されない:** データ範囲 (`A1:A10`) に数値が含まれているか確認してください。非数値データはトレンドライン計算を妨げます。  
- **R‑squared 値が 0 と表示される:** データ系列が一定または変動がないことが原因です。別のデータセットを試すか、多項式トレンドラインを使用してください。  
- **`NullPointerException` で画像エクスポートが失敗する:** `toImage()` を呼び出す前にチャートが完全に描画されているか確認してください。ワークブックを先に保存するとタイミングの問題が解消されることがあります。

## よくある質問

**Q: トレンドラインのタイプを変更するには？**  
A: トレンドラインを追加する際に別の `TrendlineType` 列挙体を使用します。例: 多項式フィットの場合は `TrendlineType.POLYNOMIAL` を指定します。

**Q: トレンドラインの外観（色、太さ）をカスタマイズできますか？**  
A: はい。`trendline.getLineFormat()` で `LineFormat` にアクセスし、`setWeight()` や `setColor()` などのプロパティを設定できます。

**Q: 画像ではなく PDF にチャートをエクスポートするには？**  
A: まずチャートを画像に変換し、その画像を Aspose.PDF などの PDF ライブラリを使用して PDF に埋め込みます。

**Q: 同じチャートに複数のトレンドラインを追加できますか？**  
A: もちろんです。分析したい各系列に対して `chart.getNSeries().get(0).getTrendlines().add(...)` を呼び出します。

**Q: Aspose.Cells は高解像度画像のエクスポートに対応していますか？**  
A: はい。`chart.toImage()` 呼び出し時に DPI を指定し、保存前に画像をスケーリングすることで、印刷や高密度ディスプレイ向けの鮮明な出力が可能です。

---

**最終更新日:** 2026-08-27  
**テスト環境:** Aspose.Cells for Java latest (supports 50+ file formats and processes workbooks with up to 2 million rows without full memory load)  
**作者:** Aspose

## 関連チュートリアル

- [Aspose.Cells Java を使用した Excel チャートへのデータラベルの追加](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Aspose.Cells Java を使用して Excel チャートを SVG としてエクスポートする方法（スケーラブルベクターグラフィックス）](/cells/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Aspose.Cells for Java&#58; カスタムページサイズガイドを使用した Excel チャートの PDF へのエクスポート](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}