---
category: general
date: 2026-10-26
description: 使用 C# 停用 Excel 的自動篩選。本教學示範如何以程式方式從 Excel 表格中移除自動篩選，並提供完整的可執行範例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- disable autofilter in excel
- remove autofilter from excel table
- Excel automation C#
- Aspose.Cells filter handling
- programmatic Excel editing
language: zh-hant
lastmod: 2026-10-26
og_description: 快速停用 Excel 的自動篩選。跟隨本指南，使用 C# 與 Aspose.Cells 從 Excel 表格中移除自動篩選。
og_image_alt: Screenshot of an Excel worksheet where the autofilter has been disabled
og_title: 使用 C# 停用 Excel 自動篩選 – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  headline: How to disable autofilter in Excel with C# – complete guide
  type: TechArticle
- description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  name: How to disable autofilter in Excel with C# – complete guide
  steps:
  - name: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
    text: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
  - name: Click any column header – you should **not** see the drop‑down filter arrow.
    text: Click any column header – you should **not** see the drop‑down filter arrow.
  - name: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
    text: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: 如何在 Excel 中使用 C# 停用自動篩選 – 完整指南
url: /zh-hant/net/excel-autofilter-validation/how-to-disable-autofilter-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Excel 中使用 C# 停用自動篩選 – 完整指南

如果您需要 **在 Excel 中停用自動篩選**，本指南將一步步示範如何在 C# 中完成。無論是要在發佈前清理報表，或是自動化資料匯出流程，移除篩選後工作表會顯示所有列。您也會學會如何在單一次可靠的呼叫中 **從 Excel 表格中移除自動篩選**。

我們將使用廣受歡迎的 **Aspose.Cells for .NET** 套件，因為它不需要在伺服器上安裝 Excel。完成本教學後，您將擁有一個自包含的主控台應用程式，能載入活頁簿、找到第一個表格，並停用其自動篩選。此解決方案適用於 Excel 2007 及更新版本所產生的 .xlsx 檔案。

## 您需要的條件

| 前置條件 | 為何重要 |
|--------------|----------------|
| .NET 6.0 或更新版 | 為 C# 程式碼提供執行環境。 |
| Aspose.Cells for .NET（NuGet 套件 `Aspose.Cells`） | 提供對工作表、表格與自動篩選的程式化存取。 |
| 一個範例 Excel 檔案（`Sample.xlsx`），內含至少一個已套用自動篩選的表格 | 程式碼會作用於第一個表格；有表格才能示範停用篩選。 |
| Visual Studio 2022（或任何 C# IDE） | 讓建立與偵錯主控台應用程式變得簡單。 |

> **專業小技巧：** 若您偏好免費方案，也可以改寫程式碼改用 **ClosedXML** 或 **EPPlus**；核心概念—將表格的 `AutoFilter` 屬性設為 `null`—保持不變。

## 步驟 1：建立新的主控台專案

在終端機或 Visual Studio 命令提示字元中執行：

```bash
dotnet new console -n ExcelFilterDemo
cd ExcelFilterDemo
dotnet add package Aspose.Cells
```

此指令會建立名為 `ExcelFilterDemo` 的全新專案，並加入 Aspose.Cells 套件。

## 步驟 2：載入活頁簿並定位第一張工作表

第一個邏輯步驟是開啟活頁簿檔案。Aspose.Cells 會將檔案讀入 `Workbook` 物件，讓您直接存取工作表與表格。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the Excel file you want to modify
        const string inputPath = "Sample.xlsx";

        // Load the workbook into memory
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **為什麼需要這一步？** 在操作任何 Excel 物件之前必須先載入活頁簿。使用第一張工作表 (`Worksheets[0]`) 反映了大多數情況下主要資料位於第一張工作表的情境。

## 步驟 3：取得工作表上定義的第一個表格

Excel 表格（亦稱 ListObjects）是保存結構化資料的容器。每個表格都可以有自己的自動篩選。要移除篩選，我們必須先取得表格物件的參考。

```csharp
        // Get the first table on the worksheet.
        // If the worksheet has no tables, this will throw an IndexOutOfRangeException.
        Table table = worksheet.Tables[0];
```

> **邊緣情況：** 若活頁簿可能包含沒有表格的工作表，請在存取前加入 `if (worksheet.Tables.Count > 0)` 檢查。這可避免執行時錯誤，提升解決方案的韌性。

## 步驟 4：停用表格的自動篩選

實際的停用只需要一行程式碼：將 `Table` 物件的 `AutoFilter` 屬性指派為 `null`。這會清除所有篩選條件，並移除標題列的下拉箭頭。

```csharp
        // Disable the autofilter – this clears any applied filter.
        table.AutoFilter = null;
```

執行此行程式碼後，表格會像普通範圍一樣，沒有任何篩選 UI。

## 步驟 5：儲存已修改的活頁簿

最後，將變更寫回磁碟。您可以覆寫原始檔案，或另存新檔以保留來源檔。

```csharp
        // Save the workbook. Use a new file name to avoid overwriting the original.
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

### 完整原始碼

將所有片段組合起來，完整程式如下：

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the original Excel file
        const string inputPath = "Sample.xlsx";

        // Load the workbook
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (worksheet.Tables.Count == 0)
        {
            System.Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Get the first table
        Table table = worksheet.Tables[0];

        // Disable the autofilter – clears any applied filter
        table.AutoFilter = null;

        // Save the modified workbook
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

使用 `dotnet run` 執行程式。執行完畢後，於 Excel 開啟 `Sample_NoFilter.xlsx`；您會看到篩選箭頭已消失，所有列皆可見。

## 驗證自動篩選真的已移除

1. 在 Microsoft Excel 中開啟已儲存的檔案（`Sample_NoFilter.xlsx`）。  
2. 點擊任意欄位標題 – 您 **不應** 看到下拉篩選箭頭。  
3. 若仍看到箭頭，請再次確認您針對的表格確實是帶有篩選的那一個。您可以使用以下程式碼列出所有表格：

```csharp
foreach (var tbl in worksheet.Tables)
{
    System.Console.WriteLine($"Table name: {tbl.Name}, Has AutoFilter: {tbl.AutoFilter != null}");
}
```

主控台輸出應顯示該表格的 `Has AutoFilter: False`。

## 常見陷阱與避免方式

| 症狀 | 可能原因 | 解決方法 |
|---------|--------------|-----|
| `IndexOutOfRangeException` 發生於 `worksheet.Tables[0]` | 工作表沒有表格。 | 在存取前加入 `if (worksheet.Tables.Count == 0)` 防護。 |
| 儲存後的檔案仍顯示篩選 | 編輯了錯誤的工作表或表格。 | 使用 `wb.Worksheets["SheetName"]` 或遍歷 `wb.Worksheets` 以定位正確的表格。 |
| 程式在較舊的 .NET 版本上當機 | Aspose.Cells 需要 .NET 6.0 以上的最新套件。 | 在 `.csproj` 檔案中升級目標框架。 |
| `NullReferenceException` 發生於 `table.AutoFilter` 已為 null 時 | 您在同一檔案上重複呼叫程式碼而未重新載入。 | 重新載入活頁簿，或在指派前檢查 `if (table.AutoFilter != null)`。 |

## 擴充解決方案

既然您已掌握 **在 Excel 中停用自動篩選**，接下來可以考慮：

* **僅在特定條件成立時移除表格的自動篩選**（例如使用者旗標被設定）。在 `table.AutoFilter = null;` 前加上 `if` 判斷式。  
* **在清除舊篩選後程式化套用新篩選**，使用 `table.AutoFilter.Range` 以及 `table.AutoFilter.AddFilterColumn(...)`。  
* **一次處理多個表格**，透過迴圈遍歷 `worksheet.Tables`，對每個表格皆停用篩選。

這些擴充方式遵循上述相同模式，且能保持程式碼乾淨易維護。

## 結論

您現在已擁有一套簡潔、可投入生產環境的 **在 Excel 中停用自動篩選** 方法，使用 C# 只需載入活頁簿、存取第一個表格，並將 `table.AutoFilter = null`。如此即可 **從 Excel 表格中移除自動篩選**，不需手動操作。完整範例可編譯、執行，並產生一個乾淨的檔案，供後續自動化或分發使用。

歡迎自行嘗試額外的表格、條件邏輯或替代套件。若遇到任何邊緣情況，請回顧故障排除章節，或參考 Aspose.Cells 豐富的文件以取得進階篩選處理方式。祝您寫程式愉快！

## 接下來您可以學習什麼？

以下教學與本指南緊密相關，能進一步深化您在本主題的技巧。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，或在專案中探索替代實作方式。

- [How to remove autofilter from Excel tables using C#](/cells/english/net/excel-autofilter-validation/how-to-remove-autofilter-from-excel-tables-using-c/)
- [Clear filter UI in Excel with C# – Remove AutoFilter Button](/cells/english/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/)
- [How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide](/cells/english/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}