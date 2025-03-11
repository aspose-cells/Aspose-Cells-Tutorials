---
title: 希望のページサイズでチャートPDFを作成する
linktitle: 希望のページサイズでチャートPDFを作成する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して、Excel グラフを含む PDF を作成します。このステップ バイ ステップ ガイドでその方法を学習します。
weight: 12
url: /ja/net/chart-rendering-and-conversion/create-chart-pdf-with-desired-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 希望のページサイズでチャートPDFを作成する

## 導入

視覚的に魅力的で情報量の多いグラフを作成することは、さまざまな分野でのデータ表現に不可欠です。販売データ、パフォーマンス メトリック、またはその他の種類の情報を扱う場合でも、高品質のグラフを作成できれば、調査結果に深みと明確さがもたらされます。.NET アプリケーションを使用している場合、Aspose.Cells は Excel ドキュメントの処理とグラフの生成を簡単にする強力なライブラリです。このチュートリアルでは、Excel ファイルから必要なページ サイズのグラフの PDF を作成する手順を説明します。

## 前提条件

コードに進む前に、スムーズなエクスペリエンスを確保するために満たす必要のある前提条件がいくつかあります。

### C# と .NET の基礎知識

C# プログラミングと .NET フレームワークの基礎知識が必要です。これにより、このガイドで取り上げるコードの構造を把握しやすくなります。

### .NET 用 Aspose.Cells

Aspose.Cells for .NETがインストールされていることを確認してください。詳細は[Aspose.Cells ドキュメント](https://reference.aspose.com/cells/net/). 

### 開発環境

開発環境を設定します。Visual StudioまたはC#をサポートする他のIDEを使用できます。Aspose.Cellsライブラリをダウンロードしてインストールします。[ダウンロードページ](https://releases.aspose.com/cells/net/).

### サンプル Excel ファイル

少なくとも 1 つのグラフを含むサンプル Excel ファイルが必要になります。このチュートリアル全体で使用するサンプル ファイルを作成するか、ダウンロードすることができます。

## パッケージのインポート

Aspose.Cells を使い始めるには、C# アプリケーションに必要な名前空間をインポートする必要があります。手順は次のとおりです。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Aspose.Cells.Charts;
```

これらの名前空間により、Excel ブックとそのコンテンツを操作するために必要なクラスとメソッドにアクセスできます。

前提条件がすべて整ったので、プロセスを詳細な手順に分解してみましょう。

## ステップ1: 出力ディレクトリとソースディレクトリを設定する

まず、出力 PDF を保存する場所とソース Excel ドキュメントが配置されている場所を定義する必要があります。

```csharp
//出力ディレクトリ
string outputDir = "Your Output Directory";

//ソースディレクトリ
string sourceDir = "Your Document Directory";
```

「出力ディレクトリ」と「ドキュメント ディレクトリ」をシステム上の実際のパスに置き換えてください。これにより、Aspose が生成された PDF を保存する場所と、Excel ファイルを検索する場所が決まります。

## ステップ2: サンプルExcelファイルを読み込む

次に、グラフを含む Excel ファイルを読み込む必要があります。手順は次のとおりです。

```csharp
//グラフを含むサンプル Excel ファイルを読み込みます。
Workbook wb = new Workbook(sourceDir + "sampleCreateChartPDFWithDesiredPageSize.xlsx");
```

の`Workbook`クラスは、Excel ドキュメントを操作する上で中心的な役割を果たします。パスが Excel ファイルを正しく指していることを確認してください。ここでエラーが発生すると、残りのコードが実行されなくなります。

## ステップ3: 最初のワークシートにアクセスする

ワークブックが読み込まれたら、次のステップは、目的のグラフを含むワークシートにアクセスすることです。

```csharp
//最初のワークシートにアクセスします。
Worksheet ws = wb.Worksheets[0];
```

 Aspose.Cellsでは、ワークシートは0から始まるインデックスが付けられるため、`Worksheets[0]`最初のシートを参照します。

## ステップ4: 最初のチャートにアクセスする

次に、PDF にエクスポートするグラフにアクセスします。この手順では、ワークシートに少なくとも 1 つのグラフが含まれていることを前提としています。

```csharp
//ワークシート内の最初のグラフにアクセスします。
Chart ch = ws.Charts[0];
```

繰り返しますが、これはワークシートの最初のグラフにアクセスします。ワークシートの構造がこのアプローチに適していることを確認してください。

## ステップ5: 希望のページサイズでPDFを作成する

最後に、指定されたページ サイズでチャートから PDF を作成します。すべてを実行する魔法のコード ラインは次のとおりです。

```csharp
//希望するページ サイズでチャートの PDF を作成します。
ch.ToPdf(outputDir + "outputCreateChartPDFWithDesiredPageSize.pdf", 7, 7, PageLayoutAlignmentType.Center, PageLayoutAlignmentType.Center);
```

このコードでは:
- PDF は、前に指定した出力ディレクトリに保存されます。
- 数字`7, 7`それぞれ、希望するページ サイズの幅と高さを表します。
- PageLayoutAlignmentType.Center は、グラフがページの中央に配置されることを保証します。

## ステップ6: 確認メッセージ

すべてがスムーズに進んだことを自分自身 (および他の人) に知らせるために、コードの最後に確認メッセージを含めます。

```csharp
Console.WriteLine("CreateChartPDFWithDesiredPageSize executed successfully.");
```

プロセスが完了すると、このメッセージがコンソール ウィンドウに表示され、PDF が問題なく作成されたことが示されます。

## 結論

おめでとうございます。Aspose.Cells for .NET を利用して、Excel ファイルに含まれるグラフから PDF を作成する方法を学習しました。この強力なライブラリは、Excel ドキュメントの操作とデータの視覚的表現の生成プロセスを効率化し、手動による書式設定に費やす時間を節約します。PDF 生成以外にも、Aspose.Cells が提供するさまざまな機能をぜひお試しください。プロジェクトをさらに強化できる機能が見つかるかもしれません。

## よくある質問

### Aspose.Cells for .NET は何に使用されますか?  
Aspose.Cells for .NET は、.NET アプリケーションでプログラムによって Excel ドキュメントを作成、編集、変換するために使用されます。

### Aspose.Cells を無料で使用できますか?  
はい、Aspose.Cellsは[無料トライアル](https://releases.aspose.com/)評価目的のため。

### 試用期間を最初の期間を超えて延長する方法はありますか?  
申請することができます[一時ライセンス](https://purchase.aspose.com/temporary-license/)拡張テスト用。

### 問題が発生した場合や質問がある場合はどうすればよいですか?  
 Asposeコミュニティからサポートを受けることができます。[サポートフォーラム](https://forum.aspose.com/c/cells/9).

### Aspose.Cells を購入するにはどうすればよいですか?  
 Aspose.Cellsは以下から購入できます。[購入ページ](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
