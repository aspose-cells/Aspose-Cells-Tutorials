---
title: .NET でカスタムの並べ替えと非表示を設定してピボット テーブルを保存する
linktitle: .NET でカスタムの並べ替えと非表示を設定してピボット テーブルを保存する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して、カスタムの並べ替えと行の非表示を設定してピボット テーブルを保存する方法を学習します。実用的な例を含むステップ バイ ステップ ガイドです。
weight: 26
url: /ja/net/creating-and-configuring-pivot-tables/saving-with-custom-sort-and-hide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET でカスタムの並べ替えと非表示を設定してピボット テーブルを保存する

## 導入
データ分析の世界では、ピボット テーブルは、データを要約、分析し、わかりやすい形式で提示するための最も強力なツールの 1 つです。.NET で作業していて、ピボット テーブルを操作する簡単な方法 (具体的には、カスタムの並べ替えや特定の行の非表示を設定して保存する方法) を探している場合は、ここが最適な場所です。今日は、Aspose.Cells for .NET を使用してピボット テーブルを保存するテクニックを説明します。このガイドでは、前提条件から実践的な例まですべてを説明し、同様のタスクに自分で取り組む準備が整うようにします。では、早速始めましょう。
## 前提条件
コーディングの細部に進む前に、次の前提条件が満たされていることを確認してください。
1. Visual Studio: 理想的には、.NET プロジェクトを処理するための堅牢な IDE が必要です。Visual Studio は最適な選択肢です。
2.  Aspose.Cells for .NET: Excelファイルをプログラムで管理するには、Asposeのライブラリにアクセスする必要があります。[Aspose.Cells for .NET をここからダウンロード](https://releases.aspose.com/cells/net/).
3. C# の基礎知識: C# の基本的なプログラミング概念と構文を理解していると、プロセスがスムーズになります。
4. サンプルExcelファイル: サンプルファイルとして、`PivotTableHideAndSortSample.xlsx`このファイルが指定されたドキュメント ディレクトリにあることを確認してください。
開発環境をセットアップし、サンプル ファイルの準備ができたら、準備は完了です。
## パッケージのインポート
前提条件を確認したので、必要なパッケージをインポートしましょう。C# ファイルで、次のディレクティブを使用して Aspose.Cells を含めます。
```csharp
using System;
using Aspose.Cells.Pivot;
```
このディレクティブを使用すると、Aspose.Cells ライブラリによって提供されるクラスとメソッドにアクセスできます。プロジェクト参照に Aspose.Cells.dll を追加したことを確認してください。
## ステップ1: ワークブックを設定する
まず最初に、ワークブックを読み込む必要があります。次のコード スニペットでこれを実現します。
```csharp
//ソースファイルと出力ファイルのディレクトリ
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
//ワークブックを読み込む
Workbook workbook = new Workbook(sourceDir + "PivotTableHideAndSortSample.xlsx");
```
このステップでは、ソースファイルと出力ファイルを保存するディレクトリを定義します。`Workbook`コンストラクターは既存の Excel ファイルを読み込み、操作できるようにします。
## ステップ2: ワークシートとピボットテーブルにアクセスする
ここで、ワークブック内の特定のワークシートにアクセスし、操作するピボット テーブルを選択しましょう。
```csharp
//最初のワークシートにアクセスする
Worksheet worksheet = workbook.Worksheets[0];
//ワークシートの最初のピボットテーブルにアクセスする
var pivotTable = worksheet.PivotTables[0];
```
このスニペットでは、`Worksheets[0]` Excel文書の最初のシートを選択し、`PivotTables[0]`最初のピボット テーブルを取得します。これにより、変更したいピボット テーブルを正確にターゲットにすることができます。
## ステップ3: ピボットテーブルの行を並べ替える
次に、データを整理するためにカスタムソートを実装します。具体的には、スコアを降順でソートします。
```csharp
//最初の行のフィールドを降順で並べ替える
PivotField field = pivotTable.RowFields[0];
field.IsAutoSort = true;
field.IsAscendSort = false;  //降順の場合は false
field.AutoSortField = 0;     //最初の列に基づいて並べ替える
```
ここでは、`PivotField`並べ替えパラメータを設定します。これにより、ピボット テーブルは指定された行フィールドを最初の列に基づいて降順で並べ替えます。 
## ステップ4: データを更新して計算する
並べ替えを適用した後は、ピボット テーブルのデータを更新して、変更が反映されていることを確認することが重要です。
```csharp
//ピボットテーブルデータを更新して計算する
pivotTable.RefreshData();
pivotTable.CalculateData();
```
この手順では、ピボット テーブルを現在のデータと同期し、これまでに行った並べ替えやフィルタリングの変更を適用します。データの新しい構成を確認するには、「更新」を押すのと同じだと考えてください。
## ステップ5: 特定の行を非表示にする
ここで、特定のしきい値（たとえば 60 未満）を下回るスコアを含む行を非表示にしてみましょう。ここで、データをさらにフィルタリングできます。
```csharp
//スコアをチェックする開始行を指定します
int currentRow = 3;
int rowsUsed = pivotTable.DataBodyRange.EndRow;
//スコアが60未満の行を非表示にする
while (currentRow < rowsUsed)
{
    Cell cell = worksheet.Cells[currentRow, 1]; //スコアが最初の列にあると仮定
    double score = Convert.ToDouble(cell.Value);
    if (score < 60)
    {
        worksheet.Cells.HideRow(currentRow);  //スコアが60未満の場合は行を非表示にする
    }
    currentRow++;
}
```
このループでは、ピボット テーブルのデータ本体の範囲内の各行をチェックします。スコアが 60 未満の場合は、その行を非表示にします。これは、ワークスペースを整理するのと似ており、全体像を把握するのに役立たない雑然としたものを削除します。
## ステップ 6: ワークブックの最終更新と保存
最後に、ピボット テーブルをもう一度更新して行の非表示が有効になっていることを確認してから、ワークブックを新しいファイルに保存します。
```csharp
//最後にもう一度データを更新して計算する
pivotTable.RefreshData();
pivotTable.CalculateData();
//変更したワークブックを保存する
workbook.Save(outputDir + "PivotTableHideAndSort_out.xlsx");
```
この最終更新により、すべてが最新であることが保証され、ワークブックを保存することで、行ったすべての変更を反映した新しいファイルが作成されます。
## ステップ7: 成功を確認する
最後に、操作が問題なく完了したことを確認するために成功メッセージを出力します。
```csharp
Console.WriteLine("PivotTableSortAndHide executed successfully.");
```
この行は、成功の確認とコンソールでのフィードバックの提供という 2 つの目的を果たし、プロセスをよりインタラクティブでユーザーフレンドリーなものにします。
## 結論
これで完了です。Aspose.Cells for .NET を使用して、カスタムの並べ替え機能と非表示機能を備えたピボット テーブルを保存する方法を学習しました。ワークブックの読み込みからデータの並べ替え、不要な詳細の非表示まで、これらの手順は、ピボット テーブルをプログラムで管理するための構造化されたアプローチを提供します。販売データを分析する場合でも、チームのパフォーマンスを追跡する場合でも、単に情報を整理する場合でも、Aspose.Cells を使用してこれらのスキルを習得すると、貴重な時間を節約し、データ分析ワークフローを改善できます。
## よくある質問
### Aspose.Cells for .NET とは何ですか?
Aspose.Cells for .NET は、開発者が Microsoft Excel に依存せずに Excel スプレッドシートを作成、操作、変換できるようにする .NET ライブラリです。Excel ドキュメント内のタスクを自動化するのに最適です。
### Microsoft Office をインストールせずに Aspose.Cells を使用できますか?
もちろんです! Aspose.Cells はスタンドアロン ライブラリなので、Excel ファイルを操作するのにシステムに Microsoft Office をインストールする必要はありません。
### Aspose.Cells の一時ライセンスを取得するにはどうすればよいですか?
一時ライセンスは、[一時ライセンスページ](https://purchase.aspose.com/temporary-license/).
### Aspose.Cells の問題に関するサポートはどこで受けられますか?
ご質問やご不明な点がございましたら、[Aspose フォーラム](https://forum.aspose.com/c/cells/9)では、コミュニティと Aspose チームからのサポートを受けることができます。
### Aspose.Cells の無料トライアルはありますか?
はい！購入前にAspose.Cellsの無料試用版をダウンロードして機能をテストすることができます。[無料トライアルページ](https://releases.aspose.com/)始めましょう。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
