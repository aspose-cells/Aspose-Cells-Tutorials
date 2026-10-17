---
category: general
date: 2026-10-10
description: C# を使用して Excel ワークブックから行全体を削除する方法を学びましょう。このステップバイステップガイドでは、インデックスで行を削除する方法や、Aspose.Cells
  を使用してインデックスで行を削除する方法も取り上げています。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete entire row
- how to delete row
- remove row by index
- delete row excel
- delete row c#
language: ja
lastmod: 2026-10-10
og_description: C# を使用して Excel ブックの行全体を削除する。インデックスで行を削除する方法、インデックスで行を除去する方法、そしてファイルを安全に保存する方法をこのガイドで学びましょう。
og_image_alt: Screenshot of an Excel worksheet before and after deleting an entire
  row with C# code
og_title: C#でExcelの行全体を削除する – 完全プログラミングガイド
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to delete entire row in an Excel workbook with C#. This step‑by‑step
    guide also covers how to delete row by index and remove row by index using Aspose.Cells.
  headline: How to delete entire row in an Excel file using C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: C#でExcelファイルの行全体を削除する方法
url: /ja/net/row-and-column-management/how-to-delete-entire-row-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# を使用して Excel ファイルの行全体を削除する

Excel ワークブックで **行全体を削除** したい場合、このガイドでは C# で正確に実行する方法を示します。インポートしたデータのクリーンアップやレポートツールの構築など、以下の手順でインデックスで行を削除し、他のデータを失うことなく結果を保存できます。

同じアプローチで **インデックスで行を削除する方法**、**インデックスで行を削除**、そして C# における **Excel 行の削除** シナリオがどのように機能するかも確認できます。

## 前提条件

開始する前に、以下が揃っていることを確認してください。

* .NET 6.0 以降（コードは .NET Framework 4.6+ でも動作します）  
* **Aspose.Cells for .NET** ライブラリ（NuGet で入手可能: `Install-Package Aspose.Cells`）  
* C# コンソールまたはデスクトッププロジェクトの基本的な知識  

追加の Excel Interop や COM コンポーネントは不要で、サーバーサイドでの実行にも軽量で安全です。

## 手順 1: プロジェクトの設定と名前空間のインポート

新しいコンソール アプリケーションを作成する（または既存プロジェクトにコードを追加する）し、必要な `using` ディレクティブを追加します。

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the tutorial code lives here.
        }
    }
}
```

*Why this matters*: `Aspose.Cells` をインポートすることで、`Workbook`、`Worksheet`、そして実際の行削除を行う `DeleteRows` メソッドにアクセスできます。

## 手順 2: ワークブックの読み込みとワークシートの選択

ソース ファイル（`input.xlsx`）を読み込み、変更したいワークシートを取得する必要があります。最初のワークシートはインデックス `0` でアクセスします。

```csharp
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Get the first worksheet (you can also use workbook.Worksheets["SheetName"])
Worksheet ws = workbook.Worksheets[0];
```

> **Tip**: 特定のシートで作業する必要がある場合は、インデックスをシート名に置き換えてください: `workbook.Worksheets["Data"]`.

## 手順 3: ゼロベースインデックスで行全体を削除する

Aspose.Cells はゼロベースのインデックスを使用するため、最初の行は `0` です。行 5（視覚的に 6 行目）を削除するには、`DeleteRows` に `DeleteOptions.DeleteEntireRow` を指定して呼び出します。

```csharp
// Delete one row starting at index 5 (zero‑based) and remove the whole row
ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
```

*Explanation*:

* `ws.Cells[5, 0]` は削除したい行の最初のセルを指します。  
* `DeleteRows(1, DeleteOptions.DeleteEntireRow)` は Aspose.Cells に **1** 行を削除するよう指示し、`DeleteEntireRow` フラグにより **行全体** が消えて下の行が上にシフトします。

### 他のシナリオでインデックスで行を削除する方法

* **複数の連続した行を削除** – 削除したい行数に合わせて最初の引数を変更します:

  ```csharp
  // Remove rows 5, 6 and 7 (three rows total)
  ws.Cells[5, 0].DeleteRows(3, DeleteOptions.DeleteEntireRow);
  ```

* **最終行を削除** – `ws.Cells.MaxDataRow` を使用して最下部にデータがある行のインデックスを取得します:

  ```csharp
  int lastRow = ws.Cells.MaxDataRow;
  ws.Cells[lastRow, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
  ```

これらのスニペットは **インデックスで行を削除** する要件に答えつつ、コードを読みやすく保ちます。

## 手順 4: 行が削除されたワークブックを保存する

削除後、変更されたワークブックをディスクに書き戻します。元のファイルを上書きすることも、新しいファイルを作成することも可能です。

```csharp
// Save the workbook to a new file (or overwrite the original)
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

元のファイルを変更せずに残したい場合は、出力パスを変更するだけです。`Save` メソッドは多数の形式（`.xls`、`.csv`、`.pdf` など）をサポートしているので、拡張子を変更すれば OK です。

## 完全な動作例

すべてをまとめると、以下のような完全な実行可能プログラムになります。

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Select the first worksheet
            Worksheet ws = workbook.Worksheets[0];

            // 3️⃣ Delete the entire row at index 5 (sixth visual row)
            ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);

            // 4️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");

            Console.WriteLine("Row deleted successfully. Output saved to output.xlsx");
        }
    }
}
```

**Expected output**: プログラム実行後、`output.xlsx` には元の行はすべて残りますが、視覚的に 6 行目に相当する行が削除されています。削除された行の下にあるデータは自動的に上へシフトし、数式や書式も保持されます。

## よくある落とし穴と回避策

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **Index out of range** | 存在しない行インデックスを削除しようとしたときに発生（例: 200 行シートで `ws.Cells[1000,0]`） | `DeleteRows` を呼び出す前に `ws.Cells.MaxDataRow` で有効な最大インデックスを確認します。 |
| **Partial row deletion** | `DeleteOptions.DeleteEntireRow` を省略するとセルの内容だけがクリアされる | 行全体を削除したい場合は必ず `DeleteOptions.DeleteEntireRow` を渡します。 |
| **Unexpected formula changes** | 数式範囲に含まれる行を削除すると参照が壊れる | ワークブックが動的範囲に依存している場合は削除後に `workbook.CalculateFormula()` で数式を再計算します。 |
| **Saving to a read‑only location** | フォルダーが保護されていると `Save` 呼び出しで例外がスローされる | 保存先ディレクトリが書き込み可能であることを確認するか、適切な権限でプログラムを実行します。 |

これらの対策を行うことで、ソリューションは本番環境でも堅牢になり、**delete row excel** や **delete row c#** の検索クエリにも対応できます。

## 上級編: 条件に基づく行の削除

場合によっては、特定の条件を満たす行（例: 列 A が空の行）を削除したいことがあります。以下のループは、下から上へスキャンしながら一致する行を安全に削除する方法を示しています。

```csharp
int lastRow = ws.Cells.MaxDataRow;
for (int row = lastRow; row >= 0; row--)
{
    // Check if column A (index 0) is empty
    if (ws.Cells[row, 0].StringValue == string.Empty)
    {
        ws.Cells[row, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
    }
}
workbook.Save("YOUR_DIRECTORY/cleaned.xlsx");
```

上向きにスキャンすることで、前方にイテレートしながら行を削除した際に発生するインデックスシフト問題を防げます。

## 結論

これで C# を使用して Excel ワークブックの **行全体を削除** する方法が分かりました。本ガイドで扱った内容は次の通りです。

* ワークブックの読み込みとワークシートの選択  
* `DeleteRows` と `DeleteOptions.DeleteEntireRow` を使って **インデックスで行を削除** する方法  
* 変更後のファイルを安全に保存する手順  
* エッジケースの処理、パフォーマンスのヒント、条件付き削除の例  

この知識があれば、**インデックスで行を削除** 機能を自信を持って実装でき、データのクリーンアップを自動化し、任意の C# アプリケーションに Excel 操作を組み込めます。

**Next steps**: 行の挿入、範囲のコピー、ワークブックの PDF 変換など、同じ `Workbook` と `Worksheet` オブジェクトを基盤とした他の Aspose.Cells 機能もぜひ探求してください。Happy coding!

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示したテクニックを基にした関連トピックをカバーしています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、プロジェクトで代替実装アプローチを検討したりするのに役立ちます。

- [Aspose.Cells .NET を使用した Excel 行の削除方法：包括的ガイド](/cells/english/net/worksheet-management/delete-excel-row-aspose-cells-net-tutorial/)
- [Aspose Cells Delete Rows – Excel でヘッダー行を保護](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [Aspose.Cells for Java を使用した Excel の効率的な行管理：行の挿入と削除](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}