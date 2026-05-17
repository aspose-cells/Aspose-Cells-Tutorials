---
category: general
date: 2026-03-22
description: カスタム数値形式のExcelチュートリアル：データテーブルをExcelにインポートし、列の背景色を設定し、列を通貨形式にフォーマットし、ブックをxlsxとして保存する方法を示す。
draft: false
keywords:
- custom number format excel
- import datatable to excel
- set column background color
- format column as currency
- save workbook as xlsx
language: ja
og_description: DataTableのインポート、列の背景色設定、列を通貨形式に書式設定し、ブックをxlsxとして保存するまでを順に解説するカスタム数値書式Excelチュートリアルです。
og_title: C#でExcelのカスタム数値書式 – ステップバイステップガイド
tags:
- C#
- Excel automation
- Aspose.Cells
- Data export
title: C#でExcelのカスタム数値書式 – 完全ガイド
url: /ja/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# カスタム数値形式 Excel – フルスタック C# チュートリアル

C# から直接 **custom number format excel** スタイルを適用したことはありますか？DataTable をスプレッドシートにダンプしたら、数字はそのままで色も通貨書式も付いていない…という経験はありませんか。これは特にステークホルダー向けに洗練されたレポートが必要なときに痛いポイントです。

このガイドではその問題を一緒に解決します。**import datatable to excel**、**set column background color**、**format column as currency**、そして **save workbook as xlsx** を、カスタム数値形式で数字を際立たせる方法を学びます。曖昧な説明はなく、プロジェクトにコピペできる完全な実装例を提供します。

---

## What You’ll Build

このチュートリアルの最後までに、以下を実現する単体の C# コンソール アプリが完成します。

1. `DataTable` を取得します（スタブは任意のクエリに置き換え可能）。  
2. Aspose.Cells（または互換ライブラリ）を使って新しい Excel ワークブックを作成します。  
3. 1 列目に青の太字フォント、2 列目に薄黄色の背景、3 列目に通貨書式（`$#,##0.00`）を適用します。  
4. 任意のフォルダーに `DataTableWithStyleArray.xlsx` として保存します。

各行が最終的な Excel ファイルにどのように影響するかを丁寧に解説し、保守性とパフォーマンスの観点から選択理由を説明します。

---

## Prerequisites

- .NET 6.0 以上（.NET Framework 4.7+ でも動作します）。  
- Aspose.Cells for .NET（無料トライアルまたはライセンス版）。NuGet でインストール：

```bash
dotnet add package Aspose.Cells
```

- `DataTable` と C# コンソール アプリケーションの基本的な知識。

---

## Step 1: Retrieve the Source Data as a DataTable

まず、エクスポートするデータが必要です。実務ではリポジトリを呼び出すか SQL クエリを実行するでしょう。ここではメモリ上にシンプルなテーブルを作成します。

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetSampleData()
{
    var table = new DataTable("Sales");
    table.Columns.Add("Product", typeof(string));
    table.Columns.Add("Quantity", typeof(int));
    table.Columns.Add("Revenue", typeof(decimal));

    table.Rows.Add("Widget A", 120, 3450.75m);
    table.Rows.Add("Widget B", 85, 2190.00m);
    table.Rows.Add("Widget C", 60, 1580.40m);

    return table;
}
```

> **Why this matters:** `DataTable` を使用すると、スキーマ情報を持った表形式のデータソースが得られ、Excel の行・列にきれいにマッピングできます。また、同じエクスポートロジックをデータセット全体で再利用でき、コードの重複を防げます。

---

## Step 2: Create a New Workbook and Grab the First Worksheet

次に Excel ワークブックを作成します。`Workbook` クラスがファイル全体を表し、`Worksheets[0]` がデフォルトシートとしてデータを書き込む対象になります。

```csharp
// Initialize a fresh workbook
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet
Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** 複数シートが必要な場合は `workbook.Worksheets.Add("SheetName")` を呼び出し、各シートに対して同様のスタイリング手順を繰り返してください。

---

## Step 3: Define Column Styles – Font, Background, and Number Format

Aspose.Cells のスタイリングは `Style` オブジェクトで行います。ここでは DataTable の各列に対応する配列を作成します。

```csharp
// Prepare an array to hold three distinct styles
Style[] columnStyles = new Style[3];

// 1️⃣ First column – blue, bold font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = System.Drawing.Color.Blue;
columnStyles[0].Font.IsBold = true;

// 2️⃣ Second column – light‑yellow background
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
columnStyles[1].Pattern = BackgroundType.Solid;

// 3️⃣ Third column – custom currency format (custom number format excel)
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Custom = "$#,##0.00";
```

> **Why a style array?** `ImportDataTable` に配列を渡すことで、1 回の呼び出しで列ごとに異なるスタイルを適用でき、コードが簡潔になるだけでなくパフォーマンスも向上します。データ順序と書式が常に同期することが保証されます。

---

## Step 4: Import the DataTable While Applying the Styles

操作の核心です。`DataTable` をワークシートにインポートし、ヘッダー行を含め、先ほど作成した `columnStyles` 配列を渡します。

```csharp
// Import data starting at cell A1 (row 0, column 0)
worksheet.Cells.ImportDataTable(
    GetSampleData(),   // source DataTable
    true,              // include column names as header
    0, 0,              // start row, start column
    columnStyles);     // apply the style array
```

> **What happens under the hood?** Aspose は各列を走査し、まずヘッダーを書き込み、続いて各行の値を書き込みます。その過程で配列から対応する `Style` を適用するため、たとえば「Product」列は青いヘッダー、「Quantity」列は黄色背景、「Revenue」列は通貨書式で出力されます。

---

## Step 5: Save the Workbook as an XLSX File

最後にワークブックをディスクに保存します。`Save` メソッドはファイル拡張子から自動的に XLSX 形式を選択します。

```csharp
// Choose a folder that exists on your machine
string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";

// Ensure the directory exists (optional safety check)
System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);

// Save the workbook
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

> **Tip:** Web API などでストリームとして返す場合は、`workbook.Save(stream, SaveFormat.Xlsx)` を使用し、ファイルパスではなくストリームを指定してください。

---

## Full Working Example

以下は新規コンソール プロジェクトに貼り付けてそのままビルド・実行できる完全なプログラムです。

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Get data
            DataTable dataTable = GetSampleData();

            // Step 2 – Create workbook & worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 3 – Prepare column styles
            Style[] columnStyles = new Style[3];

            // Font style for first column (blue, bold)
            columnStyles[0] = workbook.CreateStyle();
            columnStyles[0].Font.Color = System.Drawing.Color.Blue;
            columnStyles[0].Font.IsBold = true;

            // Background style for second column (light yellow)
            columnStyles[1] = workbook.CreateStyle();
            columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
            columnStyles[1].Pattern = BackgroundType.Solid;

            // Currency format for third column (custom number format excel)
            columnStyles[2] = workbook.CreateStyle();
            columnStyles[2].Custom = "$#,##0.00";

            // Step 4 – Import data with styles
            worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

            // Step 5 – Save as XLSX
            string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";
            System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }

        // Helper method to build a demo DataTable
        static DataTable GetSampleData()
        {
            var table = new DataTable("Sales");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Revenue", typeof(decimal));

            table.Rows.Add("Widget A", 120, 3450.75m);
            table.Rows.Add("Widget B", 85, 2190.00m);
            table.Rows.Add("Widget C", 60, 1580.40m);

            return table;
        }
    }
}
```

### Expected Result

`DataTableWithStyleArray.xlsx` を開くと次のように表示されます。

| **Product** (青・太字) | **Quantity** (薄黄色) | **Revenue** (通貨) |
|------------------------|------------------------|--------------------|
| Widget A               | 120                    | $3,450.75          |
| Widget B               | 85                     | $2,190.00          |
| Widget C               | 60                     | $1,580.40          |

指定した **custom number format excel** (`$#,##0.00`) により、すべての収益セルがドル記号、千位区切り、2 桁の小数点で表示され、財務チームが期待する形式になります。

---

## Frequently Asked Questions & Edge Cases

### Can I use this with a different Excel library?

もちろんです。スタイルを列ごとに作成しインポート時に適用するという考え方は、EPPlus、ClosedXML、NPOI でも同様に活用できます。API 呼び出しは異なりますがパターンは変わりません。

### What if my DataTable has more columns than styles?

Aspose は `columnStyles` 配列に対応するエントリがない列に対してデフォルトスタイルを適用します。予期せぬ書式になるのを防ぐには、配列のサイズを `dataTable.Columns.Count` に合わせるか、ループで動的にスタイルを生成してください。

### How do I set a custom number format for dates?

`style.Custom = "dd‑mm‑yyyy"` のように設定すれば OK です。日付、パーセンテージ、指数表記など、任意の Excel 書式文字列に対して同じ配列ベースのアプローチが使えます。

### Is there a way to auto‑size columns after import?

あります。インポート後に `worksheet.AutoFitColumns();` を呼び出すだけで、セル内容に基づいた最適幅が自動計算されます。

### What about large data sets (100k+ rows)?

`ImportDataTable` は大量データ向けに最適化されていますが、メモリ上限に達する可能性があります。その場合は `Cells[i, j].PutValue(...)` で行単位にストリーミングし、単一の `Style` オブジェクトを再利用してオーバーヘッドを削減する方法を検討してください。

---

## Pro Tips & Common Pitfalls

- **パスのハードコーディングは避ける**：本番コードでは `Environment.GetFolderPath` や設定ファイルから取得してください。  
- **Workbook の破棄**：長時間稼働するサービスでは `using` ブロックでラップし、ネイティブリソースを確実に解放しましょう。  
- **ロケール依存の区切り文字に注意**：`$#,##0.00` は OS のロケールに関係なく小数点はピリオド、千位区切りはカンマになります。金融レポートでは通常これが望ましいです。  
- **System.Drawing の参照**：スタイリングで使用する色構造体のために `System.Drawing`（.NET Core では `System.Drawing.Common`）を参照に追加してください。  
- **Excel のバージョン差異**：古いバージョンの Excel では一部カスタム書式の解釈が若干異なることがあります。必ず複数バージョンで出力を確認しましょう。

---

## Conclusion

C# から **custom number format excel** ファイルを作成するために必要なすべてを網羅しました：`DataTable` からデータ取得、**import datatable to excel**、**set column background color**、**format column as currency**、そして最終的に **save workbook as x**（続きはコード例をご参照ください）。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}