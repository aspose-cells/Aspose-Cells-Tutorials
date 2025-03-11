---
title: 円グラフの変更
linktitle: 円グラフの変更
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET のパワーを活用して、Excel の円グラフを簡単に変更します。ステップ バイ ステップのガイダンスについては、このチュートリアルに従ってください。
weight: 16
url: /ja/net/manipulating-chart-types/modify-pie-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 円グラフの変更

## 導入

Excel シートの円グラフを美しく仕上げる方法を考えたことはありませんか? 円グラフは、データを視覚化して、視聴者の関心を引き、情報を提供するための優れた方法です。しかし、円グラフでは、すぐには伝えたい内容が伝わらないことがあります。そこで、Aspose.Cells for .NET が役立ちます。この強力なライブラリを使用すると、Excel ファイルをプログラムで操作でき、円グラフを細部までカスタマイズするために必要なツールが提供されます。このチュートリアルでは、Aspose.Cells を使用して円グラフを変更する方法を詳しく説明します。データ ラベルの変更やグラフの外観の調整などです。

## 前提条件

円グラフの変更の詳細に入る前に、いくつかの前提条件を満たす必要があります。

- C# の基礎知識: C# プログラミングの基礎を理解しておくと、簡単に理解できるようになります。
- Aspose.Cells for .NET: Aspose.Cells ライブラリをインストールする必要があります。フル バージョンを使用するか、無料試用版を選択するかにかかわらず、準備が整っていることを確認してください。
- Visual Studio または任意の C# IDE: C# コードを記述して実行するための環境が必要です。
-  Excelサンプルファイル: このチュートリアルでは、サンプルExcelファイル`sampleModifyPieChart.xlsx`使用されます。

 Aspose.Cellsライブラリをダウンロードできます[ここ](https://releases.aspose.com/cells/net/).

## パッケージのインポート

この旅の最初のステップは、必要なパッケージを C# プロジェクトにインポートすることです。その方法は次のとおりです。

## プロジェクトを設定する

まず、C# IDE (Visual Studio を強く推奨) を開いて、新しいプロジェクトを作成します。

1. Visual Studio を開きます。
2. 「新しいプロジェクトを作成する」を選択します。
3. C# コンソール アプリケーションを選択します。
4. プロジェクトに名前を付けます（例：`ModifyPieChartDemo`）。
5. 「作成」をクリックします。

## Aspose.Cellsをインストールする

プロジェクトの準備ができたら、Aspose.Cells ライブラリを追加します。NuGet を使用してインストールできます。

1. 「ソリューション エクスプローラー」でプロジェクトを右クリックします。
2. NuGet パッケージの管理を選択します。
3. [参照] タブに移動します。
4. Aspose.Cells を検索します。
5. [インストール] をクリックし、ライセンス契約に同意します。

ライブラリがインストールされたので、コードに必要な名前空間をインポートしましょう。

## 名前空間のインポート

あなたの一番上に`Program.cs`ファイルで、次の名前空間をインポートします。

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

これで、実際のコードに進む準備が整いました。

## ステップ1: 入力ディレクトリと出力ディレクトリを定義する

まず、入力ファイルと出力ファイルのディレクトリを定義します。ここで、Excel ファイルの場所と変更したファイルを保存する場所を指定します。

あなたの`Main`メソッドに次のコードを入力します。

```csharp
//出力ディレクトリ
string outputDir = "Your Output Directory Path";

//ソースディレクトリ
string sourceDir = "Your Document Directory Path";
```

必ず交換してください`Your Output Directory Path`そして`Your Document Directory Path`システム上の実際のパスを使用します。

## ステップ2: 既存のワークブックを開く

次に、変更したい円グラフを含むExcelファイルを開く必要があります。これには、`Workbook`クラス：

```csharp
//既存のファイルを開きます。
Workbook workbook = new Workbook(sourceDir + "sampleModifyPieChart.xlsx");
```

このスニペットでは、新しい`Workbook`オブジェクトを作成し、Excel ファイルをそこに読み込みます。

## ステップ3: ワークシートにアクセスする

さて、円グラフが含まれている特定のシートを見てみましょう。円グラフは 2 番目のワークシート (インデックス 1) にあると仮定します。

```csharp
// 2 枚目のシートでデザイナー チャートを取得します。
Worksheet sheet = workbook.Worksheets[1];
```

アクセスすることで`Worksheets`コレクションを使用すると、必要な特定のシートにアクセスできます。

## ステップ4: チャートを取得する

これで、グラフ自体にアクセスする準備ができました。ワークシートにグラフが 1 つしかないと仮定すると、グラフを直接取得できます。

```csharp
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

ここでは、指定されたワークシートから最初のグラフを取得しています。

## ステップ5: データラベルにアクセスする

次は、円グラフのデータ ラベルを変更するという楽しい部分です。データ系列のデータ ラベルにアクセスしてみましょう。

```csharp
// 3 番目のデータ ポイントのデータ シリーズのデータ ラベルを取得します。
Aspose.Cells.Charts.DataLabels datalabels = chart.NSeries[0].Points[2].DataLabels;
```

この行では、データ シリーズの 3 番目のポイントのデータ ラベルを具体的にターゲットにしています。 

## ステップ6: ラベルテキストを変更する

次に、ラベルの内容を変更します。この例では、「イギリス、400K」に更新します。

```csharp
//ラベルのテキストを変更します。
datalabels.Text = "United Kingdom, 400K";
```

これでラベルが更新されました！ 

## ステップ7: ワークブックを保存する

変更が完了したら、変更したブックを保存しましょう。 

```csharp
// Excel ファイルを保存します。
workbook.Save(outputDir + "outputModifyPieChart.xlsx");
```

この行は、指定された出力ディレクトリにワークブックを保存します。 

## ステップ8: 実行を確認する

最後に、すべてがスムーズに実行されたことを確認するために確認メッセージを出力しましょう。

```csharp
Console.WriteLine("ModifyPieChart executed successfully.");
```

これにより、変更が期待どおりに行われたという安心感が得られます。

# 結論

これで完了です。いくつかの簡単な手順で、Aspose.Cells for .NET を使用して円グラフを修正できました。この強力なライブラリを使用すると、Excel ファイルの操作が簡単になるだけでなく、データの視覚化をカスタマイズして最大限の効果を得ることができます。仕事でデータのプレゼンテーションを扱っている場合は、Aspose.Cells の使用方法を学習する時間を投資すると、確実に成果が得られます。さあ、これらのグラフを操作して、データに命を吹き込む方法を確認してください。

# よくある質問

### Aspose.Cells for .NET とは何ですか?  
Aspose.Cells for .NET は、Microsoft Excel を必要とせずにプログラムで Excel ファイルを作成、操作、変換できるように設計された強力なライブラリです。

### 円グラフ以外のグラフを変更できますか?  
もちろんです! Aspose.Cells は、棒グラフ、折れ線グラフ、面グラフなど、さまざまな種類のグラフをサポートしており、柔軟なデータ視覚化が可能です。

### Aspose.Cells の無料版はありますか?  
はい！Aspose では、購入前にライブラリをテストできる無料試用版を提供しています。

### Aspose.Cells のサポートはどこで見つかりますか?  
Aspose フォーラムでサポートを受けることができ、コミュニティ メンバーと Aspose スタッフがサポートします。

### Aspose.Cells を使用するには Microsoft Excel をインストールする必要がありますか?  
いいえ、Aspose.Cells は Microsoft Excel とは独立して動作します。システムにインストールする必要はありません。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
