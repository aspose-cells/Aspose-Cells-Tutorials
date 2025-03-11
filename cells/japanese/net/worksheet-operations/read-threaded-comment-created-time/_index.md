---
title: ワークシート内のスレッドコメントの作成時刻を読み取る
linktitle: ワークシート内のスレッドコメントの作成時刻を読み取る
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して、Excel のスレッド コメントの作成時間を読み取る方法を学びます。コード例を含むステップ バイ ステップ ガイドです。
weight: 21
url: /ja/net/worksheet-operations/read-threaded-comment-created-time/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ワークシート内のスレッドコメントの作成時刻を読み取る

## 導入
Excel ファイルで作業する場合、コメントの管理はデータの共同作業とフィードバックの重要な側面になります。Aspose.Cells for .NET を使用している場合は、スレッド化されたコメントを含むさまざまな Excel 機能の処理に非常に役立つことがわかります。このチュートリアルでは、ワークシート内のスレッド化されたコメントの作成時間を読み取る方法に焦点を当てます。熟練した開発者でも、初心者でも、このガイドはプロセスをステップごとに説明します。
## 前提条件
コードに進む前に、始めるのに必要なものがすべて揃っていることを確認しましょう。
1. Aspose.Cells for .NET: Aspose.Cellsライブラリがインストールされていることを確認してください。[Aspose ウェブサイト](https://releases.aspose.com/cells/net/).
2. Visual Studio: C# コードを記述して実行できる Visual Studio またはその他の .NET IDE の稼働インストール。
3. C# の基礎知識: C# プログラミングに精通していると、コード スニペットをよりよく理解できるようになります。
4.  Excelファイル: スレッド化されたコメントが入ったExcelファイルを用意してください。この例では、`ThreadedCommentsSample.xlsx`.
前提条件を満たしたので、必要なパッケージをインポートしましょう。
## パッケージのインポート
Aspose.Cells を使い始めるには、必要な名前空間をインポートする必要があります。手順は次のとおりです。
### Aspose.Cells 名前空間をインポートする
Visual Studio で C# プロジェクトを開き、コード ファイルの先頭に次の using ディレクティブを追加します。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
この名前空間を使用すると、Aspose.Cells ライブラリによって提供されるすべてのクラスとメソッドにアクセスできます。
準備ができたので、スレッド化されたコメントの作成時間を読み取るプロセスを、管理しやすいステップに分解してみましょう。
## ステップ1: ソースディレクトリを定義する
まず、Excel ファイルが保存されているディレクトリを指定する必要があります。プログラムがファイルの場所を知る必要があるため、これは非常に重要です。
```csharp
//ソースディレクトリ
string sourceDir = "Your Document Directory";
```
交換する`"Your Document Directory"`Excelファイルへの実際のパスを入力します。これは次のようになります。`"C:\\Documents\\"`.
## ステップ2: ワークブックを読み込む
次に、スレッド化されたコメントを含む Excel ブックを読み込みます。手順は次のとおりです。
```csharp
Workbook workbook = new Workbook(sourceDir + "ThreadedCommentsSample.xlsx");
```
このコード行は新しい`Workbook`指定された Excel ファイルを読み込んでオブジェクトを作成します。ファイルが見つからない場合は例外がスローされるため、パスが正しいことを確認してください。
## ステップ3: ワークシートにアクセスする
ワークブックが読み込まれたら、次のステップはコメントを含む特定のワークシートにアクセスすることです。この場合は、最初のワークシートにアクセスします。
```csharp
//最初のワークシートにアクセスする
Worksheet worksheet = workbook.Worksheets[0];
```
この行は、ワークブックから最初のワークシート (インデックス 0) を取得します。コメントが別のワークシートにある場合は、それに応じてインデックスを調整します。
## ステップ4: スレッド化されたコメントを取得する
ここで、特定のセルからスレッド化されたコメントを取得します。 この例では、セル A1 からコメントを取得します。
```csharp
//スレッドコメントを取得する
ThreadedCommentCollection threadedComments = worksheet.Comments.GetThreadedComments("A1");
```
この行は、セル A1 に関連付けられたすべてのスレッド化されたコメントを取得します。コメントがない場合、コレクションは空になります。
## ステップ5: コメントを繰り返す
スレッド化されたコメントを取得したら、それらをループして、作成時刻を含む詳細を表示できます。
```csharp
foreach (ThreadedComment comment in threadedComments)
{
    Console.WriteLine("Comment: " + comment.Notes);
    Console.WriteLine("Author: " + comment.Author.Name);
    Console.WriteLine("Created Time: " + comment.CreatedTime);
}
```
このループは、`threadedComments`コレクションを読み取り、コメントのテキスト、作成者の名前、コメントが作成された時刻を出力します。
## ステップ6: 確認メッセージ
最後に、コメント読み取りロジックを実行した後は、常に確認メッセージを提供することをお勧めします。これはデバッグに役立ち、コードが正常に実行されたことを保証します。
```csharp
Console.WriteLine("ReadThreadedCommentCreatedTime executed successfully.");
```
## 結論
おめでとうございます! Aspose.Cells for .NET を使用して、Excel ワークシート内のスレッド化されたコメントの作成時間を読み取る方法を学習しました。この機能は、Excel ドキュメントでのフィードバックや共同作業を追跡するのに非常に役立ちます。わずか数行のコードで、データ分析やレポート作成のプロセスを強化できる貴重な情報を抽出できます。
## よくある質問
### Aspose.Cells for .NET とは何ですか?
Aspose.Cells for .NET は、開発者が .NET アプリケーションで Excel ファイルを作成、操作、変換できるようにする強力なライブラリです。
### Aspose.Cells for .NET をダウンロードするにはどうすればいいですか?
ダウンロードはこちらから[Aspose ウェブサイト](https://releases.aspose.com/cells/net/).
### 無料トライアルはありますか？
はい、Aspose.Cellsを無料でお試しいただけます。[無料トライアルページ](https://releases.aspose.com/).
### 他のセルからコメントにアクセスできますか?
もちろんです！セル参照は`GetThreadedComments`任意のセルからコメントにアクセスする方法。
### Aspose.Cells のサポートはどこで受けられますか?
サポートについては、[Aspose フォーラム](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
