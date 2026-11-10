---
category: general
date: 2026-10-01
description: C# を使用して Excel テーブルから行を削除し、テーブル名を変更する方法を学びます。フルコードとベストプラクティスを含むステップバイステップガイド。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows excel table
- change excel table name
- load excel workbook c#
- remove rows from excel table
- update excel table name
language: ja
lastmod: 2026-10-01
og_description: C#でExcelテーブルの行を削除し、テーブル名を変更します。ワークブックを読み込み、テーブルを編集し、結果を保存する完全なチュートリアルをご覧ください。
og_image_alt: Screenshot showing C# code that deletes rows from an Excel table and
  updates the table name
og_title: C#でExcelテーブルの行を削除し、名前を変更する完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn to delete rows from an Excel table and change the Excel table
    name using C#. Step‑by‑step guide with full code and best practices.
  headline: How to delete rows from an Excel table and change its name in C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
title: C#でExcelテーブルの行を削除し、名前を変更する方法
url: /ja/net/tables-and-lists/how-to-delete-rows-from-an-excel-table-and-change-its-name-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でExcelテーブルの行を削除し、名前を変更する方法

C#で作業中に **Excelテーブルから行を削除** する必要がある場合、このガイドでは必要な手順を正確に示します。**C#でExcelブックをロード** し、テーブルから特定の行を削除し、そして **Excelテーブルの名前を更新** してファイルの一貫性を保つ方法が分かります。

このチュートリアルでは、必要な NuGet パッケージ、完全に実行可能なコード、テーブル構造の破壊などの一般的な落とし穴についてすべてカバーしています。記事の最後までに、手動での操作なしに任意の Excel テーブルをプログラムで変更できるようになります。

## 前提条件

* .NET 6.0 SDK 以降がインストールされていること。
* .NET 開発用に設定された Visual Studio 2022（または任意の C# IDE）。
* NuGet で追加した **Aspose.Cells for .NET** ライブラリ（`Install-Package Aspose.Cells`）。
* 少なくとも 1 つのワークシートにテーブルが含まれる既存の Excel ブック（`Table.xlsx`）。

これらの項目は、**C#でExcelブックをロード** するコードを実行し、操作を確実に行うための環境を提供します。

## 手順 1: テーブルを含むブックをロードする

最初の操作はブックファイルを開くことです。Aspose.Cells はブック全体をメモリに読み込み、ワークシート、テーブル、セルデータを完全に制御できるようにします。

```csharp
using Aspose.Cells;

string inputPath = @"C:\Data\Table.xlsx";

// Load the workbook from disk
Workbook workbook = new Workbook(inputPath);
```

*Why this matters*（なぜ重要か）: ブックのロードは、以降のテーブル操作すべての基礎となります。`Workbook` オブジェクトは `Worksheets` コレクションを公開しており、対象テーブルを見つけるために使用します。

## 手順 2: 最初のワークシートとその最初のテーブルにアクセスする

ほとんどの Excel ファイルはテーブルを最初のワークシートに格納しますが、必要に応じてインデックスを調整できます。以下のコードは最初の `Table` オブジェクトを取得します。

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Retrieve the first table on that worksheet
Table table = sheet.Tables[0];
```

ワークシートにテーブルが存在しない場合、`sheet.Tables.Count` は 0 となり、そのケースを処理すべきです。テーブルが存在しない状態で `sheet.Tables[0]` にアクセスしようとすると例外がスローされるため、本番コードではガード句を使用することが推奨されます。

## 手順 3: Excel テーブルから行を削除する

Excel テーブルから **行を削除** するには、`DeleteRows(startRow, totalRows)` を呼び出します。`startRow` パラメータはテーブルの最初のデータ行（ヘッダーの次の行）を基準としたゼロベースです。

```csharp
// Delete two rows starting from the second data row (index 1)
int startRow = 1;   // second row within the table
int rowsToDelete = 2;

table.DeleteRows(startRow, rowsToDelete);
```

### `DeleteRows` を使用する理由（ワークシートの行を削除する代わりに）

`DeleteRows` はテーブルの内部範囲を更新し、テーブルに属する数式、スタイル、定義名を保持します。ワークシートの行を直接削除するとテーブル構造が壊れ、例外が発生する可能性があります。

**エッジケース**: 削除後にテーブルにデータ行が残らない場合、Aspose.Cells は `ArgumentException` をスローします。削除前に `table.RowCount` を確認してガードしてください。

```csharp
if (table.RowCount - rowsToDelete < 1)
{
    throw new InvalidOperationException("Cannot delete all data rows from the table.");
}
```

## 手順 4: Excel テーブルの名前を変更する

行を削除した後、テーブルにより説明的な識別子を付けたくなることがあります。`Name` プロパティはテーブルの定義名を設定し、数式や VBA で使用されます。

```csharp
// Assign a new name to the table
string newTableName = "SalesData2026";

if (workbook.Worksheets.GetDefinedNames().Any(d => d.Text == newTableName))
{
    throw new InvalidOperationException($"The name '{newTableName}' already exists as a defined name.");
}

table.Name = newTableName;
```

*Why rename?*（なぜ名前を変更するか） 明確なテーブル名は数式（`=SUM(SalesData2026[Amount])`）の可読性を向上させ、複数のテーブルが似た目的で使用される際の名前衝突を防ぎます。

## 手順 5: 変更されたブックを保存する（オプション）

変更を新しいファイルに保存するか、元のファイルを上書きして永続化します。開発中は新しい場所に保存する方が安全です。

```csharp
string outputPath = @"C:\Data\ModifiedTable.xlsx";
workbook.Save(outputPath);
```

`Save` メソッドは、変更されたテーブル範囲と新しいテーブル名を含む更新済みブックを書き込み、ディスクに保存します。

## 完全な動作例

すべての手順を組み合わせると、すぐに実行できる自己完結型プログラムが得られます。

```csharp
using System;
using System.Linq;
using Aspose.Cells;

class ExcelTableModifier
{
    static void Main()
    {
        // ----- Step 1: Load workbook -----
        string inputPath = @"C:\Data\Table.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // ----- Step 2: Access worksheet and table -----
        Worksheet sheet = workbook.Worksheets[0];
        if (sheet.Tables.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        Table table = sheet.Tables[0];

        // ----- Step 3: Delete rows -----
        int startRow = 1;      // second data row (zero‑based)
        int rowsToDelete = 2;

        if (table.RowCount - rowsToDelete < 1)
        {
            Console.WriteLine("Deletion would remove all data rows; operation aborted.");
            return;
        }

        table.DeleteRows(startRow, rowsToDelete);
        Console.WriteLine($"{rowsToDelete} rows removed starting at index {startRow}.");

        // ----- Step 4: Change table name -----
        string newTableName = "SalesData2026";

        bool nameExists = workbook.Worksheets.GetDefinedNames()
                               .Any(d => d.Text.Equals(newTableName, StringComparison.OrdinalIgnoreCase));

        if (nameExists)
        {
            Console.WriteLine($"The name '{newTableName}' already exists. Choose a different name.");
            return;
        }

        table.Name = newTableName;
        Console.WriteLine($"Table renamed to '{newTableName}'.");

        // ----- Step 5: Save workbook -----
        string outputPath = @"C:\Data\ModifiedTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Modified workbook saved to '{outputPath}'.");
    }
}
```

**期待される出力**（ファイルとテーブルが存在することを前提）:

```
2 rows removed starting at index 1.
Table renamed to 'SalesData2026'.
Modified workbook saved to 'C:\Data\ModifiedTable.xlsx'.
```

プログラムを実行すると、説明どおりに Excel ファイルが更新されます。行が削除され、テーブル名が変更され、結果が手動編集なしで保存されます。

## よくある質問とトラブルシューティング

| Question | Answer |
|----------|--------|
| *テーブルが結合セルにまたがる場合はどうなりますか？* | `DeleteRows` は結合範囲を尊重します。結合セルが削除境界を跨ぐ場合、Aspose.Cells が自動的に結合を調整します。複雑な結合に依存する場合は、結果を目視で確認してください。 |
| *ピボットキャッシュの一部であるテーブルから行を削除できますか？* | ピボットテーブルの元になるテーブルから行を削除しても、ピボットキャッシュは自動的に更新され**ません**。元テーブルを変更した後、`pivotTable.RefreshData()` を呼び出してください。 |
| *条件（例: 値 < 0）に基づいて行を削除できますか？* | はい。`table.ListObjects` または `table.Rows` を走査して条件に合致する行を特定し、インデックスを収集して各範囲に対して `DeleteRows` を呼び出します。 |
| *`Workbook` オブジェクトを破棄する必要がありますか？* | `Workbook` は `IDisposable` を実装しています。特に大きなファイルを処理する場合は、決定的にリソースを解放できるよう `using` ブロックでラップしてください。 |
| *EPPlus を使用する場合と何が違いますか？* | EPPlus もテーブル操作をサポートしていますが、異なる API（`ExcelTable`）を使用します。ブックのロード、行の削除、テーブルの名前変更という概念は類似しています。ライセンス要件に合ったライブラリを選択してください。 |

## C#でExcelテーブルを変更する際のベストプラクティス

* **インデックスを検証する** – テーブルの行インデックスはゼロベースです。オフバイワンエラーは予期しない削除を引き起こします。
* **名前の衝突を確認する** – Excel は重複した定義名を許可しません。新しい名前を割り当てる前に必ず一意性を確認してください。
* **元ファイルをバックアップする** – 自動化スクリプトでデータが破損する可能性があるため、元のブックのコピーを保持してください。
* **`using` 文を使用する** – ファイルハンドルが速やかに解放されることを保証します:

```csharp
using (Workbook wb = new Workbook(inputPath))
{
    // modify workbook
}
```

* **エッジケースでテストする** – データ行が1行だけのテーブル、シート全体にまたがるテーブル、チャートにリンクされたテーブルは、変更後に必ず検証してください。

## 結論

これで、C# を使用して **Excel テーブルから行を削除** し、 **Excel テーブルの名前を変更** する方法が分かりました。完全なソリューションはブックをロードし、対象テーブルにアクセスし、目的の行を削除し、テーブルの名前を変更し、結果を保存します。これらの手法をレポート作成の自動化、データクレンジング、またはプログラムで Excel テーブルを管理する必要があるあらゆるワークフローに適用してください。

次に、**Excel テーブルのセル値を更新**、**プログラムで新しい行を追加**、**テーブルデータを CSV にエクスポート** などの関連トピックを探求してください。これらの操作を習得すれば、C# アプリケーション内から Excel ファイルを完全に制御できるようになります。

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックをカバーしています。各リソースには、ステップバイステップの解説付きの完全な動作コード例が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [C#でExcelのテーブル名を変更する方法 – ステップバイステップガイド](/cells/english/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/)
- [C#でExcelテーブルを作成する – ステップバイステップガイド](/cells/english/net/tables-and-lists/create-excel-table-in-c-step-by-step-guide/)
- [C#でExcelブックから最初のテーブルを取得する – 完全ガイド](/cells/english/net/excel-autofilter-validation/get-first-table-from-excel-workbook-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}