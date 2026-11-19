---
category: general
date: 2026-11-19
description: 學習如何在 C# 中從 Excel 刪除表格。本教學亦示範如何使用 C# 讀取 Excel 檔案以及載入 Excel 工作簿，並提供完整的程式碼範例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete table from excel
- read excel file c#
- how to remove table excel
- load excel workbook c#
- how to delete excel table
language: zh-hant
lastmod: 2026-11-19
og_description: 快速在 C# 中刪除 Excel 表格。跟隨本指南閱讀 Excel 檔案 C# 並載入 Excel 工作簿 C#，附有實作範例。
og_image_alt: Screenshot of C# code that deletes a table from an Excel worksheet
og_title: 在 C# 中從 Excel 刪除表格 – 完整程式設計指南
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to delete table from Excel in C#. This tutorial also shows
    how to read Excel file C# and load Excel workbook C# with a complete code example.
  headline: How to delete table from Excel using C# – step‑by‑step guide
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: 使用 C# 從 Excel 刪除表格的逐步指南
url: /zh-hant/net/tables-and-lists/how-to-delete-table-from-excel-using-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 C# 刪除 Excel 表格 – 步驟指南

如果您需要以程式方式 **delete table from Excel**，本指南將向您展示如何使用 C# 完成此操作。您將看到一個完整、可執行的範例，該範例載入 Excel 活頁簿、刪除第一個表格，並儲存結果。同樣的模式也涵蓋 **read excel file c#** 與 **load excel workbook c#**，因此您可以將其套用到任何自動化情境。

在 .NET 中處理 Excel 檔案通常需要可靠的函式庫。本教學使用 **Aspose.Cells**，這是一個完整管理的 API，支援表格、公式與豐富的格式設定，且不需要在伺服器上安裝 Microsoft Office。步驟簡潔、程式碼自給自足，您也能了解每一行程式碼的重要性。

## 您將能達成的目標

* 將現有的 `.xlsx` 檔案載入記憶體。
* 在工作表中定位並刪除表格（亦稱 ListObject）。
* 將修改後的活頁簿儲存為新檔案。
* 擴充此方法以處理多個表格或表格不存在的情況。

不需要事先具備 Aspose.Cells 的使用經驗——只要具備基本的 C# 知識即可。

## 前置條件

* .NET 6.0 SDK 或更新版本（程式碼亦相容於 .NET Core 3.1 與 .NET Framework 4.6+）。
* Visual Studio 2022（或任何支援 .NET 專案的編輯器）。
* **Aspose.Cells** NuGet 套件。使用以下方式安裝：

```bash
dotnet add package Aspose.Cells
```

* 一個包含至少一個表格的 Excel 檔案（`input.xlsx`）。若沒有，請在 Excel 中建立簡易表格，並儲存於專案相同資料夾下。

---

## 步驟 1：在 C# 中載入 Excel 活頁簿

第一個任務是從磁碟讀取活頁簿。這是 **load excel workbook c#** 的核心。

```csharp
using Aspose.Cells;
using System;

class ExcelTableRemover
{
    static void Main()
    {
        // Define file paths
        const string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        const string outputPath = @"YOUR_DIRECTORY\output.xlsx";

        // Step 1: Load the workbook
        Workbook workbook = new Workbook(inputPath);
```

**為何這很重要：**  
`Workbook` 代表整個 Excel 檔案於記憶體中。一次載入後即可執行多項操作——讀取儲存格、修改表格或變更格式——而不必重複開啟檔案。

---

## 步驟 2：存取第一個工作表（read excel file c#）

活頁簿載入後，您需要取得包含表格的工作表參考。

```csharp
        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];
```

**說明：**  
`Worksheets` 是零基索引集合，`[0]` 會回傳第一張工作表。若您的檔案布局不同，請改用索引或 `workbook.Worksheets["SheetName"]`。

---

## 步驟 3：從工作表中刪除表格

現在執行核心 **delete table from excel** 操作。範例會移除第一個表格，但相同邏輯適用於任何表格索引。

```csharp
        // Step 3: Delete the first table in the worksheet
        if (worksheet.Tables.Count > 0)
        {
            // Table[0] is the first ListObject on the sheet
            worksheet.Tables[0].Delete();
            Console.WriteLine("Table deleted successfully.");
        }
        else
        {
            Console.WriteLine("No tables found on the worksheet.");
        }
```

**為何此方法有效：**  
`Tables` 是 `ListObject` 物件的集合。呼叫 `Delete()` 會同時移除表格定義 *以及* 其底層資料範圍，留下普通儲存格。`if` 判斷式實作了 **how to remove table excel** 的安全檢查，避免在工作表沒有表格時拋出例外。

**小技巧：**  
若需要依名稱而非位置刪除表格，可使用 `worksheet.Tables["TableName"].Delete();`。當活頁簿包含多個表格且只想針對特定表格時，此方式相當有用。

---

## 步驟 4：儲存修改後的活頁簿（how to delete excel table）

最後，將變更寫回磁碟。這完成了 **how to delete excel table** 的工作流程。

```csharp
        // Step 4: Save the modified workbook
        workbook.Save(outputPath);
        Console.WriteLine($"Modified workbook saved to {outputPath}");
    }
}
```

**底層發生的事情：**  
`Save` 會產生一個新的 `.xlsx` 檔案，反映所有記憶體中的變更。原始的 `input.xlsx` 保持不變，這是生產環境腳本的安全做法。

---

## 完整、可執行的範例

將所有片段組合起來，以下是您可以直接複製、貼上並執行的完整程式：

```csharp
using Aspose.Cells;
using System;

class ExcelTableRemover
{
    static void Main()
    {
        // Paths – adjust to your environment
        const string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        const string outputPath = @"YOUR_DIRECTORY\output.xlsx";

        // Load the workbook (load excel workbook c#)
        Workbook workbook = new Workbook(inputPath);

        // Get the first worksheet (read excel file c#)
        Worksheet worksheet = workbook.Worksheets[0];

        // Delete the first table (delete table from excel)
        if (worksheet.Tables.Count > 0)
        {
            worksheet.Tables[0].Delete();
            Console.WriteLine("Table deleted successfully.");
        }
        else
        {
            Console.WriteLine("No tables found on the worksheet.");
        }

        // Save the changes (how to delete excel table)
        workbook.Save(outputPath);
        Console.WriteLine($"Modified workbook saved to {outputPath}");
    }
}
```

**預期輸出**

```
Table deleted successfully.
Modified workbook saved to YOUR_DIRECTORY\output.xlsx
```

在 Excel 中開啟 `output.xlsx`；您剛剛移除的表格現在會以普通儲存格形式顯示，仍保留原始資料。

---

## 處理常見的邊緣案例

| 情況 | 建議做法 |
|-----------|----------------------|
| **Multiple tables** | 迴圈 `worksheet.Tables` 並刪除每個表格，或使用 `worksheet.Tables["MyTable"].Delete();` 依名稱刪除。 |
| **Table does not exist** | `if (worksheet.Tables.Count > 0)` 防護已避免 `NullReferenceException`。您也可以記錄警告以供稽核。 |
| **Large files** | 使用 `Workbook.LoadOptions` 以 **memory‑efficient** 模式開啟檔案（例如 `LoadOptions { MemorySetting = MemorySetting.MemoryPreference };`）。 |
| **Preserve formatting** | 刪除表格會移除其樣式。若需保留視覺樣式，請在呼叫 `Delete()` 前將樣式複製到目標範圍。 |

---

## 效能提示：批次操作

如果需要在多個工作表上刪除大量表格，請將所有變更集中於同一個 `Workbook` 實例，並在全部刪除完成後僅呼叫一次 `workbook.CalculateFormula()`。相較於每次刪除後即重新計算，這可減少 CPU 負擔。

---

## 下一步

現在您已掌握 **how to remove table excel** 與 **delete table from excel**，接下來可能想要：

* **Read Excel file C#** 用於在表格移除後擷取資料。`Cells` 集合讓您遍歷列與欄。
* 使用 `worksheet.Tables.Add()` 程式化產生新表格——對報表情境很有用。
* 探索其他 Aspose.Cells 功能，如圖表操作、樞紐分析表或條件格式設定。

上述主題皆以您剛剛使用的 `Workbook` 與 `Worksheet` 物件為基礎，因而易於套用與擴充。

---

## 結論

您已學會如何使用 C# **delete table from Excel**。本指南涵蓋了載入活頁簿、存取工作表、安全移除表格以及儲存更新檔案的完整流程，並提供可直接執行的範例。憑藉此基礎，您可以自動化任何 Excel 為基礎的工作流程，無論是 **read excel file c#**、**load excel workbook c#**，或是更複雜的 **how to delete excel table** 情境。

隨意嘗試多個表格、不同工作表，或改用 EPPlus 等開源函式庫。祝您開發順利！

## 接下來該學什麼？

以下教學與本指南所示技巧緊密相關，並提供完整的程式碼範例與逐步說明，協助您掌握更多 API 功能或探索替代實作方式。

- [閱讀 Excel 檔案 C# – 如何有效載入 Excel 活頁簿 C#](/cells/english/net/loading-and-saving-excel-files-with-options/read-excel-file-c-how-to-load-excel-workbook-c-efficiently/)
- [如何在 C# 中刪除 Excel 表格的列並變更其名稱](/cells/english/net/tables-and-lists/how-to-delete-rows-from-an-excel-table-and-change-its-name-i/)
- [如何使用 C# 重新命名 Excel 表格 – 步驟指南](/cells/english/net/tables-and-lists/how-to-rename-table-in-excel-with-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}