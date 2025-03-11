---
title: Aspose.Cells で名前付き宛先を持つ PDF ブックマークを追加する
linktitle: Aspose.Cells で名前付き宛先を持つ PDF ブックマークを追加する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して、ブックマーク付きのインタラクティブな PDF を作成する方法を学びます。このステップ バイ ステップ ガイドを使用すると、簡単に作成できます。
weight: 10
url: /ja/net/rendering-and-export/add-pdf-bookmarks/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells で名前付き宛先を持つ PDF ブックマークを追加する

## 導入
長い PDF ドキュメントを扱ったことがあるなら、何ページにもわたる情報の間を移動するのがいかに難しいかご存じでしょう。ブックマークは、迅速なナビゲーション ポイントを提供することで、ユーザー エクスペリエンスを向上させる上で重要な役割を果たします。このチュートリアルでは、Aspose.Cells for .NET を使用して Excel ファイルから生成された PDF に、名前付きの移動先を持つブックマークを追加する方法について説明します。
## 前提条件
細かい点に入る前に、すべてが整っていることを確認しましょう。このチュートリアルを実行するには、次のものが必要です。
1. Visual Studio: .NET 開発用の IDE です。お使いのマシンにインストールされていることを確認してください。
2.  Aspose.Cells for .NET: Aspose.Cellsライブラリが必要です。[ここからダウンロード](https://releases.aspose.com/cells/net/)まずは試してみたい方は、[無料トライアルはこちら](https://releases.aspose.com/).
3. .NET Framework: 互換性のあるバージョンがインストールされていることを確認してください。Aspose.Cells は複数のバージョンの .NET をサポートしています。
4. C# の基礎知識: C# 構文を理解しておくと、コード スニペットをよりよく理解するのに役立ちます。
ツールキットにこれらのアイテムがあれば、ブックマーク付きの PDF ドキュメントを作成できます。
## パッケージのインポート
まず、プロジェクトが Aspose.Cells の機能を利用できることを確認する必要があります。まず、Visual Studio で新しい C# プロジェクトを作成します。その後、必要なパッケージをインポートします。通常は、コード ファイルの先頭でこれを行います。
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
それがいかに簡単かお分かりいただけたでしょうか? 数行追加するだけで、Excel ファイルを処理するための強力なツールキットが利用できるようになります。
## ステップ1: ディレクトリの設定
まず、ソース ディレクトリと出力ディレクトリを指定する必要があります。これは、最初の Excel ファイルが存在する場所であり、PDF が保存される場所です。
```csharp
string sourceDir = "Your Document Directory"; //例: "C:\\MyFiles\\"
string outputDir = "Your Document Directory"; //例: "C:\\MyOutput\\"
```
このステップは、作業スペースの準備と考えてください。画家がイーゼルやキャンバスなしでは作業を始めないのと同じように、ファイルの場所を指定せずにコーディングを開始すべきではありません。
## ステップ2: ソースExcelファイルを読み込む
次に、ワークブック クラスを使用して Excel ファイルをメモリに読み込む必要があります。
```csharp
Workbook wb = new Workbook(sourceDir + "samplePdfBookmarkEntry_DestinationName.xlsx");
```
ワークブックを読み込むことは、可能性に満ちたドキュメントを開くようなものです。元の Excel ファイルのすべてのワークシート、セル、および書式設定機能にアクセスできます。
## ステップ3: ワークシートにアクセスする
ワークブックが読み込まれたので、最初のワークシートにアクセスしてみましょう。ブックマークで参照するセルはここにあります。
```csharp
Worksheet ws = wb.Worksheets[0];
```
すべてのアーティストにはキャンバスが必要です。このシナリオでは、ワークシートがキャンバスとして機能し、どのセルにブックマークを保持するかを決定します。
## ステップ4: ブックマークの作成
### 特定のセルにアクセスする
特定のセル（セル C5 とします）にブックマークを作成しましょう。ブックマーク エントリを作成し、そのセルにリンクして、名前を指定します。 
```csharp
Cell cell = ws.Cells["C5"];
PdfBookmarkEntry bookmarkEntry = new PdfBookmarkEntry();
bookmarkEntry.Text = "Text"; //好みのブックマーク名に変更する
bookmarkEntry.Destination = cell;
bookmarkEntry.DestinationName = "AsposeCells--" + cell.Name;
```
これは、ドキュメントに付箋を貼るようなものと考えることができます。タイトルはブックマークのリンク先を示し、リンク先 (セル C5) は PDF 内でのリンク先を示します。
### サブブックマークの追加
サブブックマークを追加することで、ユーザー エクスペリエンスを強化できます。ここで、さらに 2 つのセル (G56 と L4) にアクセスし、サブブックマークとして設定します。
```csharp
cell = ws.Cells["G56"];
PdfBookmarkEntry subbookmarkEntry1 = new PdfBookmarkEntry();
subbookmarkEntry1.Text = "Text1"; //最初のサブブックマーク
subbookmarkEntry1.Destination = cell;
subbookmarkEntry1.DestinationName = "AsposeCells--" + cell.Name;
cell = ws.Cells["L4"];
PdfBookmarkEntry subbookmarkEntry2 = new PdfBookmarkEntry();
subbookmarkEntry2.Text = "Text2"; //2番目のサブブックマーク
subbookmarkEntry2.Destination = cell;
subbookmarkEntry2.DestinationName = "AsposeCells--" + cell.Name;
```
これらのサブブックマークは本の章のように機能し、ユーザーをドキュメント内のより具体的なコンテンツに導きます。
### リストにサブブックマークを追加する
次に、先ほど作成したメインのブックマークの下にサブブックマークをグループ化します。
```csharp
ArrayList list = new ArrayList();
list.Add(subbookmarkEntry1);
list.Add(subbookmarkEntry2);
bookmarkEntry.SubEntry = list;
```
この構成により、ナビゲーションを簡素化する階層構造が作成されます。最適なユーザー エクスペリエンスを実現するには、「ブックマークの基本」に従ってください。
## ステップ5: ブックマーク付きのPDFを保存する
### PdfSaveOptions を作成する
PDF 保存オプションを作成し、作成したブックマークを追加します。
```csharp
PdfSaveOptions opts = new PdfSaveOptions();
opts.Bookmark = bookmarkEntry;
```
このステップでは、これまでの準備がすべて結集されます。基本的には、「PDF を単なるフラットなドキュメントではなく、インタラクティブなガイドにしたい」と言っていることになります。
### ドキュメントを保存する
最後に、ブックマークをこのアクションに組み込んで、ワークブックを PDF 形式で保存します。
```csharp
wb.Save(outputDir + "outputPdfBookmarkEntry_DestinationName.pdf", opts);
```
このように、あなたの努力はすべて報われ、便利なブックマークが満載された、よく構成された PDF ドキュメントが完成します。
## 結論
おめでとうございます! Aspose.Cells for .NET を使用して、ブックマークと名前付き宛先を含む PDF を正常に作成しました。Excel ファイル内を移動し、特定のセルにアクセスし、ユーザー操作を強化するブックマークを作成する方法を学習しました。これらの便利なブックマークを使用すると、PDF ドキュメント内を移動するのがどれだけ簡単になるか想像してみてください。
## よくある質問
### Aspose.Cells for .NET とは何ですか?
Aspose.Cells は、Excel ファイルの操作に使用できる強力なライブラリであり、プログラムによってスプレッドシートを作成、変更、変換できます。
### Aspose.Cells を無料プロジェクトで使用できますか?
はい！ライセンスを購入する前に機能を試してみたい場合は、Aspose では無料トライアルを提供しています。
### Aspose.Cells のライセンスを取得するにはどうすればよいですか?
ライセンスは直接購入することができます[購入ページ](https://purchase.aspose.com/buy).
### Aspose.Cells はどのような種類のドキュメントで使用できますか?
XLSX、XLS、CSV、PDF など、さまざまな形式で動作します。
### 問題が発生した場合、どこでサポートを受けることができますか?
サポートは[Aspose フォーラム](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
