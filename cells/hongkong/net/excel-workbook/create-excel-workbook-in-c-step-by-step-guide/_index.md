---
category: general
date: 2026-02-09
description: 在 C# 中建立 Excel 工作簿，學習如何寫入儲存格值、設定精度，並儲存檔案。非常適合 C# 產生 Excel 檔案的任務。
draft: false
keywords:
- create excel workbook
- write value to cell
- how to set precision
- c# generate excel file
- c# save excel workbook
language: zh-hant
og_description: 快速在 C# 中建立 Excel 工作簿。學習如何寫入儲存格值、設定精度，並以清晰的程式碼範例儲存工作簿。
og_title: 在 C# 中建立 Excel 工作簿 – 完整程式設計指南
tags:
- C#
- Excel automation
- Aspose.Cells
title: 在 C# 中建立 Excel 工作簿 – 步驟指南
url: /zh-hant/net/excel-workbook/create-excel-workbook-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中建立 Excel 工作簿 – 步驟教學

是否曾需要在 C# 中 **建立 Excel 工作簿** 以供報表工具使用，但不知從何下手？你並不孤單——許多開發者在首次嘗試自動化試算表時都會卡關。好消息是，只要幾行程式碼就能產生工作簿、控制數字顯示方式、寫入儲存格值，並將檔案寫入磁碟。

在本教學中，我們將完整說明工作流程，從初始化工作簿到將其保存為 `.xlsx` 檔案。途中會說明「如何設定數值精度」、示範 **如何寫入儲存格** A1，並探討 **c# generate excel file** 專案的最佳實踐。完成後，你將擁有一段可直接放入任何 .NET 解決方案的可重用程式碼。

## 前置條件

- .NET 6.0 或更新版本（此程式碼亦相容 .NET Framework 4.7+）  
- 參考 **Aspose.Cells** 函式庫（或任何相容的 API；本教學以 Aspose 為例，因為它與你提供的範例相符）  
- 具備基本的 C# 語法與 Visual Studio（或你慣用的 IDE）知識  

不需要額外設定，只要安裝 NuGet 套件即可：

```bash
dotnet add package Aspose.Cells
```

> **小技巧：** 若你偏好開源方案，EPPlus 也提供類似功能，但屬性名稱稍有不同（例如 `Workbook.Properties` 取代 `Settings`）。

## 步驟 1：在 C# 中建立 Excel 工作簿

首先需要一個工作簿物件。它是 Excel 檔案在記憶體中的表示。使用 Aspose.Cells 時，只要實例化 `Workbook` 類別即可：

```csharp
using Aspose.Cells;   // Core library for Excel manipulation
using System;        // For basic .NET types

// Step 1: Create a brand‑new workbook (empty workbook = 1 worksheet by default)
Workbook workbook = new Workbook();
```

> **為什麼這很重要：** 建立工作簿會配置內部結構（工作表、樣式、計算引擎）。沒有這個物件，就無法設定精度或寫入資料。

## 步驟 2：設定精度（有效位數）

Excel 預設會顯示許多小數位，報表中常會顯得雜亂。`NumberSignificantDigits` 設定會讓引擎將數字四捨五入至指定的 **有效位數**，而非固定的小數位數。以下示範保留五位有效位數：

```csharp
// Step 2: Configure the workbook to keep 5 significant digits when displaying numbers
workbook.Settings.NumberSignificantDigits = 5;
```

### 「有效位數」的真正意義

- **有效位數** 從第一個非零數字開始計算，與小數點位置無關。  
- 設為 `5` 時，`12345.6789` 會顯示為 `12346`（四捨五入至最近的五位數表示）。  

若需其他精度，只要更改整數值即可。對於財務資料，你可能會使用 `workbook.Settings.NumberDecimalPlaces = 2;` 以保留兩位小數。

## 步驟 3：寫入值至儲存格 A1

工作簿準備好後，就可以把值寫入儲存格。`PutValue` 方法會自動偵測資料類型（字串、double、DateTime 等）並正確儲存。

```csharp
// Step 3: Write a sample numeric value into cell A1 of the first worksheet
Worksheet sheet = workbook.Worksheets[0];   // Grab the default sheet (index 0)
Cell targetCell = sheet.Cells["A1"];        // Address cell by its A1 notation
targetCell.PutValue(12345.6789);            // Insert the number
```

> **為什麼使用 `PutValue` 而不是直接指定 `Value`？**  
> `PutValue` 會執行型別轉換，並套用工作簿的格式設定（包括先前設定的精度）。直接指定會略過這些便利功能。

## 步驟 4：將 Excel 工作簿保存至磁碟

填好工作表後，需要將檔案寫入磁碟。`Save` 方法支援多種格式（`.xlsx`、`.xls`、`.csv` 等）。以下示範將 `.xlsx` 檔案寫入自訂資料夾：

```csharp
// Step 4: Save the workbook to a file
string outputPath = @"C:\Temp\sigdigits.xlsx";   // Adjust the path as needed
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

當你在 Excel 中開啟產生的檔案時，儲存格 A1 會顯示 `12346`（因為第 2 步的有效位數設定），呈現四捨五入後的結果。

---

![create excel workbook example](excel-workbook.png){alt="建立 Excel 工作簿範例，顯示 A1 儲存格的四捨五入值"}

*上圖展示了執行程式碼後的最終工作簿畫面。*

## 完整範例（結合所有步驟）

以下是一個可直接貼到新 `.csproj` 中的完整主控台程式。它包含所有必要的 using、註解與錯誤處理，適合用於正式環境。

```csharp
// -----------------------------------------------------------
// Complete example: create excel workbook, set precision,
// write value to cell, and save the file.
// -----------------------------------------------------------

using System;
using Aspose.Cells;

namespace ExcelAutomationDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                // 1️⃣ Create a new workbook (contains one default worksheet)
                Workbook workbook = new Workbook();

                // 2️⃣ Set the number of significant digits to 5
                workbook.Settings.NumberSignificantDigits = 5;

                // 3️⃣ Write a numeric value into cell A1 of the first worksheet
                Worksheet sheet = workbook.Worksheets[0];
                Cell a1 = sheet.Cells["A1"];
                a1.PutValue(12345.6789);   // The value will be rounded per the setting

                // 4️⃣ Define the output path (ensure the directory exists)
                string folder = @"C:\Temp";
                string fileName = "sigdigits.xlsx";
                string fullPath = System.IO.Path.Combine(folder, fileName);

                // 5️⃣ Save the workbook as an .xlsx file
                workbook.Save(fullPath, SaveFormat.Xlsx);

                Console.WriteLine($"✅ Excel workbook created successfully at: {fullPath}");
                Console.WriteLine("Open the file in Excel to see the rounded value in A1.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ An error occurred: {ex.Message}");
            }
        }
    }
}
```

### 預期輸出

執行程式後會印出類似以下內容：

```
✅ Excel workbook created successfully at: C:\Temp\sigdigits.xlsx
Open the file in Excel to see the rounded value in A1.
```

開啟 `sigdigits.xlsx` 後，A1 儲存格會顯示 **12346**，證實精度設定已生效。

## 常見問題與專家建議（c# generate excel file）

| 問題 | 為什麼會發生 | 解決方式 / 最佳實踐 |
|------|--------------|-------------------|
| **找不到目錄** | `Save` 會在資料夾不存在時拋出例外。 | 在保存前使用 `Directory.CreateDirectory(folder);` 建立資料夾。 |
| **精度設定被忽略** | 某些樣式會覆寫工作簿設定。 | 先清除儲存格的既有樣式：`a1.SetStyle(new Style(workbook));` |
| **大量資料導致記憶體壓力** | Aspose 會將整個工作簿載入 RAM。 | 對於超大型檔案，可考慮使用 `WorkbookDesigner` 串流或 EPPlus 的 `ExcelPackage` 搭配 `LoadFromDataTable`、`ExcelRangeBase.LoadFromCollection`。 |
| **缺少 Aspose.Cells 授權** | 評估版會加上浮水印。 | 載入授權檔案 (`License license = new License(); license.SetLicense("Aspose.Total.lic");`) |
| **跨平台路徑分隔符** | 硬寫 `\` 會在 Linux/macOS 上失效。 | 使用 `Path.Combine` 與 `Path.DirectorySeparatorChar`。 |

### 延伸範例

- **寫入多筆資料**：遍歷資料表，對每個儲存格呼叫 `PutValue`。  
- **套用自訂數字格式**：`a1.Number = 2; a1.Style.Number = 4;` 可強制顯示兩位小數，無視有效位數設定。  
- **加入公式**：`a1.PutValue("=SUM(B1:B10)");`，之後呼叫 `workbook.CalculateFormula();`。  

以上皆屬於 **c# save excel workbook** 的常見任務，實務上經常會用到。

## 結論

現在你已掌握如何在 C# 中 **建立 Excel 工作簿**、使用 `NumberSignificantDigits` 控制顯示精度、 **寫入儲存格** A1，並最終 **c# save excel workbook** 到磁碟。上方提供的完整可執行範例消除了所有猜測，為任何自動化情境奠定堅實基礎——無論是每日報表產生、資料匯出功能，或是大量批次處理。

準備好進一步挑戰了嗎？試著將 Aspose.Cells 換成 EPPlus，觀察 API 差異；或是嘗試加入樣式（字型、顏色）讓產生的試算表更具專業感。**c# generate excel file** 的世界相當廣闊，而你已踏出最重要的第一步。

祝開發順利，願你的試算表永遠精確無誤！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}