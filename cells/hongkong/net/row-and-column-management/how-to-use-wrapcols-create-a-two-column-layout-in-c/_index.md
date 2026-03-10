---
category: general
date: 2026-02-15
description: 如何在 C# 工作表中使用 WRAPCOLS 建立雙欄佈局、加入公式並產生序列陣列 – 步驟教學
draft: false
keywords:
- how to use wrapcols
- create two column layout
- how to add formula
- how to create columns
- generate sequence array
language: zh-hant
og_description: 如何使用 WRAPCOLS 建立雙欄佈局、加入公式及於 C# 工作表中產生序列陣列 – 完整指南
og_title: 如何使用 WRAPCOLS：C# 中的雙欄佈局
tags:
- CSharp
- ExcelAutomation
- WorksheetFormula
title: 如何使用 WRAPCOLS：在 C# 中建立雙欄佈局
url: /zh-hant/net/row-and-column-management/how-to-use-wrapcols-create-a-two-column-layout-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 WRAPCOLS：在 C# 中建立雙欄佈局

有沒有想過 **how to use WRAPCOLS**，在需要快速在 Excel 風格工作表中呈現雙欄視圖時該怎麼做？你並不孤單。許多開發者在嘗試把產生的清單切分成整齊欄位時，會卡在必須為每個儲存格寫迴圈的問題。好消息是？只要使用 `WRAPCOLS` 函式，你只需要在 `A1` 放入一個公式，讓 Excel（或相容的引擎）自行完成繁重的工作。

在本教學中，我們將一步步說明 **how to add formula** 以建立 **create two column layout**，示範如何動態 **how to create columns**，甚至即時 **generate sequence array**。完成後，你將得到一段完整可執行的 C# 程式碼，直接貼到專案、執行，即可即時看到整齊的雙欄區塊。

## 你將學到

- `WRAPCOLS` 的用途，以及為何它比手動迴圈更好。  
- 如何使用 C# **add a formula** 到工作表儲存格。  
- 如何使用 `SEQUENCE` 產生序列陣列，並將其餵入 `WRAPCOLS`。  
- 讓工作表立即重新計算的技巧。  
- 邊緣案例處理（例如：空工作表、客製化欄數）。

不需要額外的函式庫，只要使用標準的 Excel 處理套件 – 我們會使用 **ClosedXML**，因為它的 API 簡潔易用，概念同樣適用於 EPPlus、SpreadsheetGear，甚至是透過 API 操作 Google Sheets。

---

## 前置條件

- .NET 6.0 或更新版本（程式碼可在 .NET Core 與 .NET Framework 上編譯）。  
- 參考 **ClosedXML**（`dotnet add package ClosedXML`）。  
- 基本的 C# 知識 – 需要熟悉 `using` 陳述式與物件初始化。

如果你已經開啟了一個活頁簿，可以跳過建立檔案的步驟，直接進入公式部分。

---

## 步驟 1：設定工作表（How to Create Columns）

首先需要取得一個 `Worksheet` 物件。於 ClosedXML 中，你會從 `XLWorkbook` 取得它。以下程式碼會建立新活頁簿，新增名為 *Demo* 的工作表，並以 `worksheet` 變數保存參考，方便後續使用。

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // Create a fresh workbook and add a worksheet named "Demo"
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");

            // Rename for clarity – this is the worksheet we’ll manipulate
            var worksheet = ws;   // <-- same object, just a clearer name

            // --------------------------------------------------------------
            // Next step: write the WRAPCOLS formula
            // --------------------------------------------------------------
```

> **為何重新命名？**  
> 保持變數名稱簡短（`worksheet`）能讓後續程式碼更易閱讀，特別是當你串接多個操作時。這也呼應大多數文件中的命名慣例，減少認知負擔。

---

## 步驟 2：寫入公式（How to Add Formula + Generate Sequence Array）

接下來就是關鍵的一行。我們會在 **A1** 儲存格放入公式，完成兩件事：

1. **Generate a sequence array**：產生六個數字的序列 (`SEQUENCE(6)` → 1,2,3,4,5,6)。  
2. **Wrap those numbers into two columns**：使用 `WRAPCOLS(..., 2)` 把這些數字「包」成兩欄。

```csharp
            // Write the WRAPCOLS formula into A1
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // --------------------------------------------------------------
            // Finally, force the engine to evaluate the formula
            // --------------------------------------------------------------
```

> **發生了什麼事？**  
> `SEQUENCE(6)` 會建立垂直陣列 `{1;2;3;4;5;6}`。`WRAPCOLS` 再把該陣列依指定的欄數「換行」——此例為 **2**。結果是一個 3 列 × 2 欄的區塊，如下所示：

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

如果把第二個參數改成 **3**，則會得到三欄佈局。這就是 **how to create columns** 的核心，無需手動迴圈即可即時產生欄位。

---

## 步驟 3：重新計算工作表（Ensuring the Formula Evaluates）

ClosedXML 不會在寫入公式時自動求值。必須在活頁簿（或特定工作表）上呼叫 `Calculate()`，才能強制計算。

```csharp
            // Recalculate so the formula is evaluated immediately
            worksheet.Calculate();

            // Optional: save the workbook to inspect the result
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

> **小技巧：** 若處理大型活頁簿，僅對實際變更的工作表呼叫 `Calculate()`，可節省記憶體並加速處理。

開啟 `WrapColsDemo.xlsx` 後，你會看到 **A1:B3** 內已自動填入雙欄佈局。無需額外的迴圈程式碼 – `WRAPCOLS` 已完成所有工作。

---

## 步驟 4：驗證輸出（What to Expect）

執行程式後，打開產生的檔案，應該會看到：

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

若數字全部垂直排列（全在欄 A），請再次確認已在設定公式後 **呼叫** `worksheet.Calculate()`。某些引擎也需要 `workbook.Calculate()`；上述程式碼適用於 ClosedXML 內建的求值器。

---

## 常見變化與邊緣案例

### 更改欄數

若要 **create two column layout** 且行數不同，只要調整 `SEQUENCE` 的大小或 `WRAPCOLS` 的第二個參數：

```csharp
worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(12), 3)";
```

上述程式會產生 4 列 × 3 欄的區塊（12 個數字分散於三欄）。

### 使用動態欄數

若欄數來源於變數，可使用字串插值：

```csharp
int colCount = 4;
worksheet.Cell("A1").FormulaA1 = $"=WRAPCOLS(SEQUENCE(8), {colCount})";
```

現在你已掌握 **how to add formula**，能在執行時自動調整欄數。

### 空工作表

即使工作表是空的，`Calculate()` 仍會正常運作 – 公式會從 A1 開始填入儲存格。但若之後刪除與輸出範圍交叉的列或欄，可能會出現 `#REF!` 錯誤。為避免此情形，先清除目標範圍：

```csharp
worksheet.Range("A1:Z100").Clear(); // wipes any leftovers
```

### 相容性

`WRAPCOLS` 與 `SEQUENCE` 屬於 Excel 的 **Dynamic Array** 函式，於 Office 365 之後推出。若目標是較舊的 Excel 版本，這些函式將不存在，需要自行寫迴圈。ClosedXML 的求值器模仿最新的 Excel 行為，適用於現代環境。

---

## 完整範例（Copy‑Paste Ready）

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook & worksheet
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");
            var worksheet = ws;   // clearer name

            // 2️⃣ Write WRAPCOLS formula that generates a sequence array
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // 3️⃣ Force calculation so the formula resolves immediately
            worksheet.Calculate();

            // 4️⃣ Save the file (optional, but handy for verification)
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

**預期結果：** 開啟 *WrapColsDemo.xlsx* 後，會看到如前所述的整齊雙欄佈局，數字 1‑6 已依序排列。

---

## 結論

我們已說明 **how to use WRAPCOLS** 以 **create a two column layout**，示範了如何以程式方式 **add a formula**，並看到 `SEQUENCE` 如何 **generate sequence array** 而不必寫迴圈。透過 C# 呼叫 Excel 的動態陣列函式，你的程式碼可以保持簡潔、可讀且易於維護。

接下來，你可以探索：

- 使用 `ROWS` 或 `COUNTA` **Creating dynamic row counts**。  
- 透過 ClosedXML 的樣式 API **Styling the output**（框線、數字格式）。  
- 在完成佈局後 **Exporting to CSV**，供後續處理使用。

試著調整欄數，快速原型出複雜的試算表吧。祝程式開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}