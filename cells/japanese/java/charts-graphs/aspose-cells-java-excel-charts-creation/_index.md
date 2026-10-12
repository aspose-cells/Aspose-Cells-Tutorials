---
date: '2026-04-08'
description: Aspose.Cells for Java を使用してマーカー付き折れ線グラフの作成方法を学び、グラフをワークシートに追加し、Excel
  グラフを自動レポート用にカスタマイズします。
keywords:
- line chart with markers
- add chart to worksheet
- automate excel chart creation
- populate data for chart
- export styled chart excel
title: Aspose.Cells for Java を使用してマーカー付き折れ線グラフを作成する
url: /ja/java/charts-graphs/aspose-cells-java-excel-charts-creation/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells Java を使用した Excel チャートの作成とスタイリング

## はじめに

データ主導の現代において、**マーカー付き折れ線グラフ**はトレンドや外れ値を可視化する最も効果的な手段の一つです。自動レポートや日々更新されるダッシュボードを構築する際に、プログラムでワークシートにマーカー付き折れ線グラフを追加できれば、手作業の工程を大幅に削減できます。本チュートリアルでは、Aspose.Cells for Java を使用してチャートを作成・スタイリング・エクスポートする手順を解説し、面倒な Excel 操作から解放されてインサイトに集中できるようにします。

**学習内容**
- Aspose.Cells を使用してワークブックを初期化し、データを入力する。  
- **ワークシートにマーカー付き折れ線グラフを追加し、その外観を設定する方法**。  
- 系列の色、マーカー、その他のスタイリングオプションをカスタマイズする。  
- スタイル設定されたチャートを含むワークブックを Excel ファイルとして保存する。

## クイック回答
- **開始に使用する主要クラスは何ですか？** `Workbook` は新しい Excel ファイルを初期化します。  
- **データ マーカー付き折れ線グラフを作成するチャートタイプはどれですか？** `ChartType.LINE_WITH_DATA_MARKERS`。  
- **系列ポイントのカスタムカラーを設定するには？** `chart.getNSeries().setColorVaried(true)` を使用し、マーカー領域の色を設定します。  
- **フル機能にライセンスは必要ですか？** はい、有料または一時的な Aspose.Cells ライセンスを使用すると評価制限が解除されます。  
- **結果を XLSX としてエクスポートできますか？** もちろんです—`workbook.save("StyledChart.xlsx")` で XLSX ファイルが作成されます。

## 前提条件

Aspose.Cells for Java を使用してチャートを作成・スタイリングする前に、以下の環境が整っていることを確認してください。

### 必要なライブラリ
プロジェクトに Aspose.Cells を依存関係として追加します。Maven と Gradle の両方の手順を示します。

**Maven:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### 環境設定要件
- システムに Java Development Kit (JDK) がインストールされていること。  
- IntelliJ IDEA や Eclipse などの統合開発環境 (IDE) があること。

### 知識の前提条件
Java プログラミングの基本的な理解と、Excel のブックやチャートの概念に慣れていることが必要です。

### ライセンス取得
Aspose.Cells は商用製品で、フル機能を使用するにはライセンスが必要です。無料トライアルで機能を評価したり、拡張テスト用に一時ライセンスをリクエストしたり、長期利用のために製品を購入したりできます。

- **無料トライアル:** [Download Free Trial](https://releases.aspose.com/cells/java/)  
- **一時ライセンスのリクエスト:** [Request Temporary License](https://purchase.aspose.com/temporary-license/)  
- **購入:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)

## Aspose.Cells for Java の設定

必要な依存関係をインストールしたら、開発環境で Aspose.Cells を使用できるように設定します。まずライブラリをインポートし、Java アプリケーションで `Workbook` オブジェクトを初期化します。

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook instance
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## 実装ガイド

このセクションでは、実装を「ワークブックの初期化とデータの入力」「チャートの作成と設定」「系列のカスタマイズ」「ワークブックの保存」の 4 つの機能に分けて解説します。

### 機能 1: ワークブックの初期化とデータの入力

**概要:** この機能は新しいワークブックを作成し、最初のワークシートにアクセスし、チャート作成用のデータを入力することに焦点を当てています。

#### 手順 1: ワークブックの初期化
まず `Workbook` オブジェクトをインスタンス化します。

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### 手順 2: 列タイトルの設定とデータの入力
列ヘッダーを定義し、サンプルデータで行を埋めます。

```java
        // Set columns title 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Create random data for series 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Create random data for series 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### 機能 2: チャートの作成と設定

**概要:** この機能はワークシートにチャートを追加し、スタイルを設定し、基本的なプロパティを構成する方法を示します。

#### 手順 3: ワークシートにチャートを追加
データ マーカー付きの折れ線グラフを追加します。

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add chart to the worksheet
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Access and configure the chart
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Set a predefined style
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### 機能 3: 系列の設定とカスタマイズ

**概要:** 系列設定（色のバリエーションやマーカー スタイルなど）をカスタマイズして、チャートの視覚的魅力を高めます。

#### 手順 4: 系列設定のカスタマイズ
系列データを設定し、カスタム書式を適用し、マーカーを調整します。

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add series to the chart
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Enable varied colors for series points
        chart.getNSeries().setColorVaried(true);

        // Customize first series marker styles and colors
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the first series
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Customize second series marker styles and colors
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the second series
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### 機能 4: ワークブックの保存

**概要:** 最後にワークブックを保存して変更を永続化し、チャートが Excel ファイルに含まれるようにします。

#### 手順 5: ワークブックの保存
新しく作成したチャートを含むワークブックを保存します。

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet and add data, chart configuration as per previous steps...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Implementation of adding data and configuring the chart would be here)

        // Save the workbook to an Excel file
        workbook.save("StyledChart.xlsx");
    }
}
```

### よくある問題とトラブルシューティング

- **チャートが空白になる:** `setXValues` と `setValues` で使用しているセル範囲が正しくデータを参照しているか確認してください。  
- **色が適用されない:** 個々の系列をカスタマイズする前に `chart.getNSeries().setColorVaried(true)` が呼び出されていることを確認してください。  
- **ライセンスエラー:** 評価版ライセンスはチャート数に制限があります。フルライセンスをインストールして制限を解除してください。

## よくある質問

**Q: Aspose.Cells で他のチャートタイプ（例: 棒グラフ、円グラフ）を作成できますか？**  
A: はい、Aspose.Cells は幅広いチャートタイプをサポートしています。`ChartType.LINE_WITH_DATA_MARKERS` を目的の enum 値に置き換えるだけです。

**Q: ワークブックを閉じたりリソースを解放したりする必要がありますか？**  
A: `Workbook` クラスはリソースを自動的に管理しますが、長時間実行するアプリケーションでは `workbook.dispose()` を呼び出してメモリを解放できます。

**Q: 同じワークシートに複数のチャートを追加できますか？**  
A: もちろんです。挿入したい各チャートに対して `worksheet.getCharts().add(...)` を呼び出します。

**Q: ファイルを古い Excel 形式（XLS）でエクスポートするには？**  
A: `workbook.save("StyledChart.xls", SaveFormat.EXCEL_97_TO_2003);` を使用します。

**Q: Microsoft Excel で開いたときにチャートのスタイルは保持されますか？**  
A: はい、Aspose.Cells はネイティブな Excel チャート オブジェクトを書き込むため、すべてのスタイル、色、マーカーは定義どおりに表示されます。

---

**最終更新日:** 2026-04-08  
**テスト環境:** Aspose.Cells 25.3 for Java  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}