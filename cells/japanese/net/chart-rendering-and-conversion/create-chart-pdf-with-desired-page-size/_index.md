---
"description": "Aspose.Cells for .NET を使って、Excel のグラフを PDF にエクスポートしましょう。このステップバイステップガイドでその方法を学びましょう。"
"linktitle": "希望のページサイズでチャートPDFを作成する"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": "希望のページサイズでチャートPDFを作成する"
"url": "/ja/net/chart-rendering-and-conversion/create-chart-pdf-with-desired-page-size/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 希望のページサイズでチャートPDFを作成する

## 導入

視覚的に魅力的で情報量の多いグラフを作成することは、様々な分野のデータ表現に不可欠です。売上データ、業績指標、その他あらゆる情報を扱う場合、高品質なグラフを作成できれば、分析結果に深みと明瞭さを与えることができます。.NETアプリケーションをお使いの場合、Aspose.CellsはExcelドキュメントの扱いとグラフ生成を非常に簡単にする強力なライブラリです。このチュートリアルでは、Excelファイルから任意のページサイズでグラフのPDFを作成する手順を説明します。

## 前提条件

コードに進む前に、スムーズなエクスペリエンスを確保するために満たす必要のある前提条件がいくつかあります。

### C#と.NETの基礎知識

C#プログラミングと.NETフレームワークの基礎知識が必要です。これにより、このガイドで扱うコードの構造を理解するのに役立ちます。

### Aspose.Cells .NET 版

Aspose.Cells for .NETがインストールされていることを確認してください。詳細は以下をご覧ください。 [Aspose.Cells ドキュメント](https://reference。aspose.com/cells/net/). 

### 開発環境

開発環境をセットアップします。Visual Studioでも、C#をサポートする他のIDEでも構いません。Aspose.Cellsライブラリを以下のサイトからダウンロードしてインストールします。 [ダウンロードページ](https://releases。aspose.com/cells/net/).

### サンプル Excel ファイル

少なくとも1つのグラフを含むサンプルのExcelファイルが必要です。このチュートリアルで使用するサンプルファイルを作成するか、ダウンロードしてください。

## パッケージのインポート

Aspose.Cells を使い始めるには、C# アプリケーションに必要な名前空間をインポートする必要があります。手順は以下のとおりです。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Aspose.Cells.Charts;
```

これらの名前空間により、Excel ブックとそのコンテンツを操作するために必要なクラスとメソッドにアクセスできるようになります。

前提条件がすべて整ったので、プロセスを詳細な手順に分解してみましょう。

## ステップ1: 出力ディレクトリとソースディレクトリの設定

まず、出力 PDF を保存する場所と、ソース Excel ドキュメントが配置されている場所を定義する必要があります。

```csharp
//出力ディレクトリ
string outputDir = "Your Output Directory";

//ソースディレクトリ
string sourceDir = "Your Document Directory";
```

「出力ディレクトリ」と「ドキュメントディレクトリ」をシステム上の実際のパスに置き換えてください。これにより、Aspose が生成した PDF を保存する場所と、Excel ファイルを検索する場所が決まります。

## ステップ2: サンプルExcelファイルを読み込む

次に、グラフを含むExcelファイルを読み込みます。手順は以下のとおりです。

```csharp
//グラフを含むサンプル Excel ファイルを読み込みます。
Workbook wb = new Workbook(sourceDir + "sampleCreateChartPDFWithDesiredPageSize.xlsx");
```

その `Workbook` クラスはExcelドキュメントの操作の中心となります。パスがExcelファイルへの正しいパスを指していることを確認してください。ここでエラーが発生すると、残りのコードが実行されなくなります。

## ステップ3: 最初のワークシートにアクセスする

ワークブックが読み込まれたら、次のステップは、目的のグラフを含むワークシートにアクセスすることです。

```csharp
//最初のワークシートにアクセスします。
Worksheet ws = wb.Worksheets[0];
```

Aspose.Cellsでは、ワークシートは0から始まるインデックスが付けられるため、 `Worksheets[0]` 最初のシートを参照します。

## ステップ4：最初のチャートにアクセスする

それでは、PDFにエクスポートしたいグラフにアクセスしてみましょう。この手順では、ワークシートに少なくとも1つのグラフが含まれていることを前提としています。

```csharp
//ワークシート内の最初のグラフにアクセスします。
Chart ch = ws.Charts[0];
```

繰り返しますが、これはワークシートの最初のグラフにアクセスします。ワークシートの構造がこのアプローチに適していることを確認してください。

## ステップ5：希望のページサイズでPDFを作成する

最後に、指定したページサイズでチャートからPDFを作成します。このコードはすべてこの魔法の行で実行されます。

```csharp
//希望するページ サイズでチャートの PDF を作成します。
ch.ToPdf(outputDir + "outputCreateChartPDFWithDesiredPageSize.pdf", 7, 7, PageLayoutAlignmentType.Center, PageLayoutAlignmentType.Center);
```

このコードでは:
- PDF は、前に指定した出力ディレクトリに保存されます。
- 数字 `7, 7` それぞれ、希望するページ サイズの幅と高さを表します。
- PageLayoutAlignmentType.Center は、グラフがページの中央に配置されることを保証します。

## ステップ6: 確認メッセージ

すべてがスムーズに進んだことを自分自身 (および他の人) に知らせるために、コードの最後に確認メッセージを含めます。

```csharp
Console.WriteLine("CreateChartPDFWithDesiredPageSize executed successfully.");
```

プロセスが完了すると、このメッセージがコンソール ウィンドウに表示され、PDF が問題なく作成されたことが通知されます。

## 結論

おめでとうございます！Aspose.Cells for .NET を活用して、Excel ファイル内のグラフから PDF を作成する方法を習得しました。この強力なライブラリは、Excel ドキュメントの操作とデータの視覚的表現の生成プロセスを効率化し、手作業による書式設定にかかる時間を節約します。Aspose.Cells には PDF 生成以外にもさまざまな機能が用意されているので、ぜひお試しください。プロジェクトをさらに強化できる可能性が無限に広がります！

## よくある質問

### Aspose.Cells for .NET は何に使用されますか?  
Aspose.Cells for .NET は、.NET アプリケーションでプログラムによって Excel ドキュメントを作成、編集、変換するために使用されます。

### Aspose.Cells を無料で使用できますか?  
はい、Aspose.Cellsは [無料トライアル](https://releases.aspose.com/) 評価目的のため。

### 試用期間を最初の期間を超えて延長する方法はありますか?  
申請することができます [一時ライセンス](https://purchase.aspose.com/temporary-license/) 拡張テスト用。

### 問題が発生した場合や質問がある場合はどうすればよいですか?  
Asposeコミュニティからサポートを受けることができます。 [サポートフォーラム](https://forum。aspose.com/c/cells/9).

### Aspose.Cells を購入するにはどうすればよいですか?  
Aspose.Cellsは以下から購入できます。 [購入ページ](https://purchase。aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}