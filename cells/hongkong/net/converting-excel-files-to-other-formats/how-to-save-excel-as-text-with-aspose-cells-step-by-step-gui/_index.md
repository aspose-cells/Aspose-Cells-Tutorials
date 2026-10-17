---
category: general
date: 2026-10-10
description: 學習如何在 C# 中使用 Aspose.Cells 將 Excel 儲存為文字檔。本指南涵蓋將 Excel 轉換為 txt、將 XLSX
  匯出為 txt，以及使用完整程式碼從 Excel 建立 txt。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as text
- convert excel to txt
- export xlsx to txt
- create txt from excel
language: zh-hant
lastmod: 2026-10-10
og_description: 使用 Aspose.Cells for .NET 將 Excel 儲存為文字檔。請參考本指南，將 Excel 轉換為 txt、將 XLSX
  匯出為 txt，並使用範例程式碼從 Excel 建立 txt。
og_image_alt: Screenshot of C# code that saves an Excel workbook as a plain‑text file
og_title: 在 C# 中將 Excel 儲存為文字檔 – 完整 Aspose.Cells 教學
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to save Excel as text in C# using Aspose.Cells. This guide
    covers convert Excel to txt, export XLSX to txt, and create txt from Excel with
    full code.
  headline: How to save Excel as text with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to save Excel as text in C# using Aspose.Cells. This guide
    covers convert Excel to txt, export XLSX to txt, and create txt from Excel with
    full code.
  name: How to save Excel as text with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Prerequisites
    text: '* .NET 6.0 or later (the code also works with .NET Framework 4.7.2+). *
      Basic familiarity with C# and Visual Studio (or any .NET IDE). * An active Aspose.Cells
      for .NET license or a free evaluation key. * The Excel file you want to convert
      (`input.xlsx` in the examples).'
  - name: Full runnable program
    text: 'Putting the pieces together, here is a complete, self‑contained console
      application:'
  - name: Verify programmatically
    text: 'You can read the generated file back into memory to confirm that the export
      succeeded:'
  - name: Common edge cases
    text: '| Situation | What to watch for | Recommended fix | |----------------------------------------|---------------------------------------------------|-----------------|
      | Cells contain formulas | The exported value is the **calculated result**,
      not the formula text. | Ensure the workbook is fully calcul'
  - name: What’s next?
    text: '* Try exporting to CSV (`CsvSaveOptions`) for Excel‑compatible comma‑separated
      files. * Explore the `PdfSaveOptions` class to **export Excel to PDF** in a
      single line. * Combine multiple worksheets into one text file by iterating over
      `workbook.Worksheets`.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Text export
title: 如何使用 Aspose.Cells 將 Excel 另存為文字檔 – 步驟教學
url: /zh-hant/net/converting-excel-files-to-other-formats/how-to-save-excel-as-text-with-aspose-cells-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.Cells 將 Excel 儲存為文字 – 步驟說明指南

如果您需要快速 **將 Excel 儲存為文字**，本教學會示範如何在 C# 中使用 Aspose.Cells 完成。您將看到如何 **將 Excel 轉換為 txt**、控制數值精度，以及處理常見的邊緣案例——全部在一個可執行的範例中。

在以下章節中，您將學習完整的工作流程，從安裝函式庫到驗證輸出檔案。無需外部文件說明；所有需要的資訊皆已包含於此。

## 您將能夠達成的目標

* 從磁碟載入任何 `.xlsx` 工作簿。  
* 設定 `TxtSaveOptions` 以限制有效位數的數量。  
* **使用單一 `Save` 呼叫將 XLSX 匯出為 txt**。  
* 了解在 **從 Excel 建立 txt** 時如何排除格式問題。

### 前置條件

* .NET 6.0 或更新版本（程式碼亦相容於 .NET Framework 4.7.2+）。  
* 具備 C# 與 Visual Studio（或任何 .NET IDE）的基本知識。  
* 擁有有效的 Aspose.Cells for .NET 授權或免費評估金鑰。  
* 您想要轉換的 Excel 檔案（範例中的 `input.xlsx`）。

> **專業提示：** 若您打算在伺服器上執行此程式，請將授權檔案存放於安全位置，並於應用程式啟動時載入一次。

## 步驟 1：設定開發環境

1. 建立新的主控台專案：

   ```bash
   dotnet new console -n ExcelToTxtDemo
   cd ExcelToTxtDemo
   ```

2. 新增 Aspose.Cells NuGet 套件：

   ```bash
   dotnet add package Aspose.Cells
   ```

   這會下載最新的穩定版（截至 2026‑10‑10 為 23.9）。

3. （可選）若您有授權檔案，請將 `Aspose.Cells.lic` 放在專案根目錄，並在 `Program.cs` 開頭加入以下程式碼：

   ```csharp
   // Load Aspose.Cells license (required for production use)
   var license = new Aspose.Cells.License();
   license.SetLicense("Aspose.Cells.lic");
   ```

   載入授權可移除評估水印並解除大小限制。

## 步驟 2：載入 Excel 工作簿

第一行功能程式碼會建立一個代表整個 Excel 檔案的 `Workbook` 實例。

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Load the workbook you want to convert
        var workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
        // Continue with export logic...
    }
}
```

**為什麼重要：** `Workbook` 抽象出工作表、儲存格、公式與格式。一次載入檔案即可保持轉換速度快且記憶體使用效率高。

## 步驟 3：設定 TxtSaveOptions 以精確控制位數

當您 **將 Excel 轉換為 txt** 時，數值可能包含許多小數位。`TxtSaveOptions` 讓您將輸出限制為特定的有效位數，這在需要固定寬度文字的下游系統中常見。

```csharp
// Step 3: Create and configure TxtSaveOptions
var txtOptions = new TxtSaveOptions
{
    // Keep only 5 significant digits (e.g., 123.45678 → 123.46)
    SignificantDigits = 5,

    // Optional: Use tab as the delimiter for column separation
    Separator = "\t",

    // Optional: Export only the first worksheet
    ExportActiveWorksheetOnly = true
};
```

**說明：**  
* `SignificantDigits` 會去除浮點噪聲，同時保留大多數商業計算所需的精度。  
* `Separator` 預設為空格；將其設定為 `\t`（tab）可讓產生的檔案更易於匯入資料庫或試算表。  
* `ExportActiveWorksheetOnly` 可防止意外匯出隱藏工作表，避免文字檔過大。

## 步驟 4：使用設定好的選項將 XLSX 匯出為 txt

現在您已具備 **將 Excel 儲存為文字** 所需的一切。`Save` 方法會將純文字表示寫入目標路徑。

```csharp
// Step 4: Save the workbook as a plain‑text file
workbook.Save(@"YOUR_DIRECTORY\output.txt", txtOptions);
Console.WriteLine("Export completed: output.txt");
```

產生的 `output.txt` 會包含以 Tab 分隔的列，每個儲存格皆依您設定的選項以純文字形式呈現。

### 完整可執行程式

將各部份組合起來，以下是一個完整、獨立的主控台應用程式：

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load license if you have one (remove comments if not needed)
        // var license = new License();
        // license.SetLicense("Aspose.Cells.lic");

        // 1️⃣ Load the Excel workbook
        var workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Configure TxtSaveOptions
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5,
            Separator = "\t",
            ExportActiveWorksheetOnly = true
        };

        // 3️⃣ Export XLSX to TXT
        workbook.Save(@"YOUR_DIRECTORY\output.txt", txtOptions);

        Console.WriteLine("✅ Excel workbook successfully saved as text at: output.txt");
    }
}
```

**預期輸出**（主控台）：

```
✅ Excel workbook successfully saved as text at: output.txt
```

**產生的 `output.txt` 範例**（前三列）：

```
Name    Age     Salary
Alice   30      55000
Bob     27      47000
```

數字會四捨五入至五個有效位數，且欄位以 Tab 分隔。

## 步驟 5：驗證輸出並處理邊緣案例

### 以程式方式驗證

您可以將產生的檔案重新讀回記憶體，以確認匯出是否成功：

```csharp
string[] lines = File.ReadAllLines(@"YOUR_DIRECTORY\output.txt");
if (lines.Length > 0)
{
    Console.WriteLine("First line of the txt file:");
    Console.WriteLine(lines[0]);
}
```

### 常見邊緣案例

| 情境                                 | 需注意的地方                                               | 推薦的解決方式 |
|--------------------------------------|-----------------------------------------------------------|----------------|
| 儲存格包含公式                       | 匯出的值是 **計算結果**，而非公式文字。                     | 在儲存前確保工作簿已完整計算 (`workbook.CalculateFormula();`) |
| 日期顯示為序列號                     | Excel 以數字儲存日期，可能看起來像 `44745`。               | 設定 `txtOptions.ConvertDateTime = true;` 以強制使用可讀的日期格式 |
| 大型工作表（>10 000 列）              | 記憶體使用量可能激增。                                     | 使用 `txtOptions.ExportAllSheets = false;` 並逐一處理工作表 |
| Unicode 字元（例如表情符號）          | 預設編碼為 UTF‑8，舊系統可能需要 ANSI。                    | 如有需要，設定 `txtOptions.Encoding = Encoding.GetEncoding("windows-1252");` |

預先考慮這些情境，您即可 **從 Excel 建立 txt** 時在不同資料集上保持可靠。

## 結論

您現在已掌握如何使用 Aspose.Cells for .NET **將 Excel 儲存為文字**，從載入工作簿、設定 `TxtSaveOptions` 到最終 **將 XLSX 匯出為 txt**。此範例示範完整程式路徑，說明每個設定背後的原因，並涵蓋在 **將 Excel 轉換為 txt** 時常見的陷阱。

### 接下來可以做什麼？

* 嘗試使用 `CsvSaveOptions` 匯出為 CSV（Excel 相容的逗號分隔檔案）。  
* 探索 `PdfSaveOptions` 類別，以單行程式碼 **將 Excel 匯出為 PDF**。  
* 透過遍歷 `workbook.Worksheets`，將多個工作表合併成一個文字檔。

歡迎自行實驗各種選項——更改分隔符、精度或工作表選擇，以符合您的特定工作流程。

祝編程愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南技術緊密相關的主題，並提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，或在自己的專案中探索替代實作方式。

- [使用自訂分隔符將 Excel 儲存為文字檔（Aspose.Cells）](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [將 Excel 儲存為 txt – 完整 C# 指南：以有效位數匯出數字](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/)
- [如何使用 Aspose.Cells .NET 將 Excel 檔案儲存為多種格式（2023 指南）](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}