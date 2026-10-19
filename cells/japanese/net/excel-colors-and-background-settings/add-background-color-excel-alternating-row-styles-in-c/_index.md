---
category: general
date: 2026-04-07
description: C# を使用して Excel の行に背景色を追加します。交互に行の色を設定する方法、単色の背景スタイルを設定する方法、そしてデータテーブルを
  Excel にインポートする方法を、1 つのワークフローで学びましょう。
draft: false
keywords:
- add background color excel
- apply alternating row colors
- style excel rows
- set solid background
- import datatable to excel
language: ja
og_description: C#でExcelの行に背景色を追加する。このガイドでは、交互の行色の適用、単色背景の設定、そしてデータテーブルを効率的にExcelにインポートする方法を示します。
og_title: Excelに背景色を追加 – C#で交互行スタイル
tags:
- C#
- Excel
- DataTable
- Styling
title: Excelに背景色を追加 – C#で交互行スタイル
url: /ja/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excelに背景色を追加 – C#での交互行スタイル

Ever needed to **add background color excel** rows but weren't sure how to do it without a thousand lines of fiddly code? You're not alone—most developers hit that wall when they first try to make their spreadsheets look more than just a raw dump of data.  

The good news? In just a few minutes you can **apply alternating row colors**, set a **solid background**, and even **import datatable to excel** using a clean, reusable pattern in C#.  

In this tutorial we’ll walk through the whole process, from pulling data into a `DataTable` to styling each row with a light‑yellow‑white stripe pattern. No external libraries beyond a solid Excel‑handling package (like **ClosedXML** or **GemBox.Spreadsheet**) are required, and you’ll see why this approach is both performant and easy to maintain.

## 学べること

- データを取得し、Excel ワークシートに入力する方法。
- 交互の背景色で **style excel rows** を行う方法。
- `Style` オブジェクトを使用した **set solid background** の仕組み。
- 行スタイルを保持しながら **import datatable to excel** する方法。
- 空のテーブルやカスタムカラー スキームなどのエッジケースを扱うためのヒント。

> **Pro tip:** すでにスタイル作成をサポートするライブラリからワークブックオブジェクト（`wb`）を使用している場合、同じ `Style` インスタンスを複数のワークシートで再利用できます—メモリを節約し、コードをすっきり保てます。

---

## ステップ 1: データの取得 – DataTable の準備

Before any styling can happen we need a source of rows. In most real‑world scenarios this comes from a database, an API, or a CSV file. For illustration, we’ll just create a simple `DataTable` in‑memory.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using GemBox.Spreadsheet;      // Or ClosedXML, whichever you prefer

// Simulated data fetch – replace with your own data access logic
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with sample rows
    for (int i = 1; i <= 10; i++)
        table.Rows.Add(i, $"Student {i}", Math.Round(new Random().NextDouble() * 100, 2));

    return table;
}
```

**Why this matters:** `DataTable` を使用すると、Excel ライブラリが直接インポートできる表形式でスキーマを認識したコンテナが得られ、セル単位のループを書く必要がなくなります。

---

## ステップ 2: 行スタイルの作成 – **Apply alternating row colors**

Now we’ll build an array of `Style` objects—one per row—so that each row can receive its own background. The pattern we’ll use is a classic light‑yellow for even rows and white for odd rows.

```csharp
// Assume 'wb' is an existing Workbook instance
Workbook wb = new Workbook();

// Retrieve data
DataTable dataTable = GetData();

// Allocate a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style instance
    rowStyles[i] = wb.CreateStyle();

    // Choose background colour based on row index
    rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;

    // Ensure the colour is actually applied
    rowStyles[i].Pattern = BackgroundType.Solid;   // <-- **set solid background**
}
```

**Explanation:**  
- `wb.CreateStyle()` は、他のスタイルに影響を与えずに調整できるクリーンなスタイルオブジェクトを提供します。  
- 三項演算子 `(i % 2 == 0)` は、行が偶数（淡い黄色）か奇数（白）かを決定します。  
- `Pattern = BackgroundType.Solid` を設定することが、**set solid background** の重要なステップです。これがないと色は無視されます。

---

## ステップ 3: 対象ワークシートの取得

Most libraries expose a worksheet collection. We’ll work with the first one, but you can target any index or name you prefer.

```csharp
Worksheet worksheet = wb.Worksheets[0];   // First worksheet in the workbook
```

If the workbook is brand new, the library usually creates a default sheet for you. Otherwise, you can add one explicitly:

```csharp
// Alternative: create a new sheet named "Report"
Worksheet worksheet = wb.Worksheets.Add("Report");
```

---

## ステップ 4: 行スタイル付きで DataTable をインポート – **Import datatable to excel**

With the styles ready, the final step is to push the `DataTable` into the sheet while applying the corresponding style to each row.

```csharp
// Parameters: (DataTable, includeHeaders, startRow, startColumn, stylesArray)
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

**What’s happening under the hood?**  
- `true` は、メソッドに列ヘッダーを最初の行として書き込むよう指示します。  
- `0, 0` は左上隅（A1）を挿入位置としてマークします。  
- `rowStyles` は各 `Style` を対応するデータ行に合わせ、事前に用意した交互の色を適用します。

---

## ステップ 5: ワークブックの保存

The last piece of the puzzle is persisting the workbook to a file so you can open it in Excel and see the result.

```csharp
// Choose a format – XLSX is the modern default
wb.Save("StudentScores.xlsx");

// Optional: open automatically (Windows only)
System.Diagnostics.Process.Start("StudentScores.xlsx");
```

Open the file and you should see a neatly formatted sheet:

- ヘッダー行は太字（デフォルトのライブラリスタイリング）。  
- 行 1, 3, 5… はクリーンな白背景。  
- 行 2, 4, 6… はさりげない淡い黄色の塗りつぶしで、スキャンしやすくなります。

### 期待される出力スナップショット

| Id | Name      | Score |
|----|-----------|-------|
| 1  | Student 1 | 78.45 |
| 2  | Student 2 | 62.13 |
| 3  | Student 3 | 91.27 |
| …  | …         | …     |

Rows 2, 4, 6, … appear with a light‑yellow background—exactly the **apply alternating row colors** effect we aimed for.

![Add background color excel example](https://example.com/excel-background.png "Add background color excel example")

*(Alt テキストには SEO 用の主要キーワードが含まれています。)*

---

## エッジケースとバリエーションの処理

### 空の DataTable

If `dataTable.Rows.Count` is zero, the `rowStyles` array will be empty and `ImportDataTable` will still write the header row (if `includeHeaders` is `true`). No exception is thrown, but you might want to guard against generating an almost‑blank file:

```csharp
if (dataTable.Rows.Count == 0)
{
    Console.WriteLine("No data to export – workbook will contain only headers.");
}
```

### カスタムカラー スキーム

Want a blue/gray stripe instead of yellow/white? Just replace the `Color` values:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightBlue : Color.LightGray;
```

Feel free to pull colours from a configuration file so non‑developers can tweak the palette without touching code.

### 複数のワークシートでスタイルを再利用する

If you export several tables into the same workbook, you can generate the style array once and reuse it:

```csharp
Style[] sharedStyles = CreateAlternatingStyles(dataTable.Rows.Count);
worksheet1.Cells.ImportDataTable(dt1, true, 0, 0, sharedStyles);
worksheet2.Cells.ImportDataTable(dt2, true, 0, 0, sharedStyles);
```

Just be careful that both tables have the same row count, or generate a new array per sheet.

---

## 完全な動作例

Putting everything together, here’s a self‑contained program you can copy‑paste into a console app.

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;   // Install-Package GemBox.Spreadsheet

class Program
{
    static void Main()
    {
        // License free for small projects – remove for commercial use
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Initialise workbook
        Workbook wb = new Workbook();

        // 3️⃣ Create alternating row styles
        Style[] rowStyles = CreateAlternatingStyles(dataTable.Rows.Count);

        // 4️⃣ Get (or create) the target worksheet
        Worksheet ws = wb.Worksheets.Add("Report");

        // 5️⃣ Import data with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // 6️⃣ Save the file
        wb.Save("Report.xlsx");
        Console.WriteLine("Excel file created – check Report.xlsx");
    }

    // Helper: generate a DataTable with sample data
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        var rnd = new Random();
        for (int i = 1; i <= 12; i++)
            dt.Rows.Add(i, $"Student {i}", Math.Round(rnd.NextDouble() * 100, 2));

        return dt;
    }

    // Helper: create style array for alternating colors
    static Style[] CreateAlternatingStyles(int rowCount)
    {
        var wb = new Workbook();               // Temporary workbook for style creation
        var styles = new Style[rowCount];
        for (int i = 0; i < rowCount; i++)
        {
            styles[i] = wb.CreateStyle();
            styles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;
            styles[i].Pattern = BackgroundType.Solid;   // **set solid background**
        }
        return styles;
    }
}
```

Run the program, open `Report.xlsx`, and you’ll see the alternating background exactly as described.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}