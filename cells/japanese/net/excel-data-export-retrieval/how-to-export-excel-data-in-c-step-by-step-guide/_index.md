---
category: general
date: 2026-03-21
description: Aspose.Cells を使用して C# で列名付きの Excel データをエクスポートし、数値形式を保持し、特定の行を読み取る方法。Excel
  ワークシートの読み取りと特定の行の効率的なエクスポートを学びましょう。
draft: false
keywords:
- how to export excel
- preserve number format
- export with column names
- read excel worksheet
- export specific rows
language: ja
og_description: Aspose.Cells を使用して、列名を含む Excel データをエクスポートし、数値形式を保持し、特定の行を読み取る方法。C#
  開発者向けの完全な実行可能サンプルです。
og_title: C#でExcelデータをエクスポートする方法 – 完全プログラミングガイド
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: C#でExcelデータをエクスポートする方法 – ステップバイステップガイド
url: /ja/net/excel-data-export-retrieval/how-to-export-excel-data-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でExcelデータをエクスポートする方法 – 完全プログラミングガイド

元の書式を失わずに **Excel データをエクスポートする方法** を考えたことはありませんか？ コピー＆ペーストだけで試したら、日付が “44728” のように表示されたり、列ヘッダーが欠落したりした経験があるかもしれません。イライラしますよね。この記事では、Excel ワークシートを読み込み、数値書式を保持し、列名付きでエクスポートし、必要な行だけを抽出する、クリーンでエンドツーエンドな手順をご紹介します。

Aspose.Cells ライブラリを使用します。これによりエクスポートオプションを細かく制御できます。このガイドが終わる頃には、任意の .NET プロジェクトに貼り付けられる再利用可能なスニペットが手に入り、各オプションの重要性が理解できるようになります。外部ドキュメントは不要です—必要な情報はすべてここにあります。

---

## 学べること

- **Excel ワークシートを** Aspose.Cells でメモリに読み込む方法  
- **特定の行**（例：0‑49 行）を列名を保持したままエクスポートする方法  
- **数値書式を保持** して通貨・日付・パーセンテージをそのまま出力する方法  
- **列名付きでエクスポート** し、必要に応じてセルコメントも含める方法  
- 完全に動作する C# サンプルと、よくある落とし穴への対策

### 前提条件

- .NET 6.0 以上（.NET Framework 4.6+ でも動作します）  
- NuGet でインストールした Aspose.Cells for .NET（`Install-Package Aspose.Cells`）  
- `input.xlsx` という名前の Excel ファイルを、参照可能なフォルダーに配置しておくこと

> **プロのコツ:** CI パイプライン上で実行する場合は、ライセンスのサプライズを防ぐためにプライベートフィードから NuGet パッケージを取得することを検討してください。

---

## Step 1 – Aspose.Cells のインストールと名前空間の追加

まず、プロジェクトに Aspose.Cells パッケージが入っていることを確認します。Package Manager Console で次のコマンドを実行してください。

```powershell
Install-Package Aspose.Cells
```

次に、C# ファイルの先頭に必要な `using` ディレクティブを追加します。

```csharp
using Aspose.Cells;
using System.Data;
using System;
```

これらのインポートにより、`Workbook`、`Worksheet`、`ExportTableOptions`、`DataTable` へアクセスでき、**Excel ワークシートの読み取り** とデータのエクスポートが可能になります。

---

## Step 2 – ワークブックの読み込み（Excel ファイルを読む）

ここで実際に **Excel ワークシートを読み込み** ます。`Workbook` コンストラクタにファイルパスを渡すだけで、Aspose.Cells が `.xlsx` と古い `.xls` の両方を自動で処理します。

```csharp
// Step 2: Load the workbook containing the data
string filePath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(filePath);
```

> **重要ポイント:** ワークブックを一度だけロードして同じ `Worksheet` オブジェクトを再利用すれば、特に大規模なスプレッドシートの場合にファイルを何度も開くよりもはるかに効率的です。

---

## Step 3 – エクスポートオプションの設定（数値書式と列名を保持）

ここで Aspose.Cells に **どのようにエクスポートするか** を指示します。`ExportTableOptions` クラスで出力を細かく調整できます。以下の 3 つのフラグを有効にします。

1. `ExportAsString = true` – すべてのセルを文字列として扱い、数値の見た目を保証します。  
2. `IncludeCellComments = true` – セルに付随するコメントもコピーします（ドキュメント化に便利）。  
3. `PreserveNumberFormat = true` – 元の数値書式（通貨記号、日付パターンなど）を保持します。

```csharp
// Step 3: Configure export options to control how the table is exported
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export all values as strings
    IncludeCellComments = true,     // Preserve any cell comments
    PreserveNumberFormat = true     // Keep the original number formatting
};
```

> **エッジケース:** `ExportAsString` を `false` にしたまま数値書式を保持しようとすると、日付が 44728 のような生数値になることがあります。両方のフラグをオンにしておくとこのサプライズを防げます。

---

## Step 4 – 最初のワークシートを取得（Excel ワークシートの読み取り）

ほとんどのシンプルなファイルは最初のシートにデータが入っています。インデックスで取得します。別シートが必要な場合は `0` を目的のゼロベースインデックスに置き換えるか、`workbook.Worksheets["SheetName"]` を使用してください。

```csharp
// Step 4: Get the first worksheet from the workbook
Worksheet firstWorksheet = workbook.Worksheets[0];
```

> **便利な理由:** ワークシートオブジェクトに直接アクセスできるため、`Cells` コレクションをフルコントロールでき、後述の **特定の行をエクスポート** が容易になります。

---

## Step 5 – セル範囲のエクスポート（特定の行をエクスポート）

チュートリアルの核心です。行 0‑49、列 0‑4（最初の 50 行と 5 列）を `DataTable` にエクスポートします。さらに、列名を `DataTable` の最初の行として含めるよう指示します。

```csharp
// Step 5: Export a range of cells (rows 0‑49, columns 0‑4) to a DataTable using the options
DataTable exportedTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 50,
    totalColumns: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

### これが行うこと

- **`startRow: 0`** – シートの最上部から開始  
- **`totalRows: 50`** – 最初の 50 行を取得（**特定の行をエクスポート**）  
- **`totalColumns: 5`** – 最初の 5 列に限定  
- **`includeColumnNames: true`** – Excel のヘッダー行と同じ列名を `DataTable` に設定し、**列名付きでエクスポート** の要件を満たす  
- **`exportOptions`** – Step 3 で設定したオプションを適用し、数値が “$1,234.56” のように表示されるようにする

---

## Step 6 – エクスポート結果の検証（出力イメージ）

コンソールに最初の数行を出力して、書式が保持されていることを確認しましょう。

```csharp
// Step 6: Display a few rows to verify the export
Console.WriteLine("=== Exported DataTable Preview ===");
foreach (DataRow row in exportedTable.Rows)
{
    // Join each column with a tab for readability
    Console.WriteLine(string.Join("\t", row.ItemArray));
}
```

**期待される出力例（例）:**

```
=== Exported DataTable Preview ===
Date        Description    Amount   Tax   Total
01/02/2024  Widget A       $120.00  $12  $132.00
01/03/2024  Widget B       $200.00  $20  $220.00
...
```

日付が `MM/dd/yyyy` 形式で表示され、通貨に `$` 記号が残っていることが確認できます—**数値書式を保持** したおかげです。

---

## よくある落とし穴と回避策

| 問題 | 発生原因 | 対策 |
|------|----------|------|
| 日付が大きな数値になる | `ExportAsString` が `false` のまま | `ExportAsString = true` を維持するか、セルを手動で変換 |
| 列ヘッダーが欠落する | `includeColumnNames` が `false` に設定されている | **列名付きでエクスポート** が必要なときは `true` にする |
| コメントが消える | `IncludeCellComments` が有効化されていない | `ExportTableOptions` で `IncludeCellComments` をオンにする |
| 間違ったシートをエクスポート | 複数シートファイルで `Worksheets[0]` を使用している | シート名を指定: `workbook.Worksheets["Data"]` |
| 範囲外例外が発生 | `totalRows` が実際の行数を超えている | `Math.Min(totalRows, worksheet.Cells.MaxDataRow + 1)` を使用 |

---

## ボーナス: シート全体をエクスポートしつつ書式を保持

後でシート全体が必要になった場合は、`totalRows` と `totalColumns` をシートの最大サイズに置き換えるだけです。

```csharp
int maxRows = firstWorksheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int maxCols = firstWorksheet.Cells.MaxDataColumn + 1;

DataTable fullTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: maxRows,
    totalColumns: maxCols,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

これで、**Excel ワークシートを読み取る** ルーチンが任意のサイズに対応し、**数値書式を保持** しつつ **列名付きでエクスポート** できるようになります。

---

## 完全動作サンプル（コピペ可能）

以下はコンソールアプリに貼り付けてそのまま実行できる完全プログラムです。すべての手順、インポート、簡易検証出力が含まれています。

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);

            // 2️⃣ Set export options (preserve number format, include comments, export as strings)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                IncludeCellComments = true,
                PreserveNumberFormat = true
            };

            // 3️⃣ Grab the first worksheet (read excel worksheet)
            Worksheet sheet = workbook.Worksheets[0];

            // 4️⃣ Export rows 0‑49, columns 0‑4 (export specific rows) with column headers
            DataTable table = sheet.Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: 50,
                totalColumns: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // 5️⃣ Show a preview
            Console.WriteLine("=== Exported DataTable Preview ===");
            foreach (DataRow row in table.Rows)
            {
                Console.WriteLine(string.Join("\t", row.ItemArray));
            }

            // Keep console open
            Console.WriteLine("\nExport complete. Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

`Program.cs` として保存し、`dotnet run` を実行すれば端末に書式付きプレビューが表示されます。

---

## まとめ

この記事では、Aspose.Cells を使って **Excel データをエクスポートする方法** を、ワークブックの読み込みから数値書式の保持、列名付きエクスポート、特定行の抽出まで一通り解説しました。コードは自己完結型で実行可能、そして最も一般的なエッジケースに対する安全策も組み込んであります。

次のステップに挑戦してみませんか？ 元の数値書式を保ったまま CSV へ直接エクスポートしたり、`DataTable` を Entity Framework Core のコンテキストに渡して一括データベース挿入を行うなど、ここで学んだ基礎を応用できます。

もし本ガイドが役に立ったら

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}