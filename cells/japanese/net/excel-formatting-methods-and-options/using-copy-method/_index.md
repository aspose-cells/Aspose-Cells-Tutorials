---
title: Excel でプログラム的にコピー メソッドを使用する
linktitle: Excel でプログラム的にコピー メソッドを使用する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET のコピー メソッドを使用して Excel ファイルを効率的に操作する方法を学びます。ステップ バイ ステップ ガイドが含まれています。
weight: 10
url: /ja/net/excel-formatting-methods-and-options/using-copy-method/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel でプログラム的にコピー メソッドを使用する

## 導入
スプレッドシートをプログラムで管理および操作する場合、Aspose.Cells for .NET は時間を節約し、ワークフローを効率化できる強力なツールです。開発者が直面する一般的なタスクの 1 つは、Excel ブック内の 1 つのワークシートから別のワークシートに範囲をコピーする必要があることです。このチュートリアルでは、Aspose.Cells の Copy メソッドの使用方法を、わかりやすい説明とコード例を使用して各手順を順を追って説明します。
## 前提条件
Copy メソッドの使用手順に進む前に、次の前提条件が満たされていることを確認する必要があります。
1. .NET Framework: .NET Frameworkがマシンにインストールされていることを確認してください。Aspose.Cellsはさまざまなバージョンと互換性があるので、[ドキュメント](https://reference.aspose.com/cells/net/)詳細については。
2. Visual Studio: .NET 開発用に Visual Studio または互換性のある IDE をセットアップしておくことが不可欠です。これにより、プロジェクトを快適に作成および管理できるようになります。
3.  Aspose.Cellsライブラリ: Aspose.Cellsライブラリを以下からダウンロードしてください。[リリースページ](https://releases.aspose.com/cells/net/)プロジェクトに参照を追加します。
4. サンプルExcelファイル: Excelファイルを作成するか、用意しておきます（例：`Book1.xlsx`) を使用します。
5. 基本的な C# の知識: C# 言語の概念と構文に精通していること。
これらの前提条件が満たされると、コーディングを開始する準備が整います。
## パッケージのインポート
Aspose.Cells が提供する機能を利用するには、必要なパッケージをインポートする必要があります。C# プロジェクトでは、コード ファイルの先頭に次の using ディレクティブを含めるようにしてください。
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
これにより、Excel ファイルを簡単に操作するために必要なクラスとメソッドにアクセスできるようになります。
これで準備はすべて整いましたので、Copy メソッドを使用するプロセスを管理しやすいステップに分解してみましょう。まず Excel ファイルを読み込み、目的の範囲をコピーします。
## ステップ1: ファイルストリームの設定
最初のステップは、Excel ファイルを開いて操作できるようにするファイル ストリームを作成することです。手順は次のとおりです。
```csharp
//ドキュメント ディレクトリへのパス。
string dataDir = "Your Document Directory";
//開くExcelファイルを含むファイルストリームを作成する
FileStream fstream = new FileStream(dataDir + "Book1.xlsx", FileMode.Open);
```
このコードでは、`Book1.xlsx`ファイルが見つかります。`FileMode.Open`パラメータは、既存のファイルを開くことを示します。
## ステップ2: ワークブックを開く
次に、先ほど設定したファイル ストリームを使用して Workbook オブジェクトを作成します。これにより、Excel ファイルのコンテンツにアクセスできるようになります。
```csharp
//ファイルストリームを介してExcelファイルを開く
Workbook workbook = new Workbook(fstream);
```
この時点で、ワークブックが開かれ、その内容の操作を開始できます。
## ステップ3: ワークシートにアクセスする
ワークブックが読み込まれたら、作業する特定のワークシートにアクセスする必要があります。通常、これはワークブックの最初のワークシートになります。
```csharp
// Excelファイルの最初のワークシートにアクセスする
Worksheet worksheet = workbook.Worksheets[0];
```
ここ、`Worksheets[0]`最初のシートを取得します。他のワークシートにアクセスする場合は、インデックスを変更するだけです。
## ステップ4: 範囲のコピー
次は、セル範囲のコピーという主要部分です。このチュートリアルでは、条件付き書式設定をあるセルから別のセルにコピーする方法と、Excel シートの範囲全体をコピーする方法を説明します。
### 条件付き書式のコピー（例）
```csharp
//条件付き書式設定をセル「A1」からセル「B1」にコピーする
//worksheet.CopyConditionalFormatting(0, 0, 0, 1);
```
この行は元のコードではコメント アウトされていますが、同じワークシートのセル A1 からセル B1 に条件付き書式をコピーする方法を示しています。パラメータは、コピー元セルとコピー先セルの行インデックスと列インデックスを表します。この機能が必要な場合は、コメントを解除できます。
### 範囲全体のコピー（例）
コピー機能をさらに拡張して、範囲全体をコピーすることもできます。そのためには、ループを使用してすべてのワークシートを調べます。
```csharp
int TotalRowCount = 0;
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    //各ワークシートへのアクセス
    Worksheet sourceSheet = workbook.Worksheets[i];
    //ワークシートの表示範囲を取得する
    Range sourceRange = sourceSheet.Cells.MaxDisplayRange;
    //宛先ワークシートに範囲を作成する
    Range destRange = worksheet.Cells.CreateRange(
        sourceRange.FirstRow + TotalRowCount,
        sourceRange.FirstColumn,
        sourceRange.RowCount,
        sourceRange.ColumnCount);
    //ソース範囲を宛先範囲にコピーする
    destRange.Copy(sourceRange);
    //次のループ反復の合計行数を更新する
    TotalRowCount += sourceRange.RowCount; 
}
```
## ステップ5: 変更したワークブックを保存する
必要な範囲をコピーした後、変更内容を保持するために変更したブックを保存します。手順は次のとおりです。
```csharp
//変更したExcelファイルを保存する
workbook.Save(dataDir + "output.xls");
```
このコードは変更したワークブックを次のように保存します。`output.xls`指定したディレクトリに保存されます。ニーズに合った適切な形式を選択してください。 
## ステップ6: ファイルストリームを閉じる
最後に、システム リソースを確実に解放するために、最初に開いたファイル ストリームを閉じる必要があります。
```csharp
//ファイルストリームを閉じてすべてのリソースを解放する
fstream.Close();
```
これで、範囲のコピーと更新された Excel ファイルの保存のプロセスが正常に完了しました。
## 結論
Aspose.Cells for .NET の Copy メソッドを使用すると、Excel ファイルを簡単に操作できる強力な機能が提供されます。このステップ バイ ステップ ガイドに従うことで、セル範囲と条件付き書式を 1 つのワークシートから別のワークシートに効果的にコピーし、データ管理タスクを効率化できます。 
## よくある質問
### Aspose.Cells for .NET とは何ですか?
Aspose.Cells for .NET は、開発者が .NET アプリケーションでプログラムによって Excel ファイルを作成、操作、管理できるようにするライブラリです。
### Aspose.Cells を使用して書式、数式、値をコピーできますか?
はい、Aspose.Cells を使用すると、範囲間で値だけでなく書式や数式もコピーできます。
### Aspose.Cells は無料で使用できますか?
 Aspose.Cellsは無料トライアルを提供していますが、継続して使用するにはライセンスを購入する必要があります。詳細については、[ここ](https://purchase.aspose.com/buy).
### 問題が発生した場合、どうすればサポートを受けることができますか?
 Asposeサポートフォーラムでサポートを受けることができます。[ここ](https://forum.aspose.com/c/cells/9).
### Aspose.Cells ライブラリはどこからダウンロードできますか?
ライブラリはリリースページからダウンロードできます。[ここ](https://releases.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
