---
title: Excel ファイルを 2007 xlsb 形式で保存する
linktitle: Excel ファイルを 2007 xlsb 形式で保存する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して Excel ファイルを xlsb 形式で保存する方法を学びます。実用的な例を交えたステップバイステップのガイドがあなたを待っています。
weight: 11
url: /ja/net/saving-files-in-different-formats/save-excel-file-in-2007-xlsb-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel ファイルを 2007 xlsb 形式で保存する

## 導入
.NET で Excel ファイルを操作する場合、特に Aspose.Cells ライブラリを使用すると、多くの柔軟性と機能性が得られます。この強力なツールを使用すると、Excel ファイルを簡単に作成、変更、保存できます。今日は、Excel ファイルを 2007 xlsb 形式で保存する方法を説明します。一般的なオーバーヘッドなしで Excel ファイルをプログラムで処理する方法をお探しの場合は、ここが最適な場所です。 
## 前提条件
始める前に、スムーズに進めるために必要なものがすべて揃っていることを確認しましょう。必要なものは次のとおりです。
1. Visual Studio: マシンに Visual Studio のバージョンがインストールされていることを確認してください。ここで .NET コードを記述します。 
2.  Aspose.Cellsライブラリ: Aspose.Cells for .NETライブラリが必要です。まだダウンロードしていない場合は、[Aspose ダウンロード ページ](https://releases.aspose.com/cells/net/)それをつかむために。 
3. C# の基礎知識: C# と .NET の基礎的な理解があれば、コード例をより快適に理解できるようになります。
4. .NET Framework: プロジェクトが Aspose.Cells ライブラリでサポートされている適切な .NET Framework を使用して設定されていることを確認します。
5. Excel ドキュメント: 新しいワークブックを作成することもできますが、既存のファイルを操作する場合には、開始ドキュメントがあると便利です。
## パッケージのインポート
プロジェクトで Aspose.Cells ライブラリの使用を開始するには、必要な名前空間をインポートする必要があります。これは、プロジェクトを開始する前にツールボックスを解凍するのと似ています。
### プロジェクトを設定する
1. Visual Studio を開きます。「新しいプロジェクトの作成」を選択して新しいプロジェクトを開始します。 
2. プロジェクト テンプレートを選択します。好みに応じて、コンソール アプリケーションまたは Windows フォーム アプリケーションを選択します。
3. Aspose.Cells 参照を追加します。プロジェクト エクスプローラーで [参照] を右クリックし、[参照の追加] をクリックします。ダウンロードした Aspose.Cells.dll ファイルを参照します。
### 名前空間をインポートする
参照を追加したら、次のステップは C# ファイルの先頭に名前空間を含めることです。
```csharp
using System.IO;
using Aspose.Cells;
```
このコード行を使用すると、Aspose.Cells ライブラリによって提供されるすべてのクラスとメソッドに修飾なしでアクセスできます。

ここで、Excel ファイルを 2007 xlsb 形式で保存する手順を詳しく説明します。
## ステップ1: 保存ディレクトリを設定する
まず、Excel ファイルを保存する場所を決定する必要があります。

```csharp
//ドキュメントディレクトリへのパス
string dataDir = "Your Document Directory\\";
```
この行はドキュメントディレクトリへのパスを定義します。`"Your Document Directory"`システム上でファイルを保存する実際のパスを入力します。
## ステップ2: ワークブックオブジェクトを作成する
次に、Aspose.Cells ライブラリを使用して新しいワークブックを作成します。

```csharp
Workbook workbook = new Workbook();
```
ここでは、`Workbook`クラス。この新しく作成されたワークブックは、必要に応じてデータの入力を開始できる空のワークブックです。
## ステップ3: ワークブックを保存する
次は楽しい部分です。ワークブックを希望の形式で保存します。
```csharp
// Excel2007 xlsb形式で保存
workbook.Save(dataDir + "output.xlsb", SaveFormat.Xlsb);
```
このコード行はワークブックを次のように保存します`output.xlsb`指定されたディレクトリで`SaveFormat.Xlsb`フォーマット。`SaveFormat`列挙型は、次のようなさまざまな形式を指定できるという点で強力です。`Xlsx`, `Xls`など
## 結論
これで、Aspose.Cells for .NET を使用して Excel ファイルを 2007 xlsb 形式で保存する方法を学習できました。このシンプルでありながら効果的な機能は、.NET アプリケーションで Excel ファイルの処理を自動化する必要がある開発者にとって画期的なものになる可能性があります。

## よくある質問
### Aspose.Cells ライブラリとは何ですか?
Aspose.Cells は、Microsoft Excel をインストールしなくても、開発者がプログラムで Excel ファイルを作成、変更、操作できるようにする強力な .NET ライブラリです。
### Aspose.Cells を無料で試すことはできますか?
もちろんです！[無料トライアル](https://releases.aspose.com/)ライブラリの機能を調べます。
### xls 形式と xlsb 形式の違いは何ですか?
xls 形式は古く、バイナリ ファイル構造に基づいていますが、xlsb はバイナリ ストレージも使用する新しい形式ですが、ファイル サイズが大きく、処理が高速です。
### Aspose.Cells のライセンスはどこで購入できますか?
ライセンスは直接購入することができます[Aspose 購入ページ](https://purchase.aspose.com/buy).
### Aspose.Cells の問題に関するサポートを受けるにはどうすればよいですか?
何か問題や質問がある場合は、お気軽に[サポートフォーラム](https://forum.aspose.com/c/cells/9)
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
