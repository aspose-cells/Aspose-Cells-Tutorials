---
"description": "Aspose.Cells for .NET を使用して、Excel で図形を含むテキストを回転させる方法を学びましょう。このステップバイステップのガイドに従って、完璧な Excel プレゼンテーションを作成しましょう。"
"linktitle": "Excelで図形に合わせてテキストを回転する"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": "Excelで図形に合わせてテキストを回転する"
"url": "/ja/net/excel-shape-text-modifications/rotate-text-shape-excel/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excelで図形に合わせてテキストを回転する

## 導入
Excelの世界では、視覚的な表現はデータそのものと同じくらい重要です。レポートを作成する場合でも、動的なダッシュボードをデザインする場合でも、情報のレイアウト方法は読みやすさや全体的な見た目に大きく影響します。テキストを回転させて図形に合わせてスタイリッシュに整列させたいと思ったことはありませんか？まさにその通りです！このチュートリアルでは、Aspose.Cells for .NETを使って図形に合わせてテキストを回転させる方法を詳しく説明します。情報を伝えるだけでなく、印象的なスプレッドシートを作成しましょう。
## 前提条件
始める前に、必要なものがすべて揃っていることを確認しましょう。
1. Visual Studio: コードを記述する場所として、Visual Studio がマシンにインストールされていることを確認してください。
2. Aspose.Cells for .NET: Aspose.Cellsライブラリが必要です。 [最新バージョンはこちらからダウンロードしてください](https://releases.aspose.com/cells/net/) または無料でお試しください [無料トライアル](https://releases。aspose.com/).
3. C# の基礎知識: C# と .NET 環境の知識があると役立ちますが、手順ごとにガイドします。
4. Excelファイル: サンプルのExcelファイルです。 `sampleRotateTextWithShapeInsideWorksheet.xlsx`はコードのテストに必要です。このファイルは簡単にアクセスできるディレクトリに置いてください。
準備はできましたか？素晴らしい！それでは、楽しいパートに進みましょう。
## パッケージのインポート
作業を開始するには、必要なパッケージをプロジェクトにインポートする必要があります。手順は以下のとおりです。
### 新しいプロジェクトを作成する
1. Visual Studio を開きます。
2. 「新しいプロジェクトを作成」を選択します。
3. 「コンソール アプリ」を選択し、優先するプログラミング言語として C# を選択します。
### Aspose.Cellsをインストールする
それでは、Aspose.Cellsをプロジェクトに追加しましょう。NuGetパッケージマネージャーを使って追加できます。
1. 上部メニューの「ツール」を開きます。
2. 「NuGet パッケージ マネージャー」を選択し、「ソリューションの NuGet パッケージの管理」を選択します。
3. 「Aspose.Cells」を検索します。
4. 「インストール」をクリックしてプロジェクトに追加します。
### Usingディレクティブを追加する
メインの C# ファイルの先頭に、次のディレクティブを追加する必要があります。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
これでコーディングを始める準備が整いました。
プロセスを分かりやすいステップに分解してみましょう。Excelファイルで図形を含むテキストを回転させる方法は次のとおりです。
## ステップ1: ディレクトリパスを設定する
まず、Excelファイルを保存するソースディレクトリと出力ディレクトリを設定する必要があります。手順は以下のとおりです。
```csharp
//ソースディレクトリ
string sourceDir = "Your Document Directory"; // ドキュメントディレクトリを設定する
//出力ディレクトリ
string outputDir = "Your Document Directory"; // 出力ディレクトリを設定する
```
交換する `"Your Document Directory"` 実際のパスで `sampleRotateTextWithShapeInsideWorksheet.xlsx` ファイルが見つかります。
## ステップ2: サンプルExcelファイルを読み込む
それでは、サンプルのExcelファイルを読み込みましょう。既存のデータを操作する必要があるため、これは非常に重要です。
```csharp
//サンプル Excel ファイルを読み込みます。
Workbook wb = new Workbook(sourceDir + "sampleRotateTextWithShapeInsideWorksheet.xlsx");
```
## ステップ3: ワークシートにアクセスする
ファイルが読み込まれたら、変更したい特定のワークシートにアクセスする必要があります。今回の場合は、最初のワークシートです。
```csharp
//最初のワークシートにアクセスします。
Worksheet ws = wb.Worksheets[0];
```
## ステップ4: セルを変更する
次に、特定のセルを変更してメッセージを表示します。この例では、セルB4を使用します。
```csharp
//セル B4 にアクセスし、その中にメッセージを追加します。
Cell b4 = ws.Cells["B4"];
b4.PutValue("Text is not rotating with shape because RotateTextWithShape is false.");
```
このステップはコミュニケーションが重要です。つまり、このシートを開いた人が何を調整しているのかを確実に理解できるようにします。
## ステップ5: 最初の図形にアクセスする
テキストを回転するには、操作対象となる図形が必要です。ここでは、ワークシートの最初の図形にアクセスします。
```csharp
//最初の図形にアクセスします。
Shape sh = ws.Shapes[0];
```
## ステップ6: 図形のテキストの配置を調整する
ここで魔法が起こります。図形のテキスト配置プロパティを調整します。
```csharp
//図形のテキストの配置にアクセスします。
Aspose.Cells.Drawing.Texts.ShapeTextAlignment shapeTextAlignment = sh.TextBody.TextAlignment;
//RotateTextWithShape を false に設定して、図形とともにテキストを回転させないようにします。
shapeTextAlignment.RotateTextWithShape = false;
```
設定により `RotateTextWithShape` false に設定すると、テキストは直立したまま図形とともに回転せず、すべてが整然と整理された状態になります。
## ステップ7: 出力Excelファイルを保存する
最後に、変更内容を新しいExcelファイルに保存しましょう。これにより、編集内容が失われることなく、出力結果が整頓されます。
```csharp
//出力された Excel ファイルを保存します。
wb.Save(outputDir + "outputRotateTextWithShapeInsideWorksheet.xlsx");
```
これで完了です。セル B4 のテキストと図形に加えられた調整を含む出力ファイルが保存されました。
## ステップ8: コードを実行する
あなたの `Main` メソッドで上記のコードスニペットをすべてラップし、プロジェクトを実行します。出力ファイルに変更が反映されていることを確認してください。
```csharp
Console.WriteLine("RotateTextWithShapeInsideWorksheet executed successfully.");
```
## 結論
Aspose.Cells for .NET を使ってExcelで図形付きのテキストを回転させる作業は、一見複雑な作業に思えるかもしれませんが、実際にやってみると非常に簡単です。これらの簡単な手順に従うだけで、スプレッドシートをよりプロフェッショナルで魅力的なものにカスタマイズできます。クライアント向けでも、個人プロジェクトでも、きっと誰もがあなたの仕事の質に感激してくれるでしょう！
## よくある質問
### Aspose.Cells を無料で使用できますか?
はい！ [無料トライアル](https://releases.aspose.com/) ライブラリを試してみましょう。
### Aspose.Cells はどのバージョンの Excel をサポートしていますか?
Aspose.Cells は、XLS、XLSX、CSV など、さまざまな Excel 形式をサポートしています。
### 古いバージョンの Excel で図形付きのテキストを回転することは可能ですか?
はい、この機能は Aspose.Cells でサポートされている古い形式にも適用できます。
### Aspose.Cells に関する詳細なドキュメントはどこで入手できますか?
包括的な [ドキュメント](https://reference.aspose.com/cells/net/) さらに詳しい情報をご覧ください。
### Aspose.Cells のサポートを受けるにはどうすればよいですか?
サポートをご希望の場合は、 [Asposeフォーラム](https://forum。aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}