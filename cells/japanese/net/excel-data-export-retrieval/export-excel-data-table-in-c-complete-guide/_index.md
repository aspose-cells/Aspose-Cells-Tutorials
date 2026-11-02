---
category: general
date: 2026-03-21
description: Aspose.Cells を使用して、ヘッダー付きの Excel データテーブルを DataTable にエクスポートし、小数点以下の桁数を制限し、最初の
  100 行だけをエクスポートする。
draft: false
keywords:
- export excel data table
- export excel to datatable
- limit decimal places excel
- export first 100 rows
- export excel with headers
language: ja
og_description: C#でExcelのデータテーブルをDataTableにエクスポートし、ヘッダーを保持し、小数点以下の桁数を制限し、最初の100行を取得する方法を学びましょう。
og_title: C#でExcelデータテーブルをエクスポートする – ステップバイステップガイド
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: C#でExcelデータテーブルをエクスポートする完全ガイド
url: /ja/net/excel-data-export-retrieval/export-excel-data-table-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Excel Data Table – Full C# Walkthrough

Need to **export excel data table** from a workbook into a .NET `DataTable`? You're in the right place—this guide shows you exactly how to do it, keep the column headers, limit decimal places, and pull only the first 100 rows.  

If you’ve ever stared at a spreadsheet and thought, “How do I get this into my app without losing formatting?” you’re not alone. In the next few minutes we’ll turn that “what‑if” into a concrete, copy‑and‑paste solution that works with Aspose.Cells, a popular library for Excel manipulation.

## What You’ll Learn

- How to **export excel to datatable** using the `ExportDataTable` method.  
- How to keep the original column names (`export excel with headers`).  
- How to **limit decimal places excel** values by configuring `ExportTableOptions`.  
- How to safely retrieve only the top‑100 rows (`export first 100 rows`).  

No external scripts, no magic strings—just plain C# that you can drop into any .NET project.

## Prerequisites

| 要件 | 重要な理由 |
|------|------------|
| .NET 6 以降（または .NET Framework 4.7+） | Aspose.Cells は両方をサポートしていますが、最新のランタイムは async 対応 API を提供します。 |
| Aspose.Cells for .NET NuGet パッケージ | `Workbook`、`ExportTableOptions`、`ExportDataTable` ヘルパーを提供します。 |
| サンプル Excel ファイル（例: `Numbers.xlsx`） | エクスポートするデータの元になります。 |
| 基本的な C# 知識 | コードスニペットに沿って進めますが、特別な知識は不要です。 |

If any of those sound unfamiliar, grab the NuGet package with `dotnet add package Aspose.Cells` and create a tiny Excel file with a few numbers—your test data.

![export excel data table example](excel-data-table.png "Screenshot of an Excel sheet that will be exported to a DataTable")

## Step 1: Load the Workbook (export excel data table)

The very first thing you need is a `Workbook` instance that points to your Excel file. Think of it as opening a book before you can read any chapters.

```csharp
using Aspose.Cells;

// 1️⃣ Load the workbook that contains the source data
Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");
```

> **Why this matters:** Loading the workbook gives you access to its worksheets, cells, and styles. If the file path is wrong, Aspose will throw a `FileNotFoundException`, so double‑check the location.

## Step 2: Configure Export Options – limit decimal places excel

By default Aspose exports every numeric value with full precision. Often you only need a handful of significant digits, especially when feeding the data into a UI grid or an API that expects rounded numbers.

```csharp
using Aspose.Cells;

// 2️⃣ Configure export options – keep only 4 significant digits
ExportTableOptions exportOptions = new ExportTableOptions
{
    // This property trims the number of significant digits.
    SignificantDigits = 4
};
```

> **Pro tip:** If you need a different rounding strategy (e.g., always round up), you can post‑process the `DataTable` after export. The `SignificantDigits` setting is the quickest way to **limit decimal places excel** without writing extra loops.

## Step 3: Export the Desired Range (export first 100 rows)

Now we tell Aspose which block of cells we want to pull into a `DataTable`. In this tutorial we grab the first 100 rows and the first 10 columns, but you can adjust those numbers to fit your scenario.

```csharp
using System.Data;
using Aspose.Cells;

// 3️⃣ Export a block of cells (first 100 rows × 10 columns) to a DataTable
DataTable dataTable = workbook.Worksheets[0].Cells.ExportDataTable(
    startRow: 0,          // zero‑based index, first row
    startColumn: 0,       // first column (A)
    totalRows: 100,       // export only the first 100 rows
    totalColumns: 10,     // and the first 10 columns
    exportColumnNames: true, // keep column headers (export excel with headers)
    options: exportOptions);
```

> **Edge case:** If the sheet contains fewer than 100 rows, Aspose will simply export what exists without throwing an error. However, you might want to guard against an unexpectedly small range:

```csharp
int rowsToExport = Math.Min(100, workbook.Worksheets[0].Cells.MaxDataRow + 1);
```

## Step 4: Verify the Result – Quick Console Dump

Seeing the data in your debugger is nice, but printing a few rows to the console confirms that the **export excel to datatable** actually worked and that the decimal places are trimmed.

```csharp
static void PrintDataTable(DataTable table)
{
    foreach (DataRow row in table.Rows)
    {
        foreach (var item in row.ItemArray)
            Console.Write($"{item}\t");
        Console.WriteLine();
    }
}

// Call the helper
PrintDataTable(dataTable);
```

### Expected Output

```
ID      Name    Score   Ratio   Date        ...
1       Alice   95.12   0.8234  2023-01-15  ...
2       Bob     88.5    0.7612  2023-01-16  ...
3       Carol   73.33   0.6721  2023-01-17  ...
...
```

Notice how the numeric columns now show only four significant digits, matching the `SignificantDigits = 4` setting we applied earlier.

## Step 5: Wrap It All Up – A Complete, Runnable Example

Below is the full program you can copy‑paste into a console app. It includes error handling, the optional row‑count guard, and the helper method for printing.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class ExportExcelDemo
{
    static void Main()
    {
        try
        {
            // 👉 Load the workbook
            Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");

            // 👉 Set up export options (limit decimal places excel)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                SignificantDigits = 4
            };

            // 👉 Determine safe row count (export first 100 rows)
            int maxRows = workbook.Worksheets[0].Cells.MaxDataRow + 1;
            int rowsToExport = Math.Min(100, maxRows);

            // 👉 Export to DataTable (export excel to datatable, export excel with headers)
            DataTable dt = workbook.Worksheets[0].Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: rowsToExport,
                totalColumns: 10,
                exportColumnNames: true,
                options: exportOptions);

            // 👉 Show a glimpse of the data
            PrintDataTable(dt);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }

    static void PrintDataTable(DataTable table)
    {
        foreach (DataRow row in table.Rows)
        {
            foreach (var item in row.ItemArray)
                Console.Write($"{item}\t");
            Console.WriteLine();
        }
    }
}
```

Run the program, and you’ll see the first 100 rows of your sheet, nicely rounded, with column names intact.

## Common Questions & Gotchas

| 質問 | 回答 |
|------|------|
| **シートに結合セルがある場合はどうなりますか？** | `ExportDataTable` は結合セルを左上のセルの値で平坦化します。カスタム処理が必要な場合は、先に結合を解除するか、生の `Cell` オブジェクトを読み取ってください。 |
| **`DataSet` にエクスポートすることはできますか？** | はい—`ExportDataTable` を使用します |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}