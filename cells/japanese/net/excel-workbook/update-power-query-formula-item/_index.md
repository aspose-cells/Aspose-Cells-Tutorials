---
title: Power Query 数式項目の更新
linktitle: Power Query 数式項目の更新
second_title: Aspose.Cells for .NET API リファレンス
description: Aspose.Cells for .NET を使用して、Excel の Power Query 数式項目を簡単に更新できます。データ操作プロセスを効率化するためのステップ バイ ステップ ガイドです。
weight: 160
url: /ja/net/excel-workbook/update-power-query-formula-item/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Power Query 数式項目の更新

## 導入

Excel を使用したことがある方なら、特に Power Queries を使い始めると、その威力に驚くことでしょう。Power Queries は、データを簡単に変換、クリーンアップ、分析できる秘密のツールです。Excel で Power Query の数式を操作する便利な方法の 1 つは、Aspose.Cells for .NET を使用することです。今日は、Power Query の数式項目を更新する手順を順を追って説明します。では、コーディングの知識を身につけて、始めましょう。

## 前提条件

コードに進む前に、設定しておきたいことがいくつかあります。

1. Visual Studio: .NET コードを記述して実行するには、統合開発環境 (IDE) が必要です。Visual Studio が最適です。
2.  Aspose.Cellsライブラリ: プロジェクト内でAspose.Cellsライブラリが利用可能であることを確認してください。[サイト](https://releases.aspose.com/cells/net/).
3. C# の基礎知識: これを一緒に進めていく中で、C# の基礎知識をある程度持っていると、特にさまざまなクラスやメソッドを操作するときに役立ちます。
4. サンプル Excel ファイル: コード スニペットに記載されている Excel ファイルが必要です。次のものを用意してください。
   - `SamplePowerQueryFormula.xlsx`
   - `SamplePowerQueryFormulaSource.xlsx`

5. .NET Framework: プロジェクトが互換性のあるバージョンの .NET Framework をターゲットにしていることを確認します。

キットの準備ができたので、楽しい部分、つまりコードの作成に進むことができます。

## パッケージのインポート

まず最初に、必要な名前空間をインポートする必要があります。手順は次のとおりです。

```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```

これらの名前空間を追加することで、Aspose.Cells ライブラリのクラスとメソッドを使用するつもりであることをコンパイラに知らせます。この手順は、後続のコードの基礎となるため、非常に重要です。

提供されたコード スニペットを分解してみましょう。このチュートリアルでは、各部分を順に説明して、何が起こっているのか理解できるようにします。

## ステップ1: 作業ディレクトリを設定する

この手順では、ソース ファイルと出力ファイルの場所を定義します。これにより、Aspose が Excel ファイルの検索場所を認識できるようになります。

```csharp
//作業ディレクトリ
string SourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

## ステップ2: ワークブックを読み込む

ここで、Power Query が存在する Excel ファイルを読み込みます。

```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
の`Workbook`クラスは Excel ファイルへのエントリ ポイントです。ソース ファイルのパスを渡すことで、それを操作できるインスタンスを作成します。本を開くようなものだと想像してください。つまり、その内容を読む (または編集する) 準備をするのです。

## ステップ3: データマッシュアップにアクセスする

次に、ワークブックのデータ マッシュアップに保存されている Power Query 数式にアクセスします。

```csharp
DataMashup mashupData = workbook.DataMashup;
```
の`DataMashup`クラスには、ワークブックに関連付けられたすべての Power Query 数式が含まれています。修理のために工具箱を開けるときのように、ここで大変な作業を行います。

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

- それぞれをループします`PowerQueryFormula`で`mashupData`.
- そのループの中で、私たちはそれぞれに深く入り込みます`PowerQueryFormulaItem`.
- アイテムの名前が「ソース」と一致するかどうかを確認します。一致する場合は、その値を更新して新しいソース ファイルにリンクします。

これは、マニュアルで適切なページを見つけて、必要な更新を行うのと似ており、単純かつ細心の注意を要するプロセスです。

## ステップ5: 更新されたワークブックを保存する

更新を行ったら、変更を保存します。

```csharp
//出力ワークブックを保存します。
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
の`Save`メソッドは、更新されたワークブックを指定された出力ディレクトリに書き込みます。これは、編集内容をマニュアルの新しいバージョンに封印し、他の人が使用できるように準備するようなものです。

## 結論

おめでとうございます! Aspose.Cells for .NET を使用して Power Query 数式項目を正常に更新しました。この方法を使用すると、Excel ファイル内の Power Query 数式の変更を自動化できるため、貴重な時間と労力を節約できます。

## よくある質問

### Aspose.Cells とは何ですか?
Aspose.Cells は、Microsoft Excel をインストールしなくても .NET アプリケーションで Excel ファイルを操作できる強力なライブラリです。

### Aspose.Cells を実行するには Microsoft Excel が必要ですか?
いいえ、Aspose.Cells を使用すると、サーバーまたは開発マシンに Excel がなくても、プログラムで Excel ファイルを作成および編集できます。

### Aspose.Cells を使用して操作できる Excel ファイルの種類は何ですか?
Aspose.Cells を使用すると、.xlsx、.xls、.xlsm、およびその他のいくつかの Excel 形式を操作できます。

### Aspose.Cells の試用版はありますか?
はい、無料試用版をこちらからダウンロードできます。[Aspose Cells リリース ページ](https://releases.aspose.com/).

### Aspose.Cells のサポートを受けるにはどうすればよいですか?
サポートは以下からアクセスできます。[Aspose フォーラム](https://forum.aspose.com/c/cells/9)では、コミュニティや Aspose チームから質問したり回答を見つけることができます。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
