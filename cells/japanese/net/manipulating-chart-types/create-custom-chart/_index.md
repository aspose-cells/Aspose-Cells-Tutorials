---
title: カスタムチャートを作成する
linktitle: カスタムチャートを作成する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して Excel でカスタム グラフを作成する方法を学びます。データ視覚化スキルを向上させるためのステップ バイ ステップ ガイドです。
weight: 10
url: /ja/net/manipulating-chart-types/create-custom-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# カスタムチャートを作成する

## 導入

.NET 用の Aspose.Cells ライブラリを使用して Excel でカスタム グラフを作成するのは簡単なだけでなく、データを効果的に視覚化する優れた方法です。グラフを使用すると、ありふれたデータを説得力のあるストーリーに変換できるため、アナリストや意思決定者が洞察を得やすくなります。このチュートリアルでは、アプリケーション内でカスタム グラフを作成する方法について詳しく説明します。レポートの質を高めたい場合や、データのプレゼンテーションにセンスを加えたい場合は、このチュートリアルが役に立ちます。

## 前提条件

チャート作成の詳細に入る前に、すべてが整っていることを確認しましょう。必要なものは次のとおりです。

1. Visual Studio または任意の .NET 互換 IDE: これは、コードを記述およびテストするための環境になります。
2.  Aspose.Cells for .NETライブラリ: このライブラリがインストールされていることを確認してください。ダウンロードできます。[ここ](https://releases.aspose.com/cells/net/).
3. C# の基本的な理解: コード例で使用するため、C# の基本的な概念を理解しておくと役立ちます。
4. サンプル データセット: グラフを作成するには、いくつかのデータが必要です。例ではシンプルなデータセットを使用しますが、必要に応じて調整できます。

## パッケージのインポート

まず、C# アプリケーションに必要な Aspose.Cells 名前空間をインポートする必要があります。手順は次のとおりです。

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

基本的な構造が定義されたので、カスタム チャートを作成するためのステップ バイ ステップ ガイドを見てみましょう。

## ステップ1: 出力ディレクトリの設定

まず最初に、Excel ファイルを保存するディレクトリを作成する必要があります。この手順は、アプリケーションが最終製品の配置場所を認識できるようにするために重要です。

```csharp
//出力ディレクトリ
string outputDir = "Your Output Directory"; //これを希望のパスに変更します
```

「出力ディレクトリ」の代わりに、Excel ファイルを保存する実際のパスを指定できます。このディレクトリがシステム上に存在することを確認してください。存在しない場合、後でエラーが発生します。

## ステップ 2: ワークブック オブジェクトのインスタンス化

さて、まずは新しいインスタンスを作成して、`Workbook`クラス。これは、Aspose.Cells を使用したあらゆる Excel 操作の基本的な構成要素です。

```csharp
//ワークブックオブジェクトのインスタンス化
Workbook workbook = new Workbook();
```

このコード行は新しいワークブックを初期化し、データとグラフの追加を開始する準備が整います。

## ステップ3: ワークシートにアクセスする

次に、データを保存するワークシートへの参照を取得する必要があります。この場合は、ワークブックの最初のワークシートを操作します。

```csharp
//新しく追加されたワークシートの参照を取得する
Worksheet worksheet = workbook.Worksheets[0];
```

この行は最初のワークシート (インデックス 0) にアクセスします。Aspose.Cells では複数のワークシートを使用できるため、それに応じて選択できます。

## ステップ4: ワークシートにサンプルデータを追加する


ワークシートの準備ができたら、セルにサンプル データを追加します。シンプルなデータセットを使用すると、グラフをより効果的に視覚化できます。

```csharp
//セルにサンプル値を追加する
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["A4"].PutValue(110);
worksheet.Cells["B1"].PutValue(260);
worksheet.Cells["B2"].PutValue(12);
worksheet.Cells["B3"].PutValue(50);
worksheet.Cells["B4"].PutValue(100);
```

ここでは、A1 から B4 の範囲に値を入力します。さまざまなデータ シナリオをテストするには、これらの値を自由に変更してください。

## ステップ5: ワークシートにグラフを追加する

次は、入力したデータを視覚的に表すグラフを追加するという、面白い部分です。Aspose.Cells で利用できるさまざまなグラフ タイプから選択できます。

```csharp
//ワークシートにグラフを追加する
int chartIndex = worksheet.Charts.Add(ChartType.Column, 5, 0, 25, 10);
```

この行では、縦棒グラフを追加しています。 必要に応じて、折れ線グラフ、円グラフ、棒グラフなどの他の種類を使用することもできます。

## ステップ6: チャートインスタンスへのアクセス

チャートを追加したら、それを参照してさらに操作できるようにする必要があります。手順は次のとおりです。

```csharp
//新しく追加されたチャートのインスタンスにアクセスする
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

この時点で、`chart`必要に応じてプロパティを変更できるオブジェクト。

## ステップ 7: グラフにデータ系列を追加する

次に、チャートにデータの取得元を通知する必要があります。これは、Aspose.Cells にデータ シリーズを追加することで行われます。

```csharp
// NSeries（チャートデータソース）をチャートに追加する
chart.NSeries.Add("A1:B4", true);
```

この線は、チャートをセルに配置したデータ ポイントに効果的に接続し、チャートにこれらの値を表示できるようにします。

## ステップ8: シリーズタイプのカスタマイズ

シリーズの種類を変更することで、グラフをさらにカスタマイズできます。たとえば、視覚的にわかりやすくするために、2 番目のシリーズを折れ線グラフに変更してみましょう。

```csharp
// 2nd NSeriesのチャートタイプを折れ線グラフとして表示するように設定する
chart.NSeries[1].Type = Aspose.Cells.Charts.ChartType.Line;
```

これにより、混合タイプのチャートが可能になり、独自の視覚化の機会が提供されます。

## ステップ9: ワークブックを保存する

すべての設定が完了したら、Excel ファイルを保存します。手順は次のとおりです。

```csharp
// Excelファイルの保存
workbook.Save(outputDir + "outputHowToCreateCustomChart.xlsx");
```

ファイル名には必ず`.xlsx`ブックが正しく保存されるようにするには、拡張機能を使用します。

## 結論

これで完了です。Aspose.Cells for .NET を使用してカスタム チャートを作成しました。わずか数行のコードで、データを効果的に視覚化して、レポートやプレゼンテーションをさらに魅力的なものにすることができます。 

チャートの力は、ストーリーを伝え、複雑なデータを一目で理解できるようにする能力にあることを忘れないでください。さまざまなデータセットとチャートの種類を試して、データに語らせましょう。

## よくある質問

### Aspose.Cells とは何ですか?
Aspose.Cells は、.NET アプリケーションで Excel ファイルを操作し、Excel ドキュメントの操作、作成、変換を可能にする強力なライブラリです。

### Aspose.Cells for .NET をインストールするにはどうすればよいですか?
 Visual StudioのNuGet経由でインストールするか、ライブラリを直接ダウンロードすることができます。[ここ](https://releases.aspose.com/cells/net/).

### 異なるタイプのグラフを作成できますか?
もちろんです! Aspose.Cells は、縦棒グラフ、折れ線グラフ、円グラフ、棒グラフなど、さまざまな種類のグラフをサポートしています。

### Aspose.Cells の一時ライセンスを取得する方法はありますか?
はい、一時ライセンスは以下から取得できます。[このリンク](https://purchase.aspose.com/temporary-license/).

### Aspose.Cells に関する詳細なドキュメントはどこで見つかりますか?
完全なドキュメントを閲覧することができます[ここ](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
