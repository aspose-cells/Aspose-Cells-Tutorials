---
"description": "Aspose.Cells for .NET を使用すると、Excel の Power Query 数式項目を簡単に更新できます。データ操作プロセスを効率化するためのステップバイステップガイドです。"
"linktitle": "Power Query の数式項目を更新する"
"second_title": "Aspose.Cells for .NET API リファレンス"
"title": "Power Query の数式項目を更新する"
"url": "/ja/net/excel-workbook/update-power-query-formula-item/"
"weight": 160
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Power Query の数式項目を更新する

## 導入

Excelを使ったことがある方なら、その強力さをご存知でしょう。特にPower Queriesを使い始めると、その威力は格段に増します。Power Queriesは、データの変換、クリーンアップ、分析をスムーズに行うための秘訣です。ExcelでPower Queryの数式を操作する便利な方法の一つが、Aspose.Cells for .NETです。本日は、Power Queryの数式項目を更新する方法をステップバイステップで解説します。さあ、コーディングの準備を始めましょう！

## 前提条件

コードに進む前に、設定しておきたいことがいくつかあります。

1. Visual Studio: .NET コードを記述して実行するには、統合開発環境 (IDE) が必要です。Visual Studio が最適です。
2. Aspose.Cellsライブラリ：プロジェクト内でAspose.Cellsライブラリが利用可能であることを確認してください。ダウンロードは以下から行えます。 [サイト](https://releases。aspose.com/cells/net/).
3. C# の基本知識: これについては一緒に進めていきますが、C# の基礎知識をある程度持っていると、特にさまざまなクラスやメソッドを操作するときに役立ちます。
4. サンプルExcelファイル：コードスニペットに記載されているExcelファイルが必要です。以下のものをご用意ください。
   - `SamplePowerQueryFormula.xlsx`
   - `SamplePowerQueryFormulaSource.xlsx`

5. .NET Framework: プロジェクトが互換性のあるバージョンの .NET Framework を対象としていることを確認します。

キットの準備ができたので、楽しい部分、つまりコードの記述に進むことができます。

## パッケージのインポート

まず最初に、必要な名前空間をインポートします。手順は以下のとおりです。

```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```

これらの名前空間を追加することで、Aspose.Cellsライブラリのクラスとメソッドを使用することをコンパイラに通知します。このステップは、後続のコードの基礎となるため、非常に重要です。

ご提供いただいたコードスニペットを詳しく見ていきましょう。このチュートリアルでは、各部分を順に解説し、何が起こっているのかを理解できるようにします。

## ステップ1: 作業ディレクトリを設定する

このステップでは、ソースファイルと出力ファイルの場所を定義します。これにより、Aspose は Excel ファイルの場所を特定できるようになります。

```csharp
// 作業ディレクトリ
string SourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

## ステップ2: ワークブックを読み込む

ここで、Power Query が存在する Excel ファイルを読み込みます。

```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
その `Workbook` クラスはExcelファイルへのエントリポイントです。ソースファイルのパスを渡すことで、ファイルを操作するためのインスタンスを作成します。これは本を開くようなもので、内容を読む（または編集する）準備をすることになります。

## ステップ3: データマッシュアップにアクセスする

次に、ワークブックのデータ マッシュアップに保存されている Power Query 数式にアクセスします。

```csharp
DataMashup mashupData = workbook.DataMashup;
```
その `DataMashup` クラスには、ブックに関連付けられたすべてのPower Query式が含まれています。修理のために工具箱を開けるときのように、ここで重要な処理を行います。

## ステップ4: Power Queryの数式をループする

ここで、Power Query の数式を反復処理して、更新する特定の数式を検索します。

```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```

- それぞれをループします `PowerQueryFormula` で `mashupData`。
- そのループの中で、私たちはそれぞれに深く入り込みます `PowerQueryFormulaItem`。
- アイテムの名前が「ソース」と一致するかどうかを確認します。一致する場合は、その値を更新して新しいソース ファイルにリンクします。

これは、マニュアルで適切なページを見つけて、必要な更新を行うのと似ており、単純かつ細心の注意を要するプロセスです。

## ステップ5: 更新されたワークブックを保存する

更新が完了したら、変更を保存します。

```csharp
// 出力ワークブックを保存します。
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
その `Save` このメソッドは、更新されたワークブックを指定された出力ディレクトリに書き込みます。これは、編集内容を新しいバージョンのマニュアルに封印し、他の人がすぐに使えるようにするようなものです。

## 結論

おめでとうございます！Aspose.Cells for .NET を使用して Power Query の数式アイテムを更新できました。この方法を使えば、Excel ファイル内の Power Query の数式の変更を自動化できるため、貴重な時間と労力を節約できます。

## よくある質問

### Aspose.Cells とは何ですか?
Aspose.Cells は、Microsoft Excel をインストールしなくても .NET アプリケーションで Excel ファイルを操作するための強力なライブラリです。

### Aspose.Cells を実行するには Microsoft Excel が必要ですか?
いいえ、Aspose.Cells を使用すると、サーバーまたは開発マシンに Excel がなくても、プログラムで Excel ファイルを作成および編集できます。

### Aspose.Cells を使用してどのような種類の Excel ファイルを扱うことができますか?
Aspose.Cells を使用すると、.xlsx、.xls、.xlsm、およびその他のいくつかの Excel 形式を操作できます。

### Aspose.Cells の試用版はありますか?
はい、無料試用版をこちらからダウンロードできます。 [Aspose Cells リリースページ](https://releases。aspose.com/).

### Aspose.Cells のサポートを受けるにはどうすればよいですか?
サポートは以下からアクセスできます。 [Asposeフォーラム](https://forum.aspose.com/c/cells/9)ここでは、コミュニティや Aspose チームに質問して回答を得ることができます。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}