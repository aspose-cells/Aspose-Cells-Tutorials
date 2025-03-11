---
title: チャートに3Dフォーマットを適用する
linktitle: チャートに3Dフォーマットを適用する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して Excel で魅力的な 3D グラフを作成する方法をご覧ください。簡単なステップバイステップ ガイドに従ってください。
weight: 10
url: /ja/net/advanced-chart-operations/apply-3d-format-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# チャートに3Dフォーマットを適用する

## 導入

データの視覚化が何よりも重要視される時代において、データを提示する方法は、基本的なグラフやチャートの域を超えています。Aspose.Cells for .NET などのツールを使用すれば、注目を集めるだけでなく情報を効果的に伝える魅力的な 3D チャートでデータ プレゼンテーションのレベルを高めることができます。このガイドでは、Aspose.Cells を使用して 3D 形式をチャートに適用し、生データを魅力的な表示に変換する手順を説明します。

## 前提条件

チャートに 3D 形式を適用するという細かい作業に入る前に、必要なものがすべて揃っていることを確認しましょう。

### ソフトウェア要件

- Visual Studio: .NET アプリケーションを操作するには、Visual Studio がインストールされていることを確認してください。
-  Aspose.Cells for .NET: まだダウンロードしていない場合は、こちらからAspose.Cellsをダウンロードしてインストールしてください。[ここ](https://releases.aspose.com/cells/net/).

### コーディング環境のセットアップ

1. 新しい .NET プロジェクトを作成する: Visual Studio を開き、「新しいプロジェクトの作成」を選択して、コンソール アプリケーションを選択します。
2. Aspose.Cells 参照の追加: NuGet パッケージ マネージャーを使用して、Aspose.Cells を検索するか、パッケージ マネージャー コンソールを使用して追加します。

```bash
Install-Package Aspose.Cells
```

3. 出力ディレクトリの設定: 生成されたファイルを保存する出力ディレクトリを指定します。これは、デスクトップにフォルダーを作成するだけの簡単な作業です。

これで準備はすべて完了です。コードを入力して、魅力的な 3D チャートを作成しましょう。

## パッケージのインポート

まず、必要な名前空間をインポートする必要があります。これにより、Aspose.Cells が提供するクラスとメソッドにアクセスできるようになります。手順は次のとおりです。

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

このセクションでは、プロセスを管理しやすいステップに分割し、各段階を明確に理解できるようにします。

## ステップ1: ワークブックを初期化する

まず、インスタンスを作成する必要があります`Workbook`クラス。このオブジェクトは Excel ドキュメントの基盤として機能します。

```csharp
//出力ディレクトリ
string outputDir = "Your Document Directory";
Workbook book = new Workbook();
```
考えてみてください`Workbook`空白のキャンバスとして、カラフルなデータとインパクトのある視覚化で埋めることができます。

## ステップ2: 最初のワークシートの名前を変更する

次に、最初のワークシートの名前を変更しましょう。これにより、どのようなデータを扱っているかが明確になります。

```csharp
book.Worksheets[0].Name = "DataSheet";
```

名前は直感的なものにする必要があります。この場合、データがどこに保存されているかがわかるように「DataSheet」という名前を付けます。

## ステップ3: グラフのデータを作成する

ここで、「データシート」にデータを追加します。グラフで使用する値を入力しましょう。

```csharp
Worksheet dataSheet = book.Worksheets["DataSheet"];
dataSheet.Cells["B1"].PutValue(1);
dataSheet.Cells["B2"].PutValue(2);
dataSheet.Cells["B3"].PutValue(3);
dataSheet.Cells["A1"].PutValue("A");
dataSheet.Cells["A2"].PutValue("B");
dataSheet.Cells["A3"].PutValue("C");
```

レシピが材料によって決まるのと同じように、チャートの効果は入力データの品質と構成によって決まります。

## ステップ4: 新しいチャートワークシートを設定する

グラフ自体の新しいワークシートを作成します。これにより、データの視覚化を整理しやすくなります。

```csharp
Worksheet sheet = book.Worksheets.Add("MyChart");
```

このワークシートを、データのパフォーマンスが展開されるステージとして考えてください。

## ステップ5: グラフを追加する

ここでは、新しく作成したワークシートに縦棒グラフを追加します。  

```csharp
ChartCollection charts = sheet.Charts;
int chartSheetIdx = charts.Add(ChartType.Column, 5, 0, 25, 15);
```

チャートのスペースを定義し、そのタイプを指定します。アートワークのフレームのタイプを選択するのと同じだと考えてください。

## ステップ6: グラフの外観をカスタマイズする

次に、背景色を設定してグラフの外観をカスタマイズしましょう。 

```csharp
Aspose.Cells.Charts.Chart chart = book.Worksheets["MyChart"].Charts[0];
chart.PlotArea.Area.BackgroundColor = Color.White;
chart.ChartArea.Area.BackgroundColor = Color.White;
chart.PlotArea.Area.ForegroundColor = Color.White;
chart.ChartArea.Area.ForegroundColor = Color.White;
chart.ShowLegend = false;
```

きれいな白い背景は、データの色を目立たせ、視認性を高めます。

## ステップ 7: グラフにデータ系列を追加する

グラフにデータを入力します。必要なデータがグラフに反映されるように、「データシート」からデータ シリーズを追加します。

```csharp
chart.NSeries.Add("DataSheet!B1:B3", true);
chart.NSeries.CategoryData = "DataSheet!A1:A3";
```

これは、シェフが特定の材料を使って料理を準備するのに似ています。各データ ポイントが重要です。

## ステップ8: データシリーズにアクセスしてフォーマットする

データがリンクされたので、データ シリーズを取得して 3D 効果を適用してみましょう。

```csharp
Aspose.Cells.Charts.Series ser = chart.NSeries[0];
ShapePropertyCollection spPr = ser.ShapeProperties;
Format3D fmt3d = spPr.Format3D;
```

料理にちょっとした風味を加える準備をしています。全体の風味を高める調味料と考えてください。

## ステップ9: 3Dベベル効果を適用する

次に、チャートに立体感を与えるためにベベル効果を追加します。

```csharp
Bevel bevel = fmt3d.TopBevel;
bevel.Type = BevelPresetType.Circle;
bevel.Height = 2;
bevel.Width = 5;
```

彫刻家が石を形作るのと同じように、私たちはチャートに命を吹き込む深みを作り出しています。

## ステップ10: 表面の材質と照明をカスタマイズする

チャートを明るく輝かせましょう。表面の材質と照明の設定を調整します。

```csharp
fmt3d.SurfaceMaterialType = PresetMaterialType.WarmMatte;
fmt3d.SurfaceLightingType = LightRigType.ThreePoint;
fmt3d.LightingAngle = 20;
```

適切な照明と素材により、平面の物体を魅力的なビジュアルに変えることができます。あらゆるシーンを引き立てるために巧みに照明された映画セットを想像してみてください。

## ステップ11: シリーズの外観の最終調整

次に、色を調整してデータ シリーズの外観を最終決定します。

```csharp
ser.Area.BackgroundColor = Color.Maroon;
ser.Area.ForegroundColor = Color.Maroon;
ser.Border.Color = Color.Maroon;
```

適切な色は特定の感情や反応を呼び起こすことができます。栗色は優雅さと洗練さの雰囲気を加えます。

## ステップ12: ワークブックを保存する

最後に、傑作を保存します。保存先を指定することを忘れないでください。

```csharp
book.Save(outputDir + "outputApplying3DFormat.xlsx");
Console.WriteLine("Applying3DFormat executed successfully.");
```

作品を保存することは、ギャラリーに作品を展示するのと同じで、大切に共有する瞬間です。

## 結論

おめでとうございます! Aspose.Cells for .NET を使用して、視覚的に魅力的な 3D グラフを作成しました。これらの手順に従うことで、データ プレゼンテーションを強化する強力なツールが手に入り、情報を伝えるだけでなく視覚的にも魅力的になります。グラフを改良する際は、各視覚化がストーリーであることを忘れないでください。魅力的で明確でインパクトのあるものにしてください。

## よくある質問

### Aspose.Cells for .NET とは何ですか?
Aspose.Cells for .NET は、グラフや図の作成など、開発者が Excel ドキュメントをプログラムで操作できるようにする強力なライブラリです。

### Aspose.Cells でグラフの種類をカスタマイズできますか?
はい！Aspose.Cells は、縦棒グラフ、折れ線グラフ、円グラフなど、さまざまなグラフ タイプをサポートしており、簡単にカスタマイズできます。

### Aspose.Cells の無料トライアルはありますか?
もちろんです！無料トライアルはこちらからダウンロードできます[ここ](https://releases.aspose.com/).

### 3D 形式以外の効果をチャートに適用できますか?
はい、影、グラデーション、さまざまなスタイルなどのさまざまな効果を適用して、3D を超えてチャートを強化できます。

### Aspose.Cells のサポートはどこで見つかりますか?
サポートについては、[Aspose フォーラム](https://forum.aspose.com/c/cells/9)コミュニティの支援と援助のため。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
