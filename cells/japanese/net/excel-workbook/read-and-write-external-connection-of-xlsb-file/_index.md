---
title: XLSB ファイルの外部接続の読み取りと書き込み
linktitle: XLSB ファイルの外部接続の読み取りと書き込み
second_title: Aspose.Cells for .NET API リファレンス
description: この包括的なチュートリアルでは、Aspose.Cells for .NET を使用して XLSB ファイル内の外部接続を管理する方法を学習します。
weight: 130
url: /ja/net/excel-workbook/read-and-write-external-connection-of-xlsb-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# XLSB ファイルの外部接続の読み取りと書き込み

## 導入

Excel 愛好家の皆さん、こんにちは。XLSB ファイルと外部接続の魅力的な世界に飛び込む準備はできていますか? Excel を使用したことがある方なら、Excel がいかに強力で多用途であるかをご存知でしょう。しかし、外部データベースへの接続を扱う場合は特に、Excel には癖があることが時々あります。そこで、Aspose.Cells for .NET が役に立ちます。この気の利いたライブラリを使用すると、Excel ファイルを簡単に操作できます。この記事では、XLSB ファイルで外部接続を読み書きする方法について、ステップ バイ ステップで説明します。

## 前提条件

始める前に、必要なものがいくつかあります。

1. C# の基礎知識: C# プログラミング言語の知識があると非常に役立ちます。C# コードの記述に慣れている場合は、そのまま進めます。
2.  Aspose.Cells for .NET: このライブラリを開発環境にインストールする必要があります。まだインストールしていない場合は、簡単にダウンロードできます。[ここ](https://releases.aspose.com/cells/net/). 
3. IDE: コード エディターまたは Visual Studio などの統合開発環境 (IDE) が必要です。 
4. サンプル XLSB ファイル: 外部接続を含むサンプル XLSB ファイルを使用します。独自のファイルを作成することも、サンプルをオンラインでダウンロードすることもできます。 

これらの前提条件がすべて整ったら、コードに取り掛かる準備が整います。

## パッケージのインポート

まず、プロジェクトに必要なパッケージをインポートしましょう。プロジェクトに Aspose.Cells への参照を追加したことを確認してください。C# でこれを行う方法は次のとおりです。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

これらのインポートにより、Excel ファイルとその接続を操作するために必要な機能にアクセスできるようになります。

## ステップ1: ディレクトリを設定する

XLSB ファイルで作業する前に、ソース ディレクトリと出力ディレクトリを設定する必要があります。この手順は、ファイルを整理しておくために不可欠です。

```csharp
//ソースディレクトリ
string sourceDir = "Your Document Directory";
//出力ディレクトリ
string outputDir = "Your Output Directory";
```

このコードスニペットでは、`"Your Document Directory"`そして`"Your Document Directory"`入力ファイルと出力ファイルが存在する場所のそれぞれのパスを取得するものと想定されています。必要に応じて、これらのメソッドをハードコードされたパスに置き換えることができます。

## ステップ2: XLSBファイルを読み込む

ここで、Excel ファイルを Workbook オブジェクトに読み込みます。これにより、内部のデータを操作できるようになります。

```csharp
//ソースExcel Xlsbファイルをロードする
Workbook wb = new Workbook(sourceDir + "sampleExternalConnection_XLSB.xlsb");
```

XLSBファイルが指定された場所にあることを確認してください`sourceDir`パスが正しければ、ワークブックを操作できるようになります。

## ステップ3: 外部接続にアクセスする

ワークブックが読み込まれると、外部接続にアクセスできるようになります。この例では、最初のデータベース接続を取得します。

```csharp
//実際にはDB接続である最初の外部接続を読み取ります
Aspose.Cells.ExternalConnections.DBConnection dbCon = wb.DataConnections[0] as Aspose.Cells.ExternalConnections.DBConnection;
```

ここ、`DataConnections[0]`ワークブックの最初の接続を参照します。これを`DBConnection`さらに操作するために入力します。

## ステップ4: 接続情報を抽出する

データベース接続にアクセスできるようになったので、その詳細を抽出してコンソールに出力してみましょう。これにより、何を操作しているのかを正確に把握できるようになります。

```csharp
// DB接続の名前、コマンド、接続情報を出力します。
Console.WriteLine("Connection Name: " + dbCon.Name);
Console.WriteLine("Command: " + dbCon.Command);
Console.WriteLine("Connection Info: " + dbCon.ConnectionInfo);
```

この手順では、外部接続の現在の状態を確認できます。接続名、使用されたコマンド、および接続情報がコンソールに表示されます。

## ステップ5: 接続を変更する

場合によっては、名前を変更するだけで、物事を明確にしたり、新しい命名規則に合わせたりすることができます。既存の接続名をより適切な名前に変更してみましょう。

```csharp
//接続名を変更する
dbCon.Name = "NewCust";
```

このコード行は、接続の名前を元の名前から「NewCust」に変更します。シンプルですが、インパクトのある変更です。

## ステップ6: 変更を保存する

変更を加えたら、変更内容を XLSB ファイルに保存します。手順は次のとおりです。

```csharp
// Excel Xlsbファイルを保存する
wb.Save(outputDir + "outputExternalConnection_XLSB.xlsb");
```

このコード行は、新しい接続名を含むすべての変更を保持しながら、更新されたワークブックを保存します。

## ステップ7: 実行を確認する

最後に、すべてがスムーズに動作したことを確認しましょう。最後に簡単なメッセージが表示され、それが明確になります。

```csharp
Console.WriteLine("ReadAndWriteExternalConnectionOfXLSBFile executed successfully.\r\n");
```

このメッセージは、コードが正常に実行され、すべての変更が期待どおりに保存されたことを保証します。

## 結論

これで完了です。Aspose.Cells for .NET を使用して XLSB ファイルで外部接続を読み書きする方法を学習できました。これらの手順に従うことで、Excel データ接続を効果的に管理でき、Excel での作業がはるかに効率化され、ストレスが軽減されます。大規模なデータセットを処理する場合でも、単に情報を整理する場合でも、Aspose.Cells には必要なツールが揃っています。

## よくある質問

### XLSB ファイルとは何ですか?  
XLSB ファイルは、スプレッドシート データをバイナリ形式で保存するバイナリ Excel ファイル形式であり、よりコンパクトで開くのが速くなります。

### Aspose.Cells for .NET をインストールするにはどうすればよいですか?  
 Asposeのウェブサイトから簡単にダウンロードできます[ここ](https://releases.aspose.com/cells/net/).

### Aspose.Cells を無料で使用できますか?  
はい！無料トライアルから始めることができます。[ここ](https://releases.aspose.com/).

### Aspose.Cells は他のファイル形式をサポートしていますか?  
もちろんです! Aspose.Cells は、XLSX、CSV など、さまざまなファイル形式をサポートしています。

### 問題が発生した場合、どこでサポートを受けることができますか?  
Asposeフォーラムからサポートを受けることができます[ここ](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
