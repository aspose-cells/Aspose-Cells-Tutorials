---
category: general
date: 2026-02-09
description: C#で薄い青色の背景を持つワークブックを作成し、ヘッダー付きでデータをインポートする方法。薄い青色の背景の追加、Excelのデフォルトスタイルの使用、DataTable
  のインポートを学びます。
draft: false
keywords:
- how to create workbook
- add light blue background
- import data with headers
- excel import datatable c#
- use default style excel
language: ja
og_description: C#で薄い青色の背景を持つワークブックを作成し、ヘッダー付きデータをインポートし、デフォルトのExcelスタイルを適用する方法—すべてを簡潔にまとめたガイド。
og_title: ワークブックの作成方法 – ライトブルーの背景、データインポート
tags:
- C#
- Excel
- Aspose.Cells
title: ワークブックの作成方法 – ライトブルーの背景、データインポート
url: /ja/net/excel-data-import-export/how-to-create-workbook-light-blue-background-data-import/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ワークブックの作成方法 – ライトブルー背景、データインポート

Ever wondered **how to create workbook** in C# that looks a little prettier straight out of the box? Maybe you’ve pulled a `DataTable` from a database and you’re tired of the bland, default‑white cells. In this tutorial we’ll walk through creating a new workbook, adding a light‑blue background to a column, and importing data with headers—all while using the default style Excel provides.

私たちは、null 値の処理や複数列のカスタマイズといった「what‑if」シナリオも少し紹介します。最後まで読めば、ステークホルダーにそのまま提供できる、完全にスタイルが適用された Excel ファイルが手に入ります。

## 前提条件

Before we dive in, make sure you have:

* **.NET 6+** (the code works on .NET Framework 4.6+ as well)  
* **Aspose.Cells for .NET** – the library that powers the `Workbook`, `Style`, and `ImportDataTable` calls. Install it via NuGet:  

  ```bash
  dotnet add package Aspose.Cells
  ```

* A `DataTable` source – we’ll fake one in the example, but you can replace it with any ADO.NET query.

Got those? Great, let’s get started.

## ステップ 1: 新しいワークブックを初期化する (Primary Keyword)

The first thing you need to do is **how to create workbook** – literally. The `Workbook` class represents the entire Excel file, and its constructor gives you a clean slate.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

namespace ExcelStylingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or obtain an existing one)
            Workbook workbook = new Workbook();   // <-- this is how to create workbook
```

> **この重要性:** Fresh な `Workbook` から始めることで、最初からすべてのスタイルをコントロールできます。既存のファイルを開くと、元の作者が残したスタイルを継承してしまい、フォーマットが一貫しなくなる可能性があります。

## ステップ 2: インポートする DataTable の準備

For the sake of illustration, let’s spin up a simple `DataTable`. In real‑world scenarios you’d probably call a stored procedure or an ORM method.

```csharp
            // Step 2: Retrieve the data you want to import (e.g., from a database)
            DataTable dataTable = GetSampleData(); // replace with your own GetData()
```

```csharp
        // Helper method that returns a dummy DataTable
        static DataTable GetSampleData()
        {
            DataTable table = new DataTable("Employees");
            table.Columns.Add("ID", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("HireDate", typeof(DateTime));
            table.Columns.Add("Salary", typeof(decimal));

            table.Rows.Add(1, "Alice Johnson", new DateTime(2020, 5, 12), 72000);
            table.Rows.Add(2, "Bob Smith", new DateTime(2019, 3, 4), 68000);
            table.Rows.Add(3, "Carol White", DBNull.Value, 75000); // demonstrates a null value
            return table;
        }
```

> **ヒント:** データベースに表示されている列順序を正確に保ちたい場合は、`ImportDataTable` の `importColumnNames` パラメータを `true` に設定します。これにより、Aspose.Cells が列ヘッダーを書き込んでくれます。

## ステップ 3: 列スタイルの定義 – デフォルト + ライトブルー背景

Now we answer the **add light blue background** part of the puzzle. Aspose.Cells lets you pass an array of `Style` objects that correspond to each column you import. The first entry is the style for column 0, the second for column 1, and so on. If you have fewer styles than columns, the remaining columns fall back to the default style.

```csharp
            // Step 3: Define column styles – the default style and a custom style with a light‑blue foreground
            Style defaultStyle = workbook.DefaultStyle; // this is the use default style excel
            Style lightBlueStyle = workbook.CreateStyle();
            lightBlueStyle.ForegroundColor = Color.LightBlue;
            lightBlueStyle.Pattern = BackgroundType.Solid; // make sure the color shows

            // Apply default style to the first column, light blue to the second column
            Style[] columnStyles = { defaultStyle, lightBlueStyle };
```

> **なぜスタイルは 2 つだけなのか？** サンプルでは 4 列ありますが、目立たせたいのは 2 列目（Name）のみです。配列の長さは列数と一致する必要はなく、足りないエントリは自動的にワークブックのデフォルトスタイルを継承します。

## ステップ 4: ヘッダーとスタイル付きで DataTable をインポート

Here’s where we bring together **excel import datatable c#** and **import data with headers**. The `ImportDataTable` method does the heavy lifting: it writes the column names, rows, and applies the style array we just built.

```csharp
            // Step 4: Import the DataTable into the first worksheet starting at cell A1, applying the styles
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells.ImportDataTable(dataTable, // the source DataTable
                                        true,       // import column names as headers
                                        0,          // start row (0‑based)
                                        0,          // start column (0‑based)
                                        columnStyles);
```

### 期待される結果

After running the program, `workbook` will contain a single worksheet that looks like this:

| **ID** | **Name** (light‑blue) | **HireDate** | **Salary** |
|-------|------------------------|--------------|------------|
| 1     | Alice Johnson          | 5/12/2020    | 72000      |
| 2     | Bob Smith              | 3/4/2019     | 68000      |
| 3     | Carol White            | *(blank)*    | 75000      |

* **Name** 列はライトブルーの背景が適用され、スタイル配列が機能していることが確認できます。
* `importColumnNames` に `true` を渡したため、列ヘッダーは自動的に生成されます。
* Null 値は空白セルとして表示され、これは Aspose.Cells のデフォルト動作です。

## ステップ 5: ワークブックを保存する（オプションだが便利）

You’ll probably want to write the file to disk or stream it back to a web client. Saving is straightforward:

```csharp
            // Step 5: Save the workbook to a file
            string outputPath = "StyledEmployees.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

> **プロのヒント:** 古い Excel バージョン向けに出力する場合は、`SaveFormat.Xlsx` を `SaveFormat.Xls` に変更してください。API が自動で変換してくれます。

## エッジケースとバリエーション

### 複数のスタイル付き列

If you need more than one styled column, simply expand the `columnStyles` array:

```csharp
Style[] columnStyles = { defaultStyle, lightBlueStyle, defaultStyle, lightBlueStyle };
```

Now both **Name** and **Salary** will be light‑blue.

### 固定スタイルの代わりに条件付き書式

Sometimes you want a column to turn red when a value exceeds a threshold. That’s where **use default style excel** meets conditional formatting:

```csharp
int salaryColIdx = 3; // zero‑based index for Salary column
FormatCondition condition = sheet.ConditionalFormattings[0]
    .AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");
condition.Style.ForegroundColor = Color.LightCoral;
condition.Style.Pattern = BackgroundType.Solid;
```

### ヘッダーなしでインポート

If your downstream system already supplies its own headers, just pass `false` for the `importColumnNames` argument. The data will start at `A1` and you can write custom headers afterwards.

```csharp
sheet.Cells.ImportDataTable(dataTable, false, 1, 0); // start at row 2 (index 1)
```

## Full Working Example (All

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}