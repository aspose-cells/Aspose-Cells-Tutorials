---
title: .NET でプログラム的に Excel ファイルの互換性を指定する
linktitle: .NET でプログラム的に Excel ファイルの互換性を指定する
second_title: Aspose.Cells .NET Excel 処理 API
description: データの更新、互換性設定、セルの書式設定など、Aspose.Cells for .NET を使用して Excel ピボット テーブルを操作する方法を学習します。
weight: 23
url: /ja/net/creating-and-configuring-pivot-tables/specifying-compatibility/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET でプログラム的に Excel ファイルの互換性を指定する

## 導入

今日のデータ駆動型の世界では、Excel ファイルをプログラムで管理および操作することが、多くの開発者にとって不可欠になっています。.NET で Excel を使用している場合、Aspose.Cells は Excel ファイルの作成、読み取り、変更、保存を簡単にする強力なライブラリです。このライブラリの重要な機能の 1 つは、Excel ファイルの互換性をプログラムで指定できることです。このチュートリアルでは、Excel ファイルの操作方法、特に Aspose.Cells for .NET を使用した互換性の管理について説明します。最後には、データを更新および管理しながら、特にピボット テーブルの Excel ファイルの互換性を設定する方法を理解できます。

## 前提条件

コーディング段階に進む前に、次のものを用意してください。

1. C# の基礎知識: C# でコードを記述するため、この言語に精通しているとチュートリアルをよりよく理解するのに役立ちます。
2.  Aspose.Cells for .NETライブラリ:以下からダウンロードできます。[Aspose Cells リリース ページ](https://releases.aspose.com/cells/net/)まだお試しでない場合は、まずは無料トライアルで機能をご確認ください。
3. Visual Studio: C# コードを効率的に記述およびテストできる IDE。
4. サンプルExcelファイル: デモ用のピボットテーブルを含むサンプルExcelファイルがあることを確認してください。この例では、`sample-pivot-table.xlsx`.

これらの前提条件が整ったら、コーディング プロセスを始めましょう。

## パッケージのインポート

アプリケーションの作成を開始する前に、Aspose.Cells ライブラリを効果的に活用するために必要な名前空間をコードに含める必要があります。その方法は次のとおりです。

### Aspose.Cells 名前空間をインポートする

```csharp
using System.IO;
using System;
using Aspose.Cells;
using Aspose.Cells.Pivot;
using System.Drawing;
```

このコード行により、Aspose.Cells ライブラリ内のすべてのクラスとメソッドにアクセスできるようになります。

それでは、すべてが明確で理解しやすいように、プロセスを詳細に分解してみましょう。

## ステップ1: ディレクトリを設定する

まず最初に、Excel ファイルが保存されているディレクトリを設定します。正しいファイル パスを指定することが重要です。

```csharp
//ドキュメント ディレクトリへのパス。
string dataDir = "Your Document Directory";
```

ここで、`"Your Document Directory"`Excel ファイルへの実際のパスを入力します。ここにサンプルのピボット テーブル ファイルが格納されます。

## ステップ2: ソースExcelファイルを読み込む

次に、サンプルのピボット テーブルを含む Excel ファイルを読み込む必要があります。 

```csharp
//サンプルピボットテーブルを含むソースExcelファイルを読み込みます
Workbook wb = new Workbook(dataDir + "sample-pivot-table.xlsx");
```

このステップでは、`Workbook`指定された Excel ファイルを読み込むクラス。 

## ステップ3: ワークシートにアクセスする

ワークブックが読み込まれたので、ピボット テーブル データを含むワークシートにアクセスする必要があります。

```csharp
//ピボットテーブルデータを含む最初のワークシートにアクセスする
Worksheet dataSheet = wb.Worksheets[0];
```

ここでは、ピボット テーブルが配置されている最初のワークシートにアクセスします。Excel の構造に基づいて、他のワークシートをループしたり指定したりすることもできます。

## ステップ4: セルデータの操作

次に、ワークシート内のいくつかのセル値を変更します。 

### ステップ4.1: セルA3を変更する

まず、セル A3 にアクセスしてその値を設定してみましょう。

```csharp
//セルA3にアクセスし、そのデータを設定する
Cells cells = dataSheet.Cells;
Cell cell = cells["A3"];
cell.PutValue("FooBar");
```

このコード スニペットは、セル A3 を値「FooBar」で更新します。

### ステップ 4.2: 長い文字列でセル B3 を変更する

ここで、Excel の標準の文字数制限を超える長い文字列をセル B3 に設定してみましょう。

```csharp
//セルB3にアクセスし、そのデータを設定する
string longStr = "Very long text 1. very long text 2.... [continue your long string]";
cell = cells["B3"];
cell.PutValue(longStr);
```

このコードは、特に Excel の互換性設定で作業する場合に、データ制限に関する期待を設定するため重要です。

## ステップ5: セルB3の長さを確認する

入力した文字列の長さを確認することも重要です。

```csharp
//セルB3の文字列の長さを印刷する
Console.WriteLine("Length of original data string: " + cell.StringValue.Length);
```

これは、セルに保持されている文字数を確認するためのものです。

## ステップ6: 他のセルの値を設定する

ここで、さらに多くのセルにアクセスし、いくつかの値を設定します。

```csharp
//セルC3にアクセスし、そのデータを設定する
cell = cells["C3"];
cell.PutValue("closed");

//セルD3にアクセスし、そのデータを設定する
cell = cells["D3"];
cell.PutValue("2016/07/21");
```

これらの各スニペットは、ワークシート内のいくつかの追加セルを更新します。

## ステップ7: ピボットテーブルにアクセスする

次に、ピボット テーブル データで構成される 2 番目のワークシートにアクセスします。

```csharp
//ピボットテーブルを含む2番目のワークシートにアクセスする
Worksheet pivotSheet = wb.Worksheets[1];

//ピボットテーブルにアクセスする
PivotTable pivotTable = pivotSheet.PivotTables[0];
```

このスニペットを使用すると、互換性設定のピボット テーブルを操作できます。

## ステップ 8: Excel 2003 の互換性を設定する

ピボット テーブルが Excel 2003 と互換性があるかどうかを設定することは非常に重要です。 

```csharp
// IsExcel2003compatibleプロパティは、ピボットテーブルを更新するときにピボットテーブルがExcel2003と互換性があるかどうかを示します。
pivotTable.IsExcel2003Compatible = true;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

ここから本当の変革が始まります。`IsExcel2003Compatible`に`true`更新時に文字数制限を 255 文字までに制限します。

## ステップ9: 互換性設定後の長さを確認する

互換性を設定したら、それがデータにどのような影響を与えるかを見てみましょう。

```csharp
//ピボットシートのセル B5 の値を確認します。
Cell b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to True: " + b5.StringValue.Length);
```

初期データが 255 文字を超えると、切り捨て効果を確認する出力が表示される可能性があります。

## ステップ10: 互換性設定を変更する

それでは、互換性設定を変更して再度確認してみましょう。

```csharp
//IsExcel2003compatibleプロパティをfalseに設定し、再度更新します。
pivotTable.IsExcel2003Compatible = false;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

これにより、以前の制限なしに、データの元の長さを反映できるようになります。

## ステップ11: 長さを再度確認する 

データが実際の長さを正確に反映していることを確認しましょう。

```csharp
//これで、セル データの元の長さが印刷されます。データは切り捨てられていません。
b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to False: " + b5.StringValue.Length);
```

出力で切り捨てが削除されたことが確認されるはずです。

## ステップ12: セルの書式を設定する

視覚的なエクスペリエンスを向上させるには、セルをフォーマットすることをお勧めします。 

```csharp
//セルB5の行の高さと列の幅を設定し、テキストも折り返します
pivotSheet.Cells.SetRowHeight(b5.Row, 100);
pivotSheet.Cells.SetColumnWidth(b5.Column, 65);
Style st = b5.GetStyle();
st.IsTextWrapped = true;
b5.SetStyle(st);
```

これらのコード行は、セルのサイズを調整し、テキストの折り返しを有効にすることで、データを読みやすくします。

## ステップ13: ワークブックを保存する

最後に、変更を加えたワークブックを保存します。

```csharp
//ワークブックを xlsx 形式で保存する
wb.Save(dataDir + "SpecifyCompatibility_out.xlsx", SaveFormat.Xlsx);
```

Excelファイルを保存するときは、適切なファイル形式を選択することが重要です。`Xlsx`この形式は広く使用されており、多くの Excel バージョンと互換性があります。

## 結論

おめでとうございます。これで、Aspose.Cells for .NET を使用して Excel ファイルの互換性設定をプログラムできました。このチュートリアルでは、環境の設定からピボット テーブルの互換性設定の変更まで、各手順について説明しました。特定の制限や互換性を必要とするデータを扱ったことがある場合、これは見逃せないスキルです。

## よくある質問

### Aspose.Cells とは何ですか?  
Aspose.Cells は、開発者が Excel ファイルをシームレスに作成、操作、変換できるように設計された .NET ライブラリです。

### Excel の互換性が重要なのはなぜですか?  
Excel の互換性は、特に以前のバージョンではサポートされていない機能や形式が含まれている場合に、ファイルを目的のバージョンの Excel で開いて使用できることを保証するために重要です。

### Aspose.Cells を使用してプログラムでピボット テーブルを作成できますか?  
はい、Aspose.Cells を使用してプログラムでピボット テーブルを作成および操作できます。ライブラリには、ピボット テーブルに関連付けられたデータ ソース、フィールド、機能を追加するためのさまざまなメソッドが用意されています。

### Excel セル内の文字列の長さを確認するにはどうすればよいですか?  
あなたは`StringValue`の財産`Cell`オブジェクトを使用してセルの内容を取得し、`.Length`文字列の長さを調べるプロパティ。

### 行の高さや幅以外にもセルの書式をカスタマイズできますか?  
もちろんです！Aspose.Cellsでは、広範囲にわたるセルの書式設定が可能です。フォントスタイル、色、境界線、数値の書式などを、`Style`クラス。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
