---
category: general
date: 2026-03-18
description: 如何在 C# 中將 Excel 資料匯出至 DataTable，並使用程式碼處理特定儲存格、將 Excel 轉換為 DataTable 以及格式化數字。了解匯出特定儲存格等更多技巧。
draft: false
keywords:
- how to export excel
- convert excel to datatable
- export specific cells
- excel to datatable c#
- excel range to datatable
language: zh-hant
og_description: 如何在 C# 中將 Excel 資料匯出至 DataTable。本教學示範如何匯出特定儲存格、將 Excel 轉換為 DataTable，並輕鬆格式化數字。
og_title: 如何在 C# 中將 Excel 匯出至 DataTable – 完整指南
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: 如何在 C# 中將 Excel 匯出為 DataTable – 步驟教學
url: /zh-hant/net/excel-data-import-export/how-to-export-excel-to-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中將 Excel 匯出至 DataTable – 步驟說明指南

有沒有想過 **如何將 Excel** 資料匯入 `DataTable` 而不失去格式？你並不是唯一有此需求的人——開發人員常常需要將試算表的一部分讀入記憶體，以便進行報表、驗證或大量插入操作。好消息是？只要幾行 C# 程式碼，就能匯出精確的範圍（例如 *A1:F11*），強制所有儲存格以字串形式處理，甚至套用自訂的數字格式。

在本教學中，我們將涵蓋所有必要的知識：從載入活頁簿、設定 **export specific cells**、將範圍轉換為 `DataTable`，到處理空白列或受語系影響的數字等邊緣情況。完成後，你將擁有一個可重複使用的方法，能在 **excel to datatable c#** 的實務情境中運作。

> **先決條件** – 你需要 Aspose.Cells for .NET 函式庫（或任何提供 `ExportDataTable` 的類似 API）。此範例假設使用 .NET 6 以上，但概念同樣適用於較早的版本。

---

## 你將學到什麼

- 如何使用 Aspose.Cells **將 Excel 轉換為 DataTable**。
- 匯出自訂範圍（`excel range to datatable`），同時將所有值視為字串。
- 在匯出時套用兩位小數的數字格式（`#,#00.00`）。
- 常見陷阱（空列、隱藏欄）以及避免方式。
- 可直接複製、完整可執行的程式碼範例。

## 先決條件與設定

在深入程式碼之前，請先確保你已完成以下設定：

1. **Aspose.Cells for .NET** 透過 NuGet 安裝：

   ```bash
   dotnet add package Aspose.Cells
   ```

2. 將 Excel 檔案（`input.xlsx`）放置於可參照的資料夾，例如 `YOUR_DIRECTORY/input.xlsx`。
3. 建立目標 .NET 6 或更新版本的專案（下方的 `using` 陳述式可直接使用）。

> **專業提示：** 若你使用其他函式庫（例如 EPPlus 或 ClosedXML），概念仍相同——載入活頁簿、選取範圍，然後呼叫回傳 `DataTable` 的方法。

## 步驟 1：載入活頁簿並取得第一個工作表

首先，你需要一個代表 Excel 檔案的 `Workbook` 物件。取得後，即可依索引或名稱存取任意工作表。

```csharp
using Aspose.Cells;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];

            // Continue with export options...
        }
    }
}
```

**為什麼重要：** 先載入活頁簿可讓你檢查其結構（隱藏工作表、保護設定），再決定要匯出的儲存格。若檔案很大，建議使用 `LoadOptions` 僅串流所需部分。

## 步驟 2：設定匯出選項 – 將所有值視為字串

當你為後續處理（例如大量插入至 SQL）匯出資料時，通常希望有 **一致的字串表示**，以避免之後的型別不匹配錯誤。

```csharp
// Configure export behavior
ExportTableOptions exportOptions = new ExportTableOptions
{
    // Force every cell to be returned as a string, regardless of its original type
    ExportAsString = true,

    // Apply a two‑decimal‑place format to numeric cells
    NumberFormat = "#,##0.00"
};
```

**說明：**  
- `ExportAsString = true` 告訴 Aspose.Cells 忽略原始儲存格型別，直接回傳格式化後的文字。  
- `NumberFormat = "#,##0.00"` 確保像 `1234.5` 這樣的數字會變成 `"1,234.50"`——對財務報表非常實用。

若你需要保留原始資料型別，只要將 `ExportAsString` 設為 `false`，自行處理轉換即可。

## 步驟 3：匯出特定範圍 (A1:F11) 至 DataTable

現在進入 **export specific cells** 的核心。`ExportDataTable` 方法接受起始與結束的列/欄索引（零基礎）以及是否包含標頭的旗標。

```csharp
// Export cells A1:F11 (rows 0‑10, columns 0‑5) including the header row
DataTable table = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    endRow: 10,
    endColumn: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

**你會得到：** 一個包含 11 列（含標頭）與 6 欄（`A`‑`F`）的 `DataTable`。所有值皆依 `exportOptions` 以字串形式格式化。

## 步驟 4：驗證結果 – 輸出至主控台

在將資料表交給其他元件之前，先做一次簡單的驗證是個好習慣。

```csharp
// Simple console dump
foreach (DataRow row in table.Rows)
{
    foreach (var item in row.ItemArray)
    {
        Console.Write($"{item}\t");
    }
    Console.WriteLine();
}
```

你應該會看到類似以下的輸出：

```
Id      Name        Qty     Price   Total   Date
1       Widget A    10      2.50    25.00   2026-01-01
2       Widget B    5       3.75    18.75   2026-01-02
...
```

注意數值欄位顯示了兩位小數，正如我們設定的那樣。

## 完整可執行範例（可直接複製）

以下是把所有步驟串起來的完整程式。將它放入新的 Console 專案，調整檔案路徑後執行——不需要額外設定。

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load workbook and select worksheet
            // -------------------------------------------------
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -------------------------------------------------
            // 2️⃣ Set export options – strings + number format
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                NumberFormat = "#,##0.00"
            };

            // -------------------------------------------------
            // 3️⃣ Export range A1:F11 (rows 0‑10, cols 0‑5)
            // -------------------------------------------------
            DataTable table = worksheet.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                endRow: 10,
                endColumn: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // -------------------------------------------------
            // 4️⃣ Output to console for verification
            // -------------------------------------------------
            Console.WriteLine("=== Exported DataTable ===");
            foreach (DataRow row in table.Rows)
            {
                foreach (var cell in row.ItemArray)
                {
                    Console.Write($"{cell}\t");
                }
                Console.WriteLine();
            }

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**程式碼重點：**

- `ExportTableOptions` 物件可重複使用；若需匯出多個範圍，可將其傳遞給多次 `ExportDataTable` 呼叫。
- 索引從 **0** 開始，因此 `A1` 對應為 `(0,0)`。
- 將 `includeColumnNames` 設為 `true` 會自動使用第一列作為欄位標題——對後續的 `DataTable` 操作非常有用。

## 處理邊緣情況與常見問題

### 若工作表有隱藏列或欄該怎麼辦？

Aspose.Cells 預設會遵守可見性。若需匯出隱藏資料，請將 `exportOptions.ExportHiddenRows = true` 與 `ExportHiddenColumns = true` 設為 `true`。

### 我的 Excel 檔案包含公式——會取得計算後的值嗎？

會的。預設情況下 `ExportDataTable` 會回傳 **顯示值**（即公式的計算結果）。若想取得原始公式文字，請將 `exportOptions.ExportFormulas = true`。

### 如何跳過完全空白的列？

匯出完成後，你可以自行修剪 `DataTable`：

```csharp
foreach (DataRow row in table.Rows.Cast<DataRow>()
                                   .Where(r => r.ItemArray.All(c => c == DBNull.Value || string.IsNullOrWhiteSpace(c.ToString()))).ToList())
{
    table.Rows.Remove(row);
}
```

### 能否匯出非連續範圍（例如 A1:B5 與 D1:E5）？

Aspose.Cells 不支援在單一次呼叫中匯出不相連的範圍。建議分別匯出每個區塊，之後手動合併產生的 `DataTable`。

## 效能建議

- **重複使用 `ExportTableOptions`** 以進行多次匯出；每次建立新實例雖然開銷微乎其微，卻會使程式碼變雜。  
- **使用 `LoadOptions` 串流大型檔案**，避免將整個活頁簿載入記憶體。  
- **避免使用 `DataTable`** 若只需快速匯出 CSV——`ExportDataTable` 雖然方便，但對於巨量工作表而言不是最省記憶體的方式。

## 結論

我們已示範 **如何將 Excel** 資料匯入 `DataTable`，同時控制格式、處理特定儲存格範圍，並確保每個值皆以字串形式呈現。完整範例展示了一個乾淨、適合上線的作法，你可以依此套用於 **convert excel to datatable**、**export specific cells** 或任何 **excel range to datatable** 的情境。

歡迎自行嘗試：變更範圍、切換 `ExportAsString`，或直接將 `DataTable` 丟給 Entity Framework 進行大量插入。只要有這個堅實基礎，未來的可能性無限。

### 後續步驟與相關主題

- **將 DataTable 匯入回 Excel** – 了解使用 `ImportDataTable` 的反向操作。  
- **將 DataTable 大量插入 SQL Server** – 使用 `SqlBulkCopy` 進行閃電般的載入。  
- **使用 EPPlus 或 ClosedXML** – 了解使用其他函式庫時相同任務的寫法。  
- **匯出時格式化儲存格** – 進一步探索 `ExportTableOptions` 的日期格式、客製化文化設定等功能。

有任何問題或不同的使用情境嗎？留下評論，我們一起討論。祝程式開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}