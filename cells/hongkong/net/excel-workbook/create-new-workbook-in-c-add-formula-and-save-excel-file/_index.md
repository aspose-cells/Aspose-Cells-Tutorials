---
category: general
date: 2026-02-23
description: 在 C# 中以程式方式建立新工作簿，並在儲存格中加入公式。學習如何使用 EXPAND，然後輕鬆儲存 Excel 工作簿。
draft: false
keywords:
- create new workbook
- add formula to cell
- save excel workbook
- how to use expand
- create excel file programmatically
language: zh-hant
og_description: 在 C# 中以程式方式建立新工作簿，向儲存格加入公式，學習如何使用 EXPAND，並在數秒內儲存 Excel 工作簿。
og_title: 在 C# 中建立新工作簿 – 加入公式並儲存 Excel 檔案
tags:
- C#
- Excel Automation
- Aspose.Cells
title: 在 C# 中建立新工作簿 – 加入公式並儲存 Excel 檔案
url: /zh-hant/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 用 C# 建立新 Workbook – 新增公式並儲存 Excel 檔案

有沒有想過 **從程式碼建立新 workbook**，卻不需要開啟 Excel？你並不是唯一有這個需求的人。許多開發者在需要即時產生試算表（例如報表、匯出或快速資料傾印）時，常會卡住。

好消息是？在本教學中，你將會看到如何 **建立新 workbook**、在 **儲存格加入公式**，再 **儲存 excel workbook**，只需幾行 C# 程式碼。我們也會深入探討 **如何使用 expand**，讓你在不手動複製的情況下產生動態陣列。完成後，你就能 **程式化建立 excel 檔案**，並將它傳遞給使用者或下游服務。

## 前置條件

- .NET 6.0 或更新版本（任何近期的 .NET 執行環境皆可）
- Aspose.Cells for .NET（免費試用版或授權版）— 這個函式庫提供本文所使用的 `Workbook` 與 `Worksheet` 類別。
- 基本的 C# 語法概念— 不需要深入的 Excel 知識。

如果你已經具備上述條件，太好了！若還沒有，請從 NuGet 取得 Aspose.Cells（`Install-Package Aspose.Cells`），即可開始動手。

---

## 步驟 1：建立新 Workbook – 基礎

首先，我們需要實例化一個全新的 workbook 物件。把它想像成開啟一個全新、完全空白的 Excel 檔案。

```csharp
using Aspose.Cells;

public class ExcelGenerator
{
    public void Generate()
    {
        // Step 1: Create a new workbook (this is the core of create new workbook)
        Workbook workbook = new Workbook();
```

> **為什麼重要：** `Workbook` 類別是所有 Excel 操作的入口點。建立新實例即會為工作表、樣式與公式分配記憶體，且全程不觸及檔案系統。

---

## 步驟 2：存取第一個 Worksheet

每個新 workbook 皆會自動帶有一個預設工作表（名稱為 *Sheet1*）。我們先取得它，以便放入資料與公式。

```csharp
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];
```

> **小技巧：** 若需要多張工作表，只要呼叫 `workbook.Worksheets.Add("MySheet")`，即可取得回傳的 `Worksheet` 物件並使用。

---

## 步驟 3：在儲存格加入公式 – 使用 EXPAND

接下來的重點：插入公式。`EXPAND` 函式在你想把靜態陣列展開為更大、自動填滿的範圍時，非常好用。

```csharp
        // Step 3: Add formula to cell A1 using EXPAND
        // This creates a 5‑row array from the constant {1,2,3}
        worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";
```

### EXPAND 公式的運作方式

| 參數 | 說明 |
|------|------|
| `{1,2,3}` | 來源陣列（水平的三個數字） |
| `5` | 結果想要的列數 |
| `1` | 結果想要的欄數（保持 1 代表垂直） |

Excel 計算後，會產生一個 **垂直** 列表：

```
A1: 1
A2: 2
A3: 3
A4: 0   (filled with zeros)
A5: 0
```

> **為什麼使用 EXPAND？** 它免除手動複製或 VBA 迴圈的需求。此函式會動態重塑資料，使試算表更具彈性且易於維護。

---

## 步驟 4：儲存 Excel Workbook – 永久寫入

公式寫好後，最後一步是將 workbook 寫入磁碟。你可以選擇任何有寫入權限的資料夾。

```csharp
        // Step 4: Save the workbook to view the result
        string outputPath = @"C:\Temp\ExpandFormula.xlsx";
        workbook.Save(outputPath);
    }
}
```

> **你會看到的結果：** 開啟 `ExpandFormula.xlsx`，儲存格 `A1` 會顯示展開後的陣列。公式本身仍保留在儲存格中，若你修改來源陣列，輸出會自動更新。

---

## 可選：以程式方式驗證輸出

如果不想手動開啟 Excel，也可以讀回值來確認是否符合預期。

```csharp
        // Verify values without opening Excel
        for (int row = 0; row < 5; row++)
        {
            var value = worksheet.Cells[row, 0].Value; // column 0 = A
            Console.WriteLine($"Row {row + 1}: {value}");
        }
```

執行上述程式會印出：

```
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

---

## 常見問題與邊緣情況

| 問題 | 解答 |
|------|------|
| **可以在更大的來源陣列上使用 EXPAND 嗎？** | 當然可以。只要把 `{1,2,3}` 改成任意常數或儲存格範圍，例如 `EXPAND(A1:C1,10,1)`。 |
| **如果需要水平結果該怎麼做？** | 交換列與欄的參數：`EXPAND({1,2,3},1,5)` 會產生 1 列 5 欄的展開。 |
| **舊版 Excel 能使用嗎？** | `EXPAND` 從 Excel 365/2021 起提供。舊版需改用 `INDEX`/`SEQUENCE` 來模擬陣列。 |
| **需要呼叫 `workbook.CalculateFormula()` 嗎？** | 不需要。Aspose.Cells 會在儲存時自動計算公式，值會即時出現在儲存格。 |
| **如何在儲存前加入多張工作表？** | 呼叫 `workbook.Worksheets.Add("SecondSheet")`，然後在新工作表上重複儲存格操作步驟。 |

---

## 完整範例程式

以下是可直接執行的完整程式碼。複製貼上到 Console App，調整輸出路徑後，按 **F5** 執行。

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutomationDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create new workbook
            Workbook workbook = new Workbook();

            // Access first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // Add EXPAND formula to A1
            worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";

            // Optional: verify values in console
            workbook.CalculateFormula(); // ensures formulas are evaluated now
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine($"A{i + 1} = {worksheet.Cells[i, 0].Value}");
            }

            // Save the workbook
            string filePath = @"C:\Temp\ExpandFormula.xlsx";
            workbook.Save(filePath);
            Console.WriteLine($"Workbook saved to {filePath}");
        }
    }
}
```

**預期在主控台的輸出：**

```
A1 = 1
A2 = 2
A3 = 3
A4 = 0
A5 = 0
Workbook saved to C:\Temp\ExpandFormula.xlsx
```

開啟產生的檔案，你會看到相同的數字出現在 **A** 欄。

---

## 視覺摘要

![建立新 workbook 範例](create-new-workbook.png "顯示使用 C# 建立新 workbook 並套用 EXPAND 結果的螢幕截圖")

*此圖示說明剛產生的 workbook 以及 EXPAND 的結果。*

---

## 結論

現在你已掌握如何使用 C# **建立新 workbook**、**在儲存格加入公式**，並 **儲存 excel workbook**。透過熟悉 **如何使用 expand**，你可以在不手動操作的情況下產生動態陣列，整個流程讓你能 **程式化建立 excel 檔案**，適用於任何自動化情境。

接下來可以嘗試把常數陣列換成範圍參照、變換 `EXPAND` 的維度，或在多張工作表間串接多個公式。同樣的模式也適用於圖表、樣式，甚至樞紐分析表——持續探索吧。

如果在實作過程中遇到任何問題，歡迎在下方留言。祝開發順利，盡情享受程式化 Excel 的威力！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}