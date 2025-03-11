---
title: Excel のワークシートに楕円を追加する
linktitle: Excel のワークシートに楕円を追加する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して Excel ワークシートに楕円を追加する方法を学びます。詳細なコード説明を含むステップバイステップ ガイド。
weight: 17
url: /ja/net/excel-shapes-controls/add-oval-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel のワークシートに楕円を追加する

## 導入
魅力的でインタラクティブな Excel ファイルを作成するには、数字や数式だけでは不十分です。楕円などの図形は、視覚的な魅力を加えたり、ワークシートに機能的な要素を提供したりできます。このチュートリアルでは、Aspose.Cells for .NET を使用してプログラムで Excel ワークシートに楕円を追加する方法について説明します。センスや機能性を追加したい場合でも、すべてを詳しく説明するステップバイステップのガイドが用意されています。
## 前提条件
コードに進む前に、準備しておくべきことがいくつかあります。
1.  Aspose.Cells for .NETライブラリ:以下からダウンロードできます。[ここ](https://releases.aspose.com/cells/net/)または、Visual Studio で NuGet を使用してインストールします。
2. 開発環境: Visual Studio のような C# IDE。
3. C# の基本的な理解: C# の基本的なコーディング概念を理解している必要があります。
また、Aspose.Cells for .NETライブラリをインストールしてプロジェクトを設定することを忘れないでください。まだライセンスを持っていない場合は、[一時ライセンス](https://purchase.aspose.com/temporary-license/)または[無料トライアル](https://releases.aspose.com/)バージョン。
## パッケージのインポート
コードを記述する前に、必要な名前空間が含まれていることを確認してください。適切なライブラリを使用していることを確認するための C# コード スニペットを次に示します。
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
## ステップ1: ディレクトリを設定する
Excel シートに楕円を追加する最初の手順は、Excel ファイルを保存する場所を指定することです。作業を保存する前に、ディレクトリ パスを定義して、ディレクトリが存在することを確認しましょう。

ディレクトリ パスを作成し、存在するかどうかを確認します。フォルダーが存在しない場合は作成されます。
```csharp
//ドキュメント ディレクトリへのパス。
string dataDir = "Your Document Directory";
//ディレクトリがまだ存在しない場合は作成します。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
この手順は、ファイルが適切な場所に保存され、後でファイル パスの問題が発生しないようにするために重要です。
## ステップ2: 新しいワークブックを初期化する
次に、楕円形を追加する新しいワークブックを作成する必要があります。ワークブックは Excel ファイルを表し、そこにコンテンツや図形を追加できます。

このステップでは、新しいインスタンスを作成します`Workbook`Excel ファイル コンテナーとして機能するオブジェクト。
```csharp
//新しいワークブックをインスタンス化します。
Workbook excelbook = new Workbook();
```
## ステップ3: 最初の楕円形を追加する
次は楽しい部分です。ワークシートに楕円形を追加します。この楕円形は、ボタンやハイライトなどの視覚要素を表すことができます。まず、ワークブックの最初のワークシートに最初の楕円形を追加します。

ここでは、`Shapes.AddOval()`ワークシート上の特定の行と列に楕円を作成する方法。
```csharp
//楕円形を追加します。
Aspose.Cells.Drawing.Oval oval1 = excelbook.Worksheets[0].Shapes.AddOval(2, 0, 2, 0, 130, 160);
```
内部のパラメータ`AddOval()`は次のとおりです。
- 最初の 2 つの数字は、楕円の左上隅の行と列を表します。
- 次の 2 つの数字は楕円の高さと幅を表します。
## ステップ4: 楕円の配置とスタイルを設定する
楕円を作成したら、位置、線の太さ、破線スタイルを設定できます。`Placement`プロパティは、ワークシート内のセルのサイズを変更したり移動したりするときに楕円がどのように動作するかを決定します。

楕円を自由に浮かせて見た目を整えます。
```csharp
//楕円の配置を設定します。
oval1.Placement = PlacementType.FreeFloating;
//線の太さを設定します。
oval1.Line.Weight = 1;
//楕円の破線スタイルを設定します。
oval1.Line.DashStyle = MsoLineDashStyle.Solid;
```
これにより、楕円はワークシート内で自由に移動できるようになり、線の太さとスタイルは視覚的な一貫性を保つように設定されます。
## ステップ5: 別の楕円形（円）を追加する
つで止まるのはなぜでしょうか? この手順では、別の楕円形を追加し、今度は高さと幅を同じにして完全な円を作成します。

別の楕円を作成し、別の場所に配置し、高さと幅を等しく設定して円形になるようにします。
```csharp
//別の楕円（円）の形を追加します。
Aspose.Cells.Drawing.Oval oval2 = excelbook.Worksheets[0].Shapes.AddOval(9, 0, 2, 15, 130, 130);
```
## ステップ6: 2番目の楕円のスタイルを設定する
前と同じように、この 2 番目の楕円 (または円) の配置、太さ、ダッシュ スタイルを調整します。

最初の楕円のスタイルに合わせて、2 番目の楕円に同様のプロパティを適用します。
```csharp
//楕円の配置を設定します。
oval2.Placement = PlacementType.FreeFloating;
//線の太さを設定します。
oval2.Line.Weight = 1;
//楕円の破線スタイルを設定します。
oval2.Line.DashStyle = MsoLineDashStyle.Solid;
```
## ステップ7: ワークブックを保存する
最後に、追加した楕円を含むワークブックを保存する必要があります。ファイルを保存すると、すべての変更が保存されます。

先ほど定義したディレクトリ パスにワークブックを保存します。
```csharp
// Excel ファイルを保存します。
excelbook.Save(dataDir + "book1.out.xls");
```
これで完了です。Excel ワークシートに楕円が正常に追加され、ファイルが保存されました。
## 結論
Aspose.Cells for .NET を使用して楕円などの図形を Excel シートに追加することは、簡単なだけでなく、追加の視覚要素でスプレッドシートを拡張する楽しい方法でもあります。デザイン目的であっても、クリック可能な要素の追加であっても、図形は Excel ファイルの外観と機能に重要な役割を果たします。そのため、次回、インタラクティブまたは視覚的に魅力的な Excel シートを必要とするプロジェクトに取り組むときには、完璧な楕円を追加する方法が正確にわかります。
## よくある質問
### Aspose.Cells for .NET を使用して、四角形や線などの他の図形を追加できますか?
はい、長方形、線、矢印などのさまざまな図形を追加できます。`Shapes` Aspose.Cells のコレクション。
### 楕円を追加した後でサイズを変更することは可能ですか?
もちろんです! 楕円を追加した後で、楕円の高さと幅のプロパティを変更できます。
### XLS 以外にどのようなファイル形式でワークブックを保存できますか?
Aspose.Cells は、XLSX、CSV、PDF などの複数の形式をサポートしています。
### 楕円の輪郭の色を変更できますか?
はい、楕円の線の色は、`Line.Color`財産。
### Aspose.Cells のライセンスは必要ですか?
 Aspose.Cellsは無料トライアルで試すことができますが、[ライセンス](https://purchase.aspose.com/buy)長期使用や高度な機能へのアクセスに。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
