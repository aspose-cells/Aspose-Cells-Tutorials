---
category: general
date: 2026-10-13
description: 學習如何使用 Aspose.Cells 將 Excel 儲存為 TXT。本指南涵蓋將 Excel 匯出為 TXT、寫入儲存格值，以及設定有效位數，只需幾個步驟。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as txt
- export excel to txt
- write value to cell
- set significant digits
- export spreadsheet as txt
language: zh-hant
lastmod: 2026-10-13
og_description: 使用 Aspose.Cells 將 Excel 儲存為 TXT。學習如何將 Excel 匯出為 TXT、寫入儲存格值，以及在僅幾行
  C# 程式碼中設定有效位數。
og_image_alt: Screenshot showing a workbook saved as a TXT file using save excel as
  txt
og_title: 將 Excel 儲存為 TXT – .NET 開發者逐步指南
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to save Excel as TXT with Aspose.Cells. This guide covers
    export Excel to TXT, write value to cell, and set significant digits in just a
    few steps.
  headline: How to save Excel as TXT using Aspose.Cells in C#
  type: TechArticle
- questions:
  - answer: It rounds to the nearest value based on the specified number of significant
      digits, ensuring the output is mathematically accurate to that precision.
    question: Does `SignificantDigits` round or truncate?
  - answer: 'Yes. Replace the file path with a `MemoryStream` instance: `workbook.Save(stream,
      txtOptions);`. This is handy for web APIs that need to return the TXT content
      without touching the file system.'
    question: Can I export directly to a memory stream?
  - answer: 'Use `txtOptions.ExportFormattedValues = true`. This forces Aspose.Cells
      to write the cell’s displayed text rather than the raw value. ## Conclusion
      You now know how to **save Excel as TXT** with full control over precision,
      formatting, and output location. By following the four steps—create a workbo'
    question: What if I need to keep the original formatting (e.g., dates)?
  type: FAQPage
tags:
- Excel
- TXT
- Aspose.Cells
- .NET
title: 如何在 C# 中使用 Aspose.Cells 將 Excel 儲存為 TXT
url: /zh-hant/net/converting-excel-files-to-other-formats/how-to-save-excel-as-txt-using-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.Cells 在 C# 中將 Excel 儲存為 TXT

如果您需要快速 **將 Excel 儲存為 TXT**，本教學會在五分鐘內展示完整流程。您將看到如何將 Excel 匯出為 TXT、將值寫入儲存格，以及設定有效位數，使文字檔正好包含您預期的資料。

將試算表匯出為 TXT 在下游系統僅接受純文字輸入、需要產生日誌，或想要取得計算結果的人類可讀轉儲時非常有用。以下範例適用於 Aspose.Cells v25.10 或更新版本，且可在任何 .NET 6+ 執行環境上執行。

## 前置條件

在開始之前，請確保您已具備：

* 一份 **Aspose.Cells for .NET** 的授權副本（免費試用版可用於測試）。
* 已安裝 .NET 6 SDK 或更新版本。
* 如 Visual Studio 2022、VS Code 或 Rider 等 IDE。
* 基本的 C# 知識——不需要進階的 Excel 自動化經驗。

您可以使用以下指令安裝 Aspose.Cells NuGet 套件：

```bash
dotnet add package Aspose.Cells
```

## 步驟 1：建立工作簿並存取第一個工作表（save excel as txt）

當您想要 **將 Excel 儲存為 TXT** 時，第一步是建立一個 `Workbook` 物件。此物件在記憶體中代表整個 Excel 檔案。

```csharp
using Aspose.Cells;

// Create a new workbook (an empty Excel file)
Workbook workbook = new Workbook();

// Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

> **為何重要：** `Workbook` 類別是所有試算表操作的入口。從全新的工作簿開始，可避免任何隱藏的格式影響純文字輸出。

## 步驟 2：將高精度數字寫入儲存格（write value to cell）

現在您需要 **將值寫入儲存格** A1。`PutValue` 方法會自動偵測資料類型，並以數值形式儲存。

```csharp
// Write a high‑precision number into cell A1
worksheet.Cells["A1"].PutValue(12345.6789012345);
```

> **提示：** 若之後需要寫入字串、日期或公式，仍可使用相同的 `PutValue` 方法——只要傳入相應的 .NET 類型即可。

## 步驟 3：設定匯出選項以保留所需精度（set significant digits）

匯出為 TXT 檔時，通常會想限制位數以減少檔案大小或符合下游規格。`TxtSaveOptions` 類別提供 `SignificantDigits` 屬性以達成此目的。

```csharp
// Configure TXT save options to retain only 6 significant digits
TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
{
    SignificantDigits = 6   // New option in v25.10
};
```

> **為何應設定有效位數：** 若未設定此項，Aspose.Cells 會寫入完整的雙精度值，可能產生如 `12345.6789012345` 的長字串。將 `SignificantDigits = 6` 設為 6 可將輸出裁減為 `12345.7`，符合大多數報告需求。

## 步驟 4：將工作簿匯出為 TXT 檔（export excel to txt）

最後，您透過呼叫 `Workbook.Save` 並傳入先前設定好的選項，即可 **將 Excel 匯出為 TXT**。

```csharp
// Save the workbook as a TXT file using the configured options
string outputPath = @"C:\Temp\LimitedDigits.txt";
workbook.Save(outputPath, txtSaveOptions);
```

程式執行完畢後，`LimitedDigits.txt` 內容如下：

```
12345.7
```

> **結果驗證：** 在任意文字編輯器（如 Notepad、VS Code）開啟檔案，確認僅有六位有效數字，且沒有額外的逗號或 Tab 分隔符。

## 完整、可執行範例

以下是一個獨立的主控台應用程式，您可以直接複製、貼上並立即執行。

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Write a high‑precision number to cell A1
            worksheet.Cells["A1"].PutValue(12345.6789012345);

            // 3️⃣ Set up TXT save options with 6 significant digits
            TxtSaveOptions txtOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                SignificantDigits = 6
            };

            // 4️⃣ Save as TXT
            string path = @"C:\Temp\LimitedDigits.txt";
            workbook.Save(path, txtOptions);

            Console.WriteLine($"Workbook exported to TXT at: {path}");
        }
    }
}
```

**每個區塊的說明**

| Block | Purpose |
|-------|---------|
| `using Aspose.Cells;` | 匯入 Aspose.Cells 命名空間，供 `Workbook`、`Worksheet` 與 `TxtSaveOptions` 使用。 |
| `Workbook workbook = new Workbook();` | 在記憶體中建立一個空的 Excel 工作簿。 |
| `worksheet.Cells["A1"].PutValue(...);` | **write value to cell** A1，寫入雙精度數字。 |
| `TxtSaveOptions` | 設定 **set significant digits** 行為，以控制 TXT 匯出的精度。 |
| `workbook.Save(..., txtOptions);` | 執行 **export excel to txt** 操作，產生純文字檔案。 |

## 邊緣情況與額外提示

| Scenario | How to handle |
|----------|---------------|
| **Large worksheets** (many rows/columns) | 若需要 Unicode 支援，使用 `txtOptions.Encoding = Encoding.UTF8`，並考慮使用 `Workbook.Save(Stream, txtOptions)` 以串流方式寫入檔案，避免大量記憶體使用。 |
| **Custom delimiters** (comma‑separated values) | `TxtSaveOptions` 亦提供 `Separator` 屬性——將其設定為 `','` 即可產生 CSV 風格的輸出，同時仍屬於 TXT 格式。 |
| **Preserving formulas** | 設定 `txtOptions.ExportFormulas = true`，將公式文字寫入而非計算後的值。 |
| **Locale‑specific decimal separators** | 將 `txtOptions.DecimalSeparator` 調整為 `','` 以符合歐洲地區的十進位分隔符。 |
| **Multiple worksheets** | 迭代 `workbook.Worksheets`，對每個工作表呼叫 `Save`，並在檔名中加入工作表名稱。 |

## 常見問題

**Q: `SignificantDigits` 會四捨五入還是截斷？**  
A: 它會根據指定的有效位數四捨五入至最接近的值，確保輸出在該精度下數學上正確。

**Q: 能直接匯出到記憶體串流嗎？**  
A: 可以。將檔案路徑改為 `MemoryStream` 實例：`workbook.Save(stream, txtOptions);`。這對需要回傳 TXT 內容而不觸及檔案系統的 Web API 非常方便。

**Q: 若需保留原始格式（例如日期）該怎麼辦？**  
A: 使用 `txtOptions.ExportFormattedValues = true`。此設定會強制 Aspose.Cells 寫入儲存格顯示的文字，而非原始值。

## 結論

您現在已了解如何 **將 Excel 儲存為 TXT**，並能完整控制精度、格式與輸出位置。依循四個步驟——建立工作簿、**write value to cell**、**set significant digits**，以及 **export Excel to TXT**——即可在任何 .NET 應用程式中整合純文字匯出功能。

接下來，您可以探索相關主題，例如 **export spreadsheet as TXT with custom delimiters**、**convert Excel to CSV**，或 **use Aspose.Cells to generate JSON reports**。這些皆基於本教學示範的核心概念，為您提供跨平台資料交換的多功能工具箱。

祝開發順利！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此技術為基礎。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索替代實作方式。

- [將 Excel 儲存為文字 – 完整 C# 教學：匯出 Excel 為 TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [建立新工作簿並以精確度匯出 Excel 為 TXT](/cells/english/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/)
- [建立新工作簿 – 以完整精度匯出 Excel 為 TXT](/cells/english/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}