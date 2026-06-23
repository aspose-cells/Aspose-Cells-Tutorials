---
category: general
date: 2026-03-25
description: C#でExcelをDataTableに素早くエクスポートする方法を学びましょう。このチュートリアルでは、列名付きでExcelをエクスポートする方法と、信頼性の高いデータ処理のためにExcelデータを文字列としてエクスポートする方法を解説します。
draft: false
keywords:
- export excel to datatable
- how to export excel to datatable
- export excel with column names
- export excel data as string
language: ja
og_description: C#でExcelをDataTableにエクスポート（列名と文字列変換付き）。すぐに実行できる解決策として、この簡潔なチュートリアルをご覧ください。
og_title: C#でExcelをDataTableにエクスポート – 完全ガイド
tags:
- C#
- Aspose.Cells
- DataTable
- Excel
title: C#でExcelをDataTableにエクスポートする – ステップバイステップガイド
url: /ja/net/excel-data-import-export/export-excel-to-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でExcelをDataTableにエクスポートする – ステップバイステップガイド

Ever needed to **export Excel to DataTable** but weren’t sure which flags to flip? You’re not alone—many developers hit the same wall when they first try to pull spreadsheet data into a `DataTable`.  

良いニュースです。数行のコードで **列名付きでExcelをエクスポート** でき、さらに **Excelデータを文字列としてエクスポート** して型不一致の問題を回避できます。以下に完全な実行可能サンプルと各設定の「理由」を示すので、推測せずにどのプロジェクトにも適用できます。

## このチュートリアルでカバーする内容

* メモリ上にワークブックを作成する方法（実際のファイルは不要）。  
* サンプル行をいくつか入力し、結果をすぐに確認できるようにする。  
* `ExportTableOptions` を設定して、すべてのセルを文字列として扱う。  
* 矩形範囲を `DataTable` にエクスポートし、最初の行を列ヘッダーとして保持する。  
* 出力を検証し、最初の行をコンソールに出力する。  

外部ドキュメントへのリンクは不要です—必要なものはすべてここにあります。ディスク上に既にExcelファイルがある場合は、ワークブック作成行を `new Workbook("path/to/file.xlsx")` に置き換えるだけで使用できます。

## ステップ 1: プロジェクトのセットアップと Aspose.Cells NuGet パッケージの追加

コードを書く前に、プロジェクトが **Aspose.Cells for .NET**（`Workbook` クラスを提供するライブラリ）を参照していることを確認してください。NuGet パッケージマネージャーから追加できます。

```bash
dotnet add package Aspose.Cells
```

> **プロのコツ:** 最新の安定版（2026年3月時点では 22.12）を使用すると、最新のバグ修正とパフォーマンス向上が得られます。

## ステップ 2: ワークブックを作成し、サンプルデータで埋める

まず新しい `Workbook` を作成し、数行を書き込んでエクスポートの動作を確認します。このステップは、ソースデータがメモリ上にのみ存在する場合の **how to export excel to datatable** のデモでもあります。

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();                 // in‑memory workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Populate a few cells – this mimics a real Excel file
        worksheet.Cells["A1"].PutValue("Name");   // column header
        worksheet.Cells["B1"].PutValue("Age");    // column header
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);
```

*この重要性:* ヘッダー行を最初に挿入することで（`A1` & `B1`）、後でエクスポーターに最初の行を列名として扱うよう指示できます—これが **export excel with column names** の意味です。

## ステップ 3: Aspose.Cells にすべてのセルを文字列として扱うよう指示する

数値や日付のセルをエクスポートすると、Aspose は .NET の型を推測しようとします。下流のコードが文字列を期待している場合、微妙なバグが発生する可能性があります。`ExportTableOptions.ExportAsString` フラグは、統一された文字列変換を強制します。

```csharp
        // 3️⃣ Configure export options – all values will be strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true       // <-- ensures Export Excel Data As String
        };
```

*なぜこれを使うのか？* 時々数値、時々文字列が混在する列（例: “00123” と “ABC”）を想像してください。すべて文字列としてエクスポートすることで、先頭のゼロが失われたり型変換例外が発生したりするのを防げます。

## ステップ 4: 必要な範囲を DataTable にエクスポートする

いよいよ **export excel to datatable** を実行します。`ExportDataTable` メソッドは開始行/列、行数/列数、列名抽出フラグ、そして先ほど作成したオプションを受け取ります。

```csharp
        // 4️⃣ Export rows 0‑9 and columns 0‑4 (adjust as needed)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,   // <-- uses the first row as headers
            exportOptions: exportOptions);
```

*内部で何が起きているか？*  
- `startRow: 0` は最初の Excel 行（ヘッダー行）を指します。  
- `exportColumnNames: true` は Aspose に “Name” と “Age” を `DataTable` の列コレクションに取り込むよう指示します。  
- `totalRows`/`totalColumns` は実際のデータより大きくても構いません；余分なセルは `ExportAsString` のため空文字列になります。

## ステップ 5: 結果の検証 – 最初の行を出力する

簡単なコンソール出力で、変換が成功し列名が保持されていることが確認できます。

```csharp
        // 5️⃣ Show the first data row (if any)
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

**期待される出力**

```
First row: Alice, 30
```

サンプルデータを変更すれば、コンソールは自動的にその変更を反映します—追加のコードは不要です。

## よくある質問とエッジケース

| Question | Answer |
|----------|--------|
| **ディスク上に既に存在するシートをエクスポートできますか？** | はい。`new Workbook()` を `new Workbook("myFile.xlsx")` に置き換えるだけです。残りの手順は同じです。 |
| **Excelファイルに結合セルがある場合はどうなりますか？** | 結合セルは解除され、左上のセルの値が結合範囲全体に使用されます。 |
| **ロケール固有の数値形式を気にする必要がありますか？** | `ExportAsString = true` の場合は心配不要です。すべてはExcelに表示されているそのままの文字列として取得されます。 |
| **一度にエクスポートできる行数はどれくらいですか？** | Aspose.Cells は数百万行を処理できますが、`DataTable` のサイズに比例してメモリ使用量が増加します。制限に達した場合はページングを検討してください。 |
| **非表示列はどうなりますか？** | `ExportTableOptions` で `ExportHiddenColumns = false` と設定しない限り、非表示列もエクスポートされます。 |

## ボーナス: DataTable の代わりに CSV にエクスポートする

場合によってはフラットファイルが好ましいことがあります。同じ `ExportTableOptions` を `ExportDataTableToCSV` と組み合わせて再利用できます。

```csharp
        string csvPath = "output.csv";
        worksheet.Cells.ExportDataTableToCSV(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            csvPath,
            exportColumnNames: true,
            exportOptions);
        Console.WriteLine($"CSV written to {csvPath}");
```

このワンライナーで、**excelデータを文字列としてエクスポート**しつつ、すぐにインポート可能な CSV が得られます。

## 完全動作サンプル（コピー＆ペースト可能）

プログラムを実行（`dotnet run`）すると、コンソールに **export excel to datatable** の結果が表示されます。サンプルデータを差し替えたり、`totalRows`/`totalColumns` を変更したり、ワークブックを実際のファイルに指すようにすれば、すべてスケールします。

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate sample data (header + two rows)
        worksheet.Cells["A1"].PutValue("Name");
        worksheet.Cells["B1"].PutValue("Age");
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);

        // Export everything as strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true
        };

        // Export range to DataTable (first row = column names)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,
            exportOptions: exportOptions);

        // Display first row
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

## 結論

これで C# における **Excel を DataTable にエクスポートする完全な自己完結型ソリューション** が手に入りました。`ExportTableOptions.ExportAsString` を設定することで **excelデータを文字列としてエクスポート** が保証され、`exportColumnNames: true` を設定すれば、**列名付きでExcelをエクスポート** するときに期待する慣れ親しんだ列ヘッダーが取得できます。  

ここからは以下のように活用できます：

* `DataTable` を Entity Framework や Dapper に渡して一括挿入する。  
* `FastReport` や **RDLC** などのレポートエンジンに渡す。  
* API 応答用に JSON に変換する（`JsonConvert.SerializeObject(table)`）。

自由に試してみてください—例えば、より大きなシートをエクスポートしたり、ネットワーク共有から **how to export excel to datatable** と組み合わせたりできます。パターンは変わらず、コードは本番環境でも使用可能です。

![Excel → DataTable 変換フローの図 – export excel to datatable](https://example.com/placeholder.png "export excel to datatable diagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}