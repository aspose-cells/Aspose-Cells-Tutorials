---
title: データマーカー付き折れ線グラフを作成する
linktitle: データマーカー付き折れ線グラフを作成する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して、Excel でデータ マーカー付きの折れ線グラフを作成する方法を学びます。このステップ バイ ステップ ガイドに従って、グラフを簡単に生成およびカスタマイズします。
weight: 10
url: /ja/net/working-with-chart-data/create-line-with-data-marker-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# データマーカー付き折れ線グラフを作成する

## 導入

Excel でプログラムを使用して魅力的なグラフを作成する方法を考えたことがありますか? さあ、シートベルトを締めてください。今日は、Aspose.Cells for .NET を使用してデータ マーカー付きの折れ線グラフを作成する方法を説明します。このチュートリアルでは、各手順を順を追って説明し、Aspose.Cells を使い始めたばかりの場合でも、グラフ生成をしっかりと理解できるようにします。

## 前提条件

始める前に、スムーズに進めるための準備がすべて整っていることを確認してください。

1. Aspose.Cells for .NET ライブラリ – これをインストールする必要があります。[ここ](https://releases.aspose.com/cells/net/).
2. .NET Framework – 開発環境が最新バージョンの .NET で設定されていることを確認します。
3. IDE (統合開発環境) - Visual Studio が推奨されます。
4. 有効なAspose.Cellsライセンス – ライセンスをお持ちでない場合は、[一時ライセンス](https://purchase.aspose.com/temporary-license/)または、[無料トライアル](https://releases.aspose.com/).

準備はできましたか？ 詳しく見ていきましょう！

## 必要なパッケージのインポート

まず、次の名前空間をプロジェクトにインポートしてください。これらは、チャートを作成するために必要なクラスとメソッドを提供します。

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

それができたら、コーディングを開始できます。

## ステップ1: ワークブックとワークシートを設定する

まず最初に、新しいワークブックを作成し、最初のワークシートにアクセスする必要があります。

```csharp
//出力ディレクトリ
static string outputDir = "Your Document Directory";
		
//ワークブックをインスタンス化する
Workbook workbook = new Workbook();

//最初のワークシートにアクセスする
Worksheet worksheet = workbook.Worksheets[0];
```

ワークブックを Excel ファイル、ワークシートをその中の特定のシートと考えてください。この場合、最初のシートを操作します。

## ステップ2: ワークシートにデータを入力する

ワークシートができたので、データを入力していきましょう。2 つの値のシリーズに対してランダムなデータ ポイントを作成します。

```csharp
//列のタイトルを設定する
worksheet.Cells[0, 0].Value = "X";
worksheet.Cells[0, 1].Value = "Y";

//チャートを生成するためのランダムデータ
Random R = new Random();

//ランダムデータを作成し、セルに保存する
for (int i = 1; i < 21; i++)
{
    worksheet.Cells[i, 0].Value = i;
    worksheet.Cells[i, 1].Value = 0.8;
}

for (int i = 21; i < 41; i++)
{
    worksheet.Cells[i, 0].Value = i - 20;
    worksheet.Cells[i, 1].Value = 0.9;
}
```

ここでは乱数を使用してデータをシミュレートしていますが、実際のアプリケーションではデータセットから実際の値を入力できます。

## ステップ3: ワークシートにグラフを追加する

次に、グラフをワークシートに追加し、種類を選択します。この場合は、データ マーカー付き折れ線グラフです。

```csharp
//ワークシートにグラフを追加する
int idx = worksheet.Charts.Add(ChartType.LineWithDataMarkers, 1, 3, 20, 20);

//新しく作成されたチャートにアクセスする
Chart chart = worksheet.Charts[idx];
```

このスニペットは、データ マーカー付きの折れ線グラフをワークシートに追加し、特定の範囲 (1,3 ～ 20,20) に配置します。とてもシンプルですよね?

## ステップ4: チャートの外観をカスタマイズする

グラフを作成したら、好みに合わせてスタイルを設定できます。背景、タイトル、グラフのスタイルを変更してみましょう。

```csharp
//チャートのスタイルを設定する
chart.Style = 3;

//自動スケーリング値をtrueに設定する
chart.AutoScaling = true;

//前景色を白に設定する
chart.PlotArea.Area.ForegroundColor = Color.White;

//グラフタイトルのプロパティを設定する
chart.Title.Text = "Sample Chart";

//チャートの種類を設定する
chart.Type = ChartType.LineWithDataMarkers;
```

ここでは、白い背景を設定し、自動スケーリングし、意味のあるタイトルを付けることで、チャートをすっきりとした外観にしています。

## ステップ5: シリーズを定義してデータポイントをプロットする

グラフの見栄えが良くなったので、プロットするデータ系列を定義する必要があります。

```csharp
//カテゴリ軸タイトルのプロパティを設定する
chart.CategoryAxis.Title.Text = "Units";

//チャートに2つのシリーズを定義する
int s2_idx = chart.NSeries.Add("A2: A21", true);
int s3_idx = chart.NSeries.Add("A22: A41", true);
```

これらのシリーズは、先ほど入力したデータ ポイントの範囲に対応しています。

## ステップ6: 色を追加してシリーズマーカーをカスタマイズする

データ マーカーにカスタム カラーを追加して、このグラフをさらに魅力的にしてみましょう。

```csharp
//最初のシリーズをカスタマイズ
chart.NSeries[s2_idx].Marker.Area.ForegroundColor = Color.Yellow;
chart.NSeries[s2_idx].Marker.Border.IsVisible = false;

//第2シリーズをカスタマイズ
chart.NSeries[s3_idx].Marker.Area.ForegroundColor = Color.Green;
chart.NSeries[s3_idx].Marker.Border.IsVisible = false;
```

色をカスタマイズすることで、チャートが機能的になるだけでなく、視覚的にも魅力的になります。

## ステップ7: 各シリーズのX値とY値を設定する

最後に、各シリーズに X 値と Y 値を割り当てます。

```csharp
//最初のシリーズのX値とY値を設定する
chart.NSeries[s2_idx].XValues = "A2: A21";
chart.NSeries[s2_idx].Values = "B2: B21";

//2番目のシリーズのX値とY値を設定する
chart.NSeries[s3_idx].XValues = "A22: A41";
chart.NSeries[s3_idx].Values = "B22: B41";
```

値は手順 2 で入力したデータに基づいています。

## ステップ8: ワークブックを保存する

すべての設定が完了したら、ワークブックを保存して、グラフの動作を確認してみましょう。

```csharp
//ワークブックを保存する
workbook.Save(outputDir + @"LineWithDataMarkerChart.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```

これで完了です。Aspose.Cells for .NET を使用して、データ マーカー付きの折れ線グラフを作成しました。

## 結論

Excel でプログラムを使用してグラフを作成するのは困難に思えるかもしれませんが、Aspose.Cells for .NET を使用すると、手順ごとのレシピに従うだけで簡単に作成できます。ワークブックの設定からグラフの外観のカスタマイズまで、この強力なライブラリがすべてを処理します。レポート、ダッシュボード、またはデータの視覚化を作成する場合でも、Aspose.Cells を使用すると簡単に実行できます。

## よくある質問

### チャートをさらにカスタマイズできますか?  
もちろんです! Aspose.Cells には、フォントからグリッド線まで、さまざまなカスタマイズ オプションが用意されています。

### Aspose.Cells を使用するにはライセンスが必要ですか?  
はい、フル機能を使用するにはライセンスが必要です。[一時ライセンス](https://purchase.aspose.com/temporary-license/)または[無料トライアル](https://releases.aspose.com/).

### さらにデータ シリーズを追加するにはどうすればよいですか?  
追加のシリーズを追加するには、`NSeries.Add`メソッドを使用して、新しいデータのセル範囲を指定します。

### チャートを画像としてエクスポートできますか?  
はい、チャートを画像として直接エクスポートすることができます。`Chart.ToImage`方法。

### Aspose.Cells は 3D グラフをサポートしていますか?  
はい、Aspose.Cells は 3D グラフを含む幅広いグラフ タイプをサポートしています。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
