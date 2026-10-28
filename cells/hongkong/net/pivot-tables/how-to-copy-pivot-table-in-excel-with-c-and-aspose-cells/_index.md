---
category: general
date: 2026-10-04
description: 學習如何使用 C# 將樞紐分析表從一個工作簿複製到另一個工作簿。本指南亦涵蓋如何複製列、複製樞紐分析表，以及高效複製 Excel 範圍。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- how to copy rows
- duplicate pivot table
language: zh-hant
lastmod: 2026-10-04
og_description: 使用 C# 複製 Excel 樞紐分析表。請參考本完整教學，了解如何複製樞紐分析表、複製列以及使用 Aspose.Cells 複製
  Excel 範圍。
og_image_alt: Screenshot showing a duplicated pivot table in an Excel worksheet after
  using C# code
og_title: 使用 C# 複製 Excel 樞紐分析表 – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Learn how to copy pivot table from one workbook to another using C#.
    This guide also covers how to copy rows, duplicate pivot table, and copy Excel
    range efficiently.
  headline: How to copy pivot table in Excel with C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: 如何使用 C# 與 Aspose.Cells 複製 Excel 樞紐分析表
url: /zh-hant/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 C# 與 Aspose.Cells 複製 Excel 中的樞紐分析表

如果您需要將 **複製樞紐分析表** 從一個工作簿複製到另一個工作簿，本教學會提供完整且可執行的解決方案。您將會看到如何載入來源檔案、定義包含樞紐分析表的範圍、複製列（包括樞紐分析表的定義），以及儲存結果。無論您是在自動化報表流程或是建立遷移工具，以下步驟都能讓您只用幾行 C# 便複製樞紐分析表。

複製樞紐分析表不僅僅是複製儲存格值；底層的快取與欄位設定也必須一起搬移。此範例使用 **Aspose.Cells** 函式庫，因為它會自動處理樞紐分析表的中繼資料，讓您不必手動重建快取。完成本指南後，您將能安全地 **如何複製樞紐分析表**、**複製 Excel 範圍** 與 **如何複製列**。

## 前置條件

- 安裝 .NET 6.0 或更新版本（程式碼亦相容於 .NET Framework 4.7+）。
- 有效的 Aspose.Cells for .NET 授權或臨時評估授權。
- 兩個 Excel 檔案：`Source.xlsx`（包含您想要複製的樞紐分析表）以及一個空資料夾，將在其中寫入 `CopyWithPivot.xlsx`。
- Visual Studio 2022（或任何支援 C# 的 IDE）。

## 步驟 1：設定專案並加入 Aspose.Cells

建立一個新的主控台專案，並加入 Aspose.Cells NuGet 套件：

```bash
dotnet new console -n PivotCopyDemo
cd PivotCopyDemo
dotnet add package Aspose.Cells
```

此套件提供程式碼中使用的 `Workbook`、`Worksheet` 與 `CellArea` 類別。

## 步驟 2：載入包含樞紐分析表的來源工作簿

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Load the source workbook that holds the pivot you want to duplicate
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");
```

> **為何重要：** 載入工作簿會在記憶體中建立所有工作表的表示，包括任何隱藏的樞紐快取。若未載入檔案，您將無法參照樞紐分析表的範圍。

## 步驟 3：定義涵蓋樞紐分析表的儲存格區域

您必須告訴 Aspose.Cells 哪些列與欄屬於樞紐分析表。`CellArea` 結構允許您指定一個矩形區塊。

```csharp
        // Define the rectangle that encloses the pivot table (adjust as needed)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,      // first row (zero‑based)
            StartColumn = 0,   // first column
            EndRow = 30,       // last row of the pivot
            EndColumn = 10     // last column of the pivot
        };
```

> **提示：** 若不確定確切大小，請在 Excel 中開啟來源檔案，選取樞紐分析表，並在名稱方塊中查看顯示的範圍（例如 `A1:K31`）。將 Excel 座標轉換為零基索引以供程式碼使用。

## 步驟 4：建立新的目標工作簿並取得其第一個工作表

```csharp
        // Create an empty workbook that will receive the copied pivot
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

> **為何需要此步驟：** 必須先建立目標工作簿才能複製列。Aspose.Cells 會自動建立預設工作表，我們將使用它作為目標。

## 步驟 5：將列（包括樞紐分析表）從來源複製到目標

`CopyRows` 方法會同時複製儲存格值與底層的樞紐快取。

```csharp
        // Copy rows from source to destination, preserving the pivot definition
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,      // source cells
            sourceRange.StartRow,                 // first row to copy
            sourceRange.EndRow - sourceRange.StartRow + 1, // number of rows
            destWorksheet.Cells,                  // target cells
            sourceRange.StartRow);                // target start row
```

> **運作原理：**  
> - `CopyRows` 會接受來源工作表、起始列以及要複製的列數。  
> - 同時會接收目標工作表以及複製應開始的列。  
> - 因為來源範圍包含樞紐分析表，該方法會完整傳遞樞紐的快取、欄位清單與版面配置。這正是 **如何複製樞紐分析表** 而不失去功能的核心。

### 邊緣情況：複製跨多工作表的樞紐分析表

如果樞紐分析表的來源資料位於與樞紐本身不同的工作表，快取仍會隨複製一起移動，因為 Aspose.Cells 將快取儲存在工作簿而非工作表中。然而，您必須確保目標工作簿包含相同的來源資料範圍；否則樞紐會顯示 `#REF!` 錯誤。在此情況下，請先複製來源資料範圍，然後再複製樞紐列。

## 步驟 6：儲存已包含複製樞紐分析表的工作簿

```csharp
        // Persist the destination workbook to disk
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

執行程式後會產生 `CopyWithPivot.xlsx`，其內容與原始樞紐分析表完全相同，包含所有切片器、篩選條件與計算欄位。

### 預期輸出

開啟 `CopyWithPivot.xlsx` 時：

- 樞紐分析表出現在與 `Source.xlsx` 相同的位置（例如 A1:K31）。
- 所有列與欄標籤、總計以及格式均被保留。
- 重新整理樞紐分析表會顯示與來源相同的資料，證實快取已正確複製。

## 如何在沒有樞紐分析表的情況下複製列（copy excel range）

如果您只需要 **copy excel range** 而不涉及任何樞紐資料，可以使用相同的 `CopyRows` 方法，只是指向不含樞紐的範圍。例如：

```csharp
// Copy a simple data table from rows 5‑15, columns A‑D
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    4,            // start at row 5 (zero‑based)
    11,           // copy 11 rows (5‑15 inclusive)
    destWorksheet.Cells,
    0);           // paste at the top of the destination sheet
```

此範例示範了 **如何複製列** 用於一般資料，強調相同 API 的多功能性。

## 在同一工作簿中複製樞紐分析表（替代方法）

有時您想在同一工作簿內 **duplicate pivot table** 而非建立新檔案。您可以透過將列複製到其他位置來達成：

```csharp
// Duplicate pivot table to start at row 40 in the same worksheet
destWorksheet.Cells.CopyRows(
    srcWorkbook.Worksheets[0].Cells,
    sourceRange.StartRow,
    sourceRange.EndRow - sourceRange.StartRow + 1,
    destWorksheet.Cells,
    40); // destination start row (zero‑based)
```

儲存後，工作簿將包含兩個相同的樞紐分析表——適用於並排比較或建立備份。

## 常見陷阱與避免方法

| 問題 | 發生原因 | 解決方法 |
|---------|----------------|-----|
| 複製後樞紐分析表顯示 `#REF!` | 目標工作簿中不存在來源資料範圍 | 先複製來源資料範圍，或在複製樞紐之前於來源資料工作表上使用 `CopyRows` |
| 格式遺失 | 僅複製了值（例如使用 `Copy` 而非 `CopyRows`） | 始終使用 `CopyRows`，它會保留樣式、格式與樞紐中繼資料 |
| 列偏移異常 | 目標起始列與來源起始列不匹配 | 確認 `destWorksheet.Cells` 的起始列與預期位置相符 |
| 大型工作簿導致記憶體壓力 | `CopyRows` 會將整個工作表載入記憶體 | 將複製分批處理，或在處理超過 100,000 列時使用串流 API |

## 完整、可執行範例

以下是完整程式碼，您可以直接貼到 `Program.cs` 並立即執行（將 `YOUR_DIRECTORY` 替換為您機器上的實際路徑）。

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook containing the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY/Source.xlsx");

        // 2️⃣ Define the area that encloses the pivot (adjust to your sheet)
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 30,
            EndColumn = 10
        };

        // 3️⃣ Create the destination workbook (empty) and get its first sheet
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // 4️⃣ Copy rows—including the pivot cache—into the destination
        destWorksheet.Cells.CopyRows(
            srcWorkbook.Worksheets[0].Cells,
            sourceRange.StartRow,
            sourceRange.EndRow - sourceRange.StartRow + 1,
            destWorksheet.Cells,
            sourceRange.StartRow);

        // 5️⃣ Save the result
        destWorkbook.Save(@"YOUR_DIRECTORY/CopyWithPivot.xlsx");
        Console.WriteLine("Pivot table copied successfully.");
    }
}
```

使用 `dotnet run` 執行程式。執行完畢後，開啟 `CopyWithPivot.xlsx` 以驗證樞紐分析表是否與來源檔案完全相同。

## 結論

您現在已了解如何使用 C# 與 Aspose.Cells **copy pivot table** 從一個 Excel 工作簿複製到另一個。指南涵蓋了完整流程——從載入來源檔案、定義樞紐的儲存格區域、複製列，到儲存目標工作簿。您也學會了 **how to copy rows**、**copy excel range** 與在同一檔案中 **duplicate pivot table**，以及常見陷阱與最佳實踐建議。

準備好進一步了嗎？試著加入程式碼以程式化重新整理複製的樞紐分析表，或探索使用 Aspose.Cells 將樞紐匯出為 PDF。嘗試不同的來源範圍，您將快速掌握 .NET 中的 Excel 自動化。

---

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索替代實作方式。

- [在 C# 中複製樞紐分析表 – 完整步驟指南](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [建立新 Excel 工作簿 – 複製與重複樞紐分析表](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [複製 Excel 列 – 在重複列時保留樞紐分析表](/cells/english/net/pivot-tables/copy-rows-excel-preserve-pivot-table-while-duplicating-rows/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}