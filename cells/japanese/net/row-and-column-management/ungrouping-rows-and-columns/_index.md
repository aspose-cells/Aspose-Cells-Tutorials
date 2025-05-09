---
"description": "この包括的なガイドでは、Aspose.Cells for .NET を使用して Excel の行と列のグループ化を解除する方法を学習します。Excel のデータ操作を簡素化します。"
"linktitle": "Aspose.Cells を使用して Excel の行と列をグループ解除する"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": "Aspose.Cells を使用して Excel の行と列をグループ解除する"
"url": "/ja/net/row-and-column-management/ungrouping-rows-and-columns/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells を使用して Excel の行と列をグループ解除する

## 導入
Excelファイルを扱う際に、行や列のグループ化を解除しなければならない場面に遭遇することがあるかもしれません。スプレッドシートを整理したり、見栄えを良くするためにデータの書式を変更したりする場合でも、Aspose.Cells for .NETは、そのプロセスを簡素化する優れたツールです。このチュートリアルでは、Aspose.Cellsを使ってExcelの行と列のグループ化を解除する手順を解説します。このチュートリアルを最後まで読めば、Excelファイルをプログラムで操作する方法をしっかりと理解できるでしょう。
## 前提条件
コードに取り組む前に、すべての準備が整っていることを確認しましょう。必要なものは次のとおりです。
1. Visual Studio: お使いのマシンにVisual Studioがインストールされている必要があります。まだインストールされていない場合は、こちらからダウンロードできます。 [Visual Studioのサイト](https://visualstudio。microsoft.com/).
2. Aspose.Cells for .NET: Aspose.Cellsライブラリをダウンロードする必要があります。 [Aspose リリースページ](https://releases.aspose.com/cells/net/)必要なライセンスを持っていることを確認してください。ライセンスは購入または代理店を通じて取得できます。 [一時ライセンス](https://purchase。aspose.com/temporary-license/).
3. C# の基本知識: C# プログラミングの基礎を理解しておくと、より簡単に理解できるようになります。
すべての準備が整ったら、楽しい部分であるコードに取り掛かります。
## パッケージのインポート
まず、C#プロジェクトに必要なパッケージをインポートする必要があります。手順は以下のとおりです。
1. Visual Studio でプロジェクトを開きます。
2. Aspose.Cellsライブラリへの参照を追加します。プロジェクト内の「参照」を右クリックし、「参照の追加」を選択することで追加できます。Aspose.Cells DLLを保存した場所を参照します。
3. C# ファイルの先頭に、次の using ディレクティブを追加します。
```csharp
using System.IO;
using Aspose.Cells;
```
すべての設定が完了したら、Excel シート内の行と列のグループを解除する手順を見ていきましょう。 
## ステップ1: ドキュメントディレクトリを定義する
まず、Excelファイルが保存されているディレクトリを指定する必要があります。設定方法は以下のとおりです。
```csharp
// ドキュメント ディレクトリへのパス。
string dataDir = "Your Document Directory";
```
交換する `"Your Document Directory"` Excel ファイルが保存されているコンピューター上の実際のパスを入力します。 
## ステップ2: ファイルストリームを作成する
次に、Excelファイルを開くためのファイルストリームを作成する必要があります。手順は以下のとおりです。
```csharp
// 開くExcelファイルを含むファイルストリームを作成する
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
ここでは、 `book1.xls`指定したディレクトリにこのファイルが存在することを確認してください。存在しない場合、ファイルが見つからないというエラーが発生します。
## ステップ3: ワークブックオブジェクトのインスタンス化
それでは、ExcelファイルをWorkbookオブジェクトに読み込みましょう。これにより、プログラムからワークブックを操作できるようになります。
```csharp
// Workbookオブジェクトのインスタンス化
// ファイルストリームを介してExcelファイルを開く
Workbook workbook = new Workbook(fstream);
```
このコード行により、Excel ファイルがメモリに正常に読み込まれ、操作する準備が整いました。
## ステップ4: ワークシートにアクセスする
ワークブックを作成したら、次は行と列のグループ化を解除したいワークシートにアクセスします。手順は以下のとおりです。
```csharp
// Excelファイルの最初のワークシートにアクセスする
Worksheet worksheet = workbook.Worksheets[0];
```
この場合、最初のワークシートにアクセスしています。データが別のシートにある場合は、それに応じてインデックスを変更できます。
## ステップ5: 行のグループ解除
いよいよ面白い部分です！最初の6行（行0から行5まで）のグループを解除しましょう。以下のコードを使ってください。
```csharp
// 最初の6行（0から5）のグループを解除する
worksheet.Cells.UngroupRows(0, 5);
```
このメソッドは、指定された行に適用されたグループ化をすべて解除します。とても簡単です！
## ステップ6: 列のグループを解除する
行と同様に、列もグループ解除できます。最初の3列（列0から列2まで）のグループを解除する方法は次のとおりです。
```csharp
// 最初の3列のグループを解除する（0から2まで）
worksheet.Cells.UngroupColumns(0, 2);
```
## ステップ7: 変更したExcelファイルを保存する
行と列のグループ化を解除したら、次のステップは変更内容をExcelファイルに保存することです。これを行うには、 `Save` 方法：
```csharp
// 変更したExcelファイルを保存する
workbook.Save(dataDir + "output.xls");
```
この例では、変更したファイルを次のように保存します。 `output.xls`ファイル名は好きな名前に変更できます。
## ステップ8: ファイルストリームを閉じる
最後に、リソースを解放するには、ファイル ストリームを閉じる必要があります。
```csharp
// ファイルストリームを閉じてすべてのリソースを解放する
fstream.Close();
```
これは、アプリケーションがファイル ハンドルを必要以上に長く保持しないようにするための良い方法です。
## 結論
これで完了です！Aspose.Cells for .NET を使って Excel ファイルの行と列のグループ化を解除する方法を習得できました。わずか数行のコードで、Excel ファイルにプログラム的に大きな変更を加えることができます。レポートの自動化や分析用データの準備など、これらのテクニックを習得すれば、作業時間を大幅に節約できます。
## よくある質問
### Aspose.Cells とは何ですか?
Aspose.Cells は、.NET アプリケーションで Excel ファイルを操作するための強力なライブラリであり、スプレッドシートの操作、変換、作成を簡単に行うことができます。
### 他のライブラリを使用して Excel の行と列のグループを解除できますか?
はい、.NET で Excel を操作するための他のライブラリもありますが、Aspose.Cells は豊富な機能と使いやすさを提供します。
### 保存後に変更を元に戻す方法はありますか?
Excel ファイルを保存すると、元のファイルのバックアップがない限り、以前の状態を復元することはできません。
### Aspose.Cells のサポートを受けるにはどうすればよいですか?
サポートについては、 [Aspose サポートフォーラム](https://forum.aspose.com/c/cells/9)、質問をしたり解決策を見つけたりすることができます。
### ライセンスなしで Aspose.Cells を使用できますか?
はい、Aspose.Cellsは一定の制限付きで無料でご利用いただけます。 [一時ライセンス](https://purchase.aspose.com/temporary-license/) 完全な機能を実現します。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}