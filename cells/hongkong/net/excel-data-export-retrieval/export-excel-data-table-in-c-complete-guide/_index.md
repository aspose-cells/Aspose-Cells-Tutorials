---
category: general
date: 2026-03-21
description: 使用 Aspose.Cells 將 Excel 資料表匯出為 DataTable（含標題列），限制小數位數，並僅匯出前 100 列。
draft: false
keywords:
- export excel data table
- export excel to datatable
- limit decimal places excel
- export first 100 rows
- export excel with headers
language: zh-hant
og_description: 學習如何將 Excel 資料表匯出為 DataTable，保留標題、限制小數位數，並在 C# 中抓取前 100 行。
og_title: 在 C# 中匯出 Excel 資料表 – 步驟教學
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: 在 C# 中匯出 Excel 資料表 – 完整指南
url: /zh-hant/net/excel-data-export-retrieval/export-excel-data-table-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 匯出 Excel 資料表 – 完整 C# 教學

需要 **將 Excel 資料表** 從活頁簿匯出成 .NET `DataTable` 嗎？您來對地方了——本指南會一步步說明如何完成，保留欄位標題、限制小數位數，並僅取得前 100 筆資料。  

如果您曾盯著試算表想「怎麼把它帶入我的應用程式而不失去格式？」您並不孤單。接下來的幾分鐘，我們會把這個「如果」變成可直接複製貼上的解決方案，使用 Aspose.Cells 這個受歡迎的 Excel 操作函式庫。

## 您將學會

- 如何使用 `ExportDataTable` 方法 **匯出 excel 到 datatable**。  
- 如何保留原始欄位名稱（`export excel with headers`）。  
- 如何透過設定 `ExportTableOptions` **限制 excel 小數位數**。  
- 如何安全地只取得前 100 筆資料（`export first 100 rows`）。  

不需要外部腳本，也不需要神奇字串——只要純粹的 C# 程式碼，您可以直接放入任何 .NET 專案。

## 前置條件

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6 或更新版本（或 .NET Framework 4.7+） | Aspose.Cells 同時支援兩者，但較新的執行環境提供 async‑ready API。 |
| Aspose.Cells for .NET NuGet 套件 | 提供 `Workbook`、`ExportTableOptions` 與 `ExportDataTable` 輔助功能。 |
| 範例 Excel 檔（例如 `Numbers.xlsx`） | 您將要匯出的資料來源。 |
| 基本 C# 知識 | 您只需要跟著程式碼片段操作，無需進階技巧。 |

如果上述任一項您不熟悉，請使用 `dotnet add package Aspose.Cells` 取得 NuGet 套件，並建立一個含有少量數字的簡易 Excel 檔作為測試資料。

![匯出 excel 資料表範例](excel-data-table.png "將要匯出至 DataTable 的 Excel 工作表截圖")

## 步驟 1：載入活頁簿（export excel data table）

首先您需要一個指向 Excel 檔案的 `Workbook` 實例。把它想成在閱讀任何章節前先打開一本書。

```csharp
using Aspose.Cells;

// 1️⃣ Load the workbook that contains the source data
Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");
```

> **為什麼重要：** 載入活頁簿後，您才能存取其工作表、儲存格與樣式。若檔案路徑錯誤，Aspose 會拋出 `FileNotFoundException`，請務必確認位置正確。

## 步驟 2：設定匯出選項 – limit decimal places excel

預設情況下，Aspose 會以完整精度匯出所有數值。通常您只需要少數有效位數，尤其是要將資料送入 UI 表格或需要四捨五入的 API 時。

```csharp
using Aspose.Cells;

// 2️⃣ Configure export options – keep only 4 significant digits
ExportTableOptions exportOptions = new ExportTableOptions
{
    // This property trims the number of significant digits.
    SignificantDigits = 4
};
```

> **小技巧：** 若您需要不同的四捨五入策略（例如永遠向上取整），可以在匯出後對 `DataTable` 進行後處理。`SignificantDigits` 設定是 **限制 excel 小數位數** 最快速的方式，無需額外迴圈。

## 步驟 3：匯出指定範圍（export first 100 rows）

現在告訴 Aspose 我們要把哪一塊儲存格拉進 `DataTable`。本教學示範抓取前 100 行與前 10 欄，您可自行調整數字以符合需求。

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

> **邊緣情況：** 若工作表少於 100 行，Aspose 只會匯出實際存在的資料，不會拋錯。但您可能想要防範意外過小的範圍：

```csharp
int rowsToExport = Math.Min(100, workbook.Worksheets[0].Cells.MaxDataRow + 1);
```

## 步驟 4：驗證結果 – 快速 Console 輸出

在除錯器中看到資料固然不錯，但將幾筆資料印到主控台可以確認 **匯出 excel 到 datatable** 已正確執行，且小數位已被裁減。

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

### 預期輸出

```
ID      Name    Score   Ratio   Date        ...
1       Alice   95.12   0.8234  2023-01-15  ...
2       Bob     88.5    0.7612  2023-01-16  ...
3       Carol   73.33   0.6721  2023-01-17  ...
...
```

您會發現數值欄位現在只顯示四位有效數字，正好對應先前設定的 `SignificantDigits = 4`。

## 步驟 5：完整封裝 – 可執行範例

以下是完整程式碼，您可以直接複製貼上到 Console 應用程式。內含錯誤處理、可選的列數保護，以及列印輔助方法。

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

執行程式後，您將看到工作表的前 100 行，已經四捨五入且欄位名稱完整保留。

## 常見問題與注意事項

| Question | Answer |
|----------|--------|
| **如果工作表有合併儲存格怎麼辦？** | `ExportDataTable` 會以左上角儲存格的值展平合併儲存格。若需要自訂處理，請先取消合併或直接讀取原始 `Cell` 物件。 |
| **可以匯出到 `DataSet` 嗎？** | 可以——使用 `ExportDataTable` 後再將結果加入 `DataSet` 即可。 |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}