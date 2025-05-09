---
"description": "Aspose.Cells for .NET を使用して、Excel ワークシートに楕円を追加する方法を学びます。詳細なコード解説付きのステップバイステップガイドです。"
"linktitle": "Excelのワークシートに楕円を追加する"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": "Excelのワークシートに楕円を追加する"
"url": "/ja/net/excel-shapes-controls/add-oval-to-worksheet-excel/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excelのワークシートに楕円を追加する

## 導入
魅力的でインタラクティブなExcelファイルを作成するには、数字や数式だけでは不十分です。楕円などの図形は、視覚的な魅力を高めたり、ワークシートに機能的な要素を加えたりすることができます。このチュートリアルでは、Aspose.Cells for .NETを使用して、プログラムからExcelワークシートに楕円を追加する方法を説明します。見た目の印象を変えたい場合でも、機能性を高めたい場合でも、すべてを詳しく説明したステップバイステップガイドをご用意しています。
## 前提条件
コードに進む前に、準備しておくべきことがいくつかあります。
1. Aspose.Cells for .NET ライブラリ: ダウンロードはこちらから [ここ](https://releases.aspose.com/cells/net/) または、Visual Studio で NuGet を使用してインストールします。
2. 開発環境: Visual Studio のような C# IDE。
3. C# の基本的な理解: C# の基本的なコーディング概念を理解している必要があります。
また、Aspose.Cells for .NETライブラリをインストールしてプロジェクトをセットアップすることを忘れないでください。まだライセンスをお持ちでない場合は、 [一時ライセンス](https://purchase.aspose.com/temporary-license/) または [無料トライアル](https://releases.aspose.com/) バージョン。
## パッケージのインポート
コードを書く前に、必要な名前空間が含まれていることを確認してください。適切なライブラリを使用していることを確認するためのC#コードスニペットを以下に示します。
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## ステップ1: ディレクトリを設定する
Excelシートに楕円を追加する最初のステップは、Excelファイルの保存場所を指定することです。作業を保存する前に、ディレクトリパスを定義し、そのディレクトリが存在することを確認しましょう。

ディレクトリパスを作成し、存在するかどうかを確認します。フォルダが存在しない場合は作成されます。
```csharp
// ドキュメント ディレクトリへのパス。
string dataDir = "Your Document Directory";
// ディレクトリがまだ存在しない場合は作成します。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
この手順は、ファイルが適切な場所に保存され、後でファイル パスの問題が発生しないようにするために重要です。
## ステップ2: 新しいワークブックを初期化する
次に、楕円形を追加する新しいワークブックを作成します。ワークブックはExcelファイルを表し、コンテンツや図形を追加できます。

このステップでは、新しい `Workbook` Excel ファイル コンテナーとして機能するオブジェクト。
```csharp
// 新しいワークブックをインスタンス化します。
Workbook excelbook = new Workbook();
```
## ステップ3：最初の楕円形を追加する
いよいよ楽しい作業、ワークシートに楕円を追加します。この楕円は、ボタンやハイライトなどの視覚的な要素を表すことができます。まずは、ワークブックの最初のワークシートに最初の楕円を追加します。

ここでは、 `Shapes.AddOval()` ワークシート上の特定の行と列に楕円を作成する方法。
```csharp
// 楕円形を追加します。
Aspose.Cells.Drawing.Oval oval1 = excelbook.Worksheets[0].Shapes.AddOval(2, 0, 2, 0, 130, 160);
```
内部のパラメータ `AddOval()` は次のとおりです。
- 最初の 2 つの数字は、楕円の左上隅の行と列を表します。
- 次の 2 つの数字は、楕円の高さと幅を表します。
## ステップ4：楕円の配置とスタイルを設定する
楕円を作成したら、位置、線の太さ、破線スタイルを設定できます。 `Placement` プロパティは、ワークシート内のセルのサイズを変更したり移動したりするときに楕円がどのように動作するかを決定します。

楕円を自由に浮かせて見た目を整えます。
```csharp
// 楕円の配置を設定します。
oval1.Placement = PlacementType.FreeFloating;
// 線の太さを設定します。
oval1.Line.Weight = 1;
// 楕円の破線スタイルを設定します。
oval1.Line.DashStyle = MsoLineDashStyle.Solid;
```
これにより、楕円はワークシート内で自由に移動できるようになり、線の太さとスタイルは視覚的な一貫性を保つように設定されます。
## ステップ5：別の楕円（円）図形を追加する
つで止まるのはなぜでしょうか? このステップでは、もう 1 つの楕円形を追加して、今度は高さと幅を同じにして完全な円を作成します。

別の楕円を作成し、別の場所に配置し、高さと幅を等しく設定して円形になるようにします。
```csharp
// 別の楕円（円）図形を追加します。
Aspose.Cells.Drawing.Oval oval2 = excelbook.Worksheets[0].Shapes.AddOval(9, 0, 2, 15, 130, 130);
```
## ステップ6：2番目の楕円のスタイルを設定する
前と同じように、この 2 番目の楕円 (または円) の配置、太さ、ダッシュ スタイルを調整します。

最初の楕円のスタイルに合わせて、2 番目の楕円に同様のプロパティを適用します。
```csharp
// 楕円の配置を設定します。
oval2.Placement = PlacementType.FreeFloating;
// 線の太さを設定します。
oval2.Line.Weight = 1;
// 楕円の破線スタイルを設定します。
oval2.Line.DashStyle = MsoLineDashStyle.Solid;
```
## ステップ7: ワークブックを保存する
最後に、追加した楕円を含むワークブックを保存します。ファイルを保存すると、すべての変更が保存されます。

先ほど定義したディレクトリ パスにワークブックを保存します。
```csharp
// Excel ファイルを保存します。
excelbook.Save(dataDir + "book1.out.xls");
```
これで完了です。Excel ワークシートに楕円を追加し、ファイルを保存しました。
## 結論
Aspose.Cells for .NET を使って Excel シートに楕円などの図形を追加するのは、簡単なだけでなく、視覚的な要素を追加してスプレッドシートを魅力的に見せる楽しい方法です。デザイン目的でも、クリック可能な要素を追加する目的でも、図形は Excel ファイルの見た目や機能に重要な役割を果たします。次回、インタラクティブな機能や視覚的に魅力的な Excel シートが必要なプロジェクトに取り組む際には、完璧な楕円を追加する方法を正確に理解できるはずです。
## よくある質問
### Aspose.Cells for .NET を使用して、四角形や線などの他の図形を追加できますか?
はい、長方形、線、矢印などのさまざまな図形を追加できます。 `Shapes` Aspose.Cells のコレクション。
### 楕円を追加した後にサイズを変更することは可能ですか?
もちろんです！楕円を追加した後で、高さと幅のプロパティを変更できます。
### XLS 以外にどのようなファイル形式でワークブックを保存できますか?
Aspose.Cells は、XLSX、CSV、PDF などの複数の形式をサポートしています。
### 楕円の輪郭の色を変更できますか?
はい、楕円の線の色は、 `Line.Color` 財産。
### Aspose.Cells のライセンスは必要ですか?
Aspose.Cellsは無料トライアルで試すことができますが、 [ライセンス](https://purchase.aspose.com/buy) 長期使用や高度な機能へのアクセスに。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}