---
title: .NET でワークブックを厳密な Open XML スプレッドシート形式で保存する
linktitle: .NET でワークブックを厳密な Open XML スプレッドシート形式で保存する
second_title: Aspose.Cells .NET Excel 処理 API
description: この詳細なチュートリアルでは、Aspose.Cells for .NET を使用して、Strict Open XML スプレッドシート形式でブックを保存する方法を学習します。
weight: 19
url: /ja/net/converting-excel-files-to-other-formats/saving-workbook-to-strict-open-xml-spreadsheet-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET でワークブックを厳密な Open XML スプレッドシート形式で保存する

## 導入
こんにちは! .NET を使用して Excel ファイル操作の世界に飛び込んでいるなら、ここは正しい場所です。今日は、Aspose.Cells for .NET を使用して Strict Open XML スプレッドシート形式でワークブックを保存する方法について説明します。Excel ファイルで最大限の互換性と標準への準拠を確保するには、この形式が不可欠です。誰もが評価できる、美しく仕上げられた高品質のドキュメントを作成すると考えてください。
それで、あなたにとって何のメリットがあるのでしょうか? このガイドを読み終えると、この形式でワークブックを保存する方法だけでなく、Aspose.Cells を使用して Excel ファイルを操作する方法についてもしっかりと理解できるようになります。準備はできましたか? さあ、始めましょう!
## 前提条件
コードに進む前に、必要なものがすべて揃っていることを確認しましょう。必要なものは次のとおりです。
1.  Visual Studio: お使いのマシンにVisual Studioがインストールされていることを確認してください。まだインストールされていない場合は、ダウンロードできます。[ここ](https://visualstudio.microsoft.com/).
2.  Aspose.Cells for .NET: プロジェクトに Aspose.Cells を追加する必要があります。サイトからダウンロードするか、Visual Studio の NuGet パッケージ マネージャーを使用することができます。パッケージは次の場所にあります。[ここ](https://releases.aspose.com/cells/net/).
3. C# の基礎知識: C# プログラミングの基本的な概念を理解している必要があります。以前にコーディングを経験したことがあるなら、問題ありません。
4. 出力ディレクトリ: Excel ファイルを保存する場所を決定します。整理するために、マシン上にフォルダーを作成します。
前提条件が整ったので、コーディング部分に進みましょう。
## パッケージのインポート
まず最初に、必要なパッケージをインポートする必要があります。これにより、コードで使用するライブラリを知らせることができます。手順は次のとおりです。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
このシンプルなコード行は、Aspose.Cells が提供する強力な機能すべてにアクセスするための入り口です。必ず C# ファイルの先頭に配置してください。 
プロセスを管理しやすいステップに分解してみましょう。コードの各部分を一緒に見ていきましょう。
## ステップ1: 出力ディレクトリを設定する
他の作業を行う前に、出力ディレクトリを設定する必要があります。これは Excel ファイルが保存される場所です。その方法は次のとおりです。
```csharp
//出力ディレクトリ
string outputDir = "Your Document Directory";
```
交換する`"Your Document Directory"`ファイルを実際に保存するパスを入力します。たとえば、デスクトップの「ExcelFiles」というフォルダに保存する場合は、次のように記述します。
```csharp
string outputDir = @"C:\Users\YourUsername\Desktop\ExcelFiles\";
```
## ステップ2: ワークブックを作成する
出力ディレクトリを設定したら、新しいワークブックを作成します。ワークブックは基本的に、複数のワークシートを含むことができる Excel ファイルです。作成方法は次のとおりです。
```csharp
//ワークブックを作成します。
Workbook wb = new Workbook();
```
このコード行は、`Workbook`クラス。これは、データを入力する準備が整った新しい空の Excel ファイルを開くものと考えることができます。
## ステップ3: コンプライアンス設定を指定する
次に、ワークブックを Strict Open XML スプレッドシート形式で保存するように指定する必要があります。これは、他の Excel プログラムとの互換性を確保するための重要なステップです。手順は次のとおりです。
```csharp
//指定 - 厳密な Open XML スプレッドシート - 形式。
wb.Settings.Compliance = OoxmlCompliance.Iso29500_2008_Strict;
```
コンプライアンスを`OoxmlCompliance.Iso29500_2008_Strict`では、Aspose.Cells に対して、ワークブックが Open XML 標準に厳密に準拠するように指示することになります。
## ステップ4: ワークシートにデータを追加する
次は楽しい部分です。ワークシートにデータを追加しましょう。ファイルが Strict Open XML 形式であることを示すメッセージをセル B4 に書き込みます。手順は次のとおりです。
```csharp
//最初のワークシートのセル B4 にメッセージを追加します。
Cell b4 = wb.Worksheets[0].Cells["B4"];
b4.PutValue("This Excel file has Strict Open XML Spreadsheet format.");
```
この手順では、最初のワークシート (ワークシートはゼロ インデックスです) にアクセスし、セル B4 にメッセージを挿入します。Excel ファイルに付箋を貼るようなものです。
## ステップ5: ワークブックを保存する
もうすぐ終わりです! 最後のステップは、先ほど指定した出力ディレクトリにワークブックを保存することです。これを行うためのコードは次のとおりです。
```csharp
//出力Excelファイルに保存します。
wb.Save(outputDir + "outputSaveWorkbookToStrictOpenXMLSpreadsheetFormat.xlsx", SaveFormat.Xlsx);
```
このコード行はワークブックを`.xlsx`指定されたディレクトリにファイルを作成します。ファイル名は自由に付けることができますが、`.xlsx`拡大。
## ステップ6: 成功を確認する
最後に、すべてが正常に実行されたことを知らせる小さな確認メッセージを追加しましょう。
```csharp
Console.WriteLine("SaveWorkbookToStrictOpenXMLSpreadsheetFormat executed successfully.");
```
これは、コードが問題なく実行されたことを確認する簡単な方法です。プログラムを実行すると、コンソールにこのメッセージが表示されれば、実行は完了です。
## 結論
これで完了です。Aspose.Cells for .NET を使用して、Strict Open XML スプレッドシート形式でブックを保存する方法を学習しました。これは、キッチンで新しいレシピをマスターするようなものです。これで、業界標準と互換性があり準拠した美しい Excel ファイルを作成するためのツールと知識が手に入りました。
ビジネス用のデータを管理する場合でも、学校のレポートを作成する場合でも、このスキルは役立ちます。さあ、Aspose.Cells のさまざまな機能を試して、何が作成できるか見てみましょう。
## よくある質問
### Strict Open XML スプレッドシート形式とは何ですか?
Strict Open XML スプレッドシート形式は、Open XML 標準に厳密に準拠しており、さまざまなアプリケーション間での互換性が保証されます。
### Aspose.Cells を無料で使用できますか?
はい！Aspose.Cellsの無料試用版で機能を試すことができます。ダウンロードしてください[ここ](https://releases.aspose.com/).
### Aspose.Cells の詳細情報はどこで入手できますか?
詳細なガイドとAPIリファレンスについてはドキュメントをご覧ください。[ここ](https://reference.aspose.com/cells/net/).
### Aspose.Cells のサポートを受けるにはどうすればよいですか?
ご質問やサポートが必要な場合は、サポートフォーラムをご覧ください。[ここ](https://forum.aspose.com/c/cells/9).
### ワークブックを異なる形式で保存できますか?
もちろんです! Aspose.Cells を使用すると、ニーズに応じて、PDF、CSV などのさまざまな形式でワークブックを保存できます。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
