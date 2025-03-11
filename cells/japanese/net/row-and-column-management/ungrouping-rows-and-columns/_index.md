---
title: Aspose.Cells を使用して Excel の行と列をグループ解除する
linktitle: Aspose.Cells を使用して Excel の行と列をグループ解除する
second_title: Aspose.Cells .NET Excel 処理 API
description: この包括的なガイドでは、Aspose.Cells for .NET を使用して Excel の行と列をグループ解除する方法を学習します。Excel データの操作を簡素化します。
weight: 15
url: /ja/net/row-and-column-management/ungrouping-rows-and-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells を使用して Excel の行と列をグループ解除する

## 導入
Excel ファイルを扱う場合、行と列のグループ化を解除しなければならない状況に遭遇することがあります。スプレッドシートをクリーンアップする場合も、データをより見やすく再フォーマットする場合も、Aspose.Cells for .NET はプロセスを簡素化する優れたツールです。このチュートリアルでは、Aspose.Cells を使用して Excel の行と列のグループ化を解除する手順を説明します。最後には、Excel ファイルをプログラムで操作する方法をしっかりと理解できるようになります。
## 前提条件
コードに進む前に、すべてがセットアップされていることを確認しましょう。必要なものは次のとおりです。
1.  Visual Studio: お使いのマシンにVisual Studioの動作するバージョンがインストールされている必要があります。まだインストールしていない場合は、ここからダウンロードできます。[Visual Studioのサイト](https://visualstudio.microsoft.com/).
2. Aspose.Cells for .NET: Aspose.Cellsライブラリをダウンロードする必要があります。[Aspose リリース ページ](https://releases.aspose.com/cells/net/)必要なライセンスを持っていることを確認してください。ライセンスは購入または代理店を通じて取得できます。[一時ライセンス](https://purchase.aspose.com/temporary-license/).
3. C# の基礎知識: C# プログラミングの基礎を理解しておくと、より簡単に理解できるようになります。
すべての準備が整ったら、楽しい部分であるコードに取り掛かります。
## パッケージのインポート
まず、C# プロジェクトに必要なパッケージをインポートする必要があります。手順は次のとおりです。
1. Visual Studio でプロジェクトを開きます。
2. Aspose.Cells ライブラリへの参照を追加します。これを行うには、プロジェクト内の参照を右クリックし、[参照の追加] を選択します。Aspose.Cells DLL を保存した場所を参照します。
3. C# ファイルの先頭に、次の using ディレクティブを追加します。
```csharp
using System.IO;
using Aspose.Cells;
```
すべての設定が完了したら、Excel シートの行と列のグループを解除する手順を見ていきましょう。 
## ステップ1: ドキュメントディレクトリを定義する
まず、Excel ファイルが保存されているディレクトリを指定する必要があります。これは次のように設定できます。
```csharp
//ドキュメント ディレクトリへのパス。
string dataDir = "Your Document Directory";
```
交換する`"Your Document Directory"` Excel ファイルが保存されているコンピューター上の実際のパスを入力します。 
## ステップ2: ファイルストリームを作成する
次に、Excel ファイルを開くためのファイル ストリームを作成する必要があります。その方法は次のとおりです。
```csharp
//開くExcelファイルを含むファイルストリームを作成する
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
ここでは、`book1.xls`指定したディレクトリにこのファイルが存在することを確認してください。存在しない場合は、ファイルが見つからないというエラーが発生します。
## ステップ3: ワークブックオブジェクトをインスタンス化する
ここで、Excel ファイルを Workbook オブジェクトに読み込みます。これにより、プログラムでワークブックを操作できるようになります。
```csharp
//ワークブックオブジェクトのインスタンス化
//ファイルストリームを介してExcelファイルを開く
Workbook workbook = new Workbook(fstream);
```
このコード行により、Excel ファイルがメモリに正常に読み込まれ、操作する準備が整いました。
## ステップ4: ワークシートにアクセスする
ワークブックを作成したら、次のステップは、行と列のグループ化を解除する特定のワークシートにアクセスすることです。その方法は次のとおりです。
```csharp
// Excelファイルの最初のワークシートにアクセスする
Worksheet worksheet = workbook.Worksheets[0];
```
この場合、最初のワークシートにアクセスしています。データが別のシートにある場合は、それに応じてインデックスを変更できます。
## ステップ5: 行のグループを解除する
次は面白い部分です! 最初の 6 行 (行 0 から行 5 まで) をグループ解除しましょう。次のコードを使用します。
```csharp
//最初の 6 行 (0 から 5) のグループを解除します
worksheet.Cells.UngroupRows(0, 5);
```
このメソッドは、指定された行に適用されているグループ化をすべて削除します。とても簡単です!
## ステップ6: 列のグループ化を解除する
行と同様に、列もグループ解除できます。最初の 3 つの列 (列 0 から列 2 まで) をグループ解除する方法は次のとおりです。
```csharp
//最初の 3 列のグループを解除します (0 から 2)
worksheet.Cells.UngroupColumns(0, 2);
```
## ステップ7: 変更したExcelファイルを保存する
行と列のグループ化を解除したら、次のステップは変更内容をExcelファイルに保存することです。これを行うには、`Save`方法：
```csharp
//変更したExcelファイルを保存する
workbook.Save(dataDir + "output.xls");
```
この例では、変更したファイルを次のように保存します。`output.xls`ファイル名は好きな名前に変更できます。
## ステップ8: ファイルストリームを閉じる
最後に、リソースを解放するには、ファイル ストリームを閉じる必要があります。
```csharp
//ファイルストリームを閉じてすべてのリソースを解放する
fstream.Close();
```
これは、アプリケーションがファイル ハンドルを必要以上に長く保持しないようにするための良い方法です。
## 結論
これで完了です。Aspose.Cells for .NET を使用して Excel ファイル内の行と列をグループ化解除する方法を学習しました。わずか数行のコードで、プログラムによって Excel ファイルに大幅な変更を加えることができます。レポートを自動化する場合でも、分析用にデータを準備する場合でも、これらのテクニックを習得すると、時間を大幅に節約できます。
## よくある質問
### Aspose.Cells とは何ですか?
Aspose.Cells は、.NET アプリケーションで Excel ファイルを操作するための強力なライブラリであり、スプレッドシートの操作、変換、作成を簡単に行うことができます。
### 他のライブラリを使用して Excel の行と列のグループを解除できますか?
はい、.NET で Excel を操作するための他のライブラリもありますが、Aspose.Cells は豊富な機能と使いやすさを提供します。
### 保存後に変更を元に戻す方法はありますか?
Excel ファイルを保存すると、元のファイルのバックアップがない限り、以前の状態を復元することはできません。
### Aspose.Cells のサポートを受けるにはどうすればよいですか?
サポートについては、[Aspose サポートフォーラム](https://forum.aspose.com/c/cells/9)、質問したり解決策を見つけたりできる場所です。
### ライセンスなしで Aspose.Cells を使用できますか?
はい、Aspose.Cellsは一定の制限付きで無料で使用でき、[一時ライセンス](https://purchase.aspose.com/temporary-license/)完全な機能を実現します。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
