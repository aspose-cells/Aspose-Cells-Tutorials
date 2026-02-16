---
category: general
date: 2026-02-15
description: 在 C# 中建立新工作簿，並複製樞紐分析表而不遺失其定義。學習如何複製列、保留樞紐分析表，輕鬆複製樞紐分析表。
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- duplicate pivot table
language: zh-hant
og_description: 在 C# 中建立新工作簿，並在保留樞紐分析表定義的同時複製該表。開發者逐步指南。
og_title: 在 C# 中建立新活頁簿 – 保留樞紐分析表
tags:
- Aspose.Cells
- C#
- Excel automation
title: 在 C# 中建立新工作簿 – 保留樞紐分析表
url: /zh-hant/net/pivot-tables/create-new-workbook-in-c-preserve-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中建立新工作簿 – 保留樞紐分析表

Ever needed to **create new workbook** in C# that contains an exact copy of a pivot table from another file? You're not the only one. In many reporting pipelines the pivot table is the heart of the analysis, and losing its definition when you move data is a nightmare.

The good news? With a few lines of Aspose.Cells code you can copy rows—including the pivot table—into a fresh workbook and keep everything intact. Below you’ll see **how to copy rows**, **preserve pivot table** settings, and even **duplicate pivot table** across files without breaking formulas or cache.

## 本教學涵蓋內容

In this guide we’ll walk through:

1. Loading the source workbook that already has a pivot table.  
2. **Create new workbook** objects for the destination.  
3. Using `CopyRows` to transfer the range that holds the pivot table.  
4. Saving the result while ensuring the pivot table stays functional.  

No external documentation required—just the code, the why, and a handful of practical tips you can paste straight into your project.

> **Pro tip:** Aspose.Cells works with .NET Core, .NET Framework, and even Xamarin, so the same snippet runs wherever you need it.

---

![建立已複製樞紐分析表的新工作簿](/images/create-new-workbook-pivot.png "建立已複製樞紐分析表的新工作簿")

## 步驟 1 – 建立新工作簿並載入來源檔案

The first thing we do is **create new workbook** objects. One holds the original data, the other will receive the copied range.

```csharp
using Aspose.Cells;

// Load the source workbook that already contains a pivot table
var sourceWorkbook = new Workbook(@"C:\Data\source.xlsx");

// Create an empty workbook that will become the destination
var destinationWorkbook = new Workbook();
```

*Why this matters:*  
`Workbook` is the entry point for any Excel manipulation in Aspose.Cells. By instantiating a fresh workbook we guarantee a clean slate—no hidden styles or stray worksheets that could interfere later.

## 步驟 2 – 如何複製包含樞紐分析表的列

Now comes the core of the problem: **how to copy rows** that encapsulate the pivot table without flattening it. The `CopyRows` method does exactly that.

```csharp
// Copy the first 20 rows (adjust as needed) from the source to the destination
// Parameters: startRow, totalRows, targetCells, targetStartRow
sourceWorkbook.Worksheets[0].Cells.CopyRows(
    startRow: 0,
    totalRows: 20,
    targetCells: destinationWorkbook.Worksheets[0].Cells,
    targetStartRow: 0);
```

A few things to note:

* `startRow` and `totalRows` define the block that contains the pivot table.  
* The method copies **both** raw data and the pivot cache, so the destination workbook knows how to rebuild the pivot table on the fly.  
* If your pivot starts deeper in the sheet, just change the indices—no need for a different API call.

> **Common question:** *Will the copied pivot lose its source data reference?*  
> No. Aspose.Cells embeds the cache directly into the worksheet, so the pivot becomes self‑contained in the new file.

## 步驟 3 – 儲存目的地時保留樞紐分析表

After the rows are copied, the pivot table lives in the destination workbook exactly as it did in the source. Saving the file is straightforward.

```csharp
// Save the destination workbook; the pivot table remains functional
destinationWorkbook.Save(@"C:\Data\destination.xlsx");
```

When you open `destination.xlsx` in Excel, you’ll see the pivot table ready to refresh. The **preserve pivot table** behavior is automatic because the cache traveled with the rows.

### 驗證結果

Open the file and:

1. Click the pivot table.  
2. Notice the field list appears—this means the cache is intact.  
3. Try a refresh; the data updates without errors.

If you encounter a *#REF!* error, double‑check that the copied range includes the hidden cache rows (usually right after the visible data).

## 步驟 4 – 複製樞紐分析表至多個工作簿（可選）

Sometimes you need the same pivot in several reports. The pattern we just used scales nicely—just repeat the copy for each new workbook.

```csharp
string[] targets = {
    @"C:\Reports\Q1.xlsx",
    @"C:\Reports\Q2.xlsx",
    @"C:\Reports\Q3.xlsx"
};

foreach (var path in targets)
{
    var wb = new Workbook(); // fresh workbook each loop
    sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 20, wb.Worksheets[0].Cells, 0);
    wb.Save(path);
}
```

This snippet **duplicates pivot table** three times with a single loop. Adjust the `targets` array to match your reporting schedule.

### 需要留意的邊緣情況

| 情況 | 需要注意的地方 | 解決方式 |
|-----------|-------------------|-----|
| Pivot uses external data source | Cache may reference a connection that doesn’t exist on the new machine | Embed the data source or recreate the connection in the destination workbook |
| Very large pivot ( > 100 k rows ) | `CopyRows` can be memory‑intensive | Use `CopyRows` in chunks or consider `Copy` with `PasteOptions` to limit memory usage |
| Worksheet has hidden rows/columns | Hidden cache rows might be skipped if you copy only visible rows | Always copy the exact row range that contains the cache, not just the visible area |

## 完整範例程式

Putting it all together, here’s a self‑contained program you can drop into a console app.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook (contains the original pivot)
            var sourcePath = @"C:\Data\source.xlsx";
            var sourceWorkbook = new Workbook(sourcePath);

            // 2️⃣ Prepare destination workbook
            var destinationWorkbook = new Workbook();

            // 3️⃣ Copy rows that include the pivot (adjust range as needed)
            sourceWorkbook.Worksheets[0].Cells.CopyRows(
                startRow: 0,
                totalRows: 20,
                targetCells: destinationWorkbook.Worksheets[0].Cells,
                targetStartRow: 0);

            // 4️⃣ Save – the pivot table is preserved
            var destPath = @"C:\Data\destination.xlsx";
            destinationWorkbook.Save(destPath);

            Console.WriteLine("Pivot table successfully copied!");
        }
    }
}
```

Run the program, open `destination.xlsx`, and you’ll see the same pivot table ready to slice and dice your data. No manual recreation required.

---

## 結論

We’ve just shown how to **create new workbook** in C# and **copy pivot table** while keeping every setting alive. By using `CopyRows` you get a reliable way to **preserve pivot table** functionality, answer the age‑old “**how to copy rows**” question, and even **duplicate pivot table** across multiple reports with minimal code.

Next steps? Try changing the copied range to include charts that reference the same pivot, or experiment with `PasteOptions` to retain formatting exactly. The same pattern works for other Aspose.Cells objects like tables and named ranges, so feel free to extend it.

Got a twist you’re wrestling with—maybe a pivot that pulls from an external DB, or a workbook that lives in the cloud? Drop a comment below, and we’ll tackle it together. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}