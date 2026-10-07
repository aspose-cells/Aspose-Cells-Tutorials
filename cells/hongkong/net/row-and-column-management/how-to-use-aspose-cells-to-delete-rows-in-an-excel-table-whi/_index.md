---
category: general
date: 2026-10-07
description: 了解如何使用 Aspose.Cells 從 Excel 表格中刪除行、刪除除標題外的所有行，以及在受保護的表格中以乾淨的 C# 程式碼處理行刪除。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- aspose cells delete rows
- delete rows excel table
- excel table row deletion
- protect excel table rows
- remove rows except header
language: zh-hant
lastmod: 2026-10-07
og_description: Aspose.Cells 從 Excel 表格中刪除列，同時保留標題列。本指南展示完整的 C# 解決方案，處理受保護的表格及常見的邊緣案例。
og_image_alt: Aspose.Cells delete rows example showing code and Excel screenshot
og_title: Aspose.Cells 刪除列 – 在 C# 中移除除標題外的所有列
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how Aspose.Cells delete rows from an Excel table, remove rows
    except header, and handle protected table row deletion with clean C# code.
  headline: How to use Aspose.Cells to delete rows in an Excel table while keeping
    the header
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: 如何使用 Aspose.Cells 刪除 Excel 表格中的列，同時保留表頭
url: /zh-hant/net/row-and-column-management/how-to-use-aspose-cells-to-delete-rows-in-an-excel-table-whi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.Cells 刪除 Excel 表格中的列，同時保留標題列

如果您需要 **aspose cells delete rows** 從表格中刪除列但保留標題列，本指南提供完整且可執行的解決方案。您將了解為何在表格受保護時直接呼叫 `ListObject.DeleteRows` 會失敗，以及如何在不影響資料完整性的情況下繞過此限制。

本教學涵蓋：

* 載入包含受保護表格的活頁簿。  
* 偵測並暫時解除表格保護。  
* 刪除所有資料列，同時保留標題列。  
* 恢復原始的保護狀態。  

閱讀完本文後，您即可在任何 Aspose.Cells 專案中可靠地執行 **delete rows excel table** 操作。

## 前置條件

* .NET 6.0 或更新版本（程式碼亦可在 .NET Framework 4.7.2+ 上執行）。  
* Aspose.Cells for .NET 23.9 或更新版本。  
* 具備 C# 與 Excel 表格（亦稱 ListObjects）的基本知識。  

除了 Aspose.Cells 之外，無需其他 NuGet 套件。

## 步驟 1：設定專案並匯入命名空間

建立新的主控台應用程式，或將以下程式碼加入現有專案。匯入 Aspose.Cells 的命名空間，使編譯器能解析 `Workbook`、`Worksheet` 與 `ListObject`。

```csharp
using System;
using Aspose.Cells;

namespace AsposeCellsTableRowDeletion
{
    class Program
    {
        static void Main()
        {
            // The full solution starts in Step 2.
        }
    }
}
```

*此步驟的重要性* – 匯入正確的命名空間可避免型別衝突錯誤，並讓後續程式碼更易讀。

## 步驟 2：載入活頁簿並定位目標表格

將 `"YOUR_DIRECTORY/TableProtection.xlsx"` 替換為您的 Excel 檔案路徑。範例假設您要修改的表格名稱為 **Orders**。

```csharp
// Load the workbook that contains the protected table
Workbook workbook = new Workbook("YOUR_DIRECTORY/TableProtection.xlsx");

// Get the first worksheet (index 0) and the ListObject named "Orders"
Worksheet worksheet = workbook.Worksheets[0];
ListObject ordersTable = worksheet.ListObjects["Orders"];
```

*此步驟的重要性* – 取得 `ListObject` 可直接操作表格，這是執行任何 **excel table row deletion** 操作的前提。

## 步驟 3：檢查表格是否受保護

當表格受保護時，Aspose.Cells 會阻止部分列的刪除。此時若嘗試 `ordersTable.DeleteRows` 會拋出例外。請先偵測保護狀態。

```csharp
bool wasProtected = ordersTable.IsProtected;
Console.WriteLine($"Table protection status: {(wasProtected ? "protected" : "unprotected")}");
```

*此步驟的重要性* – 瞭解保護狀態後，您可決定是否暫時解除保護，確保在操作後遵守 **protect excel table rows** 規則。

## 步驟 4：暫時解除表格保護（如有需要）

若表格受保護，請使用 `Unprotect` 並提供密碼（若有）。對於未設定密碼的表格，只需呼叫 `Unprotect()` 即可。

```csharp
if (wasProtected)
{
    // Provide the password if the table was protected with one; otherwise, pass null.
    ordersTable.Unprotect(null);
    Console.WriteLine("Table temporarily unprotected.");
}
```

*此步驟的重要性* – 解除表格保護後，Aspose.Cells 可執行 **aspose cells delete rows** 而不拋出例外，且稍後仍可重新設定保護。

## 步驟 5：刪除除標題列外的所有列

標題列位於表格的第一列（`RowCount` 包含標題列）。從索引 1 開始刪除即可移除所有資料列。

```csharp
int dataRows = ordersTable.RowCount - 1; // Exclude the header row
if (dataRows > 0)
{
    ordersTable.DeleteRows(1, dataRows);
    Console.WriteLine($"{dataRows} data rows removed, header preserved.");
}
else
{
    Console.WriteLine("Table contains only the header; nothing to delete.");
}
```

*此步驟的重要性* – 此程式碼實作核心的 **remove rows except header** 功能，同時避免在受保護表格上執行部分刪除時產生的例外。

## 步驟 6：重新套用保護（若原本已設定）

列刪除完成後，恢復原本的保護狀態，使活頁簿的行為與之前完全相同。

```csharp
if (wasProtected)
{
    // Re‑apply protection with the same password (null if none was used)
    ordersTable.Protect(null);
    Console.WriteLine("Table protection restored.");
}
```

*此步驟的重要性* – 恢復保護符合 **protect excel table rows** 的需求，並確保活頁簿對後續使用者保持安全。

## 步驟 7：儲存已修改的活頁簿

請選擇新檔名以避免覆寫原始檔案，除非您確實需要覆寫。

```csharp
string outputPath = "YOUR_DIRECTORY/TableProtection_Modified.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Modified workbook saved to: {outputPath}");
```

*此步驟的重要性* – 儲存可完成 **excel table row deletion** 操作，並產生可在 Excel 中開啟驗證的實際結果。

## 完整可執行範例

將所有步驟整合後，即得到一個可自行複製、貼上並執行的完整程式。

```csharp
using System;
using Aspose.Cells;

namespace AsposeCellsTableRowDeletion
{
    class Program
    {
        static void Main()
        {
            // 1. Load workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/TableProtection.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];
            ListObject ordersTable = worksheet.ListObjects["Orders"];

            // 2. Remember protection state
            bool wasProtected = ordersTable.IsProtected;
            Console.WriteLine($"Table protection status: {(wasProtected ? "protected" : "unprotected")}");

            // 3. Unprotect if needed
            if (wasProtected)
            {
                ordersTable.Unprotect(null); // use password if applicable
                Console.WriteLine("Table temporarily unprotected.");
            }

            // 4. Delete all rows except header
            int dataRows = ordersTable.RowCount - 1;
            if (dataRows > 0)
            {
                ordersTable.DeleteRows(1, dataRows);
                Console.WriteLine($"{dataRows} data rows removed, header preserved.");
            }
            else
            {
                Console.WriteLine("Table contains only the header; nothing to delete.");
            }

            // 5. Restore protection
            if (wasProtected)
            {
                ordersTable.Protect(null); // re‑apply with original password if any
                Console.WriteLine("Table protection restored.");
            }

            // 6. Save the workbook
            string outputPath = "YOUR_DIRECTORY/TableProtection_Modified.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"Modified workbook saved to: {outputPath}");
        }
    }
}
```

### 預期輸出

```
Table protection status: protected
Table temporarily unprotected.
5 data rows removed, header preserved.
Table protection restored.
Modified workbook saved to: YOUR_DIRECTORY/TableProtection_Modified.xlsx
```

在 Excel 中開啟 `TableProtection_Modified.xlsx`。您會看到 **Orders** 表格僅剩標題列，所有資料列皆已被移除。

## 處理常見變化與邊緣案例

| 情況 | 建議調整 | 原因 |
|-----------|-------------------|--------|
| 表格使用密碼 | 將密碼傳遞給 `Unprotect` 與 `Protect` | 確保操作後維持相同的安全等級 |
| 表格沒有資料列 | 跳過 `DeleteRows` 呼叫 | 避免拋出 `ArgumentOutOfRangeException` |
| 需要清理多個表格 | 遍歷 `worksheet.ListObjects` 並套用相同邏輯 | 將 **delete rows excel table** 模式擴展至整個工作表 |
| 想保留標題列與第一筆資料列 | 將 `DeleteRows(2, dataRows‑1)` 改為相應值 | 從第二列開始刪除，保留第一筆資料列 |

這些變化展示了對 **excel table row deletion** 的健全處理，並說明為何此方法是最佳建議。

## 專業提示

* **Batch processing** – 如果需要從多個活頁簿刪除列，請將邏輯封裝在接受 `Workbook` 與 `tableName` 參數的可重用方法中。  
* **Performance** – 一次呼叫 (`DeleteRows`) 刪除列的效能較逐列刪除快，因為 Aspose.Cells 只會更新內部資料結構一次。  
* **Safety** – 在套用刪除前，務必先在原始檔案的副本上操作或保留備份，特別是涉及 **protect excel table rows** 時。  

## 結論

您現在擁有一套完整、可投入生產環境的 **aspose cells delete rows** 解決方案，能在保留 Excel 表格標題列的同時刪除資料列。本指南說明了如何載入活頁簿、處理受保護的表格、執行 **remove rows except header** 操作，以及恢復保護。將此模式套用於任何 **excel table row deletion** 情境，並依需求調整程式碼，例如處理有密碼保護的表格或批次處理。

---

*下一步* – 探索相關主題，例如使用 **delete rows excel table** 搭配篩選、刪除列後合併儲存格，或使用 Aspose.Cells 在活頁簿之間複製表格。這些皆建立在本指南的核心概念之上，並深化您使用 Aspose.Cells 進行 Excel 自動化的能力。

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通其他 API 功能，並在專案中探索替代實作方式。

- [Aspose Cells 刪除列 – 在 Excel 中保護標題列](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [如何使用 Aspose.Cells for .NET 在 Excel 中插入與刪除列：完整指南](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [如何使用 Aspose.Cells .NET 刪除 Excel 中的空白列以進行資料清理](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}