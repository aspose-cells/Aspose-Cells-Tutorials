---
title: 接続ポイントで円弧コントロールを追加する
linktitle: 接続ポイントで円弧コントロールを追加する
second_title: Aspose.Cells .NET Excel 処理 API
description: この詳細なガイドでは、Aspose.Cells for .NET を使用して接続ポイントを持つ円弧コントロールを追加する方法について説明します。
weight: 27
url: /ja/net/excel-shapes-controls/add-arc-control-with-connection-points/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 接続ポイントで円弧コントロールを追加する

## 導入
視覚的に魅力的な Excel レポートを作成する場合、イラストは重要な役割を果たします。財務レポートを作成する場合でも、プロジェクトの内訳を作成する場合でも、円弧などの図形を使用すると、データのプレゼンテーションに深みと明瞭さを加えることができます。今日は、Aspose.Cells for .NET を使用して、Excel ワークシートに接続ポイントを持つ円弧コントロールを追加する方法について詳しく説明します。スプレッドシートに彩りを添えたり、データを魅力的に表現したりする方法をお探しの場合は、ぜひお読みください。
## 前提条件
コーディングの楽しさに飛び込む前に、準備が整っていることを確認しましょう。必要なものは次のとおりです。
1. .NET Framework: 互換性のあるバージョンがインストールされていることを確認してください。Aspose.Cells は、.NET Core を含む複数のバージョンで動作します。
2.  Aspose.Cells for .NET: Aspose.Cellsライブラリをダウンロードしてインストールする必要があります。[ダウンロードリンク](https://releases.aspose.com/cells/net/).
3. 優れた IDE: あらゆる .NET 開発者の忠実なパートナーである Visual Studio は、コーディング体験を効率化するのに役立ちます。
4. C# の基礎知識: C# に精通していれば、このチュートリアルはスムーズに進むでしょう。
5. ドキュメント ディレクトリへのアクセス: Excel ファイルを保存する場所を把握します。これは、出力を効率的に整理するために不可欠です。
## パッケージのインポート
次のステップは、プロジェクトに適切なパッケージがインポートされていることを確認することです。Aspose.Cells for .NET にはさまざまな機能があるため、ここでは簡単に説明します。次のものを含める必要があります。
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
これらの名前空間により、このガイド全体で使用するすべての描画機能とセル管理機能にアクセスできるようになります。
## ステップ1: ドキュメントディレクトリを設定する
まず最初に、新しい Excel ファイルを保存するディレクトリを用意しましょう。手順は次のとおりです。
```csharp
string dataDir = "Your Document Directory";
//ディレクトリがまだ存在しない場合は作成します。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
このコードは、指定されたフォルダーが存在するかどうかを確認します。存在しない場合は、フォルダーを作成します。簡単ですよね? 混乱を避けるために、ファイル用の特定の場所を用意しておくことは常に良いことです。
## ステップ 2: ワークブックをインスタンス化する
ディレクトリの準備ができたので、新しい Excel ブックを作成しましょう。
```csharp
Workbook excelbook = new Workbook();
```
電話をかけることで`Workbook`コンストラクターを使用すると、基本的に「新しい Excel ファイルを開始しましょう」と言っていることになります。これがすべての図形とデータのキャンバスになります。
## ステップ3: 最初の円弧形状を追加する
ここから楽しいことが始まります! 最初の円弧シェイプを追加しましょう。
```csharp
Aspose.Cells.Drawing.ArcShape arc1 = excelbook.Worksheets[0].Shapes.AddArc(2, 0, 2, 0, 130, 130);
```
このコード行は、最初のワークシートに円弧シェイプを追加します。パラメータは、円弧の座標と、その曲率を定義する角度を指定します。 
## ステップ4: アークの外観をカスタマイズする
空白の円弧形状は、絵の具のないキャンバスのようなもので、ちょっとした工夫が必要です。
### 円弧の塗りつぶし色を設定する
```csharp
arc1.Fill.FillType = FillType.Solid;
arc1.Fill.SolidFill.Color = Color.Blue;
```
これにより、アークは青色一色になります。色を好きな色に変更するには、`Color.Blue`別の色に。
### 円弧の配置を設定する
```csharp
arc1.Placement = PlacementType.FreeFloating;
```
配置を「FreeFloating」に設定すると、円弧はセルの境界とは独立して移動できるため、配置を柔軟に行うことができます。
### 線の太さとスタイルを調整する
```csharp
arc1.Line.Weight = 1;      
arc1.Line.DashStyle = MsoLineDashStyle.Solid;
```
ここで、線の太さとスタイルを定義して、より目立つようにし、視覚的に魅力的なものにします。
## ステップ5: 別の円弧形状を追加する
つで止まるのはなぜでしょうか。Excel のビジュアルを充実させるために、別の円弧図形を追加してみましょう。
```csharp
Aspose.Cells.Drawing.ArcShape arc2 = excelbook.Worksheets[0].Shapes.AddArc(9, 0, 2, 0, 130, 130);
```
最初のアークと同様に、このアークも別の位置に追加されます。ここでデザインの魔法が起こります。
## ステップ6: 2番目のアークをカスタマイズする
番目のアークにも個性を持たせましょう。
### 円弧線の色を変更する
```csharp
arc2.Line.FillType = FillType.Solid;
arc2.Line.SolidFill.Color = Color.Blue;
```
私たちは青色で一貫していますが、いつでも組み合わせて、デザインに最適なものを探すことができます。
### 最初の円弧と同様のプロパティを設定する
以下の美的選択を必ず再現してください。
```csharp
arc2.Placement = PlacementType.FreeFloating;
arc2.Line.Weight = 1;           
arc2.Line.DashStyle = MsoLineDashStyle.Solid;
```
ここでは、2 番目の円弧が最初の円弧と一致していることを確認し、ワークシート全体で統一感のある外観を作成します。
## ステップ7: ワークブックを保存する
保存しなければ傑作は完成しませんよね? アークを Excel ファイルに書き込むときが来ました。
```csharp
excelbook.Save(dataDir + "book1.out.xls");
```
この行は、新しく作成された円弧を、指定されたディレクトリ内の「book1.out.xls」という名前の Excel ファイルに保存します。
## 結論
おめでとうございます! Aspose.Cells for .NET を使用して、Excel シートに接続ポイントを持つ円弧コントロールを追加する基本を習得しました。この機能は、スプレッドシートを美しくするだけでなく、複雑なデータを理解しやすくすることもできます。熟練した開発者でも、初心者でも、これらの視覚要素によって、レポートが平凡なものから壮大なものへと生まれ変わります。
## よくある質問
### Aspose.Cells とは何ですか?
Aspose.Cells は、開発者がプログラムで Excel ファイルを作成および操作できるようにする強力な .NET ライブラリです。
### Aspose.Cells を無料で使用できますか?
はい！無料トライアルをお試しください。[このリンク](https://releases.aspose.com/)開始します。
### 円弧以外の図形を追加するにはどうすればよいですか?
Aspose.Cells.Drawing 名前空間で利用可能なさまざまなクラスを使用して、四角形や円などのさまざまな図形を追加できます。
### Aspose.Cells で作成できるファイルの種類は何ですか?
XLS、XLSX、CSV など、さまざまな Excel 形式を作成および操作できます。
### Aspose.Cells のテクニカル サポートは受けられますか?
もちろんです！[Aspose サポート フォーラム](https://forum.aspose.com/c/cells/9)援助をお願いします。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
