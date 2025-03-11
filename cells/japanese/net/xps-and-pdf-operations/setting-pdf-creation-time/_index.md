---
title: .NET で PDF 作成時間を設定する
linktitle: .NET で PDF 作成時間を設定する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells を使用して .NET で PDF 作成時間を設定する方法を学びます。Excel から PDF へのシームレスな変換については、ステップバイステップ ガイドに従ってください。
weight: 11
url: /ja/net/xps-and-pdf-operations/setting-pdf-creation-time/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET で PDF 作成時間を設定する

## 導入
今日のデジタル時代では、ドキュメントをさまざまな形式に変換する機能は、多くのアプリケーションにとって不可欠です。よくあるニーズの 1 つは、Excel スプレッドシートを PDF ファイルに変換することです。これにより、書式設定が保持されるだけでなく、共有や印刷がはるかに簡単になります。.NET で作業する開発者にとって、Aspose.Cells は、このプロセスを簡素化する優れたライブラリです。このチュートリアルでは、Aspose.Cells for .NET を使用して Excel ファイルを PDF に変換するときに PDF 作成時間を設定する方法について詳しく説明します。
## 前提条件
コードの細部に入る前に、始めるのに必要なものがすべて揃っていることを確認しましょう。
### 必要なもの
1. Visual Studio: マシンに Visual Studio がインストールされていることを確認してください。これが開発環境になります。
2. Aspose.Cells for .NET: Aspose.Cellsライブラリを以下からダウンロードしてください。[Webサイト](https://releases.aspose.com/cells/net/)無料トライアルで機能を試すこともできます。
3. C# の基礎知識: C# プログラミングに精通していると、コード スニペットをよりよく理解できるようになります。
4.  Excelファイル: 変換するExcelファイルを用意します。この例では、`Book1.xlsx`.
前提条件が整ったので、楽しい部分、つまり必要なパッケージをインポートしてコードを記述する作業に取り掛かりましょう。
## パッケージのインポート
まず、C# ファイルに必要な名前空間をインポートする必要があります。これは、Aspose.Cells ライブラリによって提供されるクラスとメソッドにアクセスできるようにするため、非常に重要です。
### C#プロジェクトを開く
Visual Studio を開き、PDF 変換機能を実装する新しいプロジェクトを作成するか、既存のプロジェクトを開きます。
### Aspose.Cells 参照を追加する
ソリューション エクスプローラーでプロジェクトを右クリックし、「NuGet パッケージの管理」を選択して「Aspose.Cells」を検索し、Aspose.Cells ライブラリをプロジェクトに追加できます。パッケージをインストールします。
### 名前空間のインポート
C# ファイルの先頭に、次の名前空間を含めます。
```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Charts;
```
これらの名前空間により、Workbook クラスやその他の重要な機能にアクセスできるようになります。

パッケージをインポートしたので、作成時間を設定しながら Excel ファイルを PDF に変換するプロセスを詳しく見ていきましょう。
## ステップ1: ドキュメントディレクトリを定義する
まず、ドキュメントが保存されているディレクトリを指定する必要があります。これは、Excel ファイルが保存され、出力 PDF が保存される場所です。
```csharp
string dataDir = "Your Document Directory"; //ドキュメントディレクトリを指定する
```
交換する`"Your Document Directory"`実際の経路で`Book1.xlsx`ファイルが配置されている場所。このパスは、アプリケーションが処理するファイルを見つけるのに役立ちます。
## ステップ2: Excelファイルを読み込む
次に、Excelファイルを`Workbook`オブジェクト。Aspose.Cells は、Excel ファイルを簡単に操作できるため、この点で優れています。
```csharp
string inputPath = dataDir + "Book1.xlsx"; // Excelファイルへのパス
Workbook workbook = new Workbook(inputPath); // Excelファイルを読み込む
```
の`Workbook`クラスは、Excel ファイルの読み込みと操作に使用されます。入力パスを渡すことで、どのファイルで作業するかをアプリケーションに指示します。
## ステップ3: PdfSaveOptionsを作成する
さて、インスタンスを作成しましょう`PdfSaveOptions`このクラスを使用すると、作成時間など、ワークブックを PDF として保存するためのさまざまなオプションを指定できます。
```csharp
PdfSaveOptions options = new PdfSaveOptions(); // PdfSaveOptionsインスタンスを作成する
options.CreatedTime = DateTime.Now; //作成時間を現在に設定する
```
設定により`options.CreatedTime`に`DateTime.Now`こうすることで、PDF が作成された現在の日時を反映するようになります。
## ステップ4: ワークブックをPDFとして保存する
最後に、定義したオプションを使用して、ワークブックを PDF ファイルとして保存します。
```csharp
workbook.Save(dataDir + "output.pdf", options); //PDFとして保存
```
このコード行はワークブックを取得し、指定された場所にPDF形式で保存します。`options`パラメータが渡され、PDF メタデータに作成時間が含まれます。

## 結論
これで完了です。Aspose.Cells for .NET を使用して、Excel ファイルを PDF に変換し、作成タイムスタンプも取得できました。この機能は、ドキュメントのバージョンを追跡する必要がある場合や、ドキュメントの作成日時に関する情報を受信者に提供する必要がある場合に非常に便利です。
 Aspose.Cellsのさらなる機能について知りたい場合は、ぜひご覧ください。[ドキュメント](https://reference.aspose.com/cells/net/).
## よくある質問
### Aspose.Cells とは何ですか?
Aspose.Cells は、開発者が Excel ファイルを作成、操作、変換できるようにする強力な .NET ライブラリです。
### Aspose.Cells を無料で使用できますか?
はい、無料トライアルから始めることができます。[Aspose ウェブサイト](https://releases.aspose.com/).
### その他の PDF プロパティを設定するにはどうすればよいですか?
さまざまなPDFプロパティを設定するには、`PdfSaveOptions`ページ サイズ、圧縮などのクラス。
### 複数の Excel ファイルを一度に変換することは可能ですか?
はい、ファイルのリストをループして、各ファイルに同じ変換プロセスを適用できます。
### Aspose.Cells のサポートはどこで受けられますか?
 Asposeコミュニティからサポートを受けることができます。[サポートフォーラム](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
