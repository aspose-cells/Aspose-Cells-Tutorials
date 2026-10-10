---
category: general
date: 2026-10-10
description: 學習如何使用 C# 刪除 Excel 活頁簿中的整行。本分步指南亦涵蓋如何依索引刪除行以及使用 Aspose.Cells 依索引移除行。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete entire row
- how to delete row
- remove row by index
- delete row excel
- delete row c#
language: zh-hant
lastmod: 2026-10-10
og_description: 使用 C# 刪除 Excel 工作簿中的整列。請參考本指南，了解如何依索引刪除列、移除列，以及安全儲存檔案。
og_image_alt: Screenshot of an Excel worksheet before and after deleting an entire
  row with C# code
og_title: 使用 C# 刪除 Excel 整列 – 完整程式設計指南
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to delete entire row in an Excel workbook with C#. This step‑by‑step
    guide also covers how to delete row by index and remove row by index using Aspose.Cells.
  headline: How to delete entire row in an Excel file using C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: 如何使用 C# 刪除 Excel 檔案中的整行
url: /zh-hant/net/row-and-column-management/how-to-delete-entire-row-in-an-excel-file-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 C# 刪除 Excel 檔案中的整列

如果您需要 **刪除整列**，本指南將一步步說明如何在 C# 中完成。無論是清理匯入的資料或是建立報表工具，以下步驟都能讓您依索引刪除列並儲存結果，而不會遺失其他資料。

您也會看到相同的做法如何回答 **如何依索引刪除列**、**如何依索引移除列**，以及為什麼它適用於 **delete row excel** 的情境。

## 前置條件

在開始之前，請確保您已具備：

* .NET 6.0 或更新版本（此程式碼亦相容 .NET Framework 4.6+）  
* **Aspose.Cells for .NET** 套件（可透過 NuGet 安裝：`Install-Package Aspose.Cells`）  
* 基本的 C# 主控台或桌面專案開發經驗  

不需要額外的 Excel Interop 或 COM 元件，讓解決方案保持輕量且適合在伺服器端執行。

## 步驟 1：建立專案並匯入命名空間

建立一個新的主控台應用程式（或將程式碼加入既有專案），並加入必要的 `using` 指令：

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // The rest of the tutorial code lives here.
        }
    }
}
```

*為什麼這很重要*：匯入 `Aspose.Cells` 後即可使用 `Workbook`、`Worksheet` 與 `DeleteRows` 方法，執行實際的列刪除動作。

## 步驟 2：載入活頁簿並選取工作表

必須先載入來源檔案 (`input.xlsx`) 並取得要修改的工作表。第一張工作表的索引為 `0`。

```csharp
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Get the first worksheet (you can also use workbook.Worksheets["SheetName"])
Worksheet ws = workbook.Worksheets[0];
```

> **小技巧**：若要操作特定工作表，請將索引改為工作表名稱，例如 `workbook.Worksheets["Data"]`。

## 步驟 3：依零基索引刪除整列

Aspose.Cells 使用零基索引，第一列為 `0`。若要刪除第 5 列（第六列的視覺位置），呼叫 `DeleteRows` 並傳入 `DeleteOptions.DeleteEntireRow`。

```csharp
// Delete one row starting at index 5 (zero‑based) and remove the whole row
ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
```

*說明*：

* `ws.Cells[5, 0]` 指向欲刪除列的第一個儲存格。  
* `DeleteRows(1, DeleteOptions.DeleteEntireRow)` 告訴 Aspose.Cells 刪除 **1** 列，且 `DeleteEntireRow` 旗標確保 **整列** 消失，下面的列會向上移動。

### 其他情境的依索引刪除列方式

* **刪除多列連續列** – 將第一個參數改成要刪除的列數：

  ```csharp
  // Remove rows 5, 6 and 7 (three rows total)
  ws.Cells[5, 0].DeleteRows(3, DeleteOptions.DeleteEntireRow);
  ```

* **刪除最後一列** – 使用 `ws.Cells.MaxDataRow` 取得最底部已填充列的索引：

  ```csharp
  int lastRow = ws.Cells.MaxDataRow;
  ws.Cells[lastRow, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
  ```

以上程式碼範例滿足 **remove row by index** 的需求，同時保持易讀性。

## 步驟 4：將工作簿儲存為已刪除列的檔案

完成刪除後，將修改過的活頁簿寫回磁碟。您可以覆寫原始檔案，或另存新檔。

```csharp
// Save the workbook to a new file (or overwrite the original)
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

若希望保留原始檔案，只需變更輸出路徑即可。`Save` 方法支援多種格式（`.xls`、`.csv`、`.pdf` 等），只要更改副檔名即可。

## 完整範例

以下為完整、可直接執行的程式碼：

```csharp
using System;
using Aspose.Cells;

namespace ExcelRowDeletion
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Select the first worksheet
            Worksheet ws = workbook.Worksheets[0];

            // 3️⃣ Delete the entire row at index 5 (sixth visual row)
            ws.Cells[5, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);

            // 4️⃣ Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");

            Console.WriteLine("Row deleted successfully. Output saved to output.xlsx");
        }
    }
}
```

**預期結果**：執行程式後，`output.xlsx` 會保留所有原始列，唯獨第 6 列（視覺上）的資料已被移除。被刪除列以下的資料會自動向上移動，公式與格式亦會同步更新。

## 常見問題與避免方式

| 問題 | 為什麼會發生 | 解決方法 |
|------|--------------|----------|
| **索引超出範圍** | 嘗試刪除不存在的列索引（例如在 200 列的工作表中使用 `ws.Cells[1000,0]`） | 在呼叫 `DeleteRows` 前，使用 `ws.Cells.MaxDataRow` 檢查最高有效索引。 |
| **僅刪除部分列** | 未傳入 `DeleteOptions.DeleteEntireRow` 只會清除儲存格內容 | 需要整列刪除時，務必傳入 `DeleteOptions.DeleteEntireRow`。 |
| **公式意外變更** | 刪除屬於公式範圍的列會破壞參照 | 若活頁簿依賴動態範圍，刪除後請呼叫 `workbook.CalculateFormula()` 重新計算公式。 |
| **儲存至唯讀位置** | 若目錄受保護，`Save` 會拋出例外 | 確認目標資料夾具寫入權限，或以適當的權限執行程式。 |

解決上述問題後，解決方案即可在正式環境中穩定運作，滿足 **delete row excel** 與 **delete row c#** 的搜尋需求。

## 進階：依條件刪除列

有時需要移除符合特定條件的列（例如欄位 A 為空的列）。以下迴圈示範了從下往上掃描並安全刪除符合條件的列：

```csharp
int lastRow = ws.Cells.MaxDataRow;
for (int row = lastRow; row >= 0; row--)
{
    // Check if column A (index 0) is empty
    if (ws.Cells[row, 0].StringValue == string.Empty)
    {
        ws.Cells[row, 0].DeleteRows(1, DeleteOptions.DeleteEntireRow);
    }
}
workbook.Save("YOUR_DIRECTORY/cleaned.xlsx");
```

自底向上掃描可避免在迭代過程中因刪除列而產生的索引位移問題。

## 結論

現在您已掌握如何使用 C# **刪除 Excel 活頁簿中的整列**。本指南涵蓋：

* 載入活頁簿並選取工作表  
* 使用 `DeleteRows` 搭配 `DeleteOptions.DeleteEntireRow` 進行 **how to delete row** 依索引刪除  
* 安全儲存修改後的檔案  
* 邊緣案例處理、效能建議與條件刪除範例  

有了這些知識，您可以自信地實作 **remove row by index** 功能、自動化資料清理，並將 Excel 操作整合至任何 C# 應用程式中。

**下一步**：探索 Aspose.Cells 其他功能，如插入列、複製範圍，或將活頁簿轉為 PDF——這些皆以您剛學會的 `Workbook` 與 `Worksheet` 物件為基礎。祝開發順利！

## 接下來該學什麼？

以下教學與本篇內容緊密相關，能進一步深化您對相關 API 的掌握，並提供替代實作方式的完整範例與步驟說明。

- [如何使用 Aspose.Cells .NET 刪除 Excel 列：完整指南](/cells/english/net/worksheet-management/delete-excel-row-aspose-cells-net-tutorial/)
- [Aspose.Cells 刪除列 – 保護 Excel 標題列](/cells/english/net/row-and-column-management/aspose-cells-delete-rows-protect-header-row-in-excel/)
- [使用 Aspose.Cells for Java 高效管理 Excel 列：插入與刪除列](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}