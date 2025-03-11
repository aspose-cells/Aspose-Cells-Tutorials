---
title: .NET でプログラム的にページ フィールドの書式を設定する
linktitle: .NET でプログラム的にページ フィールドの書式を設定する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して、ピボットテーブルのページ フィールド形式をプログラムで設定する方法を学びます。シームレスなデータ管理のために、ステップバイステップのチュートリアルに従ってください。
weight: 21
url: /ja/net/creating-and-configuring-pivot-tables/setting-page-field-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET でプログラム的にページ フィールドの書式を設定する

## 導入
コードを使用して Excel ファイルを作成および操作すると、特に大規模なデータセットを分析する必要がある場合に、非常に役立ちます。 優れたツールの 1 つが Aspose.Cells for .NET です。これを使用すると、プログラムで Excel ファイルを操作し、複雑なレポート構造を作成できます。 このチュートリアルでは、この強力なライブラリを使用して、ピボットテーブル内でページ フィールド形式を設定する方法を詳しく説明します。 経験豊富な開発者でも初心者でも、このガイドを読み終える頃には、.NET でピボットテーブルとそのさまざまな設定を操作する方法をしっかりと理解できるようになります。
## 前提条件
コーディングに取り掛かる前に、すべてが正しく設定されていることを確認しましょう。次のものが必要です。
- Visual Studio: .NET コードを記述して実行できる作業環境。
-  Aspose.Cells:ライブラリをダウンロードできます[ここ](https://releases.aspose.com/cells/net/).
- C# の基礎知識: C# プログラミングに精通していると、コード スニペットをよりよく理解できるようになります。
-  Excelファイル: Excelファイルを用意してください（例：`Book1.xls`) には、ピボットテーブルの作成に適したデータが含まれています。 
まだお持ちでない場合は、Aspose.Cellsの無料トライアルをお試しください。[ここ](https://releases.aspose.com/).
## パッケージのインポート
まず、プロジェクトに適切なパッケージをインポートする必要があります。まず、C# プロジェクトに Aspose.Cells ライブラリへの参照を追加します。手順は次のとおりです。
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
これにより、Aspose.Cells を使用して Excel ファイルを操作するために必要なすべてのクラスとメソッドが取り込まれます。
## ステップ1: ワークスペースを設定する
まず、Excel ファイルを保存する作業ディレクトリを定義します。たとえば、次のように変数を宣言できます。
```csharp
string dataDir = "Your Document Directory";
```
## ワークブックの読み込み
次に、Excel テンプレートを読み込む必要があります。これは、操作のコンテキストを確立するため、重要なステップです。
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
この行は、指定されたディレクトリから既存のワークブックを読み込みます。
## ステップ2: ワークシートにアクセスする
ワークブックが読み込まれたら、ピボットテーブルまたは分析するデータを含むワークシートにアクセスします。その方法は次のとおりです。
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
これにより、読み込まれたワークブックの最初のワークシートが取得されます。複数のシートで作業している場合は、インデックスを簡単に変更できます。
## ステップ3: ピボットテーブルにアクセスする
続けて、選択したワークシートのピボットテーブルにアクセスしてみましょう。単一のピボットテーブルを使用している場合は、そのインデックスを次のように設定できます。`0`:
```csharp
int pivotindex = 0;
//ピボットテーブルへのアクセス
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
このコード スニペットは、ワークシート内の最初のピボットテーブルを選択します。 
## ステップ4: ピボットテーブルの構成
次は面白い部分です。ピボットテーブルを設定して、行の合計を表示してみましょう。
```csharp
pivotTable.RowGrand = true;
```
この行により、レポートにはデータ分析に役立つ概要となる総計が表示されます。
## ステップ5: 行フィールドにアクセスして構成する
次に、ピボットテーブルの行フィールドにアクセスする必要があります。
```csharp
Aspose.Cells.Pivot.PivotFieldCollection pivotFields = pivotTable.RowFields;
```
このコレクションを使用すると、必要に応じてフィールドを操作できます。
## 最初の行フィールドを構成する
特定の小計タイプを設定したいですか? コレクションの最初のフィールドにアクセスして設定してみましょう。
```csharp
Aspose.Cells.Pivot.PivotField pivotField = pivotFields[0];
//小計の設定。
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Sum, true);
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Count, true);
```
有効にすることで`Sum`そして`Count`小計を使用すると、レポート内のデータをすばやく要約できます。
## ステップ6: 自動並べ替えオプションの設定
次に、スマートな並べ替え機能を活用してみましょう。これにより、ピボットテーブルはデータを意味のある順序で並べます。
```csharp
//自動並べ替えオプションを設定します。
pivotField.IsAutoSort = true;
pivotField.IsAscendSort = true;
pivotField.AutoSortField = -5; //定義済みの並べ替えフィールドを使用します。
```
このコード スニペットは自動ソートを有効にし、昇順を指定します。 
## ステップ 7: 自動表示オプションの設定
データをさらにフィルタリングしますか? 自動表示オプションは、定義された条件下で特定のデータ ポイントを表示するのに便利です。
```csharp
//自動表示オプションを設定します。
pivotField.IsAutoShow = true;
pivotField.IsAscendShow = false;
pivotField.AutoShowField = 0; //自動表示するフィールドを指定します。
```
これにより、ピボットテーブルには関連するデータのみが表示されるようになり、明瞭性と焦点が向上します。
## ステップ8: 作業内容を保存する
これらすべての設定を行った後、作業内容を失いたくないでしょう。変更したワークブックを次のように保存します。
```csharp
workbook.Save(dataDir + "output.xls");
```
これで、新しく作成された Excel ファイルがドキュメント ディレクトリに見つかります。
## 結論
これで完了です。Aspose.Cells for .NET を使用して、ピボットテーブルでページ フィールドの書式をプログラムで設定するための包括的かつ実用的なアプローチについて説明しました。提供されている簡単な手順に従うことで、レポートのニーズに合わせて Excel データを自信を持って変更できるようになります。C# のパワーと Aspose.Cells を組み合わせると、驚くべき成果が得られます。
## よくある質問
### Aspose.Cells とは何ですか?
Aspose.Cells は、開発者がプログラムによって Excel ファイルを作成、操作、変換できるようにする .NET ライブラリです。
### Aspose.Cells をインストールするにはどうすればよいですか?
から直接ダウンロードできます。[Aspose ウェブサイト](https://releases.aspose.com/cells/net/).
### Excel をインストールせずに Aspose.Cells を使用できますか?
はい、Aspose.Cells は Microsoft Excel をインストールする必要のないスタンドアロン ライブラリです。
### 詳細なサポートはどこで見つかりますか?
詳細なサポートとフォーラムにアクセスするには、[Aspose サポート](https://forum.aspose.com/c/cells/9).
### 一時ライセンスを取得するにはどうすればいいですか?
一時ライセンスは以下から取得できます。[ここ](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
