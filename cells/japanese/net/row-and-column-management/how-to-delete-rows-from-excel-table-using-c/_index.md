---
category: general
date: 2026-09-27
description: C#でExcelテーブルから行を削除する方法を、ステップバイステップのガイドで学びましょう。また、ExcelブックをC#で素早く読み込む方法も紹介しています。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from Excel table
- load Excel workbook C#
language: ja
lastmod: 2026-09-27
og_description: C#でExcelテーブルから行を削除する方法を、具体的な例とともに解説します。このチュートリアルでは、C#でExcelブックを読み込む方法や、一般的なエッジケースの対処法も取り上げています。
og_image_alt: Screenshot illustrating delete rows from Excel table using C# code
og_title: C#でExcelテーブルから行を削除する – 完全コードガイド
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  headline: How to delete rows from Excel table using C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  name: How to delete rows from Excel table using C#
  steps:
  - name: What if the table has a different name or position?
    text: '* **Named table:** Use `ws.ListObjects["MyTableName"]` instead of the index.
      * **Multiple tables:** Loop through `ws.ListObjects` and pick the one that matches
      a condition (e.g., column header names). * **Dynamic row count:** You can compute
      `rowCount` at runtime by inspecting `ws.ListObjects[0].Dat'
  - name: Edge‑case handling
    text: '| Situation | Recommended code change | |----------------------------------------|--------------------------------------------------------------|
      | Table is empty or has fewer rows | Check `ws.ListObjects[0].DataRange.RowCount`
      before deleting. | | Rows to delete exceed table size | Clamp `rowCount`'
  - name: How do I delete rows from **all** tables in a workbook?
    text: '```csharp foreach (Worksheet sheet in workbook.Worksheets) { foreach (ListObject
      tbl in sheet.ListObjects) { // Example: delete the first data row of each table
      if (tbl.DataRange.RowCount > 1) tbl.DeleteRows(1, 1); } } ```'
  - name: Can I delete rows based on a **cell value**?
    text: 'Yes. Scan the `DataRange` for matching cells, collect their zero‑based
      indices, then delete in descending order:'
  - name: What if I need to **preserve formatting**?
    text: '`DeleteRows` removes the entire row from the table but retains the table’s
      style for remaining rows. If you need to keep specific formatting on a row you’re
      deleting, copy the style to another row before deletion.'
  - name: Does this work with **.xls** (Excel 97‑2003) files?
    text: Yes. Aspose.Cells automatically detects the file format, so the same code
      works with `.xls`. Just change the file extension in the `Workbook` constructor.
  - name: Next steps
    text: '* Explore **ClosedXML** or **EPPlus** if you prefer a fully open‑source
      stack. * Combine row deletion with **data validation** to clean spreadsheets
      before importing into a database. * Automate the process for a folder of workbooks
      using `Directory.GetFiles` and a loop.'
  type: HowTo
tags:
- Excel
- C#
- .NET
title: C# を使用して Excel テーブルから行を削除する方法
url: /ja/net/row-and-column-management/how-to-delete-rows-from-excel-table-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Excel テーブルから行を削除する – 完全プログラミングガイド

.xlsx ファイル内の **Excel テーブルから行を削除** する必要がある場合、このチュートリアルでは C# を使用した具体的な手順を示します。Excel ワークブックを読み込み、最初のテーブルから特定の行を削除し、結果を保存する簡潔で実行可能なサンプルが確認できます。この手法は一般的な Aspose.Cells ライブラリで動作し、他の .NET Excel API にも適用可能です。

テーブルから行を削除することは、インポートされたデータのクレンジング、レポートセクションのトリミング、スプレッドシートの自動更新などで頻繁に行われるタスクです。本ガイドの最後まで読むと、**C# で Excel ワークブックをロード**し、テーブル（ListObject）を特定し、任意の行を安全に削除し、変更されたファイルをディスクに書き戻す方法が身につきます。

## 前提条件

開始する前に、以下を確認してください。

* .NET 6.0 以降がインストールされていること（コードは .NET Framework 4.7+ でも動作します）。
* **Aspose.Cells** NuGet パッケージへの参照（または `Workbook`、`Worksheet`、`ListObject` 型を公開する互換ライブラリ）。
* プロジェクトから参照できるフォルダーに配置した `input.xlsx` という名前の入力ファイル。
* C# の構文と Visual Studio（または好みの IDE）に関する基本的な知識。

> **Pro tip:** オープンソースの代替手段を好む場合、同じロジックを **ClosedXML** で適用できます – Aspose 固有のクラスを `XLWorkbook`、`IXLWorksheet`、`IXLTable` に置き換えるだけです。

## 手順 1: C# で Excel ワークブックをロードする

最初の操作は、ソースファイルをメモリに読み込むことです。ワークブックのロードは一般的なスプレッドシートサイズではコストが低く、ワークシート、テーブル、セル値へのフルアクセスが得られます。

```csharp
using Aspose.Cells;

// Step 1: Load the workbook
// Replace YOUR_DIRECTORY with the actual folder path, e.g. @"C:\Data"
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

*Why this matters:* `Workbook` は .xlsx ファイルの Open XML 構造を解析し、`Worksheet` オブジェクトのコレクションを提供します。ファイルが見つからない場合、Aspose は `FileNotFoundException` をスローするため、パスが正しいことを確認してください。

## 手順 2: 対象のワークシートにアクセスする

多くのスプレッドシートは複数のシートを持ちます。変更したいテーブルがあるシートを選択する必要があります。ここではシンプルなファイル向けに安全なデフォルトとして最初のシート（`Worksheets[0]`）を使用します。

```csharp
// Step 2: Access the first worksheet
Worksheet ws = workbook.Worksheets[0];
```

*Why this matters:* `Worksheet` はテーブル（`ListObjects`）のコンテナです。正しいシートにアクセスすることで、無関係なデータへの誤変更を防げます。

## 手順 3: Excel テーブルから行を削除する

Excel テーブルは `ListObject` オブジェクトで表されます。シート上の最初のテーブルは `ListObjects[0]` です。`DeleteRows(startIndex, rowCount)` メソッドは **テーブルのデータ領域に対して相対的に** 行を削除し、ワークシートの絶対行番号ではありません。

この例ではテーブルの 2 行目と 3 行目を削除します（ヘッダーが 0 行目なのでインデックスは 1 から開始）。

```csharp
// Step 3: Delete rows 1 and 2 from the first table (ListObject)
// The first row (index 0) is the header, so we start at index 1
ws.ListObjects[0].DeleteRows(1, 2);
```

### テーブルの名前や位置が異なる場合は？

* **名前付きテーブル:** インデックスの代わりに `ws.ListObjects["MyTableName"]` を使用します。
* **複数テーブル:** `ws.ListObjects` をループし、条件（例: 列ヘッダー名）に合致するものを選択します。
* **動的な行数:** 実行時に `ws.ListObjects[0].DataRange.RowCount` を調べて `rowCount` を算出できます。

### エッジケースの処理

| 状況 | 推奨されるコード変更 |
|------|----------------------|
| テーブルが空、または行数が不足している | 削除前に `ws.ListObjects[0].DataRange.RowCount` をチェックします。 |
| 削除対象の行数がテーブルサイズを超える | `rowCount` を `DataRange.RowCount - startIndex` にクランプします。 |
| 条件（例: 列 C の値）に基づいて行を削除する必要がある | `DataRange.Rows` を走査して一致するインデックスを収集し、インデックスが安定するよう逆順で削除します。 |

## 手順 4: 変更されたワークブックを保存する

削除が完了したら、ワークブックを新しいファイル（または上書きしたい場合は元のファイル）に書き出します。保存により、更新されたテーブルを反映した新しい .xlsx が生成されます。

```csharp
// Step 4: Save the modified workbook
workbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

*Why this matters:* `Save` はメモリ上の表現をディスクにシリアライズします。元のファイルを保持したい場合は、必ず別のパスに書き込んでください。

## 完全な実行可能サンプル

すべての手順を組み合わせると、コピー＆ペーストしてすぐに実行できる自己完結型プログラムが完成します。

```csharp
using System;
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Adjust the folder path as needed
        const string folder = @"YOUR_DIRECTORY";

        // Load the workbook (load Excel workbook C#)
        Workbook workbook = new Workbook($"{folder}\\input.xlsx");

        // Access the first worksheet
        Worksheet ws = workbook.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (ws.ListObjects.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Delete rows 1 and 2 from the first table (skip header)
        ListObject table = ws.ListObjects[0];
        int rowsToDelete = Math.Min(2, table.DataRange.RowCount - 1); // guard against short tables
        if (rowsToDelete > 0)
        {
            table.DeleteRows(1, rowsToDelete);
            Console.WriteLine($"Deleted {rowsToDelete} row(s) from table \"{table.Name}\".");
        }
        else
        {
            Console.WriteLine("Table does not have enough rows to delete.");
        }

        // Save the result
        workbook.Save($"{folder}\\output.xlsx");
        Console.WriteLine("Workbook saved as output.xlsx");
    }
}
```

**期待される出力** (コンソール):

```
Deleted 2 row(s) from table "Table1".
Workbook saved as output.xlsx
```

`output.xlsx` を開くと、最初のテーブルから削除した行がなくなり、ヘッダー行はそのまま残っていることが確認できます。

## よくある質問とバリエーション

### ワークブック内の **すべての** テーブルから行を削除するには？

```csharp
foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (ListObject tbl in sheet.ListObjects)
    {
        // Example: delete the first data row of each table
        if (tbl.DataRange.RowCount > 1)
            tbl.DeleteRows(1, 1);
    }
}
```

### **セルの値** に基づいて行を削除できますか？

はい。`DataRange` を走査して一致するセルを見つけ、ゼロベースのインデックスを収集し、降順で削除します。

```csharp
var rowsToRemove = new List<int>();
for (int i = 0; i < table.DataRange.RowCount; i++)
{
    var cell = table.DataRange[i, 2]; // column C (zero‑based)
    if (cell.StringValue == "Obsolete")
        rowsToRemove.Add(i);
}

// Delete rows from bottom to top to keep indices valid
rowsToRemove.Sort((a, b) => b.CompareTo(a));
foreach (int rowIdx in rowsToRemove)
    table.DeleteRows(rowIdx, 1);
```

### **書式を保持** する必要がある場合は？

`DeleteRows` はテーブルから行全体を削除しますが、残りの行に対してテーブルのスタイルは保持されます。削除する行の特定の書式を保持したい場合は、削除前に別の行へスタイルをコピーしてください。

### **.xls** (Excel 97‑2003) ファイルでも動作しますか？

はい。Aspose.Cells はファイル形式を自動検出するため、同じコードが `.xls` でも機能します。`Workbook` コンストラクタの拡張子を変更するだけです。

## パフォーマンスのヒント

* **バッチ削除:** 行を 1 つずつ削除すると遅くなることがあります。可能な限り `DeleteRows(start, count)` を一括で呼び出してください。
* **UI スレッドのブロッキング回避:** デスクトップアプリに組み込む場合は、ワークブック操作をバックグラウンドスレッドで実行し、UI の応答性を保ちます。
* **適切な破棄:** Aspose.Cells は管理メモリを使用しますが、大きなファイルを扱う際は `using` ブロックで `Workbook` を囲み、リソースを速やかに解放してください。

## 結論

これで **C# で Excel テーブルから行を削除** するための完全な、実運用可能なサンプルが手に入りました。本ガイドでは **C# で Excel ワークブックをロード**し、目的の `ListObject` を特定し、安全に行を削除し、更新されたファイルを保存する手順を解説しました。エッジケースの処理やパフォーマンスに関するアドバイスも含めているので、条件付き削除や複数テーブル、あるいは別の .NET Excel ライブラリへの適用など、より複雑なシナリオにも応用できます。

### 次のステップ

* 完全にオープンソースのスタックを好む場合は **ClosedXML** や **EPPlus** を調査してください。
* データベースにインポートする前にスプレッドシートをクリーンアップするため、**データ検証** と組み合わせた行削除を検討してください。
* `Directory.GetFiles` とループを使用して、フォルダー内の複数ワークブックに対して自動化プロセスを構築してください。

さまざまな行範囲、テーブル名、条件ロジックで実験してみてください。コーディングを楽しんでください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示したテクニックを基にした密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得したり、プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [Load Excel File C# – How to Delete Rows and Remove Specific Rows](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)
- [How to Insert and Delete Rows in Excel with Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [How to Delete Blank Rows in Excel Using Aspose.Cells .NET for Data Cleanup](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}