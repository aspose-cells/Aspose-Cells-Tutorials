---
category: general
date: 2026-02-28
description: 如何使用 C# 在 Excel 中建立陣列。學習產生數字、評估公式、建立 Excel 工作簿，並在數分鐘內儲存 Excel 檔案。
draft: false
keywords:
- how to create array
- create excel workbook
- save excel file
- how to evaluate formula
- how to generate numbers
language: zh-hant
og_description: 如何使用 C# 在 Excel 中建立陣列。本教學示範如何產生數字、評估公式、建立工作簿並儲存檔案。
og_title: 使用 C# 在 Excel 中建立陣列 – 完整指南
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: 如何使用 C# 在 Excel 中建立陣列 – 逐步指南
url: /zh-hant/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 C# 在 Excel 中建立陣列 – 完整程式教學

你是否曾好奇如何以 C# 程式方式在 Excel 中 **建立陣列**？你並非唯一有此需求的開發者——大家常常想要快速產生一組數字而不必手動輸入。本文將逐步說明 **建立 excel workbook**、放入一個 **產生數字** 的公式、**評估公式**，最後 **save excel file**，讓你可以在 Excel 中開啟並看到結果。

我們將使用 Aspose.Cells 函式庫，因為它讓我們在不需安裝 Excel 的情況下，完整掌控公式與計算。若你偏好其他函式庫，概念相同，只需替換 API 呼叫即可。

## 本教學涵蓋內容

- 設定 C# 專案並安裝所需的 NuGet 套件。  
- 建立新的工作簿（即 *create excel workbook* 的部分）。  
- 撰寫公式，使用 `SEQUENCE` 與 `WRAPCOLS` 建構 4 列 × 3 欄 的陣列。  
- 強制引擎 **evaluate the formula** 使陣列實體化。  
- 將工作簿儲存至磁碟（**save excel file**）並檢查輸出。  

完成後，你將得到一個可執行的程式，產生如下圖示的 Excel 工作表：

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |
| 7 | 8 | 9 |
|10 |11 |12 |

![如何在 Excel 中建立陣列 – 執行 C# 程式碼後的結果工作表](image.png)

*(圖片的 alt 文字包含主要關鍵字「how to create array」以利 SEO。)*

## 前置條件

- .NET 6.0 SDK 或更新版本（此程式碼亦可於 .NET Framework 4.6+ 執行）。  
- Visual Studio 2022 或任何你喜歡的編輯器。  
- NuGet 套件 **Aspose.Cells**（提供免費試用）。

不需要額外安裝 Excel，因為 Aspose.Cells 內部已具備計算引擎。

## 步驟 1：設定專案並匯入 Aspose.Cells

要開始，先建立一個 console 應用程式並加入函式庫：

```bash
dotnet new console -n ExcelArrayDemo
cd ExcelArrayDemo
dotnet add package Aspose.Cells
```

接著開啟 **Program.cs**，加入命名空間：

```csharp
using Aspose.Cells;
```

*為何重要*：匯入 `Aspose.Cells` 後，我們即可取得 `Workbook`、`Worksheet` 以及計算相關類別，以便 **create excel workbook** 並使用公式。

## 步驟 2：建立工作簿與目標工作表

我們需要一個全新的 workbook 物件；第一個工作表 (`Worksheets[0]`) 將承載我們的陣列。

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = workbook.Worksheets[0];            // reference to Sheet1
```

*說明*：`Workbook` 類別代表整個 Excel 檔案。預設會包含一張工作表，對於簡易示範而言已足夠。若日後需要更多工作表，可呼叫 `workbook.Worksheets.Add()`。

## 步驟 3：撰寫產生數字並形成陣列的公式

Excel 的動態陣列函式（`SEQUENCE` 與 `WRAPCOLS`）讓我們只用一個公式即可產生一整塊數值。以下是我們將指派的完整字串：

```csharp
// Step 3: Assign a formula that creates a 4‑row × 3‑col array
// SEQUENCE(12,1,1,1) generates numbers 1‑12; WRAPCOLS wraps them into 3 columns
ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(12,1,1,1),3)";
```

*為何可行*：  
- `SEQUENCE(12,1,1,1)` 會回傳 1‑12 的垂直列表。  
- `WRAPCOLS(...,3)` 會將該列表以三欄方式填滿，並自動向下溢位至後續列。  

如果你在 Excel 中開啟工作簿 **未先** 評估公式，`A1` 只會顯示公式文字。接下來的步驟會強制計算。

## 步驟 4：**Evaluate the Formula** 使陣列實體化

Aspose.Cells 在寫入時不會自動重新計算公式，因此我們必須明確呼叫計算引擎：

```csharp
// Step 4: Evaluate the formula so the array is materialised in the sheet
workbook.Calculate();   // runs all pending formulas
```

*執行內容*：`Calculate()` 會遍歷所有含公式的儲存格，計算結果並寫回數值。這就是本教學中 **how to evaluate formula** 的部分。呼叫此方法後，A1:C4 會包含 1‑12 的數字，與原生 Excel 的溢位結果相同。

## 步驟 5：**Save Excel File** 並驗證結果

最後，我們將工作簿寫入磁碟：

```csharp
// Step 5: Save the workbook to view the result
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

在 Excel 中開啟 `output.xlsx`，即可看到我們產生的 4 × 3 陣列。若使用的 Excel 版本早於 365/2019，動態陣列函式將無法辨識——Aspose.Cells 仍會寫入已計算好的數值，檔案仍可使用。

*小技巧*：若需強制特定格式，可使用 `SaveFormat.Xlsx`，例如 `workbook.Save(outputPath, SaveFormat.Xlsx);`。

## 完整範例（可直接複製貼上）

以下為完整程式碼。貼到 **Program.cs**，執行 `dotnet run`，即可在專案資料夾取得 `output.xlsx`。

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelArrayDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook and grab the first worksheet
            Workbook workbook = new Workbook();               // in‑memory workbook
            Worksheet ws = workbook.Worksheets[0];            // default sheet (Sheet1)

            // 2️⃣ Drop the formula that builds a 4‑row × 3‑col array
            // SEQUENCE creates numbers 1‑12; WRAPCOLS arranges them into 3 columns
            ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(12,1,1,1),3)";

            // 3️⃣ Force the calculation engine to evaluate the formula
            workbook.Calculate();   // now the array is "spilled" into A1:C4

            // 4️⃣ Save the file so you can open it in Excel
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);
            Console.WriteLine($"✅ Workbook saved to {outputPath}");
        }
    }
}
```

**預期輸出**（主控台）：

```
✅ Workbook saved to C:\Path\To\ExcelArrayDemo\output.xlsx
```

開啟檔案後，你會看到 1‑12 的數字正如前述排列。

## 變形與邊緣案例

### 1. 舊版 Excel 無動態陣列  
若讀者使用 Excel 2016 或更早版本，`SEQUENCE` 與 `WRAPCOLS` 不存在。可快速的解法是於 C# 中產生數字並直接寫入：

```csharp
int value = 1;
for (int row = 0; row < 4; row++)
{
    for (int col = 0; col < 3; col++)
    {
        ws.Cells[row, col].PutValue(value++);
    }
}
```

此手動迴圈雖較冗長，卻能產生相同結果。**how to generate numbers** 的概念仍然相同。

### 2. 調整陣列大小  
想要 5 × 5 的 1‑25 數字格子？只要調整 `SEQUENCE` 參數以及 `WRAPCOLS` 的欄數：

```csharp
ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(25,1,1,1),5)";
```

### 3. 使用命名範圍以供重複使用  
你可以將溢位的範圍指定名稱，以便在之後的公式中使用：

```csharp
ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(12,1,1,1),3)";
workbook.Calculate(); // ensure the range exists
int lastRow = ws.Cells.GetLastDataRow(); // should be 3 (zero‑based)
int lastCol = ws.Cells.GetLastDataColumn(); // should be 2
string address = $"A1:{CellIndexToName(lastRow, lastCol)}";
ws.Workbook.Names.Add("MyArray", ws, address);
```

如此其他工作表即可直接參照 `MyArray`。

## 常見陷阱與避免方法

| 陷阱 | 發生原因 | 解決方法 |
|---|---|---|
| **Formula not spilling** | `Calculate()` 被遺漏或在設定公式前就呼叫。 | 請務必在指派公式 **之後** 呼叫 `workbook.Calculate()`。 |
| **File saved but empty** | 不小心使用了 `SaveFormat.Csv`。 | 改用 `SaveFormat.Xlsx`，或省略格式讓 Aspose 自行推斷。 |
| **Dynamic

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}