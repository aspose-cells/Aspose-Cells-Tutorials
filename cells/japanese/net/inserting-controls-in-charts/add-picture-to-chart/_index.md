---
title: グラフに画像を追加
linktitle: グラフに画像を追加
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して Excel グラフに画像を簡単に追加する方法を学びます。わずか数ステップでグラフやプレゼンテーションを強化できます。
weight: 11
url: /ja/net/inserting-controls-in-charts/add-picture-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# グラフに画像を追加

## 導入

個性のない退屈なグラフにうんざりしていませんか? 画像を追加して Excel のビジュアルに彩りを添える方法を知りたいですか? いいえ、そんなことはありません! このチュートリアルでは、Aspose.Cells for .NET の世界に飛び込み、Excel のグラフに画像を追加する方法を学びます。では、お気に入りのコーヒーを片手に、始めましょう!

## 前提条件

コーディングの詳細に入る前に、スムーズに進めるために必要な前提条件がいくつかあります。

- Visual Studio: ここで .NET コードを記述して実行します。インストールされていることを確認してください。
-  Aspose.Cells for .NET: Excelファイルを操作するにはこのライブラリが必要です。[ここからダウンロード](https://releases.aspose.com/cells/net/).
- C# の基本的な理解: コードの説明をしますが、C# の基本を理解しておくと、よりわかりやすくなります。

### インストール手順

1. Aspose.Cells をインストールします。NuGet パッケージ マネージャーを使用して、Visual Studio プロジェクトに Aspose.Cells を追加できます。これを行うには、[ツール] > [NuGet パッケージ マネージャー] > [ソリューションの NuGet パッケージの管理] に移動し、「Aspose.Cells」を検索します。[インストール] をクリックします。
2. プロジェクトの設定: Visual Studio で新しい C# コンソール アプリケーション プロジェクトを作成します。

## パッケージのインポート

すべての設定が完了したら、次のステップは必要なパッケージをプロジェクトにインポートすることです。手順は次のとおりです。

### 必要な名前空間をインポートする

C# コード ファイルの先頭で、次の名前空間をインポートする必要があります。

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
using System.IO;
```

これはプログラムに「Aspose.Cells のこれらの優れた機能を使用します」と伝えます。

前提条件が整ったので、プロセスを細かいステップに分解してみましょう。 

## ステップ1: ディレクトリを定義する

まず最初に、入力ファイルと出力ファイルのパスを設定する必要があります。既存の Excel ファイルの場所と変更したファイルを保存する場所を知る必要があるため、この手順は非常に重要です。

```csharp
//ソースディレクトリ
string sourceDir = "Your Document Directory/";

//出力ディレクトリ
string outputDir = "Your Output Directory/";
```

交換する`Your Document Directory`そして`Your Output Directory`コンピュータ上の実際のパスを使用します。 

## ステップ2: 既存のワークブックを読み込む

ここで、グラフに画像を追加する既存の Excel ファイルを読み込みます。

```csharp
//既存のファイルを開きます。
Workbook workbook = new Workbook(sourceDir + "sampleAddingPictureInChart.xls");
```

このコードはワークブックを開き、編集できる状態にします。

## ステップ3: 画像ストリームを準備する

画像を追加する前に、グラフに挿入する画像を読み取る必要があります。 

```csharp
//ストリームに画像ファイルを取得します。
FileStream stream = new FileStream(sourceDir + "sampleAddingPictureInChart.png", FileMode.Open, FileAccess.Read);
```

指定されたディレクトリに画像が保存されていることを確認してください。

## ステップ4: チャートをターゲットにする

次に、画像を追加するグラフを指定しましょう。この例では、最初のワークシートの最初のグラフを対象とします。

```csharp
// 2 枚目のシートでデザイナー チャートを取得します。
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

インデックスを適宜変更することで、任意のワークシートにアクセスできます。

## ステップ5: チャートに画像を追加する

グラフを選択したら、画像を追加します。 

```csharp
//グラフに新しい画像を追加します。
Aspose.Cells.Drawing.Picture pic0 = chart.Shapes.AddPictureInChart(50, 50, stream, 200, 200);
```

ここ、`50`そして`50`画像を配置するX座標とY座標であり、`200`画像の幅と高さです。

## ステップ6: 画像の線の書式をカスタマイズする

写真にセンスを加えたいと思いませんか? 境界線をカスタマイズできます! やり方は次のとおりです:

```csharp
//画像の線形式タイプを取得します。
Aspose.Cells.Drawing.LineFormat lineformat = pic0.Line; 

//ダッシュスタイルを設定します。
lineformat.DashStyle = MsoLineDashStyle.Solid;

//線の太さを設定します。
lineformat.Weight = 4;    
```

このスニペットを使用すると、境界線の外観と太さを選択できます。プレゼンテーションに合ったスタイルを選択してください。

## ステップ7: 変更したワークブックを保存する

大変な作業が終わったら、次のコード行を実行して変更を保存しましょう。

```csharp
// Excel ファイルを保存します。
workbook.Save(outputDir + "outputAddingPictureInChart.xls");
```

これで、画像がチャートに正常に統合され、出力ファイルを表示できるようになりました。

## ステップ8: 成功を示す

最後に、操作が成功したことを確認するための簡単なメッセージを追加できます。

```csharp
Console.WriteLine("AddingPictureInChart executed successfully.");
```

## 結論

このチュートリアルでは、Aspose.Cells for .NET を使用して画像を追加し、Excel グラフに個性を少し加える方法について説明しました。いくつかの簡単な手順を実行するだけで、プレゼンテーションを平凡なものから思い出に残るものにすることができます。さあ、何を待っているのですか? ぜひ試して、グラフを輝かせてください!

## よくある質問

### 1 つのグラフに複数の画像を追加できますか?
はい！`AddPictureInChart`このメソッドを複数回実行して、必要な数だけ写真を追加します。

### Aspose.Cells はどのような画像形式をサポートしていますか?
Aspose.Cells は、PNG、JPEG、BMP、GIF など、さまざまな画像形式をサポートしています。

### 写真の位置をカスタマイズできますか？
確かに！XとY座標は`AddPictureInChart`正確な位置決めを可能にする方法。

### Aspose.Cells は無料で使用できますか?
Aspose.Cellsは無料トライアルを提供していますが、フル機能を使用するにはライセンスが必要です。価格については[ここ](https://purchase.aspose.com/buy).

### もっと多くの例はどこで見つかりますか?
チェックしてください[Aspose.Cells ドキュメント](https://reference.aspose.com/cells/net/)より詳細な例と機能については、こちらをご覧ください。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
