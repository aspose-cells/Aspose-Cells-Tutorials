---
category: general
date: 2026-03-25
description: 快速學習如何在 C# 中將 Excel 匯出至 DataTable。本教學涵蓋帶欄位名稱的 Excel 匯出，以及將 Excel 資料匯出為字串，以確保資料處理的可靠性。
draft: false
keywords:
- export excel to datatable
- how to export excel to datatable
- export excel with column names
- export excel data as string
language: zh-hant
og_description: 將 Excel 匯出至 C# 的 DataTable，保留欄位名稱並轉換為字串。遵循此簡潔教學，即可獲得可直接執行的解決方案。
og_title: 匯出 Excel 至 DataTable（C#）— 完整指南
tags:
- C#
- Aspose.Cells
- DataTable
- Excel
title: 在 C# 中將 Excel 匯出至 DataTable – 步驟教學
url: /zh-hant/net/excel-data-import-export/export-excel-to-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中將 Excel 匯出至 DataTable – 步驟指南

曾經需要 **export Excel to DataTable**，卻不確定要設定哪些旗標嗎？你並不孤單——許多開發者在首次嘗試將試算表資料拉入 `DataTable` 時，都會碰到同樣的障礙。  

好消息是？只要幾行程式碼，就能 **export Excel with column names**，甚至 **export Excel data as string**，避免類型不匹配的頭痛問題。以下提供完整、可執行的範例，並說明每個設定背後的「原因」，讓你能毫無猜測地套用到任何專案。

## 本教學涵蓋內容

* 如何在記憶體中建立 Workbook（不需要實體檔案）。  
* 填入幾筆範例資料，讓你立即看到匯出結果。  
* 設定 `ExportTableOptions`，讓每個儲存格皆以字串形式處理。  
* 將矩形範圍匯出至 `DataTable`，同時保留第一列作為欄位名稱。  
* 驗證輸出結果，並將第一列印出至主控台。  

不需要外部文件連結——所有資訊都在此。如果你已經有 Excel 檔案在磁碟上，只要將建立 Workbook 的程式碼改為 `new Workbook("path/to/file.xlsx")` 即可使用。

---

## 步驟 1：設定專案並加入 Aspose.Cells NuGet 套件

在撰寫任何程式碼之前，請確保你的專案已參考 **Aspose.Cells for .NET**（提供 `Workbook` 類別的函式庫）。你可以透過 NuGet 套件管理員加入：

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** 使用最新的穩定版（截至 2026 年 3 月，為 22.12）以取得最新的錯誤修正與效能提升。

---

## 步驟 2：建立 Workbook 並填入範例資料

我們將從全新的 `Workbook` 開始，寫入幾列資料，讓你看到匯出實際運作的樣子。此步驟同時示範 **how to export excel to datatable**，當來源資料僅存在於記憶體時的做法。

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();                 // in‑memory workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Populate a few cells – this mimics a real Excel file
        worksheet.Cells["A1"].PutValue("Name");   // column header
        worksheet.Cells["B1"].PutValue("Age");    // column header
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);
```

*Why this matters:* 先插入標頭列 (`A1` & `B1`)，之後即可告訴匯出程式將第一列視為欄位名稱——這正是 **export excel with column names** 的意義。

---

## 步驟 3：告訴 Aspose.Cells 將每個儲存格視為字串

當你匯出數值或日期儲存格時，Aspose 會嘗試推斷 .NET 類型。若下游程式碼預期的是字串，這可能會導致隱蔽的錯誤。`ExportTableOptions.ExportAsString` 旗標會強制統一的字串轉換。

```csharp
        // 3️⃣ Configure export options – all values will be strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true       // <-- ensures Export Excel Data As String
        };
```

*Why use this?* 想像一個欄位有時是數字、有時是文字（例如 “00123” 與 “ABC”）。將所有內容匯出為字串即可避免前導零遺失或觸發類型轉換例外。

---

## 步驟 4：將指定範圍匯出至 DataTable

現在我們真正 **export excel to datatable**。`ExportDataTable` 方法接受起始列/欄、列數/欄數、欄位名稱提取旗標，以及剛才建立的選項。

```csharp
        // 4️⃣ Export rows 0‑9 and columns 0‑4 (adjust as needed)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,   // <-- uses the first row as headers
            exportOptions: exportOptions);
```

*What’s happening under the hood?*  
- `startRow: 0` 指向第一個 Excel 列（即標頭列）。  
- `exportColumnNames: true` 告訴 Aspose 將 “Name” 與 “Age” 提升為 `DataTable` 的欄位集合。  
- `totalRows`/`totalColumns` 可以大於實際資料；多餘的儲存格會因 `ExportAsString` 而變成空字串。

---

## 步驟 5：驗證結果 – 印出第一列

快速的主控台輸出證明轉換成功且欄位名稱完整。

```csharp
        // 5️⃣ Show the first data row (if any)
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

**Expected output**

```
First row: Alice, 30
```

如果你更改了範例資料，主控台會自動反映這些變更——不需要額外程式碼。

---

## 常見問題與邊緣情況

| Question | Answer |
|----------|--------|
| **Can I export a sheet that already exists on disk?** | Yes—replace `new Workbook()` with `new Workbook("myFile.xlsx")`. The rest of the steps stay identical. |
| **What if my Excel file has merged cells?** | Merged cells are unwrapped; the top‑left cell’s value is used for the entire merged range. |
| **Do I need to worry about culture‑specific number formats?** | Not when `ExportAsString = true`; everything arrives as the raw string shown in Excel. |
| **How many rows can I export at once?** | Aspose.Cells can handle millions of rows, but memory consumption grows with the size of the `DataTable`. Consider paging if you hit limits. |
| **What about hidden columns?** | Hidden columns are exported unless you set `ExportHiddenColumns = false` in `ExportTableOptions`. |

---

## 加分項：匯出至 CSV 而非 DataTable

有時你可能較偏好平面檔案。相同的 `ExportTableOptions` 可搭配 `ExportDataTableToCSV` 重複使用：

```csharp
        string csvPath = "output.csv";
        worksheet.Cells.ExportDataTableToCSV(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            csvPath,
            exportColumnNames: true,
            exportOptions);
        Console.WriteLine($"CSV written to {csvPath}");
```

這行程式碼即可產生可直接匯入的 CSV，同時仍然 **export excel data as string**。

---

## 完整可執行範例（直接複製貼上）

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate sample data (header + two rows)
        worksheet.Cells["A1"].PutValue("Name");
        worksheet.Cells["B1"].PutValue("Age");
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);

        // Export everything as strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true
        };

        // Export range to DataTable (first row = column names)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,
            exportOptions: exportOptions);

        // Display first row
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

執行程式 (`dotnet run`) 後，你會在主控台看到 **export excel to datatable** 的結果。替換範例資料、調整 `totalRows`/`totalColumns`，或將 Workbook 指向真實檔案——一切皆可擴展。

---

## 結論

你現在擁有一套 **complete, self‑contained solution for exporting Excel to DataTable** 的完整方案。透過設定 `ExportTableOptions.ExportAsString`，即可保證 **export excel data as string**；而將 `exportColumnNames: true` 設為 true，則可取得在 **export excel with column names** 時期望的欄位標頭。  

從此你可以：

* 將 `DataTable` 注入 Entity Framework 或 Dapper 進行批次寫入。  
* 傳遞給像 **FastReport** 或 **RDLC** 的報表引擎。  
* 轉換為 JSON 作為 API 回應 (`JsonConvert.SerializeObject(table)`)。

盡情實驗吧——或許可以嘗試匯出更大的工作表，或結合 **how to export excel to datatable** 從網路共享匯出。模式保持不變，程式碼已可直接投入生產環境。

---

![Diagram of Excel → DataTable conversion flow – export excel to datatable](https://example.com/placeholder.png "export excel to datatable diagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}