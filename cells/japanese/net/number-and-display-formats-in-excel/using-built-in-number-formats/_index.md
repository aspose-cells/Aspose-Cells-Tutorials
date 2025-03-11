---
title: Excel の組み込み数値書式をプログラムで使用する
linktitle: Excel の組み込み数値書式をプログラムで使用する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して、Excel での数値書式設定を自動化します。日付、パーセンテージ、通貨の書式をプログラムで適用する方法を学びます。
weight: 10
url: /ja/net/number-and-display-formats-in-excel/using-built-in-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel の組み込み数値書式をプログラムで使用する

## 導入
このチュートリアルでは、Aspose.Cells for .NET を使用して Excel の組み込み数値書式を使用する方法について説明します。環境の設定から、日付、パーセンテージ、通貨などのさまざまな書式の適用まで、すべてをカバーします。熟練したプロでも、.NET エコシステムに足を踏み入れたばかりでも、このガイドを使用すると、Excel セルの書式設定が簡単にできるようになります。
## 前提条件
始める前に、以下のものを用意しておいてください。
-  Aspose.Cells for .NETライブラリがインストールされています。[ここからダウンロード](https://releases.aspose.com/cells/net/).
- C# および基本的な .NET プログラミングに関する実用的な知識。
- マシンにインストールされている Visual Studio または任意の .NET IDE。
- 有効なAsposeライセンスまたは[一時ライセンス](https://purchase.aspose.com/temporary-license/).
- .NET フレームワークがインストールされている (バージョン 4.0 以上)。
  
上記のいずれかが不足している場合は、提供されているリンクに従ってすべてを設定してください。準備はできましたか? 楽しい部分に飛び込みましょう!
## パッケージのインポート
チュートリアルを始める前に、Aspose.Cells for .NET を操作するために必要な名前空間をインポートしてください。
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
これらをインポートしたら、Excel ファイルをプログラムで操作する準備が整います。それでは、ステップバイステップのガイドを見ていきましょう。
## ステップ1: Excelブックを作成またはアクセスする
この手順では、新しいブックを作成します。これは、コードを使用して新しい Excel ファイルを開くことと同じだと考えてください。
```csharp
//ドキュメント ディレクトリへのパス。
string dataDir = "Your Document Directory";
//ディレクトリがまだ存在しない場合は作成します。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
//ワークブックオブジェクトのインスタンス化
Workbook workbook = new Workbook();
```
ここでは、単に新しいインスタンスを作成しています`Workbook`オブジェクト。これは Excel ファイルとして機能し、データ操作の準備が整います。パスを指定して既存のファイルを読み込むこともできます。
## ステップ2: ワークシートにアクセスする
Excel ブックには複数のワークシートを含めることができます。この手順では、ブックの最初のワークシートにアクセスします。
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
これで、ワークブックの最初のワークシートにアクセスできるようになりました。追加のシートを操作する必要がある場合は、インデックスまたは名前を使用して参照できます。
## ステップ3: セルにデータを追加する
特定のセルにデータを追加してみましょう。まず、現在のシステム日付をセル「A1」に挿入します。
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
この行は、セル A1 に現在の日付を挿入します。かなり便利ですよね。これを何百ものセルに対して手動で行うとしたら、悪夢です。では、書式設定に移りましょう。
## ステップ4: セル「A1」の日付をフォーマットする
次に、その日付を「15-Oct-24」のように、より読みやすい形式にフォーマットしてみましょう。ここで Aspose.Cells が真価を発揮します。
1. セルのスタイルを取得します。
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
ここでは、セル A1 のスタイルを取得しています。これは、微調整を行う前にセルの「スタイル」を取得することと考えてください。
2. 日付の形式を設定します。
```csharp
style.Number = 15;
```
設定`Number`プロパティを 15 に設定すると、希望する日付形式が適用されます。これは、日付を「d-mmm-yy」形式で表示するための組み込みの数値形式コードです。
3. セルにスタイルを適用します。
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
この行は、セルにスタイルの変更を適用します。これで、デフォルトの日付形式の代わりに、「15-Oct-24」のような、よりユーザーフレンドリな形式が表示されます。
## ステップ 5: セル「A2」にパーセンテージを追加して書式設定する
パーセンテージの書式設定に移りましょう。値を挿入して、それをパーセンテージとして表示したいとします。この手順では、セル「A2」に数値を追加し、それをパーセンテージとして書式設定します。
1. 数値を挿入:
```csharp
worksheet.Cells["A2"].PutValue(20);
```
これにより、セル A2 に数字 20 が挿入されます。「これは単なる数字です。これをパーセンテージに変換するにはどうすればいいのでしょうか?」と思われるかもしれません。その方法については、これから説明します。
2. スタイルを取得し、パーセンテージ形式を設定します。
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  //パーセンテージでフォーマット
worksheet.Cells["A2"].SetStyle(style);
    ```
Setting the `Number` property to 9 applies the built-in percentage format. Now the value in A2 will be displayed as "2000%." (Yes, 20 is treated as 2000% in percentage formatting).
## Step 6: Add and Format Currency in Cell "A3"
Now, let’s add a numeric value in cell A3 and format it as currency. This is a common use case for financial reports.
1. Insert Numeric Value:
```csharp
worksheet.Cells["A3"].PutValue(2546);
```
ここでは、セル A3 に 2546 を追加します。次に、この数値を通貨として表示するように書式設定します。
2. スタイルを取得し、通貨形式を設定します。
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  //通貨としてフォーマット
worksheet.Cells["A3"].SetStyle(style);
```
設定`Number`プロパティを 6 に設定すると、通貨形式が適用されます。これで、セル A3 の値は、コンマと小数点 2 桁を含む「2,546.00」と表示されます。
## ステップ7: Excelファイルを保存する
すべての書式設定の魔法を適用したので、ファイルを保存します。
```csharp
// Excelファイルの保存
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
この行はExcelファイルをExcel 97-2003形式で保存します。`SaveFormat`ニーズに合わせて。これで、Excel ファイルをプログラムで作成し、フォーマットすることができました。
## 結論
おめでとうございます。Aspose.Cells for .NET を使用して、Excel ファイルのセルに組み込みの数値書式を適用する方法を学習しました。日付からパーセンテージ、通貨まで、Excel データ処理で最も一般的な書式設定のニーズをいくつか取り上げました。これで、セルを手動で書式設定する代わりに、プロセス全体を自動化して、時間を節約し、エラーを減らすことができます。
## よくある質問
### Aspose.Cells for .NET を使用してカスタム数値書式を適用できますか?
はい！組み込みの書式に加えて、Aspose.Cellsはカスタム数値書式もサポートしています。`Custom`の財産`Style`クラス。
### 特定の記号を使用してセルを通貨としてフォーマットするにはどうすればよいですか?
特定の通貨記号を適用するには、カスタム書式設定を使用して、`Style.Custom`財産。
### 行全体または列全体をフォーマットできますか?
もちろんです！行全体または列全体にスタイルを適用するには、`Rows`または`Columns`コレクションの`Worksheet`物体。
### 複数のセルを一度にフォーマットするにはどうすればよいですか?
あなたは`Range`オブジェクトを使用して複数のセルを選択し、それらすべてに一度でスタイルを適用します。
### Aspose.Cells を使用するには Microsoft Excel をインストールする必要がありますか?
いいえ、Aspose.Cells は Microsoft Excel とは独立して動作するため、マシンに Excel をインストールする必要はありません。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
