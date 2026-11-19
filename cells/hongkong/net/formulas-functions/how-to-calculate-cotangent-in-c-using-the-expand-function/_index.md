---
category: general
date: 2026-11-19
description: 學習如何在 C# 中計算餘切，方法是將公式加入儲存格，使用 EXPAND 函數，並使用 Aspose.Cells 評估所有公式。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to calculate cotangent
- how to use expand
- add formula to cell
- evaluate all formulas
- use expand function
language: zh-hant
lastmod: 2026-11-19
og_description: 如何在 C# 中計算餘切？本教學將示範如何向儲存格加入公式、使用 EXPAND 函數，並使用 Aspose.Cells 評估所有公式。
og_image_alt: C# code snippet adding Excel formulas with Aspose.Cells
og_title: 如何在 C# 中使用 EXPAND 計算餘切 – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to calculate cotangent in C# by adding formulas to cells,
    using the EXPAND function, and evaluating all formulas with Aspose.Cells.
  headline: How to calculate cotangent in C# using the EXPAND function
  type: TechArticle
- description: Learn how to calculate cotangent in C# by adding formulas to cells,
    using the EXPAND function, and evaluating all formulas with Aspose.Cells.
  name: How to calculate cotangent in C# using the EXPAND function
  steps:
  - name: Creates a workbook and accesses the first worksheet.
    text: Creates a workbook and accesses the first worksheet.
  - name: Writes an `EXPAND` formula that turns a single value into a 5‑row array.
    text: Writes an `EXPAND` formula that turns a single value into a 5‑row array.
  - name: Writes a `COT` formula that **how to calculate cotangent** of π/4.
    text: Writes a `COT` formula that **how to calculate cotangent** of π/4.
  - name: Forces the engine to **evaluate all formulas** so the values are stored
      in the file.
    text: Forces the engine to **evaluate all formulas** so the values are stored
      in the file.
  - name: '**Validate source data** – check that cells referenced by `EXPAND` or `COT`
      contain numbers to avoid `#VALUE!` errors.'
    text: '**Validate source data** – check that cells referenced by `EXPAND` or `COT`
      contain numbers to avoid `#VALUE!` errors.'
  - name: '**Reuse the workbook object** – creating a single `Workbook` instance and
      reusing it for multiple operations reduces memory overhead.'
    text: '**Reuse the workbook object** – creating a single `Workbook` instance and
      reusing it for multiple operations reduces memory overhead.'
  - name: '**Save in the appropriate format** – `.xlsx` retains dynamic‑array formulas;
      `.xls` will downgrade them to static values.'
    text: '**Save in the appropriate format** – `.xlsx` retains dynamic‑array formulas;
      `.xls` will downgrade them to static values.'
  - name: '**Wrap calculations in try/catch** – formula parsing can throw `CellsException`
      if the syntax is invalid.'
    text: '**Wrap calculations in try/catch** – formula parsing can throw `CellsException`
      if the syntax is invalid.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- formulas
title: 如何在 C# 中使用 EXPAND 函數計算餘切
url: /zh-hant/net/formulas-functions/how-to-calculate-cotangent-in-c-using-the-expand-function/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 EXPAND 函數計算餘切

如果你需要在 C# 中於 .xlsx 檔案**計算餘切**，本指南提供完整、可直接執行的解決方案。你將會看到如何**將公式加入儲存格**、利用**EXPAND**函數產生動態陣列，最後**評估所有公式**，使活頁簿內含計算結果。

以程式方式操作 Excel 通常需要處理儲存格參照、陣列公式與自訂函式。完成本教學後，你將擁有一個單一的 C# 程式，能夠：

1. 建立活頁簿並存取第一個工作表。  
2. 寫入 `EXPAND` 公式，將單一數值轉換為 5 列陣列。  
3. 寫入 `COT` 公式，**計算餘切** π/4。  
4. 強制引擎**評估所有公式**，使值儲存於檔案中。  

此方法適用於最新的 Aspose.Cells for .NET（撰寫時為 v23.12），且僅需 NuGet 套件 `Aspose.Cells`。不需要外部的 Excel 安裝。

## 前置條件

- .NET 6.0 SDK 或更新版本（此程式碼亦可在 .NET Framework 4.7.2 上編譯）。  
- Visual Studio 2022 或任何支援 C# 的 IDE。  
- NuGet 套件 **Aspose.Cells** (`Install-Package Aspose.Cells`)。  

> **專業提示：** 若你使用 CI/CD 流水線，請將套件參考加入專案檔，而非全域安裝。這可確保可重現的建置。

## 步驟 1：建立活頁簿並存取第一個工作表

Workbook 物件是所有試算表操作的入口點。於記憶體中建立它可避免任何檔案系統的副作用，直到你明確儲存為止。

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 1 – instantiate a new workbook and get the first worksheet
        Workbook wb = new Workbook();               // empty workbook with one sheet
        Worksheet ws = wb.Worksheets[0];            // reference to Sheet1
```

**為何重要：**  
Aspose.Cells 會自動建立預設工作表 (`Sheet1`)。透過 `Worksheets[0]` 存取可確保寫入已知位置，從而避免日後出現「找不到工作表」的錯誤。

## 步驟 2：加入 EXPAND 讀取的簡單數值

`EXPAND` 函數需要來源儲存格。此處我們在 **B1** 放入一個數值，該值將被展開為垂直陣列。

```csharp
        // Step 2 – write a source value in B1
        ws.Cells["B1"].PutValue(42);   // any numeric value works
```

**邊緣情況：** 若 `B1` 為空，`EXPAND` 會回傳 `#VALUE!` 錯誤。務必確保來源儲存格包含有效的數字或會解析為數字的公式。

## 步驟 3：使用 EXPAND 函數產生 5 列陣列

現在我們在 **A1** 寫入公式，將 **B1** 的值展開為 5 列 1 欄的範圍。此示範 **如何使用 expand**，同時也提及 **使用 expand 函數**。

```csharp
        // Step 3 – write the EXPAND formula in A1
        // =EXPAND(B1,5,1) creates a vertical array of 5 rows based on B1
        ws.Cells["A1"].Formula = "=EXPAND(B1,5,1)";
```

**為何使用 EXPAND？**  
`EXPAND` 是在 Excel 365 中引入的動態陣列函數。它消除對傳統 `Ctrl+Shift+Enter` 陣列公式的需求，並自動將結果溢出至相鄰儲存格。在此範例中，結果會佔據 **A1:A5**，每個儲存格顯示數值 `42`。

## 步驟 4：寫入 **計算餘切** 的公式

角度 θ 的餘切為 `1 / tan(θ)`。Excel 內建 `COT` 函數，我們可以直接計算 `cot(π/4)`。結果應為 `1`。

```csharp
        // Step 4 – calculate cotangent of π/4 in A2
        ws.Cells["A2"].Formula = "=COT(PI()/4)";
```

**說明：**  
- `PI()` 回傳數學常數 π。  
- `PI()/4` 會計算出 π/4（45 度）。  
- `COT` 回傳該角度的餘切，即 `1`。  

如果你需要計算儲存在儲存格中的變動角度的餘切（例如 `B2`），只需將常數改為參照：`=COT(B2)`。

## 步驟 5：強制活頁簿 **評估所有公式**

預設情況下，Aspose.Cells 只會將公式寫入檔案而不計算結果。若要儲存計算後的值，請呼叫 `CalculateFormula()`。

```csharp
        // Step 5 – evaluate every formula in the workbook
        wb.CalculateFormula();
```

**背後發生了什麼？**  
Aspose.Cells 會解析每個公式，建立執行樹，並使用其自有的計算引擎計算值。此行為與 Excel 相同，確保儲存的檔案內含結果而非僅有公式。

## 步驟 6：儲存活頁簿並驗證輸出

最後，將活頁簿寫入磁碟，並可選擇將計算出的值印至主控台，以快速驗證。

```csharp
        // Step 6 – save the workbook
        string outPath = "CotangentAndExpandDemo.xlsx";
        wb.Save(outPath);

        // Optional: display calculated values in the console
        Console.WriteLine("A1–A5 (EXPAND result):");
        for (int row = 0; row < 5; row++)
        {
            Console.WriteLine($"A{row + 1} = {ws.Cells[row, 0].StringValue}");
        }
        Console.WriteLine($"A2 (COT result) = {ws.Cells["A2"].StringValue}");
        Console.WriteLine($"Workbook saved to {outPath}");
    }
}
```

### 預期輸出

執行程式時，主控台會顯示：

```
A1–A5 (EXPAND result):
A1 = 42
A2 = 42
A3 = 42
A4 = 42
A5 = 42
A2 (COT result) = 1
Workbook saved to CotangentAndExpandDemo.xlsx
```

在 Excel 中開啟 *CotangentAndExpandDemo.xlsx* 可確認：  

- 儲存格 **A1:A5** 含有 `42`（展開的陣列）。  
- 儲存格 **A2** 顯示 `1`（π/4 的餘切）。  

所有公式皆已被其計算值取代，因為我們呼叫了 `wb.CalculateFormula()`。

## 常見問題與疑難排解

| Question | Answer |
|----------|--------|
| **如果需要水平陣列該怎麼辦？** | 使用 `=EXPAND(B1,1,5)` – 第二個參數（`rows`）變為 1，第三個參數（`columns`）變為 5，結果會溢出至 **A1:E1**。 |
| **我可以展開一個範圍而非單一儲存格嗎？** | 可以。`=EXPAND(B1:B3,5,1)` 會重複三列來源以填滿 5 列的結果，必要時會截斷或填充。 |
| **為什麼 `COT` 會對某些角度回傳 `#DIV/0!`？** | `COT(θ) = 1 / tan(θ)`。若 `tan(θ)` 為零（例如 θ = 0、π、2π），結果未定義，會產生除以零錯誤。 |
| **需要啟用任何計算選項嗎？** | 不需要。當呼叫 `CalculateFormula()` 時，Aspose.Cells 會自動啟用完整計算模式。 |
| **舊版 Excel 是否支援 EXPAND 函數？** | `EXPAND` 需要 Excel 365 或更新版本。若目標為較舊版本，請考慮使用傳統陣列公式或透過程式碼手動填入儲存格。 |

## 使用 Aspose.Cells 處理公式的最佳實踐

1. **驗證來源資料** – 檢查 `EXPAND` 或 `COT` 參考的儲存格是否為數字，以避免 `#VALUE!` 錯誤。  
2. **重複使用 workbook 物件** – 建立單一 `Workbook` 實例並在多個操作中重用，可減少記憶體開銷。  
3. **以適當格式儲存** – `.xlsx` 會保留動態陣列公式；`.xls` 會將其降級為靜態值。  
4. **將計算包在 try/catch 中** – 若公式語法無效，解析時可能拋出 `CellsException`。  

## 結論

現在你已了解如何在 C# 中**計算餘切**，透過**將公式加入儲存格**、使用 **EXPAND** 函數產生動態陣列，並以 Aspose.Cells **評估所有公式**。完整範例展示了從建立活頁簿到驗證結果的清晰工作流程，隨時可整合至更大型的報表或資料處理管線中。

接下來的步驟可以探索：

- **如何使用 expand** 於多欄位陣列以處理矩陣式資料。  
- **將公式加入儲存格**，根據使用者輸入或設定檔動態產生。  
- **評估所有公式**，在多工作表活頁簿中使用自訂計算設定（例如迭代計算）。  

歡迎嘗試其他數學函數（`SIN`、`COS`、`TAN`、`COT`），並與 `EXPAND` 結合，直接在 C# 中打造強大的試算表驅動計算器。祝開發愉快

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在所示技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [如何在 Excel 中使用 C# 計算餘切 – 步驟指南](/cells/english/net/excel-formulas-and-calculation-options/how-to-calculate-cotangent-in-excel-with-c-step-by-step-guid/)
- [如何在 C# 中評估公式 – 完整 Aspose.Cells 指南](/cells/english/net/calculation-engine/how-to-evaluate-formulas-in-c-complete-aspose-cells-guide/)
- [如何在 C# 中使用 Aspose.Cells 展開陣列 – 步驟指南](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}