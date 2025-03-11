---
title: .NET でプログラム的にピボット テーブルのソース データを変更する
linktitle: .NET でプログラム的にピボット テーブルのソース データを変更する
second_title: Aspose.Cells .NET Excel 処理 API
description: 包括的なステップバイステップのチュートリアルで、Aspose.Cells for .NET を使用してピボット テーブルのソース データをプログラムで変更する方法を学習します。
weight: 10
url: /ja/net/creating-and-configuring-pivot-tables/changing-source-data/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET でプログラム的にピボット テーブルのソース データを変更する

## 導入
データ分析の世界では、Microsoft Excel ほど優れたツールはほとんどありません。毎日、数え切れないほど多くのユーザーがデータの管理と分析に Excel を利用しています。しかし、その裏では、クリックしてドラッグするだけよりもずっと複雑です。Excel ファイルをプログラムで操作したい、具体的にはピボット テーブルのソース データを変更したいと思ったことがあるなら、このガイドはまさにうってつけです。このガイドでは、Aspose.Cells for .NET を使用してこれを実現する方法を説明します。経験豊富な開発者でも、プログラミングの世界に足を踏み入れたばかりの人でも、このチュートリアルにはわかりやすい貴重な情報が満載されています。
## 前提条件
ピボット テーブルのソース データを変更する作業を始める前に、すべての設定が完了し、準備が整っていることを確認しましょう。
1. Visual Studio: ここでコードを記述するため、Microsoft Visual Studio のコピーがインストールされていることを確認してください。
2. Aspose.Cellsライブラリ: Aspose.Cellsライブラリをダウンロードしてプロジェクトで参照する必要があります。ダウンロードできます。[ここ](https://releases.aspose.com/cells/net/).
3. C# の基礎知識: このチュートリアルは簡略化されていますが、C# を理解しておくとコードをよりよく理解するのに役立ちます。
4. Excel ファイル: 操作可能なピボット テーブルを含むサンプル Excel ファイル (「Book1.xlsx」など) が必要です。
さて、これらの前提条件を確認したら、必要なパッケージをインポートしてコーディングを開始できます。
## パッケージのインポート
まず最初に、必要なパッケージをインポートしましょう。Visual Studio で C# プロジェクトを開き、コード ファイルの先頭に次の using ディレクティブを追加します。
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
これらの名前空間を使用すると、Excel ファイルの操作や Aspose.Cells を使用したコンテンツの操作に必要な重要なクラスにアクセスできるようになります。

それでは、プロセスを管理しやすいステップに分解してみましょう。Excel ファイルを開き、ワークシートを変更し、ピボット テーブルのデータ ソースを変更し、結果を保存する手順を説明します。
## ステップ1: ドキュメントディレクトリを定義する
まず、Excelファイルの保存場所を指定する必要があります。`dataDir` 「Book1.xlsx」を含むフォルダーを指す変数。
```csharp
//ドキュメント ディレクトリへのパス。
string dataDir = "Your Document Directory";
```
この行は、Excel ファイルが保存されるディレクトリを設定し、後でアクセスしやすくなります。
## ステップ2: 入力パスを指定する
次に、入力 Excel ファイルへの完全パスを指定する文字列を作成しましょう。
```csharp
string InputPath = dataDir + "Book1.xlsx";
```
これにより、ファイル アクセスが効率化され、コード全体で同じパスを何度も入力する必要がなくなります。
## ステップ3: ファイルストリームを作成する
さて、Excelファイルを開きます。`FileStream` Excel ファイルの内容を読み取ることができます。
```csharp
//開くExcelファイルを含むファイルストリームを作成する
FileStream fstream = new FileStream(InputPath, FileMode.Open);
```
この行はファイルを読み取りモードで開き、そのデータにアクセスできるようにします。
## ステップ4: ワークブックを読み込む
ファイル ストリームが配置されたら、次の手順ではワークブックを読み込みます。
```csharp
//ファイルストリームを介してExcelファイルを開く
Workbook workbook = new Workbook(fstream);
```
このコマンドはExcelファイルを読み込み、`Workbook`オブジェクト。読み込んだら、必要に応じてファイルを操作できます。
## ステップ5: ワークシートにアクセスする
具体的な内容を見ていきましょう。ワークブックの最初のワークシートにアクセスします。
```csharp
// Excelファイルの最初のワークシートにアクセスする
Worksheet worksheet = workbook.Worksheets[0];
```
これにより、最初のワークシート内のデータに直接アクセスできるようになり、簡単に変更できるようになります。
## ステップ6: 新しいデータを入力する
次に、セルに新しいデータを挿入します。この例では、サンプル データをいくつか追加します。
```csharp
//ワークシートのセルに新しいデータを入力する
worksheet.Cells["A9"].PutValue("Golf");
worksheet.Cells["B9"].PutValue("Qtr4");
worksheet.Cells["C9"].PutValue(7000);
```
ここでは、「Golf」、「Qtr4」という値を入力します。`7000`特定のセルに入力します。これらの値は、必要に応じて変更できます。
## ステップ7: 名前付き範囲を変更する
ここで、ピボット テーブルが参照する名前付き範囲を変更します。これには、範囲の作成または更新が含まれます。
```csharp
//名前付き範囲「DataSource」の変更
Range range = worksheet.Cells.CreateRange(0,0,9,3);
range.Name = "DataSource";
```
新しい範囲を定義することで、ピボット テーブルが更新されたときにこの新しいデータが使用されるようになります。
## ステップ8: 変更したExcelファイルを保存する
すべての変更が完了したら、作業内容を保存することが重要です。変更したワークブックを保存しましょう。
```csharp
//変更したExcelファイルを保存する
workbook.Save(dataDir + "output.xls");
```
このコマンドはワークブックを新しいファイルに保存するため、必要がない限り元のファイルを上書きすることはありません。
## ステップ9: ファイルストリームを閉じる
最後に、使用しているリソースを解放するためにファイル ストリームを閉じることが重要です。
```csharp
//ファイルストリームを閉じてすべてのリソースを解放する
fstream.Close();
```
この手順により、アプリケーションでメモリがリークされず、効率性が維持されます。
## 結論
おめでとうございます! Aspose.Cells を使用して、.NET でプログラム的にピボット テーブルのソース データを変更することができました。この機能により、Excel タスクを自動化し、ワークフローを改善するための多くの可能性が開かれます。財務レポートの更新、売上データの追跡、またはデータセットの操作など、プログラム的に実行できれば、時間を大幅に節約し、エラーのリスクを軽減できます。

## よくある質問
### Aspose.Cells とは何ですか?
Aspose.Cells は、Excel ファイルの操作のための強力な .NET ライブラリであり、ユーザーはプログラムによって Excel ドキュメントを作成、変更、操作できます。
### この方法を使用して、既存のピボット テーブルのソース データを変更できますか?
もちろんです! この方法を使用すると、Excel ブック内の既存のピボット テーブルのデータ ソースを更新できます。
### Aspose.Cells を使用するには Office をインストールする必要がありますか?
いいえ! Aspose.Cells はスタンドアロン ライブラリなので、Excel ファイルを操作するのに Microsoft Office をインストールする必要はありません。
### Aspose.Cells は無料で使用できますか?
Aspose.Cellsは無料試用版を提供していますが、フル機能を使用するにはライセンスを購入する必要があります。詳細については、[ここ](https://purchase.aspose.com/buy).
### より多くの例やサポートはどこで見つかりますか?
その他の例とサポートについては、[Aspose.Cells ドキュメント](https://reference.aspose.com/cells/net/)およびコミュニティフォーラム[ここ](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
