---
date: 2026-02-14
description: Aspose.Cells for Java を使用して、チャートを PNG にエクスポートする方法、データ系列を追加する方法、折れ線と棒グラフを組み合わせる方法、ワークブックを
  XLSX として保存する方法、そして凡例チャートを追加する方法を学びます。
linktitle: Export chart to PNG and add data series for combined chart
second_title: Aspose.Cells Java Excel Processing API
title: チャートをPNGにエクスポートし、結合チャート用にデータ系列を追加
url: /ja/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 複合チャート用にデータ系列を追加してチャートをPNGにエクスポート

このチュートリアルでは、Excelブックに**データ系列を追加**し、**折れ線グラフと縦棒グラフを組み合わせたチャート**を作成し、Aspose.Cells for Java を使用して**チャートをPNGにエクスポート**する方法を学びます。ワークブックの設定、ワークシートへのチャート追加、凡例のカスタマイズ、**ワークブックをxlsxとして保存**しチャートのPNG画像を生成するまで、すべての手順を順に説明します。最後には、レポートやダッシュボードに埋め込める、すぐに使用できる複合チャートが完成します。

## クイック回答
- **どのライブラリが複合チャートを作成しますか？** Aspose.Cells for Java  
- **データ系列はどうやって追加しますか？** Use `chart.getNSeries().add(...)`  
- **チャートをpngにエクスポートするにはどうすればよいですか？** Call `chart.toImage("file.png", ImageFormat.getPng())`  
- **ワークブックはどのファイル形式で保存できますか？** Standard `.xlsx` (save workbook as xlsx)  
- **本番環境でライセンスは必要ですか？** A valid Aspose.Cells license is required  

## Aspose.Cells における **export chart to PNG** とは何ですか？

チャートをPNGにエクスポートすると、Excel のチャートのラスタ画像が作成され、Web ページやレポート、メールなどで Excel アプリケーションを必要とせずに表示できます。

## なぜ **combined line column chart** を作成するのですか？

複合チャートを使用すると、異なるデータセットをそれぞれ異なる視覚表現（例：縦棒系列に対して折れ線系列）で単一のビューに表示できます。これは、合計に対するトレンドの比較、相関関係のハイライト、またはコンパクトな形式でより豊かな洞察を提供するのに最適です。

## 前提条件
- Java Development Kit (JDK) 8 以上  
- Aspose.Cells for Java ライブラリ（以下のリンクからダウンロード）  
- Java の構文と Excel の概念に関する基本的な知識  

## はじめに

まず、公式サイトから Aspose.Cells for Java ライブラリをダウンロードします。

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

JAR をプロジェクトのクラスパスに追加したら、チャートの作成を開始できます。

### 手順 1: Aspose.Cells クラスをインポート
```java
import com.aspose.cells.*;
```

### 手順 2: 新しいワークブックを作成
```java
Workbook workbook = new Workbook();
```

### 手順 3: 最初のワークシートにアクセス
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### 手順 4: ワークシートに複合チャートオブジェクトを追加  
まず折れ線チャートから始め、後で縦棒系列を追加して **combined line column chart** の効果を実現します。
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## チャートへのデータ追加

チャートコンテナが作成されたので、データを供給する必要があります。

### 手順 5: データ範囲を定義し、**データ系列を追加**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **プロのコツ:** 最初のパラメータ (`"A1:A5"`) は最初の系列の範囲で、2 番目のパラメータ (`"B1:B5"`) は最初の系列と組み合わせる第2 系列を作成します。

### 手順 6: カテゴリ (X 軸) データを設定
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## チャートのカスタマイズ

優れたチャートはストーリーを伝えます。タイトル、軸ラベル、わかりやすい凡例を設定しましょう。

### 手順 7: **チャート軸ラベル** とタイトルを設定
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### 手順 8: **凡例を追加** し、位置を調整
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## チャートの保存とエクスポート

カスタマイズが完了したら、**ワークブックをxlsxとして保存**し、画像も生成したいでしょう。

### 手順 9: ワークブックを Excel ファイル (xlsx) として保存
```java
workbook.save("CombinedChart.xlsx");
```

### 手順 10: **チャートを PNG にエクスポート**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> `chart.toImage` メソッドは **Excel チャート** の画像を生成し、Web ページ、レポート、メールで使用できます。

## よくある問題とトラブルシューティング

| Issue | Solution |
|-------|----------|
| **データが表示されません** | チャート作成前にセル範囲 (`A1:A5`, `B1:B5`, `C1:C5`) に実際にデータが入っていることを確認してください。 |
| **凡例がチャートと重なる** | `chart.getLegend().setOverlay(false)` を設定するか、凡例を別の位置（例：`RIGHT`）に移動してください。 |
| **画像ファイルが空白** | チャートに少なくとも1つの系列があり、すべてのカスタマイズ後に `chart.toImage` が呼び出されていることを確認してください。 |
| **保存時に例外がスローされる** | 対象ディレクトリへの書き込み権限があるか、ファイルが Excel で開かれていないかを確認してください。 |

## よくある質問

**Q: Aspose.Cells for Java のインストール方法は？**  
A: 公式サイトから JAR をダウンロードし、プロジェクトのクラスパスに追加してください。ダウンロードリンク: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

**Q: 折れ線と縦棒以外のチャートタイプも作成できますか？**  
A: はい、Aspose.Cells は棒グラフ、円グラフ、散布図、エリアチャートなど多数のチャートタイプをサポートしています。全リストは API ドキュメントをご参照ください。

**Q: 本番環境での使用にライセンスは必要ですか？**  
A: 本番環境での導入には有効な Aspose.Cells ライセンスが必要です。評価用の無料トライアルも利用可能です。

**Q: 各系列の色を変更するには？**  
A: 系列を追加した後、`chart.getNSeries().get(i).setAreaColor(Color.getRed())`（または類似のメソッド）を使用してください。

**Q: さらにコード例はどこで見つけられますか？**  
A: 詳細なドキュメントと追加サンプルは Aspose のリファレンスサイトで入手できます: [here](https://reference.aspose.com/cells/java/).

---

**最終更新日:** 2026-02-14  
**テスト環境:** Aspose.Cells for Java 最新バージョン  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}