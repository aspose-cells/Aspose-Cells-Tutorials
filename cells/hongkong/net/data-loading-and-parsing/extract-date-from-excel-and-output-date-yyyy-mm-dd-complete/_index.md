---
category: general
date: 2026-03-18
description: 從 Excel 提取日期並以 ISO 格式 yyyy‑mm‑dd 輸出。學習如何讀取日本元號日期、轉換它們，並在 C# 中顯示 ISO 日期。
draft: false
keywords:
- extract date from excel
- output date yyyy-mm-dd
- display date iso format
language: zh-hant
og_description: 從 Excel 提取日期並以 ISO 格式 yyyy‑mm‑dd 輸出。逐步 C# 教學，附完整程式碼與說明。
og_title: 從 Excel 提取日期 – 在 C# 中輸出 yyyy‑mm‑dd 格式的日期
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: 從 Excel 提取日期並輸出為 yyyy‑mm‑dd – 完整 C# 指南
url: /zh-hant/net/data-loading-and-parsing/extract-date-from-excel-and-output-date-yyyy-mm-dd-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 Excel 提取日期 – 如何以 ISO 格式輸出 yyyy‑mm‑dd 日期

是否曾需要 **extract date from Excel**，卻不確定如何處理日本元號日期或取得乾淨的 `yyyy‑mm‑dd` 字串？你並不孤單。在許多資料遷移專案中，來源活頁簿會使用日本天皇曆儲存日期，而下游系統則期待像 `2024-04-01` 這樣符合 ISO 標準的日期。

在本指南中，我們將一步步示範完整且可執行的解決方案：讀取儲存格、解析日本元號，並 **outputs the date yyyy‑mm‑dd**。完成後，你將清楚知道如何在任何 .NET 應用程式中 **display date ISO format**，同時取得可直接放入專案的可重用程式碼片段。

## 您需要的條件

- **.NET 6+**（或 .NET Framework 4.7.2+）。  
- **Aspose.Cells for .NET** – 讓我們在載入活頁簿時設定自訂曆法的函式庫。  
- 一個 Excel 檔案 (`japan-date.xlsx`) 內含以日本元號儲存的日期（例如 `令和3年4月1日`）。  
- 你慣用的 IDE – Visual Studio、Rider，甚至 VS Code 都可以。

不需要額外的 NuGet 套件，除 Aspose.Cells 之外，程式碼可在 Windows、Linux 或 macOS 上執行。

## 步驟 1：設定專案並安裝 Aspose.Cells

```bash
dotnet new console -n ExcelDateDemo
cd ExcelDateDemo
dotnet add package Aspose.Cells
```

> **小技巧：** 若你在 CI 伺服器上執行，請將套件版本（`Aspose.Cells 23.12`）固定，以確保可重現的建置。

## 步驟 2：以日本天皇曆載入活頁簿

在來源使用非公曆時，**extract date from Excel** 的關鍵是告訴 Aspose.Cells 在載入時套用哪個曆法。我們使用 `LoadOptions.Calendar` 來完成。

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Create load options and set the Japanese Emperor calendar
        LoadOptions loadOptions = new LoadOptions
        {
            // This tells Aspose.Cells to interpret era dates correctly
            Calendar = new JapaneseEmperorCalendar()
        };

        // Step 3: Open the workbook that contains Japanese era dates
        // Replace the path with the actual location of your Excel file
        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);
```

**為什麼這很重要：** 若未設定自訂曆法，Aspose.Cells 會將儲存格視為純文字，導致失去元號資訊。指定 `JapaneseEmperorCalendar` 後，函式庫會在背後自動將 `令和3年4月1日` 轉換為 `2021‑04‑01`。

## 步驟 3：從特定儲存格取得日期

現在活頁簿已能正確解讀元號，我們可以將儲存格讀為 `DateTime`。假設日期位於第一張工作表的 **A1**（第 0 列，第 0 欄）。

```csharp
        // Step 4: Retrieve the date value from the first worksheet, first cell
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0]; // A1

        // GetDateTime() returns a System.DateTime object
        DateTime extractedDate = dateCell.GetDateTime();
```

如果儲存格為空或不是日期值，`GetDateTime()` 會拋出例外。以下是防禦式寫法：

```csharp
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        DateTime extractedDate = dateCell.GetDateTime();
```

**邊緣情況：** 某些舊版 Excel 會以序號（序列日期）儲存日期。Aspose.Cells 會自動處理，但若預期混合內容，仍應檢查儲存格類型。

## 步驟 4：輸出 yyyy‑mm‑dd（ISO）並驗證

取得 `DateTime` 後，將其格式化為 **output date yyyy‑mm‑dd** 只需一行程式碼：

```csharp
        // Step 5: Output the date in ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

對含有 `令和3年4月1日` 的檔案執行程式，會印出：

```
Extracted date (ISO): 2021-04-01
```

這正是許多 API 所要求的 **display date iso format**。

## 完整可執行範例

將所有片段組合起來，以下是一個可直接複製貼上的完整程式：

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook with Japanese era support
        LoadOptions loadOptions = new LoadOptions
        {
            Calendar = new JapaneseEmperorCalendar()
        };

        string filePath = @"YOUR_DIRECTORY\japan-date.xlsx";
        Workbook workbook = new Workbook(filePath, loadOptions);

        // Access the cell that holds the date (A1)
        Worksheet sheet = workbook.Worksheets[0];
        Cell dateCell = sheet.Cells[0, 0];

        // Validate the cell contains a date
        if (dateCell.Type != CellValueType.IsDateTime)
        {
            Console.WriteLine("The target cell does not contain a valid date.");
            return;
        }

        // Extract the DateTime value
        DateTime extractedDate = dateCell.GetDateTime();

        // Convert to ISO format (yyyy‑mm‑dd)
        string isoDate = extractedDate.ToString("yyyy-MM-dd");
        Console.WriteLine($"Extracted date (ISO): {isoDate}");
    }
}
```

> **注意：** 請將 `YOUR_DIRECTORY` 替換為實際放置 `japan-date.xlsx` 的資料夾路徑。程式碼可支援任意工作表與儲存格，只需調整索引即可。

## 處理其他曆法（可選）

若需要 **extract date from Excel** 時使用泰國佛曆或希伯來曆，只要交換曆法實例即可：

```csharp
loadOptions.Calendar = new ThaiBuddhistCalendar();   // for Thai dates
// or
loadOptions.Calendar = new HebrewCalendar();         // for Hebrew dates
```

其餘邏輯保持不變，展示了此方法的彈性。

## 常見問題與避免方式

| 問題 | 發生原因 | 解決方法 |
|------|----------|----------|
| `GetDateTime()` 拋出 `InvalidCastException` | 儲存格不是日期（可能是字串） | 呼叫前檢查 `Cell.Type`，或對 `Cell.StringValue` 使用 `DateTime.TryParse`。 |
| 轉換後年份錯誤 | 載入活頁簿時未設定 `Calendar` | 開啟檔案前，務必使用正確的曆法建立 `LoadOptions`。 |
| ISO 輸出顯示時間部分（`2021-04-01 00:00:00`） | 使用 `ToString()` 而未指定格式字串 | 使用 `"yyyy-MM-dd"` 格式字串以強制 **output date yyyy‑mm‑dd**。 |
| 找不到檔案 | 相對路徑指向錯誤資料夾 | 使用 `Path.Combine(Environment.CurrentDirectory, "japan-date.xlsx")` 或提供絕對路徑。 |

## 產品化程式碼的小技巧

1. **Cache the workbook** 若需從同一檔案讀取多筆日期，請快取活頁簿——開啟活頁簿的成本相對較高。  
2. **Wrap the extraction logic** 成為可重用的方法：

   ```csharp
   static string ExtractIsoDate(string file, int sheetIdx, int row, int col)
   {
       var opts = new LoadOptions { Calendar = new JapaneseEmperorCalendar() };
       var wb = new Workbook(file, opts);
       var cell = wb.Worksheets[sheetIdx].Cells[row, col];
       if (cell.Type != CellValueType.IsDateTime) return null;
       return cell.GetDateTime().ToString("yyyy-MM-dd");
   }
   ```

3. **Log the original era string** (`cell.StringValue`) 連同 ISO 輸出一起記錄，以作稽核。  
4. **Unit test** 此方法，使用包含不同元號（平成、令和）的硬編碼 Excel 檔案，確保正確性。

## 視覺概覽

以下是一張快速示意圖，說明資料流向——從 Excel 儲存格到 ISO 字串。

![從 Excel 提取日期範例圖示，顯示 Excel → LoadOptions → DateTime → ISO string]  

*Alt text: 「extract date from excel」圖示，展示轉換流程。*

## 結論

我們已說明如何 **extract date from Excel**、處理日本元號值，並 **output date yyyy‑mm‑dd**，使其符合現代 API 常用的 **display date iso format**。此解決方案自包含、相容任何支援 Aspose.Cells 的 .NET 版本，且只需一行程式碼即可擴充至其他曆法。

有其他曆法需求嗎？或是需要從多欄位抓取日期？歡迎自行調整 `ExtractIsoDate` 輔助函式或在下方留言。祝開發順利，願你的日期永遠保持完美的 ISO 同步！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}