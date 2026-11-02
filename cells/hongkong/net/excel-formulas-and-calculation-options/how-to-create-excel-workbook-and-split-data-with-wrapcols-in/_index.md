---
category: general
date: 2026-10-10
description: 在 C# 中建立 Excel 工作簿，並使用 WRAPCOLS 函數將陣列資料分割成欄位。遵循完整的逐步指南，提供可執行的程式碼。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- excel formula split data
- use wrapcols function
- how to use wrapcols
- split array columns
language: zh-hant
lastmod: 2026-10-10
og_description: 在 C# 中建立 Excel 工作簿，並套用 WRAPCOLS 函式將陣列資料分割成欄位。本指南提供完整程式碼，並說明每一步驟。
og_image_alt: Screenshot of an Excel sheet showing three columns filled by the WRAPCOLS
  formula
og_title: 在 C# 中建立 Excel 工作簿並使用 WRAPCOLS 分割資料
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  headline: How to create Excel workbook and split data with WRAPCOLS in C#
  type: TechArticle
- description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  name: How to create Excel workbook and split data with WRAPCOLS in C#
  steps:
  - name: Using the function with different data types
    text: 'The `WRAPCOLS` function is not limited to numbers. You can split text values,
      dates, or mixed types:'
  - name: Variable column count at runtime
    text: 'Often the number of columns you need depends on user input. You can build
      the formula string dynamically:'
  - name: Large arrays and performance
    text: '`WRAPCOLS` can handle thousands of elements, but evaluating extremely large
      arrays in a single cell may increase calculation time. If you notice slowdown:'
  - name: Handling empty cells
    text: If the source array contains empty strings (`""`) or `NULL` values, `WRAPCOLS`
      inserts blank cells, preserving the column layout. This behavior is useful when
      you need placeholder columns for later data entry.
  - name: Using named ranges instead of literals
    text: 'For maintainability, define a named range that holds the source data, then
      reference it:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: 如何在 C# 中建立 Excel 活頁簿並使用 WRAPCOLS 分割資料
url: /zh-hant/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中建立 Excel 工作簿並使用 WRAPCOLS 分割資料

如果您需要以程式方式 **建立 Excel 工作簿**，本教學將一步步說明如何操作，並示範如何使用 `WRAPCOLS` 函式將 **陣列資料** 分散到多個欄位。您將獲得一個完整、可執行的範例，產生的 `.xlsx` 檔案會將資料分配到三個欄位。

本教學涵蓋您所需的一切：必備的 NuGet 套件、每一行程式碼、`WRAPCOLS` 公式的原理，以及如何針對不同陣列大小或欄位數做調整。完成後，您即可在任何產生 Excel 檔案的 C# 專案中嵌入 **使用 wrapcols 函式** 的技巧。

## 前置條件

開始之前，請確保您已具備：

* 已安裝 .NET 6.0 SDK 或更新版本  
* C# 開發環境 (Visual Studio、VS Code、Rider 等)  
* **Aspose.Cells for .NET** NuGet 套件 – 提供範例中使用的 `Workbook` 類別  

您不需要安裝 Office；Aspose.Cells 會直接寫入 `.xlsx` 檔案。

## 步驟 1 – 建立 Excel 工作簿

第一步是實例化一個新的 workbook 物件，並取得第一張工作表的參考。此步驟是後續所有操作的基礎。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();                // creates an empty Excel file in memory
        Worksheet ws = wb.Worksheets[0];             // the default worksheet is at index 0
```

`Workbook` 代表整個檔案，`Worksheet` 代表單一工作表。將工作簿建立於記憶體中，可避免在未明確儲存前產生磁碟 I/O。

## 步驟 2 – 套用 WRAPCOLS 以分割陣列欄位

接下來在 **A1** 儲存格放入使用 `WRAPCOLS` 的公式。此函式接受兩個參數：來源陣列與您希望陣列換行的欄位數。

```csharp
        // Step 2: Apply the WRAPCOLS formula to split the array into 3 columns
        // The array {1,2,3,4,5,6} will be distributed as:
        // 1 2 3
        // 4 5 6
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

**為什麼會這樣運作：** `WRAPCOLS` 會將平面陣列 `{1,2,3,4,5,6}` 逐列填入工作表，每列產生三個欄位。第一個參數可以是任意 Excel 陣列常數、具名範圍，或是動態陣列公式。第二個參數 (`3`) 告訴 Excel 在換到下一列前，要產生多少欄位。

### 使用不同資料類型的範例

`WRAPCOLS` 不只限於數字。您也可以分割文字、日期或混合型別：

```csharp
        // Example with mixed data: strings and numbers
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";
```

當來源陣列包含字串時，Excel 會自動將結果視為文字儲存格。此彈性讓您 **excel formula split data** 用於報表、儀表板或資料遷移等情境。

## 步驟 3 – 計算公式以填充工作表

公式會以字串形式存於儲存格，直到您要求工作簿評估它們。呼叫 `CalculateFormula` 會強制計算，並將結果寫入儲存格。

```csharp
        // Step 3: Calculate formulas so the worksheet is populated
        wb.CalculateFormula();   // evaluates all formulas in the workbook
```

若未呼叫此方法，儲存的檔案只會留下公式文字，而不會有計算後的值。此方法會遍歷整個工作簿，因此您在其他位置加入的公式也會在一次呼叫中全部解析。

## 步驟 4 – 儲存工作簿以檢視結果

最後，將工作簿寫入磁碟。選擇一個您有寫入權限的資料夾，並為檔案命名清晰。

```csharp
        // Step 4: Save the workbook to see the result
        string outputPath = @"output.xlsx";
        wb.Save(outputPath);      // creates output.xlsx in the application directory
    }
}
```

當您在 Excel（或任何相容檢視器）開啟 `output.xlsx` 時，會看到：

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

若使用混合型別範例，第 3、4 行會分別顯示文字與數字。

## 進階變形與例外情況處理

### 執行時決定欄位數

常見情況是欄位數取決於使用者輸入。您可以動態組合公式字串：

```csharp
int columns = 4; // could come from UI, config, etc.
string arrayLiteral = "{10,20,30,40,50,60,70,80}";
ws.Cells[5, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
```

### 大型陣列與效能

`WRAPCOLS` 能處理數千個元素，但在單一儲存格內評估極大陣列可能會增加計算時間。若發現效能下降：

* 將來源陣列切成較小的區塊，分別寫入不同的起始儲存格。  
* 使用 `WorkbookSettings` 開啟多執行緒計算：

```csharp
wb.Settings.CalcMode = CalculationModeType.Automatic;
wb.Settings.EnableMultiThreadedCalc = true;
```

### 處理空白儲存格

若來源陣列包含空字串 (`""`) 或 `NULL`，`WRAPCOLS` 會插入空白儲存格，保持欄位布局不變。此行為在需要為之後的資料輸入保留佔位欄位時相當有用。

### 使用具名範圍取代字面值

為了易於維護，您可以先定義一個具名範圍保存來源資料，然後在公式中引用：

```csharp
ws.Cells["D1:D6"].PutValue(new object[] { 11, 12, 13, 14, 15, 16 });
ws.Cells["E1"].Formula = "=WRAPCOLS(D1:D6,3)";
```

如此公式會直接從工作表本身讀取資料，讓 **how to use wrapcols** 能在動態報表情境中發揮作用。

## 常見陷阱與專業提示

* **不要省略第二個參數。** `WRAPCOLS(array)` 若未指定欄位數，會只產生單一欄位，失去分割資料的目的。  
* **避免混用陣列維度。** 來源陣列必須是一維的；若提供二維陣列（例如 `{ {1,2},{3,4} }`），會產生 `#VALUE!` 錯誤。  
* **計算完畢後再儲存。** 若在 `CalculateFormula` 之前呼叫 `wb.Save`，檔案只會留下公式文字。  
* **檢查檔案權限。** 在受限環境（例如 ASP.NET）執行時，確保執行身分有寫入目標資料夾的權限。  

## 完整可執行範例

以下是完整程式碼，您可以直接複製、貼上並執行。內含所有 using、錯誤處理與註解。

```csharp
using System;
using Aspose.Cells;

class ExcelWrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Split a numeric array into 3 columns
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

        // Split a mixed array (text + numbers) into 3 columns, starting at row 3
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";

        // Dynamically build a formula with a variable column count
        int columnCount = 4;
        string sourceArray = "{10,20,30,40,50,60,70,80}";
        ws.Cells[5, 0].Formula = $"=WRAPCOLS({sourceArray},{columnCount})";

        // Evaluate all formulas
        wb.CalculateFormula();

        // Save the workbook
        string outputPath = "output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

執行程式後會產生 `output.xlsx`，其中包含三個區塊，示範如何使用 **excel formula split data** 透過 `WRAPCOLS` 函式分割陣列欄位。

## 結論

您現在已掌握在 C# 中 **建立 Excel 工作簿** 的方法，以及如何 **使用 wrapcols 函式** 高效地 **分割陣列欄位**。主要步驟——實例化 `Workbook`、插入 `WRAPCOLS` 公式、計算、儲存——構成一個可重複使用的模式，適用於任何需要將資料分配到多欄的自動化任務。

接下來您可以：

* 結合 `WRAPCOLS` 與其他動態陣列函式，如 `FILTER` 或 `SORT`。  
* 從資料庫匯出大量資料，交由 Excel 自動排版。  
* 建立使用者驅動的報表，讓欄位數透過 UI 控制元件選擇。

嘗試不同的陣列來源、欄位數與額外公式，擴充此基礎。祝您寫程式愉快！

## 接下來該學什麼？

以下教學與本篇內容緊密相關，提供完整的程式碼範例與逐步說明，協助您精通更多 API 功能，並探索在專案中實作的其他方式。

- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Create Excel Workbook – Convert Array to Matrix with WRAPCOLS](/cells/english/net/calculation-engine/create-excel-workbook-convert-array-to-matrix-with-wrapcols/)
- [Create Excel Workbook C# – Step‑by‑Step Guide](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}