---
"description": "この詳細なチュートリアルでは、Aspose.Cells for .NET を使用して Numbers スプレッドシートを読み取り、PDF に変換する方法を学習します。"
"linktitle": ".NET でプログラム的に数値スプレッドシートを読み取る"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": ".NET でプログラム的に数値スプレッドシートを読み取る"
"url": "/ja/net/converting-excel-files-to-other-formats/reading-numbers-spreadsheet/"
"weight": 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# .NET でプログラム的に数値スプレッドシートを読み取る

## 導入
今日のデジタル世界では、データ管理は不可欠なスキルであり、スプレッドシートはデータ整理の最前線に立っています。しかし、AppleのNumbersアプリで作成されたNumbersスプレッドシートを.NETで操作する必要がある場合はどうでしょうか？ご安心ください。あなただけではありません！このチュートリアルでは、Aspose.Cells for .NETを使ってNumbersスプレッドシートをプログラムで読み込むプロセスを解説します。Numbersファイルを読み込んでPDFに変換する方法も学習します。
## 前提条件
始める前に、いくつか準備しておくべきことがあります。
1. Aspose.Cells for .NET: Aspose.Cellsライブラリがインストールされていることを確認してください。ダウンロードできます。 [ここ](https://releases。aspose.com/cells/net/).
2. Visual Studio: お使いのマシンに Visual Studio (またはその他の .NET 互換 IDE) をインストールしておくことをお勧めします。
3. C# の基本知識: C# プログラミングに少し精通していれば、スムーズに理解できるようになります。
4. ドキュメント ディレクトリ: Numbers ファイルが保存されるディレクトリと、変換された PDF を保存する場所が必要になります。
これらの前提条件を満たしたら、開始する準備は完了です。
## パッケージのインポート
まず、必要なパッケージをC#プロジェクトにインポートする必要があります。これは、Aspose.Cellsライブラリが提供する機能を活用できるようになるため、非常に重要なステップです。
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
この手順では、ソースの Numbers ファイルが保存されているディレクトリと、出力 PDF を保存するディレクトリを設定します。
```csharp
// ソースディレクトリ
string sourceDir = "Your Document Directory"; // これを実際のディレクトリに更新します
// 出力ディレクトリ
string outputDir = "Your Document Directory"; // これを実際のディレクトリに更新します
```
ここでは2つの文字列変数を定義しています。 `sourceDir` そして `outputDir`入力ファイルと出力ファイルの場所を指定します。 `"Your Document Directory"` システム上の実際のパスを使用します。
## ステップ2: 数値形式の読み込みオプションを設定する
次に、Numbersスプレッドシートを読み込むための読み込みオプションを指定します。この手順は、AsposeにNumbersファイルをどのように解釈するかを指示するため、非常に重要です。
```csharp
// 読み込みオプションを指定します。Numbersスプレッドシートを読み込みたい場合
LoadOptions opts = new LoadOptions(LoadFormat.Numbers);
```
私たちは `LoadOptions` オブジェクトとフォーマットを次のように指定します `LoadFormat.Numbers`これにより、Aspose.Cells ライブラリに Numbers ファイルで作業していることが伝えられます。 
## ステップ3: Numbersスプレッドシートをワークブックに読み込む
さて、実際のNumbersスプレッドシートを `Workbook` 物体。
```csharp
// 上記の読み込みオプションを使用して、Numbersスプレッドシートをワークブックに読み込みます。
Workbook wb = new Workbook(sourceDir + "sampleNumbersByAppleInc.numbers", opts);
```
インスタンス化します `Workbook` オブジェクトを作成し、読み込みオプションとともにNumbersファイルのファイルパスを渡します。ファイル名（`sampleNumbersByAppleInc.numbers`) は、Numbers ファイルの実際の名前と一致します。
## ステップ4: ワークブックをPDFとして保存する
Numbers ファイルが正常に読み込まれたら、次のステップはそれを別の形式、具体的には PDF で保存することです。
```csharp
// ワークブックをPDF形式で保存する
wb.Save(outputDir + "outputNumbersByAppleInc.pdf", SaveFormat.Pdf);
```
ここでは、 `Save` 方法 `Workbook` オブジェクトに出力ファイルのパスと保存形式を指定します。この場合はPDFとして保存します。出力ファイル名（`outputNumbersByAppleInc.pdf`) は一意であり、既存のファイルを上書きしません。
## ステップ5: 成功を確認する
最後に、操作が成功したことを確認するメッセージを追加しましょう。
```csharp
Console.WriteLine("ReadNumbersSpreadsheet executed successfully.\r\n");
```
このコード行は、すべてが完了するとコンソールに成功メッセージを表示します。フィードバックがあるといつも嬉しいですね。
## 結論
これで完了です！Aspose.Cells for .NET を使って、Numbers スプレッドシートを読み込み、PDF に変換できました。この強力なライブラリを使えば、スプレッドシートを簡単に操作でき、データ管理作業が楽になります。アプリケーションを開発している場合でも、スプレッドシートをより効率的に処理したい場合でも、Aspose.Cells はツールキットにぜひ加えておきたい素晴らしいツールです。
## よくある質問
### Aspose.Cells はどのような種類のファイルを読み取ることができますか?  
Aspose.Cells は、XLS、XLSX、CSV、Numbers ファイルなど、さまざまなファイル形式を読み取ることができます。 
### Aspose.Cells を使用して Numbers ファイルを編集できますか?  
はい、Aspose.Cells を使用して Numbers ファイルを読み取り、操作し、保存できます。
### Aspose.Cells は無料で使用できますか?  
Aspose.Cellsは無料トライアルを提供していますが、長期間使用するにはライセンスが必要です。価格をご確認ください。 [ここ](https://purchase。aspose.com/buy).
### Numbers ファイルの読み込み中にエラーが発生した場合はどうすればよいですか?  
正しい読み込みオプションを使用していること、およびファイルパスが正確であることを確認してください。さらにサポートが必要な場合は、 [Aspose サポートフォーラム](https://forum。aspose.com/c/cells/9).
### Aspose.Cells の一時ライセンスを取得するにはどうすればよいですか?  
一時ライセンスを申請できます [ここ](https://purchase。aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}