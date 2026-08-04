---
category: general
date: 2026-02-09
description: 幾分鐘內說明如何在 Excel 中使用 C# 建立陣列 – 學習產生序列號碼、使用 COT，並將活頁簿儲存為 XLSX。
draft: false
keywords:
- how to create array
- create excel workbook c#
- generate sequence numbers
- save workbook as xlsx
- how to use cot
language: zh-hant
og_description: 如何使用 C# 在 Excel 中建立陣列，逐步說明，包括產生序列號、使用 COT，以及將活頁簿另存為 XLSX。
og_title: 使用 C# 在 Excel 中建立陣列 – 快速指南
tags:
- C#
- Excel
- Aspose.Cells
title: 使用 C# 在 Excel 中建立陣列 – 步驟教學
url: /zh-hant/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Excel 中使用 C# 建立陣列 – 步驟指南

有沒有想過 **如何在 Excel 中使用 C# 建立陣列**，卻要花好幾個小時翻文件？你並不孤單。許多開發者在需要動態溢位範圍、快速取得三角函數值，或只是想把乾淨的 XLSX 檔案存到磁碟時，常會卡關。在本教學中，我們會立即解決這個問題——建立一個小型活頁簿，寫入可擴展的陣列公式、加入餘切計算，並將所有內容儲存為 XLSX 檔案。

我們還會順手示範幾個小技巧：產生序列號、精通 `COT` 函數，並確保檔案儲存到你指定的位置。完成後，你會得到一段可在任何 .NET 專案中直接使用的程式碼片段。沒有多餘的說明，只有可直接運作的程式碼。

> **專業小技巧：** 範例使用廣受歡迎的 **Aspose.Cells** 函式庫，但概念同樣適用於其他 Excel 自動化套件（EPPlus、ClosedXML），只需做少量調整。

---

## 你需要的環境

- **.NET 6** 或更新版本（程式碼同樣可在 .NET Framework 4.7+ 上編譯）  
- **Aspose.Cells for .NET** – 可從 NuGet 取得 (`Install-Package Aspose.Cells`)  
- 文字編輯器或 IDE（Visual Studio、Rider、VS Code…）  
- 具寫入權限的資料夾，用來存放輸出檔案  

就這樣——不需要額外設定、也不需要 COM Interop，只要一個乾淨的受管理組件。

---

## 第一步：如何在 Excel 中建立陣列 – 初始化活頁簿

當你想在 Excel 工作表中 **建立陣列** 時，第一件事就是建立一個活頁簿物件。把活頁簿想成空白畫布，工作表則是你繪製公式的地方。

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // <- fresh workbook
        Worksheet worksheet = workbook.Worksheets[0];    // first (and only) sheet

        // The rest of the steps follow...
```

為什麼要使用不帶參數的 `Workbook()`？它會在記憶體中建立一個預設工作表的活頁簿，非常適合快速、程式化的任務。如果需要開啟既有檔案，只要把檔案路徑傳給建構子即可。

---

## 第二步：使用 EXPAND 與 SEQUENCE 產生序列號

現在我們已經有工作表，接下來解決 **產生序列號** 的需求。Excel 全新的動態陣列函數（`SEQUENCE`、`EXPAND`）讓我們可以建立 3 列的垂直清單，並自動溢位成 3 × 5 的範圍。

```csharp
        // Write a dynamic array formula that expands a 3‑row sequence into a 3×5 spill range
        // EXPAND pads the result to 5 columns, SEQUENCE generates numbers 1‑3 vertically
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

**這段程式碼在做什麼？**  
- `SEQUENCE(3,1,1,1)` → 產生垂直陣列 `{1;2;3}`。  
- `EXPAND(...,5,1)` → 把這個三列的欄位向右延伸至五欄，額外的儲存格以空白填充。  

當你開啟產生的 `output.xlsx` 時，會看到從 **A1** 開始的 3 × 5 區塊，第一欄分別為 1、2、3，剩餘四欄則為空白。這個技巧就是 **如何在 Excel 中建立陣列**‑樣式溢位範圍的核心，無需手動寫入每一格。

---

## 第三步：如何使用 COT – 加入三角函數公式

如果你也想了解 **如何在 Excel 公式中使用 cot**，`COT` 函數可以直接取得以弧度表示的角度的餘切值。讓我們計算 `cot(π/4)`，結果應該是 **1**。

```csharp
        // Write a simple trigonometric formula that calculates cotangent of 45° (π/4)
        // COT(π/4) evaluates to 1
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

請注意，我們使用 `PI()` 取得 180° 的弧度值，再除以 4 取得 45°。Excel 會自行完成計算，儲存格 **B1** 在開啟活頁簿後會顯示 `1`。這示範了 **如何使用 cot** 進行快速工程或金融計算，而不必額外引用數學函式庫。

---

## 第四步：將活頁簿儲存為 XLSX – 檔案持久化

如果不把檔案寫入磁碟，前面的所有陣列與公式操作都毫無意義。以下是使用 Aspose.Cells **將活頁簿儲存為 xlsx** 的最直接方式：

```csharp
        // Save the workbook to verify the formulas (optional)
        string outputPath = @"C:\Temp\output.xlsx";   // adjust to your folder
        workbook.Save(outputPath, SaveFormat.Xlsx);

        // Let the user know we’re done
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

為什麼要指定 `SaveFormat.Xlsx`？它保證使用現代的 OpenXML 格式，能被所有主流軟體（Excel、LibreOffice、Google Sheets）讀取。如果需要舊版的 `.xls` 檔，只要把列舉值換成相應的格式即可。

---

## 完整範例（結合所有步驟）

以下是完整、可直接執行的程式。將它貼到 Console 專案中，還原 Aspose.Cells NuGet 套件，然後按 **F5**。

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Create a dynamic spill range (how to create array)
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";

        // Step 3: Calculate cotangent (how to use cot)
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";

        // Step 4: Persist the file (save workbook as xlsx)
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**預期結果**（開啟 `output.xlsx` 後）：

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 1 |   |   |   |
| 2 |   |   |   |   |
| 3 |   |   |   |   |

- A 欄顯示由 `SEQUENCE` 產生的 1‑3 數字。  
- B 欄則是 `COT` 公式計算出的 **1**。  
- C‑E 欄為空白，說明了 `EXPAND` 的填充效果。

---

## 常見問題與例外情況

### 如果需要更多列或欄該怎麼辦？

只要調整 `SEQUENCE` 與 `EXPAND` 的參數即可。  
- `SEQUENCE(10,2,5,2)` 會產生 10 列 × 2 欄的矩陣，起始值為 5，遞增步長為 2。  
- `EXPAND(...,10,5)` 會將結果填充至 10 欄、5 列。

### 這在舊版 Excel 能用嗎？

動態陣列函數（`SEQUENCE`、`EXPAND`）需要 Excel 365 或 2019 以上版本。對於舊版檔案，你可以改用傳統公式，或直接透過 `Cells[row, col].PutValue(value)` 寫入值。

### 可以使用 R1C1 風格寫入公式嗎？

當然可以。把 `A1` 換成 `Cells[0, 0]`，並使用 `FormulaR1C1` 屬性：

```csharp
worksheet.Cells[0, 0].FormulaR1C1 = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

### 文化特定的十進位分隔符怎麼處理？

Aspose.Cells 會遵循活頁簿的語系設定。若需指定特定文化，可在寫入公式前設定  
`workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");`

---

## 視覺摘要

![如何在 Excel 中使用 C# 建立陣列](/images/how-to-create-array-excel-csharp.png "如何在 Excel 中使用 C# 建立陣列")

*螢幕截圖顯示最終的溢位範圍與餘切計算結果。*

---

## 結論

以上就是 **如何在 Excel 中使用 C# 建立陣列** 的完整步驟，從產生序列號、運用 `COT` 函數，到 **將活頁簿儲存為 XLSX**，全部寫在同一個簡潔的程式中。重點摘要如下：

1. 使用 `Workbook` 與 `Worksheet` 物件開啟 Excel 自動化的入口。  
2. 利用動態陣列函數（`SEQUENCE`、`EXPAND`）打造彈性溢位範圍。  
3. 透過 `COT` 等三角函數，快速完成數學運算，無需額外函式庫。  
4. 使用 `SaveFormat.Xlsx` 將結果持久化，產出通用的檔案格式。

準備好進一步挑戰了嗎？試著把 `COT(PI()/4)` 換成其他角度的計算，看看會得到什麼結果吧。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}