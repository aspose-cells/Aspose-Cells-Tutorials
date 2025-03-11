---
title: HTML に保存する際に下位レベルの公開コメントを無効にする
linktitle: HTML に保存する際に下位レベルの公開コメントを無効にする
second_title: Aspose.Cells .NET Excel 処理 API
description: この詳細なステップバイステップ ガイドでは、Aspose.Cells for .NET を使用して Excel ブックを HTML に保存するときに、ダウンレベルの公開コメントを無効にする方法を学習します。
weight: 11
url: /ja/net/loading-and-saving-excel-files-with-options/disabling-downlevel-revealed-comments/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# HTML に保存する際に下位レベルの公開コメントを無効にする

## 導入
Excel ワークブックを HTML に変換する必要があり、その過程で不要なコメントや非表示のコンテンツが表示されないようにしたいと思ったことはありませんか? ダウンレベルの表示コメントを無効にすると便利です。Aspose.Cells for .NET を使用している場合は、Excel ワークブックを HTML ファイルとしてレンダリングする方法を完全に制御できます。このチュートリアルでは、ワークブックを HTML に保存する際にダウンレベルの表示コメントを無効にするための簡単な手順を順を追って説明します。 
この記事を読み終える頃には、この機能の使い方を明確に理解し、HTML 出力がクリーンでコメントのないものになるよう保証できるようになります。
## 前提条件
ステップバイステップのガイドに進む前に、スムーズに進めるために必要ないくつかの事項について説明しておきましょう。
1. Aspose.Cells for .NET: Aspose.Cellsライブラリをインストールする必要があります。まだインストールしていない場合は、ダウンロードできます。[ここ](https://releases.aspose.com/cells/net/).
2. IDE: C# コードを記述して実行するための Visual Studio のような開発環境。
3. C# の基礎知識: C# 構文とオブジェクト指向プログラミングに精通していると、コードを理解するのに役立ちます。
4. 一時版またはライセンス版: 無料トライアルを使用するか、一時ライセンスを申請することができます。[ここ](https://purchase.aspose.com/temporary-license/)これにより、ライブラリが制限なく動作することが保証されます。
準備が整いましたので、早速始めましょう!
## 名前空間のインポート
コード例に入る前に、Aspose.Cells に必要な名前空間を含めることが重要です。これらがないと、コードは Excel ファイルの操作に必要なメソッドとプロパティにアクセスできません。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Aspose.Cells 名前空間をインポートするには、この行を C# ファイルの先頭に配置するようにしてください。
## ステップ1: ディレクトリパスを設定する
まず最初に、ソース ディレクトリ (Excel ファイルが保存される場所) と出力ディレクトリ (HTML ファイルが保存される場所) を設定する必要があります。Aspose.Cells ではファイルにアクセスして保存するために正確なファイル パスが必要なので、これは非常に重要です。
```csharp
// Excel ファイルが保存されているソース ディレクトリ
string sourceDir = "Your Document Directory";
//結果のHTMLファイルが保存される出力ディレクトリ
string outputDir = "Your Document Directory";
```
このステップでは、`"Your Document Directory"`システム上の実際のファイル パスを使用します。入力ファイルと出力ファイルを整理するために、カスタム ディレクトリを作成することもできます。
## ステップ2: Excelワークブックを読み込む
このステップでは、Excelブックをメモリにロードして操作できるようにします。デモの目的で、サンプルファイルを使用します。`"sampleDisableDownlevelRevealedComments.xlsx"`好みのワークブックを使用できます。
```csharp
//ソースディレクトリからサンプルワークブックをロードします
Workbook wb = new Workbook(sourceDir + "sampleDisableDownlevelRevealedComments.xlsx");
```
これにより、Excel ファイルのすべてのデータと構造を含む Workbook オブジェクトが作成されます。ここから、それを変更したり、設定を適用したり、最終的に別の形式で保存したりできます。
## ステップ3: HTML保存オプションを設定する
ここで、HtmlSaveOptions オブジェクトを構成して、ダウンレベルの公開コメントを無効にする必要があります。このオプションにより、結果の HTML ファイルでコメントや非表示のコンテンツが公開されなくなります。
```csharp
//保存オプションを設定するために新しいHtmlSaveOptionsオブジェクトを作成します
HtmlSaveOptions opts = new HtmlSaveOptions();
//下位レベルの公開コメントを無効にする
opts.DisableDownlevelRevealedComments = true;
```
設定により`DisableDownlevelRevealedComments`に`true`ブックを HTML ファイルとして保存すると、下位レベルのコメントが無効になります。
## ステップ4: ワークブックをHTMLとして保存する
HtmlSaveOptions オブジェクトを構成したら、次の手順では、指定されたオプションを使用してワークブックを HTML に保存します。ここで実際のファイル変換が行われます。
```csharp
//指定した保存オプションを使用して、ワークブックを HTML ファイルとして保存します。
wb.Save(outputDir + "outputDisableDownlevelRevealedComments_true.html", opts);
```
このコード行では、先ほど指定した出力ディレクトリにブックを保存し、DisableDownlevelRevealedComments 設定を適用しています。その結果、不要なコメントのないクリーンな HTML ファイルが作成されます。
## ステップ5: 検証と実行
最後に、すべてが期待どおりに動作したことを確認するために、コンソールに成功メッセージを出力できます。
```csharp
//コンソールに成功メッセージを出力する
Console.WriteLine("DisableDownlevelRevealedCommentsWhileSavingToHTML executed successfully.");
```
これにより、操作がエラーなしで完了したことが分かります。
## 結論
これで完了です。Aspose.Cells for .NET を使用して Excel ワークブックを HTML に保存する際に、ダウンレベルの公開コメントを無効にする方法を学習しました。この機能を使用すると、ワークブックを HTML としてレンダリングする方法を制御し、不要なコンテンツが公開されないようにすることができます。Web アプリを開発している場合でも、単にクリーンな HTML 出力が必要な場合でも、この方法により、ワークブックの変換が正確かつ安全になります。
このチュートリアルが役に立った場合は、Excel 処理機能をさらに強化するために、Aspose.Cells の他の機能を検討することを検討してください。
## よくある質問
### ダウンレベルの公開コメントとは何ですか?
ダウンレベルの公開コメントは、通常、Web 開発で、特定の HTML 機能をサポートしていない古いブラウザーに追加情報を提供するために使用されます。Excel から HTML への変換では、非表示のコンテンツやコメントが表示されることがあるため、無効にすると便利です。
### 必要に応じてダウンレベルコメントを有効にすることはできますか?
はい、設定するだけで`DisableDownlevelRevealedComments`財産に`false`ワークブックを HTML として保存するときにダウンレベル コメントを有効にする場合。
### Aspose.Cells の一時ライセンスを取得するにはどうすればよいですか?
一時ライセンスは、次のサイトにアクセスして簡単に申請できます。[Aspose ウェブサイト](https://purchase.aspose.com/temporary-license/).
### ダウンレベルコメントを無効にすると、HTML の外観に影響しますか?
いいえ、ダウンレベルの公開コメントを無効にしても、HTML 出力の外観には影響しません。古いブラウザ向けの追加情報の公開を防ぐだけです。
### ワークブックを HTML 以外の形式で保存できますか?
はい、Aspose.CellsはPDF、CSV、TXTなどのさまざまな出力形式をサポートしています。[ドキュメント](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
