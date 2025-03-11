---
title: .NET でプログラム的にピボット テーブルをカスタム並べ替えする
linktitle: .NET でプログラム的にピボット テーブルをカスタム並べ替えする
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells を使用して .NET でピボット テーブルをプログラム的に並べ替える方法を学習します。セットアップ、構成、並べ替え、結果を Excel および PDF ファイルとして保存する手順を説明したガイドです。
weight: 29
url: /ja/net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET でプログラム的にピボット テーブルをカスタム並べ替えする

## 導入
.NET 環境で Excel を操作する場合、1 つのライブラリが他のライブラリよりも際立っています。Aspose.Cells です。ツールを使ってプログラムでスプレッドシートを操作できるとしたら、とてもうれしいと思いませんか? Aspose.Cells はまさにそれを実現します。今日のチュートリアルでは、ピボット テーブルの世界を深く掘り下げ、この多目的なライブラリを使用してプログラムでカスタム並べ替えを実装する方法を紹介します。
## 前提条件
袖をまくってコードに取り掛かる前に、いくつかの準備が整っていることを確認してください。
1. Visual Studio: Visual Studio の動作するバージョンが必要です。これは、すべての魔法が起こる遊び場です。
2. .NET Framework: .NET プログラミングに精通していることが必須です。.NET Core または .NET Framework のどちらに詳しい方でも、問題ありません。
3.  Aspose.Cellsライブラリ: Aspose.Cellsライブラリをインストールする必要があります。[ダウンロードリンク](https://releases.aspose.com/cells/net/)プロジェクトに追加します。
4. ピボット テーブルの基本的な理解: 専門家である必要はありませんが、このチュートリアルを進める上で、ピボット テーブルの仕組みについて少し知識があると役立ちます。
5. サンプルExcelファイル: サンプルExcelファイルの名前は`SamplePivotSort.xlsx`テスト用に作業ディレクトリに準備します。
## パッケージのインポート
すべての前提条件を整理したら、最初のステップは必要なパッケージをインポートすることです。これを行うには、コードの先頭に次の行を含めます。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
このパッケージは、Aspose.Cells を使用して Excel ファイルを操作するために必要なすべての機能を提供します。

さて、楽しい部分に入りましょう! ピボット テーブルを作成し、カスタム並べ替えを適用するプロセスを、管理しやすい手順に分解します。
## ステップ1: ワークブックを設定する
まず、ワークブックを設定する必要があります。手順は次のとおりです。
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
このステップでは、新しい`Workbook`Excel ファイルへのパスを持つインスタンス。これは、ピボット テーブルが実行されるキャンバスとして機能します。
## ステップ2: ワークシートにアクセスする
次に、ピボット テーブルを追加するワークシートにアクセスする必要があります。
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
ここでは、ワークブックの最初のワークシートを取り出し、`PivotTableCollection`このコレクションを使用すると、このワークシート上のすべてのピボット テーブルを管理できます。
## ステップ3: 最初のピボットテーブルを作成する
次に、ピボット テーブルを作成します。
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
データ範囲とその場所を指定して、ワークシートに新しいピボット テーブルを追加します。「E3」は、ピボット テーブルを開始する場所を示します。次に、インデックスを使用してこの新しいピボット テーブルを参照します。
## ステップ4: ピボットテーブルの設定を構成する
ピボット テーブルを設定しましょう。これは、総計やフィールドの配置などの側面を制御することを意味します。
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
行と列の合計が表示されないようにすることで、データをよりクリーンにすることができます。次に、行領域に最初のフィールドを追加して、自動並べ替えと昇順並べ替えを有効にします。
## ステップ5: 列とデータフィールドを追加する
行が設定されたら、列とデータ フィールドを追加しましょう。
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
2 番目のフィールドを列として追加し、日付としてフォーマットします。ここでも、整理された状態を保つために自動並べ替えと昇順を有効にします。最後に、データ領域に 3 番目のフィールドを追加する必要があります。
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## ステップ6: ピボットテーブルを更新して計算する
必要なフィールドをすべて追加したら、ピボット テーブルが最新の状態であることを確認しましょう。
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
これらのメソッドはデータを更新して再計算し、すべてが最新であり、ピボット テーブルに正しく表示されるようにします。
## ステップ 7: 行フィールド値に基づくカスタム並べ替え
「SeaFood」などの特定の値に基づいてピボット テーブルを並べ替えて、少し趣向を加えてみましょう。
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
別のピボット テーブルを作成し、最初のものと同様に設定することで、プロセスを繰り返します。これで、さらにカスタマイズできます。
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## ステップ 8: 追加の並べ替えのカスタマイズ特定の日付に基づいて別の並べ替え方法を試してみましょう。
```csharp
//日付で並べ替えるための別のピボットテーブルを追加する
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
//前の手順と同様の行と列の設定を繰り返します
```
同じプロセスを繰り返して、ニーズに合わせて並べ替え基準を調整した 3 番目のピボット テーブルを作成します。
## ステップ 9: ワークブックを保存するこれまでの努力をすべて保存しましょう。
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
ここでは、ワークブックをExcelファイルとPDFとして保存します。`PdfSaveOptions`より適切な書式設定が可能になり、変換時に各シートが別々のページに表示されるようになります。
## ステップ 10: 終了 すべてが順調であることをユーザーに知らせて、すべてを終了します。
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## 結論
ここまでで、Aspose.Cells のパワーを活用して .NET アプリケーションでピボット テーブルを作成し、カスタマイズする方法を学びました。初期設定からカスタム並べ替えまで、各ステップを組み合わせることでシームレスなエクスペリエンスが実現します。年間売上データを提示する必要がある場合でも、在庫統計を追跡する必要がある場合でも、これらのスキルは大いに役立ちます。
## よくある質問
### ピボットテーブルとは何ですか?
ピボット テーブルは、データを要約および分析し、洞察を簡単に抽出するための柔軟な方法を提供する Excel のデータ処理ツールです。
### Aspose.Cells をインストールするにはどうすればよいですか?
 Visual StudioのNuGet経由でインストールするか、直接ダウンロードすることができます。[ダウンロードリンク](https://releases.aspose.com/cells/net/).
### Aspose.Cells の試用版はありますか?
はい！無料でお試しいただけます。[無料トライアルリンク](https://releases.aspose.com/).
### ピボットテーブルで複数のフィールドを並べ替えることはできますか?
もちろんです! 要件に応じて複数のフィールドを追加したり並べ替えたりすることができます。
### Aspose.Cells のサポートはどこで見つかりますか?
コミュニティは非常に活発で、フォーラムで質問することができます。[ここ](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
