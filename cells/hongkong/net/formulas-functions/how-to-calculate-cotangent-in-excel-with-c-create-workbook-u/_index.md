---
category: general
date: 2026-05-04
description: 在 C# 中建立 Excel 活頁簿時，如何計算餘切。學習如何使用 EXPAND 函數、儲存活頁簿以及自動化計算。
draft: false
keywords:
- how to calculate cotangent
- create excel workbook
- how to use expand
- how to save workbook
- use expand function
language: zh-hant
og_description: 如何在 Excel 中使用 C# 計算餘切。此教學示範如何建立 Excel 工作簿、使用 EXPAND，並儲存檔案。
og_title: 如何在 Excel 中計算餘切 – 完整 C# 工作簿指南
tags:
- C#
- Aspose.Cells
- Excel Automation
title: 如何在 Excel 中使用 C# 計算餘切 – 建立工作簿、使用 EXPAND 並儲存
url: /zh-hant/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Excel 中使用 C# 計算餘切 – 完整指南

有沒有想過 **如何計算餘切** 直接在 C# 產生的 Excel 檔案中？也許你正在建立財務模型、科學報告，或只是想自動化一項乏味的試算表工作。好消息是？只需要幾行程式碼就能完成——不需要手動公式，也不需要複製貼上。

在本教學中，我們將逐步說明如何建立 Excel 活頁簿、使用 **EXPAND** 函數展開陣列、插入 **COT** 公式計算 45° 的餘切，最後儲存檔案以便在 Excel 中開啟並查看結果。過程中，我們也會涵蓋 **how to use expand**、**how to save workbook** 以及一些常被忽略的實用技巧。

> **快速回答：** 使用 Aspose.Cells（或 Microsoft Interop）建立活頁簿，設定 `ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"`，設定 `ws.Cells["B1"].Formula = "=COT(PI()/4)"`，最後呼叫 `workbook.Save("output.xlsx")`。

## 您需要的條件

- **.NET 6+**（或任何較新的 .NET 執行環境）。  
- **Aspose.Cells for .NET**（免費試用版或授權版）。  
- 具備基本的 C# 語法概念。  
- Visual Studio、Rider，或任何你喜歡的編輯器。

不需要額外的 Excel 外掛；所有操作皆在伺服器端執行，產生的檔案可在任何較新版的 Excel 中使用。

## 步驟 1：從 C# 建立 Excel 活頁簿  

建立活頁簿是基礎。可以把它想像成在開始寫作前打開一本全新的筆記本。

```csharp
using Aspose.Cells;

// Step 1: Initialize a new workbook object
Workbook workbook = new Workbook();               // Empty workbook
Worksheet ws = workbook.Worksheets[0];            // Grab the first sheet
```

**為什麼這很重要：**  

`Workbook` 代表整個 `.xlsx` 套件。預設情況下它只包含一個工作表，我們可透過 `Worksheets[0]` 取得。若之後需要更多工作表，可使用 `workbook.Worksheets.Add()` 新增。

> **專業提示：** 如果你的目標是 .NET Core，請確保 Aspose.Cells 的 NuGet 套件與你的執行環境相符，以免缺少本機相依性。

## 步驟 2：使用 EXPAND 函數填滿欄位  

**EXPAND** 函數是 Excel 將靜態陣列轉換為動態範圍的方式。當你想產生一整欄數值而不想為每個儲存格硬編碼時，它非常適用。

```csharp
// Step 2: Write an EXPAND formula in cell A1
ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"; // Expands to a 5‑row column
```

### 工作原理  

- `{1,2,3}` 為來源陣列（三個數字）。  
- `5` 告訴 Excel 產生 **5 列**。  
- `1` 告訴 Excel 產生 **1 欄**。  

當你開啟已儲存的檔案時，A1 到 A5 儲存格會分別顯示 `1, 2, 3, 0, 0`（多餘的列會以 0 填充）。  

**邊緣情況：** 若 `rows` 參數小於來源陣列長度，Excel 會截斷陣列。因此 `=EXPAND({1,2,3},2,1)` 只會顯示 `1` 與 `2`。

## 步驟 3：插入 COT 公式計算餘切  

現在來到重點：在 Excel 中 **如何計算餘切**。`COT` 函數需要以弧度為單位的角度，因此我們傳入 `PI()/4`（即 45°）。

```csharp
// Step 3: Write a COT formula in cell B1
ws.Cells["B1"].Formula = "=COT(PI()/4)"; // Returns 1
```

### 為什麼使用 COT 而非 TAN？  

餘切是正切的倒數（`cot = 1 / tan`）。雖然可以寫成 `=1/TAN(PI()/4)`，但使用 `COT` 更簡潔，且可避免角度為 0° 或 180° 時除以零的錯誤。

**預期輸出：** 開啟 `output.xlsx` 後，B1 會顯示 `1`，因為 45°（π/4 弧度）的餘切等於 1。

**如果需要使用度數該怎麼辦？**  
Excel 的三角函數使用弧度。可使用 `RADIANS(deg)` 轉換度數。例如：`=COT(RADIANS(60))`。

## 步驟 4：儲存活頁簿以檢視結果  

儲存是最後一步。你可以寫入任何你有寫入權限的資料夾。

```csharp
// Step 4: Persist the workbook to disk
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "output.xlsx");

// Save the workbook (the default format is .xlsx)
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### 如何以不同格式儲存  

- **XLS** – `workbook.Save("output.xls", SaveFormat.Excel97To2003);`  
- **CSV** – `workbook.Save("output.csv", SaveFormat.CSV);`  

如果需要將檔案以串流方式傳送（例如用於 Web API），可改用 `workbook.Save(stream, SaveFormat.Xlsx)`。

## 完整範例  

將上述步驟整合起來，以下是一個可直接貼到 Console 應用程式的完整程式碼。

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Expand an array {1,2,3} into a 5‑row column starting at A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // 3️⃣ Calculate cotangent of 45° (π/4) in B1
        ws.Cells["B1"].Formula = "=COT(PI()/4)";

        // 4️⃣ Define where to save the file (Desktop for easy access)
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "output.xlsx");

        // 5️⃣ Save the workbook
        workbook.Save(outputPath);
        Console.WriteLine($"✅ Workbook saved at: {outputPath}");
    }
}
```

**結果驗證：**  
- 開啟 `output.xlsx`。  
- A 欄應顯示 `1, 2, 3, 0, 0`。  
- B1 儲存格應顯示 `1`。  

如果看到上述數值，代表你已成功學會以程式方式 **如何計算餘切**，以及 **建立 Excel 活頁簿**、**使用 expand 函數**、**儲存活頁簿**——一次搞定。

## 常見問題與注意事項  

### `COT` 在較舊的 Excel 版本中可用嗎？

是的，`COT` 自 Excel 2007 起即已支援。若目標是 Excel 2003（`.xls`），則需改用 `1/TAN(...)`，因為 `COT` 在該版本不存在。

### 若公式未自動重新計算該怎麼辦？

Aspose.Cells 會延遲評估公式。若需要將計算結果寫入檔案，請在儲存前呼叫 `workbook.CalculateFormula()`。

```csharp
workbook.CalculateFormula();
workbook.Save(outputPath);
```

### 能否直接寫入結果而不使用公式？

當然可以，你可以在 C# 中計算值（`Math.Cos(Math.PI / 4) / Math.Sin(Math.PI / 4)`），再將結果指派給 `ws.Cells["B1"].Value = result;`。本教學著重於 Excel 公式，因為它們保持動態——之後若更改角度，結果會自動更新。

## 真實專案的進階技巧  

- **批次操作：** 若需填入數千列，寫入時可關閉計算 (`workbook.Settings.CalculateFormulaOnOpen = false`)，完成後再重新開啟。  
- **命名範圍：** 使用 `ws.Cells.CreateRange("MyArray", "A1:A5")`，在公式中引用名稱，可讓試算表更清晰。  
- **錯誤處理：** 將 `workbook.Save` 包在 try/catch 中，以捕捉權限問題（`UnauthorizedAccessException`）。

## 結論  

我們已說明如何在 C# 產生的 Excel 工作表中 **計算餘切**，示範 **如何使用 expand** 來填充欄位，並展示 **如何儲存活頁簿** 以便立即檢視。上方完整且可執行的範例為你提供了堅實的基礎，能自動化任何結合靜態資料與三角函數計算的試算表。

接下來的步驟？可以將 `COT` 公式中的角度改為參照儲存格（`=COT(PI()*A1/180)`），讓使用者自行輸入度數。或是探索其他數學函數，如 `SIN`、`COS`、`ATAN2`——它們在產生的活頁簿中皆以相同方式運作。

祝程式開發順利，願你的試算表永遠沒有錯誤！🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}