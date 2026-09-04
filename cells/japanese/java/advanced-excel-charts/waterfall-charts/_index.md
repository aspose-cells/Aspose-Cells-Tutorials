---
date: 2026-02-16
description: Aspose.Cells を使用して Java でチャートのデータ範囲を設定し、滝図（ウォーターフォールチャート）を作成する方法を学びます。データ系列チャートの追加、カスタマイズ、XLSX
  へのエクスポートまでのステップバイステップガイド。
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: チャート データ範囲の設定 – Aspose.Cells for Java ウォーターフォール チャート
url: /ja/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ウォーターフォールチャート

## Aspose.Cells for Java を使用したウォーターフォールチャートの紹介

このチュートリアルでは、Aspose.Cells for Java を使用して **set chart data range** を設定し、**waterfall chart** を作成する方法を学びます。ウォーターフォールチャートは、正と負の値の系列が累積的に与える影響を視覚化できるため、データ可視化の重要なツールです。財務諸表、販売実績レポート、その他あらゆるデータ駆動型分析を行う際に、ウォーターフォールチャートは生の数値を明確で実行可能なインサイトへと変換します。

## クイック回答
- **ウォーターフォールチャートとは？** 初期値が一連の中間値によって増減され、最終的な合計に至る様子を示すビジュアルです。  
- **使用するライブラリは？** Aspose.Cells for Java。  
- **ライセンスは必要ですか？** 開発目的であれば無料トライアルで動作しますが、本番環境では商用ライセンスが必要です。  
- **ファイルを XLSX として保存できますか？** はい – `workbook.save("FileName.xlsx")` を使用します。  
- **Java のデータ可視化に適していますか？** 完全に適しています。Aspose.Cells は Office をインストールせずに豊富なチャート機能を提供します。

## ウォーターフォールチャートとは？
ウォーターフォールチャートは、開始値に対する順次の正・負の寄与を表示し、各コンポーネントが全体結果に与える影響を理解するのに役立ちます。

## Aspose.Cells for Java でウォーターフォールチャートを追加する理由
- **Microsoft Excel 不要** – 任意のサーバーや CI パイプライン上でチャートを生成できます。  
- **書式設定をフルコントロール** – 色、データ ラベル、軸などをプログラムでカスタマイズ可能です。  
- **複数の出力形式に対応** – XLSX、PDF、HTML など多数。  
- **高性能** – 大規模ブックや自動レポート作成に最適です。

## 前提条件

コードに入る前に、以下の前提条件が整っていることを確認してください。

- Aspose.Cells for Java: Aspose.Cells for Java をインストールしている必要があります。ダウンロードは [here](https://releases.aspose.com/cells/java/) から行えます。

- Java 開発環境: システムに Java がインストールされていることを確認してください。

それでは、ウォーターフォールチャートをステップバイステップで作成していきましょう。

## Java でウォーターフォールチャートのデータ範囲を設定する方法

### 手順 1: Aspose.Cells のインポート

```java
import com.aspose.cells.*;
```

まず、Java プロジェクトに Aspose.Cells ライブラリをインポートします。このライブラリは Excel ファイル操作全般、特にチャート作成に豊富な機能を提供します。

### 手順 2: ワークブックとワークシートの初期化

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

新しいワークブックを作成し、ワークシートを追加します。このワークシートにデータを入力し、**add chart to worksheet** を行います。

### 手順 3: データの入力

次に、ウォーターフォールチャートで表現したいデータをワークシートに入力します。

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

この例では、列 A にカテゴリ、列 B に対応する値を配置しています。ご自身のデータセットに置き換えて構いません。

### 手順 4: ウォーターフォールチャートの作成

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

ワークシートにウォーターフォールチャートを追加し、データ系列とカテゴリ データを指定しました。これが **adds waterfall chart** の核心ステップです。`add` メソッドで範囲 `"B2:B6"` を使用している点に注目してください – ここで **set chart data range** を系列に対して設定しています。`Chart` オブジェクトのプロパティを使って、色やデータ ラベルなどの外観も自由にカスタマイズできます。

### 手順 5: ワークブックの保存

```java
workbook.save("WaterfallChart.xlsx");
```

ワークブックをファイルに保存します。例では XLSX 形式を使用していますが、Aspose.Cells は **export excel pdf java** 互換の PDF、CSV など多数の形式にもエクスポートできます。これにより **save workbook xlsx** の要件を満たします。

## よくある問題と解決策

- **チャートが空白になる** – データ範囲参照（`B2:B6` と `A2:A6`）が実際のセルと一致しているか確認してください。  
- **負の値が正しく表示されない** – 系列のタイプが `ChartType.WATERFALL` に設定されていることを確認してください。他のチャートタイプは負の値を異なる方法で扱います。  
- **Excel でファイルが開かない** – 最新リリースの Aspose.Cells を使用し、ファイル拡張子が形式と一致しているか（`.xlsx` は Excel 用）を確認してください。

## Frequently Asked Questions

### ウォーターフォールチャートの外観はどのようにカスタマイズできますか？

色、データ ラベル、軸ラベルなどのプロパティを変更して外観をカスタマイズできます。詳細は Aspose.Cells のドキュメントをご参照ください。

### 同じワークシートに複数のウォーターフォールチャートを作成できますか？

はい、異なるデータ範囲で同様の手順を繰り返すことで、同一シートに複数のウォーターフォールチャートを作成できます。

### Aspose.Cells はさまざまな Java 開発環境に対応していますか？

はい、Aspose.Cells for Java は Eclipse、IntelliJ IDEA、NetBeans などの主要な Java 開発環境と互換性があります。

### ウォーターフォールチャートに追加のデータ系列を追加できますか？

もちろん可能です。プログラムで **add data series chart** を使用すれば、複数の系列を追加して複雑なデータシナリオを表現できます。

### Aspose.Cells for Java のリソースやサンプルはどこで入手できますか？

詳細情報やコード例は [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) のドキュメントをご覧ください。

## FAQ

**Q: 財務ウォーターフォールチャートのデータ範囲はどう設定しますか？**  
A: チャート系列の `add` メソッドに値が入っているセル範囲（例: `"B2:B6"`）を渡します。

**Q: ワークブックを XLSX ではなく PDF にエクスポートできますか？**  
A: はい、`workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` と呼び出すことで **export excel pdf java** 互換の出力が得られます。

**Q: カテゴリが増える場合はどうすればよいですか？**  
A: 値列とカテゴリ列の両方でデータ範囲を拡張し、`add` と `setCategoryData` の呼び出しをそれに合わせて更新してください。

**Q: 正のバーと負のバーを自動で書式設定する方法はありますか？**  
A: `Series` コレクションを走査し、各値の符号に応じて `FillFormat` の色を設定できます。

**Q: チャートの動的データ更新はサポートされていますか？**  
A: はい、チャート作成後にセルの値を変更すれば、ワークブックを保存した際にチャートが自動的に更新されます。

---

**Last Updated:** 2026-02-16  
**Tested With:** Aspose.Cells for Java (latest)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}