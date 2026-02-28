---
category: general
date: 2026-02-28
description: 在 C# 中快速刪除 Excel 表格的列。學習如何新增命名範圍、以名稱存取工作表，並避免重複名稱錯誤。
draft: false
keywords:
- delete rows excel table
- add named range excel
- access worksheet by name
- how to add defined name
- named range on another sheet
language: zh-hant
og_description: 使用 C# 刪除 Excel 表格的列。本教學亦示範如何新增命名範圍以及透過名稱存取工作表。
og_title: 使用 C# 刪除 Excel 表格中的列 – 完整指南
tags:
- C#
- Excel
- DevExpress Spreadsheet
title: 使用 C# 刪除 Excel 表格列 – 步驟指南
url: /zh-hant/net/row-and-column-management/delete-rows-excel-table-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 刪除 Excel 表格列 – 完整程式教學

是否曾需要從活頁簿中 **delete rows excel table**，卻不確定該使用哪個 API 呼叫？你並非唯一遇到此問題的人——大多數開發者在首次嘗試以程式方式縮減表格時，都會碰到同樣的障礙。  

在本指南中，我們將逐步示範一個完整且可執行的範例，不僅能從 Excel 表格中移除列，還會說明 **how to add defined name**（亦即 *named range*）、如何 **access worksheet by name**，以及為何在另一張工作表上新增重複名稱會拋出 `InvalidOperationException`。  

完成本文後，你將能夠：

* 以分頁名稱取得工作表。  
* 安全地刪除該工作表上第一個表格的資料列。  
* 建立指向特定地址的命名範圍。  
* 了解跨工作表重複名稱的陷阱。

不需要外部文件說明——所有資訊都在此處。

---

## 需要的環境

* **DevExpress Spreadsheet**（或任何提供 `Workbook`、`Worksheet`、`ListObject` 與 `Names` 物件的函式庫）。  
* 目標為 **.NET 6** 或更新版本的 .NET 專案（程式碼亦可在 .NET Framework 4.8 上編譯）。  
* 基本的 C# 熟悉度——只要會寫 `foreach` 迴圈，就能上手。

> **Pro tip:** 若你使用的是 DevExpress 的免費 Community Edition，以下使用的 API 與商業版完全相同。

## 步驟 1 – 以名稱存取工作表

首先必須找出包含欲修改表格的工作表。  
大多數開發者習慣直接使用 `Worksheets[0]`，但這樣會讓程式碼與工作表順序耦合，一旦有人更改分頁名稱就會失效。

```csharp
using DevExpress.Spreadsheet;

// Assume 'workbook' is an already‑loaded Workbook instance
Worksheet worksheet = workbook.Worksheets["Sheet1"];   // <-- access worksheet by name
```

*Why this matters:* 透過工作表的 **name** 而非索引，可避免活頁簿變動時誤編輯錯誤的工作表。  

如果提供的名稱不存在，函式庫會拋出 `KeyNotFoundException`，你可以捕捉它並顯示友善的錯誤訊息。

## 步驟 2 – 刪除 Excel 表格列（安全方式）

取得正確的工作表後，接下來移除第一個表格的資料列。  
常見錯誤是呼叫 `DeleteRows(1, rowCount‑1)`。自 **DevExpress 22.2** 起，此重載已被 **禁止**，會拋出 `InvalidOperationException`。函式庫要求在表格的資料範圍內刪除列，而非標題列。

```csharp
// Grab the first table (ListObject) on the sheet
var table = worksheet.ListObjects[0];

// Calculate how many data rows we actually have (excluding the header)
int dataRowCount = table.DataRange.RowCount;

// Delete only the data rows – keep the header intact
if (dataRowCount > 0)
{
    // DeleteRows(startRow, rowCount) – startRow is zero‑based within the table
    table.DeleteRows(0, dataRowCount);
}
```

> **What if the table is empty?** `if` 防護會避免在 `rowCount = 0` 時呼叫，否則會產生例外。

### 視覺概覽  

![刪除 Excel 表格列範例](image.png "顯示從 Excel 表格中移除列的螢幕截圖")  

*Alt text: 刪除 Excel 表格列範例 in C# code*

## 步驟 3 – 如何新增已定義名稱（建立命名範圍）

清理完表格後，你可能想在之後的圖表或資料驗證清單中引用特定範圍。這時 **add named range excel** 就派上用場了。

```csharp
// Define a name that points to A1:C5 on Sheet1
workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

// Verify that the name exists
Name definedName = workbook.Names["MyTable"];
Console.WriteLine($"Defined name '{definedName.Name}' points to {definedName.RefersTo}");
```

`Names.Add` 方法接受兩個參數：識別名稱與 A1 風格的地址。  
因為前面已使用 **access worksheet by name**，地址字串可以安全地參照任何工作表，而不必擔心索引變動。

## 步驟 4 – 另一張工作表的命名範圍 – 避免重複名稱錯誤

你可能會認為可以在不同工作表上重複使用相同的識別名稱，例如：

```csharp
// Attempt to add the same name on Sheet2 – this will throw
workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

然而，Excel 的命名範圍作用域是 **整個活頁簿**，而非單一工作表。上述呼叫會觸發 `InvalidOperationException`，訊息為 *「A name with the same identifier already exists.」*  

### 解決方法

1. **Pick a unique name** (`MyTable_Sheet2`)。  
2. **Delete the existing name** before re‑adding it（僅在確實想取代時執行）。  

```csharp
// Option A – use a unique name
workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");

// Option B – replace the existing name (use with caution)
if (workbook.Names.Contains("MyTable"))
    workbook.Names.Remove("MyTable");

workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

## 完整、可執行範例

將所有步驟整合起來，以下是一個可直接放入 Visual Studio 並對 `sample.xlsx` 範例檔執行的自包含主控台應用程式。

```csharp
using System;
using DevExpress.Spreadsheet;

class Program
{
    static void Main()
    {
        // Load an existing workbook (replace with your file path)
        Workbook workbook = new Workbook();
        workbook.LoadDocument("sample.xlsx");

        // -------------------------------------------------
        // Step 1 – Access the worksheet by its tab name
        // -------------------------------------------------
        Worksheet worksheet = workbook.Worksheets["Sheet1"]; // primary sheet

        // -------------------------------------------------
        // Step 2 – Delete rows excel table (safe method)
        // -------------------------------------------------
        var table = worksheet.ListObjects[0];
        int dataRows = table.DataRange.RowCount;
        if (dataRows > 0)
            table.DeleteRows(0, dataRows); // removes only data rows

        // -------------------------------------------------
        // Step 3 – Add a defined name (named range) on Sheet1
        // -------------------------------------------------
        workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

        // -------------------------------------------------
        // Step 4 – Demonstrate duplicate‑name handling
        // -------------------------------------------------
        try
        {
            workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
        }
        catch (InvalidOperationException ex)
        {
            Console.WriteLine("Duplicate name error: " + ex.Message);
            // Use a unique identifier instead
            workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");
        }

        // Save the modified workbook
        workbook.SaveDocument("sample_modified.xlsx");
        Console.WriteLine("Workbook updated successfully.");
    }
}
```

**Expected outcome**

* 所有位於 **Sheet1** 上第一個表格的資料列皆被刪除，只剩下標題列。  
* 名稱 **MyTable** 現在指向 `Sheet1!$A$1:$C$5`。  
* 第二個名稱 **MyTable_Sheet2** 安全地參照 **Sheet2** 上的範圍，且不會拋出例外。

## 常見問題與邊緣情況

| Question | Answer |
|----------|--------|
| *What if the workbook has multiple tables?* | 透過索引取得正確的 `ListObject`（`worksheet.ListObjects[1]`）或以名稱取得（`worksheet.ListObjects["MyTable"]`）。 |
| *Can I delete rows from a table that spans multiple worksheets?* | 不行——表格只能存在於單一工作表。必須對每張工作表分別執行刪除邏輯。 |
| *Is there a way to delete only a subset of rows?* | 可以——使用 `table.DeleteRows(startRow, count)`，其中 `startRow` 為表格資料區的零基索引。 |
| *Do named ranges survive after saving?* | 會的。只要呼叫 `SaveDocument`，命名範圍就會寫入活頁簿的 XML 中。 |
| *How do I list all defined names in the workbook?* | 使用 `foreach (var name in workbook.Names) Console.WriteLine(name.Name);` 逐一列出。 |

## 結論

我們已說明如何使用 C# **delete rows excel table**、展示 **add named range excel**，以及正確的 **access worksheet by name** 方法，避免惹出令人頭痛的 duplicate‑name 例外。  

完整解決方案就在上方的程式碼片段——直接複製、貼上並對自己的檔案執行即可。之後你可以將邏輯擴充至多表格、動態範圍計算，甚至整合 UI。

**Next steps** 你可以探索：

* 使用 **named range on another sheet** 來驅動圖表系列。  
* 結合 **ExcelDataReader** 於清理前先匯入資料。  
* 透過簡單的 `foreach (var file in Directory.GetFiles(...))` 迴圈，對數十本活頁簿執行批次更新。

對 C# 中的 Excel 自動化還有其他問題嗎？留下評論，我們持續討論。祝編程愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}