---
title: .NET でプログラム的に新しいピボット テーブルを作成する
linktitle: .NET でプログラム的に新しいピボット テーブルを作成する
second_title: Aspose.Cells .NET Excel 処理 API
description: ステップバイステップ ガイドを使用して、Aspose.Cells を使用して .NET でプログラム的にピボット テーブルを作成する方法を学習します。データを効率的に分析します。
weight: 13
url: /ja/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET でプログラム的に新しいピボット テーブルを作成する

## 導入
ピボット テーブルの作成は、特にプログラムで作成する場合、困難な作業のように思えるかもしれません。しかし、心配はいりません。Aspose.Cells for .NET を使用すると、ピボット テーブルの作成は簡単なだけでなく、データ分析に非常に役立ちます。このチュートリアルでは、.NET アプリケーションで新しいピボット テーブルを作成する方法を段階的に説明します。売上、スポーツ、その他のビジネス メトリックのデータを追加する場合でも、このガイドは、すぐにピボット テーブルを稼働させるのに役立ちます。

## 前提条件
始める前に、すべての準備が整っていることを確認しましょう。必要な手順は次のとおりです。

1. .NET Framework をインストールします。マシンに .NET Framework がインストールされていることを確認します。Aspose.Cells はさまざまなバージョンをサポートしていますが、最新のバージョンを使用することをお勧めします。
2.  Aspose.Cellsライブラリ: Aspose.Cellsライブラリが必要です。[ここからダウンロード](https://releases.aspose.com/cells/net/)または[一時ライセンス](https://purchase.aspose.com/temporary-license/)評価のため。
3. IDE のセットアップ: 新しいプロジェクトを開始できる Visual Studio などの C# 互換 IDE を準備します。
4. C# の基礎知識: C# プログラミングに精通していれば、あまり行き詰まることなく理解できるようになります。

準備はできましたか? 素晴らしい! 必要なパッケージのインポートに進みましょう。

## パッケージのインポート
まず最初に、必要な名前空間を C# プロジェクトにインポートする必要があります。C# ファイルを開き、次の using ディレクティブを追加します。

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

これらの名前空間により、このチュートリアル全体で使用するワークブック、ワークシート、ピボット テーブルの機能にアクセスできるようになります。

## ステップ 1: ワークブック オブジェクトを作成する
ワークブックの作成は旅の始まりです。まずは新しいワークブックをインスタンス化し、最初のワークシートにアクセスしてみましょう。

```csharp
//ドキュメント ディレクトリへのパス。
string dataDir = "Your Document Directory";
//ワークブックオブジェクトのインスタンス化
Workbook workbook = new Workbook();

//新しく追加されたワークシートの参照を取得する
Worksheet sheet = workbook.Worksheets[0];
```

このステップでは、`Workbook`Excel ファイルを表すインスタンスを作成し、ピボット テーブルのプレイグラウンドとなる最初のワークシートを取得します。

## ステップ2: セルにデータを挿入する
次に、ワークシートにサンプル データを入力してみましょう。ピボット テーブルに集計用のデータを追加するために、さまざまなスポーツ、四半期、売上高の行を入力します。

```csharp
Cells cells = sheet.Cells;

//セルに値を設定する
Cell cell = cells["A1"];
cell.PutValue("Sport");
cell = cells["B1"];
cell.PutValue("Quarter");
cell = cells["C1"];
cell.PutValue("Sales");

//データの入力cell = cells["A2"];
cell.PutValue("Golf");
// ... その他のデータエントリ
```

ここでは、列ヘッダーを定義し、各ヘッダーの下に値を挿入します。このデータはピボット テーブルのソースとして機能するため、整理されていることを確認してください。このブロックを実行すると、包括的なデータセットが作成されます。

## ステップ3: ピボットテーブルの追加
データの準備ができたら、ピボット テーブルを作成します。ワークシートのピボット テーブル コレクションを使用して、新しいピボット テーブルを追加します。

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

//ワークシートにピボットテーブルを追加する
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

このスニペットでは、データ範囲 (この場合はセル A1 から C8) を参照するピボット テーブルをワークシートに追加します。ピボット テーブルをセル E3 から配置し、「PivotTable2」という名前を付けます。とても簡単ですよね。

## ステップ4: ピボットテーブルをカスタマイズする
ピボット テーブルが完成したので、意味のある要約が表示されるようにカスタマイズしてみましょう。ピボット テーブルの行、列、データ領域に表示される内容を制御できます。

```csharp
//新しく追加されたピボットテーブルのインスタンスにアクセスする
Aspose.Cells.Pivot.PivotTable pivotTable = pivotTables[index];

//行の合計を非表示にします。
pivotTable.RowGrand = false;

//最初のフィールドを行領域にドラッグします。
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Row, 0);

// 2 番目のフィールドを列領域にドラッグします。
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Column, 1);

// 3 番目のフィールドをデータ領域にドラッグします。
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Data, 2);
```

この手順では、ピボット テーブルで行の合計を非表示にするように指示し、行、列、およびデータ領域にどのフィールドを配置するかを指定します。スポーツ名が行に、四半期が列に、売上高が要約として表示されます。

## ステップ5: ワークブックを保存する
最後に、新しく作成したワークブックを保存して、作業の成果を確認します。

```csharp
// Excelファイルの保存
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

適切なパスを指定するだけで、ピボット テーブルの出力が Excel ファイルに保存され、開いて確認できるようになります。

## 結論
Aspose.Cells for .NET を使用してプログラムでピボット テーブルを作成すると、特に大規模なデータセットを扱う場合に時間を大幅に節約できます。プロジェクトの設定、必要なパッケージのインポート、データの入力、カスタマイズ可能なピボット テーブルを最初から作成する方法を学びました。次に数字に困ったときは、このチュートリアルを思い出して、Aspose.Cells に面倒な作業を任せてください。

## よくある質問
### Aspose.Cells とは何ですか?
Aspose.Cells は、Excel スプレッドシートをプログラムで作成および管理するための強力な .NET ライブラリです。

### Aspose.Cells の無料トライアルはありますか?
はい、無料トライアルをご利用いただけます[ここ](https://releases.aspose.com/).

### ピボットテーブルの外観をカスタマイズできますか?
もちろんです! ピボット テーブルの書式設定、レイアウト、スタイルも、必要に応じてカスタマイズできます。

### Aspose.Cells のその他の例やドキュメントはどこで見つかりますか?
確認するには[ドキュメント](https://reference.aspose.com/cells/net/)包括的なガイドと例については、こちらをご覧ください。

### Aspose.Cells のサポートを受けるにはどうすればよいですか?
サポートを受けるには[Aspose フォーラム](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
