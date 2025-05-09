---
"description": "Aspose.Cells for .NET を使って、Excel で魅力的な 3D グラフを作成する方法をご紹介します。簡単なステップバイステップガイドに従って操作してください。"
"linktitle": "グラフに3D形式を適用する"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": "グラフに3D形式を適用する"
"url": "/ja/net/advanced-chart-operations/apply-3d-format-to-chart/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# グラフに3D形式を適用する

## 導入

データの視覚化が最重要視される時代において、データの提示方法は単なるグラフやチャートにとどまりません。Aspose.Cells for .NETのようなツールを使えば、魅力的な3Dチャートを作成し、注目を集めるだけでなく、情報を効果的に伝えることで、データプレゼンテーションのレベルを高めることができます。このガイドでは、Aspose.Cellsを使ってチャートに3Dフォーマットを適用し、生のデータを魅力的な表示に変換する手順を解説します。

## 前提条件

チャートに 3D 形式を適用する具体的な手順に入る前に、必要なものがすべて揃っていることを確認しましょう。

### ソフトウェア要件

- Visual Studio: .NET アプリケーションを操作するには、Visual Studio がインストールされていることを確認してください。
- Aspose.Cells for .NET: まだインストールしていない場合は、Aspose.Cellsを以下のサイトからダウンロードしてインストールしてください。 [ここ](https://releases。aspose.com/cells/net/).

### コーディング環境のセットアップ

1. 新しい .NET プロジェクトを作成する: Visual Studio を開き、「新しいプロジェクトの作成」を選択して、コンソール アプリケーションを選択します。
2. Aspose.Cells 参照の追加: NuGet パッケージ マネージャーを使用して、Aspose.Cells を検索するか、パッケージ マネージャー コンソールを使用して追加します。

```bash
Install-Package Aspose.Cells
```

3. 出力ディレクトリの設定: 生成されたファイルを保存する出力ディレクトリを指定します。これは、デスクトップにフォルダーを作成するのと同じくらい簡単です。

これですべての準備が整いました。次はコードを入力して、魅力的な 3D チャートを作成しましょう。

## パッケージのインポート

まず、必要な名前空間をインポートする必要があります。これにより、Aspose.Cells が提供するクラスとメソッドにアクセスできるようになります。手順は以下のとおりです。

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

まず、 `Workbook` クラス。このオブジェクトは Excel ドキュメントの基盤として機能します。

```csharp
//出力ディレクトリ
string outputDir = "Your Document Directory";
Workbook book = new Workbook();
```
考えてみてください `Workbook` 空白のキャンバスとして、カラフルなデータとインパクトのある視覚化で埋め込むことができます。

## ステップ2: 最初のワークシートの名前を変更する

次に、最初のワークシートの名前を変更しましょう。これにより、どのようなデータを扱っているのかが明確になります。

```csharp
book.Worksheets[0].Name = "DataSheet";
```

名前は直感的に分かりやすいものにしましょう。今回は、データがどこに保存されているかがわかるように「DataSheet」という名前を付けています。

## ステップ3: グラフのデータを作成する

それでは、「データシート」にデータを追加し、チャートで使用する値を入力していきましょう。

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

グラフ自体用の新しいワークシートを作成しましょう。これにより、データの視覚化を整理しやすくなります。

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

チャート用のスペースを定義し、そのタイプを指定します。アートワークのフレームタイプを選択するのと同じだと考えてください。

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

## ステップ7: グラフにデータ系列を追加する

いよいよチャートにデータを入力します。「データシート」からデータ系列を追加して、チャートに必要なデータが反映されるようにします。

```csharp
chart.NSeries.Add("DataSheet!B1:B3", true);
chart.NSeries.CategoryData = "DataSheet!A1:A3";
```

これは、シェフが特定の食材を使って料理を作るようなものです。それぞれのデータポイントが重要です！

## ステップ8: データシリーズにアクセスして書式設定する

データがリンクされたので、データ シリーズを取得して 3D 効果を適用してみましょう。

```csharp
Aspose.Cells.Charts.Series ser = chart.NSeries[0];
ShapePropertyCollection spPr = ser.ShapeProperties;
Format3D fmt3d = spPr.Format3D;
```

料理にちょっとした風味を加える準備をします。全体の風味を高める調味料と考えてください。

## ステップ9：3Dベベル効果を適用する

次に、チャートに立体感を与えるためにベベル効果を追加します。

```csharp
Bevel bevel = fmt3d.TopBevel;
bevel.Type = BevelPresetType.Circle;
bevel.Height = 2;
bevel.Width = 5;
```

彫刻家が石を形作るのと同じように、私たちはチャートに命を吹き込む深みを作り出しています。

## ステップ10: 表面の材質と照明をカスタマイズする

チャートを明るく輝かせましょう！表面の材質と照明の設定を調整します。

```csharp
fmt3d.SurfaceMaterialType = PresetMaterialType.WarmMatte;
fmt3d.SurfaceLightingType = LightRigType.ThreePoint;
fmt3d.LightingAngle = 20;
```

適切な照明と素材は、平面的な物体を魅力的なビジュアルに変えることができます。あらゆるシーンを美しく演出するために巧みに照明が当てられた映画のセットを想像してみてください。

## ステップ11：シリーズの外観の最終仕上げ

次に、色を調整してデータ シリーズの外観を最終決定します。

```csharp
ser.Area.BackgroundColor = Color.Maroon;
ser.Area.ForegroundColor = Color.Maroon;
ser.Border.Color = Color.Maroon;
```

適切な色は特定の感情や反応を呼び起こすことができます。栗色は上品さと洗練さの雰囲気を加えます。

## ステップ12: ワークブックを保存する

いよいよ傑作を保存する時です！保存先を忘れずに指定してください。

```csharp
book.Save(outputDir + "outputApplying3DFormat.xlsx");
Console.WriteLine("Applying3DFormat executed successfully.");
```

作品を保存することは、ギャラリーに作品を展示するのと同じようなもので、大切にし、共有する瞬間です。

## 結論

おめでとうございます！Aspose.Cells for .NET を使って、視覚的に魅力的な3Dチャートを作成できました。これらの手順に従うことで、データプレゼンテーションを強化する強力なツールが手に入り、情報を伝えるだけでなく、視覚的にも魅力的なものになります。チャートを洗練させる際には、それぞれのビジュアライゼーションがストーリーであることを忘れないでください。魅力的で、明確で、インパクトのあるものにしましょう。

## よくある質問

### Aspose.Cells for .NET とは何ですか?
Aspose.Cells for .NET は、グラフや図の作成など、開発者が Excel ドキュメントをプログラムで操作できるようにする強力なライブラリです。

### Aspose.Cells でグラフの種類をカスタマイズできますか?
はい！Aspose.Cells は、縦棒グラフ、折れ線グラフ、円グラフなど、さまざまな種類のグラフをサポートしており、簡単にカスタマイズできます。

### Aspose.Cells の無料トライアルはありますか?
もちろんです！無料トライアルはこちらからダウンロードできます。 [ここ](https://releases。aspose.com/).

### 3D 形式以外の効果をチャートに適用できますか?
はい、影、グラデーション、さまざまなスタイルなどのさまざまな効果を適用して、チャートを 3D 以上に強化できます。

### Aspose.Cells のサポートはどこで見つかりますか?
サポートについては、 [Asposeフォーラム](https://forum.aspose.com/c/cells/9) コミュニティの支援と援助のため。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}