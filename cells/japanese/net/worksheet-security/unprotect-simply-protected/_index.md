---
title: Aspose.Cells を使用して単純に保護されたワークシートの保護を解除する
linktitle: Aspose.Cells を使用して単純に保護されたワークシートの保護を解除する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用すると、パスワードなしで Excel ワークシートの保護を簡単に解除できます。セットアップ、コード手順、出力のシームレスな保存について学習します。
weight: 20
url: /ja/net/worksheet-security/unprotect-simply-protected/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells を使用して単純に保護されたワークシートの保護を解除する

## 導入
Excel ワークシートの保護を解除すると、ロックされたセルを変更したりデータを更新したりする必要がある場合に非常に便利です。Aspose.Cells for .NET を使用すると、コードを通じてシームレスにこれを実行できるため、保護されているだけのワークシートであればパスワードを必要とせずにワークシートの保護解除を自動化できます。このチュートリアルでは、前提条件の設定から必要なコードの記述まで、シンプルでありながら効果的な方法で、各手順を順を追って説明します。
## 前提条件
始める前に、Aspose.Cells for .NET を使用してワークシートの保護を解除するために必要なすべての準備が整っていることを確認しましょう。
-  Aspose.Cells for .NET: Excelファイルをプログラム的に操作するにはこのライブラリが必要です。ダウンロードは以下から行えます。[Aspose.Cells ダウンロード ページ](https://releases.aspose.com/cells/net/)または、その広範な[ドキュメント](https://reference.aspose.com/cells/net/).
- 開発環境: Visual Studio などの .NET アプリケーションに適した環境。
- C# の基本的な理解: コード例を理解するには、C# プログラミングの基本的な知識が役立ちます。
## パッケージのインポート
.NET プロジェクトで Aspose.Cells を使用するには、まず Aspose.Cells ライブラリをインポートする必要があります。これは、Aspose.Cells NuGet パッケージをプロジェクトに追加することで実行できます。以下に簡単なガイドを示します。
1. Visual Studio でプロジェクトを開きます。
2. ソリューション エクスプローラーで、プロジェクトを右クリックし、[NuGet パッケージの管理] を選択します。
3. 「Aspose.Cells」を検索し、最新バージョンをインストールします。
4. インストールしたら、コード ファイルの先頭に次のインポートを追加します。
```csharp
using System.IO;
using Aspose.Cells;
```
それでは、Excel ワークシートの保護を解除する実際のプロセスについて詳しく見ていきましょう。
プロセスをわかりやすい手順に分解してみましょう。この例では、作業中のワークシートにパスワードで保護されたロックがないことを前提としています。
## ステップ1: ファイルディレクトリを設定する
このステップでは、Excel ファイルが保存されているディレクトリを指定します。これにより、入力ファイルにアクセスしやすくなり、出力ファイルを目的の場所に保存しやすくなります。
```csharp
//ドキュメント ディレクトリへのパス。
string dataDir = "Your Document Directory";
```
ディレクトリパスを設定することで`dataDir`を使用すると、完全なパスを繰り返し入力しなくてもファイルにアクセスして保存するための便利なショートカットを作成できます。
## ステップ2: Excelワークブックを読み込む
さて、作業したいExcelファイルを読み込みましょう。ここでは、`Workbook` Excel ファイル全体を表すオブジェクト。
```csharp
//ワークブックオブジェクトのインスタンス化
Workbook workbook = new Workbook(dataDir + "book1.xls");
   ```
の`Workbook`オブジェクトはAspose.Cellsのコア部分であり、Excelファイルに対してさまざまなアクションを実行できます。`"book1.xls"`この行は、ターゲット ファイルをプログラムに読み込みます。
## ステップ3: 保護を解除したいワークシートにアクセスする
ワークブックが読み込まれたら、次の手順では、保護を解除するワークシートを指定します。この例では、ワークブックの最初のワークシートにアクセスします。
```csharp
// Excelファイルの最初のワークシートにアクセスする
Worksheet worksheet = workbook.Worksheets[0];
```
の`Worksheets`プロパティを使用すると、ワークブック内のすべてのワークシートにアクセスできます。`[0]`、最初のワークシートにアクセスしています。ターゲット ワークシートが別の位置にある場合は、このインデックスを調整できます。
## ステップ4: ワークシートの保護を解除する
ここで、重要な部分、つまりワークシートの保護を解除します。このチュートリアルは、単純に保護されたワークシート (パスワードのないワークシート) に焦点を当てているため、保護の解除は簡単です。
```csharp
//パスワードなしでワークシートの保護を解除する
worksheet.Unprotect();
```
ここ、`Unprotect()`は、`worksheet`オブジェクト。パスワードで保護されていないシートを扱っているので、追加のパラメータは必要ありません。これでワークシートの保護が解除され、編集可能になります。
## ステップ5: 更新されたワークブックを保存する
ワークシートの保護を解除したら、ワークブックを保存する必要があります。元のファイルを上書きするか、新しいファイルとして保存するかを選択できます。
```csharp
//ワークブックを保存する
workbook.Save(dataDir + "output.xls", SaveFormat.Excel97To2003);
```
この行では、`Save`方法。`SaveFormat.Excel97To2003`ブックが古い Excel 形式で保存されることを保証します。これは互換性が懸念される場合に役立ちます。新しいバージョンの Excel を使用している場合は、形式を変更してください。
## 結論
これで完了です。わずか数行のコードで、Aspose.Cells for .NET を使用して、Excel ファイル内の単純に保護されたワークシートの保護を解除できました。この方法は、Excel ファイル内のタスクを自動化するのに最適で、時間と労力を節約できます。さらに、Aspose.Cells を使用すると、Excel ファイルをプログラムで管理および操作するための強力なツールが備わり、スプレッドシート ワークフローを自動化するための可能性が広がります。
## よくある質問
### Aspose.Cells for .NET とは何ですか?
Aspose.Cells for .NET は、.NET アプリケーションで Excel ファイルを操作するための強力なライブラリです。Microsoft Excel をインストールしなくても、Excel ファイルを作成、編集、変換、操作できます。
### この方法でパスワードで保護されたワークシートの保護を解除できますか?
いいえ、この方法は単純に保護されたワークシートにのみ有効です。パスワードで保護されたシートの場合は、`Unprotect()`方法。
### Aspose.Cells を使用するには Microsoft Excel をインストールする必要がありますか?
いいえ、Aspose.Cells は Microsoft Excel とは独立して動作するため、システムにインストールする必要はありません。
### 保護されていないワークシートを新しい Excel 形式で保存できますか?
はい、可能です。Aspose.Cellsは、以下の複数の形式をサポートしています。`XLSX`保存形式を適宜変更してください。`Save`方法。
### Aspose.Cells は .NET 以外のプラットフォームでも使用できますか?
はい、Aspose.Cells には Java およびその他のプラットフォーム用のバージョンがあり、さまざまなプログラミング環境で同様の機能を使用できます。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
