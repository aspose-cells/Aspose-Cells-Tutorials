---
title: 円グラフを作成する
linktitle: 円グラフを作成する
second_title: Aspose.Cells .NET Excel 処理 API
description: このステップバイステップ ガイドでは、Aspose.Cells for .NET を使用して Excel で円グラフを作成する方法を学習します。データを簡単に視覚化できます。
weight: 12
url: /ja/net/manipulating-chart-types/create-pie-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 円グラフを作成する

## 導入

データを視覚的に表現するにはグラフの作成が不可欠です。円グラフは、各部分が全体を構成する様子を示す最も一般的な方法の 1 つです。Aspose.Cells for .NET を使用すると、Excel ファイルでの円グラフの生成を簡単に自動化できます。このチュートリアルでは、Aspose.Cells for .NET を使用して円グラフを最初から作成する方法を詳しく説明します。この手順は、プロセスをスムーズかつ簡単に実行するためのものです。このツールを初めて使用する場合でも、Excel の自動化スキルを強化したい場合でも、このガイドが役立ちます。

## 前提条件

コードに進む前に、次の設定がされていることを確認してください。

1.  Aspose.Cells for .NET ライブラリ: プロジェクトに Aspose.Cells がインストールされていることを確認してください。まだインストールしていない場合は、以下からダウンロードできます。[ここ](https://releases.aspose.com/cells/net/).
2. .NET 開発環境: プロジェクトが .NET Framework または .NET Core を使用するように設定されていることを確認します。
3. C# の基礎知識: C# プログラミング、特にオブジェクト指向プログラミング (OOP) に精通している必要があります。

上級ユーザー向けには、Aspose.Cellsのすべての機能のロックを解除する一時ライセンスを適用できます。こちらからリクエストできます。[ここ](https://purchase.aspose.com/temporary-license/).

## パッケージのインポート

まず、このチュートリアルに必要な名前空間とパッケージをインポートします。これには、基本的な I/O 操作と Aspose.Cells パッケージが含まれます。

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## ステップ1: 新しいワークブックを作成する

まず、インスタンスを作成する必要があります`Workbook`クラスは Excel ファイルを表します。ワークブックには複数のシートが含まれており、この例では、データ用と円グラフ用の 2 つのシートを操作します。

```csharp
Workbook workbook = new Workbook();
```

これにより、新しい Excel ブックが初期化されます。しかし、データはどこに保存されるのでしょうか? 次の手順でその点について確認しましょう。

## ステップ2: ワークシートにデータを追加する

ワークブックを作成したら、最初のワークシートにアクセスして名前を付ける必要があります。ここで、円グラフに必要なデータを入力します。

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

ここで、さまざまな地域を表すダミーの販売データを入力できます。

```csharp
cells["A1"].PutValue("Region");
cells["A2"].PutValue("France");
cells["A3"].PutValue("Germany");
cells["A4"].PutValue("England");
cells["A5"].PutValue("Sweden");
cells["A6"].PutValue("Italy");
cells["A7"].PutValue("Spain");
cells["A8"].PutValue("Portugal");

cells["B1"].PutValue("Sales");
cells["B2"].PutValue(70000);
cells["B3"].PutValue(55000);
cells["B4"].PutValue(30000);
cells["B5"].PutValue(40000);
cells["B6"].PutValue(35000);
cells["B7"].PutValue(32000);
cells["B8"].PutValue(10000);
```

ここでは、地域用と売上高用の 2 つの列を追加します。このデータは円グラフに表示されます。

## ステップ3: チャートシートを追加する

次に、円グラフを保持するための別のワークシートを追加しましょう。

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

この新しいシートには円グラフが配置されます。「チャート」などの名前を付けると、ユーザーはファイルを開いたときに何が表示されるかがわかります。

## ステップ4: 円グラフを作成する

次は実際のグラフを作成します。円グラフを指定することと、シート上の位置を定義します。

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

方法`Add()`チャートタイプのパラメータを受け入れます（この場合は、`ChartType.Pie`)、およびワークシート上の位置を示します。数字は行と列の位置を表します。

## ステップ5: グラフの外観をカスタマイズする

円グラフはカスタマイズなしでは完成しません。色、ラベル、タイトルを微調整して、グラフを視覚的に魅力的なものにしましょう。

### チャートタイトルを設定する
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### プロットエリアをカスタマイズ
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

プロット領域にグラデーション塗りつぶしを設定し、境界線を非表示にして見た目をすっきりさせます。

## ステップ6: チャートデータを定義する

チャートをデータにリンクする時が来ました。`NSeries`グラフのプロパティは、売上高と地域を円グラフにバインドします。

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

最初の行は、セルの売上データを使用することを指定します`B2:B8`また、チャートには地域名を使用するように指示します。`A2:A8`カテゴリラベルとして。

## ステップ7: データラベルを追加する

グラフのセグメントに直接ラベルを追加すると、理解しやすくなります。円グラフのスライス内に地域名と売上高を含めてみましょう。

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## ステップ8: グラフ領域と凡例をカスタマイズする

最後に、グラフ領域と凡例に最後の仕上げを施しましょう。これにより、グラフ全体のプレゼンテーションが向上します。

### チャートエリア
```csharp
ChartArea chartArea = chart.ChartArea;
chartArea.Area.Formatting = FormattingType.Custom;
chartArea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
```

### 伝説
```csharp
Legend legend = chart.Legend;
legend.Position = LegendPositionType.Left;
legend.Font.IsBold = true;
legend.Border.Color = Color.Blue;
legend.Area.FillFormat.Texture = TextureType.Bouquet;
```

## ステップ9: ワークブックを保存する

最後に、ワークブックを Excel ファイルに保存します。必要に応じて出力ディレクトリとファイル名を指定できます。

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## 結論

Aspose.Cells for .NET で円グラフを作成するのは簡単でカスタマイズ可能なプロセスです。このガイドに従うと、わずか数ステップで貴重な洞察を伝えるプロフェッショナルなグラフを作成できます。ビジネス レポート用でも教育目的でも、グラフ作成をマスターすると Excel 自動化スキルが向上します。Aspose.Cells は、魅力的なデータ駆動型 Excel ファイルを簡単に作成するために必要な柔軟性を提供します。

## よくある質問

### Aspose.Cells for .NET を使用して他の種類のグラフを作成できますか?
はい。Aspose.Cells は、棒グラフ、折れ線グラフ、散布図など、さまざまな種類のグラフをサポートしています。

### Aspose.Cells for .NET を使用するには有料ライセンスが必要ですか?
無料版はいくつかの制限付きで使用できます。フル機能を使用するにはライセンスが必要です。ライセンスは購入可能です。[ここ](https://purchase.aspose.com/buy).

### チャートを PDF や画像などの形式でエクスポートできますか?
もちろんです! Aspose.Cells を使用すると、PDF や PNG などのさまざまな形式でグラフをエクスポートできます。

### 各パイスライスを異なる色でスタイル設定することは可能ですか?
はい、設定することで各スライスに異なる色を適用できます。`IsColorVaried`財産に`true`チュートリアルに示されているとおりです。

### 1 つのワークブックで複数のグラフの生成を自動化できますか?
はい、1 つの Excel ファイル内で必要な数のグラフを作成し、カスタマイズできます。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
