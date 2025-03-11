---
title: Aspose.Cells for .NET を使用して行をコピーする
linktitle: Aspose.Cells for .NET を使用して行をコピーする
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して Excel ファイル内の行を効率的にコピーする方法を学びます。このステップ バイ ステップ ガイドは、データ管理のニーズに合わせて行のコピーを簡素化します。
weight: 11
url: /ja/net/row-and-column-management/copying-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells for .NET を使用して行をコピーする

## 導入
.NET 環境で Excel ファイルを操作する場合、Aspose.Cells for .NET はぜひ知っておくべき強力なツールです。これを使用すると、新しいワークシートの作成、セルの書式設定、行のコピーなどのタスクを自動化できます。大規模なデータセットの処理やテンプレート行の繰り返しを楽々と行うことを想像してみてください。Aspose.Cells for .NET を使用すると、これらのタスクが簡単に行えます。このチュートリアルでは、Excel ファイル内で行をコピーするという特定のタスクに焦点を当てます。前提条件、必要なパッケージのインポート、およびこのプロセスを簡単にするためのステップバイステップのガイドについて説明します。それでは、始めましょう。
## 前提条件
コードに進む前に、次のものが必要です。
1.  Aspose.Cells for .NET: 最新バージョンであることを確認してください。[ここからダウンロード](https://releases.aspose.com/cells/net/)または[無料トライアルを受ける](https://releases.aspose.com/).
2. 開発環境: Visual Studio などの .NET 互換環境。
3. C# の基礎知識: このガイドは初心者向けですが、C# に精通していると、各ステップをよりよく理解するのに役立ちます。
4. ライセンス: フルアクセスするには、[一時ライセンス](https://purchase.aspose.com/temporary-license/)必要であれば。
## パッケージのインポート
まず、コードに必要な名前空間をインポートしてください。これらのライブラリにより、Excel ファイルの処理に必要なクラスとメソッドにアクセスできるようになります。
```csharp
using System.IO;
using Aspose.Cells;
```
コードを簡単なステップに分解してみましょう。各ステップでは、Excel ブックを開いて、コピーされた行を含む更新されたファイルを保存するまでのプロセスをガイドします。
## ステップ1: ディレクトリへのパスを設定する
まず最初に、Excel ファイルが保存されているディレクトリ パスを設定する必要があります。これは、プログラムが作業するファイルの場所を認識できるようにワークスペースを設定することと考えてください。
```csharp
//ドキュメント ディレクトリへのパス。
string dataDir = "Your Document Directory";
```
交換する`"Your Document Directory"` Excelファイルが保存されているマシン上の実際のパス（`book1.xls`）が格納されます。
## ステップ2: 既存のExcelファイルを開く
パスが設定されたので、Excelファイルをプログラムに読み込みます。`Workbook` Aspose.Cells のクラスを使用すると、Excel ファイルを簡単に開いてアクセスできます。
```csharp
//既存の Excel ファイルを開きます。
Workbook excelWorkbook1 = new Workbook(dataDir + "book1.xls");
```
ここ、`excelWorkbook1`ワークブックオブジェクトには、`book1.xls`これにより、このファイル内のワークシート、セル、行を操作できるようになります。
## ステップ3: 目的のワークシートにアクセスする
ワークブックを開いたら、次の手順では行のコピーを実行するワークシートを選択します。この例では、ワークブックの最初のワークシートを操作します。
```csharp
//ワークブックの最初のワークシートを取得します。
Worksheet wsTemplate = excelWorkbook1.Worksheets[0];
```
の`Worksheets[0]`インデックスは最初のワークシートを選択します。データが別のワークシートにある場合は、それに応じてインデックスを調整します。
## ステップ4: ターゲット行をコピーする
ここで、チュートリアルの核心部分である行のコピーを行います。ここでは、同じワークシート内の行 2 (行はゼロ インデックスなのでインデックス 1) から行 16 (インデックス 15) までデータをコピーします。
```csharp
//データ、書式、画像、描画オブジェクトを含む 2 行目を 16 行目にコピーします。
wsTemplate.Cells.CopyRow(wsTemplate.Cells, 1, 15);
```
このコマンドでは、
- ソース行 (1): これはコピーする行で、Excel の行 2 に相当します。
- 貼り付け先行 (15): コピーした行を貼り付ける場所で、Excel の行 16 に相当します。
の`CopyRow`この方法は効率的です。データだけでなく、その行の書式、画像、オブジェクトもコピーします。
## ステップ5: 更新されたExcelファイルを保存する
行のコピーが完了したら、変更したExcelファイルを保存します。これにより、`excelWorkbook1`保存されます。
```csharp
// Excel ファイルを保存します。
excelWorkbook1.Save(dataDir + "output.xls");
```
ここでは、更新されたワークブックを次のように保存します。`output.xls`元のファイルと同じディレクトリに保存します。必要に応じてファイル名と場所を変更できます。
## 結論
これで完了です。わずか数行のコードで、Aspose.Cells for .NET を使用して Excel の行をコピーできました。このチュートリアルでは、ドキュメント パスの設定から更新されたファイルの保存まで、重要な手順について説明します。Aspose.Cells を使用すると、行のコピー、セルの書式設定、大規模なデータセットの処理など、Excel の操作が簡単になります。そのため、次に行間でデータを複製する必要がある場合は、その方法を正確に把握できます。
## よくある質問
### Aspose.Cells for .NET を使用して複数の行を一度にコピーできますか?  
はい、行をループして、`CopyRow`ループ内で複数の行をコピーするメソッド。
### 異なるワークシート間で行をコピーするにはどうすればよいですか?  
ソースと宛先のワークシートを`CopyRow`方法。この方法は、同じブック内の異なるワークシート間で機能します。
### Aspose.Cells for .NET はコピー時に行の書式設定を維持しますか?  
絶対に！`CopyRow`メソッドは、データ、書式、画像、さらには描画オブジェクトもコピーします。
### Aspose.Cells for .NET は .NET Core と互換性がありますか?  
はい、Aspose.Cells は .NET Framework、.NET Core、.NET Standard をサポートしており、さまざまな .NET 環境にわたって柔軟性を提供します。
### Aspose.Cells for .NET を使用するにはライセンスが必要ですか?  
無料トライアルもありますが、[一時ライセンスまたは完全ライセンス](https://purchase.aspose.com/buy)完全な機能と制限の解除のためには、 をお勧めします。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
