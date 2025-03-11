---
title: Excel で非プリミティブ図形にアクセスする
linktitle: Excel で非プリミティブ図形にアクセスする
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して Excel の非プリミティブ図形にアクセスする方法を学習します。この包括的なガイドで、ステップバイステップの方法論を学びます。
weight: 19
url: /ja/net/excel-shape-text-modifications/access-non-primitive-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel で非プリミティブ図形にアクセスする

## 導入
Excel ファイルで非プリミティブ シェイプを見つけて、その複雑な詳細にアクセスする方法を考えたことはありませんか? .NET で作業し、Excel シートを操作しようとしている開発者であれば、この記事はまさにうってつけです。この記事では、Aspose.Cells ライブラリを使用して Excel で非プリミティブ シェイプに効率的にアクセスして操作する方法を説明します。包括的なステップ バイ ステップ ガイドでプロセスを詳しく説明するので、プラットフォームを初めて使用する場合でも簡単に操作できます。それでは、慣れて、魅力的な Aspose.Cells の世界に飛び込みましょう。
## 前提条件
コードに進む前に、いくつかの前提条件を満たす必要があります。
1. C# の基礎知識: スムーズに理解するには、C# プログラミング言語に精通していることが不可欠です。
2. Visual Studio: マシンに Visual Studio がインストールされている必要があります。ここでコードを記述します。
3.  Aspose.Cellsライブラリ: Aspose.Cellsライブラリをインストールする必要があります。最新バージョンをダウンロードできます。[ここ](https://releases.aspose.com/cells/net/).
4. Excelファイル: テスト用の非プリミティブ図形を含むExcelファイルを作成または取得します。このチュートリアルでは、`"NonPrimitiveShape.xlsx"`.
これらの前提条件が整ったら、楽しい部分に進むことができます。
## パッケージのインポート
すべてを稼働させるための最初のステップは、C# プロジェクトに必要なパッケージをインポートすることです。必要な手順は次のとおりです。
### 新しいプロジェクトを作成する
- Visual Studio を開き、新しい C# コンソール アプリケーション プロジェクトを作成します。
- プロジェクトに適切な名前を選択します。`AsposeShapeAccess`.
### Aspose.Cells NuGet パッケージをインストールする
- ソリューション エクスプローラーでプロジェクトを右クリックします。
- 「NuGet パッケージの管理」を選択します。
- 検索する`Aspose.Cells` 「インストール」をクリックします。
### 名前空間をインポートする
あなたの一番上に`Program.cs`ファイルに次の行を追加して Aspose.Cells 名前空間をインポートします。
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Collections;
using System;
```
それでは、Excel ファイル内の非プリミティブ シェイプにアクセスする実際のコードを見てみましょう。
## ステップ1: ドキュメントへのパスを設定する
図形にアクセスする前に、Excel ファイルが保存されているディレクトリを指定する必要があります。手順は次のとおりです。
```csharp
string dataDir = "Your Document Directory";
```
交換する`"Your Document Directory"`実際の経路で`NonPrimitiveShape.xlsx`ファイルが保存されます。 
## ステップ2: ワークブックを読み込む
ドキュメント パスが設定されたので、次はワークブックを読み込みます。手順は次のとおりです。
```csharp
Workbook workbook = new Workbook(dataDir + "NonPrimitiveShape.xlsx");
```
この行は新しい`Workbook`オブジェクトは、先ほど指定した Excel ファイルを読み取ります。
## ステップ3: ワークシートにアクセスする
次に、ワークブックの最初のワークシートにアクセスします。 やってみましょう:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
この行は、ワークブックの最初のワークシートにアクセスします。Excel は、一度に 1 つのシートに焦点を絞った場合に最も効果的に機能します。
## ステップ4: ユーザー定義シェイプにアクセスする
ここからが面白いところです。ワークシート内のユーザー定義の図形 (非プリミティブの場合もあります) にアクセスします。
```csharp
Shape shape = worksheet.Shapes[0];
```
ここでは、ワークシートの最初の図形にアクセスしています。図形が複数ある場合は、インデックスを変更できます。
## ステップ5: シェイプが非プリミティブかどうかを確認する
詳細にアクセスする前に、シェイプが非プリミティブかどうかを確認することが重要です。
```csharp
if (shape.AutoShapeType == AutoShapeType.NotPrimitive)
{
```
このブロックにより、より複雑な詳細を持つ図形のみを処理できるようになります。
## ステップ6: Shapeのデータにアクセスする
非プリミティブ シェイプであることが確認できたので、そのデータにアクセスできます。
```csharp
ShapePathCollection shapePathCollection = shape.Paths;
```
この行は、図形を定義するパスのコレクションを取得します。図形のデザインの設計図を取得するようなものだと考えてください。
## ステップ7: 各パスをループする
図形の構造をより深く理解するために、図形に関連付けられた各パスをループします。
```csharp
foreach (ShapePath shapePath in shapePathCollection)
{
```
このループにより、各パスを詳しく調べて詳細を調べることができます。
## ステップ8: アクセスパスセグメント
各シェイプパスには複数のセグメントを含めることができます。それらにアクセスしてみましょう。
```csharp
ShapeSegmentPathCollection pathSegments = shapePath.PathSegementList;
```
このコレクションには、図形のパスを構成するセグメントが保持されます。
## ステップ9: 各パスセグメントをループする
ここでは、パス セグメント コレクション内の各セグメントをループします。
```csharp
foreach (ShapeSegmentPath pathSegment in pathSegments)
{
```
ここからは楽しい部分が始まります。各セグメントの詳細に入っていきます。
## ステップ10: アクセスパスセグメントポイント
次に、各パス セグメントの個々のポイントについて説明します。
```csharp
ShapePathPointCollection segmentPoints = pathSegment.Points;
```
これは、図形の曲線と角を定義するすべての座標を収集するものと考えてください。
## ステップ11: ポイントの詳細を印刷する
最後に、パス セグメント内の各ポイントの詳細をコンソールに出力します。
```csharp
foreach (ShapePathPoint pathPoint in segmentPoints)
{
    Console.WriteLine("X: " + pathPoint.X + ", Y: " + pathPoint.Y);
}
```
これにより、非プリミティブ形状を定義するすべてのポイントの座標を効果的に出力できます。これは、内部で何が起こっているかを視覚化する優れた方法です。
## 結論
これで完了です。Aspose.Cells for .NET を使用して、Excel の非プリミティブ シェイプの詳細にアクセスし、調査することができました。この強力なライブラリは、レポートの生成、動的なスプレッドシートの作成、複雑なシェイプの処理など、Excel ファイルの操作に無限の可能性をもたらします。ご質問やさらなるサポートが必要な場合は、遠慮なくお問い合わせください。
## よくある質問
### Excel の非プリミティブ図形とは何ですか?
非プリミティブ形状は、単純な幾何学的形状ではなく、複数のセグメントと曲線から構成される複雑な形状です。
### Aspose.Cells for .NET をインストールするにはどうすればよいですか?
 Visual StudioのNuGetパッケージマネージャーからインストールするか、[サイト](https://releases.aspose.com/cells/net/).
### Aspose.Cells を無料で使用できますか?
はい、ウェブサイトから無料トライアルを入手して、その機能を試すことができます。[ここ](https://releases.aspose.com/).
### Aspose.Cells を使用する利点は何ですか?
Aspose.Cells は、マシンに Excel をインストールしなくても、Excel スプレッドシートをプログラムで操作できる強力な機能を提供します。
### Aspose.Cells のサポートはどこで見つかりますか?
 Asposeコミュニティフォーラムからヘルプとサポートを受けることができます[ここ](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
