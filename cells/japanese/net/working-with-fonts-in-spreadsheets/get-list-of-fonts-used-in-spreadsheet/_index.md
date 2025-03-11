---
title: スプレッドシートで使用されているフォントのリストを取得する
linktitle: スプレッドシートで使用されているフォントのリストを取得する
second_title: Aspose.Cells .NET Excel 処理 API
description: このわかりやすいチュートリアルで、Aspose.Cells for .NET を使用して Excel スプレッドシートからフォントを取得して一覧表示する方法を学びます。
weight: 10
url: /ja/net/working-with-fonts-in-spreadsheets/get-list-of-fonts-used-in-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# スプレッドシートで使用されているフォントのリストを取得する

## 導入
Excel スプレッドシートをスクロールしているときに、さまざまなセルで使用されているフォントについて疑問に思ったことはありませんか? 古いドキュメントに遭遇し、どのような書体が選択されたのか知りたいと思ったことはありませんか? 幸運です! Aspose.Cells for .NET は、スプレッドシートに隠されたフォントの秘密をふるいにかけて発見できるツールボックスのようなものです。 このガイドでは、Excel ファイルで使用されているすべてのフォントのリストを簡単に取得する方法を説明します。 シートベルトを締めて、スプレッドシートの世界に飛び込みましょう!
## 前提条件
コードに進む前に、始めるために必要なものがいくつかあります。心配しないでください。非常に簡単です。必要なもののチェックリストは次のとおりです。
1. Visual Studio: マシンに Visual Studio のバージョンがインストールされていることを確認してください。ここでコードを記述します。
2. Aspose.Cells for .NET: Aspose.Cellsライブラリが必要です。まだダウンロードしていない場合は、[サイト](https://releases.aspose.com/cells/net/).
3. C# の基礎知識: C# プログラミングを少し理解しておくと、コードを簡単に操作できるようになります。
4. サンプル Excel ファイル: 作業には、「sampleGetFonts.xlsx」のようなサンプル Excel ファイルが必要です。ここでフォント探索を適用します。
すべての準備が整ったら、コーディングを始める準備が整います。
## パッケージのインポート
まず、必要な名前空間をインポートしましょう。.NET では、パッケージのインポートはパーティーに適切なゲストを招待するようなものです。適切なゲストがいなければ、物事はスムーズに進みません。
Aspose.Cells をインポートする方法は次のとおりです。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
この簡単な行で、Aspose.Cells のコア機能をプロジェクトに導入します。次に、ワークブックの読み込みに移りましょう。
## ステップ1: ドキュメントディレクトリを設定する
まず最初に、コードに進む前に、ドキュメント ディレクトリへのパスを設定する必要があります。ここに Excel ファイルが保存されます。 
```csharp
string dataDir = "Your Document Directory";
```
「ドキュメント ディレクトリ」を、Excel ファイルが保存されている実際のパスに置き換えます。これは、プログラムに「Excel ファイルをここに保存しておいたから、確認してね」と伝えるようなものだと考えてください。
## ステップ2: ソースワークブックを読み込む
Excelファイルを読み込みます。新しいインスタンスを作成します。`Workbook`クラスを指定してファイルのパスを渡します。 
```csharp
Workbook wb = new Workbook(dataDir + "sampleGetFonts.xlsx");
```
ここで何が起こっているのでしょうか？基本的にはスプレッドシートへの扉を開いているのです。`Workbook`クラスを使用すると、Excel ファイルの内容を操作できます。 
## ステップ3: すべてのフォントを取得する
さあ、魔法の瞬間がやってきました。フォントを実際に取得してみましょう。`GetFonts()`この方法は私たちにとって黄金のチケットです。
```csharp
Aspose.Cells.Font[] fnts = wb.GetFonts();
```
ここでは、ワークブックに使用されているすべてのフォントに関する情報を開示するよう求めています。`fnts`配列は私たちの宝物を保持します。
## ステップ4: フォントを印刷する
最後に、それらのフォントを印刷してみましょう。これにより、発見した内容を確認することができます。
```csharp
for (int i = 0; i < fnts.Length; i++)
{
	Console.WriteLine(fnts[i]);
}
```
このループは、私たちの各フォントを順に実行します。`fnts`配列を作成し、コンソールに 1 つずつ出力します。Excel ファイルにあるすべてのクールなタイポグラフィの選択肢を披露するようなものです。
## 結論
これで完了です。わずか数行のコードで、Aspose.Cells for .NET を使用して Excel スプレッドシートで使用されているフォントの一覧を取得して印刷できました。これはフォントに関することだけではありません。ドキュメントの微妙なニュアンスを理解し、プレゼンテーションを強化し、スプレッドシートのタイポグラフィの技術を習得することも重要です。開発者であっても、Excel をいじるのが好きな人であっても、この小さなスニペットはゲームチェンジャーになる可能性があります。 
## よくある質問
### Aspose.Cells を別途インストールする必要がありますか?
はい、プロジェクトでライブラリをダウンロードして参照する必要があります。 
### Aspose.Cells を他の形式で使用できますか?
もちろんです! Aspose.Cells は、XLSX、XLS、CSV などの複数の Excel 形式で動作します。
### 無料トライアルはありますか？
はい、無料トライアルをご利用ください。[ダウンロードリンク](https://releases.aspose.com/).
### 技術サポートを受けるにはどうすればよいですか?
ヘルプが必要な場合は、[Aspose サポート フォーラム](https://forum.aspose.com/c/cells/9)素晴らしいリソースです。
### Aspose.Cells は .NET Core と互換性がありますか?
はい、Aspose.Cells は .NET Core プロジェクトとも互換性があります。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
