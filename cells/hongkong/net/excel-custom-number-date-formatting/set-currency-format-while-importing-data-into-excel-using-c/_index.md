---
category: general
date: 2026-11-19
description: 使用 C# 設定 Excel 貨幣格式 – 學習在匯入 Excel 工作表時，如何設定數字格式與欄位樣式。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set currency format
- how to set number format
- assign number format
- excel worksheet import
- style excel columns
language: zh-hant
lastmod: 2026-11-19
og_description: 以 C# 在 Excel 中設定貨幣格式，了解如何設定數字格式、指派數字格式，以及在匯入 Excel 工作表時為欄位套用樣式。
og_image_alt: Screenshot showing Excel cells formatted as currency after import
og_title: 使用 C# 在 Excel 中設定貨幣格式 – 完整一步步指南
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  headline: Set currency format while importing data into Excel using C#
  type: TechArticle
- description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  name: Set currency format while importing data into Excel using C#
  steps:
  - name: Expected result
    text: 'When you open **FinancialReport.xlsx**, you’ll see:'
  - name: Assign number format to date columns
    text: '```csharp // Suppose column 2 contains dates and you want "dd-MMM-yyyy"
      columnStyles[2].Number = 14; // 14 = built‑in short date ```'
  - name: Use custom number formats for percentages
    text: '```csharp columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00% ```'
  - name: Styling beyond number formats
    text: 'You can also set font, background color, or alignment on the same `Style`
      object:'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
- Formatting
title: 使用 C# 匯入資料至 Excel 時設定貨幣格式
url: /zh-hant/net/excel-custom-number-date-formatting/set-currency-format-while-importing-data-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中匯入資料至 Excel 時設定貨幣格式

如果您需要在 Excel 工作表中 **設定貨幣格式**，本教學將示範如何 **設定數字格式** 並在執行 **Excel 工作表匯入** 時為欄位套用樣式。您將看到完整、可執行的範例，為 `DataTable` 的每個欄位指派正確的數字格式，並以期望的樣式匯入資料。

在 C# 中操作 Excel 時，往往不只是把原始值寫入——還必須控制數字的顯示方式。無論是產生發票、財務報表或儀表板，正確的貨幣、百分比或日期格式都能讓輸出即刻易讀。

## 前置條件

開始之前，請確保您已具備：

* 已安裝 .NET 6.0（或更新版本）。
* 參考 **Aspose.Cells for .NET**（或任何提供 `Style` 類別且具 `Number` 屬性的函式庫）。  
  *NuGet*: `Install-Package Aspose.Cells`。
* 具備 `DataTable` 與 C# 集合的基本概念。
* 使用 Visual Studio 2022、VS Code 或其他 IDE。

## 步驟 1：取得要寫入工作表的資料

先取得包含欲匯出的原始資料的 `DataTable`。在實務專案中，這可能來自資料庫查詢、API 呼叫或 CSV 解析器。

```csharp
using System.Data;

/// <summary>
/// Returns a sample DataTable with three columns:
/// Id (int), Amount (decimal), and Description (string).
/// </summary>
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Amount", typeof(decimal));
    table.Columns.Add("Description", typeof(string));

    // Sample rows
    table.Rows.Add(1, 1234.56m, "Office supplies");
    table.Rows.Add(2, 98765.43m, "Consulting fees");
    table.Rows.Add(3, 0.99m, "Miscellaneous");

    return table;
}

// Retrieve the data
DataTable dataTable = GetData();
```

> **為什麼重要：** 匯入完整填充的 `DataTable` 能讓資料取得邏輯與 Excel 產生邏輯分離，提升可測試性與可維護性。

## 步驟 2：建立樣式陣列 – 每個 DataTable 欄位對應一個條目

Aspose.Cells 需要一個長度與欲匯入欄位數相同的 `Style[]`。每個元素可保存特定的數字格式。

```csharp
// Allocate a Style object for each column
Style[] columnStyles = new Style[dataTable.Columns.Count];

// Initialize each Style instance (required before assigning properties)
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = ws.Workbook.CreateStyle();
}
```

> **小技巧：** 即使只需要為部份欄位設定格式，也必須為每個欄位建立 `Style` 實例；否則匯入時會拋出 `NullReferenceException`。

## 步驟 3：為目標欄位指派數字格式

內建樣式編號因函式庫而異。以 Aspose.Cells 為例：

* `0` → 一般（整數）  
* `2` → 貨幣（例如 `$#,##0.00`）  
* `3` → 日期，等等。

此處 **為兩個欄位指派數字格式**：第一欄（Id）保留整數，第二欄（Amount）使用貨幣格式。

```csharp
// Column 0 → integer format (style number 0)
columnStyles[0].Number = 0;

// Column 1 → currency format (style number 2)
columnStyles[1].Number = 2;

// If you need a custom format, you can also use a format string:
// columnStyles[1].Custom = "$#,##0.00";
```

> **設定數字格式方式**：使用 `Number` 屬性是選取內建格式的最快方法。若需符合在地貨幣，請考慮使用自訂格式字串，加入相應的貨幣符號。

## 步驟 4：將 DataTable 匯入工作表，套用欄位樣式

樣式陣列準備好後，即可匯入資料。`ImportDataTable` 方法會遵循您傳入的樣式。

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];

// Import the DataTable, starting at cell A1 (row 0, column 0)
// The third argument (true) tells the method to write column headers.
ws.Cells.ImportDataTable(
    dataTable,
    /* includeColumnNames */ true,
    /* startRow */ 0,
    /* startColumn */ 0,
    columnStyles);

// Save the workbook
workbook.Save("FinancialReport.xlsx", SaveFormat.Xlsx);
```

### 預期結果

開啟 **FinancialReport.xlsx** 後，您會看到：

| 編號 | 金額        | 描述          |
|------|------------|--------------|
| 1    | $1,234.56  | 辦公用品      |
| 2    | $98,765.43 | 顧問費        |
| 3    | $0.99      | 雜項          |

***金額** 欄位會依您設定的貨幣格式顯示，而 **編號** 則保持整數。*

## 為其他情境設定數字格式的方法

### 為日期欄位指派數字格式

```csharp
// Suppose column 2 contains dates and you want "dd-MMM-yyyy"
columnStyles[2].Number = 14; // 14 = built‑in short date
```

### 使用自訂數字格式顯示百分比

```csharp
columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00%
```

### 超越數字格式的樣式設定

您也可以在同一個 `Style` 物件上設定字型、背景色或對齊方式：

```csharp
columnStyles[1].Font.IsBold = true;
columnStyles[1].ForegroundColor = Color.LightYellow;
columnStyles[1].HorizontalAlignment = TextAlignmentType.Center;
```

> **為什麼可行：** `Style` 物件會聚合儲存格的所有視覺屬性。將陣列傳給 `ImportDataTable` 後，每個儲存格會自動繼承已定義的樣式。

## 常見陷阱與避免方式

| 陷阱 | 症狀 | 解決方式 |
|------|------|----------|
| 忘記為每個 `Style` 實例化 | 匯入時拋出 `NullReferenceException` | 於陣列迴圈中呼叫 `CreateStyle()` 後再設定屬性。 |
| 使用錯誤的內建數字索引 | 格式錯誤（例如日期顯示為整數） | 查閱函式庫文件，取得正確的 `Number` 常數。 |
| 未儲存活頁簿 | 沒有輸出檔或檔案為空 | 匯入完成後呼叫 `workbook.Save(...)`。 |
| 貨幣符號的在地化不匹配 | 在非美國地區仍顯示 `$` | 使用自訂格式字串加入正確符號（例如 `"€#,##0.00"`）。 |

## 完整、可執行的範例



## 接下來您可以學習什麼？

以下教學與本篇內容緊密相關，能進一步深化您對 API 功能的掌握，並探索在專案中實作的其他方式。

- [Create excel file c# – style cells and set currency format](/cells/english/net/excel-formatting-and-styling/create-excel-file-c-style-cells-and-set-currency-format/)
- [How to Format Excel Columns in C# – Complete Guide](/cells/english/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/)
- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}