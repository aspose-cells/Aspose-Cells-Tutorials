---
title: グラフのデータラベルの形状タイプを設定する
linktitle: グラフのデータラベルの形状タイプを設定する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して、カスタマイズされたデータ ラベル図形で Excel グラフを強化します。このステップ バイ ステップ ガイドに従って、データのプレゼンテーションを向上させます。
weight: 14
url: /ja/net/advanced-chart-operations/set-shape-type-of-data-labels-of-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# グラフのデータラベルの形状タイプを設定する

## 導入

データ視覚化の世界では、グラフは複雑な情報をわかりやすい方法で提示するための頼りになる方法です。ただし、すべてのデータ ラベルが同じように作成されるわけではありません。ラベルを目立たせる必要がある場合、さまざまな図形を使用すると大きな違いが生まれます。Excel グラフのデータ ラベルをカスタム図形で強化したい場合は、ここが最適な場所です。このガイドでは、Aspose.Cells for .NET を使用してグラフのデータ ラベルの図形の種類を設定する方法について説明します。さっそく見ていきましょう。

## 前提条件

コーディングを始める前に、すべてが正しく設定されていることを確認しましょう。必要なものは次のとおりです。

1.  Aspose.Cells for .NET: まだダウンロードしていない場合は、[Aspose ウェブサイト](https://releases.aspose.com/cells/net/)このライブラリを使用すると、Excel ドキュメントに対するあらゆる種類の操作が可能になります。
2. Visual Studio: .NET アプリケーションを作成して実行するには、システムにこれをインストールする必要があります。プロジェクトのニーズに応じて、.NET Framework または .NET Core をサポートするバージョンであることを確認してください。
3. C# の基本的な理解: 基本的なプログラミング概念と C# 構文に精通していると、コード スニペットをより深く理解するのに役立ちます。
4. Excel ファイル: 作業に使用するサンプルの Excel ワークブックも必要です。独自のワークブックを作成することも、既存のワークブックを使用することもできます。

前提条件が揃ったので、すぐに始めましょう。

## パッケージのインポート

コーディングを始める前に、関連する Aspose.Cells 名前空間をインポートする必要があります。これにより、ライブラリが提供する豊富な機能にアクセスできるようになります。手順は次のとおりです。

### Aspose.Cells をインポートする

Visual Studio プロジェクトを開き、C# ファイルの先頭に次の using ディレクティブを追加します。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
```

これらの名前空間を使用すると、ワークブック、ワークシート、グラフを簡単に作成および操作できるようになります。

準備がすべて整ったので、コーディングの部分に取り掛かりましょう。わかりやすくするために、ステップごとに詳しく説明します。

## ステップ1: ディレクトリを定義する

まず最初に、ファイルの保存場所（ソース ファイルと、変更したファイルを保存する保存先フォルダーの両方）を定義しましょう。

```csharp
//ソースディレクトリ
string sourceDir = "Your Document Directory";

//出力ディレクトリ
string outputDir = "Your Output Directory";
```

交換する`"Your Document Directory"`そして`"Your Output Directory"`マシン上の実際のパスを使用します。

## ステップ2: ソースExcelファイルを読み込む

次に、作業したい Excel ファイルを読み込む必要があります。ここから魔法が始まります。

```csharp
//ソースExcelファイルを読み込む
Workbook wb = new Workbook(sourceDir + "sampleSetShapeTypeOfDataLabelsOfChart.xlsx");
```

この行は新しい`Workbook`オブジェクトを作成し、既存のファイルを指定します。ファイル パスが正しいことを確認してください。

## ステップ3: 最初のワークシートにアクセスする

ワークブックが作成されたので、カスタマイズするグラフが含まれているワークシートにアクセスする必要があります。

```csharp
//最初のワークシートにアクセスする
Worksheet ws = wb.Worksheets[0];
```

ここでは、最初のワークシート（インデックス）にアクセスしています`0`）。グラフが別のシートにある場合は、インデックスを調整します。

## ステップ4: 最初のチャートにアクセスする

ワークシートができたら、グラフにアクセスします。各ワークシートには複数のグラフを含めることができますが、ここでは簡単にするために最初のグラフのみを使用します。

```csharp
//最初のチャートにアクセス
Chart ch = ws.Charts[0];
```

繰り返しますが、希望するチャートが最初のチャートでない場合は、それに応じてインデックスを変更してください。

## ステップ5: チャートシリーズにアクセスする

グラフにアクセスできるようになりました。データ ラベルを変更するには、さらに深く掘り下げる必要があります。シリーズはグラフ内のデータ ポイントを表します。

```csharp
//最初のシリーズにアクセス
Series srs = ch.NSeries[0];
```

ここでは、通常、変更する可能性のあるラベルが含まれる最初のシリーズをターゲットにしています。

## ステップ6: データラベルの形状の種類を設定する

さて、重要な部分です。データ ラベルの図形の種類を設定しましょう。Aspose.Cells はさまざまな図形をサポートしていますが、この例では、楽しいタッチを加えるために吹き出しの楕円形を選択します。

```csharp
//データラベルの形状タイプを設定します（吹き出し、楕円など）。
srs.DataLabels.ShapeType = DataLabelShapeType.WedgeEllipseCallout;
```

さまざまな形状のタイプを自由に試してみてください。`DataLabelShapeType.WedgeEllipseCallout`その他の利用可能なオプションへ！

## ステップ7: 出力Excelファイルを保存する

大変な作業が終わりました。次は作業内容を保存します。変更したデータ ラベルの図形を Excel ファイルに戻しましょう。

```csharp
//出力されたExcelファイルを保存する
wb.Save(outputDir + "outputSetShapeTypeOfDataLabelsOfChart.xlsx");
```

これにより、変更されたワークブックが指定した出力ディレクトリに保存されます。

## ステップ8: 実行して確認する

最後に、プログラムを実行します。実行後、すべてがスムーズに実行されたことを確認するメッセージが表示されます。

```csharp
Console.WriteLine("SetShapeTypeOfDataLabelsOfChart executed successfully.");
```

メッセージが表示されたら、出力ディレクトリに移動して新しい Excel ファイルを確認します。ファイルを開いて、新しく形作られたデータ ラベルで創造性を発揮してください。

## 結論

これで、Aspose.Cells for .NET を使用して Excel グラフのデータ ラベルを強化するためのわかりやすいガイドができました。図形の種類をカスタマイズすると、グラフの見た目が魅力的になるだけでなく、データ ストーリーをより効果的に伝えることにも役立ちます。データの視覚化は、明瞭さとエンゲージメントが重要だということを覚えておいてください。さまざまな図形やスタイルをためらわずに試してみてください。結局のところ、データは最高のプレゼンテーションに値します。

## よくある質問

### Aspose.Cells とは何ですか?  
Aspose.Cells は、開発者が Excel ファイルをプログラムで操作できるようにする強力な .NET ライブラリです。

### Aspose を使用して Excel グラフのさまざまな側面を変更できますか?  
もちろんです! Aspose.Cells は、データ シリーズ、ラベル、スタイルなど、グラフを変更するための広範な機能を提供します。

### Aspose.Cells ではどのようなプログラミング言語を使用できますか?  
この記事では .NET に焦点を当てていますが、Aspose.Cells は REST API を介して Java、PHP、Python などもサポートしています。

### Aspose.Cells には料金がかかりますか?  
Aspose.Cellsは商用製品ですが、無料トライアルも提供されており、[ここ](https://releases.aspose.com/).

### Aspose.Cells で問題が発生した場合、どこでサポートを受けることができますか?  
何か問題が起こった場合は、[サポートフォーラム](https://forum.aspose.com/c/cells/9)専門家からの支援を得るための素晴らしいリソースです。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
