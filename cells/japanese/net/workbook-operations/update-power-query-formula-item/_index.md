---
title: ワークブック内の Power Query 数式項目を更新する
linktitle: ワークブック内の Power Query 数式項目を更新する
second_title: Aspose.Cells .NET Excel 処理 API
description: この包括的なステップバイステップ ガイドでは、Aspose.Cells for .NET を使用して Excel の Power Query 数式を更新する方法を学習します。
weight: 27
url: /ja/net/workbook-operations/update-power-query-formula-item/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ワークブック内の Power Query 数式項目を更新する

## 導入
Excel で Power Query を使用してデータを効率的に管理する方法を理解することは、データ アナリストや Excel 愛好者にとって非常に重要です。Power Query ワークブックの数式項目を更新する必要がある場合は、このガイドが役に立ちます。このガイドは、Aspose.Cells for .NET を使用して Excel ワークブックの Power Query 数式をシームレスに更新する方法を学習できるように作られています。いくつかの簡単な手順で、データを操作および合理化して、ワークブックを動的かつ一元管理された状態に保つことができます。
## 前提条件
サンプル コードと手順に進む前に、必要なものを確認しましょう。
1. C# と .NET の基本的な理解: コードを書くことになるので、C# のプログラミング概念を理解していると役立ちます。
2.  Aspose.Cells for .NETをインストールします。Aspose.Cellsライブラリを.NETプロジェクトに統合する必要があります。ダウンロードできます。[ここ](https://releases.aspose.com/cells/net/).
3. 変更可能なExcelファイル: 更新したいPower Queryを含むExcelファイルがあることを確認してください。次のようなサンプルワークブックが必要です。`SamplePowerQueryFormula.xlsx`ご自由にお使いください。
## パッケージのインポート
開始するには、C# ファイルに次の名前空間が含まれていることを確認します。
```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```
これにより、特にワークブックや Power Query データの操作に、Aspose.Cells ライブラリによって提供される機能にアクセスできるようになります。
## ステップ1: 作業ディレクトリを設定する
まず最初に、ソース ファイルと出力ファイルが配置されている場所を定義する必要があります。 
```csharp
string SourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
```
このステップでは、ディレクトリパスを指定します。`"Your Document Directory"` Excel ファイルが保存されている実際のパスを入力します。これにより、プログラムがソース ファイルを検索する場所と更新されたファイルを保存する場所が指示されます。
## ステップ2: ワークブックを読み込む
作業ディレクトリの設定が完了したら、次のステップは Excel ファイルをプログラムに読み込むことです。
```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
ここでは、`Workbook`指定されたExcelファイルを読み込むオブジェクト。`Workbook`クラスは Aspose.Cells ライブラリの一部であり、Excel ファイルで実行するすべての操作に不可欠です。
## ステップ3: Power Queryデータにアクセスする
ワークブックが読み込まれたら、その中に保存されている Power Query 数式にアクセスします。
```csharp
DataMashup mashupData = workbook.DataMashup;
```
この行では、`DataMashup`プロパティは、ブック内の Power Query データ構造にアクセスするのに役立ちます。このプロパティを使用すると、Excel ファイルに含まれる Power Query データのさまざまな側面を操作できるようになります。
## ステップ4: Power Queryの数式をループする
Power Query データにアクセスできたら、次のステップは存在する各数式を反復処理することです。
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
ここで魔法が起こります。各ループを`PowerQueryFormula`そして、それぞれを通して`PowerQueryFormulaItem` 。`if`ステートメントは、「ソース」という名前の数式項目を検索し、その値を Power Query が参照するソース ファイルのパスに更新します。これにより、Power Query がデータを取得するファイルを動的に変更できます。
## ステップ5: 更新されたワークブックを保存する
必要な数式項目を更新したら、最後の手順としてワークブックを保存します。
```csharp
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
```
この行は、変更されたワークブックを新しいファイルに保存し、元のワークブックを保持しながら更新されたバージョンで作業できるようにします。
## ステップ6: 確認メッセージ
最後に、コードが適切に実行されたかどうかを確認することをお勧めします。
```csharp
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
この簡単なメッセージにより、コンソールで操作が成功したことが確認され、プロセスが安心して終了します。
## 結論
これで完了です。Aspose.Cells for .NET を使用して Excel の Power Query 数式項目を更新するのは、簡単な手順で実行できます。このガイドに従うことで、Excel データ接続を効率的に管理し、ワークブックをスムーズに実行できます。熟練したプロでも、データ操作を始めたばかりでも、Aspose.Cells は Excel ワークフローを自動化および強化する強力な方法を提供します。 
## よくある質問
### Aspose.Cells はどのバージョンの .NET でも使用できますか?
Aspose.Cells は、.NET Framework や .NET Core を含む複数のバージョンの .NET と互換性があります。
### Aspose.Cells は無料で使用できますか?
 Aspose.Cellsは無料トライアルを提供していますが、継続して使用するにはライセンスが必要です。一時ライセンスを取得できます。[ここ](https://purchase.aspose.com/temporary-license/).
### 既存の Excel ファイルに Power Query が含まれていない場合はどうなりますか?
説明したプロセスは Power Query アイテムの更新に重点を置いているため、ファイルに Power Query アイテムがない場合は、まず Power Query を組み込む必要があります。
### Aspose.Cells の詳細情報はどこで入手できますか?
包括的なガイダンスと例については、ドキュメントを参照してください。[ドキュメント](https://reference.aspose.com/cells/net/).
### Aspose.Cells のバグや問題を報告するにはどうすればよいですか?
発生した問題に関してサポートが必要な場合は、サポートされているフォーラムにお問い合わせください。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
