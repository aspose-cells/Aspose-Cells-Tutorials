---
"description": "Aspose.Cells for .NET を使用して、Excel で図形を前面または背面に移動する方法を学びます。このガイドでは、ヒントを交えたステップバイステップのチュートリアルを提供しています。"
"linktitle": "Excel で図形を前面または背面に移動"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": "Excel で図形を前面または背面に移動"
"url": "/ja/net/excel-shape-text-modifications/send-shape-front-back-excel/"
"weight": 16
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel で図形を前面または背面に移動

## 導入
Excelファイルで作業していると、スプレッドシート内の視覚要素をより細かく制御する必要に迫られることがあります。画像やグラフィックなどの図形は、データのプレゼンテーション効果を高めることができます。しかし、これらの図形が重なったり、順序を変更したりする必要がある場合はどうすればよいでしょうか？ここでAspose.Cells for .NETが威力を発揮します。このチュートリアルでは、Excelワークシート内の図形を操作する手順、特に図形を他の図形の前面または背面に移動する方法を詳しく説明します。Excelをもっと使いこなしたい方は、ぜひ実践してみてください！
## 前提条件
始める前に、いくつか準備しておく必要があります。
1. Aspose.Cellsライブラリのインストール：.NET用のAspose.Cellsライブラリがインストールされていることを確認してください。 [ここ](https://releases。aspose.com/cells/net/).
2. 開発環境: Visual Studio などの .NET サポートを備えた開発環境が設定されていることを確認します。
3. C# の基礎知識: C# プログラミングに精通していると、コード スニペットをよりよく理解できるようになります。
さあ、前提条件リストのボックスをすべてチェックしましたか？素晴らしい！それでは、楽しい部分、つまりコードを書いてみましょう！
## パッケージのインポート
実際のコーディングに入る前に、必要なパッケージをインポートしましょう。C#ファイルの先頭に次のusingディレクティブを追加するだけです。
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
これらの名前空間は、Excel ファイルと図形を操作するために使用するクラスとメソッドが含まれているため、非常に重要です。
## ステップ1: ファイルパスを定義する
この最初のステップでは、ソースディレクトリと出力ディレクトリを設定する必要があります。これはExcelファイルが保存されている場所であり、変更後のファイルを保存する場所です。
```csharp
//ソースディレクトリ
string sourceDir = "Your Document Directory";
//出力ディレクトリ
string outputDir = "Your Document Directory";
```
交換する `"Your Document Directory"` Excel ファイルが保存されている実際のパスを入力します。
## ステップ2: ワークブックを読み込む
ディレクトリが設定されたので、操作する図形が含まれているワークブック (Excel ファイル) を読み込みます。
```csharp
//ソースExcelファイルを読み込む
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
このコード行は新しい `Workbook` オブジェクトを作成し、指定された Excel ファイルをメモリに読み込んで操作できるようにします。
## ステップ3: ワークシートにアクセスする 
次に、図形が格納されている特定のワークシートにアクセスする必要があります。この例では、最初のワークシートを使用します。
```csharp
//最初のワークシートにアクセスする
Worksheet ws = wb.Worksheets[0];
```
参照することで `Worksheets[0]`ワークブックの最初のシートをターゲットにしています。図形が別のシートにある場合は、それに応じてインデックスを調整してください。
## ステップ4: 図形にアクセスする
ワークシートへのアクセスが準備できたら、興味のある図形を取得しましょう。この例では、最初の図形と 4 番目の図形にアクセスします。
```csharp
//1番目と4番目の図形にアクセスする
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
これらの行は、インデックスに基づいてワークシートから特定の図形を取得します。
## ステップ5: 図形のZオーダー位置を印刷する
図形を移動する前に、現在のZオーダーの位置を出力しましょう。これにより、変更を加える前に図形の位置を追跡できます。
```csharp
//図形のZオーダー位置を印刷する
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
電話をかける `ZOrderPosition`、各図形が描画順序のどこに位置しているかを確認できます。
## ステップ6: 最初の図形を最前面に送る
さあ、いよいよ実行です！最初の図形を Z オーダーの最前面に送りましょう。
```csharp
//この図形を最前面に送る
sh1.ToFrontOrBack(2);
```
通過することで `2` に `ToFrontOrBack`では、Aspose.Cells にこの図形を最前面に移動するように指示します。 
## ステップ7: 2番目の図形のZオーダー位置を印刷する
番目の図形を後ろに送る前に、それがどこに配置されているかを確認しましょう。
```csharp
//図形のZオーダー位置を印刷する
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
これにより、変更を加える前に 4 番目の図形の位置を把握できるようになります。
## ステップ8: 4番目の図形を背面へ移動
最後に、4 番目の図形を Z オーダー スタックの後ろに送ります。
```csharp
//この図形を背面へ移動
sh4.ToFrontOrBack(-2);
```
使用 `-2` パラメータにより図形がスタックの背面に送られ、他の図形やテキストを妨げないようにします。
## ステップ9: ワークブックを保存する 
最後の手順は、新しく配置された図形を含むワークブックを保存することです。
```csharp
//出力されたExcelファイルを保存する
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
このコマンドは、変更されたワークブックを指定された出力ディレクトリに保存します。
## ステップ10: 確認メッセージ
最後に、タスクが正常に完了したことを知らせる簡単な確認を提供しましょう。
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
これでチュートリアルのコードは完了です。
## 結論
Aspose.Cells for .NET を使った Excel の図形操作は、シンプルでありながら強力です。このガイドに従うことで、図形を簡単に前面または背面に移動できるようになり、Excel プレゼンテーションをより適切にコントロールできるようになります。これらのツールを活用すれば、スプレッドシートの視覚的な魅力を高める準備が整います。
## よくある質問
### Aspose.Cells にはどのようなプログラミング言語が必要ですか?  
Aspose.Cells を操作するには、C# または .NET でサポートされている言語を使用する必要があります。
### Aspose.Cells を無料で試すことはできますか?  
はい、Aspose.Cellsの無料トライアルから始めることができます。 [ここ](https://releases。aspose.com/).
### Excel ではどのような図形を操作できますか?  
長方形、円、線、画像など、さまざまな図形を操作できます。
### Aspose.Cells のサポートを受けるにはどうすればよいですか?  
サポートや質問がある場合はコミュニティフォーラムをご覧ください。 [ここ](https://forum。aspose.com/c/cells/9).
### Aspose.Cells に利用できる一時ライセンスはありますか?  
はい、一時ライセンスを申請できます [ここ](https://purchase。aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}