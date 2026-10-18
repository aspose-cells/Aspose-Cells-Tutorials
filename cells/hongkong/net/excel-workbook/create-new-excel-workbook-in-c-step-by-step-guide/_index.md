---
category: general
date: 2026-02-15
description: 建立新的 Excel 活頁簿，學習如何使用 EXPAND、展開序列及計算餘切。亦可了解如何將活頁簿儲存為檔案。
draft: false
keywords:
- create new excel workbook
- save workbook to file
- how to use expand
- how to expand sequence
- how to calculate cotangent
language: zh-hant
og_description: 使用 C# 建立新的 Excel 活頁簿。學習如何使用 EXPAND、展開序列、計算餘切，並將活頁簿儲存至檔案。
og_title: 在 C# 中建立新的 Excel 活頁簿 – 完整程式設計指南
tags:
- C#
- Aspose.Cells
- Excel automation
title: 在 C# 中建立新的 Excel 活頁簿 – 逐步指南
url: /zh-hant/net/excel-workbook/create-new-excel-workbook-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中建立新的 Excel 工作簿 – 完整程式指南

是否曾需要從程式碼 **create new Excel workbook**，卻不知從何開始？你並不孤單；許多開發者在自動化報告或建構資料管線時都會碰到這個問題。在本教學中，我們將完整示範如何 create new Excel workbook、寫入幾個有趣的公式，然後 **save workbook to file** 以供日後檢查。  

我們還會深入探討 `EXPAND` 函數的細節，示範 **how to use expand** 如何將小型序列擴展成大區塊，說明 **how to expand sequence** 的實作方式，最後揭示 **how to calculate cotangent** 在 Excel 內直接計算。完成後，你將擁有一個可直接放入任何 .NET 專案的可執行 C# 程式。

## 需要的環境

- **Aspose.Cells for .NET**（免費試用或授權版）– 讓我們在未安裝 Office 的情況下操作 Excel 的函式庫。  
- **.NET 6+**（或 .NET Framework 4.6+）。  
- 一個簡易的 IDE，例如 Visual Studio 2022、VS Code 或 Rider。  

除了 `Aspose.Cells` 之外不需要其他 NuGet 套件。如果尚未安裝，請執行以下指令：

```bash
dotnet add package Aspose.Cells
```

就這樣——不需要其他設定。

## 步驟 1：建立新的 Excel 工作簿

我們首先要做的事是實例化一個 `Workbook` 物件。可以把它想像成所有工作表、儲存格與公式的空白畫布。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];    // default sheet is named "Sheet1"
```

> **為什麼重要：** 在記憶體中建立工作簿表示在明確執行 **save workbook to file** 之前，我們不會觸及磁碟。這樣可保持操作快速，且能在不產生 I/O 負擔的情況下串接後續修改。

## 步驟 2：如何使用 EXPAND 來展開序列

`EXPAND` 是較新的 Excel 函數，能將較小的陣列延伸至指定大小。在本例中，我們從三列的垂直序列開始，將其展開為 5 × 5 的區塊。

```csharp
        // Step 2: Write a formula that expands a 3‑row sequence into a 5×5 block
        // The formula lives in A1 and will spill over to E5
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3),5,5)";
```

> **說明：** `SEQUENCE(3)` 產生 `{1;2;3}`（垂直陣列）。`EXPAND(...,5,5)` 告訴 Excel 重複該陣列，直到填滿從 A1 開始的 5 列 5 欄矩形。結果是一個矩陣，每欄都重複原始的三個數字，最後兩列為空白，因為來源只有三列。

### 預期輸出

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 1 | 1 | 1 | 1 |
| 2 | 2 | 2 | 2 | 2 |
| 3 | 3 | 3 | 3 | 3 |
|   |   |   |   |   |
|   |   |   |   |   |

## 步驟 3：如何在 Excel 中計算餘切

大多數人熟悉 `SIN`、`COS` 與 `TAN`，但 `COT` 是計算正切倒數的便利快捷方式。以下示範如何使用弧度取得 45°（即 1）的餘切值。

```csharp
        // Step 3: Write a formula that returns the cotangent of 45° (π/4 radians)
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

> **為什麼使用 COT？** 直接呼叫 `COT` 可避免使用 `1/TAN(...)` 所需的額外除法，使公式更清晰，且在大型工作表上稍微提升效能。

## 步驟 4：評估所有公式

除非明確指示，Aspose.Cells 不會自動計算公式。`CalculateFormula` 方法會強制完整評估，將結果值儲存於儲存格中。

```csharp
        // Step 4: Evaluate all formulas so the results are stored in the cells
        workbook.CalculateFormula();
```

> **小技巧：** 若有大量計算成本高的公式，可傳入 `CalculationOptions` 物件以微調效能（例如啟用多執行緒）。

## 步驟 5：將工作簿儲存至檔案

現在一切就緒，我們終於 **save workbook to file**。選擇一個具有寫入權限的資料夾，並為檔案命名一個有意義的名稱。

```csharp
        // Step 5: Save the workbook to a file for inspection
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath);
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

> **磁碟上會發生什麼？** `Save` 呼叫會寫入完整的 `.xlsx` 套件，包含來自 `EXPAND` 的展開陣列與計算出的餘切值。以 Excel 開啟檔案，即可看到從 A1 開始的 5 × 5 區塊，以及 B1 中的數值 `1`。

![Excel 輸出顯示展開序列與餘切值](excel-output.png "建立新 Excel 工作簿範例輸出")

*圖片替代文字：建立新 Excel 工作簿範例輸出*

### 快速驗證

1. 開啟 `output.xlsx`。  
2. 檢查儲存格 **A1:E5** 是否包含重複的 1‑2‑3 模式。  
3. 查看 **B1**——應顯示 `1`。  

如果一切符合，恭喜你——已成功自動化 Excel！

## 如何在其他情境下展開序列

雖然上述範例使用靜態的 `SEQUENCE(3)`，但你可以輕鬆將其換成動態範圍或其他公式：

```csharp
// Expand a dynamic range from D1:D10 to a 4×4 block
worksheet.Cells["F1"].Formula = "=EXPAND(D1:D10,4,4)";
```

**何時使用？**  
- 為範本產生佔位表格。  
- 快速在多個欄位複製標題列。  
- 建立熱圖格子，免於手動複製貼上。

## 常見陷阱與避免方法

| 問題 | 發生原因 | 解決方式 |
|------|----------|----------|
| `EXPAND` 後出現 `#VALUE!` | 來源陣列不是有效範圍（例如包含錯誤） | 清理來源資料或使用 `IFERROR` 包裹。 |
| 0° 時餘切返回 `#DIV/0!` | `COT(0)` 在數學上為無限大 | 使用 `IF(PI()/4=0,0,COT(...))` 進行防護。 |
| 工作簿未儲存 | 路徑無效或缺少寫入權限 | 使用 `Path.GetFullPath` 並確認資料夾存在。 |
| 公式未計算 | 未呼叫 `CalculateFormula` | 一定要在 `Save` 前呼叫它。 |

## 加分項：加入樣式（可選）

如果想讓輸出更美觀，可以在計算完成後套用簡單樣式：

```csharp
        // Apply a light gray background to the expanded block
        Style style = workbook.CreateStyle();
        style.Pattern = BackgroundType.Solid;
        style.ForegroundColor = System.Drawing.Color.LightGray;
        StyleFlag flag = new StyleFlag { CellShading = true };
        worksheet.Cells.CreateRange("A1:E5").ApplyStyle(style, flag);
```

此程式碼片段為可選，但它示範了如何在一次流程中結合 **create new Excel workbook** 邏輯與格式設定。

## 重點回顧

1. 使用 Aspose.Cells **create new Excel workbook**。  
2. 使用 **how to use expand** 將小型 `SEQUENCE` 轉為 5 × 5 矩陣。  
3. 示範 **how to calculate cotangent** 直接於儲存格中計算。  
4. 以 `CalculateFormula` 強制計算。  
5. **Save workbook to file** 並驗證結果。

以上全部為獨立完成，可在任何近期的 .NET 執行環境上執行，且僅需一個 NuGet 套件。

## 接下來可以做什麼？

- **動態資料來源：** 從資料庫取得資料並輸入至 `EXPAND`。  
- **多工作表：** 迭代工作表集合以產生完整的報告簿。  
- **進階公式：** 探索 `LET`、`LAMBDA` 或基於陣列的條件邏輯，以打造更智慧的試算表。  

盡情試驗吧——替換 `SEQUENCE` 參數、嘗試不同角度的 `COT`，或結合圖表產生。只要能以程式方式 **create new Excel workbook**，就沒有任何限制。

---

*祝編程愉快！如果遇到任何問題，歡迎在下方留言或在 Twitter 上私訊我 @YourHandle。我很樂意協助。*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}