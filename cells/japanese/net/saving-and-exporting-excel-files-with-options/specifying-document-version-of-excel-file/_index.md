---
"description": "Aspose.Cells for .NET を使用して、Excel ファイル内のバージョン、作成者、タイトルなどのドキュメント プロパティをプログラムで指定する方法を、ステップ バイ ステップの手順で学習します。"
"linktitle": ".NET でプログラム的に Excel ファイルのドキュメント バージョンを指定する"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": ".NET でプログラム的に Excel ファイルのドキュメント バージョンを指定する"
"url": "/ja/net/saving-and-exporting-excel-files-with-options/specifying-document-version-of-excel-file/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# .NET でプログラム的に Excel ファイルのドキュメント バージョンを指定する

## 導入
Aspose.Cells for .NETは、開発者がExcelファイルをプログラムで簡単に操作できる強力なライブラリです。Excelファイルを新規作成する場合でも、既存のファイルを変更する場合でも、Aspose.Cellsは目的を達成するための包括的なAPIを提供します。その一つとして、バージョン、作成者、タイトルなどのドキュメントプロパティの指定機能があります。このチュートリアルでは、Aspose.Cells for .NETを使用してExcelファイルのドキュメントバージョンをプログラムで指定する方法を説明します。
## 前提条件
詳細に入る前に、このチュートリアルを実行するために必要なものがすべて揃っていることを確認しましょう。
1. Aspose.Cells for .NET: 最新バージョンをダウンロードできます [ここ](https://releases.aspose.com/cells/net/)ライセンスをまだ購入していない場合は、 [一時ライセンス](https://purchase.aspose.com/temporary-license/) 機能を探索します。
2. .NET 開発環境: Visual Studio または任意の .NET 互換 IDE を使用できます。
3. C# の基礎知識: C# プログラミングを理解しておくと、理解しやすくなります。
## パッケージのインポート
コーディングを始める前に、Aspose.Cellsライブラリから必要な名前空間をインポートする必要があります。これにより、Excelファイルの操作に必要なクラスとメソッドにアクセスできるようになります。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
これら 2 つの名前空間は、ワークブックとその組み込みドキュメント プロパティを操作するために不可欠です。
ここで、バージョン、タイトル、作成者など、Excel ファイルでドキュメントのプロパティを指定するプロセスを詳しく説明します。
## ステップ1: ワークブックオブジェクトを初期化する
最初のステップは、 `Workbook` オブジェクト。このオブジェクトは、作業対象となる Excel ファイル全体を表します。
```csharp
Workbook wb = new Workbook();
```
その `Workbook` クラスはExcelファイルの表現を提供します。これをインスタンス化することで、操作可能な空のExcelブックが作成されます。
## ステップ2: 組み込みのドキュメントプロパティにアクセスする
Aspose.Cellsには、タイトル、作成者、ドキュメントバージョンなどのフィールドを含む組み込みのドキュメントプロパティが用意されています。これらのプロパティには、 `BuiltInDocumentProperties` コレクション。
```csharp
Aspose.Cells.Properties.BuiltInDocumentPropertyCollection bdpc = wb.BuiltInDocumentProperties;
```
その `BuiltInDocumentPropertyCollection` クラスは、タイトル、作成者、およびドキュメントに通常関連付けられるその他のメタデータなど、組み込みのドキュメント プロパティのコレクションへのアクセスを提供します。
## ステップ3: Excelドキュメントのタイトルを設定する
次に、Excelドキュメントのタイトルを設定します。このメタデータは、後でファイルを識別および管理するのに役立ちます。
```csharp
bdpc.Title = "Aspose File Format APIs";
```
タイトルの設定はドキュメントの整理に重要です。このメタデータはファイルのプロパティで確認でき、外部システムでドキュメントをより効果的にカタログ化または識別するために使用できます。
## ステップ4: 著者を指定する
ドキュメントの作成者を指定して、ファイルを作成または変更したユーザーを反映することもできます。
```csharp
bdpc.Author = "Aspose APIs Developers";
```
このステップは、ドキュメントの作成者を特定し、ドキュメント管理やコラボレーションのシナリオに追加のメタデータを提供するのに役立ちます。
## ステップ5: ドキュメントのバージョンを指定する
このチュートリアルで扱う最も重要なプロパティの一つは、ドキュメントのバージョンです。このステップでは、ドキュメントのバージョンを指定できます。これは、バージョン管理が必要な環境で作業する場合に役立ちます。
```csharp
bdpc.DocumentVersion = "Aspose.Cells Version - 18.3";
```
ドキュメントのバージョンを設定すると、ファイルの作成に使用されたドキュメントまたはライブラリのバージョンが明確になります。これは、ファイルのリビジョンや異なるライブラリバージョンとの互換性を追跡する必要がある環境では特に重要です。
## ステップ6: Excelファイルを保存する
最後に、設定したすべてのプロパティを含むExcelファイルを保存します。Aspose.Cellsでは様々な形式でファイルを保存できますが、この例では `.xlsx` 形式。
```csharp
wb.Save("outputSpecifyDocumentVersionOfExcelFile.xlsx", SaveFormat.Xlsx);
```
その `Save` メソッドは、ファイルを指定したディレクトリに保存するために使用されます。ここでは、Excelファイルとして保存しています。 `.xlsx` 形式。必要に応じて、Aspose.Cellsは次のような形式もサポートします。 `.xls`、 `.csv`、 そして `.pdf`プロジェクトのニーズに応じて柔軟に対応します。
## 結論
このチュートリアルでは、Aspose.Cells for .NET を使用して、Excel ファイルのドキュメントプロパティ、特にドキュメントバージョンを指定する方法を説明しました。Aspose.Cells は、Excel ファイルをプログラムで操作できる非常に柔軟で強力なツールであり、スプレッドシートを扱うすべての .NET 開発者にとって非常に役立ちます。
## よくある質問
### Aspose.Cells を使用して他の組み込みプロパティを変更できますか?  
はい、件名、キーワード、コメントなど、その他の組み込みプロパティを変更できます。
### Aspose.Cells でサポートされているファイル形式は何ですか?  
Aspose.Cellsは、次のようなさまざまな形式をサポートしています。 `.xls`、 `.xlsx`、 `.csv`、 `.pdf`、などなど。
### Aspose.Cells for .NET を使用するにはライセンスが必要ですか?  
Aspose.Cellsを詳しく知るには [無料トライアル](https://releases.aspose.com/) または申請する [一時ライセンス](https://purchase.aspose.com/temporary-license/) 拡張テスト用。
### Aspose.Cells を Web アプリケーションで使用できますか?  
はい、Aspose.CellsはデスクトップアプリケーションとWebアプリケーションの両方で使用できます。非常に汎用性が高く、.NET Webフレームワークとの統合性も優れています。
### Aspose.Cells のサポートはどこで受けられますか?  
コミュニティとサポートにアクセスするには、 [Aspose.Cells サポートフォーラム](https://forum。aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}