---
"description": "Aspose.Cellsを使用して、.NETでピボットテーブルをプログラム的に並べ替える方法を学びましょう。セットアップ、構成、並べ替え、そして結果をExcelファイルとPDFファイルとして保存する方法をステップバイステップで解説します。"
"linktitle": ".NET でプログラム的にピボットテーブルをカスタム並べ替えする"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": ".NET でプログラム的にピボットテーブルをカスタム並べ替えする"
"url": "/ja/net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/"
"weight": 29
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# .NET でプログラム的にピボットテーブルをカスタム並べ替えする

## 導入
.NET環境でExcelを操作する場合、数あるライブラリの中でもひときわ目立つ存在がAspose.Cellsです。スプレッドシートをプログラムで操作できるツールがあれば、本当に便利ですよね？まさにAspose.Cellsがそれを実現します！本日のチュートリアルでは、ピボットテーブルの世界を深く掘り下げ、この多機能なライブラリを使ってプログラムでカスタムソートを実装する方法をご紹介します。
## 前提条件
袖をまくってコードに取り掛かる前に、いくつかの準備が整っていることを確認してください。
1. Visual Studio: Visual Studio の動作するバージョンが必要です。Visual Studio は、あらゆる魔法が起こる遊び場です。
2. .NET Framework：.NETプログラミングの知識は必須です。.NET Coreや.NET Frameworkの愛用者であれば、このコースで十分です。
3. Aspose.Cellsライブラリ: Aspose.Cellsライブラリをインストールする必要があります。 [ダウンロードリンク](https://releases.aspose.com/cells/net/) プロジェクトに追加します。
4. ピボット テーブルの基本的な理解: 専門家である必要はありませんが、このチュートリアルを進める上で、ピボット テーブルの仕組みについて少し知っておくと役立ちます。
5. サンプルExcelファイル: サンプルExcelファイルの名前は `SamplePivotSort.xlsx` テスト用に作業ディレクトリに準備します。
## パッケージのインポート
前提条件をすべて整えたら、まず必要なパッケージをインポートします。そのためには、コードの先頭に以下の行を追加します。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
このパッケージは、Aspose.Cells を使用して Excel ファイルを操作するために必要なすべての機能を提供します。

さあ、楽しい部分に入りましょう！ピボットテーブルを作成し、カスタム並べ替えを適用するプロセスを、わかりやすい手順に分解して説明します。
## ステップ1: ワークブックを設定する
まず、ワークブックを設定する必要があります。手順は以下のとおりです。
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
このステップでは、新しい `Workbook` Excelファイルへのパスを持つインスタンスを作成します。これがピボットテーブルを作成するキャンバスとして機能します。
## ステップ2: ワークシートにアクセスする
次に、ピボット テーブルを追加するワークシートにアクセスする必要があります。
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
ここでは、ワークブックの最初のワークシートを取得し、 `PivotTableCollection`このコレクションを使用すると、このワークシート上のすべてのピボット テーブルを管理できます。
## ステップ3: 最初のピボットテーブルを作成する
次はピボット テーブルを作成します。
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
ワークシートに新しいピボットテーブルを追加し、データ範囲と位置を指定します。「E3」はピボットテーブルの開始位置を示します。次に、この新しいピボットテーブルをインデックスで参照します。
## ステップ4: ピボットテーブルの設定を構成する
ピボットテーブルを設定しましょう！つまり、総計やフィールドの配置といった側面をコントロールするということです。
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
行と列の合計が表示されないようにすることで、データの見やすさが向上します。次に、行エリアに最初のフィールドを追加し、自動並べ替えと昇順並べ替えを有効にします。
## ステップ5: 列とデータフィールドを追加する
行が設定されたら、列とデータ フィールドを追加しましょう。
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
2つ目のフィールドを列として追加し、日付形式に設定します。ここでも、自動並べ替えと昇順を有効にして、データを整理します。最後に、3つ目のフィールドをデータエリアに追加します。
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## ステップ6: ピボットテーブルを更新して計算する
必要なフィールドをすべて追加したら、ピボット テーブルが最新の状態であることを確認しましょう。
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
これらのメソッドは、データを更新して再計算し、すべてが最新の状態になり、ピボット テーブルに正しく表示されるようにします。
## ステップ7: 行フィールド値に基づくカスタムソート
「SeaFood」などの特定の値に基づいてピボット テーブルを並べ替えて、少し趣向を加えてみましょう。
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
同じ手順を繰り返し、別のピボットテーブルを作成し、最初のものと同じように設定します。さらにカスタマイズできます。
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## ステップ 8: 追加の並べ替えのカスタマイズ特定の日付に基づいて別の並べ替え方法を試してみましょう。
```csharp
// 日付で並べ替えるためのピボットテーブルを追加する
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
// 前の手順と同様に行と列の設定を繰り返します
```
同じプロセスを繰り返して、ニーズに合わせて並べ替え基準を調整した 3 番目のピボット テーブルを作成します。
## ステップ 9: ワークブックを保存するこれまでの努力をすべて保存しましょう。
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
ここでは、ワークブックをExcelファイルとPDFとして保存します。 `PdfSaveOptions` より適切なフォーマットが可能になり、変換時に各シートが別々のページに表示されるようになります。
## ステップ 10: 終了 すべてが順調であることをユーザーに知らせて、すべてを終了します。
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## 結論
ここまでで、Aspose.Cells のパワーを活用して .NET アプリケーションでピボットテーブルを作成およびカスタマイズする方法を学習しました。初期設定から並べ替えのカスタマイズまで、各ステップを組み合わせることでシームレスなエクスペリエンスが実現します。年間売上データの提示や在庫統計の追跡など、これらのスキルはきっと役立ちます。
## よくある質問
### ピボットテーブルとは何ですか?
ピボット テーブルは、データを要約および分析し、洞察を簡単に抽出するための柔軟な方法を提供する Excel のデータ処理ツールです。
### Aspose.Cells をインストールするにはどうすればよいですか?
Visual StudioのNuGet経由でインストールするか、直接ダウンロードすることができます。 [ダウンロードリンク](https://releases。aspose.com/cells/net/).
### Aspose.Cells の試用版はありますか?
はい！無料でお試しいただけます。 [無料トライアルリンク](https://releases。aspose.com/).
### ピボットテーブル内の複数のフィールドを並べ替えることはできますか?
もちろんです！要件に応じて複数のフィールドを追加したり並べ替えたりできます。
### Aspose.Cells のサポートはどこで見つかりますか?
コミュニティは非常に活発で、フォーラムで質問することができます。 [ここ](https://forum。aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}