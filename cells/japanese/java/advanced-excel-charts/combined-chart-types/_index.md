---
date: 2025-12-06
description: Aspose.Cells for Java を使用して、データ系列の追加、複合チャートタイプの作成、Excel ワークブックの保存、チャートの
  PNG へのエクスポート方法を学びましょう。
language: ja
linktitle: Add data series to create combined chart using Aspose.Cells
second_title: Aspose.Cells Java Excel Processing API
title: Aspose.Cells を使用して複合チャートを作成するためにデータ系列を追加する
url: /java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells を使用して結合チャートを作成するためにデータ系列を追加する

このチュートリアルでは、Excel ワークブックに **データ系列を追加** し、Aspose.Cells for Java を使用して **結合チャート** タイプを作成する方法を学びます。ワークブックの設定、系列の追加、凡例のカスタマイズ、**Excel ワークブックを保存** して **チャートを PNG にエクスポート** するまでのすべての手順を順に解説します。最後まで実施すれば、レポートやダッシュボードに埋め込める、すぐに使用できる結合チャートが完成します。

## クイック回答
- **どのライブラリが結合チャートを作成しますか？** Aspose.Cells for Java  
- **データ系列はどうやって追加しますか？** `chart.getNSeries().add(...)` を使用  
- **チャートを画像としてエクスポートできますか？** はい、`chart.toImage(...)` (PNG) で可能  
- **ワークブックはどのファイル形式で保存できますか？** 標準の `.xlsx` (Excel)  
- **本番環境でライセンスは必要ですか？** 有効な Aspose.Cells ライセンスが必要です  

## Aspose.Cells の **add data series** とは？
データ系列を追加すると、チャートがプロットすべきセル範囲を認識します。各系列は折れ線、棒、その他任意のチャートタイプを表すことができ、これらを組み合わせて **結合チャート** を構築できます。

## **combined chart** を作成する理由
結合チャートを使用すると、異なるデータセットを別々のビジュアル表現（例：棒グラフ上に折れ線を重ねる）で同一画面に表示できます。トレンドと総計の比較、相関関係の強調、またはコンパクトな形式での豊富なインサイト提供に最適です。

## 前提条件
- Java Development Kit (JDK) 8 以上  
- Aspose.Cells for Java ライブラリ（下記リンクからダウンロード）  
- Java の基本構文と Excel の概念に関する基礎知識  

## はじめに

まず、公式サイトから Aspose.Cells for Java ライブラリをダウンロードしてください。

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

### 手順 4: 結合チャートオブジェクトを追加  
最初に折れ線チャートを作成し、後で他の系列を追加して **結合チャート** の効果を実現します。
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## チャートへのデータ追加

チャートコンテナが作成されたので、データを供給します。

### 手順 5: データ範囲を定義し **データ系列を追加**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **プロのコツ:** 最初のパラメータ (`"A1:A5"`) は最初の系列の範囲を示し、2 番目のパラメータ (`"B1:B5"`) は最初の系列と組み合わせて表示される第 2 系列を作成します。

### 手順 6: カテゴリ (X 軸) データを設定
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## チャートのカスタマイズ

良いチャートはストーリーを語ります。タイトル、軸ラベル、明確な凡例を付けましょう。

### 手順 7: チャートタイトルと軸ラベルを設定
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### 手順 8: **凡例を追加** し位置を調整
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## チャートの保存とエクスポート

カスタマイズが完了したら、**Excel ワークブックを保存** し、画像も生成します。

### 手順 9: ワークブックを Excel ファイルとして保存
```java
workbook.save("CombinedChart.xlsx");
```

### 手順 10: **チャートを PNG にエクスポート**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> `chart.toImage` メソッドは **Excel チャート画像** を生成し、Web ページ、レポート、メールなどで使用できます。

## よくある問題とトラブルシューティング

| 問題 | 解決策 |
|-------|----------|
| **データが表示されない** | チャート作成前にセル範囲 (`A1:A5`, `B1:B5`, `C1:C5`) に実際にデータが入っているか確認してください。 |
| **凡例がチャートと重なる** | `chart.getLegend().setOverlay(false)` を設定するか、凡例を別の位置（例: `RIGHT`）に移動してください。 |
| **画像ファイルが空白になる** | 少なくとも 1 つの系列が存在し、すべてのカスタマイズ後に `chart.toImage` が呼び出されていることを確認してください。 |
| **保存時に例外がスローされる** | 保存先ディレクトリへの書き込み権限があるか、ファイルが Excel で開かれていないかを確認してください。 |

## FAQ（よくある質問）

**Q: Aspose.Cells for Java のインストール方法は？**  
A: 公式サイトから JAR をダウンロードし、プロジェクトのクラスパスに追加します。ダウンロードリンクは: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)。

**Q: 折れ線や棒グラフ以外のチャートタイプも作成できますか？**  
A: はい、Aspose.Cells はバー、円、散布図、エリアなど多数のチャートタイプをサポートしています。詳細は API ドキュメントをご参照ください。

**Q: 本番環境でライセンスは必須ですか？**  
A: はい、製品を本番環境で使用する場合は有効な Aspose.Cells ライセンスが必要です。評価用の無料トライアルも提供されています。

**Q: 各系列の色を変更するには？**  
A: 系列を追加した後に `chart.getNSeries().get(i).setAreaColor(Color.getRed())` などを使用して色を設定できます。

**Q: もっとコード例はどこで見られますか？**  
A: 詳細なドキュメントと追加サンプルは Aspose 参照サイトで入手可能です: [here](https://reference.aspose.com/cells/java/)。

---

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

**最終更新日:** 2025-12-06  
**テスト環境:** Aspose.Cells for Java 24.12  
**作者:** Aspose  

---