---
category: general
date: 2026-09-27
description: 學習如何在 C# 中刪除 Excel 表格的列，透過一步一步的教學，同時展示如何快速載入 Excel 工作簿（C#）。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from Excel table
- load Excel workbook C#
language: zh-hant
lastmod: 2026-09-27
og_description: 在 C# 中刪除 Excel 表格的列，並提供清晰範例。本教學亦會說明如何在 C# 中載入 Excel 活頁簿，並處理常見的邊緣情況。
og_image_alt: Screenshot illustrating delete rows from Excel table using C# code
og_title: 在 C# 中刪除 Excel 表格列 – 完整程式碼指南
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  headline: How to delete rows from Excel table using C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  name: How to delete rows from Excel table using C#
  steps:
  - name: What if the table has a different name or position?
    text: '* **Named table:** Use `ws.ListObjects["MyTableName"]` instead of the index.
      * **Multiple tables:** Loop through `ws.ListObjects` and pick the one that matches
      a condition (e.g., column header names). * **Dynamic row count:** You can compute
      `rowCount` at runtime by inspecting `ws.ListObjects[0].Dat'
  - name: Edge‑case handling
    text: '| Situation | Recommended code change | |----------------------------------------|--------------------------------------------------------------|
      | Table is empty or has fewer rows | Check `ws.ListObjects[0].DataRange.RowCount`
      before deleting. | | Rows to delete exceed table size | Clamp `rowCount`'
  - name: How do I delete rows from **all** tables in a workbook?
    text: '```csharp foreach (Worksheet sheet in workbook.Worksheets) { foreach (ListObject
      tbl in sheet.ListObjects) { // Example: delete the first data row of each table
      if (tbl.DataRange.RowCount > 1) tbl.DeleteRows(1, 1); } } ```'
  - name: Can I delete rows based on a **cell value**?
    text: 'Yes. Scan the `DataRange` for matching cells, collect their zero‑based
      indices, then delete in descending order:'
  - name: What if I need to **preserve formatting**?
    text: '`DeleteRows` removes the entire row from the table but retains the table’s
      style for remaining rows. If you need to keep specific formatting on a row you’re
      deleting, copy the style to another row before deletion.'
  - name: Does this work with **.xls** (Excel 97‑2003) files?
    text: Yes. Aspose.Cells automatically detects the file format, so the same code
      works with `.xls`. Just change the file extension in the `Workbook` constructor.
  - name: Next steps
    text: '* Explore **ClosedXML** or **EPPlus** if you prefer a fully open‑source
      stack. * Combine row deletion with **data validation** to clean spreadsheets
      before importing into a database. * Automate the process for a folder of workbooks
      using `Directory.GetFiles` and a loop.'
  type: HowTo
tags:
- Excel
- C#
- .NET
title: 如何使用 C# 刪除 Excel 表格中的列
url: /zh-hant/net/row-and-column-management/how-to-delete-rows-from-excel-table-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 Excel 表格中刪除列（C#）—完整程式指南

如果您需要在 .xlsx 檔案中**刪除 Excel 表格的列**，本教學會精確示範如何使用 C# 完成。您將看到一個簡潔、可執行的範例，載入 Excel 活頁簿、從第一個表格中移除特定列，並將結果儲存。此方法適用於流行的 Aspose.Cells 函式庫，亦可套用至其他 .NET Excel API。

在清理匯入資料、裁剪報告區段或自動化試算表更新時，從表格中刪除列是一項常見任務。閱讀完本指南後，您將能夠**載入 Excel 活頁簿（C#）**、定位表格（ListObject）、刪除任意列，並將修改後的檔案寫回磁碟。

## Prerequisites

先決條件

Before you start, make sure you have:

* .NET 6.0 或更新版本已安裝（此程式碼亦相容於 .NET Framework 4.7+）。
* 參考 **Aspose.Cells** NuGet 套件（或任何提供 `Workbook`、`Worksheet`、`ListObject` 型別的相容函式庫）。
* 一個名為 `input.xlsx` 的輸入檔案，放置於專案可參照的資料夾中。
* 基本的 C# 語法與 Visual Studio（或您慣用的 IDE）使用經驗。

> **Pro tip:** 如果您偏好開源方案，完全相同的邏輯也可套用於 **ClosedXML** ——只需將 Aspose 專屬類別換成 `XLWorkbook`、`IXLWorksheet` 與 `IXLTable`。

## Step 1: Load the Excel workbook in C#

步驟 1：在 C# 中載入 Excel 活頁簿

The first operation is to read the source file into memory. Loading the workbook is cheap for typical spreadsheet sizes and gives you full access to worksheets, tables, and cell values.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook
// Replace YOUR_DIRECTORY with the actual folder path, e.g. @"C:\Data"
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

*Why this matters:* `Workbook` parses the Open XML structure of the .xlsx file, exposing a collection of `Worksheet` objects. If the file cannot be found, Aspose throws a `FileNotFoundException`, so ensure the path is correct.

*為何重要：* `Workbook` 會解析 .xlsx 檔案的 Open XML 結構，並公開 `Worksheet` 物件集合。若找不到檔案，Aspose 會拋出 `FileNotFoundException`，因此請確認路徑正確。

## Step 2: Access the target worksheet

步驟 2：存取目標工作表

Most spreadsheets contain multiple sheets; you need to pick the one that holds the table you want to modify. Here we use the first sheet (`Worksheets[0]`), which is a safe default for simple files.

```csharp
// Step 2: Access the first worksheet
Worksheet ws = workbook.Worksheets[0];
```

*Why this matters:* `Worksheet` is the container for tables (`ListObjects`). Accessing the correct sheet prevents accidental changes to unrelated data.

*為何重要：* `Worksheet` 是表格（`ListObjects`）的容器。存取正確的工作表可避免意外修改無關資料。

## Step 3: Delete rows from Excel table

步驟 3：從 Excel 表格中刪除列

Excel tables are represented by `ListObject` objects. The first table on the sheet is `ListObjects[0]`. The `DeleteRows(startIndex, rowCount)` method removes rows **relative to the table’s data area**, not the worksheet’s absolute row numbers.  

In this example we delete the second and third rows of the table (the header is row 0, so we start at index 1).

```csharp
// Step 3: Delete rows 1 and 2 from the first table (ListObject)
// The first row (index 0) is the header, so we start at index 1
ws.ListObjects[0].DeleteRows(1, 2);
```

### What if the table has a different name or position?

如果表格有不同的名稱或位置，該怎麼辦？

* **Named table:** Use `ws.ListObjects["MyTableName"]` instead of the index.
* **Multiple tables:** Loop through `ws.ListObjects` and pick the one that matches a condition (e.g., column header names).
* **Dynamic row count:** You can compute `rowCount` at runtime by inspecting `ws.ListObjects[0].DataRange.RowCount`.

### Edge‑case handling

邊緣情況處理

| 情況 | 建議的程式碼變更 |
|------|-------------------|
| 表格為空或列數不足 | 在刪除前檢查 `ws.ListObjects[0].DataRange.RowCount`。 |
| 要刪除的列超過表格大小 | 將 `rowCount` 限制為 `DataRange.RowCount - startIndex`。 |
| 需要根據條件刪除列（例如 C 欄的值） | 迭代 `DataRange.Rows`，收集符合條件的索引，然後以相反順序刪除以保持索引穩定。 |

## Step 4: Save the modified workbook

步驟 4：儲存已修改的活頁簿

After the deletion, write the workbook back to a new file (or overwrite the original if you prefer). Saving creates a fresh .xlsx that reflects the updated table.

```csharp
// Step 4: Save the modified workbook
workbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

*Why this matters:* `Save` serializes the in‑memory representation to disk. If you need to preserve the original file, always write to a different path.

*為何重要：* `Save` 會將記憶體中的表示序列化寫入磁碟。若需保留原始檔案，請務必寫入不同的路徑。

## Full, runnable example

完整、可執行的範例

Putting all steps together gives you a self‑contained program you can copy, paste, and run.

```csharp
using System;
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Adjust the folder path as needed
        const string folder = @"YOUR_DIRECTORY";

        // Load the workbook (load Excel workbook C#)
        Workbook workbook = new Workbook($"{folder}\\input.xlsx");

        // Access the first worksheet
        Worksheet ws = workbook.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (ws.ListObjects.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Delete rows 1 and 2 from the first table (skip header)
        ListObject table = ws.ListObjects[0];
        int rowsToDelete = Math.Min(2, table.DataRange.RowCount - 1); // guard against short tables
        if (rowsToDelete > 0)
        {
            table.DeleteRows(1, rowsToDelete);
            Console.WriteLine($"Deleted {rowsToDelete} row(s) from table \"{table.Name}\".");
        }
        else
        {
            Console.WriteLine("Table does not have enough rows to delete.");
        }

        // Save the result
        workbook.Save($"{folder}\\output.xlsx");
        Console.WriteLine("Workbook saved as output.xlsx");
    }
}
```

**Expected output** (console):

**預期輸出**（主控台）：

```
Deleted 2 row(s) from table "Table1".
Workbook saved as output.xlsx
```

Open `output.xlsx` – the first table now lacks the rows you removed, while the header row remains intact.

開啟 `output.xlsx` ——第一個表格已不含您剛剛刪除的列，且標題列仍然完整。

## Common questions and variations

常見問題與變體

### How do I delete rows from **all** tables in a workbook?

如何從活頁簿中的**所有**表格刪除列？

```csharp
foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (ListObject tbl in sheet.ListObjects)
    {
        // Example: delete the first data row of each table
        if (tbl.DataRange.RowCount > 1)
            tbl.DeleteRows(1, 1);
    }
}
```

### Can I delete rows based on a **cell value**?

我能根據**儲存格值**刪除列嗎？

Yes. Scan the `DataRange` for matching cells, collect their zero‑based indices, then delete in descending order:

```csharp
var rowsToRemove = new List<int>();
for (int i = 0; i < table.DataRange.RowCount; i++)
{
    var cell = table.DataRange[i, 2]; // column C (zero‑based)
    if (cell.StringValue == "Obsolete")
        rowsToRemove.Add(i);
}

// Delete rows from bottom to top to keep indices valid
rowsToRemove.Sort((a, b) => b.CompareTo(a));
foreach (int rowIdx in rowsToRemove)
    table.DeleteRows(rowIdx, 1);
```

### What if I need to **preserve formatting**?

如果我需要**保留格式**該怎麼辦？

`DeleteRows` removes the entire row from the table but retains the table’s style for remaining rows. If you need to keep specific formatting on a row you’re deleting, copy the style to another row before deletion.

### Does this work with **.xls** (Excel 97‑2003) files?

這是否適用於 **.xls**（Excel 97‑2003）檔案？

Yes. Aspose.Cells automatically detects the file format, so the same code works with `.xls`. Just change the file extension in the `Workbook` constructor.

## Performance tips

效能建議

* **Batch deletions:** Deleting many rows one by one can be slower. Use a single `DeleteRows(start, count)` call when possible.
* **Avoid UI thread blocking:** If you integrate this into a desktop app, run the workbook manipulation on a background thread to keep the UI responsive.
* **Dispose properly:** Although Aspose.Cells uses managed memory, wrap the `Workbook` in a `using` block if you’re dealing with large files to free resources promptly.

## Conclusion

結論

You now have a complete, production‑ready example that **deletes rows from Excel table** using C#. The guide covered how to **load Excel workbook C#**, locate the desired `ListObject`, safely remove rows, and save the updated file. With the edge‑case handling and performance advice included, you can adapt this pattern to more complex scenarios such as conditional deletions, multiple tables, or alternative .NET Excel libraries.

### Next steps

下一步

* Explore **ClosedXML** or **EPPlus** if you prefer a fully open‑source stack.
* Combine row deletion with **data validation** to clean spreadsheets before importing into a database.
* Automate the process for a folder of workbooks using `Directory.GetFiles` and a loop.

Feel free to experiment with different row ranges, table names, and conditional logic. Happy coding!

## What Should You Learn Next?

接下來該學什麼？

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [載入 Excel 檔案 C# – 如何刪除列並移除特定列](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)
- [如何在 Aspose.Cells for .NET 中插入與刪除 Excel 列：完整指南](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [如何使用 Aspose.Cells .NET 刪除 Excel 中的空白列以進行資料清理](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}