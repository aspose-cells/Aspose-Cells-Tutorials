---
title: Excel 他のブックからワークシートをコピーする
linktitle: Excel 他のブックからワークシートをコピーする
second_title: Aspose.Cells for .NET API リファレンス
description: このステップバイステップ ガイドでは、Aspose.Cells for .NET を使用して、ある Excel ワークブックから別の Excel ワークブックにワークシートをコピーする方法を学習します。
weight: 10
url: /ja/net/excel-copy-worksheet/excel-copy-worksheet-from-other-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel 他のブックからワークシートをコピーする

## 導入

複数の Excel ワークブックを扱い、データを整理して簡単にアクセスできるようにしようと苦労したことはありませんか? もしそうなら、それはあなただけではありません! 私たちの多くは、仕事や個人のプロジェクトで、さまざまなファイルを扱います。朗報は、Aspose.Cells for .NET のちょっとした助けを借りて、あなたの生活を楽にすることができるということです。この強力なライブラリを使用すると、ワークシートを 1 つのワークブックから別のワークブックにコピーするなど、Excel ファイルを簡単に操作できます。このガイドでは、そのための手順を順を追って説明し、ワークフローを合理化して生産性を向上させることができるようにします。

## 前提条件

コーディングの作業に入る前に、必要なものをすべて揃えましょう。心配しないでください。これはロケット科学ではありません。必要なものは次のとおりです。

1. Visual Studio (または任意の .NET IDE): マシンに .NET 開発環境が設定されている必要があります。
2.  Aspose.Cells for .NET: Aspose.Cellsをダウンロードしてインストールする必要があります。まだお持ちでない場合は、[ここ](https://releases.aspose.com/cells/net/).
3. C# の基本的な理解: C# プログラミングに少し慣れていると、この作業はよりスムーズになりますが、まだ始めたばかりでも心配する必要はありません。
4. .NET Framework: プロジェクトが互換性のあるバージョンの .NET Framework をターゲットにしていることを確認します。
5. システム設定: 制限なくアプリケーションを実行およびテストできることを確認します。

準備が整ったので、コーディングを始めましょう。

## パッケージのインポート

機能の実装を始める前に、必要なパッケージをインポートする必要があります。こうすることで、Aspose.Cells が提供するすべての機能にアクセスできるようになります。手順は次のとおりです。

### Usingステートメントを追加する

C# ファイルを開き、先頭に次の using ディレクティブを追加します。

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

このパッケージは Aspose ライブラリの中核であり、すべてのクラスとメソッドにアクセスできるようになります。

これで準備がすべて整いました。次は、実際にワークシートをあるワークブックから別のワークブックにコピーするという楽しい作業に取り掛かりましょう。これをいくつかの明確な手順に分解します。

## ステップ1: ドキュメントディレクトリを設定する

まず、Excel ファイルを保存する場所を指定する必要があります。ドキュメント ディレクトリのパスを定義します。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";  //これを実際のディレクトリに更新します
```
の`dataDir`変数には、最終的な Excel ファイルを保存するパスが格納されます。「YOUR DOCUMENT DIRECTORY」をシステム上の実際のパスに置き換えてください。

## ステップ2: 新しいワークブックを作成し、データを入力する

次に、最初のワークブックを作成し、サンプル データを追加してみましょう。手順は次のとおりです。

```csharp
//新しいワークブックを作成する
Workbook excelWorkbook0 = new Workbook();
//本の最初のワークシートを入手する
Worksheet ws0 = excelWorkbook0.Worksheets[0];

//ヘッダー行にデータを入れる（A1:A4）
for (int i = 0; i < 5; i++)
{
    ws0.Cells[i, 0].PutValue(string.Format("Header Row {0}", i));
}

//詳細データを入力します（A5:A999）
for (int i = 5; i < 1000; i++)
{
    ws0.Cells[i, 0].PutValue(string.Format("Detail Row {0}", i));
}
```
ここでは、最初のワークブックを作成し、最初のワークシートにデータを入力します（`ws0`) にヘッダーと詳細行を追加します。このシミュレートされたデータは、後でコピー プロセスを視覚化するのに役立ちます。

## ステップ3: 印刷用のページ設定を行う

印刷時にヘッダー行を繰り返すようにページ設定を構成して、その機能が実際に動作するか確認してみましょう。

```csharp
//最初のワークシートに基づいてページ設定オブジェクトを定義する
PageSetup pagesetup = ws0.PageSetup;
//最初の5行は各ページで繰り返されます
pagesetup.PrintTitleRows = "$1:$5";
```
この部分は文書の印刷方法を定義します。`PrintTitleRows`、最初の 5 行がすべての印刷ページに表示されるようにし、読みやすさの向上に非常に役立ちます。

## ステップ4: 2番目のワークブックを作成する

ここで、最初のワークシートをコピーする別のワークブックを作成する必要があります。

```csharp
//別のワークブックを作成する
Workbook excelWorkbook1 = new Workbook();
//本の最初のワークシートを入手する
Worksheet ws1 = excelWorkbook1.Worksheets[0];
//ワークシートに名前を付ける
ws1.Name = "MySheet";
```
新しいワークブックを作成しました（`excelWorkbook1`) を作成し、最初のワークシートの名前を「MySheet」に変更しました。後で簡単にアクセスできるように、シートに意味のある名前を付けることをお勧めします。

## ステップ5: ワークシートをコピーする

最初のワークブックのワークシートの内容を 2 番目のワークブックにコピーしてみましょう。

```csharp
//最初のワークブックの最初のワークシートからデータをコピーし、
// 2番目のワークブックの最初のワークシート
ws1.Copy(ws0);
```
の`Copy`メソッドはソースワークシートからすべてのコンテンツを取得します（`ws0`）をコピーし、コピー先のワークシート（`ws1`）。とても簡単ですよね？

## ステップ6: 新しいワークブックを保存する

最後に、新しく作成したワークブックを保存します。

```csharp
// Excelファイルを保存する
excelWorkbook1.Save(dataDir + "CopyWorksheetFromWorkbookToOther_out.xls");
```
この行は、指定されたパスに 2 番目のワークブックを保存します。コードを実行した後、すべてが正常であることを確認することを忘れないでください。

## 結論

これで完了です。Aspose.Cells for .NET を使用して、ワークシートを 1 つのワークブックから別のワークブックにコピーする方法を学習しました。これは、特に複数のファイルに分散している大量のデータを処理する場合に非常に便利なスキルです。わずか数行のコードで、Excel データを整理、管理、アクセスすることがはるかに簡単になります。

## よくある質問

### Aspose.Cells とは何ですか?  
Aspose.Cells は、開発者がさまざまな形式で Excel ファイルを作成、操作、変換、レンダリングできるようにする .NET ライブラリです。

### Aspose.Cells を無料で使用できますか?  
はい、Aspose.Cellsは無料トライアルを提供しており、[ここ](https://releases.aspose.com/).

### Aspose.Cells の一時ライセンスを取得するにはどうすればよいですか?  
一時ライセンスを申請するには、[このリンク](https://purchase.aspose.com/temporary-license/).

### Aspose.Cells に関する詳細なドキュメントはどこで見つかりますか?  
詳細なドキュメントは以下をご覧ください[ここ](https://reference.aspose.com/cells/net/).

### Aspose.Cells ユーザー向けのサポートはありますか?  
もちろんです！[Aspose フォーラム](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
