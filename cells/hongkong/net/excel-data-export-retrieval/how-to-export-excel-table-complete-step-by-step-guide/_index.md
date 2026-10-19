---
category: general
date: 2026-07-03
description: 學習如何使用 C# 將 Excel 表格匯出為 .txt 檔案，並將 Excel 表格儲存為 .txt 檔。提供完整程式碼範例，將 Excel
  資料匯出為純文字。
draft: false
keywords:
- how to export excel table
- save excel table to .txt file
- export excel data as plain text
- Aspose.Cells export table
- C# Excel to text
language: zh-hant
og_description: 如何將 Excel 表格匯出為純文字。本指南說明如何將 Excel 資料匯出為純文字，並使用 Aspose.Cells 將 Excel
  表格儲存為 .txt 檔案。
og_title: 如何匯出 Excel 表格 – 完整 C# 教學
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to export Excel table to a .txt file and save Excel table
    to .txt file using C#. Export Excel data as plain text with full code example.
  headline: How to Export Excel Table – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- File I/O
title: 如何匯出 Excel 表格 – 完整逐步指南
url: /zh-hant/net/excel-data-export-retrieval/how-to-export-excel-table-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何匯出 Excel 表格 – 完整步驟指南

有沒有想過 **how to export Excel table** 而不需要將整個工作簿載入記憶體？你並不是唯一有此疑問的人。在許多自動化工作中，下游系統只接受簡單的 `.txt` 檔案，因此你需要快速且可靠地 **save Excel table to .txt file**。

在本教學中，我們將逐步說明一個乾淨的 C# 解決方案，使用 Aspose.Cells **exports Excel data as plain text**。完成後，你將擁有一個可直接執行的程式，了解每一行程式碼的意義，並學會如何為自己的特殊情況微調匯出。

## 你需要的條件

- **Aspose.Cells for .NET**（任何較新版本，例如 23.12）。
- .NET 6 SDK 或更新版本 – 程式碼同樣可在 .NET Core 上編譯。
- 一個包含至少一個 Excel 表格的範例 `input.xlsx`。
- 文字編輯器或 IDE（Visual Studio、VS Code、Rider … 隨你挑選）。

不需要除 Aspose.Cells 之外的其他 NuGet 套件，且整個程式可在 Windows、Linux 或 macOS 上執行。

## 步驟 1：設定專案與引用

首先，建立一個 console 應用程式，並將必要的命名空間匯入。

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTableExport
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the export logic here.
        }
    }
}
```

> **專業提示：** 若使用 .NET CLI，請執行 `dotnet new console -n ExcelTableExport`，然後在貼上上述程式碼前執行 `dotnet add package Aspose.Cells`。

## 步驟 2：載入工作簿並取得第一個工作表

Workbook 物件代表整個 Excel 檔案。只載入一次即可降低記憶體使用量。

```csharp
// Step 2: Load the workbook and get the first worksheet
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = wb.Worksheets[0];
```

為什麼選擇第一個工作表？在許多自動產生的報告中，資料位於第一張工作表，但你可以更改索引，或使用 `wb.Worksheets["SheetName"]` 來指定名稱工作表。

## 步驟 3：取得工作表上定義的第一個表格

Excel 表格（ListObjects）提供結構化資料，使匯出更具可預測性。

```csharp
// Step 3: Retrieve the first table defined on the worksheet
Table tbl = ws.Tables[0];
```

如果工作簿包含多個表格，只需遍歷 `ws.Tables` 或依 `tbl.Name` 取得特定表格。

## 步驟 4：設定匯出選項 – 將每個儲存格匯出為字串

Aspose.Cells 允許在匯出時控制每個儲存格的格式。設定 `ExportAsString` 可確保數字、日期與公式皆以純文字形式匯出。

```csharp
// Step 4: Set up export options – export every cell as a string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true
};
```

### 新增自訂匯出動作以修剪空白字元

來源資料常常包含前置或後置空白。修剪這些空白可讓最終的 `.txt` 檔案更整潔。

```csharp
// Define a custom export action to trim cell values before writing
exportOptions.CustomExport = (cell, writer) =>
{
    writer.Write(cell.StringValue.Trim());
};
```

此 lambda 會接收 `Cell` 物件與 `TextWriter`。你也可以在此加入條件邏輯，例如將逗號替換為分號以產生 CSV 風格的輸出。

## 步驟 5：從 A1 儲存格開始匯出表格至文字檔

現在我們實際將表格寫入磁碟。`ExportTable` 方法會逐列走訪表格，套用剛才定義的選項。

```csharp
// Step 5: Export the table starting at cell A1 to a text file
using (StreamWriter writer = new StreamWriter("YOUR_DIRECTORY/Table.txt"))
{
    ws.Cells.ExportTable(tbl, "A1", exportOptions, writer);
}
```

**你會看到：**Excel 表格的每一列會變成 `Table.txt` 中的一行。預設情況下，欄位以制表符 (`\t`) 分隔，非常適合下游解析。

### 預期輸出範例

假設 `input.xlsx` 包含一個有三個欄位（`ID`、`Name`、`Score`）且有兩筆資料列的表格，`Table.txt` 會如下所示：

```
1    Alice    85
2    Bob      92
```

請注意空格已被修剪，且所有內容皆為純文字——正是 **export excel data as plain text** 所要求的。

## 處理常見的邊緣案例

| Situation | What to Do | Why |
|-----------|------------|-----|
| **表格有空白儲存格** | lambda 寫入 `cell.StringValue.Trim()`，對於空白儲存格會回傳空字串。 | 保持欄位對齊，且不會加入不必要的字元。 |
| **需要自訂分隔符** | 將 `writer.Write(cell.StringValue.Trim());` 改為 `writer.Write($"{cell.StringValue.Trim()},");`，並在每列結尾修剪多餘的分隔符。 | 某些系統偏好使用逗號或管道符號而非制表符。 |
| **大型工作表（> 100 k 列）** | 使用 `ExportTableOptions` 並將 `ExportAsString = true`，如範例所示以串流方式寫入檔案；Aspose.Cells 以串流方式處理列，避免記憶體不足錯誤。 | 確保可擴充性。 |
| **同一工作表內有多個表格** | 遍歷 `ws.Tables`，對每個表格呼叫 `ExportTable`，必要時在匯出之間加入分隔線。 | 讓你能對每個表格 **save Excel table to .txt file**。 |

## 完整範例程式

以下是完整程式碼，可直接複製貼上至 `Program.cs`。將 `YOUR_DIRECTORY` 替換為你機器上存在的絕對或相對路徑。

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTableExport
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
            Worksheet ws = wb.Worksheets[0];

            // Get first table
            if (ws.Tables.Count == 0)
            {
                Console.WriteLine("No tables found on the first worksheet.");
                return;
            }
            Table tbl = ws.Tables[0];

            // Configure export options
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                CustomExport = (cell, writer) =>
                {
                    // Trim whitespace and write value
                    writer.Write(cell.StringValue.Trim());
                }
            };

            // Export to text file
            string outputPath = "YOUR_DIRECTORY/Table.txt";
            using (StreamWriter writer = new StreamWriter(outputPath))
            {
                ws.Cells.ExportTable(tbl, "A1", exportOptions, writer);
            }

            Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

使用 `dotnet run` 執行程式。若環境設定正確，你會看到確認訊息，且會產生一個全新的 `Table.txt`，其中包含 **export excel data as plain text**。

## 加分項：視覺確認（可選）

如果想快速檢視產生的檔案畫面，可在任何文字編輯器中開啟。以下是一張佔位圖，顯示預期的版面配置。

![how to export excel table screenshot](https://example.com/images/export-excel-table.png "how to export excel table")

*Alt text:* **how to export excel table** – 顯示匯出 Excel 表格的純文字輸出。

## 重點回顧與後續步驟

我們已完整說明使用 Aspose.Cells **how to export Excel table** 所需的所有步驟，從載入工作簿、修剪儲存格值，到最終寫入乾淨的 `.txt` 檔案。

- 你現在了解如何使用自訂邏輯 **save Excel table to .txt file**。
- 你可以調整 lambda 以處理日期、數字或自訂分隔符。
- 對於較大的專案，建議將此邏輯封裝成可重用的方法或類別。

**接下來要做什麼？** 嘗試匯出多個表格，或透過更改分隔符將輸出格式改為 CSV。你也可以探索將 **export excel data as plain text** 直接寫入網路串流，以支援即時整合。

有任何問題或遇到卡關嗎？留下評論，我們祝你寫程式愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並在此基礎上延伸。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [How to Export Excel Files in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [How to Export Visible Excel Rows Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [How to Combine Excel Sheets into a Single Text File Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/combine-excel-sheets-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}