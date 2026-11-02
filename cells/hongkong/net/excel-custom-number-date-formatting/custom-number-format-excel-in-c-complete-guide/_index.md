---
category: general
date: 2026-03-22
description: 自訂數字格式 Excel 教學，示範如何將資料表匯入 Excel、設定欄位背景顏色、將欄位格式化為貨幣，並將工作簿另存為 xlsx。
draft: false
keywords:
- custom number format excel
- import datatable to excel
- set column background color
- format column as currency
- save workbook as xlsx
language: zh-hant
og_description: 自訂數字格式 Excel 教學，逐步帶您匯入 DataTable、設定欄位背景顏色、將欄位格式化為貨幣，並將工作簿另存為 xlsx。
og_title: C# 中的 Excel 自訂數字格式 – 步驟教學
tags:
- C#
- Excel automation
- Aspose.Cells
- Data export
title: C# 中的 Excel 自訂數字格式 – 完整指南
url: /zh-hant/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 自訂數字格式 Excel – 全端 C# 教學

你是否曾想過如何直接從 C# 套用 **custom number format excel** 樣式？也許你曾把 DataTable 匯入試算表，結果只看到純數字，沒有顏色，也沒有貨幣格式。這是常見的痛點——尤其在需要為利害關係人提供精緻報告時。

在本教學中，我們將一起解決這個問題：你將學會 **import datatable to excel**、**set column background color**、**format column as currency**，以及最終 **save workbook as xlsx**，使用自訂數字格式讓你的數據更醒目。沒有模糊的說明，僅提供完整、可直接複製貼上的可執行範例。

---

## 你將建立的內容

完成本教學後，你將擁有一個自包含的 C# 主控台應用程式，具備以下功能：

1. 取得一個 `DataTable`（你可以自行替換成自己的查詢）。  
2. 使用 Aspose.Cells（或任何相容的函式庫）建立新的 Excel 活頁簿。  
3. 為第一欄套用藍色粗體字型，為第二欄套用淡黃色背景，為第三欄套用貨幣格式（`$#,##0.00`）。  
4. 將檔案儲存為 `DataTableWithStyleArray.xlsx`，存放於你指定的資料夾。

你將清楚看到每一行程式碼如何影響最終的 Excel 檔案，並討論為何這些選擇對可維護性與效能很重要。

---

## 前置條件

- .NET 6.0 或更新版本（此程式碼亦相容 .NET Framework 4.7+）。  
- Aspose.Cells for .NET（免費試用或正式授權版）。透過 NuGet 安裝：

```bash
dotnet add package Aspose.Cells
```

- 具備 `DataTable` 與 C# 主控台應用程式的基本概念。

---

## Step 1: Retrieve the Source Data as a DataTable

首先，我們需要一些資料來匯出。實務上你可能會呼叫資料庫或執行 SQL 查詢。此處為說明起見，我們直接在記憶體中建立一個簡易表格。

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetSampleData()
{
    var table = new DataTable("Sales");
    table.Columns.Add("Product", typeof(string));
    table.Columns.Add("Quantity", typeof(int));
    table.Columns.Add("Revenue", typeof(decimal));

    table.Rows.Add("Widget A", 120, 3450.75m);
    table.Rows.Add("Widget B", 85, 2190.00m);
    table.Rows.Add("Widget C", 60, 1580.40m);

    return table;
}
```

> **Why this matters:** 使用 `DataTable` 能提供具結構的表格來源，能直接對應到 Excel 的列與欄。它也讓你可以在任何資料集上重複使用相同的匯出邏輯，而不必重新撰寫程式碼。

---

## Step 2: Create a New Workbook and Grab the First Worksheet

現在我們建立一個 Excel 活頁簿。`Workbook` 類別代表整個檔案；`Worksheets[0]` 為預設工作表，我們將資料寫入此工作表。

```csharp
// Initialize a fresh workbook
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet
Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** 若需要多個工作表，只要呼叫 `workbook.Worksheets.Add("SheetName")`，然後對每個工作表重複樣式設定步驟即可。

---

## Step 3: Define Column Styles – Font, Background, and Number Format

在 Aspose.Cells 中，樣式是透過 `Style` 物件來設定。我們會建立一個陣列，每個元素對應 DataTable 中的欄位。

```csharp
// Prepare an array to hold three distinct styles
Style[] columnStyles = new Style[3];

// 1️⃣ First column – blue, bold font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = System.Drawing.Color.Blue;
columnStyles[0].Font.IsBold = true;

// 2️⃣ Second column – light‑yellow background
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
columnStyles[1].Pattern = BackgroundType.Solid;

// 3️⃣ Third column – custom currency format (custom number format excel)
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Custom = "$#,##0.00";
```

> **Why a style array?** 將陣列傳入 `ImportDataTable` 可在一次呼叫中為每一欄套用不同的樣式，既簡潔又具效能。此方式也確保格式與資料順序保持同步。

---

## Step 4: Import the DataTable While Applying the Styles

以下是核心操作：將 `DataTable` 匯入工作表，告訴 Aspose 包含標題列，並傳入我們的 `columnStyles` 陣列。

```csharp
// Import data starting at cell A1 (row 0, column 0)
worksheet.Cells.ImportDataTable(
    GetSampleData(),   // source DataTable
    true,              // include column names as header
    0, 0,              // start row, start column
    columnStyles);     // apply the style array
```

> **What happens under the hood?** Aspose 會逐欄遍歷，先寫入標題，接著寫入每一列的值。寫入過程中會套用陣列中對應的 `Style`，因此最終會得到「Product」欄位的藍色標題、「Quantity」欄位的淡黃色底色，以及「Revenue」欄位的貨幣格式。

---

## Step 5: Save the Workbook as an XLSX File

最後，我們將活頁簿寫入磁碟。`Save` 方法會根據檔案副檔名自動選擇 XLSX 格式。

```csharp
// Choose a folder that exists on your machine
string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";

// Ensure the directory exists (optional safety check)
System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);

// Save the workbook
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

> **Tip:** 若需要將檔案以串流方式傳送（例如 Web API），請使用 `workbook.Save(stream, SaveFormat.Xlsx)` 取代檔案路徑。

---

## Full Working Example

以下是完整程式碼，你可以直接貼到新的主控台專案中。它可以直接編譯執行，產生具樣式的 Excel 檔案。

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Get data
            DataTable dataTable = GetSampleData();

            // Step 2 – Create workbook & worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 3 – Prepare column styles
            Style[] columnStyles = new Style[3];

            // Font style for first column (blue, bold)
            columnStyles[0] = workbook.CreateStyle();
            columnStyles[0].Font.Color = System.Drawing.Color.Blue;
            columnStyles[0].Font.IsBold = true;

            // Background style for second column (light yellow)
            columnStyles[1] = workbook.CreateStyle();
            columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
            columnStyles[1].Pattern = BackgroundType.Solid;

            // Currency format for third column (custom number format excel)
            columnStyles[2] = workbook.CreateStyle();
            columnStyles[2].Custom = "$#,##0.00";

            // Step 4 – Import data with styles
            worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

            // Step 5 – Save as XLSX
            string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";
            System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }

        // Helper method to build a demo DataTable
        static DataTable GetSampleData()
        {
            var table = new DataTable("Sales");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Revenue", typeof(decimal));

            table.Rows.Add("Widget A", 120, 3450.75m);
            table.Rows.Add("Widget B", 85, 2190.00m);
            table.Rows.Add("Widget C", 60, 1580.40m);

            return table;
        }
    }
}
```

### Expected Result

開啟 `DataTableWithStyleArray.xlsx` 後，你會看到：

| **產品** (藍色、粗體) | **數量** (淡黃色) | **收入** (貨幣) |
|----------------------|-------------------|----------------|
| Widget A             | 120               | $3,450.75      |
| Widget B             | 85                | $2,190.00      |
| Widget C             | 60                | $1,580.40      |

你所指定的 **custom number format excel** (`$#,##0.00`) 會讓每個收入欄位顯示美元符號、千位分隔符與兩位小數——正是財務團隊所期待的格式。

---

## Frequently Asked Questions & Edge Cases

### 可以改用其他 Excel 函式庫嗎？

當然可以。建立每欄樣式並在匯入時套用的概念，同樣適用於 EPPlus、ClosedXML 或 NPOI。API 呼叫方式不同，但整體流程保持一致。

### 如果我的 DataTable 欄位比樣式陣列多，會怎樣？

Aspose 會對沒有對應樣式的欄位使用預設樣式。為避免意外，請將陣列長度調整為 `dataTable.Columns.Count`，或在迴圈中動態產生樣式。

### 如何為日期設定自訂數字格式？

只要設定 `style.Custom = "dd‑mm‑yyyy"`（或任何有效的 Excel 格式字串）即可。相同的陣列方式同樣適用於日期、百分比或科學記號。

### 匯入後可以自動調整欄寬嗎？

可以——在匯入完成後呼叫 `worksheet.AutoFitColumns();`，系統會根據儲存格內容自動計算適當寬度。

### 大量資料（10 萬筆以上）會有問題嗎？

`ImportDataTable` 已針對批次操作做過最佳化，但仍可能受記憶體限制。若遇到此情況，可改為手動逐列寫入 `Cells[i, j].PutValue(...)`，並重複使用單一 `Style` 物件以降低開銷。

---

## Pro Tips & Common Pitfalls

- **Avoid hard‑coding paths**：在正式環境中請避免硬寫路徑，改用 `Environment.GetFolderPath` 或設定檔取得路徑。  
- **Dispose of the workbook**：若程式長時間執行，請將 workbook 包在 `using` 區塊中，以釋放本機資源。  
- **Watch out for culture‑specific separators**：自訂格式 `$#,##0.00` 會強制使用點號作為小數點，不受作業系統語系影響，這通常是財務報表的需求。  
- **Remember to reference System.Drawing**（或 .NET Core 上的 `System.Drawing.Common`），以取得樣式中使用的顏色結構。  
- **Test the output on different Excel versions**：舊版 Excel 可能會對某些自訂格式的解讀略有差異，請務必測試相容性。

---

## Conclusion

We’ve covered everything you need to **custom number format excel** files from C#: pulling data from a `DataTable`, **import datatable to excel**, applying a **set column background color**, using **format column as currency**, and finally **save workbook as x

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}