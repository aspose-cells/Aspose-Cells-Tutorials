---
title: Aspose.Cells を使用してワークブック内のデータをコピーする
linktitle: Aspose.Cells を使用してワークブック内のデータをコピーする
second_title: Aspose.Cells .NET Excel 処理 API
description: ステップバイステップのガイド、コード サンプル、役立つヒントを使用して、Aspose.Cells for .NET を使用して Excel ブック内でデータを効率的にコピーする方法を学習します。
weight: 12
url: /ja/net/worksheet-value-operations/copy-data-within-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells を使用してワークブック内のデータをコピーする

## 導入
Excel ブック内のデータ管理は、多くのアプリケーションの中核部分です。重要なデータが入ったテンプレートまたはシートがあり、それを同じブック内で複製して後で使用したいとします。ここで Aspose.Cells for .NET が活躍します。このガイドでは、Aspose.Cells を使用して同じブック内でデータをコピーする手順を、わかりやすくわかりやすいステップバイステップのチュートリアルで説明します。
## 前提条件
コーディングを始める前に、このタスクを完了するために必要なものがすべて揃っていることを確認しましょう。
1.  Aspose.Cells for .NETライブラリ – 最新バージョンをダウンロードするには、[Aspose.Cells for .NET のダウンロード ページ](https://releases.aspose.com/cells/net/).
2. 開発環境 - Visual Studio などの .NET 互換 IDE が必要です。
3. ライセンス – Aspose.Cellsの無料トライアルまたは購入したライセンスを使用します。一時ライセンスを取得できます。[ここ](https://purchase.aspose.com/temporary-license/)または購入オプションを調べる[ここ](https://purchase.aspose.com/buy).
## パッケージのインポート
コードでは、クラスとメソッドを利用するために Aspose.Cells をインポートする必要があります。
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
コードを見てみましょう。Aspose.Cells for .NET を使用してワークブック内でデータをコピーするタスクを、わかりやすい手順に分解します。
## ステップ1: ディレクトリパスを設定する
ワークブックの処理を開始する前に、ファイルの場所と出力を保存する場所を定義しましょう。ディレクトリ パスを設定すると、整理された状態が保たれます。
```csharp
//ドキュメントのディレクトリ パスを設定します。
string dataDir = "Your Document Directory";
string inputPath = dataDir + "book1.xls";
```
ここで、`"Your Document Directory"`ワークブックが保存されている実際のパスに置き換えます。このパス変数を使用すると、入力ファイルと出力ファイルを簡単に参照できます。
## ステップ2: 既存のExcelファイルを開く
Excel ファイルを操作するには、そのファイルを Aspose.Cells のワークブック オブジェクトに読み込む必要があります。この手順では、データのコピー元のファイルを開きます。
```csharp
//既存の Excel ファイルを開きます。
Workbook wb = new Workbook(inputPath);
```
これにより、私たちの`Workbook`物体`wb`コンテンツと対話する準備ができました`book1.xls`.
## ステップ3: ワークシートコレクションにアクセスする
ワークブックが開いたので、ワークシートのコレクションにアクセスします。`WorksheetCollection`クラスは、ワークブック内の複数のシートを操作するのに役立ちます。
```csharp
//ワークブック内のすべてのシートを参照する Worksheets オブジェクトを作成します。
WorksheetCollection sheets = wb.Worksheets;
```
ここ、`sheets`既存のシートのコピーを追加するなど、ワークブック内の各シートを操作できるようになります。
## ステップ4: 新しいシートにデータをコピーする
タスクの主な部分は、1 つのシートの内容を同じワークブック内の新しいシートにコピーすることです。この例では、「Sheet1」から新しいシートにデータをコピーします。
```csharp
// 「Sheet1」からワークブック内の新しいシートにデータをコピーします。
sheets.AddCopy("Sheet1");
```
の`AddCopy`メソッドは、指定されたシートの正確なコピーを作成し、それをワークブックに追加します。ここでは、「Sheet1」を複製しています。コピーするシートの名前は任意に指定できます。
## ステップ5: 新しいシートを含むワークブックを保存する
シートをコピーした後、変更内容を保持するために、ブックを新しい名前で保存するか、新しい場所に保存します。
```csharp
//コピーしたデータを含むワークブックを保存します。
wb.Save(dataDir + "CopyWithinWorkbook_out.xls");
```
この行は変更されたワークブックを次のように保存します。`CopyWithinWorkbook_out.xls`指定されたディレクトリ内。
## 結論
これで完了です。Aspose.Cells for .NET を使用してワークブック内でデータをコピーするのは簡単です。Aspose.Cells を使用すると、Excel ファイルの処理が簡単になり、複雑なデータ管理タスクを簡単に実行できます。テンプレートの使用、バックアップ、または新しいバージョンの作成のためにシートを複製する必要がある場合でも、ここで説明した手順は目的の達成に役立ちます。
もっと詳しく知りたい方は、[Aspose.Cells ドキュメント](https://reference.aspose.com/cells/net/)高度な機能と性能を実現します。
## よくある質問
### 一度に複数のシートをコピーできますか?
Aspose.Cells は、1 回の呼び出しで複数のシートのコピーをサポートしていませんが、複製するシートをループして個別にコピーすることはできます。
### コピーしたシートの名前を変更できますか?
はい、シートをコピーした後、次の方法で名前を変更できます。`sheets[sheets.Count - 1].Name = "NewSheetName";`.
### Aspose.Cells は .NET Core と互換性がありますか?
もちろんです! Aspose.Cells は .NET Framework と .NET Core の両方の環境をサポートしています。
### シートをコピーするときに書式設定をどのように処理すればよいですか?
の`AddCopy`この方法では、すべてのコンテンツと書式が保持されるため、コピーしたシートは元のシートとまったく同じように見えます。
### シートを別のブックにコピーしたい場合はどうすればよいでしょうか?
あなたは`Copy`別のワークブックへの参照を持つメソッド、例えば`sheets.Add().Copy(wb.Worksheets["Sheet1"]);`.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
