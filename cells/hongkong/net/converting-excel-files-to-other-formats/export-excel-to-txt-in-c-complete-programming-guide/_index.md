---
category: general
date: 2026-08-11
description: 在 C# 中將 Excel 匯出為 txt，提供逐步教學。學習如何使用 Aspose.Cells 將 xlsx 轉換為純文字。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- convert xlsx to plain text
- how to export excel worksheet as text
- export worksheet as text file
language: zh-hant
lastmod: 2026-08-11
og_description: 在 C# 中快速將 Excel 匯出為 txt。本教學示範如何將 xlsx 轉換為純文字、設定格式，並處理大型工作表。
og_image_alt: Code snippet that exports an Excel worksheet to a plain text file using
  C#
og_title: 在 C# 中將 Excel 匯出為 TXT – 開發者逐步指南
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  headline: Export excel to txt in C# – complete programming guide
  type: TechArticle
- description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  name: Export excel to txt in C# – complete programming guide
  steps:
  - name: – load the workbook
    text: '```csharp using Aspose.Cells;'
  - name: – get the first worksheet
    text: '```csharp Worksheet sheet = workbook.Worksheets[0]; ```'
  - name: – define export options for text conversion
    text: '```csharp ExportTableOptions exportOptions = new ExportTableOptions { ExportAsString
      = true, // Export all values as text DateTimeFormat = "yyyy-MM-dd", // Desired
      date format NumberFormat = "#,##0.00" // Desired numeric format }; ```'
  - name: – export worksheet as text file
    text: '```csharp // Apply the options to the worksheet sheet.ExportTableOptions
      = exportOptions;'
  type: HowTo
tags:
- excel
- csharp
- text export
- aspose.cells
title: 在 C# 中將 Excel 匯出為 TXT – 完整程式設計指南
url: /zh-hant/net/converting-excel-files-to-other-formats/export-excel-to-txt-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export excel to txt in C# – 完整程式設計指南

如果你需要 **export excel to txt**，只要幾行 C# 程式碼即可完成。本指南說明如何將 `.xlsx` 工作簿轉換成純文字檔，同時保留你自行定義的資料格式。

將工作表匯出為文字檔是常見需求，尤其在下游系統只接受分隔資料，或是需要稽核原始儲存格值時。接下來的章節將教你如何設定日期與數字格式、處理大型工作表，以及避免常見的陷阱。

## Prerequisites for converting xlsx to plain text

在開始之前，請確保你已具備以下環境：

* 已安裝 .NET 6.0（或更新版本）— 程式碼以 .NET Standard 2.0 為目標，因此同樣支援 .NET Framework 4.6 以上。
* 取得 **Aspose.Cells** 授權（免費評估版可用於測試）。
* 使用 Visual Studio 2022 或 Visual Studio Code 等 IDE。
* 在專案可參考的資料夾中放置名為 `input.xlsx` 的 Excel 檔案。

以上項目即為唯一的外部需求；本教學不依賴其他 NuGet 套件。

## How to export excel to txt using Aspose.Cells

Aspose.Cells 提供 `ExportTableOptions` 類別，讓你控制儲存格值如何以字串形式輸出。將 `ExportAsString` 設為 `true` 後，所有儲存格都會以文字寫入，這對於需要確定性純文字輸出的情境相當重要。

### Step 1 – load the workbook

```csharp
using Aspose.Cells;

string inputPath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(inputPath);
```

*`Workbook` 建構子會將 Excel 檔案讀入記憶體。若檔案不存在會拋出例外，建議在正式環境中將此呼叫包在 try‑catch 區塊內。*

### Step 2 – get the first worksheet

```csharp
Worksheet sheet = workbook.Worksheets[0];
```

*工作表採用零基索引，索引 0 代表第一個分頁。若需指定特定分頁，可改用工作表名稱（`workbook.Worksheets["Sheet1"]`）。*

### Step 3 – define export options for text conversion

```csharp
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,               // Export all values as text
    DateTimeFormat = "yyyy-MM-dd",       // Desired date format
    NumberFormat   = "#,##0.00"          // Desired numeric format
};
```

*`ExportAsString` 確保每個儲存格不論原始類型為何，都會在輸出檔案中變成字串。`DateTimeFormat` 與 `NumberFormat` 屬性則讓你自行決定日期與數字的呈現方式，這在 **convert xlsx to plain text** 時尤為關鍵，因為系統往往要求特定的格式。*

### Step 4 – export worksheet as text file

```csharp
// Apply the options to the worksheet
sheet.ExportTableOptions = exportOptions;

// Export the data to a tab‑delimited text file
string outputPath = @"YOUR_DIRECTORY\Exported.txt";
sheet.ExportDataTable(outputPath);
```

*`ExportDataTable` 會依照你提供的選項，將工作表內容寫入純文字檔。預設分隔符為 Tab (`\t`)。若需其他分隔符，可使用接受 `ExportTableOptions` 實例的重載，並設定 `ExportTableOptions.Separator`。產生的檔案可用任何文字編輯器開啟，或匯入資料庫。*

#### Expected output

假設 `input.xlsx` 內容如下：

| A            | B       | C          |
|--------------|---------|------------|
| 2023‑05‑01   | 1234.5  | Sample text|

使用上述選項匯出的 `Exported.txt` 會是：

```
2023-05-01	1,234.50	Sample text
```

每欄以 Tab 分隔，日期遵循 `yyyy‑MM‑dd` 格式，數字則使用千位分隔符（逗號）與兩位小數。

## Common pitfalls when you export worksheet as text file

| Issue | Why it happens | How to avoid it |
|-------|----------------|-----------------|
| Locale‑dependent number formatting | 預設格式會遵循作業系統語系，可能導致逗號或句點使用不一致。 | 在 `ExportTableOptions` 中明確設定 `NumberFormat`。 |
| Hidden rows or columns appear in the output | Aspose.Cells 會匯出整個使用範圍，包括隱藏的列。 | 設定 `ExportTableOptions.ExportHiddenRows = false` 與 `ExportHiddenColumns = false` 以跳過隱藏項目。 |
| Large worksheets cause memory pressure | 整個工作簿會先載入記憶體再匯出。 | 使用 `Workbook.LoadOptions` 並將 `LoadDataOnly = true` 以降低記憶體使用，或分批處理檔案。 |
| Date cells stored as text in the source file | 若儲存格已是格式化字串，匯出器會視為文字並忽略 `DateTimeFormat`。 | 確保來源工作簿的日期儲存為正確的 Excel 日期類型。 |

解決上述問題後，**how to export excel worksheet as text** 的流程即可在各種環境中穩定執行。

## Extending the solution – custom delimiters and streaming export

若需產生逗號分隔值（CSV）檔案，而非 Tab 分隔檔，可調整選項：

```csharp
exportOptions.Separator = ',';
exportOptions.ExportHiddenRows = false;   // optional
exportOptions.ExportHiddenColumns = false; // optional
sheet.ExportTableOptions = exportOptions;
sheet.ExportDataTable(@"YOUR_DIRECTORY\Exported.csv");
```

對於超過 500 MB 的大型檔案，使用串流輸出可避免耗盡記憶體：

```csharp
using (FileStream stream = new FileStream(@"YOUR_DIRECTORY\LargeExport.txt",
                                          FileMode.Create,
                                          FileAccess.Write,
                                          FileShare.None,
                                          bufferSize: 81920,
                                          useAsync: true))
{
    sheet.ExportDataTable(stream, exportOptions);
}
```

接受 `Stream` 的重載會逐行寫入，非常適合批次工作或直接將文字檔回傳給客戶端的 Web 服務。

## Verify the result programmatically

匯出完成後，你可以讀取第一行回到記憶體，以驗證格式是否正確：

```csharp
string firstLine = File.ReadLines(outputPath).First();
Console.WriteLine($"First line: {firstLine}");
```

執行此程式碼應會印出與 *Expected output* 章節相同的內容，讓你確信轉換成功。

## Recap of the complete code

將所有片段整合後，即成為一個可直接貼到 Console 應用程式的完整程式：

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputPath  = @"YOUR_DIRECTORY\input.xlsx";
        string outputPath = @"YOUR_DIRECTORY\Exported.txt";

        // Load workbook
        Workbook workbook = new Workbook(inputPath);
        Worksheet sheet = workbook.Worksheets[0];

        // Configure export options
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            DateTimeFormat = "yyyy-MM-dd",
            NumberFormat   = "#,##0.00",
            Separator      = '\t' // tab delimiter
        };

        // Apply options and export
        sheet.ExportTableOptions = exportOptions;
        sheet.ExportDataTable(outputPath);

        // Simple verification
        string firstLine = File.ReadLines(outputPath).First();
        Console.WriteLine($"Export completed. First line: {firstLine}");
    }
}
```

編譯並執行程式；`Exported.txt` 會出現在與來源工作簿相同的目錄下。

## Next steps and related topics

* **Export worksheet as text file** – 嘗試不同的分隔符、編碼（UTF‑8 與 ASCII）以及換行樣式，以提升跨平台相容性。
* **Bulk conversion** – 迭代 `workbook.Worksheets`，為每個分頁產生獨立的文字檔。
* **Integration with databases** – 直接將產生的文字檔導入 SQL Server 或 PostgreSQL 的批次插入作業。
* **

## What Should You Learn Next?

以下教學與本指南內容緊密相關，能幫助你進一步掌握 API 功能並探索其他實作方式：

- [How to Export Excel Files in .NET Using Aspose.Cells&#58; A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [How to Export Visible Excel Rows Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}