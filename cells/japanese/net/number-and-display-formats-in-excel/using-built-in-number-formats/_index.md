---
"description": "Aspose.Cells for .NET を使用して、Excel の数値書式設定を自動化します。日付、パーセンテージ、通貨の書式をプログラムで適用する方法を学びます。"
"linktitle": "Excel の組み込み数値書式をプログラムで使用する"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": "Excel の組み込み数値書式をプログラムで使用する"
"url": "/ja/net/number-and-display-formats-in-excel/using-built-in-number-formats/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel の組み込み数値書式をプログラムで使用する

## 導入
このチュートリアルでは、Aspose.Cells for .NET を使って Excel の組み込み数値書式を設定する方法を詳しく説明します。環境設定から日付、パーセンテージ、通貨などの様々な書式の適用まで、あらゆる手順を網羅しています。熟練のプロの方でも、.NET エコシステムに初めて触れる方でも、このガイドを使えば Excel のセルの書式設定が驚くほど簡単にできるようになります。
## 前提条件
始める前に、次のものを用意してください。
- Aspose.Cells for .NETライブラリがインストールされています。 [ここからダウンロード](https://releases。aspose.com/cells/net/).
- C# および基本的な .NET プログラミングに関する実用的な知識。
- マシンにインストールされている Visual Studio または任意の .NET IDE。
- 有効なAsposeライセンスまたは [一時ライセンス](https://purchase。aspose.com/temporary-license/).
- .NET Framework がインストールされている (バージョン 4.0 以上)。
  
上記のいずれかが不足している場合は、提供されているリンクに従って設定してください。準備はいいですか？さあ、楽しい部分に入りましょう！
## パッケージのインポート
チュートリアルを始める前に、Aspose.Cells for .NET を操作するために必要な名前空間をインポートしておいてください。
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
これらをインポートしたら、Excelファイルをプログラムで操作する準備は完了です。それでは、ステップバイステップガイドをご覧ください。
## ステップ1: Excelブックを作成またはアクセスする
このステップでは、新しいワークブックを作成します。これは、コードを使って新しいExcelファイルを開くのと似ています。
```csharp
// ドキュメント ディレクトリへのパス。
string dataDir = "Your Document Directory";
// ディレクトリがまだ存在しない場合は作成します。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Workbookオブジェクトのインスタンス化
Workbook workbook = new Workbook();
```
ここでは、単に新しいインスタンスを作成しています `Workbook` オブジェクトです。これはExcelファイルとして機能し、データ操作の準備が整います。パスを指定して既存のファイルを読み込むこともできます。
## ステップ2: ワークシートにアクセスする
Excelブックには複数のワークシートを含めることができます。この手順では、ブックの最初のワークシートにアクセスします。
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
ワークブックの最初のワークシートにアクセスしています。追加のシートを操作する必要がある場合は、インデックスまたは名前を使用して参照できます。
## ステップ3: セルにデータを追加する
特定のセルにデータを追加してみましょう。まず、現在のシステム日付をセル「A1」に挿入します。
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
この行は、セルA1に現在の日付を挿入します。かなり便利ですよね？これを何百ものセルに手動で行うとしたら、悪夢のような作業になるでしょう。さて、次は書式設定に移りましょう！
## ステップ4：セル「A1」の日付をフォーマットする
次に、日付を「15-Oct-24」のように読みやすい形式にフォーマットしてみましょう。Aspose.Cellsの真価が発揮されるのはここです。
1. セルのスタイルを取得します。
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
ここでは、セルA1のスタイルを取得しています。これは、微調整を加える前のセルの「スタイル」を取得すると考えてください。
2. 日付の形式を設定します。
```csharp
style.Number = 15;
```
設定 `Number` プロパティを15に設定すると、希望する日付形式が適用されます。これは、日付を「d-mmm-yy」形式で表示するための組み込みの数値書式コードです。
3. セルにスタイルを適用する:
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
この行はセルにスタイルの変更を適用します。これで、デフォルトの日付形式ではなく、「15-Oct-24」のような、よりユーザーフレンドリーな形式が表示されます。
## ステップ5: セル「A2」にパーセンテージを追加して書式設定する
パーセンテージの書式設定に移りましょう。値を挿入し、それをパーセンテージで表示したいとします。この手順では、セル「A2」に数値を追加し、パーセンテージとして書式設定します。
1. 数値を挿入:
```csharp
worksheet.Cells["A2"].PutValue(20);
```
これでセルA2に20という数字が挿入されます。「ただの数字なのに、どうやってパーセンテージに変換すればいいの？」と思われるかもしれませんが、その方法については後ほど説明します。
2. スタイルを取得し、パーセンテージ形式を設定します。
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  // パーセンテージでフォーマット
worksheet.Cells["A2"].SetStyle(style);
    ```
Setting the `Number` property to 9 applies the built-in percentage format. Now the value in A2 will be displayed as "2000%." (Yes, 20 is treated as 2000% in percentage formatting).
## Step 6: Add and Format Currency in Cell "A3"
Now, let’s add a numeric value in cell A3 and format it as currency. This is a common use case for financial reports.
1. Insert Numeric Value:
```csharp
worksheet.Cells["A3"].PutValue(2546);
```
ここでは、セルA3に2546を加算します。次に、この数値を通貨として表示するように書式設定します。
2. スタイルを取得し、通貨形式を設定します。
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // 通貨としてフォーマット
worksheet.Cells["A3"].SetStyle(style);
```
設定 `Number` プロパティを6に設定すると、通貨形式が適用されます。これでセルA3の値は「2,546.00」と表示され、カンマと小数点以下2桁まで表示されます。
## ステップ7: Excelファイルを保存する
すべての書式設定の魔法を適用したので、ファイルを保存します。
```csharp
// Excelファイルを保存する
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
この行はExcelファイルをExcel 97-2003形式で保存します。 `SaveFormat` ニーズに合わせて。これで、プログラムでExcelファイルを作成し、フォーマットすることができました。
## 結論
おめでとうございます！Aspose.Cells for .NET を使って、Excel ファイルのセルに組み込みの数値書式を適用する方法を習得しました。日付からパーセンテージ、通貨まで、Excel データ処理でよく使われる書式設定をいくつか解説しました。これで、セルの書式設定を手動で行う代わりに、プロセス全体を自動化できるため、時間の節約とエラーの削減につながります。
## よくある質問
### Aspose.Cells for .NET を使用してカスタム数値形式を適用できますか?
はい！Aspose.Cellsは、組み込みの書式に加えて、カスタム数値書式もサポートしています。 `Custom` の財産 `Style` クラス。
### 特定の記号を使用してセルを通貨としてフォーマットするにはどうすればよいですか?
特定の通貨記号を適用するには、 `Style.Custom` 財産。
### 行全体または列全体をフォーマットできますか?
もちろんです！行全体または列全体にスタイルを適用するには、 `Rows` または `Columns` コレクションの `Worksheet` 物体。
### 複数のセルを一度にフォーマットするにはどうすればいいですか?
使用することができます `Range` オブジェクトを使用して複数のセルを選択し、それらすべてに一度でスタイルを適用します。
### Aspose.Cells を使用するには Microsoft Excel をインストールする必要がありますか?
いいえ、Aspose.Cells は Microsoft Excel とは独立して動作するため、マシンに Excel をインストールする必要はありません。


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}