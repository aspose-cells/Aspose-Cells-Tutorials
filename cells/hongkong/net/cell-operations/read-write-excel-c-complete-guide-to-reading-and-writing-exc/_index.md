---
category: general
date: 2026-03-01
description: 《Read write Excel C# 教程》示範如何使用 C# 及 Aspose.Cells 於簡單幾步內讀取 Excel 儲存格值並寫入日期時間至
  Excel。
draft: false
keywords:
- read write excel c#
- read excel cell value
- write datetime to excel
- c# excel interop
- aspnet excel automation
language: zh-hant
og_description: 讀寫 Excel C# 教學說明如何讀取 Excel 儲存格的值以及寫入日期時間至 Excel，並提供清晰的程式碼範例與最佳實踐。
og_title: Excel C# 讀寫 – 逐步指南
tags:
- C#
- Excel
- Aspose.Cells
title: 讀寫 Excel C# – 完整指南：讀取與寫入 Excel 儲存格
url: /zh-hant/net/cell-operations/read-write-excel-c-complete-guide-to-reading-and-writing-exc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 讀寫 Excel C# – 完整指南：讀取與寫入 Excel 儲存格

曾嘗試過 **read write Excel C#**，卻遇到難以理解的例外或日期不匹配嗎？你並不孤單。許多開發者在需要從工作表中取出日本元號日期，然後再將正確的 `DateTime` 寫回同一儲存格時，常會卡關。  

在本指南中，我們將逐步說明如何使用 C# 以及功能強大的 Aspose.Cells 函式庫，**read excel cell value** 與 **write datetime to excel**。完成後，你將擁有一個可自行執行的範例，能直接放入任何 .NET 專案中使用。

## 你將學到

- 如何在 .NET 6+ 專案中安裝與引用 Aspose.Cells。  
- 取得包含日本元號字串（例如 `"R3/5/12"`）之儲存格的完整程式碼。  
- 使用 `"ja-JP"` 文化將該字串解析為 `DateTime`。  
- 將產生的 `DateTime` 寫回同一工作表儲存格的步驟。  
- 處理空儲存格或非預期元號格式等邊緣情況的技巧。  

不需要任何 Excel interop 的先前經驗——只要具備 C# 與 .NET 的基本概念即可。讓我們開始吧。

![讀寫 Excel C# 操作的螢幕截圖，顯示 B2 儲存格在轉換前後的樣子](read-write-excel-csharp.png "讀寫 excel c# 範例")

## 第一步：設定專案 – Read Write Excel C# 基礎

在深入程式碼之前，我們需要先打好基礎。

1. **建立新的 console 應用程式**（或任何 .NET 專案），目標為 .NET 6 或更新版本：

   ```bash
   dotnet new console -n ExcelEraDemo
   cd ExcelEraDemo
   ```

2. **加入 Aspose.Cells NuGet 套件**。這是一個完整受管理的函式庫，無需 COM interop 即可運作：

   ```bash
   dotnet add package Aspose.Cells
   ```

3. **將 Excel 檔案** (`EraDates.xlsx`) 複製到專案根目錄。此活頁簿應包含名為 `"Sheet1"` 的工作表，且儲存格 **B2** 內的值為類似 `"R3/5/12"`（令和 3 年 5 月 12 日）。

以上即為你所需的全部基礎建設。接下來的教學將聚焦於實際的 **read excel cell value** 與 **write datetime to excel** 邏輯。

## 第二步：使用 C# 讀取 Excel 儲存格值

專案就緒後，讓我們從工作表中取得字串。以下程式碼片段示範了完整的呼叫鏈：

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Load the workbook (adjust the path as needed)
        Workbook wb = new Workbook("EraDates.xlsx");
        Worksheet ws = wb.Worksheets["Sheet1"];   // assumes the sheet is named Sheet1

        // Step 2: Get the cell that holds the Japanese era date string
        // B2 contains something like "R3/5/12"
        Cell dateCell = ws.Cells["B2"];  

        // Step 3: Read the string representation from the cell
        string eraDateString = dateCell.StringValue;  

        Console.WriteLine($"Original cell value: {eraDateString}");
        // -------------------------------------------------
        // From here we’ll convert the era string to a DateTime.
        // -------------------------------------------------
    }
}
```

**為什麼這樣可行：** `Cell.StringValue` 總是回傳顯示的文字，無論底層的數值格式為何。這確保我們取得使用者看到的精確 `"R3/5/12"` 字串。

### 常見陷阱

- **空儲存格** – `StringValue` 會回傳空字串。解析前需先檢查。  
- **非預期格式** – 若儲存格內容為 `"2023/05/12"`，元號解析器會拋出例外；可能需要備援處理。

## 第三步：使用 C# 寫入 DateTime 至 Excel

取得元號字串後，我們使用 `DateTime.ParseExact` 進行解析。格式 `"ggyy/MM/dd"` 告訴 .NET 期待日本元號（`gg`）、兩位數年份（`yy`）以及月份/日期。

```csharp
        // Step 4: Convert the era date string to a DateTime using the Japanese culture
        DateTime parsedDate;
        try
        {
            parsedDate = DateTime.ParseExact(
                eraDateString,
                "ggyy/MM/dd",
                new CultureInfo("ja-JP"));
        }
        catch (FormatException)
        {
            Console.WriteLine("The cell value does not match the expected Japanese era format.");
            return;
        }

        Console.WriteLine($"Parsed DateTime (UTC): {parsedDate:u}");

        // Step 5: Store the resulting DateTime back into the same cell
        dateCell.PutValue(parsedDate);

        // Optional: Apply a standard date format so Excel shows it nicely
        dateCell.SetStyle(new Style { Number = 14 }); // 14 = "m/d/yyyy"

        // Save the workbook to a new file so we don’t overwrite the original
        wb.Save("EraDates_Converted.xlsx");
        Console.WriteLine("Workbook saved as EraDates_Converted.xlsx");
```

**為什麼使用 `PutValue`**：Aspose.Cells 會自動偵測 .NET 類型，並寫入相對應的 Excel 儲存格類型。傳入 `DateTime` 後會產生真正的 Excel 日期，可在之後的格式設定或公式中使用。

### 邊緣情況與技巧

- **時區** – `DateTime` 物件不含時區資訊。若需要 UTC，可呼叫 `DateTime.SpecifyKind`。  
- **文化備援** – 若預期會有其他文化，請將解析包在輔助函式中，嘗試多個 `CultureInfo` 物件。  
- **效能** – 處理數千列時，請重複使用同一個 `CultureInfo` 實例，而非在每次迴圈中重新建立。

## 第四步：完整可執行範例 – 整合所有步驟

以下為完整、可直接執行的程式。將其複製貼上至 `Program.cs`，確保 `EraDates.xlsx` 與編譯後的二進位檔案同目錄，然後執行 `dotnet run`。

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Load workbook
        Workbook wb = new Workbook("EraDates.xlsx");
        Worksheet ws = wb.Worksheets["Sheet1"];   // Change if your sheet has a different name

        // -------------------------------------------------
        // 1️⃣ Read the Japanese era string from B2
        // -------------------------------------------------
        Cell dateCell = ws.Cells["B2"];
        string eraDateString = dateCell.StringValue?.Trim();

        if (string.IsNullOrEmpty(eraDateString))
        {
            Console.WriteLine("Cell B2 is empty. Nothing to convert.");
            return;
        }

        Console.WriteLine($"Original cell value: {eraDateString}");

        // -------------------------------------------------
        // 2️⃣ Parse the era string into a DateTime
        // -------------------------------------------------
        DateTime parsedDate;
        try
        {
            parsedDate = DateTime.ParseExact(
                eraDateString,
                "ggyy/MM/dd",
                new CultureInfo("ja-JP"));
        }
        catch (FormatException)
        {
            Console.WriteLine("The value does not match the expected Japanese era format (ggyy/MM/dd).");
            return;
        }

        Console.WriteLine($"Parsed DateTime: {parsedDate:u}");

        // -------------------------------------------------
        // 3️⃣ Write the DateTime back into the same cell
        // -------------------------------------------------
        dateCell.PutValue(parsedDate);

        // Apply a friendly date format (e.g., 2023/05/12)
        Style style = wb.CreateStyle();
        style.Number = 14; // Built‑in date format
        dateCell.SetStyle(style);

        // Save the updated workbook
        wb.Save("EraDates_Converted.xlsx");
        Console.WriteLine("Conversion complete – saved as EraDates_Converted.xlsx");
    }
}
```

**Expected output**

```
Original cell value: R3/5/12
Parsed DateTime: 2021-05-12 00:00:00Z
Conversion complete – saved as EraDates_Converted.xlsx
```

當你開啟 `EraDates_Converted.xlsx` 時，儲存格 **B2** 會顯示一般日期（例如 `5/12/2021`），且可像其他日期值一樣在 Excel 計算中使用。

## 專業技巧：打造穩健的 Read Write Excel C# 程式碼

- **寫入前驗證** – 使用 `Cell.IsFormula` 或 `Cell.Type` 以避免不小心覆寫公式。  
- **批次處理** – 若需轉換整欄，遍歷 `ws.Cells.Columns[1]`（B 欄）並套用相同邏輯。  
- **執行緒安全** – Aspose.Cells 物件非執行緒安全；在平行化時，請為每個執行緒建立獨立的 `Workbook` 實例。  
- **日誌記錄** – 於正式腳本中，將 `Console.WriteLine` 換成正式的記錄器（例如 Serilog），以捕捉解析失敗。  
- **測試** – 撰寫單元測試，將已知的元號字串傳入輔助方法，並斷言其產生的 `DateTime` 值。

## 結論

你剛剛已掌握 **read write Excel C#**，學會了 **read excel cell value**、解析日本元號字串，並自信地 **write datetime to excel**。完整範例展示了乾淨的端對端工作流程，可套用於批次作業、不同文化，甚至 Excel 到資料庫的管線。  

接下來可以嘗試將腳本擴展至處理整欄元號日期，或探索 Aspose.Cells 豐富的格式設定功能，以美化輸出儲存格。你也可以試試其他函式庫，如 EPPlus 或 ClosedXML——大部分邏輯相同，僅 API 呼叫不同。  

有任何問題或棘手的 Excel 情境嗎？歡迎在下方留言，祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}