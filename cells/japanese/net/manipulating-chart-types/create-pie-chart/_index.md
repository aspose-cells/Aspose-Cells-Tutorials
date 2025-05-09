---
"description": "このステップバイステップガイドでは、Aspose.Cells for .NET を使用して Excel で円グラフを作成する方法を学びます。データを簡単に視覚化できます。"
"linktitle": "円グラフを作成する"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": "円グラフを作成する"
"url": "/ja/net/manipulating-chart-types/create-pie-chart/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 円グラフを作成する

## 導入

データを視覚的に表現するにはグラフの作成が不可欠です。中でも円グラフは、各要素が全体を構成する様子を示す最も一般的な方法の一つです。Aspose.Cells for .NETを使えば、Excelファイルでの円グラフ生成を簡単に自動化できます。このチュートリアルでは、Aspose.Cells for .NETを使って円グラフをゼロから作成する方法を、ステップバイステップで分かりやすく解説します。Aspose.Cells for .NETを初めて使う方にも、Excelの自動化スキルを高めたい方にも、このガイドはきっとお役に立ちます。

## 前提条件

コードに進む前に、次の設定がされていることを確認してください。

1. Aspose.Cells for .NET ライブラリ: プロジェクトに Aspose.Cells がインストールされていることを確認してください。まだインストールしていない場合は、こちらからダウンロードできます。 [ここ](https://releases。aspose.com/cells/net/).
2. .NET 開発環境: プロジェクトが .NET Framework または .NET Core を使用するように設定されていることを確認します。
3. C# の基礎知識: C# プログラミング、特にオブジェクト指向プログラミング (OOP) に精通している必要があります。

上級ユーザー向けには、Aspose.Cellsの全機能を利用するための一時ライセンスを申請できます。 [ここ](https://purchase。aspose.com/temporary-license/).

## パッケージのインポート

まず、このチュートリアルに必要な名前空間とパッケージをインポートします。これには、基本的なI/O操作とAspose.Cellsパッケージが含まれます。

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## ステップ1: 新しいワークブックを作成する

まず、 `Workbook` Excelファイルを表すクラスです。ワークブックには複数のシートが含まれており、この例では2つのシート（1つはデータ用、もう1つは円グラフ用）を操作します。

```csharp
Workbook workbook = new Workbook();
```

これで新しいExcelブックが初期化されます。では、データはどこに行くのでしょうか？次のステップで確認しましょう。

## ステップ2: ワークシートにデータを追加する

ワークブックを作成したら、最初のワークシートにアクセスして名前を付けます。ここで円グラフに必要なデータを入力します。

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

ここでは、地域別と売上高別の2つの列を追加します。これらのデータは円グラフに表示されます。

## ステップ3: チャートシートを追加する

次に、円グラフを保持するための別のワークシートを追加しましょう。

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

この新しいシートに円グラフを配置します。「Chart」などの名前を付けることで、ユーザーがファイルを開いたときに何が表示されるかがわかりやすくなります。

## ステップ4: 円グラフを作成する

いよいよ実際のグラフを作成します。円グラフを作成し、シート上の位置を定義します。

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

方法 `Add()` チャートタイプのパラメータを受け入れます（この場合は、 `ChartType.Pie`）とワークシート上の位置を示します。数字は行と列の位置を表します。

## ステップ5: グラフの外観をカスタマイズする

円グラフはカスタマイズなしでは完成しません！色、ラベル、タイトルを微調整して、見た目に魅力的なグラフを作りましょう。

### チャートのタイトルを設定する
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

チャートをデータにリンクしてみましょう。 `NSeries` グラフのプロパティは、売上高と地域を円グラフにバインドします。

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

最初の行は、セルからの販売データを使用することを指定します `B2:B8`また、チャートには地域名を使用するように指示します。 `A2:A8` カテゴリラベルとして。

## ステップ7: データラベルを追加する

グラフの各セグメントに直接ラベルを追加すると、より分かりやすくなります。円グラフのスライスに地域名と売上高を表示してみましょう。

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

最後に、グラフエリアと凡例に最後の仕上げを施しましょう。これにより、グラフ全体の見栄えが向上します。

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

最後に、ワークブックをExcelファイルに保存します。必要に応じて出力ディレクトリとファイル名を指定できます。

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## 結論

Aspose.Cells for .NET を使った円グラフの作成は、シンプルでカスタマイズ性に優れています。このガイドに従えば、わずか数ステップで、価値ある洞察を伝えるプロフェッショナルなグラフを作成できます。ビジネスレポート作成でも教育目的でも、グラフ作成をマスターすれば、Excel の自動化スキルが向上します。Aspose.Cells は、データドリブンで魅力的な Excel ファイルを簡単に作成するために必要な柔軟性を提供します。

## よくある質問

### Aspose.Cells for .NET を使用して他の種類のグラフを作成できますか?
はい！Aspose.Cells は、棒グラフ、折れ線グラフ、散布図など、さまざまな種類のグラフをサポートしています。

### Aspose.Cells for .NET を使用するには有料ライセンスが必要ですか?
無料版は一部機能制限付きでご利用いただけます。フル機能を使用するには、ライセンスを購入する必要があります。 [ここ](https://purchase。aspose.com/buy).

### チャートを PDF や画像などの形式でエクスポートできますか?
もちろんです！Aspose.Cells を使用すると、PDF や PNG などのさまざまな形式でグラフをエクスポートできます。

### 各円グラフのスライスを異なる色でスタイル設定することは可能ですか?
はい、設定することで各スライスに異なる色を適用できます。 `IsColorVaried` 財産に `true`チュートリアルに示されているとおりです。

### 1 つのワークブック内で複数のグラフの生成を自動化できますか?
はい、1 つの Excel ファイル内で必要な数のグラフを作成し、カスタマイズできます。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}