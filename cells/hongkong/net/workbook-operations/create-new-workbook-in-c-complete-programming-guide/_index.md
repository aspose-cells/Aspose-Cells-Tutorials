---
category: general
date: 2026-03-25
description: 在 C# 中建立新工作簿，學習如何使用 EXPAND、計算餘切，並以逐步程式碼將工作簿儲存至檔案。
draft: false
keywords:
- create new workbook
- save workbook to file
- how to use expand
- how to calculate cotangent
- how to save excel
language: zh-hant
og_description: 在 C# 中建立新工作簿，即時了解如何使用 EXPAND、計算餘切，並將工作簿儲存至檔案。
og_title: 在 C# 中建立新工作簿 – 完整程式設計指南
tags:
- Aspose.Cells
- C#
- Excel Automation
title: 在 C# 中建立新工作簿 – 完整程式設計指南
url: /zh-hant/net/workbook-operations/create-new-workbook-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中建立新工作簿 – 完整程式指南

是否曾經需要在 C# 中 **建立新工作簿**，卻不知從何著手？你並非唯一面臨此問題的人。無論是自動化報表流程，還是僅僅在程式碼中玩弄 Excel 公式，能夠快速產生工作簿、插入像 `EXPAND` 或 `COT` 這樣的公式，然後 **將工作簿儲存至檔案**，都是任何 .NET 開發者的核心技能。

在本教學中，我們將示範一個真實案例：建立全新的工作簿、使用 `EXPAND` 函數將靜態陣列轉為動態欄位、以 `COT` 函數計算餘切，最後 **將工作簿儲存至檔案** 為 `.xlsx`。完成後，你將擁有可直接執行的程式碼片段，了解每個呼叫的原因，並看到一些實用的變體以因應特殊情況。

> **專業提示：** 以下所有程式碼皆相容於截至 2026 年 3 月的最新 Aspose.Cells for .NET 版本。若使用較舊版本，API 大致相同，但請再次確認命名空間的引用。

## 您需要的環境

- .NET 6.0 或更新版本（範例以 .NET 6 為目標，.NET 5 亦可執行）  
- 透過 NuGet 安裝 Aspose.Cells for .NET (`Install-Package Aspose.Cells`)  
- 基本的 C# 知識（你已經具備）  

就這樣——不需要額外的 DLL、COM interop，亦不需要在機器上安裝 Excel。準備好了嗎？讓我們開始吧。

![顯示如何在 C# 中建立新工作簿的螢幕截圖](assets/create-new-workbook.png){alt="顯示如何在 C# 中建立新工作簿的螢幕截圖"}

## 步驟 1：建立新工作簿

首先必須實例化 `Workbook` 類別。可以把它想像成在記憶體中開啟一個空白的 Excel 檔案。此物件會保存工作表、樣式以及之後可能需要的所有內容。

```csharp
using Aspose.Cells;

class ExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();               // <-- creates an empty .xlsx structure
        Worksheet ws = workbook.Worksheets[0];            // default sheet is named "Sheet1"
```

為什麼要立刻取得第一張工作表？大多數快速入門範例只使用單一工作表，而 `Worksheets[0]` 存取子是取得參考的最快方式，無需迴圈。若之後需要多張工作表，可使用 `workbook.Worksheets.Add()` 來新增。

## 步驟 2：如何使用 EXPAND 產生動態範圍

`EXPAND` 是較新的 Excel 函數，可將陣列填充至指定大小。在本範例中，我們會把字面陣列 `{1,2,3}` 展開成 **5 列的欄位**，起始於儲存格 `A1`。字串內的語法與在 Excel 中直接輸入完全相同，之後若需要，可直接複製貼上到儲存格。

```csharp
        // Step 2: Apply EXPAND to turn {1,2,3} into a 5‑row vertical range
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"; // rows=5, cols=1
```

### 背後發生了什麼？

- `{1,2,3}` 為水平陣列常數。  
- 第二個參數 (`5`) 告訴 Excel 將陣列展開至 **5 列**。  
- 第三個參數 (`1`) 強制輸出為 **單一欄位**。  

如果省略第三個參數，Excel 會嘗試保留原始形狀，可能會得到 5×3 的區塊，而非單欄。這是剛開始使用 `EXPAND` 時常見的陷阱。

#### 可能需要的變體

| 欲求形狀 | 公式範例 |
|----------|----------|
| 3 列、2 欄區塊 | `=EXPAND({1,2,3},3,2)` |
| 僅向下填充（同一欄） | `=EXPAND({10,20},10,1)` |
| 展開至較多欄數 | `=EXPAND({5},5,4)` |

隨意替換常數或尺寸，以符合你的資料產生邏輯。

## 步驟 3：如何使用 COT 函數計算餘切

`COT` 函數會回傳以弧度表示的角度之餘切值。在本例中，我們計算 45°（π/4 弧度）的餘切，結果 `1` 會放入儲存格 `B1`。

```csharp
        // Step 3: Use COT to calculate cotangent of 45 degrees (π/4 radians)
        ws.Cells["B1"].Formula = "=COT(PI()/4)"; // PI() returns π, divided by 4 = 45°
```

### 為何使用 COT 而非手動計算？

Excel 已內建三角函數的轉換機制，使用 `COT` 可避免手動計算 `1 / TAN(angle)` 時可能產生的浮點數捨入誤差。此外，公式對日後檢閱試算表的任何人都更具可讀性。

#### 邊緣情況：角度超過 0‑360°

如果輸入的角度大於 `2*PI()`（或為負值），Excel 會自動將其環繞，但結果可能出乎意料。為保險起見，建議先將角度正規化：

```csharp
        // Normalize angle to 0‑2π range before applying COT
        ws.Cells["C1"].Formula = "=COT(MOD(PI()*3, 2*PI()))";
```

上述程式碼示範了如何結合 `MOD` 與 `COT` 以實作更健全的計算。

## 步驟 4：如何將工作簿儲存至檔案（Excel）

公式寫好後，最後一步就是 **將工作簿儲存至檔案**。可以自行決定儲存路徑，只要確保目錄已存在且具有寫入權限即可。

```csharp
        // Step 4 (optional): Save the workbook so you can inspect the results
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "output.xlsx");

        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### 實際儲存了什麼？

開啟 `output.xlsx` 後，你會看到：

| A | B |
|---|---|
| 1 | 1 |
| 2 |   |
| 3 |   |
|   |   |
|   |   |

- **A 欄** 包含展開後的陣列 `{1,2,3}`，其後兩格為空白（因為我們要求 5 列）。  
- **B1** 顯示 `1`，即 45° 的餘切值。  

若重新整理工作簿（按 `F9` 或啟用自動計算），Excel 會評估公式並顯示結果。若不想開啟 Excel，也可使用 Aspose.Cells 的 `CalculateFormula` 方法直接取得數值：

```csharp
        workbook.CalculateFormula();
        double cotResult = ws.Cells["B1"].DoubleValue; // should be 1.0
```

## 常見問題與注意事項

| 問題 | 答案 |
|------|------|
| **我需要手動啟用計算嗎？** | 不需要。預設情況下 Aspose.Cells 會原樣儲存公式；Excel 在開啟時會自行計算。如需預先計算，可使用 `workbook.CalculateFormula()`。 |
| **我可以一次寫入多個儲存格的公式嗎？** | 當然可以。使用 `ws.Cells["D1:D5"].Formula = "=RAND()"` 即可將隨機數填入整個範圍。 |
| **如果目標資料夾不存在該怎麼辦？** | 先建立它：`Directory.CreateDirectory(Path.GetDirectoryName(outputPath));` |
| **舊版 Excel 是否支援 `EXPAND`？** | `EXPAND` 是在 Excel 365/2019 中加入的。若需相容舊版檔案，請考慮改用 `INDEX`/`SEQUENCE` 組合。 |
| **我要如何隱藏公式檢視？** | 設定 `ws.Cells["A1"].FormulaHidden = true;`，並保護工作表，即可防止使用者看到底層公式。 |

## 總結

你現在已掌握 **如何在 C# 中建立新工作簿**、利用 `EXPAND` 產生動態陣列、以 `COT` 計算餘切，並 **將工作簿儲存至檔案** 成為整潔的 Excel 文件。完整且可執行的範例已在上述程式碼片段中——將其複製到 Console 應用程式、按下 `F5`，再開啟產生的 `output.xlsx`，即可看到成效。

### 接下來呢？

- **探索其他動態陣列函數**，如 `SEQUENCE`、`FILTER`、`SORT`。  
- **自動化圖表建立**，使用 Aspose.Cells 豐富的圖表 API。  
- **整合資料來源**（SQL、CSV），將資料程式化寫入公式。  
- **學習將 Excel 另存為 PDF** 或其他格式——非常適合報表自動化流程。

盡情實驗：更改陣列值、調整角度，或將結果寫入不同工作表。結合 C# 與 Excel 現代公式引擎，無所不能。

祝程式開發順利，願你的試算表永遠正確計算！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}