---
category: general
date: 2026-03-30
description: 使用 Aspose.Cells 於 C# 建立 Excel 工作簿。學習在 Excel 中套用 lambda 函數、sequence 函數、展開陣列，並將工作簿儲存為
  xlsx。
draft: false
keywords:
- create excel workbook c#
- lambda function excel
- save workbook as xlsx
- sequence function excel
- expand array excel
language: zh-hant
og_description: 快速使用 C# 建立 Excel 工作簿。本指南說明如何在 Excel 中使用 Lambda 函數、序列函數、展開陣列，並將工作簿另存為
  xlsx。
og_title: 使用 C# 建立 Excel 工作簿 – Lambda、SEQUENCE 與 EXPAND 指南
tags:
- Aspose.Cells
- C#
- Excel automation
title: 使用 C# 建立 Excel 工作簿 – Lambda、SEQUENCE 與 EXPAND 指南
url: /zh-hant/net/formulas-functions/create-excel-workbook-c-lambda-sequence-expand-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 Excel 工作簿 C# – Lambda、SEQUENCE 與 EXPAND 指南

是否曾需要 **create Excel workbook C#** 來產生自動化報告，但不確定該使用哪個 API 呼叫？你並不孤單——許多開發者在首次接觸程式化 Excel 產生時都會遇到相同的障礙。在本指南中，你將看到一個完整、可執行的範例，涵蓋從全新的 **SEQUENCE function Excel** 到強大的 **LAMBDA function Excel**，甚至如何 **expand array Excel** 結果。

我們也會示範如何使用 **save workbook as xlsx** 的精確步驟，讓你能將檔案交給任何使用 Excel 的人。完成本教學後，你將擁有一段穩固、可直接投入生產環境的程式碼片段，能放入任何 .NET 專案中。沒有模糊的「請參考文件」連結——只有即刻可用的程式碼。

## 你需要的條件

- **.NET 6.0 或更新版本** – 本範例以 .NET 6 為目標，但任何較新的版本皆可運作。  
- **Aspose.Cells for .NET** – 透過 NuGet 安裝 (`Install-Package Aspose.Cells`)。  
- 具備基本的 C# 語法概念（變數、物件與 lambda 表達式）。  
- 使用你熟悉的 IDE（Visual Studio、Rider 或 VS Code）。  

就這樣。無需額外的 COM interop，也不需要在伺服器上安裝 Office——Aspose.Cells 會在記憶體中處理所有工作。

## 建立 Excel 工作簿 C# – 步驟式實作

以下我們將流程拆解為易於消化的步驟。每個步驟都有清晰的標題、簡短的程式碼片段，以及說明 **為何** 這樣做。隨意複製最後的完整程式碼塊，將其作為主控台應用程式執行。

### 步驟 1 – 初始化新工作簿

首先，我們需要一個空白的工作簿物件，代表記憶體中的 Excel 檔案。

```csharp
using Aspose.Cells;

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // empty workbook
Worksheet sheet = workbook.Worksheets[0];         // default first sheet
```

*Why this matters:* `Workbook` 是所有 Aspose.Cells 操作的入口點。取得第一個 `Worksheet` 後，我們就得到一個可以寫入公式、數值或格式的畫布。

> **Pro tip:** 若需要多個工作表，只要呼叫 `workbook.Worksheets.Add()` 並保留對每個工作表的參考即可。

### 步驟 2 – 使用 SEQUENCE function Excel 產生資料

**sequence function excel** 會在不使用 VBA 的情況下建立動態數字陣列。我們將它放在 `A1` 儲存格，讓 Excel 自動展開。

```csharp
// Step 2: Generate a 5‑row, 1‑column array from a SEQUENCE
sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)"; // 1..3 padded with blanks
```

*Why this matters:* `SEQUENCE(3)` 會產生 `[1,2,3]`。將其包裹在 `EXPAND` 中會將結果強制展開為 5 列的範圍，額外的列會以空白填充。這同時示範了 **sequence function excel** 與 **expand array excel**。

### 步驟 3 – 使用 LAMBDA function Excel 彙總數字

現在讓我們展示 **lambda function excel** 的功能。我們將使用新推出的 `REDUCE` 函數（內部依賴 lambda）來加總 1‑5 的數字。

```csharp
// Step 3: Aggregate a sequence (sum 1..5) using REDUCE/LAMBDA
sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))"; // result = 15
```

*Why this matters:* `REDUCE` 會遍歷由 `SEQUENCE(5)` 產生的陣列，將每個元素（`b`）與累加器（`a`）一起傳入 lambda。lambda `a+b` 將它們相加，最終在 `B1` 中得到 `15`。這是一種純公式、無需在 C# 中迴圈的簡潔縮減方式。

### 步驟 4 – 直接在儲存格中套用三角函數

Excel 內建的數學函數非常適合快速計算。我們將在相鄰的儲存格中放入餘切與雙曲餘切。

```csharp
// Step 4: Trigonometric functions directly in Excel cells
sheet["C1"].Formula = "COT(PI()/4)";   // evaluates to 1
sheet["D1"].Formula = "COTH(1)";      // hyperbolic cotangent of 1
```

*Why this matters:* 示範了可以將傳統數學函數與較新的動態陣列公式混合使用。除非有特定的效能需求，否則無需在 C# 中計算這些值。

### 步驟 5 – 計算所有公式

當設定公式時，Aspose.Cells 不會自動評估。必須明確要求它計算。

```csharp
// Step 5: Force calculation so that cells store the results
workbook.CalculateFormula();
```

*Why this matters:* 呼叫此方法後，每個儲存格的 `Value` 屬性會包含已評估的結果，隨時可保存或讀取。

### 步驟 6 – 將工作簿儲存為 Xlsx

最後，我們使用 **save workbook as xlsx** 的方式將工作簿寫入磁碟。

```csharp
// Step 6: Save the workbook to an Excel file (XLSX format)
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "NewFunctions.xlsx");

workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

*Why this matters:* `Save` 方法會自動偵測檔案副檔名。使用「.xlsx」即可確保檔案相容於現代 Excel 版本。路徑指向桌面，方便測試時快速存取。

### 完整可執行範例

以下是完整的程式碼，你可以貼到新的主控台專案中。它包含上述所有步驟，並加入一個小型驗證區塊，將計算結果輸出至主控台。

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Initialize workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // SEQUENCE + EXPAND
        sheet["A1"].Formula = "EXPAND(SEQUENCE(3),5,1)";

        // REDUCE with LAMBDA
        sheet["B1"].Formula = "REDUCE(0, SEQUENCE(5), LAMBDA(a,b, a+b))";

        // Trig functions
        sheet["C1"].Formula = "COT(PI()/4)";
        sheet["D1"].Formula = "COTH(1)";

        // Calculate formulas
        workbook.CalculateFormula();

        // Verify results (optional)
        Console.WriteLine("A1‑A5 (expanded SEQUENCE):");
        for (int i = 0; i < 5; i++)
        {
            Console.WriteLine($"  Row {i + 1}: {sheet.Cells[i, 0].Value ?? "blank"}");
        }
        Console.WriteLine($"B1 (sum 1‑5): {sheet["B1"].Value}");
        Console.WriteLine($"C1 (cot(π/4)): {sheet["C1"].Value}");
        Console.WriteLine($"D1 (coth(1)): {sheet["D1"].Value}");

        // Save workbook
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "NewFunctions.xlsx");
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

**預期在主控台的輸出**

```
A1‑A5 (expanded SEQUENCE):
  Row 1: 1
  Row 2: 2
  Row 3: 3
  Row 4: blank
  Row 5: blank
B1 (sum 1‑5): 15
C1 (cot(π/4)): 1
D1 (coth(1)): 1.31303528549933
Workbook saved to: C:\Users\YourName\Desktop\NewFunctions.xlsx
```

當你開啟 *NewFunctions.xlsx* 時，會看到相同的數字排列在前四欄。

![create excel workbook c# screenshot of the resulting spreadsheet](/images/create-excel-workbook-csharp.png)

## 邊緣情況、技巧與常見問題

- **如果需要多於一個工作表該怎麼辦？**  
  只要呼叫 `workbook.Worksheets.Add()`，然後在每個新的 `Worksheet` 物件上重複公式設定即可。  

- **我可以使用較舊的 Excel 版本嗎？**  
  動態陣列函數（`SEQUENCE`、`EXPAND`、`REDUCE`）需要 Excel 365 或 Excel 2021 以上。若要支援較舊版本，請改用傳統公式或在寫入前於 C# 中計算數值。  

- **效能問題？**  
  對於數千列的情況，在整個範圍設定公式後再呼叫 `CalculateFormula`，通常比逐一迴圈指派值更快。  

- **改為儲存至串流而非檔案？**  
  `work

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}