---
category: general
date: 2026-11-16
description: 學習如何在 Excel 中使用 Aspose.Cells、動態陣列函數和 lambda 縮減器來展開陣列，然後從 C# 寫入 Excel
  檔案。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- create excel workbook
- how to use lambda
- dynamic array functions
- write excel file
language: zh-hant
lastmod: 2026-11-16
og_description: 如何在 Excel 中使用 Aspose.Cells、動態陣列函數和 lambda 縮減器展開陣列。請參考完整的 C# 範例來寫入
  Excel 檔案。
og_image_alt: Diagram illustrating how to expand array in an Excel worksheet
og_title: 如何使用 Aspose.Cells 在 Excel 中擴展陣列 – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to expand array in Excel using Aspose.Cells, dynamic array
    functions, and a lambda reducer, then write the Excel file from C#.
  headline: How to expand array in Excel with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. `EXPAND` pads missing columns with blank cells. The same works for
      rows.
    question: Can I expand to more columns than the source provides?
  - answer: '`EXPAND` will treat the source as a single row; you can still specify
      rows and columns to reshape it.'
    question: What if the source array is horizontal (`{1,2,3,4,5}`)?
  - answer: The lambda must return a value compatible with the accumulator type. For
      text concatenation you could use `LAMBDA(acc, val, acc & val)`.
    question: Does `REDUCE` work with non‑numeric data?
  - answer: Only when you need the computed values before saving. Excel will recalculate
      on open if you skip it.
    question: Do I need to call `CalculateFormula` for every change?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: 如何在 Excel 中使用 Aspose.Cells 擴展陣列
url: /zh-hant/net/calculation-engine/how-to-expand-array-in-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Excel 中使用 Aspose.Cells 展開陣列

如果您需要在 C# 中 **展開陣列** 到 Excel 工作表，本教學會示範完整步驟。您將建立 Excel 活頁簿、使用 `EXPAND` 與 `REDUCE` 等動態陣列函式、套用 **lambda** 累加器，最後 **寫入 Excel 檔案** 到磁碟。此方法適用於 Aspose.Cells 23.10 以上版本，且不需要手動安裝 Excel。

閱讀完本指南後，您將得到一個功能完整的 `ExpandReduceDemo.xlsx`，展示在程式化環境中使用動態陣列公式的威力。

## 需要的環境

- .NET 6.0（或任何 Aspose.Cells 支援的 .NET 版本）
- Aspose.Cells for .NET 套件（`dotnet add package Aspose.Cells`）
- 程式碼編輯器或 IDE（Visual Studio、VS Code、Rider 等）

不需要額外的 COM interop 或 Office 安裝，因為 Aspose.Cells 會在內部處理檔案格式。

## 第一步：建立 Excel 活頁簿

第一個任務是 **在記憶體中建立 Excel 活頁簿**。Aspose.Cells 提供 `Workbook` 類別，代表整個 XLSX 檔案。

```csharp
using System;
using Aspose.Cells;

class ExpandReduceDemo
{
    static void Main()
    {
        // Step 1: instantiate a new workbook and get the default worksheet
        Workbook workbook = new Workbook();              // creates an empty .xlsx structure
        Worksheet sheet = workbook.Worksheets[0];        // the first (and only) sheet by default
```

> **為什麼重要：** 建立 `Workbook` 後會得到一個乾淨的畫布。預設工作表已經建立，除非您需要多張工作表，否則不必手動新增。

## 第二步：插入垂直陣列常數

Excel 的動態陣列引擎可以直接使用文字陣列常數。我們將垂直陣列 `{1;2;3;4;5}` 放入 **A1** 儲存格。

```csharp
        // Step 2: put a vertical array constant into A1
        sheet.Cells["A1"].PutValue("{1;2;3;4;5}");
```

> **小技巧：** 分號（`;`）用來分隔常數中的列，逗號（`,`）則分隔欄。這與 Excel 本身的語法相同。

## 第三步：使用 EXPAND 將陣列展開為矩陣

現在回答核心問題 – **如何展開陣列** – 使用 `EXPAND` 函式。此公式會把單欄陣列展開為 5 列 × 2 欄的矩陣，起始位置為 **B1**。

```csharp
        // Step 3: use EXPAND to create a 5‑row by 2‑column matrix
        sheet.Cells["B1"].Formula = "EXPAND(A1,5,2)";
```

> **為什麼使用 EXPAND？** `EXPAND(source, rows, cols)` 會強制來源範圍佔據指定的大小，必要時以空白填充。這是從單一陣列產生較大矩陣最易讀的方式。

## 第四步：使用 lambda 累加器對矩陣進行 REDUCE

`REDUCE` 函式會遍歷範圍，並以 **lambda** 表達式彙總值。此處我們把每欄的值加總至單一欄，結果放在 **D1**。

```csharp
        // Step 4: REDUCE the expanded matrix using a lambda accumulator
        sheet.Cells["D1"].Formula = "REDUCE(A1, B1:E5, LAMBDA(acc, val, acc+val))";
```

> **如何使用 lambda：** `LAMBDA(acc, val, acc+val)` 會接收目前的累加值（`acc`）與下一個儲存格值（`val`），回傳新的累加值，等同於執行累計總和。這示範了 **在 Excel 公式中使用 lambda** 的方法。

## 第五步：計算公式以顯示結果

設定公式後，Aspose.Cells 不會自動計算。呼叫 `CalculateFormula` 會強制引擎計算活頁簿中的所有公式。

```csharp
        // Step 5: recalculate all formulas so the results are materialized
        workbook.CalculateFormula();
```

> **注意：** 若您在 Excel 中開啟產生的檔案，值已經可見，因為它們已被預先計算。

## 第六步：將 Excel 檔案寫入磁碟

最後，使用 `Save` 方法 **寫入 Excel 檔案**。請選擇您有寫入權限的資料夾。

```csharp
        // Step 6: save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\ExpandReduceDemo.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### 預期結果

| A | B | C | D |
|---|---|---|---|
| {1;2;3;4;5} | 1 |  | 15 |
|            | 2 |  |    |
|            | 3 |  |    |
|            | 4 |  |    |
|            | 5 |  |    |

- **B 欄** 與 **C 欄** 包含由 `EXPAND` 產生的 5 × 2 矩陣。
- **D1 儲存格** 顯示 `15`，即所有數字的總和，由 `REDUCE` + **lambda** 公式計算得出。

## 常見問題與邊緣情況

- **我可以展開到比來源更多的欄位嗎？**  
  可以。`EXPAND` 會以空白儲存格填補缺少的欄位，列亦同理。

- **如果來源陣列是水平的（`{1,2,3,4,5}`）會怎樣？**  
  `EXPAND` 會將來源視為單一列；您仍可指定列數與欄數來重新塑形。

- **`REDUCE` 能處理非數值資料嗎？**  
  lambda 必須回傳與累加器類型相容的值。若要串接文字，可使用 `LAMBDA(acc, val, acc & val)`。

- **每次變更都需要呼叫 `CalculateFormula` 嗎？**  
  只在需要於儲存前取得計算結果時才必須。若省略，Excel 開啟檔案時會自行重新計算。

## 專業小技巧

- **效能：** 大型活頁簿請在全部公式設定完畢後一次呼叫 `workbook.CalculateFormula`，而非每個儲存格都呼叫。
- **版本相容性：** `EXPAND` 與 `REDUCE` 於 Excel 365 及更新版提供。Aspose.Cells 內建計算引擎，無論目標 Excel 版本為何皆可使用。
- **除錯公式：** 使用 `sheet.Cells["B1"].Formula` 讀回您設定的公式字串，對於動態產生公式時特別有幫助。

## 結論

現在您已掌握 **如何在 Excel 中展開陣列**，利用 Aspose.Cells 套用 **動態陣列函式**、使用 `REDUCE` 搭配 **lambda**，並 **寫入 Excel 檔案** 從 C# 執行。此端對端範例可延伸至更複雜的資料轉換，例如矩陣轉置、累積總計或自訂彙總。

---

*後續步驟：*  
- 探索其他動態函式，如 `FILTER`、`SORT` 與 `UNIQUE`。  
- 結合多個 `LAMBDA` 表達式，建立可重複使用的自訂函式。  
- 將活頁簿產生整合至 ASP.NET Core API，實現即時報表產出。

## 接下來該學什麼？

以下教學與本指南主題緊密相關，能進一步深化您對相關技術的掌握。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您在專案中探索更多 API 功能與替代實作方式。

- [How to create Excel workbook C# with a dynamic array formula](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/)
- [How to expand array in Excel and populate a template](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)
- [How to Expand Array in C# with Aspose.Cells – Step‑by‑Step Guide](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}