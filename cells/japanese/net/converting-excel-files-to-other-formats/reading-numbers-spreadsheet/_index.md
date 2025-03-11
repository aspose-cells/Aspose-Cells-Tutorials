---
title: .NET でプログラム的に数値スプレッドシートを読み取る
linktitle: .NET でプログラム的に数値スプレッドシートを読み取る
second_title: Aspose.Cells .NET Excel 処理 API
description: この詳細なチュートリアルでは、Aspose.Cells for .NET を使用して Numbers スプレッドシートを読み取り、PDF に変換する方法を学習します。
weight: 18
url: /ja/net/converting-excel-files-to-other-formats/reading-numbers-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET でプログラム的に数値スプレッドシートを読み取る

## 導入
今日のデジタル世界では、データ管理は不可欠なスキルであり、スプレッドシートはデータ整理の最前線にあります。しかし、.NET を使用して、Apple の Numbers アプリで作成されたファイルである Numbers スプレッドシートを操作する必要がある場合はどうでしょうか。心配しないでください。あなただけではありません。このチュートリアルでは、Aspose.Cells for .NET を使用してプログラムで Numbers スプレッドシートを読み取るプロセスについて説明します。Numbers ファイルを読み込み、PDF に変換する方法を学習します。
## 前提条件
始める前に、準備しておくべきことがいくつかあります。
1. Aspose.Cells for .NET: Aspose.Cellsライブラリがインストールされていることを確認してください。ダウンロードできます。[ここ](https://releases.aspose.com/cells/net/).
2. Visual Studio: マシンに Visual Studio (またはその他の .NET 互換 IDE) をインストールしておくことをお勧めします。
3. C# の基礎知識: C# プログラミングに少し精通していると、スムーズに理解できるようになります。
4. ドキュメント ディレクトリ: Numbers ファイルが保存されるディレクトリと、変換された PDF を保存する場所が必要になります。
これらの前提条件を満たしたら、開始する準備は完了です。
## パッケージのインポート
まず、必要なパッケージを C# プロジェクトにインポートする必要があります。これは、Aspose.Cells ライブラリによって提供される機能を活用できるようになるため、重要なステップです。
1. Visual Studio で C# プロジェクトを開きます。
2. Aspose.Cells ライブラリへの参照を追加します。
   - NuGet を使用している場合は、パッケージ マネージャー コンソールで次のコマンドを実行するだけです。
```
 Install-Package Aspose.Cells
 ```
3. コードに必要な名前空間をインポートします。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
必要なパッケージをインポートしたので、Numbers スプレッドシートを読み取るためのステップバイステップ ガイドに進みましょう。
## ステップ1: ソースディレクトリと出力ディレクトリを指定する
この手順では、ソース Numbers ファイルが保存されているディレクトリと、出力 PDF を保存するディレクトリを設定します。
```csharp
//ソースディレクトリ
string sourceDir = "Your Document Directory"; //これを実際のディレクトリに更新します
//出力ディレクトリ
string outputDir = "Your Document Directory"; //これを実際のディレクトリに更新します
```
ここでは2つの文字列変数を定義しています。`sourceDir`そして`outputDir` 、入力ファイルと出力ファイルの場所を指定します。`"Your Document Directory"`システム上の実際のパスを使用します。
## ステップ2: 数値形式の読み込みオプションを設定する
次に、Numbers スプレッドシートを読み込むための読み込みオプションを指定します。この手順は、Aspose に Numbers ファイルの解釈方法を指示するため重要です。
```csharp
//読み込みオプションを指定します。Numbersスプレッドシートを読み込みたい場合
LoadOptions opts = new LoadOptions(LoadFormat.Numbers);
```
私たちは`LoadOptions`オブジェクトとフォーマットを次のように指定します`LoadFormat.Numbers`これにより、Aspose.Cells ライブラリに Numbers ファイルで作業していることが通知されます。 
## ステップ3: Numbersスプレッドシートをワークブックに読み込む
さて、実際のNumbersスプレッドシートを`Workbook`物体。
```csharp
//上記の読み込みオプションを使用して、Numbersスプレッドシートをワークブックに読み込みます。
Workbook wb = new Workbook(sourceDir + "sampleNumbersByAppleInc.numbers", opts);
```
我々は`Workbook`オブジェクトを作成し、読み込みオプションとともに Numbers ファイルのファイルパスを渡します。ファイル名 (`sampleNumbersByAppleInc.numbers`) は、Numbers ファイルの実際の名前と一致します。
## ステップ4: ワークブックをPDFとして保存する
Numbers ファイルが正常に読み込まれたら、次のステップはそれを別の形式、具体的には PDF で保存することです。
```csharp
//ワークブックをPDF形式で保存する
wb.Save(outputDir + "outputNumbersByAppleInc.pdf", SaveFormat.Pdf);
```
ここでは、`Save`方法`Workbook`オブジェクトに出力ファイルのパスと保存形式を指定します。この場合は PDF として保存します。出力ファイル名 (`outputNumbersByAppleInc.pdf`) は一意であり、既存のファイルを上書きしません。
## ステップ5: 成功を確認する
最後に、操作が成功したことを確認するメッセージを追加しましょう。
```csharp
Console.WriteLine("ReadNumbersSpreadsheet executed successfully.\r\n");
```
このコード行は、すべてが完了するとコンソールに成功メッセージを出力します。フィードバックがあるといつでも便利ですよね?
## 結論
これで完了です。Aspose.Cells for .NET を使用して Numbers スプレッドシートを正常に読み取り、PDF に変換できました。この強力なライブラリを使用すると、スプレッドシートを簡単に操作でき、データ管理タスクが簡単になります。アプリケーションを開発している場合でも、スプレッドシートをより効率的に処理する必要がある場合でも、Aspose.Cells はツールキットに組み込むと便利なツールです。
## よくある質問
### Aspose.Cells はどのような種類のファイルを読み取ることができますか?  
Aspose.Cells は、XLS、XLSX、CSV、Numbers ファイルなど、さまざまなファイル形式を読み取ることができます。 
### Aspose.Cells を使用して Numbers ファイルを編集できますか?  
はい、Aspose.Cells を使用して Numbers ファイルを読み取り、操作し、保存できます。
### Aspose.Cells は無料で使用できますか?  
 Aspose.Cellsは無料トライアルを提供していますが、延長使用にはライセンスが必要です。価格を確認してください。[ここ](https://purchase.aspose.com/buy).
### Numbers ファイルの読み込み中にエラーが発生した場合はどうすればよいですか?  
正しいロードオプションを使用していることと、ファイルパスが正確であることを確認してください。さらにサポートが必要な場合は、[Aspose サポート フォーラム](https://forum.aspose.com/c/cells/9).
### Aspose.Cells の一時ライセンスを取得するにはどうすればよいですか?  
一時ライセンスを申請することができます[ここ](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
