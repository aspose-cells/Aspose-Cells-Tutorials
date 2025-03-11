---
title: Excel で図形に合わせてテキストを回転する
linktitle: Excel で図形に合わせてテキストを回転する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して、Excel で図形を含むテキストを回転する方法を学びます。このステップ バイ ステップ ガイドに従って、完璧な Excel プレゼンテーションを実現してください。
weight: 12
url: /ja/net/excel-shape-text-modifications/rotate-text-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel で図形に合わせてテキストを回転する

## 導入
Excel の世界では、視覚的な表現はデータ自体と同じくらい重要です。レポートを作成する場合でも、動的なダッシュボードを設計する場合でも、情報のレイアウト方法は、その読みやすさと全体的な外観に大きく影響します。テキストを回転させて図形に合わせてスタイリッシュに揃えたいと思ったことはありませんか? 幸運です! このチュートリアルでは、Aspose.Cells for .NET を使用して図形に合わせてテキストを回転する方法について詳しく説明します。これにより、スプレッドシートが情報を伝えるだけでなく、印象に残るものになります。
## 前提条件
始める前に、必要なものがすべて揃っていることを確認しましょう。
1. Visual Studio: コードを記述する場所として、Visual Studio がマシンにインストールされていることを確認してください。
2.  Aspose.Cells for .NET: Aspose.Cellsライブラリが必要です。[最新バージョンはこちらからダウンロードしてください](https://releases.aspose.com/cells/net/)または無料でお試しいただけます[無料トライアル](https://releases.aspose.com/).
3. C# の基礎知識: C# と .NET 環境に精通していると役立ちますが、すべての手順をガイドします。
4.  Excelファイル: サンプルのExcelファイルです。`sampleRotateTextWithShapeInsideWorksheet.xlsx`は、コードをテストするために必要です。このファイルは、簡単にアクセスできるディレクトリに配置する必要があります。
準備はできましたか? 素晴らしい! 楽しい部分に飛び込みましょう。
## パッケージのインポート
まず、プロジェクトに必要なパッケージをインポートする必要があります。手順は次のとおりです。
### 新しいプロジェクトを作成する
1. Visual Studio を開きます。
2. 「新しいプロジェクトを作成する」を選択します。
3. 「コンソール アプリ」を選択し、優先するプログラミング言語として C# を選択します。
### Aspose.Cellsをインストールする
それでは、Aspose.Cells をプロジェクトに追加しましょう。これは NuGet パッケージ マネージャーを使用して実行できます。
1. 上部メニューの「ツール」を開きます。
2. 「NuGet パッケージ マネージャー」を選択し、「ソリューションの NuGet パッケージの管理」を選択します。
3. 「Aspose.Cells」を検索します。
4. 「インストール」をクリックしてプロジェクトに追加します。
### Usingディレクティブの追加
メインの C# ファイルの先頭に、次のディレクティブを追加する必要があります。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
これでコーディングを始める準備が整いました。
プロセスを簡単に理解できるステップに分解してみましょう。Excel ファイルで図形を使用してテキストを回転する方法は次のとおりです。
## ステップ1: ディレクトリパスを設定する
まず、Excel ファイルを保存するソース ディレクトリと出力ディレクトリを設定する必要があります。手順は次のとおりです。
```csharp
//ソースディレクトリ
string sourceDir = "Your Document Directory"; //ドキュメントディレクトリを設定する
//出力ディレクトリ
string outputDir = "Your Document Directory"; //出力ディレクトリを設定する
```
交換する`"Your Document Directory"`実際の経路で`sampleRotateTextWithShapeInsideWorksheet.xlsx`ファイルが見つかります。
## ステップ2: サンプルExcelファイルを読み込む
次に、サンプル Excel ファイルをロードします。既存のデータを操作する必要があるため、これは非常に重要です。
```csharp
//サンプル Excel ファイルを読み込みます。
Workbook wb = new Workbook(sourceDir + "sampleRotateTextWithShapeInsideWorksheet.xlsx");
```
## ステップ3: ワークシートにアクセスする
ファイルが読み込まれたら、変更する特定のワークシートにアクセスする必要があります。この場合、最初のワークシートです。
```csharp
//最初のワークシートにアクセスします。
Worksheet ws = wb.Worksheets[0];
```
## ステップ4: セルを変更する
次に、特定のセルを変更してメッセージを表示します。この例では、セル B4 を使用します。
```csharp
//セル B4 にアクセスし、その中にメッセージを追加します。
Cell b4 = ws.Cells["B4"];
b4.PutValue("Text is not rotating with shape because RotateTextWithShape is false.");
```
このステップではコミュニケーションが重要であり、このシートを開いた人が何を調整しているのかを確実に理解できるようにします。
## ステップ5: 最初の図形にアクセスする
テキストを回転するには、操作する図形が必要です。ここでは、ワークシートの最初の図形にアクセスします。
```csharp
//最初の図形にアクセスします。
Shape sh = ws.Shapes[0];
```
## ステップ6: 図形のテキスト配置を調整する
ここで魔法が起こります。図形のテキスト配置プロパティを調整します。
```csharp
//図形のテキストの配置にアクセスします。
Aspose.Cells.Drawing.Texts.ShapeTextAlignment shapeTextAlignment = sh.TextBody.TextAlignment;
//RotateTextWithShape を false に設定して、テキストを図形とともに回転させないようにします。
shapeTextAlignment.RotateTextWithShape = false;
```
設定により`RotateTextWithShape` false に設定すると、テキストが垂直のままになり、図形とともに回転しないので、すべてが整然と整理された状態になります。
## ステップ7: 出力Excelファイルを保存する
最後に、変更内容を新しい Excel ファイルに保存します。これにより、編集内容が失われず、出力が整頓されます。
```csharp
//出力された Excel ファイルを保存します。
wb.Save(outputDir + "outputRotateTextWithShapeInsideWorksheet.xlsx");
```
これで完了です。セル B4 のテキストと図形に加えられた調整を含む出力ファイルが保存されました。
## ステップ8: コードを実行する
あなたの`Main`メソッドを使用して、上記のコード スニペットをすべてラップし、プロジェクトを実行します。出力ファイルに反映される変更を確認してください。
```csharp
Console.WriteLine("RotateTextWithShapeInsideWorksheet executed successfully.");
```
## 結論
Aspose.Cells for .NET を使用して Excel で図形付きのテキストを回転させる作業は、最初は複雑なプロセスのように思えるかもしれませんが、分解してみると非常に簡単です。これらの簡単な手順に従うことで、スプレッドシートをよりプロフェッショナルで視覚的に魅力的なものにカスタマイズできます。これで、クライアントのために行う場合でも、個人のプロジェクトのために行う場合でも、誰もがあなたの仕事の質を絶賛するでしょう。
## よくある質問
### Aspose.Cells を無料で使用できますか?
はい！[無料トライアル](https://releases.aspose.com/)ライブラリを試してみる。
### Aspose.Cells はどのバージョンの Excel をサポートしていますか?
Aspose.Cells は、XLS、XLSX、CSV など、さまざまな Excel 形式をサポートしています。
### 古いバージョンの Excel で図形付きのテキストを回転することは可能ですか?
はい、この機能は Aspose.Cells でサポートされている古い形式に適用できます。
### Aspose.Cells に関する詳細なドキュメントはどこで入手できますか?
包括的な[ドキュメント](https://reference.aspose.com/cells/net/)詳しい情報についてはこちらをご覧ください。
### Aspose.Cells のサポートを受けるにはどうすればよいですか?
サポートをご希望の場合は、[Aspose フォーラム](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
