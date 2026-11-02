---
category: general
date: 2026-03-30
description: 如何在 C# 中使用 Aspose.Cells 複製工作表 – 步驟說明，涵蓋複製儲存格範圍、在工作表之間複製欄位、複製工作表樞紐分析表以及新增工作表程式碼。
draft: false
keywords:
- how to copy worksheet
- copy cell range
- copy columns between sheets
- copy worksheet pivot table
- add new worksheet code
language: zh-hant
og_description: 學習如何在 C# 中使用 Aspose.Cells 複製工作表。本指南展示了複製儲存格範圍、保留樞紐分析表、在工作表之間複製欄位，以及新增工作表的程式碼。
og_title: 如何在 C# 中複製工作表 – 完整 Aspose.Cells 教程
tags:
- Aspose.Cells
- C#
- Excel Automation
title: 如何在 C# 中使用 Aspose.Cells 複製工作表 – 完整指南
url: /zh-hant/net/excel-copy-worksheet/how-to-copy-worksheet-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 使用 Aspose.Cells 複製工作表 – 完整指南

曾經想過在 C# 中 **how to copy worksheet** 而不遺失任何樞紐分析表或公式嗎？你並不孤單——許多開發者在需要複製工作表同時保留所有功能時會卡關。在本教學中，我們將一步步示範一個實用的端到端解決方案，不僅能複製資料，還能保留 **copy worksheet pivot table**、處理 **copy cell range**，並展示你需要的 **add new worksheet code**。

我們將涵蓋從載入來源活頁簿到儲存目標檔案的全部步驟，讓你能在工作表之間 **copy columns between sheets**、保留物件，並保持程式碼整潔。沒有模糊的說明，只有完整、可直接執行的範例，今天就能放入你的專案。

## 本教學涵蓋內容

- 使用 Aspose.Cells 載入現有的 Excel 檔案  
- 使用 **add new worksheet code** 建立目標工作表  
- 定義包含樞紐分析表的 **copy cell range**  
- 設定 **CopyOptions** 以保留圖表、公式與樞紐分析表  
- 執行 **copy columns between sheets**，以列為單位的精確度  
- 儲存結果並驗證工作表已正確複製  

閱讀完本指南後，你將能自信地回答「how to copy worksheet」這個問題，無論是自動化報表或是打造以試算表為基礎的 UI。

## 複製工作表概述

在深入程式碼之前，先概述高層次的流程。把它想像成一道食譜：

1. **Load** 來源活頁簿 (`Source.xlsx`)。  
2. **Add** 一個新的工作表以容納複製內容 (`add new worksheet code`)。  
3. **Define** 想要複製的區域 (`copy cell range`)。  
4. **Configure** 複製選項以確保樞紐分析表存活 (`copy worksheet pivot table`)。  
5. **Copy** 列與欄 (`copy columns between sheets`)。  
6. **Save** 新的活頁簿 (`Destination.xlsx`)。  

就是這樣——六個步驟，沒有魔法。每個步驟在下方都有程式碼片段與背後的原理說明。

## 步驟 1 – 載入來源活頁簿

首先，你需要一個指向欲複製檔案的 `Workbook` 實例。此步驟很重要，因為 Aspose.Cells 直接操作檔案系統，而非 Office UI。

```csharp
using Aspose.Cells;

// Path to the original file
string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";

// Load the workbook – this is the starting point for how to copy worksheet
Workbook workbook = new Workbook(sourcePath);
```

*為什麼這很重要：* 載入檔案會在記憶體中建立每個工作表、儲存格與物件的表示。若沒有這一步，就沒有可複製的內容，之後任何 `add new worksheet code` 的嘗試都會失敗，因為來源資料不存在。

## 步驟 2 – 新增工作表（add new worksheet code）

現在我們需要一個地方貼上複製的資料。這正是 **add new worksheet code** 發揮作用的地方。工作表名稱可以自行命名；此處我們稱之為 `"Copy"`。

```csharp
// Grab the first worksheet (the one we want to copy)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a fresh worksheet to receive the copy
Worksheet copySheet = workbook.Worksheets.Add("Copy");
```

*小技巧：* 若要複製多個工作表，請在迴圈中呼叫 `Worksheets.Add`，並為每個工作表指定唯一名稱。如此可避免名稱衝突，保持活頁簿整潔。

## 步驟 3 – 定義複製儲存格範圍

一個 **copy cell range** 告訴 Aspose.Cells 要複製哪些列與欄。在許多實務情境中，範圍會包含樞紐分析表，因此必須精確指定。

```csharp
// Define the area that contains the pivot table (A1:G20)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 19,       // Row 20
    EndColumn = 6      // Column G
};

// Destination range – we start at the same top‑left corner
CellArea destinationRange = new CellArea
{
    StartRow = 0,
    StartColumn = 0,
    EndRow = 19,
    EndColumn = 6
};
```

*為什麼需要這一步：* 明確指定範圍可避免複製整張工作表（可能會浪費資源），同時確保樞紐分析表位於複製區域內。這就是在只需工作表部分內容時 **how to copy worksheet** 的核心。

## 步驟 4 – 設定複製選項（preserve copy worksheet pivot table）

Aspose.Cells 提供 `CopyOptions` 物件，可控制貼上的內容。為了保留樞紐分析表、圖表與公式，我們將 `PasteType.All` 設為貼上類型，並啟用 `PasteSpecial`。

```csharp
CopyOptions copyOptions = new CopyOptions
{
    PasteType = PasteType.All,   // Copy everything: values, formats, objects
    PasteSpecial = true          // Enable special paste to retain pivot tables
};
```

*說明：* `PasteType.All` 是最全面的選項，而 `PasteSpecial` 讓引擎正確處理複雜物件（如樞紐分析表）。忽略此步驟是常見的陷阱，會導致複製的工作表失去互動功能。

## 步驟 5 – 複製列與欄（copy columns between sheets）

現在進入重點：實際搬移資料。我們將使用 `CopyRows` 與 `CopyColumns` 來處理 **copy columns between sheets**。兩者同時使用可確保合併儲存格與欄寬被保留。

```csharp
// Copy rows from the source to the destination sheet
sourceSheet.Cells.CopyRows(
    sourceRange.StartRow,
    sourceRange.EndRow,
    copySheet.Cells,
    destinationRange.StartRow,
    copyOptions);

// Copy columns from the source to the destination sheet
sourceSheet.Cells.CopyColumns(
    sourceRange.StartColumn,
    sourceRange.EndColumn,
    copySheet.Cells,
    destinationRange.StartColumn,
    copyOptions);
```

*發生了什麼：* `CopyRows` 逐列搬移資料，`CopyColumns` 則逐欄搬移。兩者同時執行可保證整個矩形區塊被完整複製，這在需要 **copy columns between sheets**、且兩張工作表的欄寬或隱藏欄不同時尤為重要。

## 步驟 6 – 儲存活頁簿

最後，將變更寫回磁碟。此步驟完成 **how to copy worksheet** 的流程。

```csharp
// Save the workbook with the newly copied sheet
workbook.Save(destinationPath);
```

*驗證提示：* 開啟 `Destination.xlsx`，確認 `"Copy"` 工作表與原始檔案完全相同，樞紐分析表可正常運作，且欄寬相符。如有異常，請重新檢查 `CopyOptions` 設定。

## 邊緣情況與常見變化

### 複製多個工作表

若需複製多張工作表，請將上述邏輯包在 `foreach` 迴圈中：

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    Worksheet newWs = workbook.Worksheets.Add(ws.Name + "_Copy");
    // Re‑use sourceRange/destinationRange or calculate per sheet
    // Then call CopyRows/CopyColumns as shown earlier
}
```

### 跨不同活頁簿保留公式

當來源與目標活頁簿的命名範圍不同時，請將 `copyOptions` 設為 `PasteType.Formulas`，同時保留 `All`：

```csharp
copyOptions.PasteType = PasteType.All | PasteType.Formulas;
```

### 大範圍與效能

對於龐大資料集（數十萬列），可考慮僅使用 `CopyRows`，若欄寬不重要則省略 `CopyColumns`。這樣可節省數秒的執行時間。

## 完整範例程式

以下是完整、可直接執行的程式範例，涵蓋前述所有內容。將其貼入 Console 應用程式，調整檔案路徑後，按下 **F5**。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // ---------- Step 1: Load the source workbook ----------
        string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
        string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // ---------- Step 2: Add a new worksheet (add new worksheet code) ----------
        Worksheet sourceSheet = workbook.Worksheets[0];
        Worksheet copySheet = workbook.Worksheets.Add("Copy");

        // ---------- Step 3: Define the copy cell range ----------
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };
        CellArea destinationRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };

        // ---------- Step 4: Set copy options (preserve copy worksheet pivot table) ----------
        CopyOptions copyOptions = new CopyOptions
        {
            PasteType = PasteType.All,
            PasteSpecial = true
        };

        // ---------- Step 5: Copy rows and columns (copy columns between sheets) ----------
        sourceSheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            copySheet.Cells,
            destinationRange.StartRow,
            copyOptions);

        sourceSheet.Cells.CopyColumns(
            sourceRange.StartColumn,
            sourceRange.EndColumn,
            copySheet.Cells,
            destinationRange.StartColumn,
            copyOptions);

        // ---------- Step 6: Save the workbook ----------
        workbook.Save(destinationPath);
    }
}
```

**預期結果：** 開啟 `Destination.xlsx` 後會看到名為 **Copy** 的工作表，與 `Source.xlsx` 的第一張工作表完全相同——包括所有樞紐分析表、格式與欄寬。原始檔案保持不變。

## 常見問答

**Q: 這能用於 Excel 2019 建立的 .xlsx 檔案嗎？**  
A: 當然可以。Aspose.Cells 支援所有現代 Excel 格式，因此相同程式碼同樣適用於 `.xlsx`、`.xlsm`，甚至舊版的 `.xls` 檔案

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}