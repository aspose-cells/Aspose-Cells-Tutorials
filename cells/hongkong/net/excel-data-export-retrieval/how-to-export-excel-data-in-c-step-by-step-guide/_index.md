---
category: general
date: 2026-03-21
description: 如何使用 Aspose.Cells 在 C# 中匯出含欄位名稱的 Excel 資料、保留數字格式，並讀取特定列。學習如何讀取 Excel
  工作表並有效率地匯出指定列。
draft: false
keywords:
- how to export excel
- preserve number format
- export with column names
- read excel worksheet
- export specific rows
language: zh-hant
og_description: 如何使用 Aspose.Cells 匯出含欄位名稱的 Excel 資料、保留數字格式，並讀取特定列。提供完整可執行的 C# 開發者範例。
og_title: 如何在 C# 中匯出 Excel 資料 – 完整程式設計指南
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: 如何在 C# 中匯出 Excel 資料 – 步驟指南
url: /zh-hant/net/excel-data-export-retrieval/how-to-export-excel-data-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中匯出 Excel 資料 – 完整程式指南

有沒有想過 **如何匯出 Excel** 資料而不失去原始格式？也許你曾嘗試快速複製貼上，結果日期變成「44728」或缺少欄位標題。這真的很令人沮喪，對吧？在本教學中，你將看到一個乾淨、端到端的方式來讀取 Excel 工作表、保留數字格式、匯出欄位名稱，甚至只挑選你需要的列。

我們將使用 Aspose.Cells 函式庫，因為它提供對匯出選項的細緻控制。完成本指南後，你將擁有一段可重複使用的程式碼片段，能直接放入任何 .NET 專案，並且了解每個選項的重要性。無需外部文件——所有需要的資訊都在這裡。

---

## 你將學到什麼

- **讀取 Excel 工作表** 到記憶體中，使用 Aspose.Cells。
- **匯出特定列**（例如第 0‑49 列），同時保留欄位名稱。
- **保留數字格式**，讓貨幣、日期和百分比保持原樣。
- 如何 **匯出欄位名稱** 並在需要時包含儲存格註解。
- 完整、可直接執行的 C# 範例，並提供常見陷阱的技巧。

### 前置條件

- .NET 6.0 或更新版本（此程式碼亦相容 .NET Framework 4.6+）。
- 透過 NuGet 安裝 Aspose.Cells for .NET（`Install-Package Aspose.Cells`）。
- 一個 Excel 檔案（`input.xlsx`），放在可參考的資料夾中。

> **專業提示：** 若你在 CI 流程中，建議從私有 Feed 取得 NuGet 套件，以避免授權意外。

---

## 第一步 – 安裝 Aspose.Cells 並加入命名空間

首先，確保 Aspose.Cells 套件已加入你的專案。開啟 Package Manager Console 並執行：

```powershell
Install-Package Aspose.Cells
```

接著，在 C# 檔案的頂部加入必要的 `using` 指示詞：

```csharp
using Aspose.Cells;
using System.Data;
using System;
```

這些匯入讓你能使用 `Workbook`、`Worksheet`、`ExportTableOptions` 與 `DataTable`——即 **讀取 Excel 工作表** 並匯出資料的核心元件。

---

## 第二步 – 載入活頁簿（讀取 Excel 檔案）

現在我們真的要 **讀取 Excel 工作表**。`Workbook` 建構子接受檔案路徑，Aspose.Cells 會同時支援 `.xlsx` 與舊版 `.xls` 格式。

```csharp
// Step 2: Load the workbook containing the data
string filePath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(filePath);
```

> **為何重要：** 只載入一次活頁簿並重複使用相同的 `Worksheet` 物件，比起重複開啟檔案更有效率，尤其是面對大型試算表時。

---

## 第三步 – 設定匯出選項（保留數字格式與欄位名稱）

這裡我們告訴 Aspose.Cells *如何* 匯出。`ExportTableOptions` 類別讓我們能微調輸出。我們將啟用三個旗標：

1. `ExportAsString = true` – 強制每個儲存格皆轉為字串，確保數字保留其視覺表示。
2. `IncludeCellComments = true` – 複製儲存格上的任何註解（對文件說明很有幫助）。
3. `PreserveNumberFormat = true` – 保留原始的數字格式（貨幣符號、日期樣式等）。

```csharp
// Step 3: Configure export options to control how the table is exported
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export all values as strings
    IncludeCellComments = true,     // Preserve any cell comments
    PreserveNumberFormat = true     // Keep the original number formatting
};
```

> **邊緣情況：** 若將 `ExportAsString` 設為 `false`，但仍想保留數字格式，可能會得到原始數值（例如日期變成 44728）。同時開啟兩個旗標即可避免此情況。

---

## 第四步 – 取得第一個工作表（讀取 Excel 工作表）

大多數簡單檔案的資料都在第一張工作表，因此我們會依索引取得。如果需要其他工作表，只要將 `0` 換成相應的零基索引，或使用 `workbook.Worksheets["SheetName"]`。

```csharp
// Step 4: Get the first worksheet from the workbook
Worksheet firstWorksheet = workbook.Worksheets[0];
```

> **為何有用：** 直接存取工作表物件可完全控制其 `Cells` 集合，這對之後 **匯出特定列** 極為重要。

---

## 第五步 – 匯出儲存格範圍（匯出特定列）

現在進入本教學的核心：將第 0‑49 列與第 0‑4 欄（即前 50 列與前五欄）匯出至 `DataTable`。我們也會要求 Aspose.Cells 將欄位名稱作為 `DataTable` 的第一列。

```csharp
// Step 5: Export a range of cells (rows 0‑49, columns 0‑4) to a DataTable using the options
DataTable exportedTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 50,
    totalColumns: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

### 這段程式的作用

- **`startRow: 0`** – 從工作表最上方開始。
- **`totalRows: 50`** – 取得前 50 列（即 **匯出特定列**）。
- **`totalColumns: 5`** – 限制匯出至前五欄。
- **`includeColumnNames: true`** – 確保 `DataTable` 的欄位標題與 Excel 標題列相符，滿足 **匯出欄位名稱** 的需求。
- **`exportOptions`** – 套用第 3 步的設定，使數值保持如 “$1,234.56” 而非 “1234.56”。

---

## 第六步 – 驗證匯出結果（結果長什麼樣）

讓我們將前幾列印到主控台，看看格式是否仍然保留。

```csharp
// Step 6: Display a few rows to verify the export
Console.WriteLine("=== Exported DataTable Preview ===");
foreach (DataRow row in exportedTable.Rows)
{
    // Join each column with a tab for readability
    Console.WriteLine(string.Join("\t", row.ItemArray));
}
```

**預期輸出（範例）：**

```
=== Exported DataTable Preview ===
Date        Description    Amount   Tax   Total
01/02/2024  Widget A       $120.00  $12  $132.00
01/03/2024  Widget B       $200.00  $20  $220.00
...
```

請注意日期以 `MM/dd/yyyy` 格式顯示，且貨幣保留 `$` 符號——這全賴 **保留數字格式**。

---

## 常見陷阱與避免方法

| 問題 | 為何發生 | 解決方式 |
|-------|----------------|-----|
| 日期變成大數字 | `ExportAsString` 為 `false` | 保持 `ExportAsString = true` 或手動轉換儲存格 |
| 缺少欄位標題 | `includeColumnNames` 設為 `false` | 需要 **匯出欄位名稱** 時設為 `true` |
| 註解消失 | 未啟用 `IncludeCellComments` | 在 `ExportTableOptions` 中開啟 `IncludeCellComments` |
| 匯出錯誤的工作表 | 在多工作表檔案中使用 `Worksheets[0]` | 指定工作表名稱：`workbook.Worksheets["Data"]` |
| 超出範圍例外 | `totalRows` 超過實際列數 | 使用 `Math.Min(totalRows, worksheet.Cells.MaxDataRow + 1)` |

---

## 加分項：匯出整張工作表同時保留格式

如果之後需要整張工作表，只要將 `totalRows` 與 `totalColumns` 換成工作表的最大尺寸即可：

```csharp
int maxRows = firstWorksheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int maxCols = firstWorksheet.Cells.MaxDataColumn + 1;

DataTable fullTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: maxRows,
    totalColumns: maxCols,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

現在你擁有一個 **讀取 Excel 工作表** 的例程，適用於任何大小，同時 **保留數字格式** 並 **匯出欄位名稱**。

---

## 完整可執行範例（可直接複製貼上）

以下是完整程式碼，你可以直接放入 Console 應用程式。它包含所有步驟、匯入以及簡易的驗證列印。

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);

            // 2️⃣ Set export options (preserve number format, include comments, export as strings)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                IncludeCellComments = true,
                PreserveNumberFormat = true
            };

            // 3️⃣ Grab the first worksheet (read excel worksheet)
            Worksheet sheet = workbook.Worksheets[0];

            // 4️⃣ Export rows 0‑49, columns 0‑4 (export specific rows) with column headers
            DataTable table = sheet.Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: 50,
                totalColumns: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // 5️⃣ Show a preview
            Console.WriteLine("=== Exported DataTable Preview ===");
            foreach (DataRow row in table.Rows)
            {
                Console.WriteLine(string.Join("\t", row.ItemArray));
            }

            // Keep console open
            Console.WriteLine("\nExport complete. Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

將其儲存為 `Program.cs`，執行 `dotnet run`，即可在終端機看到格式化的預覽。

---

## 結論

我們剛剛示範了使用 Aspose.Cells **匯出 Excel** 資料的完整流程，涵蓋從載入活頁簿、保留數字格式、匯出欄位名稱，到限制匯出特定列的所有步驟。程式碼自成一體、可直接執行，且包含對常見邊緣情況的實用防護。

準備好接受下一個挑戰了嗎？試著直接匯出為 CSV 同時保留原始數字格式，或將 `DataTable` 推入 Entity Framework Core 以批次寫入資料庫。上述情境皆建立在本教學的基礎上。

如果你覺得本指南對你有幫助

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}