---
category: general
date: 2026-07-13
description: C# を使用して Excel でセルを上にシフトします。最初の行を削除し、複数行を削除し、テーブルから行を削除する方法を、1 回の安全な操作で学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- shift cells up
- remove first rows
- remove rows from table
- delete multiple rows
- how to delete rows
language: ja
lastmod: 2026-07-13
og_description: C# を使用して Excel ワークシートのセルを上にシフトします。このチュートリアルでは、最初の行を削除する方法、複数行を削除する方法、テーブルから行を安全に削除する方法を示します。
og_image_alt: Screenshot of C# code that shifts cells up after deleting rows in an
  Excel worksheet
og_title: C#でExcelのセルを上にシフトする – 完全プログラミング解説
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Shift cells up in Excel using C#. Learn how to remove first rows, delete
    multiple rows, and remove rows from table in a single, safe operation.
  headline: Shift Cells Up in Excel with C# – Complete Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Loop through `sheet.Cells.Rows` and call `DeleteRows(rowIndex,
      1, true)` whenever the condition matches. Just remember to iterate backwards
      to avoid index shifting.
    question: Can I delete rows based on a condition instead of a fixed index?
  - answer: Yes. Aspose.Cells supports both `.xlsx` and legacy `.xls` formats. The
      same API applies.
    question: Does this work with `.xls` files?
  - answer: 'Target the specific table by name: `Table myTable = sheet.Tables["MyTable"];`
      then use `myTable.Range.StartRow` to calculate the rows to delete. --- ## Full
      Working Example Below is the complete, ready‑to‑run program that incorporates
      everything we discussed. Copy‑paste it into a console app, adjust'
    question: What if my workbook contains multiple tables and I only want to affect
      one?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: C#でExcelのセルを上にシフトする – 完全ガイド
url: /ja/net/row-and-column-management/shift-cells-up-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でExcelのセルを上にシフトする – 完全ガイド

Excelファイルで行を削除した後に **セルを上にシフト** する方法を考えたことはありますか？ あなただけではありません。インポートしたデータのクリーンアップや大規模レポートの削減を行う際、テーブルを壊さずに最初の行を削除できることは、C# 開発者にとって必須のスキルです。

このチュートリアルでは、実践的なエンドツーエンドのソリューションを順に解説します。**行の削除方法** を示し、ヘッダーを保持したまま残りのセルを自動的に上にシフトします。最後まで読むと、数行のコードで **テーブルから行を削除**、**複数行の削除**、そして **最初の行の削除** ができるようになります。

---

## 必要なもの

- .NET 6+（または .NET Framework 4.7.2 以上）  
- **Aspose.Cells for .NET** ライブラリ（無料トライアルまたはライセンス版）  
- C# と Visual Studio（またはお好みの IDE）に関する基本的な理解  

他に依存関係はありません—NuGet パッケージと操作対象の Excel ファイルだけです。

## 手順 1: Aspose.Cells のインストール

まずは、Aspose.Cells パッケージをプロジェクトに追加します。

```bash
dotnet add package Aspose.Cells
```

この一行で、ブック、ワークシート、テーブルを操作するために必要なものがすべて取得できます。Visual Studio を使用している場合は、プロジェクトを右クリック → **Manage NuGet Packages** → *Aspose.Cells* を検索し、**Install** をクリックすることもできます。

*Pro tip:* 最新の安定版を使用してください。2026年7月時点では **23.9.0** で、最新の Excel ファイル形式をサポートしています。

## 手順 2: テーブルを含むワークブックの読み込み

次に、クリーンアップしたいデータが入っている Excel ファイルを開きます。`YOUR_DIRECTORY` を実際のパスに置き換えてください。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains the table
        Workbook workbook = new Workbook(@"C:\Data\table.xlsx");
        
        // Grab the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];
        
        // Optional: get a reference to the first table for context
        Table table = sheet.Tables[0];
```

この時点で、操作可能な `Worksheet` オブジェクトが取得できました。まだテーブルには触れていません—後で **セルを上にシフト** する際にヘッダーを保持することが重要です。

## 手順 3: 最初の 2 行を削除しながらセルを上にシフト

ここが本題です：行を削除し、下のセルを自動的に上に移動させます。Aspose.Cells の `DeleteRows` メソッドは、`shiftCellsUp` フラグに `true` を渡すとまさにそれを実行します。

```csharp
        // Delete the first two rows (row index starts at 0)
        // The third argument ‑‑> true tells Aspose.Cells to shift cells up.
        sheet.Cells.DeleteRows(0, 2, true);
```

### `true` フラグが重要な理由

`true` フラグを省略すると、行は削除されますが、その位置は空白のままでデータに隙間が残ります。**true** に設定すると、ライブラリは範囲を縮め、実質的に **セルを上にシフト** して行 3 が新しい行 1 になります。これが、数式やテーブル構造を壊さずに **最初の行を削除** する最もクリーンな方法です。

> **重要:** テーブルヘッダーを含む行を削除すると例外がスローされます。ヘッダー行（通常は行 0）をそのまま保持するか、テーブルヘッダーを再作成した後に別途削除してください。

## 手順 4: テーブルが正しく保持されているか確認

削除後、テーブル参照が正しい範囲を指しているか二重チェックすることをお勧めします。テーブルのアドレスを出力するか、リフレッシュできます。

```csharp
        // Refresh the table range to reflect the new data area
        table.Refresh();

        // Output the new range for debugging
        Console.WriteLine($"Table now spans: {table.Ref}");
```

プログラムを実行すると、元の `A1:D10` の代わりに `Table1!A1:D8` のように表示され、行が削除されセルが上にシフトしたことが確認できます。

## 手順 5: 変更後のワークブックを保存

最後に、変更をディスクに書き戻します。元のファイルを上書きしても、別のコピーを作成しても構いません。

```csharp
        // Save the workbook with the changes
        workbook.Save(@"C:\Data\modified_table.xlsx");
    }
}
```

`modified_table.xlsx` を Excel で開くと、最初の 2 行が削除され、残りの行が上に移動し、テーブルはそのまま保持されていることがわかります。この操作により、データの整合性を保ったまま **複数行の削除** が実現されました。

## エッジケースと一般的な落とし穴

| 状況 | 起こること | 対処方法 |
|-----------|--------------|------------------|
| **ヘッダー行が削除範囲に含まれる** | テーブルはヘッダーを失うことができないため、Aspose.Cells は `InvalidOperationException` をスローします。 | データ行だけを削除するか、削除後に `sheet.Cells["A1"].PutValue("Header")` を使用してヘッダーを再作成してください。 |
| **テーブルが複数のワークシートにまたがる** | あるシートで行を削除しても、他のシートには影響しません。 | 全体をクリーンアップする必要がある場合は、各ワークシートのテーブルをループしてください。 |
| **大容量ファイル（>100 MB）** | メモリ使用量が急増します。 | `LoadOptions` の `MemoryPreference` を `MemoryPreference.MemoryOnly` に設定して、RAM の使用量を削減します。 |
| **削除された行を参照している数式を保持する必要がある** | 数式が `#REF!` になる可能性があります。 | `sheet.Cells.DeleteRows(startRow, count, true, true)` を使用します—4 番目の引数が Aspose.Cells に数式の更新を指示します。 |

## よくある質問

**Q: 固定インデックスではなく条件に基づいて行を削除できますか？**  
A: もちろんです。`sheet.Cells.Rows` をループし、条件に合致したときに `DeleteRows(rowIndex, 1, true)` を呼び出します。インデックスのシフトを防ぐために、逆方向にイテレートすることを忘れないでください。

**Q: `.xls` ファイルでも動作しますか？**  
A: はい。Aspose.Cells は `.xlsx` とレガシーな `.xls` の両方の形式をサポートしており、同じ API が使用できます。

**Q: ワークブックに複数のテーブルがあり、特定のテーブルだけに影響を与えたい場合はどうすればいいですか？**  
A: 名前で特定のテーブルを対象にします：`Table myTable = sheet.Tables["MyTable"];` そして `myTable.Range.StartRow` を使用して削除する行を計算します。

## 完全な動作例

以下は、ここまで説明したすべてを組み込んだ完全な実行可能プログラムです。コンソールアプリにコピー＆ペーストし、ファイルパスを調整して **F5** を押してください。

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"C:\Data\table.xlsx");
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ (Optional) Reference the first table for context
        Table table = sheet.Tables[0];

        // 3️⃣ Delete the first two rows and shift cells up
        //    Row index starts at 0, delete 2 rows, shift up = true
        sheet.Cells.DeleteRows(0, 2, true);

        // 4️⃣ Refresh the table range so it reflects the new data area
        table.Refresh();

        // 5️⃣ Show the new table reference (useful for debugging)
        Console.WriteLine($"Table now spans: {table.Ref}");

        // 6️⃣ Save the modified workbook
        workbook.Save(@"C:\Data\modified_table.xlsx");

        Console.WriteLine("Rows removed and cells shifted up successfully!");
    }
}
```

**期待される結果:**  
- シートから行 1‑2 が消えます。  
- 行 3 が新しい行 1 となり、行 4 が行 2 になるなど。  
- テーブルの範囲が自動的に更新され、**セルを上にシフト** が意図通りに機能したことが確認できます。

## 結論

ここでは、C# を使用して Excel ワークシートで **セルを上にシフト** する方法を解説しました。Aspose.Cells の `DeleteRows` メソッドに `true` フラグを使用することで、データモデルを壊すことなく **最初の行を削除**、**複数行の削除**、そして **テーブルから行を削除** が安全に行えます。この手法は高速で信頼性が高く、すべての最新 Excel 形式で動作します。

次のステップに進みませんか？この手法と条件フィルターを組み合わせて、空白や重複エントリを含む行を削除してみてください。また、シフト後に書式を再適用するために Aspose.Cells のスタイリング API を試すのも良いでしょう。Excel の行操作をマスターすれば、可能性は無限です。

質問や面白いユースケースがあれば、ぜひ下にコメントを残してください。ハッピーコーディング！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.Cells .NET を使用した Excel の複数行削除 – データ操作の包括的ガイド](/cells/english/net/data-manipulation/delete-rows-excel-aspose-cells-net/)
- [Aspose.Cells for .NET を使用した Excel の行の挿入と削除 – 包括的ガイド](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Aspose.Cells .NET を使用した Excel の空白行削除 – データクリーンアップガイド](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}