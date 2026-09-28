---
category: general
date: 2026-03-18
description: C#でExcelデータをDataTableにエクスポートする方法（特定のセルを処理し、ExcelをDataTableに変換し、数値をフォーマットするコード）。特定のセルのエクスポートやその他のテクニックを学びましょう。
draft: false
keywords:
- how to export excel
- convert excel to datatable
- export specific cells
- excel to datatable c#
- excel range to datatable
language: ja
og_description: C#でExcelデータをDataTableにエクスポートする方法。このチュートリアルでは、特定のセルをエクスポートし、ExcelをDataTableに変換し、数値を簡単にフォーマットする方法を紹介します。
og_title: C#でExcelをDataTableにエクスポートする方法 – 完全ガイド
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: C#でExcelをDataTableにエクスポートする方法 – ステップバイステップガイド
url: /ja/net/excel-data-import-export/how-to-export-excel-to-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel を DataTable にエクスポートする方法（C#） – ステップバイステップ ガイド

**Excel をエクスポート** して `DataTable` に変換する際、書式を失わない方法を考えたことはありませんか？ あなただけではありません。開発者はレポート作成、検証、または一括挿入処理のために、スプレッドシートの一部をメモリに取り込む必要があります。良いニュースは、数行の C# コードで、正確な範囲（例: *A1:F11*）をエクスポートし、すべてのセルを文字列として扱い、さらにカスタム数値書式を適用できることです。

このチュートリアルでは、ブックの読み込み、**特定セルのエクスポート** の設定、範囲を `DataTable` に変換する方法、空行やロケール依存の数値といったエッジケースの処理まで、必要なすべてを網羅します。最後まで読むと、実運用コードで **excel to datatable c#** シナリオに対応できる再利用可能なメソッドが手に入ります。

> **前提条件** – Aspose.Cells for .NET ライブラリ（または `ExportDataTable` を提供する類似 API）が必要です。例は .NET 6+ を想定していますが、概念は以前のバージョンでも適用できます。

---

## 学べること

- Aspose.Cells を使用した **Excel から DataTable への変換** 方法
- すべての値を文字列として扱いながらカスタム範囲（`excel range to datatable`）をエクスポートする方法
- エクスポート時に小数点以下2桁の数値書式（`#,#00.00`）を適用する方法
- よくある落とし穴（null 行、非表示列）と回避策
- コピーしてすぐに実行できる完全なコードサンプル

---

## 前提条件とセットアップ

コードに入る前に、以下を用意してください。

1. **Aspose.Cells for .NET** を NuGet 経由でインストール：

   ```bash
   dotnet add package Aspose.Cells
   ```

2. `input.xlsx` という名前の Excel ファイルを、参照可能なフォルダーに配置（例: `YOUR_DIRECTORY/input.xlsx`）。
3. .NET 6 以上を対象としたプロジェクト（下記の `using` 文はそのまま使用可能）。

> **プロのコツ:** 別のライブラリ（例: EPPlus や ClosedXML）を使用する場合でも概念は同じです。ブックを読み込み、範囲を選択し、`DataTable` を返すメソッドを呼び出すだけです。

---

## 手順 1: ワークブックを読み込み、最初のワークシートを取得

まずは Excel ファイルを表す `Workbook` オブジェクトが必要です。取得できたら、インデックスまたは名前で任意のワークシートにアクセスできます。

```csharp
using Aspose.Cells;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];

            // Continue with export options...
        }
    }
}
```

**なぜ重要か:** 早い段階でワークブックを読み込むことで、非表示シートや保護状態など構造を確認できます。ファイルが大きい場合は `LoadOptions` を使って必要な部分だけをストリームすることを検討してください。

---

## 手順 2: エクスポートオプションを設定 – すべての値を文字列として扱う

下流処理（例: SQL への一括挿入）のためにデータをエクスポートする際、**一貫した文字列表現** が欲しいことが多いです。これにより型不一致エラーを防げます。

```csharp
// Configure export behavior
ExportTableOptions exportOptions = new ExportTableOptions
{
    // Force every cell to be returned as a string, regardless of its original type
    ExportAsString = true,

    // Apply a two‑decimal‑place format to numeric cells
    NumberFormat = "#,##0.00"
};
```

**説明:**  
- `ExportAsString = true` は Aspose.Cells に対し、セルの元の型を無視して書式設定済みテキストを返すよう指示します。  
- `NumberFormat = "#,##0.00"` は `1234.5` のような数値を `"1,234.50"` に変換し、財務レポートで便利です。

元のデータ型が必要な場合は `ExportAsString` を `false` に設定し、後で自分で変換してください。

---

## 手順 3: 特定範囲（A1:F11）を DataTable にエクスポート

ここが **特定セルのエクスポート** の核心です。`ExportDataTable` メソッドは開始/終了行・列インデックス（0 ベース）とヘッダー含有フラグを受け取ります。

```csharp
// Export cells A1:F11 (rows 0‑10, columns 0‑5) including the header row
DataTable table = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    endRow: 10,
    endColumn: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

**得られるもの:** ヘッダーを含む 11 行、6 列（`A`‑`F`）の `DataTable` が生成されます。すべての値は `exportOptions` に従った文字列としてフォーマットされています。

---

## 手順 4: 結果を検証 – コンソールに出力

テーブルを別コンポーネントに渡す前に、出力を確認することをお勧めします。

```csharp
// Simple console dump
foreach (DataRow row in table.Rows)
{
    foreach (var item in row.ItemArray)
    {
        Console.Write($"{item}\t");
    }
    Console.WriteLine();
}
```

以下のような結果が表示されるはずです：

```
Id      Name        Qty     Price   Total   Date
1       Widget A    10      2.50    25.00   2026-01-01
2       Widget B    5       3.75    18.75   2026-01-02
...
```

数値列が指定通り小数点以下2桁で表示されていることに注目してください。

---

## 完全動作サンプル（コピー＆ペースト可能）

以下は全体をまとめたプログラムです。新しいコンソールプロジェクトに貼り付け、ファイルパスを調整して実行すれば、追加設定は不要です。

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load workbook and select worksheet
            // -------------------------------------------------
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -------------------------------------------------
            // 2️⃣ Set export options – strings + number format
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                NumberFormat = "#,##0.00"
            };

            // -------------------------------------------------
            // 3️⃣ Export range A1:F11 (rows 0‑10, cols 0‑5)
            // -------------------------------------------------
            DataTable table = worksheet.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                endRow: 10,
                endColumn: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // -------------------------------------------------
            // 4️⃣ Output to console for verification
            // -------------------------------------------------
            Console.WriteLine("=== Exported DataTable ===");
            foreach (DataRow row in table.Rows)
            {
                foreach (var cell in row.ItemArray)
                {
                    Console.Write($"{cell}\t");
                }
                Console.WriteLine();
            }

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**コードから得られる主なポイント:**

- `ExportTableOptions` オブジェクトは再利用可能です。複数範囲をエクスポートする場合は同じインスタンスを渡せます。  
- インデックスは **0** から始まるため、`A1` は `(0,0)` に相当します。  
- `includeColumnNames` を `true` にすると、最初の行が自動的に列ヘッダーとして使用され、下流の `DataTable` 操作が楽になります。

---

## エッジケースとよくある質問

### ワークシートに非表示行や列がある場合は？

Aspose.Cells はデフォルトで可視性を尊重します。非表示データもエクスポートしたい場合は `exportOptions.ExportHiddenRows = true` と `ExportHiddenColumns = true` を設定してください。

### Excel に数式が含まれている場合、計算結果が取得できますか？

はい。デフォルトでは `ExportDataTable` は **表示値**（数式の結果）を返します。数式そのもののテキストが欲しい場合は `exportOptions.ExportFormulas = true` を設定してください。

### 完全に空の行はスキップできますか？

エクスポート後に `DataTable` を整理できます：

```csharp
foreach (DataRow row in table.Rows.Cast<DataRow>()
                                   .Where(r => r.ItemArray.All(c => c == DBNull.Value || string.IsNullOrWhiteSpace(c.ToString()))).ToList())
{
    table.Rows.Remove(row);
}
```

### 非連続範囲（例: A1:B5 と D1:E5）をエクスポートできますか？

Aspose.Cells は単一呼び出しで不連続範囲をサポートしていません。代わりに各ブロックを個別にエクスポートし、結果の `DataTable` を手動で結合してください。

---

## パフォーマンス向上のヒント

- **`ExportTableOptions` を再利用** すると、複数回のエクスポートでもインスタンス生成コストが削減され、コードがすっきりします。  
- **`LoadOptions` で大容量ファイルをストリーム** し、ワークブック全体をメモリに読み込むのを回避してください。  
- **大量シートの場合は `DataTable` を避ける** のも一策です。`ExportDataTable` は便利ですが、CSV への即時エクスポートの方がメモリ効率が高いことがあります。

---

## 結論

**Excel を DataTable にエクスポート** する方法を、書式制御、特定セル範囲の処理、すべての値を文字列として取得する点に焦点を当てて解説しました。完全なサンプルは、**convert excel to datatable**、**export specific cells**、あるいは **excel range to datatable** といったシナリオに適用できる、クリーンで本番環境向けのアプローチを示しています。

ぜひ試してみてください：範囲を変更したり、`ExportAsString` を切り替えたり、`DataTable` を直接 Entity Framework に渡して一括挿入したり。基盤ができれば、可能性は無限に広がります。

### 次のステップと関連トピック

- **DataTable を Excel にインポート** – `ImportDataTable` を使った逆操作を学びましょう。  
- **DataTable を SQL Server に一括挿入** – `SqlBulkCopy` で超高速ロードを実現。  
- **EPPlus や ClosedXML の活用** – 代替ライブラリで同様のタスクを実装する方法を比較。  
- **エクスポート時のセル書式設定** – `ExportTableOptions` の日付書式やカスタムカルチャ設定など、さらに高度なオプションを探求してください。

質問や別のユースケースがあればコメントで教えてください。会話を続けましょう。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}