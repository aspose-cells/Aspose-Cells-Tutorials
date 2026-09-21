---
category: general
date: 2026-03-22
description: 如何在 C# 中使用 lambda 來處理 Excel 公式。學習將公式寫入儲存格、將範圍轉換為陣列、在主控台顯示陣列，以及在 Excel
  中計算餘切。
draft: false
keywords:
- how to use lambda
- display array in console
- convert range to array
- write formula to cell
- calculate cotangent in excel
language: zh-hant
og_description: 如何在 C# 中使用 lambda 操作 Excel 公式、將範圍轉換為陣列、將公式寫入儲存格、在主控台顯示陣列，以及在 Excel
  中計算餘切。
og_title: 如何在 C# 中使用 Lambda 搭配 Excel 公式 – 步驟說明
tags:
- C#
- Aspose.Cells
- Excel Automation
- Lambda Expressions
title: 如何在 C# 中使用 Lambda 搭配 Excel 公式 – 完整指南
url: /zh-hant/net/formulas-functions/how-to-use-lambda-in-c-with-excel-formulas-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 Lambda 搭配 Excel 公式 – 完整指南

有沒有想過在 C# 自動化 Excel 時 **如何使用 lambda**？你並不孤單。許多開發者在需要將 Excel 全新的動態陣列函數與 C# 的 `LAMBDA` 功能結合時，常會卡關。好消息是？只要看清楚各個部件如何配合，這其實相當簡單。

在本教學中，我們將逐步說明 **將公式寫入儲存格**、**將範圍轉換為陣列**、**在主控台顯示該陣列**，甚至 **在 Excel 中計算餘切**——同時示範 **如何在 `REDUCE` 呼叫中使用 lambda**。完成後，你將得到一段可直接放入任何引用 Aspose.Cells（或類似函式庫）的 .NET 專案的可執行程式碼。

---

## 你將學會

- 如何使用 C# **將公式寫入儲存格**。  
- 如何使用 `EXPAND` 函數 **將範圍轉換為陣列**。  
- 如何在計算完畢後 **在主控台顯示陣列**。  
- 如何使用 `COT` 與 `COTH` **在 Excel 中計算餘切**。  
- 從 C# 呼叫 Excel 的 `REDUCE` 函數時 **如何使用 lambda** 的完整語法。

> **先備條件：** 需要安裝 .NET（Core 6+ 或 .NET Framework 4.7+）以及透過 NuGet 安裝 Aspose.Cells for .NET 函式庫。

---

## 步驟 1：建立活頁簿並將公式寫入儲存格

首先，我們會新建一個活頁簿並取得第一張工作表。接著 **將公式寫入儲存格**——此例中 `A1` 會放置 `EXPAND` 的結果。

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write formula to A1 – we’ll expand B1:C2 into a 4‑by‑5 array later
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";
```

**為什麼這很重要：** 直接從程式碼寫入公式，讓你能在不開啟 Excel 的情況下即時產生複雜的試算表。這也為下一步 **將範圍轉換為陣列** 打下基礎。

---

## 步驟 2：使用 EXPAND 將範圍轉換為陣列

`EXPAND` 是 Excel 用來把小範圍展開成更大矩陣的功能。將公式放在 `A1` 後，Excel 會自動在該儲存格向下向右溢出成 4 × 5 的區塊。從 C# 端，我們不必手動複製值——在呼叫 `Calculate` 時，函式庫會自動完成這項工作。

```csharp
        // The EXPAND formula will spill into A1:E4 (4 rows × 5 columns)
        // No extra code needed – the workbook will handle the spill.
```

**如何使用 lambda：** 暫時還沒出現，稍後會說明。先取得工作表中的資料，之後再以 lambda 進行縮減。

---

## 步驟 3：在 REDUCE 中使用 LAMBDA – 「如何使用 Lambda」的核心

Excel 365 引入了 `REDUCE`，它接受 **初始值**、**範圍** 以及一個 **LAMBDA**，用來定義如何合併每個元素。從 C# 只要把公式字串指定給儲存格即可，lambda 會寫在 Excel 公式內，而不是 C# 程式碼中。

```csharp
        // Reduce the spilled array by summing all its values.
        // This demonstrates how to use lambda inside REDUCE.
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";
```

**說明：**  
- `0` 為起始累加器（`acc`）。  
- `A1:D4` 為要處理的範圍（溢出結果的前四欄）。  
- `LAMBDA(acc, x, acc + x)` 告訴 Excel 把每個儲存格 (`x`) 加到累加器上。

這就是在試算表環境中 **如何使用 lambda** 進行聚合的精髓。

---

## 步驟 4：在 Excel 中計算餘切 – 從角度到雙曲

若需要三角函數結果，Excel 的 `COT` 與 `COTH` 非常好用。我們會分別把它們放在 `G1` 與 `G2`。

```csharp
        // Demonstrate trigonometric functions – cotangent and hyperbolic cotangent
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected result: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";      // Hyperbolic cotangent of 1
```

**為什麼實用：** 熟悉 **在 Excel 中計算餘切** 能讓你免除自行撰寫數學程式碼，特別是當活頁簿要與非開發人員共享時。

---

## 步驟 5：強制計算並取得展開的陣列

現在讓活頁簿評估所有公式，然後從 `A1` 取回溢出的陣列。這一步會把結果 **顯示在主控台**。

```csharp
        // Force calculation of all formulas
        workbook.Calculate();

        // Retrieve the spilled array from A1 as a 2‑D object
        var expanded = worksheet.Cells["A1"].Value;

        // Pretty‑print the 2‑D array to the console
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show the result of the REDUCE lambda
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**你會看到的內容：**  
- 以列為單位印出的整齊 4 × 5 矩陣。  
- 由 `REDUCE` lambda 計算出的總和。  
- 兩個餘切值。

至此，從 **將公式寫入儲存格** 到 **在主控台顯示陣列** 的完整流程已完成。

---

## 完整範例（直接複製貼上）

以下程式碼可直接放入 Console 應用程式。記得先加入 `Aspose.Cells` NuGet 套件（`dotnet add package Aspose.Cells`）。

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Write EXPAND formula (convert range to array)
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";

        // Step 3: Use REDUCE with LAMBDA (how to use lambda)
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";

        // Step 4: Calculate cotangent values (calculate cotangent in excel)
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";

        // Step 5: Force calculation
        workbook.Calculate();

        // Step 6: Retrieve and display the expanded array (display array in console)
        var expanded = worksheet.Cells["A1"].Value;
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show REDUCE result
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**預期的主控台輸出（數值會依 B1:C2 的預設內容而異，預設皆為 0）：**

```
Expanded array from A1 (4×5):
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0

Sum of A1:D4 (via REDUCE lambda): 0
Cotangent of π/4: 1
Hyperbolic cotangent of 1: 1.31303528549933
```

在執行前可自行在 `B1:C2` 填入數字——矩陣會即時反映這些值。

---

## 專業小技巧與常見陷阱

- **小技巧：** 若想讓溢出範圍從其他位置開始，只需更改目標儲存格（`A1`）。`EXPAND` 會遵循新的錨點。  
- **注意事項：** 來源範圍的空白儲存格會在溢出陣列中變成 `0`，可能會影響 `REDUCE` 的加總結果。  
- **邊緣情況：** 若活頁簿內含依賴易變函數（例如 `NOW()`）的公式，請在設定完所有公式後呼叫 `workbook.Calculate()`，確保計算結果為最新。  
- **效能提醒：** 對於巨大的溢出區域，建議在 `EXPAND` 呼叫中限制大小，否則可能會分配過多記憶體。  
- **相容性：** The `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}