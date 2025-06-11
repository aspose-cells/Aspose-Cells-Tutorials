---
"description": "このわかりやすいチュートリアルで、Aspose.Cells for .NET を使用して Excel スプレッドシートからフォントを取得して一覧表示する方法を学びます。"
"linktitle": "スプレッドシートで使用されているフォントのリストを取得する"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": "スプレッドシートで使用されているフォントのリストを取得する"
"url": "/ja/net/working-with-fonts-in-spreadsheets/get-list-of-fonts-used-in-spreadsheet/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# スプレッドシートで使用されているフォントのリストを取得する

## 導入
Excelスプレッドシートをスクロールしながら、各セルで使われているフォントが気になったことはありませんか？古い文書を見て、どんなフォントが使われているのか知りたいと思ったことはありませんか？そんな時、Aspose.Cells for .NETを使えば、スプレッドシートに隠されたフォントの秘密を解き明かすツールボックスを手に入れることができます。このガイドでは、Excelファイルで使用されているすべてのフォントリストを簡単に取得する方法をご紹介します。シートベルトを締めて、スプレッドシートの世界に飛び込みましょう！
## 前提条件
コードを書き始める前に、いくつか必要なものがあります。ご安心ください。とても簡単です。必要なもののチェックリストを以下に示します。
1. Visual Studio: お使いのマシンにVisual Studioがインストールされていることを確認してください。ここでコードを記述します。
2. Aspose.Cells for .NET: Aspose.Cellsライブラリが必要です。まだダウンロードしていない場合は、こちらからダウンロードできます。 [サイト](https://releases。aspose.com/cells/net/).
3. C# の基本知識: C# プログラミングを少し理解しておくと、コードを簡単に操作できるようになります。
4. サンプルExcelファイル：サンプルExcelファイル（「sampleGetFonts.xlsx」など）が必要です。このファイルを使ってフォント探索を行います。
すべての準備が整ったら、コーディングを始める準備が整います。
## パッケージのインポート
まずは必要な名前空間をインポートしましょう。.NETでは、パッケージのインポートはパーティーに適切なゲストを招待するようなものです。適切なゲストがいなければ、スムーズに動作しません。
Aspose.Cells をインポートする方法は次のとおりです。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
このシンプルな行で、Aspose.Cells のコア機能をプロジェクトに導入できます。それでは、ワークブックの読み込みに移りましょう。
## ステップ1: ドキュメントディレクトリを設定する
まず最初に、コードに入る前に、ドキュメントディレクトリへのパスを設定する必要があります。ここにExcelファイルが保存されます。 
```csharp
string dataDir = "Your Document Directory";
```
「ドキュメントディレクトリ」をExcelファイルの実際のパスに置き換えます。これは、プログラムに「ここにExcelファイルを保存してあるから、確認して！」と伝えるようなものです。
## ステップ2: ソースブックを読み込む
Excelファイルを読み込みます。新しいインスタンスを作成します。 `Workbook` クラスを指定してファイルのパスを渡します。 
```csharp
Workbook wb = new Workbook(dataDir + "sampleGetFonts.xlsx");
```
ここで何が起こっているのでしょうか？基本的にはスプレッドシートへの扉を開いているようなものです。 `Workbook` クラスを使用すると、Excel ファイルの内容を操作できます。 
## ステップ3：すべてのフォントを取得する
いよいよ魔法の瞬間です。フォントを実際に取得してみましょう。 `GetFonts()` この方法は私たちにとって黄金のチケットです。
```csharp
Aspose.Cells.Font[] fnts = wb.GetFonts();
```
ここでは、ワークブックに使用されているすべてのフォントに関する情報を開示するよう求めています。 `fnts` 配列は私たちの宝物を保持します。
## ステップ4：フォントを印刷する
最後に、これらのフォントを印刷してみましょう。これにより、発見した内容を検証しやすくなります。
```csharp
for (int i = 0; i < fnts.Length; i++)
{
	Console.WriteLine(fnts[i]);
}
```
このループは、私たちの `fnts` 配列を作成し、コンソールに一つずつ出力します。Excelファイルで使える素敵なタイポグラフィの選択肢を全部見せびらかすようなものです！
## 結論
これで完了です！わずか数行のコードで、Aspose.Cells for .NET を使って Excel スプレッドシートで使用されているフォントの一覧を取得し、印刷することができました。これは単なるフォントの問題ではありません。ドキュメントの微妙なニュアンスを理解し、プレゼンテーションの質を高め、スプレッドシートのタイポグラフィをマスターすることにつながります。開発者の方でも、Excel をいじるのが好きな方でも、この小さなコードがゲームチェンジャーになるかもしれません。 
## よくある質問
### Aspose.Cells を別途インストールする必要がありますか?
はい、プロジェクトでライブラリをダウンロードして参照する必要があります。 
### Aspose.Cells を他の形式で使用できますか?
もちろんです! Aspose.Cells は、XLSX、XLS、CSV など、複数の Excel 形式で動作します。
### 無料トライアルはありますか？
はい、無料トライアルをご利用ください。 [ダウンロードリンク](https://releases。aspose.com/).
### テクニカルサポートを受けるにはどうすればよいですか?
助けが必要な場合は、 [Aspose サポートフォーラム](https://forum.aspose.com/c/cells/9) 素晴らしいリソースです。
### Aspose.Cells は .NET Core と互換性がありますか?
はい、Aspose.Cells は .NET Core プロジェクトとも互換性があります。


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}