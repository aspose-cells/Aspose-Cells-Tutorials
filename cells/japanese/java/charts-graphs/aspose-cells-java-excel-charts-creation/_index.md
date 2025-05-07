---
"date": "2025-04-07"
"description": "Aspose.Cells for Javaを使用してExcelでグラフを作成およびカスタマイズする方法を学びましょう。この詳細なガイドで、グラフ作成を自動化し、データの視覚化を強化し、時間を節約しましょう。"
"title": "Aspose.Cells Java を使用した Excel グラフの作成とスタイル設定の総合ガイド"
"url": "/ja/java/charts-graphs/aspose-cells-java-excel-charts-creation/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Aspose.Cells Java を使用した Excel グラフの作成とスタイル設定

## 導入

今日のデータドリブンな世界では、効果的な情報視覚化が分析と意思決定に不可欠です。特に大規模なデータセットや自動レポートシステムを扱う場合、Excelブックで動的なグラフをプログラム的に作成する必要が生じることがよくあります。このチュートリアルでは、Aspose.Cells for Javaを使用してExcelでグラフをシームレスに作成およびカスタマイズする方法を説明します。Aspose.CellsをJavaアプリケーションに統合することで、グラフ作成の自動化、データのプレゼンテーションの強化、そして時間の節約が可能になります。

**学習内容:**
- Aspose.Cells を使用してワークブックを初期化し、データを入力します。
- データ マーカーを使用して折れ線グラフを作成および構成します。
- シリーズの外観と色をカスタマイズして、視覚化を向上させます。
- 新しく作成されたグラフを含むワークブックを Excel 形式で保存します。

まず、始めるために必要な前提条件について説明しましょう。

## 前提条件

Aspose.Cells for Java を使用してグラフを作成し、スタイル設定する前に、次の設定が行われていることを確認してください。

### 必要なライブラリ
Aspose.Cellsをプロジェクトの依存関係として含めます。MavenとGradleの両方のユーザー向けの手順は次のとおりです。

**メイヴン:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**グレード:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### 環境設定要件
- Java Development Kit (JDK) がシステムにインストールされています。
- コーディングとテスト用の IntelliJ IDEA や Eclipse などの統合開発環境 (IDE)。

### 知識の前提条件
Java プログラミングの基本的な理解に加え、Excel ワークブックとグラフ作成の概念に関する知識も必要です。 

### ライセンス取得
Aspose.Cells は、全機能を使用するにはライセンスが必要となる商用製品です。無料トライアル版で機能を評価したり、長期テスト用の一時ライセンスをリクエストしたり、製品をご購入いただくことで、長期間のご利用が可能です。

- **無料トライアル:** [無料トライアルをダウンロード](https://releases.aspose.com/cells/java/)
- **一時ライセンス:** [一時ライセンスの申請](https://purchase.aspose.com/temporary-license/)
- **購入：** [Aspose.Cellsを購入する](https://purchase.aspose.com/buy)

## Aspose.Cells for Java のセットアップ

必要な依存関係をインストールしたら、Aspose.Cells を使用する開発環境をセットアップします。まず、ライブラリをインポートし、Java アプリケーションで Workbook オブジェクトを初期化します。

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // 新しいワークブックインスタンスを初期化する
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## 実装ガイド

このセクションでは、実装を、ワークブックの初期化とデータの入力、グラフの作成と構成、シリーズのカスタマイズ、ワークブックの保存という個別の機能に分けます。

### 機能1: ワークブックの初期化とデータの入力

**概要：** この機能は、新しいワークブックを作成し、その最初のワークシートにアクセスし、グラフ作成用のデータを入力することに重点を置いています。

#### ステップ1: ワークブックを初期化する
まずインスタンス化して `Workbook` 物体：

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // ワークブックをインスタンス化する
        Workbook workbook = new Workbook();
        
        // 最初のワークシートにアクセスする
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### ステップ2: 列タイトルを設定し、データを入力する
列ヘッダーを定義し、行にサンプル データを入力します。

```java
        // 列のタイトルを設定する 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // シリーズ1のランダムデータを作成する
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // シリーズ2のランダムデータを作成する
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### 機能2: チャートの作成と設定

**概要：** この機能は、ワークブックのワークシートにグラフを追加し、そのスタイルを設定し、基本的なプロパティを構成する方法を示します。

#### ステップ3: ワークシートにグラフを追加する
データ マーカー付きの折れ線グラフを追加します。

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // ワークブックをインスタンス化する
        Workbook workbook = new Workbook();
        
        // 最初のワークシートにアクセスする
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // ワークシートにグラフを追加する
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // チャートにアクセスして設定する
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // 定義済みのスタイルを設定する
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### 機能3：シリーズ構成とカスタマイズ

**概要：** さまざまな色やマーカー スタイルなどのシリーズ設定をカスタマイズして、グラフの視覚的な魅力を高めます。

#### ステップ4: シリーズ設定をカスタマイズする
系列データを構成し、カスタム書式を適用し、マーカーを調整します。

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // ワークブックをインスタンス化する
        Workbook workbook = new Workbook();
        
        // 最初のワークシートにアクセスする
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // グラフにシリーズを追加する
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // シリーズポイントにさまざまな色を有効にする
        chart.getNSeries().setColorVaried(true);

        // 最初のシリーズのマーカーのスタイルと色をカスタマイズする
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // 最初のシリーズのXとYの値を設定する
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // 第 2 シリーズのマーカーのスタイルと色をカスタマイズする
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // 2番目のシリーズのXとYの値を設定する
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### 機能4: ワークブックの保存

**概要：** 最後に、ワークブックを保存して変更を保持し、グラフが Excel ファイルに含まれていることを確認します。

#### ステップ5: ワークブックを保存する
新しく作成されたグラフを含むワークブックを保存します。

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // ワークブックをインスタンス化する
        Workbook workbook = new Workbook();
        
        // 最初のワークシートにアクセスし、前の手順に従ってデータとグラフの構成を追加します...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // （データの追加とチャートの設定の実装はここで行います）

        // ワークブックをExcelファイルに保存する
        workbook.save("StyledChart.xlsx");
    }
}
```

**キーワードの推奨事項:**
- 「Aspose.Cells for Java」
- 「Java による Excel グラフ作成」
- 「Excel自動化のためのJavaプログラミング」

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}