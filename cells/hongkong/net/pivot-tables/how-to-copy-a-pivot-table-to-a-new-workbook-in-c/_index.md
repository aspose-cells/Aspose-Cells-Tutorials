---
category: general
date: 2026-11-16
description: 如何使用 C# 從一個 Excel 檔案將樞紐分析表複製到新工作簿。學習載入工作簿、複製範圍，並保留樞紐分析表。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new workbook
- load excel workbook c#
- Aspose.Cells copy pivot
- preserve pivot table C#
- Excel automation C#
language: zh-hant
lastmod: 2026-11-16
og_description: 如何使用 C# 從現有工作簿複製樞紐分析表至新工作簿。請參考本完整指南，了解如何載入 Excel 工作簿、複製範圍，並保持樞紐分析表完整。
og_image_alt: how to copy pivot table example in C#
og_title: 如何在 C# 中將樞紐分析表複製到新工作簿 – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  headline: How to copy a pivot table to a new workbook in C#
  type: TechArticle
- description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  name: How to copy a pivot table to a new workbook in C#
  steps:
  - name: Expected output
    text: 'Running the program produces `CopyWithPivot.xlsx`. Opening the file in
      Excel shows:'
  - name: Copying multiple pivot tables
    text: If your source sheet contains several pivots, expand the `CellArea` to cover
      the union of all ranges, or repeat the copy step for each distinct area.
  - name: Preserving styles and conditional formatting
    text: '`CopyRows` copies cell styles automatically. If you need to preserve workbook‑wide
      named styles or custom number formats, call `destWorkbook.Worksheets[0].CopyStyle`
      before saving.'
  - name: Working with large workbooks
    text: For files larger than 100 MB, consider using `Workbook.LoadOptions` with
      the `MemorySetting` set to `MemorySetting.MemoryPreference` to reduce memory
      pressure.
  - name: Next steps
    text: '* Explore **Aspose.Cells** features such as refreshing pivots programmatically.
      * Combine this approach with **ExcelPackage** (EPPlus) if you need an open‑source
      alternative. * Automate copying across multiple sheets by looping through `srcWorkbook.Worksheets`.'
  type: HowTo
- questions:
  - answer: Aspose.Cells can read macro‑enabled files (`.xlsm`), but the macro code
      isn’t copied. The pivot table itself is preserved because it’s part of the worksheet
      XML.
    question: Does this work with macros or VBA‑enabled workbooks?
  - answer: The copy operation includes the cached data only. If the destination workbook
      needs to refresh from the original source, you’ll have to re‑configure the data
      connection manually.
    question: What if the pivot uses an external data source?
  - answer: 'No. A pivot table needs its cache. The most reliable way is to copy the
      rows that contain the cache, as demonstrated. You can later hide those rows
      if you don’t want them visible. ## Conclusion You now know **how to copy pivot
      table** from one Excel file to another using C#. The tutorial covered **l'
    question: Can I copy the pivot without the underlying data rows?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: 如何在 C# 中將樞紐分析表複製到新工作簿
url: /zh-hant/net/pivot-tables/how-to-copy-a-pivot-table-to-a-new-workbook-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中將樞紐分析表複製到新活頁簿

如果您需要 **how to copy pivot table** 從一個 Excel 檔案複製到全新的活頁簿，本指南會向您展示具體步驟。您將學習如何 **load excel workbook c#**、定義來源範圍，並 **copy range to new workbook** 同時保持樞紐分析表完整。

複製樞紐分析表是常見需求，當您想重複使用報告範本、在專案之間遷移資料，或產生輕量化的檔案以供分發時。以下程式碼範例使用 Aspose.Cells，一個完整管理的 .NET 函式庫，無需安裝 Microsoft Office 即可運作。完成本教學後，您將擁有一個可執行的程式，能建立包含原始樞紐分析表的新活頁簿，供進一步處理或分享。

## 前置條件

* .NET 6.0 SDK 或更新版本（此範例適用於 .NET Core 與 .NET Framework）
* Visual Studio 2022 或您偏好的任何 C# 編輯器
* Aspose.Cells for .NET 授權（免費試用可用於評估）
* 包含至少一個樞紐分析表的來源 Excel 檔案（`Source.xlsx`）

> **Pro tip:** 如果您使用免費試用版，請在程式碼中設定授權，以避免評估浮水印。

## 第一步：載入來源活頁簿（load excel workbook c#）

第一步是開啟包含樞紐分析表的活頁簿。Aspose.Cells 會將檔案讀入記憶體，讓您完整存取工作表、儲存格與樞紐物件。

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Load the source workbook that contains the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");
```

*Why this matters*：載入活頁簿是任何 Excel 自動化的基礎。若沒有有效的 `Workbook` 物件，您將無法檢視樞紐或複製其資料。

## 第二步：定義包含樞紐分析表的儲存格區域（copy range to new workbook）

樞紐分析表位於一個矩形儲存格區塊內。您必須指定該區塊，讓複製操作知道要搬移什麼。`CellArea` 建構子使用零基索引：`StartRow, StartColumn, EndRow, EndColumn`。

```csharp
        // Define the cell range that encloses the pivot table, e.g., A1:K21
        // Row and column indexes start at 0, so A1 = (0,0)
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21
```

*Why this matters*：透過明確設定範圍，您可避免複製不相關的資料，且確保包含樞紐的快取。若需處理不同大小的樞紐，可動態計算此範圍。

## 第三步：建立新活頁簿並取得其第一個工作表

現在建立將接收複製列的目標活頁簿。Aspose.Cells 會自動新增一個預設工作表，我們將使用它作為目標。

```csharp
        // Create a new workbook that will receive the copied range
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Why this matters*：從空白活頁簿開始，可保證檔案中僅包含樞紐分析表（及其支援列），使輸出保持輕量。

## 第四步：將來源範圍的列複製到目標工作表（how to copy pivot table）

`CopyRows` 方法會複製整列，保留公式、格式，且最重要的是保留樞紐分析表。此方法的參數為：起始列、結束列、目標儲存格集合，以及在目標工作表中開始複製的列索引（此處為 `0`，即從第一列開始）。

```csharp
        // Copy the rows that contain the pivot table.
        // Pivot tables inside the range are preserved automatically.
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);
```

*Why this matters*：使用 `CopyRows` 而非單一儲存格複製，可確保樞紐快取仍與複製的資料保持連結。Aspose.Cells 會處理底層 XML 結構，您無需手動重建樞紐。

## 第五步：儲存產生的活頁簿（copy range to new workbook）

最後，將新檔案寫入磁碟。目標活頁簿現在包含一個與來源檔案相同且可獨立運作的樞紐分析表。

```csharp
        // Save the new workbook with the copied pivot table
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        // Optional: inform the user
        System.Console.WriteLine("Pivot table copied successfully!");
    }
}
```

### 預期輸出

執行程式會產生 `CopyWithPivot.xlsx`。在 Excel 中開啟此檔案會顯示：

* 與 `Source.xlsx` 中相同的樞紐分析表版面配置
* 所有屬於樞紐快取的來源資料列
* 不含對原始活頁簿的參照（樞紐可離線運作）

## 處理常見變化

### 複製多個樞紐分析表

如果來源工作表包含多個樞紐，請將 `CellArea` 擴展以覆蓋所有範圍的聯集，或對每個獨立區域重複複製步驟。

```csharp
// Example: copy two separate ranges
CellArea firstPivot = new CellArea(0, 0, 20, 10);
CellArea secondPivot = new CellArea(25, 0, 45, 10);

destWorksheet.Cells.CopyRows(firstPivot.StartRow, firstPivot.EndRow, destWorksheet.Cells, 0);
destWorksheet.Cells.CopyRows(secondPivot.StartRow, secondPivot.EndRow, destWorksheet.Cells, 21); // start after first block
```

### 保留樣式與條件格式

`CopyRows` 會自動複製儲存格樣式。若需保留活頁簿層級的命名樣式或自訂數字格式，請在儲存前呼叫 `destWorkbook.Worksheets[0].CopyStyle`。

### 處理大型活頁簿

對於大於 100 MB 的檔案，建議使用 `Workbook.LoadOptions`，將 `MemorySetting` 設為 `MemorySetting.MemoryPreference` 以降低記憶體壓力。

```csharp
LoadOptions loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeSrc = new Workbook(@"bigfile.xlsx", loadOptions);
```

## 完整原始碼（即可執行）

以下為完整程式，包括 `using` 指令與註解。將其複製到新的主控台專案，並將 `YOUR_DIRECTORY` 替換為實際的資料夾路徑。

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source workbook (load excel workbook c#)
        // -------------------------------------------------
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");

        // -------------------------------------------------
        // Step 2: Define the area that contains the pivot table
        // -------------------------------------------------
        // Adjust the indices if your pivot occupies a different range.
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21

        // -------------------------------------------------
        // Step 3: Create the destination workbook
        // -------------------------------------------------
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // -------------------------------------------------
        // Step 4: Copy rows (how to copy pivot table)
        // -------------------------------------------------
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);

        // -------------------------------------------------
        // Step 5: Save the new file (copy range to new workbook)
        // -------------------------------------------------
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        Console.WriteLine("Pivot table copied successfully!");
    }
}
```

執行程式（`dotnet run` 或在 Visual Studio 中按 `Ctrl+F5`）。執行完畢後，開啟 `CopyWithPivot.xlsx` 以驗證樞紐分析表的行為與原始檔案完全相同。

## 常見問題

**Q: 這能用於含有巨集或 VBA 啟用的活頁簿嗎？**  
A: Aspose.Cells 可以讀取巨集啟用的檔案（`.xlsm`），但不會複製巨集程式碼。樞紐分析表本身會被保留，因為它是工作表 XML 的一部份。

**Q: 若樞紐使用外部資料來源，該怎麼辦？**  
A: 複製操作僅包含快取的資料。若目標活頁簿需要從原始來源重新整理，必須手動重新設定資料連線。

**Q: 能否只複製樞紐而不包括底層資料列？**  
A: 不行。樞紐分析表需要其快取。最可靠的方式是如示範般複製包含快取的列。之後若不想顯示，可將這些列隱藏。

## 結論

您現在已了解如何使用 C# **how to copy pivot table** 從一個 Excel 檔案複製到另一個。教學涵蓋了 **load excel workbook c#**、定義 **copy range to new workbook**，並使用 Aspose.Cells 的 `CopyRows` 方法保持樞紐完整。透過完整且可執行的範例，您可以將此模式整合至報表管線、自動匯出工具，或任何需要在活頁簿間傳遞樞紐的情境。

### 後續步驟

* 探索 **Aspose.Cells** 功能，例如以程式方式重新整理樞紐。  
* 若需要開源替代方案，可將此方法與 **ExcelPackage**（EPPlus）結合使用。  
* 透過迴圈 `srcWorkbook.Worksheets`，自動在多個工作表間複製。  

歡迎嘗試不同的範圍、加入自訂樣式，或將此邏輯嵌入更大型的資料處理服務。祝開發順利！

## 接下來該學什麼？

以下教學涵蓋與本指南技術密切相關的主題。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索替代實作方式。

- [在 C# 中建立新活頁簿 – 複製樞紐分析表](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)
- [如何使用 C# 與 Aspose.Cells 複製 Excel 樞紐分析表](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/)
- [將樞紐分析表複製到新活頁簿，並匯出圖形至 PowerPoint](/cells/english/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}