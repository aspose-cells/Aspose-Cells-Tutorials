---
title: .NET でプログラム的に Excel ファイルのドキュメント バージョンを指定する
linktitle: .NET でプログラム的に Excel ファイルのドキュメント バージョンを指定する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して、Excel ファイル内のバージョン、作成者、タイトルなどのドキュメント プロパティをプログラムで指定する方法を、ステップ バイ ステップの手順で学習します。
weight: 12
url: /ja/net/saving-and-exporting-excel-files-with-options/specifying-document-version-of-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET でプログラム的に Excel ファイルのドキュメント バージョンを指定する

## 導入
Aspose.Cells for .NET は、開発者が Excel ファイルをプログラムで簡単に操作できるようにする強力なライブラリです。Excel ファイルを最初から作成する場合でも、既存のファイルを変更する場合でも、Aspose.Cells は目的を達成するための包括的な API を提供します。そのような機能の 1 つは、バージョン、作成者、タイトルなどのドキュメント プロパティを指定することです。このチュートリアルでは、Aspose.Cells for .NET を使用して Excel ファイルのドキュメント バージョンをプログラムで指定する方法について説明します。
## 前提条件
詳細に入る前に、このチュートリアルを実行するために必要なものがすべて揃っていることを確認しましょう。
1. Aspose.Cells for .NET: 最新バージョンをダウンロードできます[ここ](https://releases.aspose.com/cells/net/)ライセンスをまだ購入していない場合は、[一時ライセンス](https://purchase.aspose.com/temporary-license/)機能を探索します。
2. .NET 開発環境: Visual Studio または任意の .NET 互換 IDE を使用できます。
3. C# の基礎知識: C# プログラミングを理解しておくと、理解しやすくなります。
## パッケージのインポート
コーディングを開始する前に、Aspose.Cells ライブラリから必要な名前空間をインポートする必要があります。これにより、Excel ファイルの操作に必要なクラスとメソッドにアクセスできるようになります。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
これら 2 つの名前空間は、ワークブックとその組み込みドキュメント プロパティを操作するために不可欠です。
ここで、バージョン、タイトル、作成者など、Excel ファイルでドキュメントのプロパティを指定するプロセスを詳しく説明します。
## ステップ 1: ワークブック オブジェクトを初期化する
最初のステップは、`Workbook`オブジェクト。このオブジェクトは、作業する Excel ファイル全体を表します。
```csharp
Workbook wb = new Workbook();
```
の`Workbook`クラスは Excel ファイルの表現を提供します。これをインスタンス化することで、操作可能な空の Excel ブックが作成されます。
## ステップ2: 組み込みドキュメントプロパティにアクセスする
Aspose.Cellsには、タイトル、作成者、ドキュメントバージョンなどのフィールドを含む組み込みのドキュメントプロパティが用意されています。これらのプロパティには、`BuiltInDocumentProperties`コレクション。
```csharp
Aspose.Cells.Properties.BuiltInDocumentPropertyCollection bdpc = wb.BuiltInDocumentProperties;
```
の`BuiltInDocumentPropertyCollection`クラスは、タイトル、作成者、およびドキュメントに通常関連付けられるその他のメタデータなど、組み込みのドキュメント プロパティのコレクションへのアクセスを提供します。
## ステップ3: Excelドキュメントのタイトルを設定する
次に、Excel ドキュメントのタイトルを設定します。このメタデータは、後でファイルを識別および管理するのに役立ちます。
```csharp
bdpc.Title = "Aspose File Format APIs";
```
タイトルの設定は、ドキュメントの整理に重要です。このメタデータはファイルのプロパティで確認でき、外部システムでドキュメントをより効果的にカタログ化または識別するために使用できます。
## ステップ4: 著者を指定する
ドキュメントの作成者を指定して、ファイルを作成または変更したユーザーを反映することもできます。
```csharp
bdpc.Author = "Aspose APIs Developers";
```
このステップは、ドキュメントの作成者を特定し、ドキュメント管理やコラボレーションのシナリオに追加のメタデータを提供するのに役立ちます。
## ステップ5: ドキュメントのバージョンを指定する
このチュートリアルで取り上げる最も重要なプロパティの 1 つは、ドキュメントのバージョンです。この手順では、ドキュメントのバージョンを指定できます。これは、バージョン管理が必要な環境で作業する場合に役立ちます。
```csharp
bdpc.DocumentVersion = "Aspose.Cells Version - 18.3";
```
ドキュメント バージョンを設定すると、ファイルの作成に使用されたドキュメントまたはライブラリのバージョンが明確になります。これは、ファイルのリビジョンや異なるライブラリ バージョンとの互換性を追跡する必要がある環境では特に重要です。
## ステップ6: Excelファイルを保存する
最後に、設定したすべてのプロパティを含むExcelファイルを保存します。Aspose.Cellsでは、さまざまな形式でファイルを保存できますが、この例では、`.xlsx`形式。
```csharp
wb.Save("outputSpecifyDocumentVersionOfExcelFile.xlsx", SaveFormat.Xlsx);
```
の`Save`メソッドは、ファイルを指定したディレクトリに保存するために使用されます。ここでは、Excelファイルとして保存しています。`.xlsx`フォーマット。必要に応じて、Aspose.Cellsは次のようなフォーマットもサポートします。`.xls`, `.csv`、 そして`.pdf`プロジェクトのニーズに応じて柔軟に対応します。
## 結論
このチュートリアルでは、Aspose.Cells for .NET を使用して、Excel ファイルでドキュメント プロパティ、特にドキュメント バージョンを指定する方法について説明しました。Aspose.Cells は、Excel ファイルをプログラムで操作できる非常に柔軟で強力なツールであり、スプレッドシートを扱う .NET 開発者にとって非常に役立ちます。
## よくある質問
### Aspose.Cells を使用して他の組み込みプロパティを変更できますか?  
はい、件名、キーワード、コメントなど、その他の組み込みプロパティを変更できます。
### Aspose.Cells ではどのようなファイル形式がサポートされていますか?  
 Aspose.Cellsは、以下のさまざまな形式をサポートしています。`.xls`, `.xlsx`, `.csv`, `.pdf`、などなど。
### Aspose.Cells for .NET を使用するにはライセンスが必要ですか?  
 Aspose.Cellsを探索するには、[無料トライアル](https://releases.aspose.com/)または申請する[一時ライセンス](https://purchase.aspose.com/temporary-license/)拡張テスト用。
### Aspose.Cells を Web アプリケーションで使用できますか?  
はい、Aspose.Cells はデスクトップ アプリケーションと Web アプリケーションの両方で使用できます。汎用性が高く、.NET Web フレームワークとうまく統合されます。
### Aspose.Cells のサポートはどこで受けられますか?  
コミュニティやサポートにアクセスするには、[Aspose.Cells サポート フォーラム](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
