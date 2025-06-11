---
"date": "2025-04-08"
"description": "Aspose.Cells for Javaを使って円グラフを作成、カスタマイズする方法を学びましょう。開発者向けのコード例を交えたステップバイステップガイドです。"
"title": "Aspose.Cells をマスターして Java で円グラフを作成およびカスタマイズする"
"url": "/ja/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Aspose.Cells をマスターする: Java で円グラフを作成およびカスタマイズする

## 導入
Excelでデータビジュアライゼーションを行う際、視覚的に魅力的なグラフを作成することはよくある要件です。人口統計情報を提示する場合でも、市場動向を分析する場合でも、円グラフは割合データを明確に表現する手段となります。しかし、円グラフをプログラムで設定するのは複雑になる場合があります。このチュートリアルでは、Javaを使用してAspose.Cellsの円グラフを作成およびカスタマイズする方法を解説し、開発者のプロセスを簡素化します。

**学習内容:**
- Aspose.Cells for Java を使用して環境を設定します。
- 新しいワークブックを作成し、ワークシートのセルにアクセスします。
- グラフ作成の準備として、特定のセルにデータを入力します。
- このデータから円グラフを生成します。
- 色、タイトル、凡例など、円グラフの外観をカスタマイズします。

始める前に、JavaプログラミングとMavenまたはGradleの依存関係管理について基本的な知識を身に付けておきましょう。それでは環境を構築しましょう！

## 前提条件
このチュートリアルを実行するには、次のものが必要です。
- **Java開発キット（JDK）**: バージョン 8 以上。
- **統合開発環境（IDE）**: IntelliJ IDEA や Eclipse など。
- **依存関係管理**依存関係を管理するには、Maven または Gradle を使用します。

### 必要なライブラリと依存関係
Maven または Gradle を使用して、プロジェクトに Aspose.Cells for Java を必ず含めてください。

**メイヴン**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**グラドル**
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### ライセンス取得手順
Aspose.Cells for Javaは商用ライブラリですが、無料トライアルから始めることも、一時ライセンスを申請することもできます。 [購入ページ](https://purchase.aspose.com/buy) ライセンス オプションを検討します。

## Aspose.Cells for Java のセットアップ
まず、上記のようにMavenまたはGradleを使って必要なライブラリを追加し、プロジェクト環境に必要なライブラリが含まれていることを確認します。ライブラリが追加されたら、Aspose.Cellsを初期化できます。

```java
import com.aspose.cells.Workbook;

// 新しいワークブックインスタンスを初期化する
Workbook workbook = new Workbook();
```

## 実装ガイド

### ワークブックの作成と構成
ワークブックの作成は、データを設定する最初のステップです。

#### ライブラリのインポート
次のインポートがファイルの先頭に含まれていることを確認します。

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

#### ステップ1: ワークブックインスタンスを作成する
```java
// 作業する空のワークブック インスタンスを作成します。
Workbook workbook = new Workbook();
```
この手順では、Excel ファイルをプログラムで初期化し、Aspose.Cells 機能を使用して操作できるようになります。

### ワークシートのセルにアクセスまたは変更する
次に、円グラフに使用するワークシートのセルにデータを入力します。

#### ステップ2: ワークシートとそのセルにアクセスする
```java
// ワークブックの最初のワークシートにアクセスします。
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// 円グラフに使用するサンプル値を特定のセルに入力します。
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// 円グラフのパーセンテージ値を特定のセルに入力します。
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```
ここでは、円グラフのさまざまなセグメントを表すデータをワークシートに入力します。

### 円グラフを作成する

#### ステップ3: ワークシートに円グラフを追加する
```java
// ワークシートに円グラフを作成します。
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```
この手順では、指定された位置と寸法で新しい円グラフをワークシートに追加します。

### 円グラフのシリーズとデータを設定する

#### ステップ4: グラフの系列を設定する
```java
// グラフの系列データ範囲を設定します。
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// 円グラフのタイトルを、タイトル テキストを含むセルにリンクします。
pie.getTitle().setLinkedSource("D2");
```
このコードはデータ範囲をリンクし、円グラフの系列を設定します。

### グラフの凡例とタイトルの外観を構成する

#### ステップ5: グラフの凡例とタイトルをカスタマイズする
```java
// 凡例の位置をグラフの下部に設定します。
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// グラフのタイトルのフォントプロパティを設定します。
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```
外観をカスタマイズすると、読みやすさと視覚的な魅力が向上します。

### グラフシリーズの色をカスタマイズする

#### ステップ6: 円グラフのセグメントの色を変更する
```java
import com.aspose.cells.Color;

// 個々の円グラフセグメントの色にアクセスしてカスタマイズします。
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```
これらの設定により、特定の配色に合わせてグラフをカスタマイズできます。

### 列の自動調整とワークブックの保存

#### ステップ7: 列幅を調整してファイルを保存する
```java
// すべての列を自動調整します。
worksheet.autoFitColumns();

// ワークブックを保存するための出力ディレクトリのプレースホルダー パスを定義します。
String outDir = "YOUR_OUTPUT_DIRECTORY";

// 変更したブックを指定されたディレクトリ内の Excel ファイルに保存します。
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```
最後に、列を自動調整してワークブックを保存します。

## 実用的なアプリケーション
1. **人口統計分析**さまざまな国や地域の人口分布を表示するには、円グラフを使用します。
2. **市場シェアレポート**業界内のさまざまな企業の市場シェアを示します。
3. **予算配分**組織内のさまざまな部門に予算がどのように割り当てられているかを視覚化します。

これらのアプリケーションは、実際のシナリオにおける Aspose.Cells の汎用性と有用性を実証します。

## パフォーマンスに関する考慮事項
Aspose.Cells を使用する際のパフォーマンスを最適化するには:
- 不要になったオブジェクトを破棄してメモリ使用量を最小限に抑えます。
- 大規模なデータセットを処理するには、効率的なデータ構造を使用します。
- アプリケーションをプロファイルしてボトルネックを特定します。

ベスト プラクティスに従うことで、スムーズで応答性の高いアプリケーションが保証されます。

## 結論
このチュートリアルでは、JavaでAspose.Cellsを使用して円グラフを作成およびカスタマイズする手順を詳しく説明しました。このチュートリアルで学んだ知識があれば、プロジェクトの様々なデータ視覚化タスクにこれらのテクニックを適用できるようになります。さらに詳しく知りたい場合は、Aspose.Cellsで利用できる他のグラフの種類や高度なカスタマイズオプションについても調べてみてください。


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}