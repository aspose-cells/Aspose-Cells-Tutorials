---
"description": "この詳細なチュートリアルでは、Aspose.Cells for .NET を使用して、指定された数式フィールドを持つ Excel シートにデータをインポートする方法を学習します。"
"linktitle": "Excelシートにデータをインポートするときに数式フィールドを指定する"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": "Excelシートにデータをインポートするときに数式フィールドを指定する"
"url": "/ja/net/excel-custom-number-date-formatting/specify-formula-fields-while-importing-data-to-worksheet-in-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excelシートにデータをインポートするときに数式フィールドを指定する

## 導入

Excelファイルをプログラムで操作する場合、Aspose.Cells for .NETは非常に便利なツールです。Excelスプレッドシートを簡単に作成、変更、操作するための強力な機能を提供します。特に興味深い機能の一つは、Excelシートにデータをインポートする際に数式フィールドを指定できることです。例えば、財務レポートを作成中で、ユーザー入力に基づいて合計を自動計算する必要がある場合を想像してみてください。このチュートリアルでは、シンプルで分かりやすいアプローチで、まさにそれを実現する方法をステップバイステップで解説します。

## 前提条件

コードに進む前に、必要なものがすべて揃っていることを確認しましょう。 

1. Visual Studio または任意の .NET 統合開発環境 (IDE): C# コードを記述して実行するには適切な IDE があることを確認してください。
2. Aspose.Cells for .NET: プロジェクトでAspose.Cellsライブラリをダウンロードして参照する必要があります。ダウンロードは以下から行えます。 [Asposeリリース](https://releases。aspose.com/cells/net/).
3. 基本的な C# の知識: C# とオブジェクト指向プログラミングの概念を理解していると、例をよりよく理解するのに役立ちます。
4. .NET Framework: このチュートリアルでは、.NET Framework 4.5 以降を使用していることを前提としています。

前提条件を整理したら、指定された数式フィールドを持つ Excel シートにデータをインポートしてみましょう。

## パッケージのインポート

コードを書き始める前に、必要なAspose.Cells名前空間をインポートする必要があります。これは通常、C#ファイルの先頭で行います。

```csharp
using Aspose.Cells;
using System;
using System.Collections.Generic;
```

これにより、毎回名前空間をプレフィックスとして付けなくても、Aspose.Cells ライブラリによって提供されるクラスとメソッドを使用できるようになります。

プロセス全体を管理しやすいステップに分解してみましょう。

## ステップ1: 出力ディレクトリを定義する

まず、Excelファイルを保存する場所を決める必要があります。手順は以下のとおりです。

```csharp
static string outputDir = "Your Document Directory"; // ここでドキュメントディレクトリを指定してください
```

交換する `"Your Document Directory"` 実際のファイルパスを入力します。生成されたExcelファイルはここに保存されます。

## ステップ2: データ項目のユーザー定義クラスを作成する

次に、インポートする予定のデータを構造化するクラスを定義します。

```csharp
class DataItems
{
    public int Number1 { get; set; }
    public int Number2 { get; set; }
    public string Formula1 { get; set; }
    public string Formula2 { get; set; }
}
```

これ `DataItems` クラスは、Excel シートに書き込む生の整数と数式を保持します。 

## ステップ3: データ項目を保持するリストを初期化する

リストを使用して、複数のインスタンスを保持します。 `DataItems` クラス。

```csharp
List<DataItems> dis = new List<DataItems>();
```

## ステップ4: リストにデータ項目を追加する

それでは、リストにいくつかのエントリを追加してみましょう。各エントリには2つの数値と2つの数式が含まれます。

```csharp
// 各データ項目を定義して追加する
DataItems di = new DataItems();
di.Number1 = 2002;
di.Number2 = 3502;
di.Formula1 = "=SUM(A2,B2)";
di.Formula2 = "=HYPERLINK(\"https://www.aspose.com\",\"Aspose ウェブサイト\")";
dis.Add(di);

// 追加のデータ項目について繰り返します
```

それぞれをカスタマイズしてください `DataItems` 一意の値と数式を持つインスタンス。

## ステップ5: ワークブックとアクセスワークシートを作成する

次に、ワークブックを作成し、最終的にデータをインポートする最初のワークシートにアクセスします。

```csharp
Workbook wb = new Workbook(); // 新しいワークブックを作成する
Worksheet ws = wb.Worksheets[0]; // 最初のワークシートにアクセスする
```

## ステップ6: インポートテーブルオプションを指定する

ここで魔法が起こります。データ内のどのフィールドが数式に対応するかを指定する必要があります。 

```csharp
ImportTableOptions opts = new ImportTableOptions();
opts.IsFormulas = new bool[] { false, false, true, true };
```

この例では、最後の2つのフィールドには数式が含まれており、 `true`最初の2つのフィールドは `false`。

## ステップ7: カスタムオブジェクトのインポート

すべての設定が完了したら、データ項目のリストをワークシートにインポートしましょう。

```csharp
ws.Cells.ImportCustomObjects(dis, 0, 0, opts);
```

この行は、セル A1 から始まるデータを効果的にインポートします。

## ステップ8: 数式を計算する

いくつかの数式をインポートしたので、それらを計算することが重要です。

```csharp
wb.CalculateFormula();
```

この方法により、数式は依存関係に基づいて評価されるようになります。

## ステップ9: 列の自動調整

データが適切に表示されるように、コンテンツに基づいて列を自動調整することができます。

```csharp
ws.AutoFitColumns();
```

この手順では、Excel ファイルのレイアウトが最適化されます。 

## ステップ10: Excelファイルを保存する

最後に、新しく作成した Excel ファイルを保存します。 

```csharp
wb.Save(outputDir + "outputSpecifyFormulaFieldsWhileImportingDataToWorksheet.xlsx");
```

出力ファイル名が関連性があり、説明的なものであることを確認してください。

## ステップ11: 実行の確認

すべてが正しく実行されたことを確認する簡単な方法として、メッセージを印刷することができます。

```csharp
Console.WriteLine("SpecifyFormulaFieldsWhileImportingDataToWorksheet executed successfully.");
```

これにより、コードが問題なく動作したというフィードバックがすぐに得られます。

## 結論

これで完了です！Aspose.Cells for .NETと指定した数式フィールドを使って、Excelシートにデータをインポートできました。これらの手順に従うことで、同様のテクニックを適用し、ニーズに合わせてデータ処理タスクを自動化できます。レポート用の数値計算を行う場合でも、単にデータをメンテナンスする場合でも、Asposeを使ったExcel操作のスキルを習得することは、習得する価値のあるスキルです。

## よくある質問

### Aspose.Cells とは何ですか?
Aspose.Cells は、Excel ファイルをプログラムで作成、操作、変換するために設計された .NET ライブラリです。

### Aspose.Cells for .NET をインストールするにはどうすればよいですか?
ダウンロードはこちらから [Asposeリリース](https://releases.aspose.com/cells/net/) プロジェクト内で参照します。

### Aspose.Cells を無料で使用できますか?
はい、Asposeは無料トライアルを提供しています。 [このリンク](https://releases。aspose.com/).

### さらに例はどこで見つかりますか?
追加の例とドキュメントは、 [Aspose ドキュメントページ](https://reference。aspose.com/cells/net/).

### Aspose の使用中に問題が発生した場合はどうすればよいですか?
Asposeサポートフォーラムからサポートを受けることができます [ここ](https://forum。aspose.com/c/cells/9).
 

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}