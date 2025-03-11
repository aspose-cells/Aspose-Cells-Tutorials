---
title: Excel でデータテーブル行を挿入するときに最初の行を下へシフトする
linktitle: Excel でデータテーブル行を挿入するときに最初の行を下へシフトする
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して、最初の行を下に移動せずに Excel に DataTable 行を挿入する方法を学びます。手間をかけずに自動化するためのステップバイステップ ガイドです。
weight: 11
url: /ja/net/excel-data-import-export/shift-first-row-down-when-inserting-cells-datatable-rows-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel でデータテーブル行を挿入するときに最初の行を下へシフトする

## 導入

Excel スプレッドシートに新しいデータを挿入するときに、手動で行を移動するのにうんざりしていませんか? いいえ、大丈夫です! この記事では、Aspose.Cells for .NET を使用してこのプロセスを自動化する方法について詳しく説明します。このチュートリアルの最後までに、Excel でデータ テーブルを操作する方法だけでなく、インポート オプションをカスタマイズしてニーズに合わせる方法も学習できます。信じてください。これで多くの時間と手間が節約できます! では、コーヒーを 1 杯飲んで、始めましょう!

## 前提条件

コーディングを始める前に、すべてがセットアップされていることを確認しましょう。

1. Visual Studio: Visual Studio がインストールされていることを確認します (2017 以降であれば問題なく動作するはずです)。
2.  Aspose.Cells for .NET: Aspose.Cellsライブラリが必要です。まだインストールしていない場合は、ダウンロードできます。[ここ](https://releases.aspose.com/cells/net/).
3. C# と Excel の基本的な理解: C# プログラミングと Excel の動作の基本的な理解があれば、より効果的に理解できるようになります。

また、サンプルのExcelファイルも用意しておくとよいでしょう。このガイドでは、サンプルとして`sampleImportTableOptionsShiftFirstRowDown.xlsx`このファイルを作成するか、ニーズに合ったテンプレートを見つけることができます。

## パッケージのインポート

コーディングを始める前に、必要なパッケージをインポートしていることを確認する必要があります。C# プロジェクトに次の名前空間を含めます。

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

これらのパッケージは、ワークブック、ワークシート、およびテーブルを操作するために不可欠です。

## ステップ1: プロジェクトを設定する

### 新しい C# プロジェクトを作成する

まず、Visual Studio で新しい C# コンソール アプリケーションを作成します。プロジェクトに「ExcelDataImport」などの適切な名前を付けます。

### Aspose.Cells NuGet パッケージを追加する

Aspose.Cells パッケージを追加するには、ソリューション エクスプローラーでプロジェクトを右クリックし、[NuGet パッケージの管理] を選択して、「Aspose.Cells」を検索します。パッケージをインストールして、必要なすべての機能にアクセスできることを確認してください。

## ステップ2: データテーブルを定義する

次に、`ICellsDataTable`インポートするデータを提供するクラスを作成するためのインターフェース。`CellsDataTable`クラス：

```csharp
class CellsDataTable : ICellsDataTable
{
    int m_index = -1;
    static String[] colsNames = new String[] { "Pet", "Fruit", "Country", "Color" };
    static String[] col0data = new String[] { "Dog", "Cat", "Duck" };
    static String[] col1data = new String[] { "Apple", "Pear", "Banana" };
    static String[] col2data = new String[] { "UK", "USA", "China" };
    static String[] col3data = new String[] { "Red", "Green", "Blue" };
    static String[][] colsData = new String[][] { col0data, col1data, col2data, col3data };
    
    // ...他のメンバーを実装します...
}
```

ここでは、列名と各列のデータを定義し、インポートしたテーブルの構造を容易にします。

## ステップ3: ICellsDataTableインターフェースメンバーを実装する

内で`CellsDataTable`クラスのメンバーを実装する必要があります`ICellsDataTable`インターフェース。必要な実装は次のとおりです。

```csharp
public object this[string columnName]
{
    get
    {
        throw new NotImplementedException();
    }
}

object ICellsDataTable.this[int columnIndex]
{
    get
    {
        return colsData[columnIndex][m_index];
    }
}

string[] ICellsDataTable.Columns
{
    get { return colsNames; }
}

int ICellsDataTable.Count
{
    get { return col0data.Length; }
}

void ICellsDataTable.BeforeFirst()
{
    m_index = -1;
}

bool ICellsDataTable.Next()
{
    m_index++;
    return (m_index < Count);
}
```

クラスのこの部分は、データの取得、行と列の数の定義、現在のインデックス状態の管理を処理します。

## ステップ4: メイン関数を書く

さて、`Run`テーブルのインポートプロセス全体を調整する方法:

```csharp
public static void Run()
{
    string sourceDir = "Your Document Directory\\";
    string outputDir = "Your Document Directory\\";
    
    CellsDataTable cellsDataTable = new CellsDataTable();
    Workbook wb = new Workbook(sourceDir + "sampleImportTableOptionsShiftFirstRowDown.xlsx");
    Worksheet ws = wb.Worksheets[0];
```

## ステップ5: インポートオプションを設定する

インポート動作を制御するには、`ImportTableOptions`そしてそれに応じてプロパティを設定します。具体的には、`ShiftFirstRowDown`に`false`.

```csharp
    ImportTableOptions opts = new ImportTableOptions();
    opts.ShiftFirstRowDown = false; //最初の行を下に移動したくない
```

## ステップ6: DataTableをインポートする

これで、データをインポートできるようになりました`CellsDataTable`ワークシートに入力します。

```csharp
    ws.Cells.ImportData(cellsDataTable, 2, 2, opts);
}
```

このコマンドは、指定された行と列からデータ テーブルを直接挿入します。

## ステップ7: ワークブックを保存する

最後に、変更したワークブックをファイルに保存します。

```csharp
    wb.Save(outputDir + "outputImportTableOptionsShiftFirstRowDown-False.xlsx");
}
```

## 結論

これで完了です。Aspose.Cells for .NET を使用して、最初の行を移動せずに DataTable 行を Excel シートに挿入する方法を学習しました。このプロセスは、Excel 内でのデータ操作を効率化するだけでなく、通常は面倒なタスクを自動化することでアプリケーションのパフォーマンスを向上させます。この知識をツールキットに組み込むことで、Excel の自動化タスクをより適切に処理できるようになり、時間と労力を節約できます。

## よくある質問

### Aspose.Cells for .NET とは何ですか?
Aspose.Cells for .NET は、開発者が .NET アプリケーションで Excel ファイルを作成、操作、変換できるようにするプログラミング ライブラリです。

### Aspose.Cells を使用するにはライセンスが必要ですか?
はい、全機能を使用するには有効なライセンスが必要です。ただし、初期テスト用に無料トライアルをご利用いただけます。

### Aspose.Cells を Web アプリケーションで使用できますか?
もちろんです! Aspose.Cells は、.NET で開発されたデスクトップ、Web、クラウドベースのアプリケーションに最適です。

### Aspose.Cells で作成できる Excel ファイルの種類は何ですか?
XLSX、XLS、CSV など、さまざまな Excel ファイル形式を作成できます。

### Aspose.Cells のサポートはどこで受けられますか?
質問したり、ヘルプを見つけたりすることができます[Aspose フォーラム](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
