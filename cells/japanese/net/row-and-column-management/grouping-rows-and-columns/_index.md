---
title: Aspose.Cells を使用して Excel の行と列をグループ化する
linktitle: Aspose.Cells を使用して Excel の行と列をグループ化する
second_title: Aspose.Cells .NET Excel 処理 API
description: このステップバイステップ ガイドでは、Aspose.Cells for .NET を使用して Excel の行と列をグループ化する方法を学習します。
weight: 12
url: /ja/net/row-and-column-management/grouping-rows-and-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells を使用して Excel の行と列をグループ化する

## 導入
大きな Excel シートで作業している場合、すべてを整理してユーザーフレンドリーに保つことがいかに重要であるかはご存じでしょう。行と列をグループ化するとセクションを作成しやすくなり、データのナビゲーションがはるかにスムーズになります。Aspose.Cells for .NET を使用すると、Excel の行と列をプログラムで簡単にグループ化できるため、ファイルのレイアウトを完全に制御できます。
このチュートリアルでは、Aspose.Cells for .NET を使用して Excel シートの行と列を設定、グループ化、非表示にするために必要なすべての手順を説明します。最後には、Excel 自体を開かなくても、プロのように Excel ファイルを操作できるようになります。準備はできましたか?
## 前提条件
コードに進む前に、すべてがセットアップされ準備ができていることを確認しましょう。
1.  Aspose.Cells for .NET ライブラリ: Excel ファイルを操作するにはこのライブラリが必要です。ダウンロードできます。[ここ](https://releases.aspose.com/cells/net/).
2. Visual Studio: このチュートリアルでは、コード例として Visual Studio を使用します。
3. 基本的な C# の知識: C# と .NET の知識があると役立ちます。
4. Aspose ライセンス: 評価の制限を回避するには、有料ライセンスまたは一時ライセンスが必要です。一時ライセンスを取得する[ここ](https://purchase.aspose.com/temporary-license/).
## パッケージのインポート
開始するには、必要な Aspose.Cells 名前空間と、ファイル処理に不可欠な .NET ライブラリをインポートします。 
```csharp
using System.IO;
using Aspose.Cells;
```
コードの各部分を分解して、理解しやすくしてみましょう。
## ステップ1: データディレクトリを設定する
まず最初に、作業する Excel ファイルへのパスを定義する必要があります。これは通常ローカル パスですが、ネットワーク上のパスの場合もあります。
```csharp
//ドキュメント ディレクトリへのパス。
string dataDir = "Your Document Directory";
```
ここで、`"Your Document Directory"` Excel ファイルへの実際のパスを入力します。この設定により、コードが作業に必要なファイルを見つけやすくなります。
## ステップ2: Excelファイルにアクセスするためのファイルストリームを作成する
Aspose.Cells では、ファイル ストリームを介してファイルを開く必要があります。このストリームは、処理のためにファイルのコンテンツを読み取って読み込みます。
```csharp
//開くExcelファイルを含むファイルストリームを作成する
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
上記のコードは`book1.xls`指定したディレクトリから。ファイルが存在しない場合は、必ず作成するか、ファイル名を変更してください。
## ステップ 3: Aspose.Cells を使用してワークブックを読み込む
次に、Aspose.Cells を使用してワークブックを初期化します。この手順により、Excel ファイルにアクセスして簡単に操作できるようになります。
```csharp
//ファイルストリームを介してExcelファイルを開く
Workbook workbook = new Workbook(fstream);
```
この行の後に、`workbook`オブジェクトには、Excel ファイルのすべてのデータと構造が含まれます。スプレッドシート全体がメモリに読み込まれるようなものと考えてください。
## ステップ4: 変更したいワークシートにアクセスする
Aspose.Cells は、ワークブック内の各ワークシートを個別のオブジェクトとして保存します。ここでは、最初のワークシートを選択しています。
```csharp
// Excelファイルの最初のワークシートにアクセスする
Worksheet worksheet = workbook.Worksheets[0];
```
特定のワークシートが必要な場合は、この行を変更して、名前またはインデックスでアクセスできます。
## ステップ5: ワークシートの行をグループ化する
次は楽しい部分、つまり行のグループ化です。最初の 6 行をグループ化して非表示にしましょう。
```csharp
//最初の6行（0から5）をグループ化し、trueを渡して非表示にする
worksheet.Cells.GroupRows(0, 5, true);
```
各パラメータの機能は次のとおりです。
- 0、5: グループ化する行の開始インデックスと終了インデックス。Excel では、行のインデックスは 0 から始まります。
- true: これを true に設定すると、グループ化された行が非表示になります。
実行すると、0 から 5 までの行がグループ化され、表示されなくなります。
## ステップ6: ワークシートの列をグループ化する
行と同様に、列をグループ化して、よりすっきりと整理されたレイアウトを作成できます。最初の 3 つの列をグループ化する方法は次のとおりです。
```csharp
//最初の3列（0から2）をグループ化し、trueを渡して非表示にする
worksheet.Cells.GroupColumns(0, 2, true);
```
この関数のパラメータは次のとおりです。
- 0、2: グループ化する列の範囲。インデックスは 0 から始まります。
- true: このパラメータはグループ化された列を非表示にします。
選択した列 (0 ～ 2) が Excel ファイル内でグループ化され、非表示になります。
## ステップ7: 変更したExcelファイルを保存する
変更を加えたら、元のファイルが上書きされないように、新しい名前でファイルを保存しましょう。
```csharp
//変更したExcelファイルを保存する
workbook.Save(dataDir + "output.xls");
```
これで、グループ化された行と列が`output.xls`必要に応じてファイル名を調整できます。
## ステップ 8: ファイル ストリームを閉じてリソースを解放する
最後に、ファイル ストリームを閉じてリソースを解放します。これを行わないと、ファイルに再度アクセスしたり変更したりする必要がある場合に問題が発生する可能性があります。
```csharp
//ファイルストリームを閉じてすべてのリソースを解放する
fstream.Close();
```
これで完了です。Aspose.Cells for .NET を使用して、Excel ファイル内の行と列をグループ化できました。
## 結論
Aspose.Cells for .NET を使用して Excel の行と列をグループ化することは、スプレッドシートをより使いやすく整理できる簡単なプロセスです。わずか数行のコードで、Excel で手動で行う場合はより多くの手順が必要となる強力な機能を習得できます。さらに、このプロセスを多数のファイルで自動化できるため、時間を節約し、エラーを減らすことができます。このガイドでは、Excel ファイルをプログラムで制御するために必要なすべての手順を示しました。
## よくある質問
### 行と列を非表示にせずにグループ化できますか?  
はい！パスするだけです`false`3番目のパラメータとして`GroupRows`または`GroupColumns`方法。
### 行または列のグループを解除したい場合はどうすればよいでしょうか?  
使用`worksheet.Cells.UngroupRows(startRow, endRow)`または`worksheet.Cells.UngroupColumns(startColumn, endColumn)`グループを解除します。
### 同じワークシート内で複数の範囲をグループ化できますか?  
もちろんです。`GroupRows`または`GroupColumns`グループ化する各範囲に対してメソッドを実行します。
### Aspose.Cells for .NET を使用するにはライセンスが必要ですか?  
はい、試用版は利用可能ですが、全機能を使用するにはライセンスが必要です。一時ライセンスを取得できます。[ここ](https://purchase.aspose.com/temporary-license/).
### 条件付きロジックを使用して行と列をグループ化できますか?  
はい。各行または列のデータに応じて、グループ化の前にコードにロジックを組み込むことで、条件付きグループ化を作成できます。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
