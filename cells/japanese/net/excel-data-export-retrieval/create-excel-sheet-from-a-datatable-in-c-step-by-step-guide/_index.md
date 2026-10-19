---
category: general
date: 2026-08-11
description: C#でDataTableからExcelシートを作成し、シート名を自動付与してDataTableをExcelにエクスポートします。DataTableに行を追加する方法と、ブックをxlsx形式で保存する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel sheet
- export datatable to excel
- add rows to datatable
- create multiple excel sheets
- save workbook as xlsx
language: ja
lastmod: 2026-08-11
og_description: C#でDataTableからExcelシートを作成する。このチュートリアルでは、DataTableをExcelにエクスポートする方法、DataTableに行を追加する方法、複数のExcelシートを生成する方法、そしてブックをxlsxとして保存する方法を示します。
og_image_alt: Screenshot of an Excel workbook created from a DataTable with automatically
  renamed sheets
og_title: C#でDataTableからExcelシートを作成する – 完全プログラミングガイド
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create excel sheet from a DataTable in C# and export datatable to excel
    with automatic sheet naming. Learn how to add rows to datatable and save workbook
    as xlsx.
  headline: Create excel sheet from a DataTable in C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: C#でDataTableからExcelシートを作成する – ステップバイステップガイド
url: /ja/net/excel-data-export-retrieval/create-excel-sheet-from-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# の DataTable から Excel シートを作成する – ステップバイステップ ガイド

If you need to **create excel sheet** from a `DataTable` in C#, this guide shows you exactly how to do it. You’ll see how to **export datatable to excel**, add rows, handle duplicate sheet names, and finally **save workbook as xlsx**.

The example uses Aspose.Cells, a widely‑used .NET library for Excel automation. The same concepts apply to other libraries that support SmartMarker‑style processing, but the code below works out‑of‑the‑box with Aspose.Cells 22.12 or later.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 SDK or later installed  
* A reference to the **Aspose.Cells** NuGet package (`Install-Package Aspose.Cells`)  
* Basic familiarity with `DataTable` and C# console applications  

These requirements keep the tutorial self‑contained and avoid external tooling.

## Step 1: Excel にエクスポートする DataTable を作成する

The first step is to build a `DataTable` that mirrors the data you want in the worksheet. Here we create a table named **Sheet1**, add an `Id` column, and insert two rows.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a DataTable named "Sheet1"
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // 2️⃣ Add rows to the DataTable
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);

        // Subsequent steps are called from here
        ProcessAndSaveWorkbook(dataTable);
    }
```

**この重要性:**  
`DataTable` is a convenient in‑memory representation of tabular data. Naming the table `"Sheet1"` tells Aspose.Cells which sheet to target when processing SmartMarkers.

## Step 2: Add rows to the DataTable (optional expansion)

If your source data is dynamic, you’ll often need to add rows in a loop. The following snippet demonstrates a typical pattern:

```csharp
        // Example: add rows from a collection
        int[] ids = { 3, 4, 5 };
        foreach (int id in ids)
        {
            dataTable.Rows.Add(id);
        }
```

**Tip:** When adding many rows, consider disabling constraints (`dataTable.Constraints.Clear()`) to improve performance.

## Step 3: Configure SmartMarker options to create multiple excel sheets automatically

SmartMarker options let you control how duplicate sheet names are handled. Setting `DetailSheetNewName` to `"Sheet1_{0}"` tells Aspose.Cells to rename subsequent sheets as `Sheet1_1`, `Sheet1_2`, and so on.

```csharp
    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // 3️⃣ Set SmartMarker options for automatic sheet renaming
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            // New sheets will be named Sheet1_1, Sheet1_2, etc.
            DetailSheetNewName = "Sheet1_{0}"
        };
```

**この重要性:**  
When you process several `DataTable` objects that share the same name, Excel would normally throw an error because sheet names must be unique. The `DetailSheetNewName` pattern eliminates that conflict automatically.

## Step 4: Process the SmartMarkers and export datatable to excel

Now we create a fresh `Workbook`, run `ProcessSmartMarkers`, and let Aspose.Cells populate the worksheet(s) based on the `DataTable`.

```csharp
        // 4️⃣ Create a workbook and process SmartMarkers
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);
```

**Explanation:**  
`ProcessSmartMarkers` scans the workbook for markers like `&=Sheet1!A1` (not shown here) and replaces them with the data from `dataTable`. Because we started with an empty workbook, Aspose.Cells creates a new sheet matching the table name and fills it with the rows we added.

## Step 5: Save workbook as xlsx

Finally, write the workbook to disk with the modern OpenXML format (`.xlsx`). You can change the path to suit your environment.

```csharp
        // 5️⃣ Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Result:**  
Running the program produces an Excel file that contains:

| シート名 | 行 |
|------------|------|
| Sheet1     | 1, 2, 3, 4, 5 |
| Sheet1_1   | (if another DataTable with the same name were processed) |

The sheet‑renaming logic ensures **create multiple excel sheets** without manual name management.

## Common variations and edge cases

| 状況 | 対処方法 |
|-----------|------------------|
| **非常に大きなテーブル** (≥ 100 000 行) | 処理前に `WorkbookSettings.MemorySetting = MemorySetting.MemoryOptimized` を使用して、メモリ使用量を低く抑えます。 |
| **カスタム列順序** | `ProcessSmartMarkers` を呼び出す前に、`DataTable` 内の `DataColumn` オブジェクトの順序を入れ替えます。 |
| **異なる名前の複数の DataTable** | 各テーブルに対して `ProcessSmartMarkers` を呼び出します。Aspose.Cells は自動的に名前ごとに別々のシートを作成します。 |
| **スタイル付きヘッダー行が必要** | 処理後に `Worksheet.Cells["A1"]` にアクセスし、`Style` プロパティ（フォント、背景）を適用します。 |
| **ファイルではなくストリームに保存** | `workbook.Save(outputPath, SaveFormat.Xlsx)` を `workbook.Save(stream, SaveFormat.Xlsx)` に置き換えます。 |

**Pro tip:** ファイルシステム操作は常に `try…catch` ブロックでラップし、権限問題を早期に検出できるようにします。

## Full source code (ready to copy)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create the DataTable that will be exported
        DataTable dataTable = new DataTable("Sheet1");
        dataTable.Columns.Add("Id", typeof(int));

        // Add rows – you can replace this with your own data source
        dataTable.Rows.Add(1);
        dataTable.Rows.Add(2);
        int[] extraIds = { 3, 4, 5 };
        foreach (int id in extraIds)
        {
            dataTable.Rows.Add(id);
        }

        // Process SmartMarkers and save the workbook
        ProcessAndSaveWorkbook(dataTable);
    }

    private static void ProcessAndSaveWorkbook(DataTable dataTable)
    {
        // Configure SmartMarkerOptions to rename duplicate sheets automatically
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "Sheet1_{0}"
        };

        // Create a new workbook and populate it from the DataTable
        Workbook workbook = new Workbook();
        workbook.ProcessSmartMarkers(dataTable, smartMarkerOptions);

        // Save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\DuplicateSheets.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Expected output

Running the program prints:

```
Workbook saved to YOUR_DIRECTORY\DuplicateSheets.xlsx
```

Opening `DuplicateSheets.xlsx` shows a sheet named **Sheet1** with the `Id` column containing the values `1, 2, 3, 4, 5`. If you later process another `DataTable` named `"Sheet1"` in the same workbook, Aspose.Cells will create **Sheet1_1**, **Sheet1_2**, etc., automatically.

## Conclusion

You now know how to **create excel sheet** from a `DataTable` in C#, **export datatable to excel**, **add rows to datatable**, generate **create multiple excel sheets** with automatic naming, and **save workbook as xlsx**. The complete, runnable example demonstrates the end‑to‑end workflow and provides practical tips for large data sets and custom styling.

### What’s next?

* Explore **cell formatting** (fonts, colors, borders) by accessing `Worksheet.Cells` after `ProcessSmartMarkers`.  
* Use **SmartMarker loops** to generate master‑detail reports in a single workbook.  
* Switch to **CSV export** by changing `SaveFormat.Csv` if you need a plain‑text representation.  

Feel free to adapt the code to your own data sources—whether it’s a database query, an API response, or an in‑memory collection. Happy coding!

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Aspose.Cells for .NET を使用して Excel ワークブックを ODS として作成・保存する方法](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Aspose.Cells for Java を使用して Excel ワークブックを SVG として作成・保存する方法](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Aspose.Cells Java を使用して Excel を HTML にエクスポートする方法 | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}